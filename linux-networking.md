# Networking in a Linux Container in Docker

([Back to Home](README.md))

Some tips to help with Networking in a Linux container in Docker.

## Docker Networking

-   [Docker Networking Crash Course](https://www.youtube.com/watch?v=OU6xOM0SE4o)
-   [How Linux processes your network packet](https://www.youtube.com/watch?v=3Ij0aZRsw9w)

## Docker Networking Commands

-   List all networks: `docker network ls`
-   Remove a network: `docker network rm <network_id>`
-   Learn more details about a network: `docker network inspect <network_id>`
-   Create a network: `docker network create <network_name>`
    -   Many flags can be added optionally added, like `--subnet 10.0.3.0/24`
-   Connect a network to a container: `docker network connect <network_id/name> <container_id/name>`
-   Disconnect a network from a container: `docker network disconnect <network_id/name> <container_id/name>`
-   `docker container run --cap-add=NET_ADMIN -it -v "%cd%":/mnt --name kali kalilinux/kali-rolling`
    -   [Giving network privileges to the container](https://unix.stackexchange.com/questions/459206/list-ip-tables-in-docker-container)
    -   [Giving all privileges to the container](https://stackoverflow.com/questions/36425230/privileged-containers-and-capabilities)
    -   [Docker Networking Crash Course](https://www.youtube.com/watch?v=OU6xOM0SE4o)
-   Execute a Bash terminal and enter into the container: `docker container exec -it <container_id/name> bash`

## Linux Container Commands

> NOTE:
>
> -   Extrapolate these commands for other Linux distros.
> -   `sudo` might have to be used before some commands.

#### Distro Updates

-   `apt-get update` (One might have to run this randomly as well.)
-   `apt-get upgrade`

#### Utility Packages

```shell
$ apt-get install -y vim git man
```

#### Networking Packages

```shell
$ apt-get install -y iputils-ping inetutils-traceroute iproute2 dnsutils net-tools tcpdump wireshark curl
```

> NOTE:
>
> -   `iputils-ping` for `ping`
> -   `inetutils-traceroute` for `traceroute`
> -   `iproute2` for `ip route`
> -   `dnsutils` for `nslookup`, `dig`
> -   `net-tools` for `arp`, `ifconfig`, `netstat`
> -   `dsniff` for `arpspoof`
> -   `tcpdump` for `tcpdump`
> -   `wireshark` for Wireshark
> -   `curl` for cURL

## Resources

-   [Sample `Dockerfile`](https://github.com/HarshKapadia2/mac-ip-routing/blob/main/Dockerfile) and [sample `compose.yaml` file](https://github.com/HarshKapadia2/mac-ip-routing/blob/main/compose.yaml) used in [MAC and IP Routing project](https://talks.harshkapadia.me/mac-and-ip-routing).
-   [How to clear the ARP cache on Linux?](https://linux-audit.com/how-to-clear-the-arp-cache-on-linux)
-   [Run GUI app in linux docker container on windows host](https://dev.to/darksmile92/run-gui-app-in-linux-docker-container-on-windows-host-4kde)
-   [How to set up wireshark with correct permissions](https://unix.stackexchange.com/questions/111650/how-to-set-up-wireshark-with-correct-permissions)
-   [Automatically set YES when asked "Should non-superusers be able to capture packets"](https://askubuntu.com/questions/1214612/tshark-automatically-set-yes-when-asked-should-non-superusers-be-able-to-capt)
-   [Linux file system](https://gist.github.com/HarshKapadia2/18150e1e57eab1f0e500f18feea890aa)
-   [Linux Terminal commands](https://harshkapadia2.github.io/cli)
