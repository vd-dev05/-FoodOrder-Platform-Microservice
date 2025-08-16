# FROM golang:1.24.5  AS builder
# WORKDIR /app
# COPY go.mod ./
# RUN go mod tidy
# COPY . .
# RUN go build -o gateway .

# FROM alpine:3.19
# WORKDIR /app
# COPY --from=builder /app/gateway .
# EXPOSE 8080
# CMD ["./gateway"]



# Stage 1: Build binary
FROM golang:1.24.5 AS builder
WORKDIR /app

# Copy go mod files first (để cache dependency)
COPY go.mod ./ go.sum* ./
# COPY go.sum ./
RUN go mod download 

# Copy toàn bộ source và build
COPY . .
RUN go build -o gateway .

# Stage 2: Chạy binary
FROM alpine:3.19
WORKDIR /app
COPY --from=builder /app/gateway .
EXPOSE 8080
CMD ["./gateway"]
