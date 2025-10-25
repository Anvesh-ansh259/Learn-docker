# Step 1: Use official Nginx image
FROM nginx:alpine

# Step 2: Remove default content
RUN rm -rf /usr/share/nginx/html/*

# Step 3: Copy your index.html into Nginx
COPY index.html /usr/share/nginx/html/

# Step 4: Expose port 80
EXPOSE 80

# Step 5: Start Nginx
CMD ["nginx", "-g", "daemon off;"]

