# Step 1: Use official Node.js image
FROM node:18

# Step 2: Create app directory
WORKDIR /app

# Step 3: Create a simple Node.js server (multi-line echo using printf)
RUN printf "const http = require('http');\n\
const server = http.createServer((req, res) => {\n\
  res.writeHead(200, {'Content-Type': 'text/plain'});\n\
  res.end('Hello from Node.js container!');\n\
});\n\
server.listen(3000, () => console.log('Server running on port 3000'));\
" > server.js

# Step 4: Expose port 3000
EXPOSE 3000

# Step 5: Run the app
CMD ["node", "server.js"]
