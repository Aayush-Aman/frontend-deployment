# Stage 1: Build the React application
FROM node:20-alpine AS build

WORKDIR /app

# Copy package files first to leverage Docker cache
COPY package*.json ./
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the app (Vite or Create React App)
RUN npm run build

# Stage 2: Serve the app with Nginx
FROM nginx:stable-alpine

# Copy the production build from the build stage
# Note: For Vite, use /app/dist. For CRA, use /app/build
COPY --from=build /app/dist /usr/share/nginx/html

# Copy a custom nginx config if you have one (optional)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]