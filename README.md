# Docker image of Nginx Proxy with Basic Auth And Whitelist Ip

[![Docker Repository on docker hub](https://www.unixtutorial.org/images/software/docker-hub.png "Docker Repository on Docker Hub")](https://hub.docker.com/r/vlacour97/nginx-basic-auth-proxy-whitelist-ip)

Simple HTTP Proxy with Basic Authentication

```
       w/ user:pass   +------------------------+      +-------------+
User ---------------> | nginx-basic-auth-proxy | ---> | HTTP Server |
                      +------------------------+      +-------------+
```

## Run

```bash
$ docker run \
    --rm \
    --name nginx-basic-auth-proxy \
    -p 8080:80 \
    -p 8090:8090 \
    -e BASIC_AUTH_USERNAME=username \
    -e BASIC_AUTH_PASSWORD=password \
    -e WHITELIST_IPS="192.168.0.1,192.168.0.2" \
    -e PROXY_PASS=https://www.google.com \
    -e SERVER_NAME=proxy.dtan4.net \
    -e PORT=80 \
    vlacour97/nginx-basic-auth-proxy-whitelist-ip
```

Access to http://localhost:8080 , then browser asks you username and password.

You can also try complete HTTP-proxy example using Docker Compose.
hello-world web application cannot be accessed without authentication.

```bash
$ docker-compose up
# http://localhost:8080/
# - Username: username
# - Password: password
```

### Endpoint for monitoring

`:8090/nginx_status` returns the metrics of Nginx.

```sh-session
$ curl localhost:8090/nginx_status
Active connections: 1
server accepts handled requests
 8 8 8
Reading: 0 Writing: 1 Waiting: 0
```

## Environment variables

### Required

|Key|Description|
|---|---|
|`BASIC_AUTH_USERNAME`|Basic auth username|
|`BASIC_AUTH_PASSWORD`|Basic auth password|
|`PROXY_PASS`|Proxy destination URL|

### Optional

|Key| Description                                | Default       |
|---|--------------------------------------------|---------------|
|`SERVER_NAME`| Value for `server_name` directive          | `example.com` |
|`PORT`| Value for `listen` directive               | `80`          |
|`WHITELIST_IPS`| Value for `whitelist` directive            | ` `           |
|`CLIENT_MAX_BODY_SIZE`| Value for `client_max_body_size` directive | `1m`          |
|`PROXY_READ_TIMEOUT`| Value for `proxy_read_timeout` directive   | `60s`         |
|`WORKER_PROCESSES`| Value for `worker_processes` directive     | `auto`        |

## Author

* Daisuke Fujita (forked) ([@dtan4](https://github.com/dtan4))  
* Valentin Lacour ([@vlacour97](https://github.com/vlacour97))

## License

[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)
