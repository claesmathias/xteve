# xteve
xteve, in docker with cron

docker runs in host mode \
access xteve webui ip:34400/web/

after docker start check your config folder and do your setups, setup is persistent, start from scratch by delete them

cron and xteve start options are updated on docker restart.


## Usage

Here are some example snippets to help you get started creating a container.

### docker-compose (recommended, [click here for more info](https://docs.linuxserver.io/general/docker-compose))

```yaml
---
version: "2.1"
services:
  xteve:
    image: claesmathias/xteve:latest-arm64
    container_name: xteve
    network_mode: host
    restart: always
    environment:
      - TZ=${TZ}
    volumes:
      - /path/to/conf:/home/xteve/conf
      - /path/to/xteve:/root/.xteve:rw
      - /path/to/config:/config:rw
      - /tmp/xteve:/tmp/xteve:rw
    logging:
      options:
        max-file: "3"
        max-size: "10m"
    restart: unless-stopped

```

### docker cli ([click here for more info](https://docs.docker.com/engine/reference/commandline/cli/))

```bash
  docker run -d \
  --name=xteve \
  --net=host \
  --log-opt max-size=10m \
  --log-opt max-file=3 \
  -e TZ="Europe/Berlin" \
  -v /path/to/xteve:/root/.xteve:rw \
  -v /path/to/config:/config:rw \
  -v /tmp/xteve/:/tmp/xteve:rw \
  -v /path/to/tvheadend/data/:/TVH `#optional` \
  claesmathias/xteve:latest-arm64
```

## Parameters

Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `--net=host` | Use Host Networking |
| `-v /config` | Config data |
| `-v /root/.xteve` | User data |
| `-v /tmp` | Temporary storage |
| `-v /TVH` | TvHeaded |


