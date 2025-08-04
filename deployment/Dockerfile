FROM nginx:alpine
RUN echo '<html><head><title>Dummy App</title></head><body><h1>Jenkins Pipeline Success!</h1><p>Build completed successfully</p></body></html>' > /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
