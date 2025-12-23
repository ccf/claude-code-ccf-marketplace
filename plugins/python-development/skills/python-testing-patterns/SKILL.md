---
name: python-testing-patterns
description: Comprehensive testing strategies with pytest, fixtures, mocking, and TDD.

summary: |
  - pytest: `pytest -v`, `pytest -k "test_name"`, `pytest --cov`
  - Fixtures: `@pytest.fixture` for setup, `conftest.py` for shared
  - Mocking: `unittest.mock.patch`, `@patch('module.function')`
  - Parametrize: `@pytest.mark.parametrize("input,expected", [...])`
  - AAA pattern: Arrange → Act → Assert

context_cost: high
load_when:
  - "python testing"
  - "pytest"
  - "test fixtures"
  - "mocking python"
  - "tdd python"

enhances:
  - async-python-patterns
  - python-packaging
---

# Python Testing Patterns

pytest-based testing for Python applications.

## When to Use

- Writing unit tests for Python code
- Setting up test suites and infrastructure
- Implementing test-driven development (TDD)
- Mocking external dependencies
- Testing async code

## Quick Start

```python
# test_example.py
def test_add():
    """Basic test with AAA pattern."""
    # Arrange
    a, b = 2, 3
    
    # Act
    result = a + b
    
    # Assert
    assert result == 5
```

```bash
# Run tests
pytest -v                    # Verbose output
pytest -k "test_add"         # Run matching tests
pytest --cov=src --cov-report=html  # Coverage
```

## Fixtures

```python
# conftest.py (shared fixtures)
import pytest

@pytest.fixture
def user():
    """Create a test user."""
    return {"id": 1, "name": "Test User", "email": "test@example.com"}

@pytest.fixture
def db_session():
    """Database session with rollback."""
    session = create_session()
    yield session
    session.rollback()
    session.close()

# test_user.py
def test_user_name(user):
    assert user["name"] == "Test User"
```

## Parametrization

```python
import pytest

@pytest.mark.parametrize("input,expected", [
    (2, 4),
    (3, 9),
    (4, 16),
    (-2, 4),
])
def test_square(input, expected):
    assert input ** 2 == expected
```

## Mocking

```python
from unittest.mock import patch, MagicMock

# Patch a module function
@patch('myapp.services.external_api.fetch')
def test_service(mock_fetch):
    mock_fetch.return_value = {"data": "mocked"}
    result = my_service.get_data()
    assert result["data"] == "mocked"
    mock_fetch.assert_called_once()

# Mock an object method
def test_with_mock():
    mock_client = MagicMock()
    mock_client.get.return_value = {"status": "ok"}
    
    result = process_with_client(mock_client)
    
    mock_client.get.assert_called_with("/api/status")
```

## Async Testing

```python
import pytest

@pytest.mark.asyncio
async def test_async_function():
    result = await async_fetch_data()
    assert result is not None

@pytest.fixture
async def async_client():
    async with AsyncClient() as client:
    yield client
```

## Markers

```python
import pytest

@pytest.mark.slow
def test_slow_operation():
    """Run with: pytest -m slow"""
    pass

@pytest.mark.skip(reason="Not implemented")
def test_future_feature():
    pass

@pytest.mark.xfail(reason="Known bug")
def test_known_failure():
    assert False
```

## Commands

```bash
pytest -v                     # Verbose
pytest -x                     # Stop on first failure
pytest --lf                   # Run last failed
pytest -n auto                # Parallel (pytest-xdist)
pytest --cov=src              # Coverage
pytest --cov-fail-under=80    # Fail if < 80%
```

---

*For fixture patterns, see [fixtures.md](./fixtures.md)*
*For mocking examples, see [mocking.md](./mocking.md)*
