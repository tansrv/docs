## Stop the server

Before upgrading, you need to stop the server first.

```shell
sudo /etc/init.d/tanserver stop
```

## Download the latest version

```shell
git clone https://github.com/tansrv/tanserver.git
```

## Update

```shell linenums="1"
cd tanserver/src/core/build/
cmake .. && make && make install
```

!!! note
    The above update will not overwrite the APIs you have already written.

## Check the version

```shell
sudo /etc/init.d/tanserver version
```
