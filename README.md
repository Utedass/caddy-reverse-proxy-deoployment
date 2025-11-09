# To run

Make sure to update the docker-compose file to suit your needs. You need to add all the named networks that your other docker compose projects use that you want to proxy to.

For example, you can add the following to add / join a few networks:

```
    networks:
      - docker_service_network
      - another_docker_service_network

...

networks:
  docker_service_network:
    name: docker_service_network
  another_docker_service_network:
    name: another_docker_service_network
```

Then in your caddy-file, you can refer to the names of the services. Dockers DNS-thingies will sort it out. For example:

```
wordpress.mysite.com {
    reverse_proxy docker-wordpress-service:80
}

maps.minecraft.my-friends-site.com {
    reverse_proxy docker-minecraft-map-service:8080
}

```

When you have finished the setup, just run:

```
docker compose up -d
```

To shut down and remove all docker volumes (only cache and config, which are not really important) run

```
docker compose down -v
```

To reload the Caddyfile without restarting, run

```
docker exec -w /etc/caddy caddy caddy reload
```

For more info, check out the official Caddy page at dockerhub: https://hub.docker.com/_/caddy

Or the official Caddy documentation: https://caddyserver.com/docs/
