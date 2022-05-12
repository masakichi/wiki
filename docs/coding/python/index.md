# Python

## Packaging

See [Poetry](poetry.md) for more information.

## Testing

### Using testing data

```python
@pytest.mark.parametrize("hostname,expected", [('localhost', True), ('no-such-hostname.omnia', False)])
def test_hostname_resolvable(hostname, expected):
    assert hostname_resolvable(hostname) == expected
```

### Patch & mock

- Mock decorator [https://stackoverflow.com/a/43213188](https://stackoverflow.com/a/43213188)
- Fixture & Patch order in py.test [https://stackoverflow.com/a/51890193](https://stackoverflow.com/a/51890193)

```python
from unittest import mock

@mock.patch('my.module.my.class')
def test_my_code(mocked_class, my_fixture):
```

```python
@pytest.mark.parametrize("tenant_id,http_status", [('abc', '201 Created'), ('def', '409 Conflict')])
@patch('app.views.deployments.get_cluster_metadata')
@patch('app.views.deployments.get_existing_deployment_names')
def test_create_deployment_with_conflicting_deleted_deployment_name(mock_get_existing_deployment_names, mock_get_cluster_metadata, tenant_id, http_status, client, monkeypatch):
```

- Patch builtins.open

===! "Context Manager"

    ```python
    from unittest.mock import patch, mock_open
    with patch("builtins.open", mock_open(read_data="data")) as mock_file:
        assert open("path/to/open").read() == "data"
    mock_file.assert_called_with("path/to/open")
    ```

=== "Decorator"

    ```python
    @patch("builtins.open", new_callable=mock_open, read_data="data")
    def test_patch(mock_file):
        assert open("path/to/open").read() == "data"
        mock_file.assert_called_with("path/to/open")
    ```

Ref: [mocking - How do I mock an open used in a with statement (using the Mock framework in Python)? - Stack Overflow](https://stackoverflow.com/questions/1289894/how-do-i-mock-an-open-used-in-a-with-statement-using-the-mock-framework-in-pyth)

## Links

- [The Python Standard Library](https://docs.python.org/3/library/index.html)
- [Ship better Python software, faster](https://pythonspeed.com/)
- [Python Mock Gotchas - Alex Marandon](https://alexmarandon.com/articles/python_mock_gotchas/)
