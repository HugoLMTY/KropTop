# build stage
FROM node:16 as build-stage

WORKDIR /app

COPY /front/package.json ./

RUN npm install

COPY ./front .

ARG API_HOST
RUN touch .env
RUN echo API_HOST=${API_HOST} >> .env

EXPOSE 3000

RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage

COPY --from=build-stage /app/dist /usr/share/nginx/html
COPY ./front/nginx/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
