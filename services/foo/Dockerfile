# Pulling the node image from docker hub.
FROM node:18-alpine

# Installing pnpm to the global.
RUN curl -f https://get.pnpm.io/v6.16.js | npm i -g pnpm

# Creating a directory called `app` in the `/usr/src` directory.
WORKDIR /usr/src/app

# Copying the pnpm-lock.yaml file to the WORKDIR.
COPY pnpm-lock.yaml ./

# Fetching the dependencies from the pnpm-lock.yaml file.
RUN pnpm fetch --prod

# Copying the files from the current directory to the WORKDIR.
COPY . .

# Installing the dependencies from the pnpm-lock.yaml file.
RUN pnpm install

# Exposing the port 3000 to the outside world.
EXPOSE 3000

# Starting the server.
CMD node index.js