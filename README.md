# Banco de Preguntas Saber PRO — Taller 8

Proyecto académico de Laboratorio de Ingeniería de Software II de la Universidad del Cauca. Aplica los patrones State, Template Method, Decorator, Adapter y Facade sobre un modelo común de preguntas. Se conserva Builder como mecanismo de construcción del proyecto base.

## Patrones implementados

- **State:** controla el ciclo de vida de una pregunta y restringe las transiciones no permitidas.
- **Template Method:** centraliza cinco pasos de evaluación: validar pregunta, obtener/validar respuestas, comparar, determinar el resultado y generar retroalimentación. Incluye evaluadores para selección única, selección múltiple, verdadero/falso y pregunta abierta.
- **Decorator:** agrega características como dificultad alta, contextualización, retroalimentación, competencia y marca de revisión sin modificar `Question`.
- **Adapter:** recibe una pregunta de un servicio externo como JSON en un `String` y transforma `question_text` y `answer_text` al modelo interno.
- **Facade:** ofrece operaciones coordinadas para crear, consultar, cambiar estado, evaluar, decorar e importar preguntas.
- **Builder (base heredada):** permite construir preguntas abiertas, de selección múltiple y verdadero/falso.

## Tecnologías

- Java 21
- Maven
- JUnit 5.10.2

## Requisitos y ejecución

Se necesita JDK 21 y Maven 3.x. Verifica las instalaciones con `java -version` y `mvn -version`. Desde la carpeta del proyecto ejecuta:

```bash
mvn clean test
mvn exec:java
```

La clase principal es `co.unicauca.taller08.ApplicationMain`.

## Preguntas abiertas importadas

El servicio de ejemplo devuelve un JSON como:

```json
{
  "question_text": "¿Cuál es la capital de Colombia?",
  "answer_text": "Bogotá"
}
```

El Adapter transforma esos campos en una pregunta interna de tipo `OPEN`. `OpenQuestionEvaluator` compara la respuesta escrita después de normalizar mayúsculas, espacios y tildes; por ejemplo, `Bogotá`, `BOGOTA` y ` bogotá ` se consideran equivalentes. Para demostrar la evaluación a través de la Facade, la pregunta debe recorrer el ciclo de revisión y publicación antes de evaluarse.

## Estructura principal

```text
src/main/java/co/unicauca/taller08/
├── adapter/
├── builder/
├── decorator/
├── director/
├── domain/
├── facade/
├── state/
└── templatemethod/
```

## Nota de evaluación

Las preguntas solo se pueden evaluar cuando están publicadas. Las respuestas abiertas requieren una respuesta esperada no vacía.
