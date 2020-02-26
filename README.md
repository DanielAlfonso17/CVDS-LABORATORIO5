# CVDS Laboratorio 5
# Escuela Colombiana de Ingenieria Julio Garavito 
# Daniel Felipe Alfonso Bueno 

## Parte I. - Jugando a ser un cliente HTTP
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

Realice una nueva conexión con telnet, esta vez a:

    Host: www.httpbin.org
    Puerto: 80
    Versión HTTP: 1.1

Ahora, solicite (GET) el recurso /html. ¿Qué se obtiene como resultado?
![](https://github.com/DanielAlfonso17/CNYT-2019-2/blob/master/4.png)

Obtenemos como resultado el codigo 200 que significa que la solicitud ha tenido exito en este caso el recurso se ha obtenido de manera correcta 

El archivo HTML tiene 3741 palabras usando el comando wc -c 

_¿Cuál es la diferencia entre los verbos GET y POST? ¿Qué otros tipos de peticiones existen?_
HTTP define un conjunto de métodos de petición para indicar la acción que se desea realizar para un recurso determinado.
##### GET 
solicita una representación de un recurso específico. Las peticiones que usan el método GET sólo deben recuperar datos.
##### POST 
se utiliza para enviar una entidad a un recurso en específico, causando a menudo un cambio en el estado o efectos secundarios en el servidor.
##### HEAD 
pide una respuesta idéntica a la de una petición GET, pero sin el cuerpo de la respuesta.
##### PUT 
reemplaza todas las representaciones actuales del recurso de destino con la carga útil de la petición.
##### DELETE 
borra un recurso en específico.
##### CONNECT 
establece un túnel hacia el servidor identificado por el recurso.
##### TRACE
realiza una prueba de bucle de retorno de mensaje a lo largo de la ruta al recurso de destino.
##### OPTIONS 
 es utilizado para describir las opciones de comunicación para el recurso de destino.
 
 
¿Cuáles son las diferencias con los diferentes parámetros curl -v y -i?
- El comando curl -v nos muestra una informacion completa de la peticion GET realizada y el estado de la peticion en este caso 200 exitosa
- El comando curl -i nos muestra solo la informacoin completa del estado de la peticion en este caso 200 

## Parte II. - Haciendo una aplicación Web dinámica a bajo nivel.
![](https://github.com/DanielAlfonso17/CNYT-2019-2/blob/master/5.png)

Teniendo en cuenta las siguientes métodos disponibles en los objetos ServletRequest y ServletResponse recibidos por el método doGet:

    response.setStatus(N); <- Indica con qué código de error N se generará la respuesta. Usar la clase HttpServletResponse para indicar el           
    código de respuesta.
    request.getParameter(param); <- Consulta el parámetro recibido, asociado al nombre ‘param’.
    response.getWriter() <- Retorna un objeto PrintWriter a través del cual se le puede enviar la respuesta a quien hizo la petición.
    response.setContentType(T) <- Asigna el tipo de contenido (MIME type) que se entregará en la respuesta.

Implemente dicho método de manera que:

    Asuma que la petición HTTP recibe como parámetro el número de id de una lista de cosas por hacer (todo), y que dicha identificación es  
    un número entero.

    Con el identificador recibido, consulte el item por hacer de la lista de cosas por hacer, usando la clase "Service" creada en el punto.
![](https://github.com/DanielAlfonso17/CNYT-2019-2/blob/master/6.PNG)

Recompile y ejecute la aplicación. Abra en su navegador en la página del formulario, y rectifique que la página hecha anteriormente sea mostrada. Ingrese los datos y verifique los resultados. Cambie el formulario para que ahora en lugar de POST, use el método GET . Qué diferencia observa?
Creamos nuestro formulario 
![](https://github.com/DanielAlfonso17/CNYT-2019-2/blob/master/7.PNG)
Con el metodo _GET_ lleva los datos de forma "visible" al cliente (navegador web). El medio de envío es la URL. Los datos los puede ver cualquiera. Esto podria significar un peligro de confidencialidad de los datos 
![](https://github.com/DanielAlfonso17/CNYT-2019-2/blob/master/8.PNG)
Con el metodo _POST_ consiste en datos "ocultos" (porque el cliente no los ve) enviados por un formulario cuyo método de envío es post. Es adecuado para formularios. Los datos no son visibles.
![](https://github.com/DanielAlfonso17/CNYT-2019-2/blob/master/9.PNG)

¿Qué se está viendo? Revise cómo están implementados los métodos de la clase Service.java para entender el funcionamiento interno.

En la clase Service encontramos 3 metodos: 
- getTodo: Nos permite obtener todos los datos que necesitamos en este caso Id, UserId, Title, Completed pero esta información está en JSON (JavaScrip Object Notation) y luego por medio de Google Gson nos permite pasar de una representación JSON a un objeto java.

todoToHTMLRow y todosToHTMLTable lo que nos permite es coger los objetos java que transformamos en el método anterior y convertirlos en HTML con un estilo de tabla para que el navegador nos pueda mostrar esta información.
