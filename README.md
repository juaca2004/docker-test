
Quiz
En mi Dockerfile, primero utilizo un contenedor de Node.js en este caso la version 18 y establezco /app como directorio de trabajo. Allí copio primero mis archivos de dependencias (package.json y package-lock.json) y ejecuto npm install para instalar los paquetes. Luego copio todo mi proyecto al contenedor y ejecuto npm run build, generando la carpeta build con los archivos listos para producción. Después cambio a un contenedor de Nginx y copio desde la etapa de Node la carpeta build hacia /usr/share/nginx/html, que es donde Nginx sirve los archivos estáticos; finalmente, expongo el puerto 80 y configuro Nginx para ejecutarse en primer plano al iniciar el contenedor.

En la siguiente parte, se creo el .yml para el flujo el trabajo, configuro un flujo que se ejecuta cada vez que hago push a la rama main. Primero, ejecuto un job llamado build sobre un runner ubuntu-latest. Dentro del job, hago varios pasos: primero hago el checkout de mi repositorio para tener acceso a los archivos; luego configuro Docker Buildx para poder construir imágenes multiplataforma; después hago login en Docker Hub usando mis secretos (DOCKER_USERNAME y DOCKER_PASSWORD) para poder subir la imagen; y finalmente construyo y subo la imagen Docker usando el contexto actual y etiquetándola con mi usuario de Docker Hub y el nombre docker-test:latest.



