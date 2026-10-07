# Arkanoid concurrente

**Asignatura:** Fundamentos de Sistemas Operativos · **Trabajo:** en pareja · **Código:** disponible bajo petición

Un *Arkanoid/Breakout* en terminal (ncurses) que, a lo largo de cinco fases, se transforma de un programa secuencial en uno **concurrente** con procesos, hilos y comunicación entre procesos de System V.

## Qué hace, fase a fase

| Fase | Qué se introduce |
|---|---|
| 0 | Versión **secuencial**: campo de juego, paleta controlada por teclado, pelota que rebota y bloques que se rompen. |
| 1 | Cada pelota es un **proceso** (`fork` + `execlp`). El tablero y los contadores viven en **memoria compartida**. Al romper ciertos bloques nace una pelota nueva. |
| 2 | **Semáforos** para proteger la pantalla y las variables compartidas, y un **buzón de mensajes** con el que las pelotas piden al proceso principal que cree pelotas nuevas. |
| 3 | Arquitectura **híbrida**: el proceso principal es **multihilo** (pthreads), con un hilo para la paleta del jugador y otro para cada paleta autónoma, sincronizados con *mutex*. |
| 4 | **Superpoderes** (bloques que dan 5 s en los que las pelotas destruyen el muro) y **sacrificios**: la pelota que se pierde reparte su velocidad entre las demás mediante un segundo buzón que cada pelota escucha con su propio hilo. El proceso principal recoge a los hijos con `waitpid` para que no queden procesos *zombie*. |

También hicimos un script para limpiar los recursos IPC que quedan huérfanos si una ejecución se interrumpe.

## Mi aportación

Fue un **trabajo conjunto en todas las fases (0-4)**. Diseñamos, programamos y depuramos cada fase entre los dos, sin repartirnos el trabajo por módulos.

## Tecnologías

C · Linux · `fork`/`exec`/`waitpid` · IPC System V (memoria compartida, semáforos, colas de mensajes) · pthreads · ncurses · Make
