

### WEB Application
```
npm install

node src/app.js

Server is running on http://localhost:25000
```

### MinIO Server
```

Experiment CORS with minio.

CI=true MINIO_ROOT_USER=minio MINIO_ROOT_PASSWORD=minio123 minio server --address ":22000" --console-address ":10000" /tmp/sr1/data{1...4}

mc alias set local22 http://localhost:22000 minio minio123


mc mb local22/test-bucket
echo "1" > 1.txt
mc cp 1.txt "local22/test-bucket/1.txt" 
mc anonymous set public  local22/test-bucket

```
### Testing

```
> To Observe cors error 
mc admin config set local22 api  cors_allow_origin="http://example.com"

Refresh Page and observe the CORS error

> Observe success
2. mc admin config set local22 api  cors_allow_origin="*"

 Refresh Page and observe the success
```
### cURL
```
#Successful scenario
curl -H "Access-Control-Request-Method: GET" -H "Origin: http://example.com" -I http://localhost:22000/test-bucket/1.txt
# Failure scenario with different origin
curl -H "Access-Control-Request-Method: GET" -H "Origin: http://example1.com" -I http://localhost:22000/test-bucket/1.txt
```
