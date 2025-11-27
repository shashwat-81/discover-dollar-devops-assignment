# backend/Dockerfile
FROM node:18-alpine

WORKDIR /app

# Copy package files
COPY package*.json ./

RUN npm install

# Copy all backend code
COPY . .

# App listens on port 3000 (or check server.js for the actual port)
EXPOSE 3000

# Run server.js directly since no "start" script exists
CMD ["node", "server.js"]
