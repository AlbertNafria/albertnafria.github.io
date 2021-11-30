---
layout: post
title: "Vivir en el terminal"
date: 2021-02-05 19:16:07 CET
categories: jekyll update
---



## Interfaz línea de comandos

Hace exactamente un año me propuse aprender a utilizar la terminal de mi
portátil, motivado en parte por la fascinación que me producía ver como, a golpe
de teclado, era posible hacer tanto, y por la frustración que me producían
algunas tareas muy repetitivas que solía hacer. Desde entonces he cambiado
diametralmente mi manera de trabajar con el ordenador, todo gracias a las
diferentes herramientas que pueden ejecutarse en un `shell` de `Unix`.


Podría decir que gran parte de la culpa la tiene [este libro][linux_command_line], muy
completo y ameno, que cubre gran parte de las posiblidades de la línea de
comandos partiendo desde el principio. Puede servir de referencia tanto para el
novato como para alguien con algo de experiencia. Además, la página web dispone
de mucho material adicional para profundizar en algunos temas, como los
*shell scripts*.

Las principales ventajas que he encontrado en las herramientas CLI (Command Line
Interface) sobre de las que disponen una interfaz gráfica son las siguientes:

- Uso de menos recursos. Las interfaces gráficas consumen muchos recursos,
  utilizar herramientas CLI consigue que la carga de la batería dure más, que el
  ordenador se caliente menos, etc.
- Facilidad de configuración y ubicuidad. Las configuraciones se guardan en
  archivos de texto plano, por lo que son fáciles de entender, configurar e
  incluso son más portables entre distintas máquinas.
- Liberarse del ratón. Algunos programas con CLI tienen soporte para el ratón,
  pero en general, el principal método de entrada es el teclado. De esta manera
  se gana en productividad, rapidez y comodidad de no ir moviendo la mano del
  teclado al ratón y viceversa.
  
En algún sitio leí que la diferencia entre utilizar una línea de comandos o una
interfaz gráfica es la misma que mantener una conversación o gritar. A
continuación haré un pequeño repaso del *software* que utilizo normalmente.


## Hay software para todo

Quizá la herramienta más importante a la hora de trabajar desde una terminal sea el
editor de texto. `Vim` es el editor de los sistemas `Unix` por excelencia, y a pesar de tener
una curva de aprendizaje muy inclinada, creo que a la larga vale la pena el
tiempo invertido en aprenderlo.

Otro programa básico para trabajar cómodamente es el **multiplexor de
terminal**. Los dos más conocidos son `Screen` y `Tmux`, aunque el segundo es
más moderno y avanzado. Esto te permite tener varias sesiones virtuales dentro
de un solo terminal y poder visualizar esas sesiones en distintas ventanas o
pestañas dentro de la terminal.

De hecho, lo primero que hago al encender el ordenador es abrir una terminal y
ejecutar `Tmux`.


### Emulador de terminal

Paradójicamente, para trabajar desde la línea de comandos hacemos uso de una herramienta con
interfaz gráfica: el *emulador de terminal*. Se llama emulador porque intenta
recrear las terminales de los teletipos del pasado, pero siendo software en vez de
un dispositivo. 

Cada sistema operativo ofrece un emulador de terminal por defecto, pero siempre
es posible instalar otra que te guste más. A mí, la que mejor me va es
`Alacritty`, una terminal muy sobria y que se configura a través del fichero
`~/.alacritty.yml`. Creo que esta aplicación casa más con las otras aplicaciones
que ejecuto a través de ella.

### Correo electrónico

Otra de las tareas más comunes a la hora de trabajar con un ordenador es
consultar el email. Una aplicación interesante es `mutt`, un cliente de email
muy potente y configurable que facilita mucho el uso del correo, especialmente
cuando el *buzón de entrada* está muy lleno. Sin apartar las manos del teclado
es posible gestionar todo con unas pocas teclas. Como reza el eslógan de `mutt`,
*all mail clients suck. This one just sucks less*. Es curioso que el año pasado
cumpliera 25 años y aún siga siendo tan útil...

### Contenidos multimedia

La interfaz de línea de comandos está fuertemente basada en el texto, pero
también hace posible trabajar con otros tipos de ficheros. Hay algunas
herramientas para reproducir contenidos multimedia que son fáciles de utilizar y
muy efectivas.

- `mpv` es un reproductor de vídeo open source, con una interfaz gráfica muy
  sobria por no decir casi inexistente, muy configurable a través de fichero
  `mpv.conf`, el cual puedes controlar únicamente con atajos de teclado. También
  ofrece soporte para el mouse.
- En lo que refiere a escuchar música, existe una aplicación muy interesante:
  `cmus`. Esta aplicación reproduce **todos** los ficheros de audio que existen,
  incluso `flac`, y tiene una *peculiaridad*, y es que solo reproduce música,
  nada más.
- También se pueden manipular imágenes gracias a los programas incluídos en el
  [paquete `imagemagick`][imagemagick], muy útil sobretodo a la hora de programar tareas
  repetitivas mediante *scripts*.


### Navegar por la web

Cómo no, en modo texto también es posible visitar páginas web. La única
peculiaridad es que los navegadores son basados en texto, por lo que solamente
renderizan el contenido `html`, sin ejecutar `javascript` ni formatear con
`css`. Eso puede ser un problema o una ventaja, a veces tiene sentido navegar por
internet sin las distracciones de los anuncios o las políticas de cookies, y las
páginas con contenido estático se ven prácticamente igual.

![Google en la terminal](/img/google-w3m.png)

Hay varios navegadores basados en texto, pero mi favorito es `w3m`.

### Visualizador de PDF

Para los que están acostumbrados a `Vim` hay un visor de pdf, `Zathura`, que
utiliza los mismos atajos de teclado. Es una herramienta muy útil para leer
ficheros en pdf sin necesidad de quitar las manos del teclado. Se puede hacer
scroll, acercar o alejar, y todo con sencillos atajos de teclado. 


## Lenguajes de marcado

Aunque existe algún procesador de texto basado en línea de comandos, yo prefiero
utilizar `Vim` para escribir mis documentos. Como los editores solamente editan
texto sin formato, a veces es necesario echar mano de lenguajes de marcado para
poder procesarlos posteriormente y obtener documentos formateados. `markdown`
es una buena idea para este trabajo, por su equivalencia con `html`, y para
obtener documentos de más calidad, `LaTeX`. Este último es más complejo y está
muy enfocado a documentos científicos, pero para documentos de texto sencillos
el marcado necesario es muy fácil.

Por último, hay una herramienta, `pandoc`, que convierte ficheros de un formato a
otro, y trabaja con `docx`, `LaTeX`, `markdown`, `odt`, etc, de modo
que la limitación es poca.



## Conclusión

Quería hacer un pequeño viaje a través de algunas aplicaciones que utilizo en mi
día a día y que, por su minimalismo y sencillez, facilitan mucho el flujo de
trabajo. Por otro lado, hoy en día la línea de comandos es **totalmente**
**prescindible**, hay herramientas gráficas para todo, incluso para las tareas
de administración de sistemas más complejas. El principal problema es la curva
de aprendizaje, pero a la larga vale la pena.


[linux_command_line]:https://linuxcommand.org/tlcl.php
[imagemagick]:https://imagemagick.org/
