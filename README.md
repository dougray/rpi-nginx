# rpi-nginx
[Nginx](https://www.nginx.com/) for [Docker](https://www.docker.com) on the [Raspberry Pi](https://www.raspberrypi.org).  This Nginx build has been built using Hypriot's Alpine Linux base image built for Raspberry Pi Docker systems.

Docker Hub: [https://hub.docker.com/r/frozenfoxx/rpi-nginx/](https://hub.docker.com/r/frozenfoxx/rpi-nginx/)

# How to Build
## Basic
```
git clone git@github.com:frozenfoxx/rpi-nginx.git
cd rpi-nginx
docker build .
```

## Custom Content Dir
* Check out
```
git clone git@github.com:frozenfoxx/rpi-nginx.git
cd rpi-nginx
```
* Open the `Dockerfile` and add the following:
```
FROM frozenfoxx/rpi-nginx
COPY some-html-static-dir /usr/share/nginx/html
```
* Resume build
```
docker build -t [custom-name-here] .
```

# How to Use this Image
##  Basic Run
This assumes you have static content to host in the container from the hypervisor.
```
docker run --name nginx -v /path/to/content:/usr/share/nginx/html:ro -d frozenfoxx/rpi-nginx
```

## Expose a Port
This allows you to expose the native ports to additional ones on the hypervisor.  In this case, 8080 will also access port 80.
```
docker run --name nginx -v /path/to/content:/usr/share/nginx/html:ro -p 8080:80 -d frozenfoxx/rpi-nginx
```
## Custom Configuration
This assume you have a custom nginx configuration you wish to run instead of the default.
```
[edit nginx.conf]
docker run --name nginx -v /path/to/custom/nginx.conf:/etc/nginx/nginx.conf:ro -d nginx
```

# Notes
* Be sure to include `daemon off;` in custom configurations or the container will immediately stop.
