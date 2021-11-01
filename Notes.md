# DO280 Notes

## Working with Podman
### running a specific version of a container named httpd-simple with network mapped from 8080 on the host to 80 in the container
	podman run -d -p 8080:80 --name httpd-simple   quay.io/redhattraining/httpd-parent:2.4
### checking on a pod on a port
	curl http://localhost:8080
### getting prompt inside a running container
  podman exec -it httpd-basic /bin/bash
