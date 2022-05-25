"# Az_Nginx" 

# Este comando usa la extensión de script personalizado para ejecutar un script de Bash en la máquina virtual. El script se almacena en GitHub.

Mientras se ejecuta el comando, puede optar por examinar el script de Bash en una pestaña independiente del explorador.

En resumen, el script hace lo siguiente:

Ejecuta apt-get update para descargar la información más reciente del paquete desde Internet. Este paso ayuda a garantizar que el siguiente comando pueda encontrar la versión más reciente del paquete Nginx.
Instala Nginx.
Establece la página principal, /var/www/html/index.html, para que imprima un mensaje de bienvenida en el que se incluye el nombre de host de la máquina virtual.
# 

Creación de una máquina virtual Linux e instalación de Nginx
Use los comandos siguientes de la CLI de Azure para crear una máquina virtual Linux e instalar Nginx. Una vez creada la máquina virtual, usará la extensión de script personalizado para instalar Nginx. La extensión de script personalizado es una manera fácil de descargar y ejecutar scripts en máquinas virtuales de Azure. Es solo una de las numerosas formas de configurar el sistema después de que la máquina virtual esté en funcionamiento.

Desde Cloud Shell, ejecute el siguiente comando az vm create para crear una máquina virtual Linux:

az vm create \
  --resource-group learn-91ddade0-1cd2-4b0d-98da-b7d817178a0e \
  --name my-vm \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys


La máquina virtual tardará unos minutos en aparecer.

Asigne el nombre my-vm a la máquina virtual. Use este nombre para hacer referencia a la máquina virtual en los pasos posteriores.

Ejecute el siguiente comando az vm extension set para configurar Nginx en la máquina virtual:

az vm extension set \
  --resource-group learn-91ddade0-1cd2-4b0d-98da-b7d817178a0e \
  --vm-name my-vm \
  --name customScript \
  --publisher Microsoft.Azure.Extensions \
  --version 2.1 \
  --settings '{"fileUris":["https://github.com/rgjtokiota/Az_Nginx/blob/main/configure-nginx.sh"]}' \
  --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'

