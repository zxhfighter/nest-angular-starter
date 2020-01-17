# stage 1
FROM node:8.16.0-alpine as node

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY src/* ./
COPY *.json ./
COPY boot.sh ./

RUN yarn install
RUN yarn run build

EXPOSE 3000
ENTRYPOINT ["./boot.sh"]
