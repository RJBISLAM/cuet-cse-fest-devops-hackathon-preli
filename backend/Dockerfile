# backend/Dockerfile
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
# Install ALL dependencies (including tools to build the app)
RUN npm install
COPY . .
# --- NEW STEP: Build the application ---
RUN npm run build

FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
# Install only production dependencies
RUN npm install --only=production
# --- FIX: Copy the 'dist' folder created by the build step ---
COPY --from=builder /app/dist ./dist
USER node
EXPOSE 3847
CMD ["npm", "start"]