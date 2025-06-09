# Build stage
FROM golang:1.24-alpine as builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o /readiness-condition-reporter ./cmd/readiness-condition-reporter

# Final stage
FROM alpine:latest
COPY --from=builder /readiness-condition-reporter /readiness-condition-reporter

ENTRYPOINT ["/readiness-condition-reporter"]
