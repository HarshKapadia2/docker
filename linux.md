# Running a Linux distro in Docker

Some tips to help with Linux in Docker.

## Commands

### Docker

-   `docker container run --cap-add=NET_ADMIN -it -v "%cd%":/mnt --name kali kalilinux/kali-rolling`
    -   [Giving network privileges to the container](https://unix.stackexchange.com/questions/459206/list-ip-tables-in-docker-container)
    -   [Giving all privileges to the container](https://stackoverflow.com/questions/36425230/privileged-containers-and-capabilities)
    -   [Docker Networking Crash Course](https://www.youtube.com/watch?v=OU6xOM0SE4o)
-   `docker container start kali`
-   `docker exec -it kali bash`
-   `exit`
-   `docker container stop kali`
-   `docker container rm kali` (NOTE: Only use this if the container needs to be destroyed.)

### Kali Linux

> NOTE:
>
> -   Extrapolate these commands for other Linux distros.
> -   `sudo` might have to be used before some commands.

#### Run on container creation

-   `apt-get update` (One might have to run this randomly as well.)
-   `apt-get upgrade`

#### Necessary utilities

-   `apt-get install vim`
-   `apt-get install man`

#### Networking packages

> `apt-get install <package_name>`

-   `iputils-ping` for `ping`
-   `iproute2` for `ip route`
-   `net-tools` for `arp`, `ifconfig`, `netstat`
-   `dnsutils` for `nslookup`, `dig`
-   `dsniff` for `arpspoof`
