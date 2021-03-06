![kibana-logo](https://raw.githubusercontent.com/blacktop/docker-kibana-alpine/master/kibana-logo.png)

# docker-kibana-alpine

[![CircleCI](https://circleci.com/gh/blacktop/docker-kibana-alpine.png?style=shield)](https://circleci.com/gh/blacktop/docker-kibana-alpine) [![License](http://img.shields.io/:license-mit-blue.svg)](http://doge.mit-license.org) [![Docker Stars](https://img.shields.io/docker/stars/blacktop/kibana.svg)](https://hub.docker.com/r/blacktop/kibana/) [![Docker Pulls](https://img.shields.io/docker/pulls/blacktop/kibana.svg)](https://hub.docker.com/r/blacktop/kibana/) [![Docker Image](https://img.shields.io/badge/docker%20image-576MB-blue.svg)](https://hub.docker.com/r/blacktop/kibana/)

Alpine Linux based [Kibana](https://www.elastic.co/products/kibana) Docker Image

**Table of Contents**

- [docker-kibana-alpine](#docker-kibana-alpine)
  - [Why?](#why)
  - [Dependencies](#dependencies)
  - [Image Tags](#image-tags)
  - [Getting Started](#getting-started)
  - [Documentation](#documentation)
    - [Customize at runtime via environment variables](#customize-at-runtime-via-environment-variables)
    - [To use your own elasticsearch address via `KIBANA_ELASTICSEARCH_URL`](#to-use-your-own-elasticsearch-address-via-kibanaelasticsearchurl)
  - [Issues](#issues)
  - [Credits](#credits)
  - [License](#license)

## Why?

Compare Image Sizes:

* official kibana = 1.01GB
* blacktop/kibana = 322MB

**Alpine version is 688 MB smaller !**

## Dependencies

* [node:alpine](https://hub.docker.com/_/node/)

## Image Tags

``` bash
REPOSITORY          TAG                 SIZE
blacktop/kibana     latest              576MB
blacktop/kibana     7.7                 576MB
blacktop/kibana     7.6                 389MB
blacktop/kibana     7.5                 306MB
blacktop/kibana     7.4                 310MB
blacktop/kibana     7.3                 322MB
blacktop/kibana     7.2                 294MB
blacktop/kibana     7.1                 253MB
blacktop/kibana     7.0                 253MB
blacktop/kibana     6.8                 242MB
blacktop/kibana     6.7                 242MB
blacktop/kibana     6.6                 225MB
blacktop/kibana     6.5                 269MB
blacktop/kibana     6.4                 250MB
blacktop/kibana     6.3                 316MB
blacktop/kibana     6.2                 309MB
blacktop/kibana     6.1                 255MB
blacktop/kibana     6.0                 209MB
blacktop/kibana     5.6                 191MB
blacktop/kibana     5.5                 189MB
blacktop/kibana     5.4                 203MB
blacktop/kibana     5.3                 145MB
blacktop/kibana     x-pack              685MB
blacktop/kibana     5.2                 246MB
blacktop/kibana     5.1                 246MB
blacktop/kibana     5.0                 245.8MB
blacktop/kibana     4.6                 229.7MB
```

> **NOTE:** tag **x-pack** is the same as tag **latest**, but includes the _x-pack_ plugin.

## Getting Started

``` bash
$ docker run --init -d --name elasticsearch -p 9200:9200 blacktop/elasticsearch
$ docker run --init -d --name kibana --link elasticsearch -p 5601:5601 blacktop/kibana
```

## Documentation

### Customize at runtime via environment variables

There are two types of env vars:

* `KIBANA_ELASTICSEARCH_URL=http://localhost:9200`
* `elasticsearch.url=http://localhost:9200`

### To use your own elasticsearch address via `KIBANA_ELASTICSEARCH_URL`

``` bash
$ docker run --init -d --name kibana -e KIBANA_ELASTICSEARCH_URL=http://some-elasticsearch:9200 -p 5601:5601 blacktop/kibana
```

For elasticsearch running on a OSX host it would be

``` bash
$ docker run --init -d --name kibana \
  -p 5601:5601 \
  --net host \
  -e KIBANA_ELASTICSEARCH_URL="http://$(ipconfig getifaddr en0):9200" \
  blacktop/kibana
```

For `x-pack` with basic auth:

``` bash
$ docker run --init -d --name kibana \
             --restart unless-stopped \
             -p 443:5601 \
             -v /etc/letsencrypt/archive/demo.malice.io:/certs \
             -e KIBANA_SERVER_SSL_ENABLED=true \
             -e KIBANA_SERVER_SSL_KEY=/certs/privkey1.pem \
             -e KIBANA_SERVER_SSL_CERTIFICATE=/certs/cert1.pem \
             -e KIBANA_ELASTICSEARCH_URL=$KIBANA_ELASTICSEARCH_URL \
             -e KIBANA_ELASTICSEARCH_USERNAME=$KIBANA_ELASTICSEARCH_USERNAME \
             -e KIBANA_ELASTICSEARCH_PASSWORD=$KIBANA_ELASTICSEARCH_PASSWORD \
             --log-opt max-size=100m \
             --log-opt max-file=3 \
             blacktop/kibana:x-pack
```

## Issues

Find a bug? Want more features? Find something missing in the documentation? Let me know! Please don't hesitate to [file an issue](https://github.com/blacktop/docker-kibana-alpine/issues/new)

## Credits

Heavily (if not entirely) influenced by https://github.com/docker-library/kibana

## License

MIT Copyright (c) 2016-2020 **blacktop**

