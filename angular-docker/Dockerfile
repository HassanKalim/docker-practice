# Use the official Node.js image as the base image
FROM node:14 as build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Install Angular CLI globally
RUN npm install -g @angular/cli

# Install project dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Build the Angular app for production
RUN ng build --prod

# Use a smaller HTTP server image to serve the Angular app (e.g., 'http-server')
FROM node:14 as final

# Set the working directory in the final container
WORKDIR /app

# Copy the built Angular app to the final container
COPY --from=build /app/dist /app/dist

# Expose a port for serving the Angular app (e.g., 8080)
EXPOSE 8080

# Install a simple HTTP server (e.g., 'http-server') to serve the Angular app
RUN npm install -g http-server

# Start the HTTP server to serve the Angular app
CMD ["http-server", "./dist", "-p", "8080"]
