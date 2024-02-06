Here is a sample Dockerfile that you could use to build the Astro project:

```dockerfile
FROM node:14 as builder

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM nginx:alpine as runner

COPY --from=builder /app/build /usr/share/nginx/html
```

This Dockerfile uses a multi-stage build process to first build the Astro project using the Node.js runtime, and then copies the built files into an nginx container for deployment.

To build the Docker image using this Dockerfile, you can run the following command:

```
docker build -t astro-image .
```
This will build the image and tag it with the name “astro-image”. You can then run the image using the following command:

```
docker run -p 80:80 astro-image
```

This will start a container running the nginx web server and serve the built Astro project on port 80.