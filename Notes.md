# DO280 Notes

## Working with Podman
### run with external variables
	 podman run -e GREET=wassup -e NAME=bananas ubi8/ubi:8.3 printenv GREET NAME
### running a specific version of a container named httpd-simple with network mapped from 8080 on the host to 80 in the container, in the background (detach)
	podman run -d -p 8080:80 --name httpd-simple   quay.io/redhattraining/httpd-parent:2.4
### checking on a pod on a port
	curl http://localhost:8080
### getting prompt inside a running container
	podman exec -it httpd-basic /bin/bash
### More Podman
	sudo podman run --rm --name asroot -ti registry.access.redhat.com/ubi8:latest /bin/bash # run a container as root
	podman ps # list processes
	podman stop [name] # stop a container
	podman rm [name] # remove a container
	podman search
	podman pull ubi8/ubi:latest
	podman run -d -p 8080 registry.redhat.io/rhel8/httpd-24 # run in the background, connect container port 8080
	podman push
	podman login
	podman rm -a
	podman stop -a
	podman cp /path/on/host containername:/path/on/container
	podman exec mysql /bin/bash -c 'mysql -uuser1 -pmypa55 items < /db.sql'
	
### persistent storage
	mkdir /home/jsmith/dbfiles
	podman unshare chown -R 27:27 /home/jsmith/dbfiles #change ownership to mysql, uid 27
	sudo semanage fcontext -a -t container_file_t '/home/jsmith/dbfiles(/.*)?' #apparently we're setting SELinux contexts now
	sudo restorecon -Rv /home/jsmith/dbfiles
	podman run -v /path/on/host:/path/in/container/filesystem ubi8:ubi:latest #mount a volume

### makin new images
	podman exec -it my-container /bin/bash #then change something
	podman commit -a "its me" image-name repo/new-image-name:tag
	
	podman build --layers=false -t repo/name . # where the current directory contains a dockerfile
	
	
## oc stuff
	#you konw this
