# Candy Crush para Nintendo DS

**Asignatura:** Computadores · **Trabajo:** grupo de 4 (yo era el programador 2) · **Código:** disponible bajo petición

Versión de *Candy Crush* para la consola **Nintendo DS**. La lógica del juego está en **ensamblador ARM** y la parte gráfica en **C y ensamblador** sobre libnds, programando directamente la memoria de vídeo, los sprites y las interrupciones de los timers del hardware.

## Qué hace

- **Fase 1, lógica (ensamblador ARM):** tablero de 6 × 8 con caramelos, bloques sólidos, huecos y gelatinas simples y dobles. Detección y eliminación de secuencias, caída de elementos, recombinación del tablero y sugerencia de jugadas.
- **Fase 2, gráficos e interrupciones:** caramelos como sprites, tres fondos (gelatinas animadas, tablero ajedrezado e imagen de fondo), gráficos comprimidos con LZ77, transparencias entre fondos y animaciones controladas por las interrupciones de los cuatro timers: movimiento de sprites (timer 0), escalado (timer 1), gelatinas (timer 2) y desplazamiento del fondo (timer 3).

## Mi aportación

| Tarea | Descripción |
|---|---|
| **1C · `hay_secuencia`** (ARM) | Detecta si hay al menos una secuencia de 3 o más elementos iguales en horizontal o vertical, ignorando huecos y bloques sólidos y teniendo en cuenta las gelatinas. |
| **1D · `elimina_secuencias`** (ARM) | Marca cada grupo de secuencias con un identificador único. Las secuencias verticales que cruzan una horizontal reutilizan su identificador. Después elimina los elementos y rebaja el nivel de gelatina: la doble pasa a simple y la simple desaparece. |
| **2B · Fondo 2** (C) | Reserva de memoria de vídeo, **descompresión LZ77** de las baldosas en VRAM y generación del tablero ajedrezado con **metabaldosas** de 32 × 32 px. |
| **2F · Escalado de sprites** (ARM) | Rutina de servicio de interrupción del **timer 1** (unos 90 Hz) que, en 32 pasos, aumenta o reduce el factor de escalado de los sprites en coma fija 0.8.8. |
| **2Jb · Soporte de sprites** (ARM) | Activación del movimiento animado de un elemento entre dos casillas del tablero. |
| **Juego de pruebas** (C) | Programa de test con tres pantallas, una por cada parte: fondo 2, escalado y secuencias + movimiento. |

## Tecnologías

Ensamblador ARMv5TE · C · libnds / devkitARM · Nintendo DS · interrupciones y timers hardware · LZ77 · Make
