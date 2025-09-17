# --------- Stage 1: Build ---------
FROM golang:1.21 AS builder

WORKDIR /app

COPY go.mod ./

RUN go mod download

COPY . .

RUN go build -o hello-api main.go

# --------- Stage 2: Run ---------
FROM debian:bookworm-slim

RUN apt-get update && apt-get install -y ca-certificates && rm -rf /var/lib/apt/lists/*

WORKDIR /root/

COPY --from=builder /app/hello-api .

EXPOSE 8080

CMD ["./hello-api"]


#Stage แรก (golang:1.21) สำหรับ build binary เพราะมันมี Go compiler + tools ครบ
#Stage สอง (debian:bookworm-slim) สำหรับ run จริง debian:bookworm-slim ซึ่งเป็น Linux เบาๆ ไม่มี Go compiler