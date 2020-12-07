# Bind Mount

> NOTE: Docker Toolbox uses VirtualBox.

- From https://forums.docker.com/t/map-windows-directory-to-docker-container/5715:
	- On Windows, you can not directly map Windows directory to your container. Because your containers are reside inside a VirtualBox VM. So your docker -v command actually maps the directory between the VM and the container.

- So you have to do it in two steps:
	- Map a Windows directory to the VM through VirtualBox manager
	- Map a directory in your container to the directory in your VM

- So to use a volume, add a shared folder to virtualBox. (Refer to below link)
	- I added x drive as a shared folder with the name x_drive in virtualBox.
	- http://support.divio.com/en/articles/646695-how-to-use-a-directory-outside-c-users-with-docker-toolbox-docker-for-windows
	- Use `sudo vi profile` to edit the profile file. VI editor: Hit <kbd>i</kbd> to add data. Once done, hit <kbd>esc</kbd>. Then type `:wq` to save and exit.
	- Then use cmd: `docker container run -d -p 8083:80 -v /x_drive/coding/docker/docker_basics/mounting_example:/usr/share/nginx/html --name nginx-website nginx`
