# internal-service-health-check-api
A simple and very light weight health check api with rust (originally written in golang but encountered CPU spike issues after the server had not been rebooted for a while)

Link to: [internal-health-check-api](https://github.com/Ponlponl123-Labs/internal-health-check-api) (with golang)

### ENV

- Format:
    ```env
    PORT=8080 // Default HTTP port is 8080

    SINGLE_THREADED=false // use thread?
    
    {SERVICE_NAME}_HEALTH_HOST // target host
    {SERVICE_NAME}_HEALTH_PORT // port number
    {SERVICE_NAME}_HEALTH_TYPE // this should be "TCP" or "UDP"
    ```

- Example:

    ```env
    WEB_HEALTH_HOST=google.com
    WEB_HEALTH_PORT=80
    WEB_HEALTH_TYPE=TCP

    DNS_HEALTH_HOST=1.1.1.1
    DNS_HEALTH_PORT=53
    DNS_HEALTH_TYPE=TCP
    ```

## Docker

https://hub.docker.com/r/ponlponl123/internal-service-health-check-api

### Pull

```bash
docker pull ponlponl123/internal-service-health-check-api
```

### docker-compose.yaml

```yaml
services:
  internal-service-health-check-api:
    image: ponlponl123/internal-service-health-check-api:latest
    ports:
      - 8080:8080
    environment:
      - SINGLE_THREADED=true
      
      - WEB_HEALTH_HOST=google.com
      - WEB_HEALTH_PORT=80
      - WEB_HEALTH_TYPE=TCP
      
      - DNS_HEALTH_HOST=1.1.1.1
      - DNS_HEALTH_PORT=53
      - DNS_HEALTH_TYPE=TCP
    restart: always
```
