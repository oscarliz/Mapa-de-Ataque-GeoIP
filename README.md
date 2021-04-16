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
