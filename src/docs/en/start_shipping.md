## Edit configuration file

Edit `/etc/tanshipper.conf`

``` linenums="1"
#x.x.x.x:1117
#z.z.z.z:1117
```

Add connection information (IP address:port), cannot contain spaces.

## Start shipping

```shell
sudo /etc/init.d/tanshipper start
```

!!! note
    The client IP address should be in the server's `allowlist`.

## Check log files

Directory: `/usr/local/tanshipper/logs/`

## Restart and apply the new configuration

```shell
sudo /etc/init.d/tanshipper restart
```
