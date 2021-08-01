## Import `tanserver` module

```python
from tanserver import *
```

## Database

| Declaration         | pg_query(hostaddr, query, *args)
| :------             | :------
| Description         | Do a database query and get the first field of the first row.
| Param `hostaddr`    | Database server IP address. Edit in `/etc/tanserver.conf`.
| Param `query`       | SQL statement, use `$1`, `$2`, `$3`... to replace variable arguments.
| Param `*args`       | Variable arguments, only supports string.
| Exception           | When an error occurs, the cause will be automatically written in the log file.
| Return              | The first field of the first row or an empty string.
| Availability        | 2.0.0+
| Examples            | [login_register](../examples/#api-login_register)&emsp;[get_items](../examples/#api-get_items)&emsp;[transaction](../examples/#api-transaction)

## JSON

| Declaration         | json_append_status(json_string, status_code, message)
| :------             | :------
| Description         | Appends status code and message to a JSON string.
| Param `json_string` | The JSON string to be processed.
| Param `status_code` | The specified status code.
| Param `message`     | The specified message.
| Return              | For example: `{"status":200,"message":"OK","result":$json_string}`
| Availability        | 2.0.0+
| Example             | [append_status](../examples/#api-append_status)
