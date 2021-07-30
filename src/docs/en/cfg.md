## server

| Option               | Description | Default         | Availability
| :----                | :----       | :----           | :----
| listen               | Listen port | `2579`          | 1.0.0+
| client_max_body_size | None        | `16384` (bytes) | 2.0.0+
| request_timeout      | None        | `60` (seconds)  | 1.0.0+

---

## ssl

| Option               | Description      | Default    | Availability
| :----                | :----            | :----      | :----
| ssl_cert_file        | Certificate path | `cert.pem` | 1.0.0+
| ssl_key_file         | Private key path | `cert.key` | 1.0.0+

---

## database

### pgsql

| Option               | Description                | Default     | Availability
| :----                | :----                      | :----       | :----
| hostaddr             | Database server IP address | `127.0.0.1` | 1.0.0+
| port                 | Listen port                | `5432`      | 1.0.0+
| user                 | User                       | `postgres`  | 1.0.0+
| password             | Password                   | `postgres`  | 1.0.0+
| database             | Database                   | `postgres`  | 1.0.0+

---

## log

| Option               | Description   | Default               | Availability
| :----                | :----         | :----                 | :----
| directory            | Log file path | `/var/log/tanserver/` | 1.0.0+

### shipper

| Option               | Description         | Default     | Availability |
| :----                | :----               | :----       | :---- |
| listen               | Listen port         | `1117`      | 1.0.0+ |
| hostname             | Host name           | `tanserver` | 1.0.0+ |
| allowlist            | Client IP addresses | None        | 1.0.0+ |

!!! note
    The `hostname` of each server should be inconsistent.
