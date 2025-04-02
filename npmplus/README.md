# Nginx Proxy Manager Plus

This compose stack is custom tailored to work in a way that allows my setup to have some container accesible outside using their own certificates and different domains that the ones I use in my home. This might not be thhe  way to go but is the more practical one for my use-case. 

```yaml
services:
  npmplus:
    container_name: npmplus
    image: docker.io/zoeyvid/npmplus:latest # or ghcr.io/zoeyvid/npmplus:latest
    restart: always
    ports:
      - '80:80' 
      - '81:81'
      - '443:443'
    volumes:
      - "./data:/data"
      - "./letsencrypt:/etc/letsencrypt" # Only needed for first time migration from original nginx-proxy-manager to this fork
      - "./config.json:/app/config/production.json"
    environment:
      - "DB_MYSQL_HOST=npmplus-db"
      - "DB_MYSQL_PORT=3306"
      - "DB_MYSQL_USER=npm"
      - "DB_MYSQL_PASSWORD=npmplus"
      - "DB_MYSQL_NAME=npm"
      - "LOGROTATE=true"
      - "LOGROTATIONS=7"
      - "TZ=Etc/UTC" # set timezone, required, set it to one of the values from the "TZ identifier" https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List
      - "ACME_EMAIL=test@mail.com" # email address which should be used for acme, currently optional, may be required in the future, so I recommend you to enter your email here, optional for letsencrypt, but required for zerossl and google public ca
      - "PUID=0" # set group id, needs to be a number greater or equal to 99, or equal to 0, default 0 (root)
      - "PGID=0" # set user id, needs to be a number greater or equal to 99, or equal to 0, default 0 (root), requires PUID to be not 0

  db:
    image: 'jc21/mariadb-aria:latest'
    container_name: npmplus-db
    restart: unless-stopped
    command: 
    #   --mysql-native-password=ON
      --skip-grant-tables
    environment:
      MYSQL_ROOT_PASSWORD: 'root'
      MYSQL_DATABASE: 'npm'
      MYSQL_USER: 'npm'
      MYSQL_PASSWORD: 'npmplus'
    volumes:
      - ./data/mysql:/var/lib/mysql


```