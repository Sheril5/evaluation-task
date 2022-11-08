FROM golang:alpine as builder
WORKDIR /app
COPY go.mod ./
COPY go.sum ./
RUN go mod download

# Copy the source from the current directory to the working Directory inside the container 
COPY . .

RUN go build -o main .

FROM alpine:latest

WORKDIR /root/

COPY --from=builder /app/main .
COPY --from=builder /app/.env .

EXPOSE 8000

CMD [ "./main" ]
