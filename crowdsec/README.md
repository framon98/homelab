# Crowdsec

Using the official guide [Crowdsec](https://docs.crowdsec.net/u/getting_started/installation/docker/) and a couple fo more blogposts my config for crowdesc container looks like this. It is separate from the nginx public ontainer since I set it up afterwards and to prevent downtime If I needed to adjust things here. 

It was easier to debug having them separate to allow killing only one at a time and not both each time.
For this deployment fo crowdsec I used the npm plus image from ZoeyVid

```yaml
services:
  crowdsec:
    image: crowdsecurity/crowdsec
    restart: always
    network_mode: host
    environment:
      COLLECTIONS: "ZoeyVid/npmplus"
      GID: "${GID-1000}"
    volumes:
      # - ./acquis.yaml:/etc/crowdsec/acquis.yaml
      - /data/nginx:/opt/npm/nginx # This line should point to the location of the nginx proxy manager logs.
      - ./crowdsec-db:/var/lib/crowdsec/data/
      - ./crowdsec-config:/etc/crowdsec/
      - "/var/run/docker.sock:/var/run/docker.sock:ro"
```