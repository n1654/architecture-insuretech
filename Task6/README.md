# Задание 6. Настройка Rate Limiting

Конфигурационный файл 

[nginx-rate-limit.conf](./nginx-rate-limit.conf)

____

Доработанная конфигурация nginx

```conf
http {
    # Настройка upstream для балансировки нагрузки
    upstream backend_servers {
        server backend1.example.com;
        server backend2.example.com;
        server backend3.example.com;
    }

    limit_req_zone $binary_remote_addr zone=one:10m rate=10r/m;

    server {
        listen 80;

        location / {
            limit_req zone=one;
            limit_req_status 429;

            proxy_pass http://backend_servers;
        }

    }
}
```