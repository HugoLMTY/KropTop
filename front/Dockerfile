# build stage
FROM node:18 as build-stage

WORKDIR /front

COPY package.json ./

RUN npm install

COPY . .
RUN touch .env

RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage

COPY --from=build-stage /front/dist /usr/share/nginx/html
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
