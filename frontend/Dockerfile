# FROM nginx:1.24
# RUN rm -rf /usr/share/nginx/html/index.html
# RUN rm -rf /etc/nginx/nginx.conf
# RUN rm -rf /etc/nginx/conf.d/default.conf
# COPY nginx.conf /etc/nginx/nginx.conf
# COPY static /usr/share/nginx/html/



# Below is the optimized image

FROM nginx:1.24-alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf /usr/share/nginx/html/* /etc/nginx/nginx.conf /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf
COPY static/ .
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

