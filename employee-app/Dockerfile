# Step 1: Build Frontend Client
FROM node:18-alpine AS client-build
WORKDIR /app/client
COPY client/package*.json ./
RUN npm ci
COPY client/ ./
RUN npm run build

# Step 2: Set up Backend Server & Static Production Files
FROM node:18-alpine AS final
WORKDIR /app
COPY server/package*.json ./server/
RUN cd server && npm ci --only=production
COPY server/ ./server/
COPY --from=client-build /app/client/dist ./server/public

EXPOSE 5000
ENV PORT=5000
CMD ["node", "server/server.js"]