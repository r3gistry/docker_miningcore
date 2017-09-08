## MiningCore-Docker

Official MiningCore docker-image

### Usage

The image expects a valid pool configuration file as volume argument:

```bash
$ docker run -d -p 3032:3032 -v /path/to/config.json:/config.json:ro coinfoundry/miningcore-docker
```

As shown in the example above you also need to expose all the stratum ports you've specified in config.json.
