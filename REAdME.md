# Docker CMIT

## 1 Descargar codigo fuente.
descarge el codigo de cmit o realice un git clone es esta carpeta.
```bash
git clone <codigo-cmit-repo> cmit
```

## 3 modifique el docker compose
tiene que agregra la ruta completa a la carpeta cmit en la seccion de `volumenes:` en la seccion de my-app y composer-aux indicando la ruta ej: `'C:/Users/pepe/DOCKER-LARAVEL/cmit:/app'`.

## 5 ejecute el docker compose
ejecute `docker compose up -d` para levantar los servicios

## 6 composer install
el contenedor de composer va a realizar la instalacion de las dependencias del proyecto, el contenedor de myapp se iniciara luego de que se levante el contenedor de composer, mariadb y redis pero la instalacion lleva tiempo en realizarse. por lo que tendra que reiniciar el contenedor de myapp luego de que se finalize la instalacion.

## 7 configue el sistema
copie el script config.sh a la carpeta cmit (carpeta con la aplicacion)
luego identifique la aplicacion en docker usando `docker ps` vera algo como esto
```bash
CONTAINER ID   IMAGE                  COMMAND                  CREATED         STATUS         PORTS                              NAMES
84b9e35bd071   bitnami/laravel:10     "/opt/bitnami/script…"   3 minutes ago   Up 3 minutes   3000/tcp, 0.0.0.0:8000->8000/tcp   docker-laravel-myapp-1
4614b680f375   bitnami/mariadb:11.0   "/opt/bitnami/script…"   3 minutes ago   Up 3 minutes   3306/tcp                           docker-laravel-mariadb-1
bd918170c7b3   redis                  "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:6382->6379/tcp             docker-laravel-redis-1
```

ejecute `docker exec -it docker-larave-myapp-1 bash` esto le abrira una terminal interactiva donde podra ejecutar el siguiente comando `./config.sh` esto iniciara la configuracion del proyecto.

sino desde docker desktop en `container>docker-laravel>my-app` en la seccion de terminal podra ejecute `bash` y luego .`/config.sh`.