# Explicacion del codigo

## Recorrido de una operacion

LoginFrame abre la pantalla de ingreso. Autenticacion calcula el SHA-256 de la clave mediante Sesion.hash y consulta ENCUESTADOR, SUPERVISOR y RECUENTISTA. Cuando encuentra una coincidencia, LoginFrame guarda el identificador, nombre y rol en Sesion y abre la ventana correspondiente.

Las pantallas llaman a Conexion para consultar o guardar en Oracle. CasoServicio y VisitaServicio agrupan operaciones que necesitan validaciones y transacciones. La interfaz utiliza Estilo para mantener una apariencia comun.

## Responsabilidad de cada clase

| Clase | Responsabilidad |
| --- | --- |
| LoginFrame | Campos de ingreso, autenticacion en segundo plano y apertura de pantalla por rol. |
| Autenticacion | Consultas parametrizadas de credenciales; resultado Usuario o null; deteccion de coincidencias entre roles. |
| Sesion | Datos del usuario activo, cierre de sesion y calculo SHA-256. |
| Conexion | Lectura de configuracion, conexiones JDBC, consultas, modificaciones, transacciones, combos y mensajes. |
| RecuentistaFrame | Registro de hogares, asignacion de encuestador y acceso al catalogo de categorias. |
| EncuestadorFrame | Hogares asignados, acceso a gastos y consultas, envio de casos completos. |
| SupervisorFrame | Filtro de casos, consultas, aprobacion y devolucion. |
| RegistrarGastoFrame | Seleccion de fecha y visita, productos y miembros; validacion y registro de gastos. |
| CasoServicio | Validacion de rol, bloqueos de filas y cambios coordinados de estado. |
| VisitaServicio | Fecha dentro del ciclo y reutilizacion o creacion de visita. |
| CategoriaFrame | Crear, consultar, actualizar y eliminar categorias; manejo de restricciones referenciales. |
| ResumenHogarFrame | Registros y suma de valores por categoria en un intervalo de dias. |
| FrecuenciaCompraFrame | Dias distintos con Compra por producto y porcentaje respecto a 14. |
| FormaAdquisicionFrame | Resumen por forma y detalle de gastos de la seleccion. |
| SelectorFecha | Campo de fecha, calendario de mes y ano y eventos de cambio. |
| Item | Identificador, texto visible y dato extra para opciones de JComboBox. |
| Estilo | Configuracion visual, encabezados, tablas, filas y botones. |

## Conexion y consultas

Conexion carga conexion.local.properties al inicializar la clase. Busca el archivo en el directorio de trabajo; si se cambia durante la ejecucion, se debe reiniciar la aplicacion. Las propiedades JVM enph.url, enph.usuario y enph.clave tienen prioridad sobre los valores del archivo. La URL predeterminada del codigo es localhost:1521:orcl; el archivo local de este equipo configura XE.

Cada operacion abre su conexion y utiliza try-with-resources para cerrar conexion, sentencia y resultados. PreparedStatement envia los parametros separados de la sentencia SQL. consultar devuelve un DefaultTableModel no editable y convierte las fechas a dd/MM/yyyy. valor devuelve un unico dato. ejecutar confirma una modificacion. transaccion permite confirmar varias sentencias juntas o revertirlas si falla una.

## Reglas del ciclo y de los casos

VisitaServicio calcula el dia como diferencia entre inicio y fecha mas uno. Solo acepta dias del 1 al 14. Bloquea el hogar con FOR UPDATE antes de comprobar estado y encuestador; reutiliza una visita del dia o crea una nueva y actualiza dia_ciclo_actual.

CasoServicio comprueba el rol y el estado actual en Oracle, no solo la fila visible en pantalla. Para cerrar o aprobar exige 14 dias distintos con visita y ninguna visita Revisar. Usa commit y rollback para coordinar los registros. El cierre crea o actualiza el caso Completo; aprobar guarda el supervisor y actualiza las visitas; devolver reabre el hogar. Estas comprobaciones cuentan visitas, no gastos por dia.

## Fechas y valores

SelectorFecha convierte entre Date y LocalDate usando la zona del equipo. RegistrarGastoFrame usa BigDecimal para leer cantidades y valores y reemplaza coma por punto antes de interpretarlos. Rechaza entradas no numericas y valores menores o iguales a cero. Los totales de algunas pantallas se presentan mediante double; esta documentacion describe el comportamiento existente.

## Sesion e interfaz

LoginFrame utiliza SwingWorker para conectar sin bloquear el hilo grafico durante el ingreso; done procesa el resultado en ese hilo. Las demas consultas de pantalla se ejecutan como estan implementadas en sus eventos. Sesion mantiene datos estaticos del usuario actual y cerrar los limpia. Los caracteres de la clave de ingreso se borran al terminar el trabajo, aunque la autenticacion crea una cadena para calcular el hash.

Estilo.iniciar establece es-CO. El proyecto tambien conserva los argumentos JVM de configuracion regional agregados en la reparacion previa. Documentar no modifica ninguno de esos ajustes.

## Base de datos utilizada

Las tablas consultadas son HOGAR, MIEMBRO, VISITA, GASTO, PRODUCTO, CATEGORIA, CASO, ENCUESTADOR, SUPERVISOR y RECUENTISTA. Algunas inserciones omiten identificadores; requieren que la base importada conserve sus mecanismos de generacion de identificadores y restricciones.

## Alcance de la documentacion

Se agregaron 88 comentarios explicativos en 17 archivos Java. No se modificaron instrucciones ni consultas. Al retirar exactamente los comentarios agregados, los archivos recuperan los bytes de la version anterior a esta documentacion. Tambien se comprueba la compilacion.
