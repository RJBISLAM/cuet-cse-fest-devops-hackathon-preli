# gateway/Dockerfile
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
# CHANGED: "ci" to "install"
RUN npm install
COPY . .

FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
# CHANGED: "ci" to "install"
RUN npm install --only=production
COPY --from=builder /app/src ./src
USER node
EXPOSE 5921
CMD ["npm", "start"]