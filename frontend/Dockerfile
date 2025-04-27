# Étape 1 : Build Angular
FROM node:18 AS build
WORKDIR /app
COPY frontend/package.json frontend/package-lock.json ./
RUN npm install
COPY frontend/ .
RUN npm run build --prod

# Étape 2 : Serveur NGINX pour les fichiers statiques
FROM nginx:alpine
COPY --from=build /app/dist/frontend /usr/share/nginx/html
COPY frontend/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80