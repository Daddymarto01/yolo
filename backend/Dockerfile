# ---- BUILD STAGE ----
FROM node:20-alpine AS build

WORKDIR /usr/src/app

# Copy only package files first (better caching)
COPY package*.json ./

# Install only production dependencies
RUN npm ci --only=production

# Copy application source code
COPY . .

# ---- RUNTIME STAGE ----
FROM node:20-alpine

WORKDIR /app

# Copy only the built app and node_modules
COPY --from=build /usr/src/app /app

# Expose the port the app runs on
EXPOSE 5000

# Define the command to run your app
CMD ["node", "server.js"]
