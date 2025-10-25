# Step 1: Use official Golang image
FROM golang:1.21-alpine

# Step 2: Set working directory
WORKDIR /app

# Step 3: Copy the Go source code into the container
COPY main.go .

# Step 4: Build the Go application
RUN go build -o server main.go

# Step 5: Expose port 8080
EXPOSE 8080

# Step 6: Run the Go server
CMD ["./server"]
