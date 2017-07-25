# Denial service #


 Los ataques DoS de amplificación de tráfico son capaces de generar una condición DoS al consumir el
 Ancho de banda de red que está disponible para un servidor, dispositivo o red en particular. Dos condiciones 
 Son necesarios para que un ataque de amplificación de tráfico tenga éxito. Estas condiciones son las siguientes:
 
 *Redirección*: Un atacante debe poder solicitar una respuesta que pueda ser redirigida a una Víctima. 
   Esto generalmente se logra mediante la suplantación de identidad IP. Como UDP no es un Protocolo orientado a conexión,
   a mayoría de los protocolos de capa de aplicación que usan UDP como
   Protocolo de capa de transporte se puede utilizar para redirigir las respuestas de servicio a otros Peticiones falsas.

 *Amplificación*: La respuesta redireccionada debe ser de mayor tamaño que la solicitud que inicial
   Cuanto mayor sea el tamaño en bytes de la respuesta, más exito el ataque será.
   
   
 # Protocolo UDP #
   
   El protcolo UDP no es un protocolo orientado a la conexion, aqui nace el primer problema
   
   "Toda implementación TCP/IP que no se use exclusivamente para ruteo incluye UDP"
   "UDP no otorga garantías para la entrega de sus mensajes (por lo que realmente no se debería encontrar en la capa 4) "
   
   Por lo tan to UDP, no necesita establecer un conexion a priori para el intercambio de paquetes, por ende, este no sanitiza  ni          comprueba el origen y confiabilidad del emisor, lo que lo hace totalmente vulnerable a suplantacion de identidad.
   
   gracias  a lo anterior es posible realizar los siguiente ataques, que resultaran en una denegacion de servicio, siendo capaz de       
   rediriguir trafico a una maquina especifica.
   
   
 # ftp_fuzzy.py #
   
   En general, los desbordamientos de búfer son capaces de causar una denegación de servicio, porque
   Pueden dar lugar a que se carguen datos arbitrarios en segmentos de memoria no deseados. Esta
   Puede interrumpir el flujo de ejecución y resultar en un bloqueo del servicio o del sistema operativo.
   
   ftp_fuzzy.py solo intenta encontrar un desbordamiento de buffer en algun comando usado en consola, ingresando un payload
   cabe destacar que la conexion al ftp,  en este es script se hace de forma remota con ayuda de la libreria socket
   
   
 # Dos_icmp.py #
    
  Cuando hacemos un ping hacia una maquina, lo que en realidad sucede, es que enviamos una solicitud echo request, por lo tanto 
  si la maquina objetivo se encuentra activa, y libre de algun firewall, deberia responde con un echo reply
    
    
  ![alt-text](img/icmp.png) 
    
    
  **Ddos con respuestas tipo echo reply**
    
  ![alt-text](img/icmp2.png) 
  
  
  
 # Dos_dns.py #
 
 La denegacion de servicio por medio de peticiones al servidor DNS, cumple con las dos condicione necesarias para que el ataque se lleve   a cabo.
 
  * Primero, trabaja con el protocolo UDP, por lo tanto podremos spoofear la ip de origen
  * Segunfo, la respuesta en bytes es mucho mas grande, que la peticiones realizada
  
  La peticion para averiguar los diferentes registro DNS asociados a un dominio o IP, suelen responder con registros de direccion,         registro de dirección IPv6,Registro de servidor de nombres, registros de punteros entre otros.
  
  Lo que reprentaria en bytes un tamaño mayor a la solicitud enviada, si logramos redireccionar esa respuesta a un equipo especifico y     ademas lo hacemos indefinidamente, es muy probable que el sistema sufra fallos, a causa del trafico entrante
  
  
    ![alt-text](img/dns1.png)
  
   **Ddos con respuestas DNSRR**
   
    ![alt-text](img/dnsa.png)
  
  
  
  
  
  
   
 
 
    
  
   