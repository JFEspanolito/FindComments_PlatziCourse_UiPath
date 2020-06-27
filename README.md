### **FindComments_PlatziCourse_UiPath**

## El proyecto
Este proyecto nace para agilizar la revisión de "comentarios pendientes por resolver a los alumnos", el proyecto solicita la url del curso a validar, navega a cada clase y extrae los comentarios existentes.
Posteriormente divide a los comentarios con más de un corazón y los que no tienen mas de 1, esto permite saber cuales son comentarios nuevos y cuales no.
Seguido pregunta si deseas hacer el seguimiento de los N comentarios encontrados, con control de log interno para el profesor y sistema para responder inmediatamente al alumno, después de responder con este sistema marca el comentario con un Corazón para "indicar que ya no es nuevo".
Al finalizar la revisión de seguimiento (o si se omite) genera un reporte en Excel con la url de cada comentario, el número de corazones del comentario y la información de seguimiento que generamos (si no generamos información, esa columna queda vacía)
**Diagrama general del robot:**

![Diagrama del Proyecto][0]

## Requisitos para utilizar este Robot.
- [UiPath Studio](https://platform.uipath.com) 
- [Cuenta en Platzi](https://platzi.com)
- Url del Curso
- [Firefox](https://www.mozilla.org/es-MX/firefox/download/thanks/)
- [Balareva Excel Activities (Dependencia)](https://connect.uipath.com/marketplace/components/balareva-xl-activities)

![Diagrama del Proyecto][0.1]

Si deseas cambiar el navegador, es posible solo recuerda validar los selectores de interacción con el navegador.
Si quieres cambiarlo y no sabes como hacerlo, puedes ver el [Curso de Automatización de Procesos RPA con UiPath](https://platzi.com/cursos/uipath/) 

## Tutorial de uso
Para ejecutar el robot, debemos ir al [UiPath Studio](https://platform.uipath.com) abrir el proyecto descargado de este repositorio y dar clic en **Run** ubicado en la parte superior del Studio.

![Diagrama del Proyecto][0.2]

Al ejecutar el robot (es Asistido) solicita la url del curso que desea validar.

![Solicitud de URL][1]

Si no proporcionas una URL, buscará el archivo de excel previamente creado en alguna ejecución anterior, de no existir te notificará y posteriormente preguntará si deseas reiniciar la ejecución.

![Solicitud de URL 1.1][1.1]
![Solicitud de URL 1.2][1.2]

Si proporcionas una URL, el robot abrirá el navegador web para el curso proporcionado, buscará la url de cada clase del curso y luego navegará en cada clase para leer los comentarios.

*Actualización 17/06/2020* Ahora el robot pregunta si deseas obtener las respuestas existentes de cada comentario, este paso es opcional y automático.

![Solicitud de URL 1.3][1.3]

Luego de leer todos los comentarios de todas las clases del curso indicado, nos pregunta si deseamos (opcional) hacer el seguimiento puntual de cada comentario.

![Seguimiento Puntual 1][2]

Dependiendo de la opción elegida el robot realizará cierta acción.
1) Respuesta automática, realizará una lectura del acumulado de información (excel y comentarios encontrados), posteriormente navegará a la url de cada comentario que tenga información en la columna "Repuesta" y escribirá dicho valor como una respuesta al alumno.

2) Realizará la navegación a la url del primer comentario a revisar y veremos una ventana como la siguiente:
En esta podemos dejar una nota interna (para nosotros) en el reporte que el robot generará.

![Seguimiento Puntual 2][3]
![Seguimiento Puntual 3][4]

*Así mismo en cualquier momento podemos romper el ciclo de revisión de comentarios escribiendo “{exit}” en la ventana de comentarios internos.*

![Seguimiento Puntual 4][5]

Posteriormente nos preguntará si deseamos responder al alumno, el texto que escribamos en este cuadro de texto, se escribirá en el comentario del alumno como respuesta. 
Adicional si respondemos el comentario del alumno, el robot marcará el corazón (para identificar que fue respondido).

![Seguimiento Puntual 5][6]
![Seguimiento Puntual 6][7]

Posteriormente realizará una revisión para evaluar si el comentario está o no marcado con un corazón, en el caso de no estar marcado preguntará si deseas marcarlo.

![Seguimiento Puntual 7][8]

Al finalizar el ciclo de seguimiento, se generá un reporte con 2 hojas:
- La primer hoja donde se meustran los comentarios que se clasifican como “nuevos” por tener 0 o 1 corazón (que es el valor que les aparece al ser creado).
- La segunda hoja es para todos los que tienen más de un corazón.

Ambas hojas contiendrán 
- Nombre : Nombre del Estudiante que dejó el comentario escrito por el estudiante en el curso.
- Comentario : Comentario escrito por el estudiante en el curso.
- URL : La URL del comentario. No la modifiques es la que se usa para navegar al comentario en el sistema de seguimiento.
- Corazon : El número de corazones que hay en el sitio web al momento de extraer los datos.
- Curso : Nombre del curso donde se encontró el comentario.
- Seguimiento : Colocar aquí el mensaje de seguimiento para ti, son tus notas de profesor.
- CorazonDado : Indica si el comentario ya cuenta con un corazón dado por el robot o el usuaro que ejecuta el robot.
- DarCorazon : Colocar un 1 si deseas dar un corazón a este comentario dentro del sitio web.
- MiRespuestaAnterior : La última respuesta que fue dada al comentario desde el robot.
- ResponderLoSiguiente : El texto que coloques en esta columna será el texto que se le responderá al estudiante en el próximo seguimiento automático que realices.
- Respuestas : Todas las respuesta encontradas en el comentario.

![Seguimiento Puntual 8][9]
![Seguimiento Puntual 9][10]

El documento generado se guarda en la carpeta Archivos dentro de la carpeta del proyecto.

[//]: #
[0]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img0.png> "Diagrama del Proyecto"
[0.1]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img0.1.png> "Pre-requisito"
[0.2]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img0.2.png> "Ejecutar Proyecto"
[1]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img1.png> "Solicitud de URL"
[1.1]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img1.1.png> "Solicitud de URL"
[1.2]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img1.2.png> "Solicitud de URL"
[1.3]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img1.3.png> "Obtener Respuestas del Comentario"
[2]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img2.png> "Seguimiento Puntual 1"
[3]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img3.png> "Seguimiento Puntual 2"
[4]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img4.png> "Seguimiento Puntual 3"
[5]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img5.png> "Seguimiento Puntual 4"
[6]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img6.png> "Seguimiento Puntual 5"
[7]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img7.png> "Seguimiento Puntual 6"
[8]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img8.0.png> "Seguimiento puntual"
[9]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img8.1.png> "Solicitud de URL"
[10]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img9.1.png> "Solicitud de URL"
