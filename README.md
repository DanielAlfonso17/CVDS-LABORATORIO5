# CVDS Laboratorio 5
# Escuela Colombiana de Ingenieria Julio Garavito 
# Daniel Felipe Alfonso Bueno 

Realice una conexión síncrona TCP/IP a través de Telnet al siguiente servidor:

    Host: www.escuelaing.edu.co
    Puerto: 80

Realizamos conexion con TELNET de la siguiente manera: 
![](https://github.com/DanielAlfonso17/CNYT-2019-2/blob/master/1.png)

Realizamos la peticion GET: 
    
    GET /sssss/abc.html HTTP/1.1
    Host: www.escuelaing.edu.co

![](https://github.com/DanielAlfonso17/CNYT-2019-2/blob/master/2.png)

Revise el resultado obtenido. ¿Qué codigo de error sale?, revise el significado del mismo en la lista de códigos de estado HTTP.
![](https://github.com/DanielAlfonso17/CNYT-2019-2/blob/master/3.png)

El resultado obtenido es el codigo error 301 que significa que el cliente debe tomar medidas adicionales para completar la solicitud realizada existen una variedad de opciones que el cliente puede elegir como: 
- 301 Movido permanentemente 
- 302 Encontrado (Anteriormente movido) 
- 303 Ver otro 
- 304 No modificado 
- 305 Usar proxy 

Qué otros códigos de error existen?, ¿En qué caso se manejarán?
### Codigos de Error: 
- Error 100: Esta respuesta provisional indica que todo hasta ahora está bien y que el cliente debe continuar con la solicitud o ignorarla si ya está terminada.
- Error 200: La solicitud ha tenido éxito. El significado de un éxito varía dependiendo del método HTTP:
  - GET: El recurso se ha obtenido y se transmite en el cuerpo del mensaje.
  - HEAD: Los encabezados de entidad están en el cuerpo del mensaje.
  - PUT o POST: El recurso que describe el resultado de la acción se transmite en el cuerpo del mensaje.
  - TRACE: El cuerpo del mensaje contiene el mensaje de solicitud recibido por el servidor.
- Error 400:Esta respuesta significa que el servidor no pudo interpretar la solicitud dada una sintaxis inválida.
- Error 500: El servidor ha encontrado una situación que no sabe como manejarla.

