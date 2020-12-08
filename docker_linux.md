# Running a Linux distro in Docker

Some tips to help with Linux in Docker.

## Container privileges

- Network privileges might be required sometimes (https://unix.stackexchange.com/questions/459206/list-ip-tables-in-docker-container)
- All privileges: https://stackoverflow.com/questions/36425230/privileged-containers-and-capabilities

## Commands

### Docker

- `docker container run --cap-add=NET_ADMIN -it -v "%cd%":/mnt --name kali kalilinux/kali-rolling`
- `docker container start kali`
- `docker exec -it kali bash`
- `exit`
- `docker container stop kali`
- `docker container rm kali` (NOTE: Only use this if the container needs to be destroyed.)

### Linux Distro

> NOTE: `sudo` might have to be used before the commands.

- `apt-get update`
- `apt-get upgrade`

#### Necessary utilities

- `apt-get install vim`
- `apt-get install man`
- `apt-get install dnsutils`
- `apt-get install net-tools`
