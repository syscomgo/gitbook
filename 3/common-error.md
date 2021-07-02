# Common error

## 1. Using MySQL database, 500 Internal Server Error appears

Similar error messages are as follows:

* populate\(\) isn't reentrant
* MySQLdb.\_exceptions.OperationalError: \(2059, NULL\)

### Solution:

Because Django does not currently support the caching\_sha2\_password encryption method of mysql8.0, it needs to be modified to the mysql\_native\_password encryption method.

Open the mysql command window and enter the command：

```text
ALTER USER '<USER>'@'localhost' IDENTIFIED BY '<USER>' PASSWORD EXPIRE NEVER;
```

Update password

```text
ALTER USER '<USER>'@'localhost' IDENTIFIED WITH mysql_native_password BY '<PASS>';
```

Restart the service after modification

