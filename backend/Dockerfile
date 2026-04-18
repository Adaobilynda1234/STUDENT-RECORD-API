# Use lightweight Node image
FROM node:18-alpine

WORKDIR /app

# Copy dependency files first (for caching)
COPY package*.json ./

# Install dependencies 
RUN npm install

# Copy rest of the code
COPY . .

# Expose backend port
EXPOSE 5000

# Start server
CMD ["npm", "start"]