FROM node:13.14.0

# Install pm2
RUN npm install pm2 -g
RUN mkdir /app
COPY . /app/
EXPOSE 3000
WORKDIR /app/dist/
RUN ls -lh /app/dist
# Start pm2.json process file
CMD ["pm2-runtime", "start", "index.js"]
