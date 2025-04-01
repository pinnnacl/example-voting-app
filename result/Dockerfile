FROM node:18-slim

# add curl for healthcheck
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl tini && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /usr/local/app

# have nodemon available for local dev use (file watching)
RUN npm install -g nodemon  #kind of hot reloadin, if the application is ruuning and we made any changes, it will reflect automatically"

COPY package*.json ./

RUN npm ci && \        #more like npm install, if any version defined in package.json, it will istall that perticular package"
 npm cache clean --force && \     #npm cache clean --force
 mv /usr/local/app/node_modules /node_modules

COPY . .

ENV PORT=80
EXPOSE 80

ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["node", "server.js"]
