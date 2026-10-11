# Guia facil de uso

## Entrar

1. Ejecuta el proyecto como explica el README.
2. Escribe tu usuario del operativo y contraseña.
3. Pulsa Ingresar al sistema. Se abre la pantalla de tu rol.

## Registrar y asignar un hogar

1. Entra como Recuentista.
2. Escribe un codigo de hogar que no exista y su direccion.
3. Selecciona la fecha de inicio del ciclo.
4. Elige el encuestador y pulsa Registrar hogar.
5. Si lo dejaste Sin asignar, selecciona el hogar en la tabla, elige el encuestador y pulsa Asignar encuestador al hogar seleccionado.

## Registrar un gasto

1. Entra como Encuestador.
2. Haz clic sobre uno de tus hogares con estado Asignado.
3. Pulsa Registrar gasto diario.
4. Elige la fecha del gasto dentro del intervalo mostrado para el hogar.
5. Pulsa Cargar / crear visita de la fecha.
6. Elige categoria, producto, miembro o Todo el hogar y forma de adquisicion.
7. Escribe cantidad y valor pagado, ambos mayores que cero. Puedes usar coma o punto decimal.
8. Pulsa Guardar gasto. Revisa que aparezca en la tabla inferior.

Los cambios se guardan en Oracle. Crear una visita y guardar un gasto son acciones que agregan datos.

## Consultar

Selecciona el hogar y abre la opcion que necesitas:

- Resumen por hogar: elige dias inicial y final y pulsa Consultar. Muestra registros y valor por categoria.
- Frecuencia de compra: elige una categoria o Todas y pulsa Consultar. Cuenta dias con forma Compra; el porcentaje usa 14 dias como denominador.
- Forma de adquisicion: selecciona una forma en la tabla superior para ver sus gastos en la tabla inferior.

## Enviar al supervisor

1. Registra las visitas correspondientes a los 14 dias del ciclo.
2. Verifica que no haya visitas en estado Revisar.
3. Selecciona el hogar y pulsa Crear caso para supervisor.
4. Lee el mensaje y confirma cuando los datos esten listos.

El cierre valida visitas de 14 dias; no exige que cada visita tenga un gasto. La ventana de gastos de esta version exige un valor mayor que cero incluso para formas distintas de Compra.

## Revisar como supervisor

1. Entra como Supervisor.
2. Selecciona un caso Completo o Con alertas.
3. Abre sus consultas para revisar los datos.
4. Pulsa Aprobar caso o Devolver caso y confirma.

Al aprobar se guardan los estados del caso, hogar y visitas. Al devolver, el caso pasa a Devuelto y el hogar a Asignado para corregirlo. Un caso aprobado queda protegido en las operaciones de cierre y revision.

## Ver los comentarios del codigo

1. En NetBeans abre Paquetes de fuentes > enph.
2. Haz doble clic en una clase, por ejemplo LoginFrame.java.
3. Busca los comentarios que empiezan con DOCUMENTACION. Cada uno explica el metodo que aparece justo debajo.
4. Consulta CODIGO.md para entender como se conectan las clases.

## Si aparece un error

- Configura conexion.local.properties: revisa que exista en la raiz y que usuario tenga un valor.
- Falta ojdbc14.jar: agrega el controlador a lib y revisa Bibliotecas del proyecto.
- Network Adapter o ORA-12505: revisar el servicio de Oracle y el registro de XE en el listener.
- ORA-01017: revisar la cuenta Oracle del archivo local.
- ORA-00942: las tablas pueden estar en otro esquema o faltar en la importacion.
- Usuario o contraseña incorrectos: revisar la cuenta del operativo, no la cuenta de Oracle.

No vuelvas a importar la base sobre datos existentes para solucionar un error de ingreso sin revisar primero la causa.
