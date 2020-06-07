### **FindComments_PlatziCourse_UiPath**

## El proyecto
Este proyecto nace para agilizar la revisión de "comentarios pendientes por resolver a los alumnos", el proyecto solicita la url del curso a validar, navega a cada clase y extrae los comentarios existentes.
Posteriormente divide a los comentarios con más de un corazón y los que no tienen mas de 1, esto permite saber cuales son comentarios nuevos y cuales no.
Seguido pregunta si deseas hacer el seguimiento de los N comentarios encontrados, con control de log interno para el profesor y sistema para responder inmediatamente al alumno, después de responder con este sistema marca el comentario con un Corazón para "indicar que ya no es nuevo".
Al finalizar la revisión de seguimiento (o si se omite) genera un reporte en Excel con la url de cada comentario, el número de corazones del comentario y la información de seguimiento que generamos (si no generamos información, esa columna queda vacía)

## Requisitos para utilizar este Robot.
- [UiPath Studio](platform.uipath.com) 
- [Cuenta en Platzi](https://platzi.com)
- Url del Curso
- [Firefox](https://www.mozilla.org/es-MX/firefox/download/thanks/)

Si deseas cambiar el navegador, es posible solo recuerda validar los selectores de interacción con el navegador.
Si quieres cambiarlo y no sabes como hacerlo, puedes ver el [Curso de Automatización de Procesos RPA con UiPath](https://platzi.com/cursos/uipath/) 

## Tutorial para Ejecución
Al ejecutar el robot (es Asistido) solicita la url del curso que desea validar.
![Solicitud de URL][0]
Luego de leer todos los comentarios de todas las clases del curso indicado, nos pregunta si deseamos (opcional) hacer el seguimiento puntual de cada comentario.
![Seguimiento Puntual 1][1]
Si afirmamos, se abrirá el navegador web con la url del primer comentario a revisar y veremos una ventana como la siguiente:
En esta podemos dejar una nota interna (para nosotros) en el reporte que el robot generará.
![Seguimiento Puntual 2][2]
![Seguimiento Puntual 3][3]
*Así mismo en cualquier momento podemos romper el ciclo de revisión de comentarios escribiendo “{exit}” en la ventana de comentarios internos.*
![Seguimiento Puntual 4][4]
Posteriormente nos preguntará si deseamos responder al alumno, el texto que escribamos en este cuadro de texto, se escribirá en el comentario del alumno como respuesta. 
Adicional si respondemos el comentario del alumno, el robot marcará el corazón (para identificar que fue respondido).
![Seguimiento Puntual 5][5]
![Seguimiento Puntual 6][6]
Al finalizar el ciclo de seguimiento, se generá un reporte con 2 hojas:
- La primer hoja donde se meustran los comentarios que se clasifican como “nuevos” por tener 0 o 1 corazón (que es el valor que les aparece al ser creado).
- La segunda hoja es para todos los que tienen más de un corazón.

Ambas hojas contiendrán 
- URL del comentario.
- Número de corazones.
- Texto del seguimiento que escribimos durante la revisión puntual.

![Seguimiento Puntual 7][7]
![Seguimiento Puntual 8][8]

El documento generado se guarda en la carpeta Archivos dentro de la carpeta del proyecto.

[//]: #
[0]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img1.png> "Solicitud de URL"
[1]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img2.png> "Seguimiento Puntual 1"
[2]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img3.png> "Seguimiento Puntual 2"
[3]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img4.png> "Seguimiento Puntual 3"
[4]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img5.png> "Seguimiento Puntual 4"
[5]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img6.png> "Seguimiento Puntual 5"
[6]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img7.png> "Seguimiento Puntual 6"
[7]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img8.png> "Solicitud de URL"
[8]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img9.png> "Solicitud de URL"
[9]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img10.png> "Solicitud de URL"
