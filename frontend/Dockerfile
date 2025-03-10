# Use an appropriate Node.js base image for building the frontend
FROM node:20-alpine AS builder

# Set the working directory
WORKDIR /app

# Copy frontend source code
COPY frontend/ .

# Install PNPM globally
RUN npm install -g pnpm

# Install dependencies and build the project
RUN pnpm install && pnpm build

# Move the build output outside the frontend folder and clean up
RUN mv dist /build && rm -rf /app

# Use Nginx for serving the frontend
FROM nginx:alpine

# Copy the built frontend files to the Nginx serving directory
COPY --from=builder /build /usr/share/nginx/html

# Copy the custom Nginx configuration file
COPY frontend/config.nginx /etc/nginx/conf.d/default.conf

# Expose ports for both HTTP and HTTPS
EXPOSE 80 443

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
