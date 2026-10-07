# Estructuras de datos en Java

**Asignatura:** Estructuras de Datos · **Trabajo:** individual · **Código:** disponible bajo petición

Cinco actividades en las que implemento tipos abstractos de datos **genéricos** en Java. Cada actividad reutiliza la anterior: listas → tablas hash → grafo bipartito → recomendador.

## Qué hace

| Actividad | Contenido |
|---|---|
| 0 · Calculadora | Calculadora decimal y binaria sobre una interfaz común y una clase abstracta, con excepciones propias. |
| 1 · Listas | `TADLlista<E>` con tres implementaciones: **estática** (array), **dinámica** (nodos enlazados) y sobre **`ArrayList`**. Carga de 1000 canciones desde CSV. |
| 2 · Tablas hash | `IHashMap<K,V>` con **encadenamiento indirecto** (listas propias), **direccionamiento abierto** (sondeo lineal con marcas de borrado) y sobre `java.util.HashMap`. Rehash que duplica el tamaño al llegar al 75 % de factor de carga, e iteración ordenada. |
| 3 · Grafo bipartito | `GrafBipartit<K1,V1,K2,V2,E>` como **multilista dinámica**: una tabla hash por cada lado y listas de adyacencia con peso. Modela usuarios ↔ canciones con valoraciones del 1 al 5, cargadas desde CSV. Incluye consultas de grado, adyacencias, usuarios con canciones en común y medias de valoración. |
| 4 · Recomendador | Recomendador de artistas sobre el grafo bipartito con datos reales de **Last.fm** (1000 usuarios, 15103 artistas, 48655 relaciones). Busca usuarios parecidos por sexo, edad, país y artistas favoritos, y recomienda lo que han escuchado y el usuario aún no conoce. |

Salida real del recomendador:

```
=== RECOMANADOR D'ARTISTES ===

Dades carregades correctament.
Usuaris: 1000
Artistes: 15103
Valoracions (escoltes): 48655
```

## Calidad

- **423 tests JUnit 5**, todos en verde (`./gradlew test`).
- Build multiproyecto de Gradle con wrapper: un único comando compila y prueba las cinco actividades.
- Las interfaces de los TAD, la configuración de Gradle y los tests los proporcionaba el profesorado. Las implementaciones, la carga de datos y el recomendador son míos.

## Tecnologías

Java 21 · Gradle · JUnit 5 · Genéricos · Estructuras enlazadas · Hashing
