# Resumen y Apuntes: Feminismo de Datos y Arquitectura Conceptual de Sistemas

Este documento recopila el análisis, resumen y desgloses conceptuales del Capítulo 1 (*Examine Power*) e Introducción del libro ***Data Feminism*** **(Feminismo de Datos)** de Catherine D'Ignazio y Lauren F. Klein (MIT Press), junto con su aplicación directa al diseño y arquitectura conceptual de software.

---

## 1. Resumen General del Texto

### Diagnóstico del problema

* **El "God Trick" (El truco de Dios):** La ciencia de datos tradicional opera bajo la falsa premisa de que los algoritmos y los datos ofrecen un punto de vista "neutral", "objetivo" y desde la nada. El texto denuncia que este punto de vista desencarnado suele ser en realidad el punto de vista del grupo dominante (hombres, blancos, cisgénero, del Norte global).

* **La Matriz de Dominación:** Apoyándose en la socióloga interseccional Patricia Hill Collins, el texto sostiene que el poder y la opresión operan a través de 4 dominios interconectados: Estructural, Disciplinario, Hegemónico e Interpersonal.

### Principios Fundamentales

* **Examinar el Poder (*Examine Power*):** Revelar, visibilizar y analizar cómo las desigualdades de la sociedad están codificadas en los conjuntos de datos, en las bases de datos y en las reglas del software.

* **Desafiar el Poder (*Challenge Power*):** Utilizar la tecnología, los datos y el diseño para desmantelar las asimetrías de poder y trabajar hacia la justicia social.

### Ejemplos Clave del Texto

1. **Christine Darden y las "computadoras humanas" en la NASA:** Christine Darden, con maestría en matemáticas, fue asignada durante años al pool de "computadoras humanas" (reservado a mujeres), mientras que hombres con sus mismas credenciales ascendían rápidamente como ingenieros. Ilustra cómo las estructuras disciplinarias e institucionales invisibilizan el trabajo de ciertos grupos.

2. **Mortalidad materna en EE. UU. y datos faltantes:** Investigaciones revelaron que las mujeres negras con educación universitaria sufrían más complicaciones en el parto que mujeres blancas sin secundario completo. Demuestra que métricas genéricas ignoran las intersecciones de raza y clase.

3. **Puntajes de riesgo predictivo (COMPAS):** Algoritmos en el sistema judicial que otorgan mayor riesgo a personas negras/latinas basándose en datos históricos de arrestos (que reflejan patrullaje policial discriminatorio, no mayores tasas reales de delito). Muestra la "limpieza" algorítmica de la discriminación con fachada de objetividad.

4. **"Contradatos" (*Counter-data*):** Proyectos comunitarios que registran datos de manera independiente cuando las instituciones oficiales se niegan a hacerlo o manipulan las cifras (ej. registros ciudadanos de detenciones por perfilamiento racial).

5. **Visibilidad vs. Vigilancia (*Surveillance*):** Para grupos privilegiados, ser visible en los datos significa representación y acceso a servicios; para grupos marginados, ser visible muchas veces significa hipervigilancia y control.

---

## 2. Desglose de Conceptos Clave

### A. La Matriz de Dominación

La Matriz de Dominación describe cómo la opresión se organiza en la sociedad a través de 4 dominios:

```
                      ┌─────────────────────────────────┐
                      │    MATRIZ DE DOMINACIÓN         │
                      └────────────────┬────────────────┘
                                       │
         ┌──────────────────┬──────────┴──────────┬──────────────────┐
         ▼                  ▼                     ▼                  ▼
  ┌──────────────┐   ┌──────────────┐      ┌──────────────┐   ┌──────────────┐
  │ Estructural  │   │Disciplinario │      │  Hegemónico  │   │Interpersonal │
  │(Leyes/Infra) │   │(Burocracia)  │      │  (Cultura)   │   │(Experiencia) │
  └──────────────┘   └──────────────┘      └──────────────┘   └──────────────┘
```

1. **Dominio Estructural:** Leyes, políticas de Estado e infraestructura macro (ej. Leyes de migración o la distribución de sucursales bancarias por zonas).

2. **Dominio Disciplinario:** Reglas de juego diarias, burocracia y normativas organizacionales (ej. Exigir recibo de sueldo formal e historial de 5 años para pedir un crédito).

3. **Dominio Hegemónico:** Ideas, estereotipos y cultura compartida (ej. La noción social de que *"el hombre joven es el estándar de profesional tecnológico competente"*).

4. **Dominio Interpersonal:** Experiencias cotidianas e interacciones individuales (ej. *Manterrupting* en reuniones técnicas o acoso a personas trans por inconsistencias con el DNI).

### B. "Examinar el Poder" en Datos y Entidades

* **En Esquemas de Base de Datos:** Crear campos como `genero ENUM('M', 'F')` o exigir `nombre_completo` estricto bajo el formato occidental `[Nombre] [Apellido]` define implícitamente qué es un ser humano "válido" para el sistema, excluyendo a personas no binarias o personas con estructuras de nombre diversas.

* **En Datasets de Entrenamiento y Prueba:** Entrenar o testear un modelo con datasets donde la mayoría son hombres blancos de entre 20 y 30 años genera sistemas que fallan estrepitosamente al reconocer rostros o voces de mujeres o personas con pieles oscuras.

### C. Desafiar el Poder

* **Ejemplo Práctico:** El mapa interactivo de femicidios creado por la investigadora María Salguero en México. Ante la omisión del Estado en registrar adecuadamente estos crímenes, utilizó prensa y fuentes abiertas (OSINT) para crear un mapa detallado que visibilizó miles de casos, arrebatando el monopolio de la narrativa a las autoridades.

---

## 3. Conexión con la Arquitectura Conceptual de Sistemas

La arquitectura de software no es un instrumento neutro; refleja la ideología y los privilegios de quienes la diseñan y financian.

```
                  ┌────────────────────────────────────────┐
                  │   Matriz de Dominación (Poder)         │
                  │   Estructural | Disciplinario          │
                  │   Hegemónico  | Interpersonal         │
                  └───────────────────┬────────────────────┘
                                      │
                                      ▼
             ┌──────────────────────────────────────────────────┐
             │ Lentes e Ideología del Diseñador / Arquitecto    │
             └──────────────┬───────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                      ARQUITECTURA CONCEPTUAL DE SISTEMAS                        │
├────────────────────────────────┬────────────────────────────────────────────────┤
│ Modelo de Datos / Entidades    │ Codifica binarios, esquemas rígidos y jerarquías. │
├────────────────────────────────┼────────────────────────────────────────────────┤
│ Algoritmos / Reglas de Negocio │ Automatiza y perpetúa reglas disciplinarias.    │
├────────────────────────────────┼────────────────────────────────────────────────┤
│ Perfiles / Permisos (RBAC)     │ Define quién tiene agencia, visibilidad y control.│
└────────────────────────────────┴────────────────────────────────────────────────┘
```

### Reflejo de los Financiadores

* **Gig Economy (Apps de Delivery):** Arquitectura optimizada para métricas financieras de inversores (evaluación unidireccional cliente-repartidor, penalizaciones automáticas por rechazar viajes sin contemplar clima o zonas peligrosas).

* **Triaje Médico:** Algoritmos que utilizaron el gasto previo de dinero en salud como *proxy* de necesidad médica, desplazando a personas de menores recursos que históricamente gastaban menos por falta de acceso y no por estar más sanas.

---

## 4. El Principio de Interseccionalidad y los "Puntos Ciegos"

La **interseccionalidad** (Kimberlé Crenshaw) demuestra que las discriminaciones no actúan de forma aislada, sino que se cruzan creando vivencias de opresión únicas.

```
       [ Discriminación de Género ]
                  │
                  ▼
          ┌──────────────┐
          │ INTERSECCIÓN │ ──► Experiencia de exclusión única
          └──────────────┘
                  ▲
                  │
        [ Discriminación de Raza ]
```

### El Punto Ciego en la Arquitectura (Ejemplo SQL)

Si un algoritmo de selección de personal evalúa métricas en canales separados:

```sql
-- Métrica de género (Devuelve 50% mujeres)
SELECT COUNT(*) FROM contrataciones WHERE genero = 'Femenino';

-- Métrica étnica (Devuelve 30% afrodescendientes)
SELECT COUNT(*) FROM contrataciones WHERE etnia = 'Afrodescendiente';
```

El sistema reporta un "falso positivo de justicia". Sin embargo, si la arquitectura no permite o no ejecuta la **consulta interseccional**:

```sql
-- Consulta interseccional que revela el punto ciego
SELECT COUNT(*) FROM contrataciones 
WHERE genero = 'Femenino' AND etnia = 'Afrodescendiente';
```

El resultado puede ser **0**. La omisión de análisis interseccionales en el modelo de datos encubre discriminaciones sistémicas contra grupos específicos.

---

## 5. Conceptos Adicionales de la Introducción

1. **Feminismo como Marco Analítico:** Se define como creencia en la igualdad, compromiso de acción y herramienta de análisis de poder aplicable a cualquier sistema.

2. **Datos Faltantes (*Missing Data*):** La falta de datos sobre ciertos problemas (ej. acoso callejero) es una decisión política de las instituciones con poder.

3. **Cuestionar el Big Data:** Más volumen de datos no corrige el sesgo, sino que lo amplifica a mayor escala. Los datos siempre tienen contexto.

4. **Data Hazard (Riesgo de Datos):** Publicar o recopilar datos de comunidades vulnerables puede usarse para vigilarlas o perseguirlas. Se relaciona con la *Privacidad por Diseño*.

---

## 6. Explicación Detallada de los 7 Principios del Feminismo de Datos y su Aplicación en Software

A continuación se detalla cada uno de los **7 principios** propuestos por Catherine D'Ignazio y Lauren F. Klein, junto con su traducción directa a prácticas concretas de ingeniería de software y arquitectura de sistemas:

### 1. Examinar el Poder (*Examine Power*)
* **Definición Teórica:** Analizar cómo las estructuras de poder y las desigualdades sociales operan en el mundo y cómo quedan codificadas en los sistemas de información.
* **Aplicación en Desarrollo de Software:**
  * **Ingeniería de Requerimientos:** Preguntarse críticamente durante el descubrimiento de producto: ¿A quién beneficia esta funcionalidad? ¿A quién vigila, penaliza o margina?
  * **Modelado de Dominio:** Identificar si las entidades representadas imponen privilegios o jerarquías no cuestionadas (por ejemplo, definir un tipo único de "usuario estándar" que en verdad asume una persona de clase media/alta con conectividad permanente).
  * **Auditoría de Datasets:** Auditar los datos de entrenamiento y pruebas para verificar si reproducen discriminaciones históricas.

### 2. Desafiar el Poder (*Challenge Power*)
* **Definición Teórica:** Utilizar la tecnología, el diseño y los datos no para mantener el *statu quo*, sino para desmantelar asimetrías de poder e impulsar la justicia social.
* **Aplicación en Desarrollo de Software:**
  * **Diseño Centrado en la Justicia (*Design Justice*):** Crear plataformas orientadas al control ciudadano, la transparencia pública, la denuncia comunitaria o la preservación de derechos.
  * **Accesibilidad y Software Libre:** Priorizar licencias de código abierto, compatibilidad con tecnologías asistivas (WCAG) y optimización para redes de baja velocidad o dispositivos de gama baja (reducir brechas de acceso).
  * **Descentralización del control:** Diseñar arquitecturas donde la propiedad y la gobernanza del dato residan en los propios usuarios o comunidades, no en un único actor centralizado.

### 3. Elevar la Emoción y el Afecto (*Elevate Emotion and Affect*)
* **Definición Teórica:** Desafiar la premisa de que solo la información cuantitativa, fría y distante es "objetiva", validando el valor de los datos cualitativos, las emociones y la experiencia vivida.
* **Aplicación en Desarrollo de Software:**
  * **Diseño UX/UI y Visualización:** Superar los tableros de control (*dashboards*) puramente numéricos incorporando elementos narrativos, diseño empático, testimonios o datos de contexto humano.
  * **Formularios y Captura de Datos:** Evitar forzar todas las respuestas humanas a campos numéricos rígidos (escalas del 1 al 5); proveer espacios para datos cualitativos en texto libre, voz o registros narrativos.

### 4. Cuestionar las Clasificaciones y Categorías (*Rethink Binaries and Hierarchies*)
* **Definición Teórica:** Cuestionar las taxonomías binarias y las jerarquías rígidas que simplifican en exceso la diversidad y la complejidad del mundo real.
* **Aplicación en Desarrollo de Software:**
  * **Diseño de Bases de Datos:** Reemplazar enumeraciones binarias tipo `ENUM('M', 'F')` por atributos opcionales, textos libres o tablas maestras extensibles de identidad.
  * **Validación de Formularios y Lógica Frontend:** Eliminar validaciones de formato rígidas para nombres, direcciones o documentos que asumen un estándar occidental único (ej. requerir obligatoriamente dos apellidos, un único número de documento estatal o código postal en formatos rígidos).

### 5. Abrazar el Pluralismo (*Embrace Pluralism*)
* **Definición Teórica:** Priorizar la integración de múltiples perspectivas, saberes locales y comunitarios por encima de una "única fuente de verdad" impuesta centralizadamente.
* **Aplicación en Desarrollo de Software:**
  * **Sistemas Participativos:** Construir plataformas colaborativas donde las comunidades puedan etiquetar, aportar, corregir o validar los datos directamente.
  * **Arquitectura de Integración (APIs / Microservicios):** Diseñar interfaces que permitan conectar y procesar múltiples fuentes de datos locales con formatos heterogéneos, sin obligar a todas a convertirse a una estructura rígida central.

### 6. Considerar el Contexto (*Consider Context*)
* **Definición Teórica:** Reconocer que los datos no son hechos "puros" u "objetivos"; siempre se recolectan en un momento histórico, bajo ciertas reglas e intenciones específicas.
* **Aplicación en Desarrollo de Software:**
  * **Trazabilidad de Datos (*Data Lineage*):** Guardar metadatos explícitos en las tuberías de procesamiento (ETL) sobre *cómo*, *cuándo*, *dónde* y *con qué propósito* se capturó cada dato.
  * **Documentación Técnica de Modelos:** Adoptar estándares como *Datasheets for Datasets* o *Model Cards* para documentar formalmente las limitaciones, origen, sesgos conocidos y condiciones de uso adecuado de un conjunto de datos o modelo de ML.

### 7. Hacer Visible el Trabajo (*Make Labor Visible*)
* **Definición Teórica:** Reconocer y revalorizar todo el trabajo humano (a menudo precarizado e invisible) que permite que los sistemas de software y de datos funcionen.
* **Aplicación en Desarrollo de Software:**
  * **Reconocimiento en Documentación y Créditos:** Incluir explícitamente en la documentación y en los sistemas las tareas de moderación de contenido, limpieza de datos, etiquetado manual, soporte técnico y mantenimiento.
  * **Ética en la Operación de Plataformas:** Asegurar que los flujos de trabajo automatizados no exploten ni precaricen a los trabajadores humanos que entrenan, corrigen o moderan los contenidos de las aplicaciones.

---

### Resumen de Aplicación por Capa de Arquitectura

| Principio | Capa / Etapa del Software | Enfoque Práctico |
| :--- | :--- | :--- |
| **1. Examinar el Poder** | Requerimientos y Negocio | Cuestionar fines, sesgos y beneficiarios del sistema. |
| **2. Desafiar el Poder** | Arquitectura y Licenciamiento | Herramientas de auditoría social, código abierto, accesibilidad (WCAG). |
| **3. Elevar Emoción y Afecto** | Frontend / UX / UI | Dashboard narrativo, integración de datos cualitativos e interfaces empáticas. |
| **4. Cuestionar Clasificaciones** | Base de Datos / Validaciones | Esquemas flexibles, campos no binarios ni jerárquicos, formularios inclusivos. |
| **5. Abrazar el Pluralismo** | Integración / APIs | Múltiples fuentes heterogéneas, co-creación y datos comunitarios. |
| **6. Considerar el Contexto** | Data Engineering / Pipelines | Trazabilidad (*Data Lineage*), metadatos y *Datasheets for Datasets*. |
| **7. Hacer Visible el Trabajo** | Operaciones / Gestión | Documentar y dignificar el trabajo de moderación, etiquetado y mantenimiento. |

---
*Documento generado colaborativamente basado en el libro "Data Feminism" (MIT Press) y discusiones de Arquitectura Conceptual de Sistemas.*