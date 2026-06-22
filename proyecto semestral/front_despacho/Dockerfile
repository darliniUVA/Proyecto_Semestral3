# --- ETAPA 1: Construcción (Build) ---
FROM node:20-alpine AS builder
WORKDIR /app

# Copiamos archivos de dependencias e instalamos
COPY package*.json ./
RUN npm install

# Copiamos el resto del código y compilamos la app
COPY . .
RUN npm run build

# --- ETAPA 2: Producción (Imagen ultraliviana con Nginx) ---
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Limpiamos el contenido por defecto de nginx
RUN rm -rf ./*

# Copiamos los archivos estáticos compilados desde la etapa anterior
COPY --from=builder /app/dist .

# Requisito Pauta: Modificar permisos para que funcione con usuario No-Root
RUN touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid /var/cache/nginx /var/log/nginx /usr/share/nginx/html

# Cambiamos al usuario de privilegios mínimos
USER nginx

# Exponer el puerto estándar de Nginx
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]