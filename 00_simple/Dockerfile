FROM --platform=arm64 ubuntu:22.04

RUN apt-get update && apt-get install -y apache2
RUN echo "<!DOCTYPE html><html><body><h1>Hello from ARM Container!</h1></body></html>" > /var/www/html/index.html

EXPOSE 80
CMD ["apache2", "-f", "/etc/apache2/apache2.conf"]
