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

![Requerimiento - Dependencias][1]

Si deseas cambiar el navegador, es posible solo recuerda validar los selectores de interacción con el navegador.
Si quieres cambiarlo y no sabes como hacerlo, puedes ver el [Curso de Automatización de Procesos RPA con UiPath](https://platzi.com/cursos/uipath/) 

## Tutorial de uso
Para ejecutar el robot, debemos ir al [UiPath Studio](https://platform.uipath.com) abrir el proyecto descargado de este repositorio, configurar lo siguiente:
Dentro del archivo de excel que está en el proyecto en la carpeta Data, debemos configurar los cuadros marcados en rojos, con la ruta donde se guardará el reporte resultado y la(s) páginas web de los cursos que va a procesar el robot.
También debemos actualizar la ruta dentro de la sección de **variables** en la parte inferior, la Variable **rutaConfig** con la ruta donde esta el archivo Config (excel que actualizamos el paso anterior).

![Config_1][2]

Posteriormente dar clic en **Run** o **Debug** ubicado en la parte superior del Studio.

![Rung_Software][3]

Al ejecutar el robot navegará a la ruta indicada en el Config, si no proporcionas una URL, buscará el archivo de excel previamente creado en alguna ejecución anterior, de no existir te notificará y posteriormente preguntará si deseas reiniciar la ejecución.

![Config_2][4]

Si proporcionas una URL, el robot abrirá el navegador web para el curso proporcionado, buscará la url de cada clase del curso y luego navegará en cada clase para leer los comentarios.
Luego de leer todos los comentarios de todas las clases del curso indicado realizará una búsqueda de cada Respuesta de cada comentario (es romendado dejar que lo haga al menos 1 primera vez que lo ejecutes), para que NO lo realice, en el Excel debemos cambiar la bandera de True a False llamada **ExtraerRespuestasDeComentarios**

Posteriormente, si activamos las vanderas **SeguimientoManual** y/o **SeguimientoAutomático** realizará lo siguiente:
**Seguimiento automática**, realizará una lectura del acumulado de información (excel y comentarios encontrados), posteriormente navegará a la url de cada comentario que tenga información en la columna "Repuesta" y escribirá dicho valor como una respuesta al alumno.

**Seguimiento Manual** Realizará la navegación a la url del primer comentario a revisar y veremos una ventana como la siguiente:
En esta podemos dejar una nota interna (para nosotros) en el reporte que el robot generará.

![Seguimiento Puntual 2][5]
![Seguimiento Puntual 3][6]

*Así mismo en cualquier momento podemos romper el ciclo de revisión de comentarios escribiendo “{exit}” en la ventana de comentarios internos.*

![Seguimiento Puntual 4][7]

Posteriormente nos preguntará si deseamos responder al alumno, el texto que escribamos en este cuadro de texto, se escribirá en el comentario del alumno como respuesta. 
Adicional si respondemos el comentario del alumno, el robot marcará el corazón (para identificar que fue respondido).

![Seguimiento Puntual 5][8]
![Seguimiento Puntual 6][9]

Posteriormente realizará una revisión para evaluar si el comentario está o no marcado con un corazón, en el caso de no estar marcado preguntará si deseas marcarlo.

![Seguimiento Puntual 7][10]

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

![Reporte][11]
![Reporte][12]

El documento generado se guarda en la carpeta Archivos dentro de la carpeta del proyecto.

## Actualizaciones implementadas

- **Actualización 17/06/2020** : Ahora el robot pregunta si deseas obtener las respuestas existentes de cada comentario, este paso es opcional y automático.
- **Actualización 27/06/2020** : Ahora el robot detecta cuando otorgaste ya un corazón al comentario para marcarlo como "atendido" o "leído".
- **Actualización 30/06/2020** :  Ahora el robot acepta múltiples urles de cursos separadas por ; como ejemplo:  " platzi.com/clases/uipath ; https://platzi.com/cursos/machine-learning/ " lo que permitirá que realice búsquedas de comentarios en ambos cursos (o más, ¡puedes poner los que quieras!)
- **Actualización 30/06/2020** : Se añade sistema de delay dinámico controlado por variable "varTimeOutGeneral", el valor proporcionado será transformado en "milisegundos de espera."
- **Actualización 15/07/2020** : Se modifica el sistema ahora en versión REF, lo que permite tener un control desde archivo CONFIG para hacerlo *desatendido* a menos que hagas un seguimiento manual. De esta manera la revisión se puede realizar sin estar en el equipo donde el robot se ejecuta.
- **Actualización 07/08/2020** : Se añade soporte para múltiples navegadores web.

[//]: #
[0]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img0.png> "Diagrama del Proyecto"
[1]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img1.png> "Dependencias"
[2]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img2.png> "Config_1"
[3]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img3.png> "Run"
[4]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img4.png> "Config_2"
[5]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img5.png> "Seguimiento_1"
[6]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img6.png> "Seguimiento_2"
[7]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img7.png> "Seguimiento_3"
[8]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img8.png> "Seguimiento_4"
[9]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img9.png> "Seguimiento_5"
[10]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img10.png> "Seguimiento_6"
[11]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img11.png> "Reporte_1"
[12]: <https://raw.githubusercontent.com/JFEspanolito/FindComments_PlatziCourse_UiPath/master/imgParaReadMe/img12.png> "Reporte_2"
