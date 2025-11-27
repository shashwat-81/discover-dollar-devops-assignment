# frontend/Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

# Copy Angular code
COPY . .

EXPOSE 4200

# For Angular dev server
CMD ["npm", "run", "start"]
# Or ["ng", "serve", "--host", "0.0.0.0"] if that's how the project runs
