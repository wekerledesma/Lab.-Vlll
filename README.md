PRÁCTICA 1: Instalación y Configuración de Docker con NGINX
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
Paso 2: Descargar la imagen de NGINX desde Docker Hub
sudo docker pull nginx
Paso 3: Crear un volumen para almacenar archivos persistentes
sudo mkdir -p /home/website
Paso 4: Crear un contenedor de NGINX con mapeo de puertos y volumen
sudo docker run -d -p 8888:80 \
    --name mi_nginx \
    -v /home/website:/usr/share/nginx/html \
    nginx
 Paso 5: Crear un archivo HTML en el volumen compartido
echo "<h1>Mi Nombre: [Tu Nombre]</h1> <h2>Matrícula: [Tu Matrícula]</h2>" | sudo tee /home/website/index.html
 Paso 6: Verificar que la página se muestra en el navegador
Abre:
http://127.0.0.1:8888


PRÁCTICA 2: Instalación y Uso de Portainer
Paso 1: Descargar la imagen de Portainer desde Docker Hub
sudo docker pull portainer/portainer-ce
 Paso 2: Crear un volumen de datos para Portainer
sudo docker volume create portainer_data
 Paso 3: Crear y ejecutar el contenedor de Portainer
sudo docker run -d -p 9000:9000 \
    --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce
Paso 4: Ingresar a la interfaz de Portainer
Abre el navegador e ingresa:
http://127.0.0.1:9000
Configura un usuario y vincula el Docker Engine local.

 Paso 5: Detener el contenedor de NGINX desde Portainer
Inicia sesión en Portainer.

Busca el contenedor "mi_nginx".

Haz clic en "Stop" para detenerlo.

También puedes hacerlo por terminal:
sudo docker stop mi_nginx
 Paso 6: Verificar que la página ya no está disponible
Intenta acceder nuevamente a:
http://127.0.0.1:8888
