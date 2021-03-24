## HEALTHCHECK:
Toda imagen de Docker puede definir un healthcheck, que no es nada más que un comando, que ejecutado periódicamente, indica si el servicio está funcionando correctamente o no. Docker ejecuta este comando como un proceso separado dentro del mismo contenedor. Si el comando devuelve un error, Docker considera que el contenedor no está funcionando.

Se le puede especificar opciones:
- --interval=DURATION (default: 30s)
- --timeout=DURATION (default: 30s)
- --start-period=DURATION (default: 0s)
- --retries=N (default: 3)

Ej:
'''
HEALTHCHECK --interval=5m --timeout=3s \
  CMD curl -f http://localhost/ || exit 1
'''

## ONBUILD
Agrega a la imagen un trigger que se ejecutará en un momento posterior, cuando la imagen se use como base para otro build. El trigger se ejecutará como si se hubiera insertado inmediatamente después de la instrucción FROM.

ej:
''' 
ONBUILD ADD . /app/src
ONBUILD RUN /usr/local/bin/python-build --dir /app/src
'''

## VOLUME
Sirve para crear puntos de montado y lo marca como que contiene volúmenes montados externamente desde el host nativo u otros contenedores

Ej:
''' 
FROM ubuntu
RUN mkdir /myvol
RUN echo "hello world" > /myvol/greeting
VOLUME /myvol
'''
