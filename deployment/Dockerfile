FROM nginx:alpine
COPY docker build -t nabilwics/dummy-app -f deployment/Dockerfile .
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
