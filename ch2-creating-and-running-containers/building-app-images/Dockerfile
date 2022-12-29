# Start from a Node.js 18 (LTS) image
FROM node:18

# Specify the directory inside the image in which all commands will run
WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm config set proxy <proxy-url>
RUN npm config set https-proxy <proxy-url>
RUN npm install
RUN npm install express

# Copy all of the app files into the image
COPY . .

# The default command to run when starting the container
CMD [ "npm", "start" ]
