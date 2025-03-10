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

# Expose port 80 for serving the frontend
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
