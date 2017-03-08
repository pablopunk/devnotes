### Multiple domains in nginx.

Edit `/etc/nginx/sites-available/default` and add one configuration per domain.
In this case we have a domain pointing to a folder (`/home/pi/www`) while the other server is pointing to a port:

```shell
server {
    listen 80;
    server_name pablopunk.ga;
    root /home/pi/www;
    autoindex on;
}

server {
    listen 80;
    server_name pablo.life;
    location / {
        proxy_pass http://127.0.0.1:3001;
    }
}
```
