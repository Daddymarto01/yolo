# ---- BUILD STAGE ----
FROM node:20-alpine AS build

WORKDIR /usr/src/app
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy app source
COPY . .

# Fix OpenSSL issue (Node 17+)
ENV NODE_OPTIONS=--openssl-legacy-provider

# Build static production files
RUN npm run build

# ---- RUNTIME STAGE ----
FROM nginx:alpine

# Remove default nginx static assets
RUN rm -rf /usr/share/nginx/html/*

# Copy built React app from build stage
COPY --from=build /usr/src/app/build /usr/share/nginx/html

# Expose port 80 for Nginx
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
