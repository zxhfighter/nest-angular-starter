# stage 1
FROM node:10.9.0-alpine as node

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY ./package*.json ./
COPY angular.json ./
COPY tsconfig.json ./
COPY tsconfig.app.json ./
COPY src/ ./src

RUN yarn install --registry=https://registry.npm.taobao.org
RUN yarn run build

RUN mkdir -p /usr/dist
RUN cp -r /usr/src/app/dist /usr/dist
RUN rm -rf /usr/src/app

# stage 2
FROM nginx:1.15.12-alpine

RUN rm -rf /usr/share/nginx/html/*
COPY --from=node /usr/dist/* /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
