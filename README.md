# RUN

```bash
docker-compose up --build -d
```

# Files

- docker-compose.yml
- conf.d
| - fintake.conf
| - [new service conf]


# docker-compose.yml

```yml
version: '3'
services:
  nginx:
    container_name: nginx
    image: staticfloat/nginx-certbot
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    environment:
      CERTBOT_EMAIL: birken1018@gmail.com
    volumes:
      - ./conf.d:/etc/nginx/user.conf.d:ro
      - letsencrypt:/etc/letsencrypt
      - /home/ray_xie/fintake/vue/dist:/usr/share/nginx/html/fintake
      - [new views for other service]
    networks:
      - fintake_flask
      - [new docker network]

volumes:
    letsencrypt:

networks:
  fintake_flask:
    external: true
  [new docker network]
    external: true
```
