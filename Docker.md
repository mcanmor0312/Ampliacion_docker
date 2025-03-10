# Ampliación DOCKER

## Nombre: Marcos Canto Moreno

## Preámbulo

1. **Instalar Docker y realizar los pasos post-instalación**

    ```bash
    sudo apt update  # Actualiza la lista de paquetes
    sudo apt install docker.io -y  # Instala Docker
    sudo systemctl enable --now docker  # Habilita y arranca el servicio Docker
    sudo usermod -aG docker admin  # Añade el usuario 'admin' al grupo Docker
    ```

    ![Instalación de Docker](images/captura1.png)

2. **Instalar servidor Samba y exponer la carpeta home**

    ```bash
    sudo apt install samba -y  # Instala Samba
    sudo smbpasswd -a admin  # Crea una contraseña para el usuario 'admin' en Samba
    sudo systemctl enable --now smbd  # Habilita y arranca el servicio Samba
    ```

    ![Samba](images/captura2.png)

3. **Descargar las imágenes necesarias**

    ```bash
    docker pull php:7.4-apache  # Descarga la imagen de PHP con Apache
    docker pull mariadb:latest  # Descarga la imagen de MariaDB
    ```

    ![Descarga de imágenes](images/captura3.png)

4. **Comprobar que se pueden crear contenedores**

    ```bash
    docker run --rm php:7.4-apache php -v  # Ejecuta un contenedor de PHP y muestra la versión
    docker run --rm mariadb:latest --version  # Ejecuta un contenedor de MariaDB y muestra la versión
    ```

    ![Ejecución de los contenedores de prueba](images/captura4.png)

---

## Ejercicio 1: Desplegar un servidor WordPress en el puerto 8181

1. **Crear las carpetas necesarias**

    ```bash
    mkdir -p ~/Music/docker1/wp  # Crea la carpeta para los archivos de WordPress
    mkdir -p ~/Music/docker1/data  # Crea la carpeta para los datos de MariaDB
    ```

    ![Creación de las carpetas](images/captura5.png)

2. **Crear el archivo `compose.yml`**

    ![Archivo compose.yml](images/captura6.png)

3. **Lanzar los servicios simultáneamente**

    ```bash
    docker-compose -f ~/Music/docker1/compose.yml up -d  # Levanta los servicios definidos en el archivo compose.yml
    ```

    ![Ejecución del comando docker-compose](images/captura7.png)

---

## Ejercicio 2: Replicar el WordPress en los puertos 8282 y 8383

1. **Copiar y modificar `compose.yml` para los nuevos entornos**

    ```bash
    cp ~/Music/docker1/compose.yml ~/Music/docker1/compose_8282.yml  # Copia el archivo compose.yml para el puerto 8282
    cp ~/Music/docker1/compose.yml ~/Music/docker1/compose_8383.yml  # Copia el archivo compose.yml para el puerto 8383
    ```

    ![Nuevos entornos](images/captura8.png)

2. **Editar `compose_8282.yml` para cambiar nombres de contenedores y puertos:**

    ![Ejecución del comando docker-compose](images/captura9.png)

3. **Repetir el proceso para `compose_8383.yml` cambiando los nombres a `db3` y `web3` y asignando el puerto `8383:80`.**

4. **Lanzar los nuevos entornos con los siguientes comandos:**

    ```bash
    docker-compose -f ~/Music/docker1/compose_8282.yml up -d  # Levanta los servicios definidos en el archivo compose_8282.yml
    docker-compose -f ~/Music/docker1/compose_8383.yml up -d  # Levanta los servicios definidos en el archivo compose_8383.yml
    ```

    ![Contenedores en ejecución en los puertos 8181, 8282 y 8383](images/captura10.png)

---

## Verificación

Para comprobar que los tres WordPress están en funcionamiento:

```bash
docker ps  # Muestra los contenedores en ejecución
```

![Contenedores corriendo](images/captura11.png)

Gracias por ver
