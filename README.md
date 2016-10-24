# rpi-nginx
[Nginx](https://www.nginx.com/) for [Docker](https://www.docker.com) on the [Raspberry Pi](https://www.raspberrypi.org).

# Build
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

# Run
* Basic usage using content in a bound directory:
```
docker run --name nginx -v /path/to/content:/usr/share/nginx/html:ro -d frozenfoxx/rpi-nginx
```

* Running a custom built image:
```
docker run --name nginx -d [custom-name-here]
```

* Custom config:
```
[edit nginx.conf]
docker run --name nginx -v /path/to/custom/nginx.conf:/etc/nginx/nginx.conf:ro -d nginx
```

# Notes
* Be sure to include `daemon off;` in custom configurations or the container will immediately stop.
