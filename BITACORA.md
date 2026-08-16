# Bitácora

> Completá este archivo y dejalo en la raíz de tu repositorio.
> **Una página alcanza.** En serio: no buscamos un ensayo, buscamos lo concreto.
> Las tres últimas preguntas son las mismas que vas a tener que pegar en el formulario de entrega, así que escribilas una sola vez, acá.

---

## 1 · Qué hice

Tres o cuatro líneas. Lo que tocaste, en el orden en que lo tocaste.

- Primero leí completo el caso práctico y el README como contrato; después, la consigna, la Resolución 118 y la bitácora. Recién entonces recorrí código y tests, separando hechos de hipótesis.
- Establecí un baseline de 15 tests y typecheck en verde. Para cada defecto escribí un test que reprodujera el incumplimiento y seguí RED → corrección mínima → suite completa y typecheck.
- Corregí tres incumplimientos concretos: el límite inclusivo de entrada a las 08:10; el divisor nocturno del turno mixto, que pasó de 48.750 G$ → 55.714 G$; y el feriado en un cruce de medianoche, cuyo caso 30/04–01/05 quedó en 120 minutos ordinarios y 360 de feriado.
- Implementé la Resolución 118 con adhesión opcional, 40% para ordinarias alcanzadas y base multiplicativa 2,80 para extras nocturnas. Cubrí cuatro casos de adhesión, vigencia y compatibilidad histórica; el cierre fue de 22 tests y typecheck en verde, integrado en cuatro PRs.

---

## 2 · Qué recorté del alcance, y por qué

Qué decidiste **no** hacer, y con qué criterio. Si tuvieras tres horas más, ¿qué harías primero?
No hace falta que nos digas cuánto tardaste: decinos qué quedó afuera y por qué, que es lo que de verdad nos sirve.

- Prioricé los riesgos contractuales que alteraban liquidaciones: los tres incumplimientos y la Resolución 118. Excluí la refactorización amplia de `calcularJornada`, la validación exhaustiva y un modelo de feriados más rico; también la matriz combinatoria de la Resolución con feriados, jornaleros, ventanas personalizadas y cruces de vigencia, porque ampliaban la superficie sin resolver otro incumplimiento confirmado.
- Con tres horas más, primero probaría el intervalo posterior a medianoche. Después aclararía con negocio qué régimen corresponde cuando una jornada cruza la fecha efectiva.

---

## 3 · Cómo trabajaste con la IA

La parte que más nos interesa de toda la bitácora. **No queremos la solución: queremos el camino.**

Tres cosas concretas, con ejemplos y no con descripciones generales:

- **Qué le pediste**, y cómo le armaste el contexto antes de pedírselo.
- **En qué momento no le hiciste caso**, y cómo te diste cuenta de que estaba equivocada. Un caso puntual vale más que un párrafo.
- **Qué no le delegás nunca**, y por qué.

> Si mandás el historial de la sesión, decilo acá y no repitas lo que ya está ahí. Y si no usaste IA, también está bien: contanos cómo trabajaste.

- **Qué le pedí y cómo armé el contexto:** antes de pedir código, le hice leer caso, README, consigna, resolución y bitácora, y luego recorrer implementación y tests. Cada propuesta debía distinguir hechos de hipótesis y partir de un RED reproducible.
- **Cuándo no le hice caso:** PowerShell interpretó `G$100,000` como variable y guardó `G,000` en un commit; lo detecté al inspeccionarlo y lo corregí. También rechacé commits breves o en inglés: exigí mensajes detallados en español con problema, observado, esperado, causa, solución y verificación.
- **Qué no le delego nunca:** la interpretación final del dominio, el alcance ni la aceptación. Contrasté cada propuesta con contrato y pruebas; por ejemplo, decidí explícitamente la semántica parcial de `esFeriado` y la lectura multiplicativa del artículo 3.

---

## 4 · Qué parte de mi solución no me da confianza

Qué dejaste con dudas, qué no llegaste a verificar, qué te parece frágil.
Decir "esto no lo entendí y no quise adivinar" es una respuesta válida y buena.

- La Resolución no formaliza la composición del artículo 3 ni el criterio de vigencia para jornadas que cruzan la fecha efectiva. Asumí base multiplicativa y fecha inicial; están probadas, pero las confirmaría con negocio antes de usarlas en producción.
- No verifiqué si, en un turno 22:00–06:00, el intervalo 02:00–03:00 se construye sobre la fecha incorrecta. Además, `esFeriado` sigue siendo booleano: conserva minutos por categoría, pero no distingue una jornada parcial de una totalmente feriada.

---

## Preguntas o comentarios sobre el ejercicio

Opcional. Si algo del enunciado, del README o de la resolución te pareció ambiguo, mal escrito o directamente equivocado, este es el lugar.

- ¿La vigencia de una jornada que cruza la fecha efectiva se decide por su inicio o por cada tramo?
- ¿El artículo 3 pretende que adicional nocturno y recargo extraordinario se compongan multiplicativamente?
