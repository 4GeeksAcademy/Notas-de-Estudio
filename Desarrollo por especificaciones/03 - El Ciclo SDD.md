# El Ciclo SDD

**Fecha:** 2026-10-08

## Resumen

El desarrollo guiado por especificaciones (SDD, *Spec-Driven Development*) organiza el desarrollo en un ciclo repetible de cinco fases: especificar, planificar, desglosar tareas, implementar y verificar. Cada fase produce un artefacto que guía la siguiente, y la verificación permite corregir el ciclo cuando el resultado no cumple lo esperado.

## Conceptos clave

### El poder de un proceso repetible

SDD introduce un ciclo de cinco fases que guía el desarrollo de principio a fin:

- **Especificar**: definir qué debe hacer el software y cómo verificarlo.
- **Planificar**: decidir el enfoque y la arquitectura.
- **Desglosar en tareas**: dividir el trabajo en unidades manejables y verificables.
- **Implementar**: construir las unidades, a menudo delegando tareas a agentes.
- **Verificar**: comprobar los resultados frente a la especificación.

### Definición de SDD

El desarrollo guiado por especificaciones se basa en:

- Una especificación precisa que indique qué hace el software y cómo medir el éxito.
- La especificación como artefacto principal para guiar el desarrollo.
- Un documento vivo que se revisa, actualiza y reutiliza.

### El papel de los agentes de codificación

Los agentes ejecutan tareas basándose en la especificación y pueden amplificar tanto sus fortalezas como sus debilidades:

- Una especificación precisa favorece una implementación eficiente y exacta.
- Una especificación ambigua o incompleta puede producir errores y malentendidos acumulativos.

### Una especificación no es solo una indicación detallada

- **Indicación o prompt**: suele estar orientado a obtener una salida inmediata.
- **Especificación**: se revisa antes de implementar, se usa para verificar el resultado y puede reutilizarse en futuras iteraciones.

### Beneficios del desarrollo guiado por especificaciones

- El trabajo puede revisarse antes de que exista una implementación, lo que ayuda a reducir retrabajos costosos.
- Los resultados pueden juzgarse con un estándar claro, mejorando la calidad y la alineación.
- Un proceso repetible facilita la colaboración y el mantenimiento a largo plazo.

## Las cinco fases del ciclo SDD

1. **Especificar**
   - Definir el comportamiento requerido, las restricciones y los criterios de aceptación.
   - **Artefacto**: documento de especificación.
2. **Planificar**
   - Decidir el enfoque, la arquitectura y los límites.
   - **Artefacto**: plan.
3. **Desglosar en tareas**
   - Dividir el plan en unidades de trabajo ordenadas y atómicas.
   - Definir un resultado verificable para cada tarea.
   - **Artefacto**: lista de tareas.
4. **Implementar**
   - Ejecutar las tareas.
   - **Artefacto**: código y otros resultados de cada tarea.
5. **Verificar**
   - Comprobar los resultados frente a los criterios de aceptación.
   - **Artefacto**: evaluación de conformidad y observaciones.

### Qué hacer si falla la verificación

El ciclo vuelve a la fase responsable del problema:

- **Comportamiento incorrecto**: regresar a **especificar** para aclarar los requisitos.
- **Problemas arquitectónicos**: regresar a **planificar** para revisar las decisiones.
- **Problemas en el desglose**: regresar a **tareas** para ajustar la granularidad.

Cada fase produce un artefacto que consume la siguiente. Saltarse una fase no elimina ese trabajo: lo traslada a una etapa donde puede quedar sin revisar y el ciclo pierde parte de su capacidad de corregirse.

## Ejemplo: añadir una función de «Me gusta»

- **Especificar**: definir qué cuenta como un «me gusta» y cómo verificarlo.
- **Planificar**: decidir si la lógica se ejecutará en el cliente o en el servidor.
- **Desglosar en tareas**: crear tareas como «Implementar el endpoint de la API para los me gusta» y «Actualizar la interfaz para mostrar el estado».
- **Implementar**: desarrollar los componentes de la API y de la interfaz.
- **Verificar**: comprobar que al pulsar el botón aumenta el contador y que el cambio queda guardado.

Si la verificación detecta que el conteo no se guarda, el ciclo puede regresar a **planificar** para reconsiderar el enfoque de almacenamiento.

## Qué ocurre si se omite una fase

- **Omitir Especificar**: no hay una definición clara de qué construir y la verificación carece de un comportamiento acordado como referencia.
- **Omitir Planificar**: las tareas pueden asumir arquitecturas distintas y provocar fallos de integración.
- **Omitir el desglose en Tareas**: la implementación carece de límites claros y la revisión se vuelve difícil.
- **Omitir Verificar**: no hay retroalimentación, los errores pueden propagarse y el proceso deja de ser un ciclo.

## Gestionar cambios en los requisitos

Cuando cambia un requisito:

1. Actualiza los criterios de aceptación en la especificación.
2. Identifica qué partes del plan dependen de los criterios modificados.
3. Regenera solo las tareas afectadas por esos cambios.
4. Regenera el código correspondiente a esas tareas.
5. Verifica los cambios frente a la especificación actualizada.

La regeneración dirigida mantiene el flujo enfocado y evita retrabajos innecesarios.

## Mantener la especificación en el repositorio

- **Control de versiones**: el historial registra los cambios y permite revisar qué se acordó anteriormente.
- **Visibilidad**: la especificación está junto al código y es accesible para quienes trabajan en el proyecto.
- **Sincronización**: confirmar juntos los cambios relacionados en la especificación y el código ayuda a mantenerlos alineados.

## Cómo gestionar la especificación y el código juntos

1. **Almacena el archivo de especificación en una carpeta dedicada** dentro del repositorio, como `/spec` o `/docs/spec`. Usa formatos claros y estructurados, como Markdown o YAML, para mantenerlo legible para las personas y procesable por herramientas.
2. **Confirma los cambios de la especificación junto con los cambios relacionados en el código.** Por ejemplo, si actualizas los criterios de aceptación de una función, edita tanto el archivo de especificación como el código de implementación antes de confirmar:

   ```bash
   git add /spec/feature-x.md src/feature-x.js
   git commit -m "Actualizar especificación e implementación de la función X"
   ```

3. **Crea pull requests (PR) que incluyan los cambios relacionados en la especificación y el código.** Así, quienes revisen podrán comparar ambos cambios y verificar que la implementación coincide con los requisitos actualizados.

## Referencias

- Pendiente de añadir.
