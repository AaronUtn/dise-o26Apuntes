# Resumen y Apuntes: Arquitecturas Concurrentes - Episodio 1
**"El diablo está en los detalles"** (por Franco Bulgarelli / *flbulgarelli*)

Este documento resume los conceptos clave del primer episodio de la serie sobre Arquitecturas Concurrentes, explorando la definición de arquitectura de software, sus restricciones, el concepto de abstracciones con fugas y las cualidades de calidad (atributos de calidad) como la escalabilidad.

---

## 1. ¿Qué es la Arquitectura de Software? (Más allá del diagrama)

* **Definición:** La arquitectura de software no se limita a diagramas de cajas y flechas ni a documentación estática. Es el conjunto de **decisiones de diseño significativas e irreversibles** (o difíciles de cambiar) que estructuran un sistema, definiendo sus componentes, responsabilidades, fronteras y reglas de interacción.
* **El "diablo está en los detalles":** Aunque la arquitectura busca abstraernos de la complejidad técnica macro, las decisiones de alto nivel condicionan e impactan directamente el código de todos los días. 

### Ejemplo:
Un desarrollador puede escribir una función para guardar un usuario. Si la arquitectura se diseñó sobre un esquema de eventos asincrónicos (como Event Sourcing), el desarrollador no puede asumir una consistencia inmediata (`Read-Your-Own-Writes`) ni que la transacción se completó síncronamente al salir del método.

---

## 2. Restricciones e Invisibilidad de la Arquitectura

* **El terreno de juego:** La arquitectura establece las reglas y fronteras dentro de las cuales se programa.
* **Invisibilidad:** A medida que el equipo se acostumbra a un marco de trabajo o patrón (ej. MVC, Microservicios, Ports & Adapters), las restricciones arquitectónicas se vuelven **invisibles**: los desarrolladores escriben código respetando las reglas de forma natural sin cuestionar su origen.

### Ejemplo:
En un framework como Spring Boot o Ruby on Rails, un programador crea un controlador y un servicio siguiendo el flujo preestablecido. Siente que "solo programa", pero está operando estrictamente dentro del ciclo de vida y las reglas de inyección de dependencias impuestas por la arquitectura.

---

## 3. Abstracciones e "Ilusiones" con Fugas (*Leaky Abstractions*)

* **Ilusiones útiles:** La arquitectura provee abstracciones para simplificar la complejidad del hardware, los hilos de ejecución o la red.
* **Fuga de abstracción:** Ninguna abstracción es perfecta. Cuando el sistema se somete a alta carga, concurrencia o fallas de red, la ilusión se "filtra" (*leaks*) y el desarrollador se ve obligado a entender los detalles de bajo nivel para corregir el problema.

### Ejemplo:
Un ORM (como Hibernate o Sequelize) abstrae la base de datos haciendo parecer que las tablas son colecciones de objetos en memoria. Cuando el sistema escala y el ORM genera el problema de rendimiento N+1 (múltiples consultas SQL individuales), la abstracción falla y el programador debe bajar a optimizar las consultas SQL manualmente.

---

## 4. Atributos de Calidad (*Quality Attributes*) y Escalabilidad

La arquitectura no existe en el vacío; se diseña para satisfacer **cualidades de calidad** (requisitos no funcionales) que determinan cómo se comporta el sistema bajo distintas condiciones:

1. **Escalabilidad:** Capacidad del sistema para manejar un crecimiento en la carga de trabajo (peticiones, usuarios, volumen de datos) añadiendo recursos, sin degradar significativamente su rendimiento.
   * *Escalabilidad Vertical (Scale Up):* Agregar más hardware (CPU, RAM) a un servidor existente.
   * *Escalabilidad Horizontal (Scale Out):* Agregar más instancias o nodos distribuidos para repartir la carga.
2. **Disponibilidad (*Availability*):** Porcentaje de tiempo que el sistema permanece operativo y accesible para los usuarios.
3. **Mantenibilidad y Modificabilidad:** Facilidad para extender, corregir o modificar el sistema a lo largo del tiempo sin romper funcionalidades existentes.
4. **Desempeño / Latencia (*Performance*):** Tiempos de respuesta y capacidad de procesamiento por unidad de tiempo (*throughput*).

### Ejemplo de Mapeo a la Concurrencia:
Para lograr **escalabilidad horizontal** en una aplicación web, la arquitectura exige que los componentes sean **sin estado (*stateless*)**. Si un componente guarda variables globales en memoria local, la arquitectura no podrá escalar agregando múltiples servidores balanceados.

---

## 5. Introducción a la Concurrencia en la Arquitectura

El artículo concluye vinculando la arquitectura con el desafío central de la serie: **la concurrencia**.

* La concurrencia no es solo un problema de sintaxis (usar `threads`, `promises` o `async/await`).
* Es un **desafío arquitectónico de alto nivel**: implica decidir cómo se modela el estado, cómo interactúan múltiples tareas en simultáneo y cómo se evitan problemas como condiciones de carrera (*race conditions*) y bloqueos mutuos (*deadlocks*).

---

## Esquema Resumen de Conceptos

```
                     ARQUITECTURA DE SOFTWARE
                                │
       ┌────────────────────────┼────────────────────────┐
       ▼                        ▼                        ▼
Define Restricciones      Crea Abstracciones      Busca Atributos
 (Reglas invisibles)     (Ilusiones que pueden     de Calidad
  para el desarrollador   filtrarse por detalles)  (Escalabilidad,
       │                        │                  Disponibilidad, etc.)
       └────────────────────────┴────────────────────────┘
                                │
                                ▼
                   DESAFÍO: SISTEMAS CONCURRENTES
              (Requieren arquitecturas diseñadas para
               gestionar el estado y el tiempo)
```

*Documento basado en el Episodio 1 de la serie "Arquitecturas Concurrentes" por Franco Bulgarelli.*