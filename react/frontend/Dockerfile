FROM node:13.12.0-alpine as build
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH
ENV REACT_APP_BACKEND http://abc4fsdfsdfasdfagdsafds.asf4gd681.ap-southeast-1.elb.amazonaws.com

#RUN COPY package-lock.json ./ if exist and then install 
COPY package.json ./
COPY package-lock.json ./
COPY . ./
RUN npm i
RUN npm install react-scripts@3.4.1 -g --silent
RUN npm run build

# production environment
FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
