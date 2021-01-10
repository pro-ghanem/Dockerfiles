#stage 1
FROM node:10 as node
RUN  mkdir  /app
WORKDIR /app

# copy app files
COPY . .

# angular - install and cache app dependencies
RUN npm i
RUN npm run ng build -- --configuration=staging

# vuejs - install and cache app dependencies
RUN cd ./src/framer && ls && pwd &&  NODE_ENV=development && npm i && npm run build && pwd && ls &&  mkdir -p /app/dist/framer/dist &&>

# stage 2
FROM nginx:alpine
COPY --from=node /app/dist/ /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf

