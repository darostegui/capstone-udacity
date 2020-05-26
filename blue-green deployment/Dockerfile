FROM nginx

## Step 1: Clear conf
RUN rm /etc/nginx/conf.d/default.conf
RUN rm /usr/share/nginx/html/index.html

## Step 2:
COPY content /usr/share/nginx/html
COPY conf /etc/nginx
