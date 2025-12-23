# Pytest Fixtures

Advanced fixture patterns for Python testing.

## Fixture Scopes

```python
import pytest

@pytest.fixture(scope="function")  # Default: new for each test
def per_test_resource():
    return create_resource()

@pytest.fixture(scope="class")  # Shared within test class
def per_class_resource():
    return create_resource()

@pytest.fixture(scope="module")  # Shared within module
def per_module_resource():
    return create_resource()

@pytest.fixture(scope="session")  # Shared across all tests
def per_session_resource():
    return create_expensive_resource()
```

## Factory Fixtures

```python
@pytest.fixture
def user_factory():
    """Factory for creating users with custom attributes."""
    def _create_user(**kwargs):
        defaults = {
            "id": 1,
            "name": "Test User",
            "email": "test@example.com",
            "active": True,
        }
        return {**defaults, **kwargs}
    return _create_user

def test_active_user(user_factory):
    user = user_factory(active=True)
    assert user["active"] is True

def test_inactive_user(user_factory):
    user = user_factory(active=False, name="Inactive")
    assert user["active"] is False
```

## Database Fixtures

```python
@pytest.fixture(scope="session")
def db_engine():
    """Create test database engine."""
    engine = create_engine("sqlite:///:memory:")
    Base.metadata.create_all(engine)
    yield engine
    engine.dispose()

@pytest.fixture
def db_session(db_engine):
    """Create session with transaction rollback."""
    connection = db_engine.connect()
    transaction = connection.begin()
    session = Session(bind=connection)
    
    yield session
    
    session.close()
    transaction.rollback()
    connection.close()
```

## Async Fixtures

```python
import pytest_asyncio

@pytest_asyncio.fixture
async def async_client():
    """Async HTTP client fixture."""
    async with httpx.AsyncClient() as client:
        yield client

@pytest_asyncio.fixture(scope="session")
async def database():
    """Async database connection."""
    db = await Database.connect(TEST_DATABASE_URL)
    yield db
    await db.disconnect()
```

## Parametrized Fixtures

```python
@pytest.fixture(params=["mysql", "postgresql", "sqlite"])
def database_url(request):
    """Run tests against multiple databases."""
    urls = {
        "mysql": "mysql://localhost/test",
        "postgresql": "postgresql://localhost/test",
        "sqlite": "sqlite:///:memory:",
    }
    return urls[request.param]

def test_connection(database_url):
    # This test runs 3 times, once per database
    engine = create_engine(database_url)
    assert engine.connect()
```

## Fixture Dependencies

```python
@pytest.fixture
def config():
    return {"api_key": "test-key", "timeout": 30}

@pytest.fixture
def api_client(config):
    """Depends on config fixture."""
    return APIClient(**config)

@pytest.fixture
def authenticated_client(api_client, user):
    """Depends on both api_client and user."""
    api_client.authenticate(user)
    return api_client
```

## Cleanup with yield

```python
@pytest.fixture
def temp_directory():
    """Create and cleanup temp directory."""
    import tempfile
    import shutil
    
    path = tempfile.mkdtemp()
    yield path
    shutil.rmtree(path)

@pytest.fixture
def mock_server():
    """Start and stop mock server."""
    server = MockServer()
    server.start()
    yield server
    server.stop()
```

## conftest.py Organization

```
tests/
├── conftest.py           # Shared fixtures
├── unit/
│   ├── conftest.py       # Unit test fixtures
│   └── test_services.py
├── integration/
│   ├── conftest.py       # Integration fixtures
│   └── test_api.py
└── e2e/
    ├── conftest.py       # E2E fixtures
    └── test_flows.py
```

```python
# tests/conftest.py
import pytest

@pytest.fixture(autouse=True)
def reset_environment():
    """Runs before each test automatically."""
    os.environ.clear()
    os.environ.update(TEST_ENV)
    yield
    os.environ.clear()
```

