## Install tanserver

=== "RedHat / CentOS 7+"

    ```shell linenums="1"
    git clone https://github.com/tansrv/tanserver.git
    cd tanserver/install
    chmod +x yum-install.sh && sudo ./yum-install.sh
    ```

=== "Debian 9+ / Ubuntu 16+"

    ```shell linenums="1"
    git clone https://github.com/tansrv/tanserver.git
    cd tanserver/install
    chmod +x apt-install.sh && sudo ./apt-install.sh
    ```

=== "Arch"

    ```shell linenums="1"
    git clone https://github.com/tansrv/tanserver.git
    cd tanserver/install
    chmod +x pacman-install.sh && sudo ./pacman-install.sh
    ```

!!! bug
    If there is a problem during installation, please create an [issue](https://github.com/tansrv/tanserver/).
