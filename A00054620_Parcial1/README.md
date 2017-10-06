# Parcial 1

**Universidad ICESI**  
**Curso:** Sistemas Operativos  
**Docente:** Daniel Barragán C. 
**Tema:** Comandos de Linux, Virtualización  
**Correo:** daniel.barragan at correo.icesi.edu.co

**Fecha de entrega:** Domingo, 08 de octubre de 2017  
**Estudiante:** Juan Camilo Swan  
**Código:** A00054620  


### Objetivos
* Conocer y emplear comandos de Linux para la realización de tareas administrativas
* Virtualizar un sistema operativo
* Conocer y emplear capacidades de CentOS7 para la vitualización

### Prerrequisitos
* Virtualbox o WMWare
* Máquina virtual con sistema operativo CentOS7

### Descripción
El primer parcial del curso sistemas operativos trata sobre el manejo de los comandos de Linux, virtualización y el uso de las características de CentOS7

### Actividades
1. Incluir nombre, código (5%)
2. Ortografía y redacción cuando sea necesario (5%)
3. Resuelva los siguienes retos de la página https://cmdchallenge.com y presente la solución a cada uno de ellos a través de un ejemplo práctico en CentOS7. Presente capturas de pantalla relevantes como evidencias de lo realizado (20%)
  * sum_all_numbers
  * replace_spaces_in_filenames
  * reverse_readme
  * remove_duplicated_lines
  * disp_table
4. Realice un script que cumpla las condiciones que se describen a continuación. Presente capturas de pantalla relevantes como evidencias del funcionamiento (30%)
  * El usuario gutenberg debe existir en el sistema operativo
  * El script se debe ejecutar cada 5 minutos, consulte el manual de crontab
  * EL script debe descargar un libro del proyecto https://www.gutenberg.org/ en el directorio /home/gutenberg/mybooks
  * Si ya existe un libro en el directorio mybooks, debe ser reemplazado  
5. Describa el funcionamiento del código fuente rickroll.c del repositorio de github https://github.com/jvns/kernel-module-fun. Muestre el funcionamiento al compilar el código y cargarlo como un módulo del kernel a través de un video que deberá cargar en Youtube e incluir el enlace en el informe (30%). Se recomienda emplear el sistema operativo Ubuntu con interfaz gráfica para esta prueba.
6. El informe debe ser entregado en formato pdf a través del moodle y el informe en formato README.md debe ser subido a un repositorio de github. El repositorio de github debe ser un fork de https://github.com/ICESI-Training/so-exam1 y para la entrega deberá hacer un Pull Request (PR) respetando la estructura definida. El código fuente y la url de github deben incluirse en el informe (10%)  

### Solución
**3.** Los desafios presentes en https://cmdchallenge.com se solucionaron dos veces. La primera vez fueron solucionados en la consola virtual que nos brinda la aplicación web, Y la segunda vez fueron realizados en la maquina virtual con sistema operativo CentOS7. A continuación muestro la solución de cada uno de dichos desafios.  
  
* **sum_all_numbers:** Para realizar la suma de todos los numeros comprendidos en el archivo de texto investigué un poco y encontré que es posible realizarlo mediante la concatenación del comando 'cat' para leer el archivo de texto con otro comando capaz de realiar la suma, para esto empleé un filtro de JSON llamado jq; este recibe una entrada y la salida depende del parametro requerido, para este caso yo he utilizado una salida en forma de arreglo 'jq -s' y con el comando add le indico a jq que debe sumar todos los valores de dicho arreglo. Este proceso fue realizado en la consola virtual sin ningún problema, pero para realizarlo en la consola de CentOS7 se necesitó realizar la instalación del 'jq'.  

| Navegador Web  | CentOS7 |
|------|------|
| ![][1] | ![][2] |  
  
* **replace_spaces_in_filenames:** En este reto habia una serie de ficheros con un espacio en su nombre y se debia reemplazar dicho espacio por un punto. Para realizar dicha tarea se me ocurrió listar todos los ficheros mediante el comando 'ls' y posteriormente concatenar este comando con otro capaz de reemplazar todos los espacios por puntos, lo anterior lo realicé mediante el comando 'tr' que se encarga de reemplazar un caracter especificado por otro, es decir que debo especificar que caracter quiero quitar y cual quiero poner 'tr " " "."'.
Con esto se logra que el comando 'tr' se aplique a todos los ficheros encontrados por 'ls'. dicha solución funcionó sin ningun problema tanto en el navegador como en CentOS7.

| Navegador Web  | CentOS7 |
|------|------|
| ![][3] | ![][4] | 
  
* **reverse_readme:** En este reto hay un archivo de texto y lo que se quiere es leer dicho archivo pero en el orden inverso, leer de abajo para arriba. Para lograr esto concateno el comando para leer el archivo 'cat' con el comando 'tac' que indica que se quiere leer en la dirección contraria. 

| Navegador Web  | CentOS7 |
|------|------|
| ![][5] | ![][6] | 

* **remove_duplicated_lines:** En este reto existe un archivo de texto que tiene lineas repetidas, con el mismo texto, entonces se quiere que al leer el archivo las lineas duplicadas sean removidas. Para solucionar este problema utilicé  el comando 'awk' de linux. Este es como una clase de 'cat', permite leer y manejar archivos de texto, pero la diferencia es que 'awk' además de leer el archivo nos brinda algunas acciones sobre el texto. utiliza el siguiente formato: 'awk '/search_pattern/ { action_to_take_on_matches; another_action; }' file_to_parse'. De esta forma en 'action_to_take' investigué la forma de hacer que las lineas repetidas solo salgan una vez. Esto se pudo realizar sin ningun problema tanto en la web como en CentOS7.

| Navegador Web  | CentOS7 |
|------|------|
| ![][7] | ![][8] | 
  
* **disp_table:** En este desafío existe un archivo de texto con una tabla que se encuentra en un mal formato ya que las columnas estan separadas con ',' y se dificulta de leer la tabla. Así que se desea que con el archivo de texto separado con ',' se genere una tabla que se pueda leer correctamente. Para esto yo utilicé el comando de linux 'column' y como parametros llamé '-t' que le indica a column que con el archivo a leer quiero hacer una tabla y '-s' que le indica que quiero utilizar un separador (en este caso el separador por defecto es TAB).
el formato del comando 'column' es el siguiente: 'column parametros, archivo'

| Navegador Web  | CentOS7 |
|------|------|
| ![][9] | ![][10] | 
  
**4.**  En este punto se requiere crear un script capaz de descargar un libro de la web https://www.gutenberg.org/ y ubicarlo en el directorio /home/gutenberg/mybooks. Cada libro nuevo debe reemplazar el libro anterior y cada 5 minutos se debe realizar la descarga de un libro nuevo. Tras analizar el link donde se encuentran ubicados los libros he identificado que para descargar un libro u otro solamente debo variar un numero en la URL, de este modo he creado un script llamado dwLibro.sh donde inicialmente creo un numero aleatorio entre 0 y 28(gutenberg tiene muchos libros pero para este ejercicio he restringido la descarga solamente entre los libros 343 y el 371, por este motivo genero un numero aleatorio entre 0 y 28 y luego le sumo 343; con esto logro descargar un libro aleatorio entre el 343 y el 371. Posteriormente a tener el número concateno toda la URL en una variable, acto seguido utilizo el comando ‘wget -O’. wget significa “web get”, es una línea de comando que descarga contenido  de internet, en este caso utilicé el parámetro –O seguido de la dirección  y nombre con el que deseo almacenar el contenido descargado y como segundo parámetro la URL de la web que deseo descargar. El código del script descrito se muestra a continuación:  
![][11]  
  
Ahora ya es posible descargar los libros de gutemberg por medio del script anterior. Pero el requerimiento exige que cada cinco minutos se descargue un nuevo libro, es decir que cada cinco minutos se debe ejecutar el script, para lograr esto editaremos el fichero del sistema crontab, el crontab es una lista de comandos y scripts que nos gustaria que se ejecutara siguiendo un horario. las lineas en el crontab se deben agregar de la siguiente manera:  

| # | # | # | # | # | texto |
|------|------|------|------|------|------|
| minuto de la hora | Hora del día | día del mes | mes del año | día de la semana | ruta del script |
  
Si se quieren incluir varios numeros, existen varias formas: separar los numeros con ',' ejemplo: 2,8,10 (en este caso se incluyen solo los tres numeros especificados), incluir un rango: 2-10 (en este caso se incluyen todos los numeros desde el 2 hasta el 10 incluyendo al 2 y al 10). Para editar el crontab se debe ejecutar el comando 'crontab -e', la forma en la que logré ejecutar el script dwLibro.sh se muestra a continuación.  
![][12]  
  
Para demostrar que mi proceso anteriomente descrito se encuentra bien, a continuacion se mostrarán tres imagenes. La primera muestra que el usuario, directorio y libro se encuentran almacenados de la forma que el requerimiento lo pide. La segunda muestra el mensaje que se obtiene cuando el crontab ejecuta el script dwLibro.sh. Y la tercera muestra el correo que el crontab registra cuando se activa.  

| Directorio del usuario gutenberg  | Reporte cuando se activa el crontab | Correo generado por el crontab |
|------|------|------|
| ![][13] | ![][14] | ![][15] |
  
 
**5.** 
  
  


### Referencias
* https://cmdchallenge.com  
* https://www.gutenberg.org  
* https://github.com/jvns/kernel-module-fun/blob/master/rickroll.c
* https://www.youtube.com/watch?v=efEZZZf_nTc
* https://www.computerhope.com/unix/utr.htm
* https://www.digitalocean.com/community/tutorials/how-to-use-the-awk-language-to-manipulate-text-in-linux
* http://man7.org/linux/man-pages/man1/column.1.html
* https://www.computerhope.com/unix/wget.htm
* https://www.computerhope.com/unix/ucrontab.htm

[1]: images/Reto1.PNG
[2]: images/Reto1Centos.PNG
[3]: images/Reto2.PNG
[4]: images/Reto2Centos.PNG
[5]: images/Reto3.PNG
[6]: images/Reto3Centos.PNG
[7]: images/Reto4.PNG
[8]: images/Reto4Centos.PNG
[9]: images/Reto5.PNG
[10]: images/Reto5Centos.PNG
[11]: images/Punto4Script.PNG
[12]: images/Punto4Crontab.PNG
[13]: images/Punto4.PNG
[14]: images/Punto4Reporte.PNG
[15]: images/Punto4Correo.PNG

