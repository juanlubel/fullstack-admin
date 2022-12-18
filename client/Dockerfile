FROM node:18-alpine3.16 as build
WORKDIR /app

COPY ./package.json .
COPY ./package-lock.json .
RUN npm install
COPY . /app
RUN npm run  build

# stage 2 - build the final image and copy the react build files
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf /etc/nginx/conf.d
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]