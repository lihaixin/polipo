Polipo — a caching web proxy
============================

[Polipo][1] is a small and fast caching web proxy (a web cache, an HTTP proxy, a
proxy server). While Polipo was designed to be used by one person or a small
group of people, there is nothing that prevents it from being used by a larger
group.

## docker-compose.yml

```yaml
polipo:
  image: lihaixin/polipo
  command:
    proxyAddress=0.0.0.0
    proxyPort=8123
    authCredentials=username:password
    socksParentProxy=ParentServerIP:8123
  ports:
    - "8123:8123"
  restart: always
```

## server

```bash
$ docker-compose up -d
```
OR

```bash
$ docker run -d --restart=always --name=polipo -p 8123:8123 lihaixin/polipo proxyAddress=0.0.0.0  authCredentials=username:password
```

more parameter use

```bash
$ docker run --rm lihaixin/polipo --help
```
## client

```bash
$ curl -x http://username:password@server:8123 https://www.youtube.com/
$ wget -e use_proxy=yes -e proxy-user=username -e proxy-password=password -e http_proxy=server:8123 http://cachefly.cachefly.net/100mb.test
```

[1]: https://www.irif.univ-paris-diderot.fr/~jch/software/polipo/

