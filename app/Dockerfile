# Stage 1: Build
FROM golang:1.21-alpine AS builder
# Установка зависимостей для сборки
RUN apk add --no-cache git
# Рабочая директория
WORKDIR /app
#-------------------------ЗАМЕНИЛ ЭТОТ БЛОК-----------------
# Копирование файлов зависимостей
#COPY go.mod ./
# Загрузка зависимостей
#RUN go mod download
#RUN go get containers-lab-1
# Копирование исходного кода
#COPY . .
#-----------------------------------------------------------
# Копирование файлов зависимостей и исходного кода
COPY go.mod ./
COPY . .

# Автоматический поиск и загрузка всех нужных пакетов (включая драйвер pq)
RUN go mod tidy    

# Сборка приложения
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .
# Stage 2: Final
FROM alpine:latest
# Установка CA сертификатов для HTTPS
RUN apk --no-cache add ca-certificates
# Рабочая директория
WORKDIR /root/
# Копирование собранного приложения из builder
COPY --from=builder /app/main .

# Копирование статических файлов
#COPY --from=builder /app/static ./static   УДАЛИЛИ ЭТУ СТРОКУ ТАК КАК СТАТИКОЙ ЗАНИМАЕТСЯ NGINX

# Экспонирование порта
EXPOSE 8080
# Запуск приложения
CMD ["./main"]