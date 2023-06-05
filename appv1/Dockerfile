FROM nginx:1.24.0
LABEL version="1.0" maintainer="Manouchehr Soleymani <manouchehr.sgh@gmail.com>"
WORKDIR /usr/share/nginx/html/ 
COPY ./src/* .
RUN mkdir /etc/nginx/html/
COPY ./src/favicon.ico /etc/nginx/html/favicon.ico
EXPOSE 80
