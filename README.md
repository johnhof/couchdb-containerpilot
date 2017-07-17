# couchdb-containerpilot

couchdb + [containerpilot](https://www.joyent.com/containerpilot) docker images for bootstrapping your [autopiloted](https://www.joyent.com/blog/applications-on-autopilot) infractructure

[**Dockerhub Link**](https://hub.docker.com/r/johnhof/couchdb-containerpilot/)

## Configuration

### Couchdb

See the [couchdb image](https://hub.docker.com/_/couchdb/) documentation

### Containerpilot

Uses default containerpilot.json file:

```
{
  "consul": "consul:8500",
  "logging": {
    "level": "INFO",
    "format": "default",
    "output": "stdout"
  },
  "jobs": [
    {
      "name": "couchdb",
      "exec": "couchdb",
      "restarts": "unlimited",
      "port": 3000,
      "health": {
        "exec": "/usr/bin/curl --fail -s -o /dev/null http://localhost:5984",
        "interval": 3,
        "ttl": 10
      }
    }
  ]
}
```

Can be overwritten by either:
- Mapping a custom volume/config to `/etc/containerpilot.json`
- Mapping a custom volume/config to a custom location and setting the `CONTAINERPILOT` path to reflect it

#### Consul

Expects DNS entry for `consul`

Expects consul port to be `8500`

Healthcheck hits `/` expecting 200
