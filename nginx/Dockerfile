# Используем легковесный образ Nginx
FROM nginx:alpine

# Копируем конфигурационный файл Nginx с локальной машины внутрь образа
COPY nginx.conf /etc/nginx/nginx.conf

# Копируем HTML-файл с локальной машины в директорию, откуда Nginx раздает статику
COPY index.html /usr/share/nginx/html/index.html