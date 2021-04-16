# Mapa de ataque GeoIP 🌐

Visualización de mapas de ataques GeoIP de seguridad cibernética
Este visualizador de mapas de ataques geoip se desarrolló para mostrar los ataques de red en su organización en tiempo real. El servidor de datos sigue un archivo syslog y analiza la IP de origen, la IP de destino, el puerto de origen y el puerto de destino. Los protocolos se determinan a través de puertos comunes y las visualizaciones varían en color según el tipo de protocolo. HAGA CLIC AQUÍ para ver un video de demostración. Este proyecto no sería posible si no fuera por Sam Cappella, quien creó un visualizador de tráfico de red de competencia de ciberdefensa para el Concurso de Ciberdefensa de Palmetto 2015. Usé principalmente su código como referencia, pero tomé prestadas algunas funciones mientras creaba el servidor de visualización y los aspectos visuales de la aplicación web. También me gustaría agradecer especialmente a Dylan Madisetti por darme consejos sobre ciertos aspectos de mi implementación.

# Importante

Este programa se basa completamente en syslog, y debido a que todos los dispositivos dan formato a los registros de manera diferente, deberá personalizar las funciones de análisis de registros. Si su organización utiliza un sistema de gestión de eventos e información de seguridad (SIEM), probablemente pueda normalizar los registros para ahorrarle mucho tiempo escribiendo expresiones regulares.

###### NOTA: 

###### Debido a que no mantengo este proyecto, hay algunas características que probablemente no funcionan, por ejemplo, el mapa probablemente no se mostrará porque no pago por una clave API de MapBox legítima. Para solucionar este problema, probablemente tendrá que crear su propia cuenta MapBox y usar su propia clave.

* Envíe todo el syslog a SIEM.
* Utilice SIEM para normalizar los registros.
* Envíe registros normalizados a la caja (cualquier máquina Linux que ejecute syslog-ng funcionará) que ejecute este software para que el servidor de datos pueda analizarlos.

# Configuracion base

* Asegúrese en /etc/redis/redis.conf de cambiar bind 127.0.0.1 a bind 0.0.0.0 si planea ejecutar DataServer en una máquina diferente a AttackMapServer.
* Asegúrese de que la dirección WebSocket en /AttackMapServer/index.html apunte a la dirección IP del AttackMapServer para que el navegador conozca la dirección del WebSocket.
* Descargue la base de datos MaxMind GeoLite2 y cambie la variable db_path en DataServer.py al lugar donde almacene la base de datos.
./db-dl.sh
* Agregue la latitud / longitud de la sede a la variable hqLatLng en index.html
Utilice syslog-gen.py o syslog-gen.sh para simular tráfico ficticio "listo para usar".

###### IMPORTANTE: Recuerde, este código solo se ejecutará correctamente en un entorno de producción después de personalizar las funciones de análisis. La función de análisis predeterminada solo se escribe para analizar el tráfico ./syslog-gen.sh.

# Errores, comentarios y preguntas

Si encuentra algún error o error, hágamelo saber. Las preguntas y comentarios también son bienvenidos, y se pueden enviar a oscarliz2162@gmail.com, o abrir un problema en este repositorio.

# Implementacion
Probado en Ubuntu 16.04 LTS.


```
* Clone el repositorio: git clone https://github.com/matthewclarkmay/geoip-attack-map.git
```
```
* Instala Dependencias: sudo apt install python3-pip redis-server
```
```
* Instala los requerimientos de python: sudo pip3 install -U -r requirements.txt
```
```
* Iniciar el servidor: redis-server
```
```
* Configuracion del Data Server DB: cd DataServerDB
                                    ./db-dl.sh
                                    cd ..
```
```
* Iniciar el Data Server: cd DataServer
                          sudo python3 DataServer.py
```
* Start the Syslog Gen Script, inside DataServer directory:

  * Open a new terminal tab (Ctrl+Shift+T, on Ubuntu).
```
*     ./syslog-gen.py
      ./syslog-gen.sh
```
```
* Configuracion del Data Server DB: cd DataServerDB
                                    ./db-dl.sh
                                    cd ..
```

# Resultado Final

![2021-04-15 17-04-03_Trim_Trim](https://user-images.githubusercontent.com/46871300/115046633-af228680-9ea5-11eb-8975-ebd4f42bd6e9.gif)


## Contribuyendo 🖇️

Por favor lee el [CONTRIBUTING.md](https://gist.github.com/villanuevand/xxxxxx) para detalles de nuestro código de conducta, y el proceso para enviarnos pull requests.

## Autor ✒️

_Menciona a todos aquellos que ayudaron a levantar el proyecto desde sus inicios_

* **Oscar Encarnacion Liz** - *Trabajo Inicial* - [oscarliz](http://oscarliz.herokuapp.com/

## Licencia 📄

Este proyecto está bajo la Licencia (Tu Licencia) - mira el archivo [LICENSE.md](LICENSE.md) para detalles

## Expresiones de Gratitud 🎁

* Comenta a otros sobre este proyecto 📢
* Invita una cerveza 🍺 o un café ☕ a alguien del equipo. 
* Da las gracias públicamente 🤓.
* etc.

---
