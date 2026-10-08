# Los límites de la programación asistida por IA

**Fecha:** 2026-10-08

## Resumen

La generación rápida de código deja de ser una ventaja cuando el resultado no resuelve el problema previsto, requiere mucho esfuerzo de revisión o acumula correcciones. Las especificaciones ayudan a definir con claridad qué debe hacer el código y permiten comprobar si la implementación se mantiene alineada con ese objetivo.

## Conceptos clave

### El límite de la generación rápida

El código generado rápidamente puede acelerar el trabajo, pero esa velocidad no garantiza que el resultado sea correcto ni mantenible. Es importante reconocer cuándo la revisión, la corrección y la integración cuestan más que lo que se ahorró al generar el código.

### Desviación

La **desviación** ocurre cuando la IA produce código plausible que funciona, pero resuelve un problema distinto al previsto. Puede pasar inadvertida durante las verificaciones iniciales y aparecer más tarde durante la integración o en producción.

### Cambio de costos

Con la programación asistida por IA, el cuello de botella puede desplazarse de escribir código a revisarlo, corregirlo y rehacerlo. Por eso, la velocidad de generación por sí sola no representa el costo total de una implementación.

### Vibe Coding

El *Vibe Coding* puede ser útil para:

- Explorar ideas rápidamente.
- Crear prototipos desechables.
- Escribir scripts puntuales.
- Aprender nuevas librerías.

Estos usos se centran en la exploración y no implican necesariamente que el código resultante esté preparado para mantenerse a largo plazo.

### Requisitos de un código mantenible

El código mantenible debe ser:

- **Legible por otras personas.**
- **Modificable con el tiempo.**
- **Estable en su comportamiento.**
- **Predecible en sus modos de fallo.**

## El costo de las implementaciones desviadas

Una implementación desviada puede recorrer este ciclo:

1. **Generación**: la IA produce código a partir de una solicitud poco especificada.
2. **Revisión**: el código supera las verificaciones iniciales porque parece plausible.
3. **Descubrimiento**: los problemas aparecen más tarde, durante la integración o en producción.
4. **Re-prompt**: el desarrollador debe aclarar y volver a especificar los requisitos.
5. **Corrección**: se aplican arreglos parciales que pueden dejar problemas ocultos.
6. **Reescritura**: en los casos más graves, es necesaria una reescritura completa.

## Por qué importan las especificaciones

- **Longevidad**: una especificación sobrevive a un intento de generación; puede revisarse, refinarse y reutilizarse.
- **Claridad**: expresa los comportamientos esperados, las restricciones y los casos límite.
- **Responsabilidad**: desplaza el foco de escribir código a definir el objetivo que debe cumplir.
- **Verificación**: proporciona una referencia concreta para comprobar el código generado y detectar desviaciones.

## Elaboración de especificaciones efectivas

Una especificación debe declarar claramente:

- **Comportamiento esperado**: qué debe hacer exactamente la función.
- **Restricciones**: límites de rendimiento, seguridad u operación.
- **Casos límite**: cómo manejar errores, concurrencia o entradas inusuales.

## Integrar especificaciones en el flujo de trabajo

1. **Antes de la generación**: revisa la especificación con las partes interesadas para detectar ambigüedades pronto.
2. **Durante la generación**: usa la especificación como fuente de verdad.
3. **Después de la generación**: compara el resultado con la especificación para detectar desviaciones.

## Ejemplo: ciclo de una implementación desviada

Una solicitud poco especificada puede producir código que parece correcto y supera las verificaciones iniciales. Si el desajuste se descubre durante la integración, el desarrollador tendrá que aclarar los requisitos, corregir la implementación y, en el peor caso, reescribirla. Una especificación explícita ofrece un criterio para reconocer antes si el resultado satisface el objetivo.

## Referencias

- Pendiente de añadir.
