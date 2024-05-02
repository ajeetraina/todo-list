## Building Multi-arch Docker Image


You can use `docker buildx` to build multi-architecture platform Docker Image 

```
 docker buildx build --platform linux/amd64 -t todo-multiarch .
```

## Inspecting the architecture of the Docker Image

```
 docker inspect --format='{{.Os}}/{{.Architecture}}' todo-multiarch:latest
```

## Result:

```
 linux/amd64
```

## Try running it on your new Apple Laptop

```
docker run -d -p 3003:3000 todo-multiarch
WARNING: The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
895ea3e02d38a19c56ad1d15493d681091310fbbbd00031cf2c5d803a787a542
```


## Try building it for multiple platforms

``1
docker buildx build --platform linux/amd64,linux/arm64 -t todo-multiarch .
```
