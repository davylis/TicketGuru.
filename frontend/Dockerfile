# Use an official Node runtime as a parent image
# Use an official Node runtime as a parent image
FROM node:22-alpine AS build

# Set the working directory to /app
WORKDIR /app

# Copy the package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm ci

# Set memory limit for Node.js during build
ENV NODE_OPTIONS=--max-old-space-size=2048

# Copy the rest of the application code to the container
COPY . .

# Build the React app
RUN npm run build

# Use Nginx to serve the React app
FROM nginx:alpine

# Copy React build to nginx HTML directory 
COPY --from=build /app/build /usr/share/nginx/html/

# Copy nginx configuration file 
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose the port
EXPOSE 8081

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
