# FROM node:20
# WORKDIR /opt/server
# EXPOSE 8080
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node","server.js"]


# Above is basic structure , as we need to reduce image size for best practices , below are the things

FROM node:20.19.6-alpine3.22 AS build
WORKDIR /opt/server
EXPOSE 8080
COPY package.json .
COPY *.js .
# as we know npm install will create node_modules folder and some extra cache , we need only node_modules no need cache
RUN npm install 

# after build the above will be deleted only below will be there as final image so we need to do user in second 

FROM node:20.19.6-alpine3.22
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
COPY --from=build /opt/server /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      component="catalogue" \
      created_by="phani"  
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
RUN chown -R roboshop:roboshop /opt/server
USER roboshop
# CMD ["node","server.js"]
CMD ["server.js"]
ENTRYPOINT ["node"]