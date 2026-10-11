# ENPH Cuadernillo 2

Proyecto integrador para registrar y consultar gastos diarios de hogares urbanos durante un ciclo de 14 dias. Desarrollado con Java Swing, JDBC y Oracle 10g.

## Descargar y abrir

1. Abre el archivo ENPH-para-GitHub.zip de este repositorio y pulsa Download raw file para descargarlo.
2. Descomprime el ZIP. Dentro encontraras la carpeta ENPH-publico.
3. Abre NetBeans y selecciona File > Open Project.
4. Selecciona ENPH-publico, la carpeta que contiene build.xml y nbproject.
5. Prepara el controlador Oracle, la cuenta de conexion y la base siguiendo el README incluido dentro del ZIP.
6. Ejecuta el proyecto con clic derecho > Run.

## Documentacion

- [Guia muy facil de uso](GUIA-FACIL.md)
- [Explicacion del codigo y sus 17 clases](CODIGO.md)

El ZIP incluye los archivos Java comentados y los archivos de proyecto de NetBeans con sus carpetas originales. Se agregaron 88 comentarios sin cambiar el codigo base. Se verifico la compilacion y la igualdad del codigo ejecutable generado, excluyendo informacion de depuracion.

La configuracion Oracle local, sus contrasenas, el dump y los datos de hogares no se publican. Cada equipo debe configurar su conexion e importar la base por separado. El controlador ojdbc14.jar debe colocarse en lib antes de ejecutar; no esta incluido en el ZIP publico.
