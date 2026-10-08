# La Anatomía de una Especificación

**Fecha:** 2026-10-08

## Resumen

Una especificación describe el comportamiento observable de un sistema, las restricciones que debe respetar y cómo verificar que cumple lo esperado. Separarla del plan y de las tareas ayuda a distinguir los requisitos de las decisiones de implementación y del trabajo necesario.

## Conceptos Clave

### Elementos centrales de una especificación

- **Comportamiento**: acción observable que realiza el sistema.
- **Restricciones**: límites o condiciones que debe respetar.
- **Verificación**: evidencia o prueba que demuestra que se cumple lo especificado.

### De tickets o documentación a especificaciones

Al convertir una solicitud en una especificación:

1. Describe el comportamiento observable.
2. Define las restricciones.
3. Escribe criterios de aceptación que puedan probarse.

### Las tres capas del desarrollo

- **Especificación (el qué)**:
  - **Comportamiento**: acciones observables que realiza el sistema.
  - **Contratos**: entradas, salidas y límites de los componentes.
  - **Invariantes**: condiciones que siempre deben cumplirse.
- **Plan (el cómo)**: decisiones sobre cómo cumplir la especificación, sin repetirla.
- **Tareas (el orden)**: unidades de trabajo atómicas y comprobables.

Para distinguirlas, pregúntate:

- ¿Describe un resultado observable? Es una **especificación**.
- ¿Registra una decisión entre alternativas? Es parte del **plan**.
- ¿Define una unidad de trabajo? Es una **tarea**.

### Criterios de aceptación y EARS

EARS (*Easy Approach to Requirements Syntax*, o Enfoque Fácil para la Sintaxis de Requisitos) es un conjunto de patrones para redactar requisitos explícitos, verificables y no ambiguos. Ayuda a declarar claramente el disparador y la respuesta esperada.

#### Patrones EARS

- **Patrón ubicuo**: requisito que siempre es verdadero.
- **Patrón impulsado por eventos**: requisito activado por un evento discreto.
- **Patrón impulsado por estado**: requisito que se aplica mientras una condición permanezca activa.
  - **Estructura**: Mientras [condición], el sistema deberá [respuesta].
  - **Ejemplo**: Mientras la carga de la foto esté en progreso, el sistema deberá actualizar la barra de progreso cada segundo.
- **Patrón de comportamiento no deseado**: define la respuesta del sistema ante un fallo o evento no deseado.
  - **Estructura**: Si [evento de fallo], entonces el sistema deberá [respuesta].
  - **Ejemplo**: Si se pierde la conexión de red durante la publicación de un tweet, entonces el sistema deberá guardar el borrador del tweet y notificar al usuario.
- **Patrón de característica opcional**: requisito que se aplica solo cuando una configuración o característica está habilitada.
  - **Estructura**: Donde [configuración], el sistema deberá [comportamiento].
  - **Ejemplo**: Donde la autenticación de dos factores esté habilitada, el sistema deberá requerir un código de verificación antes de completar el inicio de sesión.

#### Elegir el patrón correcto

- ¿La condición es continua y constante? Usa el patrón **impulsado por estado**.
- ¿Se desencadena por un evento de fallo o error? Usa el patrón de **comportamiento no deseado**.
- ¿Aplica solo bajo una configuración específica? Usa el patrón de **característica opcional**.

#### Cómo escribir criterios verificables

- Identifica claramente el disparador.
- Expresa con precisión el comportamiento esperado.
- Evita palabras vagas como «apropiado» o «correctamente».
- Pregúntate: *¿Qué evidencia demostraría que este criterio está satisfecho?*

### Restricciones explícitas

- **Restricciones positivas**: indican lo que el sistema debe hacer.
- **Restricciones negativas**: indican lo que el sistema no debe hacer.

### Archivo persistente de reglas del proyecto

Este archivo documenta convenciones que deben mantenerse a lo largo del proyecto.

#### Contenido típico

- **Convenciones de stack y framework**: por ejemplo, “Todas las llamadas HTTP deben usar el envoltorio `apiClient` existente; las llamadas directas a `fetch` están prohibidas”.
- **Estilo de código y expectativas de pruebas**: por ejemplo, “Las pruebas unitarias deben cubrir todas las funciones nuevas con al menos un 80 % de cobertura” o “Usar ESLint con la configuración compartida del equipo”.
- **Estructura de directorios**: por ejemplo, “Los módulos de características residen bajo `src/features/` y las utilidades compartidas, bajo `src/utils/`”.
- **Convenciones de commits y ramas**: por ejemplo, “Las ramas de características deben tener el prefijo `feat/` e incluir el número del ticket”.

#### Qué no pertenece a este archivo

Los requisitos o comportamientos específicos de una característica pertenecen a sus respectivas especificaciones, no al archivo de reglas del proyecto. Por ejemplo, “La página de pago debe mostrar un desglose de impuestos” es un requisito de una característica y debe documentarse en su especificación.

## Ejemplos

### Confirmación de compra

- **Comportamiento**: El sistema enviará un correo de confirmación después de una compra.
- **Restricción**: El correo debe enviarse dentro de los 5 minutos posteriores a la compra.
- **Verificación**: El usuario recibe un correo de confirmación con los detalles correctos del pedido.

### Guardar búsquedas de usuario

- **Especificación**: Un usuario puede almacenar hasta 20 búsquedas con nombre. Al guardar la número 21, se reemplaza la menos usada recientemente. Los nombres son únicos por usuario y tienen un máximo de 60 caracteres.
- **Plan**: Guardar las búsquedas en la columna JSON `user_preferences` existente en lugar de crear una tabla nueva, porque el volumen está limitado y ninguna consulta filtra por el contenido de la búsqueda.
- **Tareas**:
  1. Añadir una función auxiliar de almacenamiento.
  2. Aplicar el límite de 20 elementos con reemplazo LRU.
  3. Exponer un endpoint para listar las búsquedas.
  4. Exponer un endpoint para eliminar una búsqueda.

Si el límite aumenta de 20 a 50, cambia la especificación y la tarea relacionada. La decisión de almacenamiento del plan puede permanecer igual.

## Referencias
Referencia EARS de Alistair Mavin — la notación original con el conjunto completo de patrones.
El formato abierto AGENTS.md — la convención de reglas de proyecto neutral para proveedores.
Documentación de reglas de Cursor — la implementación de un editor de reglas persistentes para proyectos.
