#### Para uso en desarrollo (Dockerfile)

```dockerfile
FROM node:18

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm install

COPY . .

EXPOSE 4200

CMD ["npm", "start"]
```

Usando Node.js sin compilar. Puerto 4200 en modo desarrollo.

#### Para uso en desarrollo (docker-compose.yml)

```yml
services:
	angular-app:
		build: .
		ports:
			- "4200:4200"
		volumnes:
			- .:/app
			- /app/node_modules
		environmnet:
			- CHOKIDAR_USEPOLLING=true
		command: npm start
```

(Con `CHOKIDAR_USEPOLLING` Angular detecta cambios en entornos como Docker en Windows)

#### Servir aplicación Angular en Nginx

- Usa **Node.js** para instalar dependencias y compilar el proyecto.
- Usa **Nginx** para servir la aplicación en producción.
- Expone el puerto **80** para servir la aplicación en un contenedor liviano.

```yaml
# -------CONSTRUCCION DEL PROYECTO CON NodeJs-------
FROM node:18 AS build

WORKDIR /app # Se establece el directorio de trabajo

COPY package.json package-lock.json ./  # Se copian los ficheros package.json para aprovechar la cache de Docker y no reinstalar dependencias innecesariamente

RUN npm install # Se instalan las dependencias del proyecto basadas en packages.json (se genera la carpeta node_modules en el contenedor)

COPY . . # Se copia todo el contenido fuente de la app al contenedor en /app

RUN npm run build --prod # Se ejecuta el build de Angular en modo produccion

# -------SERVIR APLICACION CON NGINX-------
FROM nginx:alpine 

COPY --from=build /app/dist/tu-proyecto-angular /usr/share/nginx/html # Se copian los archivos estáticos generados en build a la carpeta de Nginx donde se sirven los archivos

COPY nginx.conf /etc/nginx/conf.d/default.conf # Copiar configuración personalizada de Nginx (opcional)

EXPOSE 80 # Se servira la app en el puerto 80

CMD ["nginx", "-g", "daemon off;"] # Arranca Nginx en modo "foreground" (`daemon off;`), lo que mantiene el contenedor en ejecución.
```



Para obligar al `docker-compose` a generar la imagen de nuevo: 
```
docker-compose up --build -d
```