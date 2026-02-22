### Overview of the Assignment ###

Step 1: 
# Cloned the existing repository, created a new submission directory, and structured the service directories accordingly.

<img width="1567" height="402" alt="image" src="https://github.com/user-attachments/assets/1854ab49-1ea9-45c6-bd06-bf15bbed9834" />

Step 2:
# Docker File

cat > user-service/Dockerfile << 'EOF'
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
EOF

# Product Service
cat > product-service/Dockerfile << 'EOF'
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3001
CMD ["npm", "start"]
EOF

# Gateway Service
cat > gateway-service/Dockerfile << 'EOF'
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3003
EOF ["npm", "start"]

# Dockerfile and Compose setup

# Docker Compose file 

cat > docker-compose.yml << 'EOF'
services:
  user-service:
    build: ./user-service
    ports: ["3000:3000"]
    networks: ["app-net"]
  product-service:
    build: ./product-service
    ports: ["3001:3001"]
    networks: ["app-net"]
  order-service:
    build: ./order-service
    ports: ["3002:3002"]
    networks: ["app-net"]
  gateway-service:
    build: ./gateway-service
    ports: ["3003:3003"]
    networks: ["app-net"]
    depends_on:
      - user-service
      - product-service
      - order-service
networks:
  app-net:
EOF


# Output 

<img width="1918" height="945" alt="image" src="https://github.com/user-attachments/assets/babc536f-5c0a-427b-aefa-36c5eff000c4" />

# Output of services

http://54.163.31.226:3000/

http://54.163.31.226:3001/

http://54.163.31.226:3003/
