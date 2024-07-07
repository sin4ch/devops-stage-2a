# Stage 1: Build the React application
FROM node:20 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the frontend codebase to the working directory
COPY . .

# Build the application for production
RUN npm run build

# Stage 2: Serve the application using Nginx
FROM nginx:stable-alpine

# Validate the output directory
# Check if it's named `build`, `dist`, or something else in the actual project after the build process
# Typically for React, it should be `build`, but for tools like Vite, it might be `dist`.
# Assuming it might be `dist` based on common Vite configurations, you can adjust accordingly.

# Copy the built application from the build stage to the Nginx HTML directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80  to allow external access
EXPOSE 80 

# Start the Nginx server
CMD ["nginx", "-g", "daemon off;"]
