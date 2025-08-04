FROM nginx:alpine
COPY src/dummy_app.mpk /usr/share/nginx/html/mendix.mpk
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
