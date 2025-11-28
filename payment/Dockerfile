FROM python:3.9
EXPOSE 8080
WORKDIR /opt/server
COPY payment.ini .
COPY *.py .
COPY requirements.txt .
RUN pip3 install -r requirements.txt
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
CMD ["uwsgi", "--ini", "payment.ini"]


# Below is the optimized image

# FROM python:3.9 AS build
# WORKDIR /opt/server
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# # RUN pip3 install -r requirements.txt
# RUN pip3 install --prefix=/libraries -r requirements.txt


# FROM python:3.9-alpine 
# WORKDIR /opt/server
# EXPOSE 8080
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
#     chown -R roboshop:roboshop /opt/server
# RUN apk add --no-cache pcre 
# LABEL project="roboshop" \
#       component="payment" \
#       created_by="phani"  

# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# COPY --from=build /libraries /usr/local
# COPY payment.ini *.py requirements.txt .
# USER roboshop
# CMD ["uwsgi", "--ini", "payment.ini"]



