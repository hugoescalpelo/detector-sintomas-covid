# detector-sintomas-covid
Este repositorio contiene todo lo necesario para realizar un detector de síntomas COVID con NodeRed, ESP32CAM, el sensor MAX30100, el sensor MLX90614 y MySQL

## Introducción
Este ejercicio consiste en realizar una detector de sintomas COVID.

- Obtiene información de los siguientes sensores con ayuda del ESP32CAM por WiFi
    - Sensor de oxigenacion y ritmo cardiaco MAX30100
    - Sensor de temperatura infrarrojo MLX90614
- El micro controlador envía la información de los sensores por MQTT de forma local con un mensaje JSON.
- Se cuenta con un Flow en NodeRed que obtiene la información del micro controlador por MQTT y muestra sus valores en un dashboard
- El dashboard del Flow incluye una sección para que el paciente ponga sus nombre y correo
- El dashboard cuenta con un boton que toma captura de los datos y realiza un proto diagnostico

#### Importante:

Este flow no realiza un diagnostico médico, su proposito es realizar una consulta de los signos vitales del paciente y comprobar que se encuentren en un rango saludable. Este flow realiza un "proto diagnostico", el cual sugiere al paciente ir con un médico en caso de encontrar algo fuera de lo común.

#### Limitantes

- Este proyecto tiene como limitante las capacidades de prototipado de los sensores usados. 
- Es importante contextualizar las dificultades de la lectura del ritmo cardiaco y oxigenación, el fabricante del sensor sugiere que este sea ajustado a un dedo con una banda elástica y que el sensor se encuentre suspendido en el aire, debido a que el pulso y el peso de la mano pueden alterar las lecturas
- El sensor de temperatura infrarrojo es sensible a la luz ambiental


### Material Necesario

Para realizar este ejercicio necesitarás contar con lo siguiente:

- Micro controlador ESP32CAM
- Convertidor de niveles FTDI
- Cable USB-A a USB-mini
- Jumpers MM
- Protoboard
- Sensor MAX30100
- Sensor MLX90614

### Software necesario

Para poder hacer funcionar este proyecto, es necesario contar con el siguiente software:
- [Ubuntu 20.04](https://releases.ubuntu.com/20.04/)
- [Arduino IDE](https://www.arduino.cc/en/software)
    - [Gestor de tarjetas ESP32](https://github.com/iotechbugs/esp32-arduino/blob/master/docs/arduino-ide/boards_manager.md)
    - [Configuración de la IDE de Arduino para trabajar con el ESP32CAM](https://github.com/iotechbugs/esp32-arduino)
    - [Biblioteca PubSubClient](https://github.com/knolleary/pubsubclient)
- [Mosquitto MQTT Broker](https://mosquitto.org/download/)
    - [Listener en puerto 1883 para 0.0.0.0 y conexiones no autentificadas activadas](https://mosquitto.org/man/mosquitto-conf-5.html)
- [NodeJS](https://nodejs.org/es/)
    - [NPM](https://www.npmjs.com/)
    - [NodeRed](https://nodered.org/docs/getting-started/local)
    - [Nodos Dashboard: node-red-dashboard](https://flows.nodered.org/node/node-red-dashboard)
    - [Nodos MySQL: node-red-node-mysql](https://flows.nodered.org/node/node-red-node-mysql)
    - [Nodos eMail: node-red-node-email](https://flows.nodered.org/node/node-red-node-email)
- [MySQL Server](https://dev.mysql.com/doc/mysql-getting-started/en/)

### Material de referencia

En los siguientes enlaces puedes encontrar cursos en la plataforma de edu.codigoiot.com que te permitirán realiar las configuraciones necesarias

- [Instalación de Virutal Box y Ubuntu 20.04](https://edu.codigoiot.com/course/view.php?id=812)
- [Configuración de Arduino IDE para ESP32CAM](https://edu.codigoiot.com/course/view.php?id=850)
- [Instalación de NodeRed](https://edu.codigoiot.com/course/view.php?id=817)
- [Introducción a NodeRed](https://edu.codigoiot.com/course/view.php?id=278)
- [Instalación de Mosquitto MQTT](https://edu.codigoiot.com/course/view.php?id=818)
- [Instalación de MySQL](https://edu.codigoiot.com/course/view.php?id=294)
- [Medición de indicadores COVID](https://edu.codigoiot.com/course/view.php?id=805)

## Instrucciones

### Requisitos previos
Para realizar este ejercicio necesitas cumplir con los siguientes requisitos previos

1. Tener configurado en entorno de desarrollo. Para esto es necesario contar con la IDE de Arduino configurada para poder cargar programas al ESP32CAM
2. Entorno de NodeJS configurado para trabajar con NodeRed. Deberás tener agregados los nodos Dashboard, nodos MySQL y nodos eMail.
3. Entorno de Mosquitto MQTT configurado. Deberás tener modificado el archivo mosquitto.conf para que acepte conexiones externas y no autentificadas. Deberás tener el firewall de Ubuntu abierto para permitir conexiones en el puerto 1883.

### Instrucciones de preparación de entorno
Para poder configurar tu entorno y realizar este ejercicio, encesitas lo siguiente

1. Realiza el circuito. Las instrucciones se encuentran en el encabezado del código para el ESP32CAM. Deberás cambiar lo siguiente:
    - El tema de publicación y suscripción
    - Nombre de red y contraseña al que deseas conectarte
    - Tiempo de espera entre envío de datos en milisegundos
2. Arrancar NodeRed y cargar el Flow. Deberás modificar lo siquiente:
    - Temas MQTT a reportar. Deberás ajustarlos de acuerdo a tus fines
    - Coordenadas. Deberás actualizar las coordenadas geográficas usadas para hacer la petición por API a OpenWheatherMap
    - API Key. Deberás generar tus propias API Keys para hacer uso del servicio de OpenWeatherMap
    - Temperatura umbral para envíar señal de encendido del LED Flash para indicar sobre temperatura
3. Energiza el circuito. Asegurate de energizar el circuito realizado y de que este se encuentre en rango de la red de WiFi seleccionada

### Instrucciones de operación

Para observar el funcionamiento de este ejercicio, es necesario que abras el dashboard. Generalmente puedes encontrarlo en http://localhost:1880/ui desde la computadora que ejecuta NodeRed.

## Resultado

A continuación puedes observar una vista previa del resultado de este ejercicio. La captura de pantalla presente fue tomada durante el [Diplomado Internet de las Cosas](https://www.codigoiot.com/curso/seminario-iot-de-samsung-innovation-campus/) de [CódigoIoT](https://www.codigoiot.com), motivo por el cual se pueden ver múltiples gráficas de múltples alumnos reportandose.

![Vista previa](https://github.com/hugoescalpelo/esp32cam-dht11-g7/blob/main/Dashboard%20estacion%20climatica%20API%20y%20Sensores.png?raw=true)

# Evidencias
A continuación puedes ver enlaces a las evidencias de este proyecto

- [Repositorio](https://github.com/hugoescalpelo/esp32cam-dht11-g7)
- [Youtube](https://youtu.be/q8GJ5GMVQMY)
- [TikTok](https://www.tiktok.com/@hugoescalpelo/video/7135200073343896837)



# FAQ

- **P: ¿Porque no se conecta el ESP32CAM a mi WiFi?**
    **R:** Verifica que hayas colocado correctamente tu SSID y contraseña
    **R:** Verifica que tu red tenga una conexión AES-WPA2
    **R:** Asegurate que el micro controlador se encuentra en el rango de alcance de tu red WiFi
- **P: ¿Que significa el error BrownOut?**
    **R:** Significa que tu micro controlador tiene sobre carga de ruido o le falta potencia de alimentación. Intenta moverlo un poco o conectarlo en un puerto USB3.0 diferente
- **P: ¿Porqué no puedo ver la información en las gráficas del Dashboard?**
    **R:** Verifica que hayas escrito los mismos temas en los suscriptores y en los publicadores tanto de flow como del programa del ESP32CAM
    **R:** Asegurate de tener una regla que permita conexiones en el puerto 1883 y tener correctamente configurado el archivo mosquitto.conf
    **R:** Asegurate de buscar la IP mas reciente del broker publico, esta es dinámica y cambia seguido

# Compatibilidad

Este código es directamente compatible con:
- Tarjeta de desarrollo ESP32CAM
- Sensor de temperatura y humedad DHT11

Con modificaciones menores, puede ser compatible con:
- Micro controladores de la familia ESP32
    - NodeMCU (probado)
    - ESP8266 (probado)
    - ESP32-S (probado)
- Sensor DHT22 (pendiente)

Con modificaciones mayores, puede ser compatible con:
- Micro controladores Arduino
    - Arduino UNO (pendiente)
    - Arduino MEGA (pendiente)
    - Arduino Leonardo (pendiente)

# Créditos

Desarrollado por Hugo Escalpelo
- [hugoescalpelo.com](https://hugoescalpelo.com/)
- [Página en Facebook](https://www.facebook.com/Hugo-Escalpelo-Profesional-337708683840136)
- [GitHub](https://github.com/hugoescalpelo)