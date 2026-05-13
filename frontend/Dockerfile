# ==========================================
# ETAPA 1: Preparación (Builder)
# ==========================================
FROM alpine:latest AS builder
WORKDIR /app
# Copiamos los archivos estáticos
COPY index.html app.js ./

# ==========================================
# ETAPA 2: Servidor Web Nginx (No Root)
# ==========================================
FROM nginxinc/nginx-unprivileged:alpine

# Cambiamos temporalmente al usuario root para tener permisos de escritura y borrado
USER root

# Limpiamos el contenido por defecto
RUN rm -rf /usr/share/nginx/html/*

# Copiamos desde la etapa builder
COPY --from=builder /app/index.html /app/app.js /usr/share/nginx/html/
COPY default.conf /etc/nginx/conf.d/default.conf

# Asignamos la propiedad de los archivos al usuario nginx para evitar problemas de permisos al servir la web
RUN chown -R nginx:nginx /usr/share/nginx/html /etc/nginx/conf.d

# Volvemos al usuario seguro 'nginx' (no root)
USER nginx

# Exponemos el puerto 8080 (los usuarios no root no pueden usar puertos menores a 1024)
EXPOSE 8080

# Despertando a GitHub frontend

# Despertando a GitHub frontend 2.0