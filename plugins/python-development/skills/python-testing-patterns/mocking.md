# Python Mocking Patterns

## Basic Mocking

```python
from unittest.mock import Mock, MagicMock, patch

# Create a mock
mock = Mock()
mock.return_value = 42
assert mock() == 42

# Configure responses
mock.method.return_value = "result"
mock.method.side_effect = ValueError("error")
mock.method.side_effect = [1, 2, 3]  # Sequential returns
```

## Patching

```python
# Patch as decorator
@patch('module.ClassName')
def test_class(MockClass):
    instance = MockClass.return_value
    instance.method.return_value = "mocked"

    result = function_that_uses_class()
    assert result == "mocked"

# Patch as context manager
def test_with_context():
    with patch('module.function') as mock_func:
        mock_func.return_value = 42
        result = code_that_calls_function()
        assert result == 42

# Patch object attribute
@patch.object(TargetClass, 'method')
def test_method(mock_method):
    mock_method.return_value = "patched"
```

## Where to Patch

```python
# IMPORTANT: Patch where it's USED, not where it's DEFINED

# mymodule.py
from external_lib import api_call

def my_function():
    return api_call()

# test_mymodule.py
# CORRECT: patch where it's imported
@patch('mymodule.api_call')
def test_my_function(mock_api):
    mock_api.return_value = "mocked"
    result = my_function()
    assert result == "mocked"

# WRONG: patching the original location
@patch('external_lib.api_call')  # Won't work!
def test_wrong(mock_api):
    pass
```

## Assertions

```python
mock = Mock()

# Call assertions
mock("arg1", key="value")

mock.assert_called()
mock.assert_called_once()
mock.assert_called_with("arg1", key="value")
mock.assert_called_once_with("arg1", key="value")

# Check call count and history
assert mock.call_count == 1
assert mock.call_args == (("arg1",), {"key": "value"})
assert mock.call_args_list == [call("arg1", key="value")]
```

## Spec and Autospec

```python
from unittest.mock import create_autospec

class RealClass:
    def method(self, arg: str) -> int:
        pass

# Create mock with same interface
mock = create_autospec(RealClass)
mock.method.return_value = 42

# This will raise AttributeError
# mock.nonexistent_method()

# With patch
@patch('module.RealClass', autospec=True)
def test_with_spec(MockClass):
    instance = MockClass.return_value
    instance.method.return_value = 42
```

## Mocking External Services

```python
import responses
import requests

# Mock HTTP requests with responses library
@responses.activate
def test_api_call():
    responses.add(
        responses.GET,
        "https://api.example.com/data",
        json={"key": "value"},
        status=200,
    )

    result = requests.get("https://api.example.com/data")
    assert result.json()["key"] == "value"

# Mock with httpretty
import httpretty

@httpretty.activate
def test_http():
    httpretty.register_uri(
        httpretty.GET,
        "https://api.example.com/data",
        body='{"key": "value"}',
    )
    result = requests.get("https://api.example.com/data")
    assert result.json()["key"] == "value"
```

## Async Mocking

```python
from unittest.mock import AsyncMock

# Create async mock
async_mock = AsyncMock()
async_mock.return_value = "async result"

async def test_async():
    result = await async_mock()
    assert result == "async result"

# Patch async function
@patch('module.async_function', new_callable=AsyncMock)
async def test_patched_async(mock_func):
    mock_func.return_value = "mocked"
    result = await code_that_awaits()
    assert result == "mocked"
```

## Property Mocking

```python
class MyClass:
    @property
    def data(self):
        return fetch_expensive_data()

# Mock property
with patch.object(MyClass, 'data', new_callable=PropertyMock) as mock_data:
    mock_data.return_value = "mocked data"
    obj = MyClass()
    assert obj.data == "mocked data"
```

## Freezing Time

```python
from freezegun import freeze_time
from datetime import datetime

@freeze_time("2024-01-15 12:00:00")
def test_time_dependent():
    assert datetime.now() == datetime(2024, 1, 15, 12, 0, 0)

# As context manager
def test_time_context():
    with freeze_time("2024-06-01"):
        assert datetime.now().month == 6
```
