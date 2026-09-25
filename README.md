# Guia de Instalacion y Optimizacion Adaptador USB Wi-Fi 6 AIC8800-en-Linux-Mint
Información del DispositivoModelo: Adaptador USB Wi-Fi 6 AX900 (Wi-Fi + Bluetooth).   Fabricante / Editor: Keroro Technology Ltd.   Chipset interno: AICSemi AIC8800.   Identificador en modo disco: 1111:1111 Pandora International Ltd. 88M80.
Guía de Instalación y Optimización: Adaptador USB Wi-Fi 6 (AIC8800) en Linux MintInformación del DispositivoModelo: Adaptador USB Wi-Fi 6 AX900 (Wi-Fi + Bluetooth).   Fabricante / Editor: Keroro Technology Ltd.   Chipset interno: AICSemi AIC8800.   Identificador en modo disco: 1111:1111 Pandora International Ltd. 88M80.   

Paso 1: Instalar dependencias del sistemaAbre la terminal (Ctrl + Alt + T) con conexión a internet previa (vía cable Ethernet o compartiendo datos por USB desde un teléfono) e instala las herramientas necesarias: 

sudo apt update && sudo apt install -y build-essential dkms git linux-headers-$(uname -r) usb-modeswitch.

Paso 2: Descargar e instalar el controladorClona el repositorio optimizado para la variante del chip AIC8800 y ejecuta la instalación:

git clone https://github.com/shenmintao/aic8800d80.git
cd aic8800d80
sudo ./install.sh

Nota: La instalación compila el módulo aic8800_fdrv mediante DKMS. Esto garantiza que el controlador se recompilará automáticamente si Linux Mint actualiza el kernel en el futuro.   

Paso 3: Reiniciar el equipoAl finalizar la compilación, reinicia el sistema para registrar los cambios en la memoria:   

sudo reboot

Pasos Adicionales Opcionales (Solución de problemas y estabilidad) estos pasos son recomendados si el adaptador se desconecta durante transferencias pesadas o si al encender la PC no muestra las redes de inmediato.

Opciónes= 

-opcion A: Desactivar el ahorro de energía USB (Evita apagos por carga alta)Linux Mint puede suspender la energía del puerto USB al detectar picos de consumo o tráfico intenso (por ejemplo, durante pruebas de velocidad). 

Para prevenir esto de forma permanente:
echo "options usbcore autosuspend=-1" | sudo tee /etc/modprobe.d/disable-usb-autosuspend.conf

-Opción B: Conmutación manual de modo (Si el adaptador se queda atascado como disco)Si al conectar el adaptador el sistema lo reconoce como una unidad virtual (1111:1111) y no activa el Wi-Fi, ejecuta estos dos comandos para forzar el paso a modo antena:  

sudo modprobe aic8800_fdrv
sudo usb_modeswitch -c /etc/usb_modeswitch.d/1111:1111

-Opción C: Cuidado térmico en pruebas de velocidadLos adaptadores USB ultra compactos no cuentan con disipación de calor dedicada. Realizar múltiples pruebas de velocidad (speedtests) consecutivas lleva el integrado al 100% de uso continuo, lo que activa la protección térmica del chip o del puerto. Para uso diario (navegación, descargas, streaming o juegos), el adaptador mantendrá un funcionamiento estable sin sobrecalentarse.
