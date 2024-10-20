# Tarea 3 SXE -- Pedro Piñeiro
## 1. Descarga la imagen 'httpd' y comprueba que está en tu equipo
### Para descargar la imagen (concretamente la version 2.4) usamos
```
docker pull httpd:2.4
```
### Comprobamos que la imagen está en nuestro equipo con
```
docker images httpd
```


## 2. Crea un contenedor con el nombre 'dam_web1'
### Lo creamos con
```
docker run -d --name dam_web1 httpd:2.4 
```
### Comprobamos que se ha creado con
```
docker ps
```


## 3. Si quieres poder acceder desde el navegador de tu equipo, ¿que debes hacer?Utiliza bind mount para que el directorio del apache2 'htdocs' esté montado un directorio que tu elijas
### Primero hay que eliminar el contenedor para crear otro con el puerto mapeado, esto lo hacemos con
```
docker stop dam_web1
docker rm dam_web1
```
### Creamos un directorio en nuestro host y creamos el contenedor
```
mkdir /home/pedro/hostApache
docker run -d --name dam_web1 -p 8000:80 httpd:2.4
```
### Ahora creamos el contenedor con el bind mount
```
sudo docker run -d --name dam_web1 -p 8000:80 -v /home/pedro/hostApache:/usr/local/apache2/htdocs httpd:2.4
```



## 4. Realiza un 'hola mundo' en html y comprueba que accedes desde el navegador.
### Creamos el archivo index.html en el directorio hostApache
```
echo "<h1>Hola Mundo</h1>" > /home/pedro/hostApache/index.html
```
### Comprobamos que accedemos desde el navegador con
```
http://localhost:8000
```


## 5. Crea otro contenedor 'dam_web2' con el mismo bind mount y a otro puerto, por ejemplo 9080
### Creamos el contenedor con el bind mount y en el puerto 9080
```
sudo docker run -d --name dam_web2 -p 9080:80 -v /home/pedro/hostApache:/usr/local/apache2/htdocs httpd:2.4
```
### Comprobamos que se ha creado con
```
docker ps
```


## 6. Comprueba que los dos servidores 'sirven' la misma página, es decir, cuando consultamos en el navegador
### En el navegador accedemos a
```
http://localhost:8000
http://localhost:9080
```
### Y comprobamos que vemos el mismo contenido en ambos



