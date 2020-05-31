FROM nginx

## Step 1: Clear HTML - May want a new conf as well.
# RUN rm /etc/nginx/conf.d/default.conf
RUN rm /usr/share/nginx/html/index.html

## Step 2:
COPY green/content /usr/share/nginx/html
# COPY conf /etc/nginx
