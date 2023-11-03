# Examen Parcial: Entretenimientos

## Aclaraciones sobre el parcial

- El parcial es **individual** y se entrega **pusheando a este repositorio** como en las entregas anteriores. Recomendamos _ir pusheando cada cierto tiempo_ para evitar inconvenientes, lo ideal es después de cada punto resuelto.
- No se tendrán en cuenta los commits realizados después de la hora de finalización del examen.
- Una vez hecho el _push_ final, **verifiquen en github.com** que haya quedado la versión final. Nosotros corregiremos lo que está en github, si ustedes lo pueden ver ahí entonces nosotros también.
- No olvidarse de **los conceptos aprendidos**: polimorfismo, delegación, buenas abstracciones, no repetir lógica, guardar vs calcular, lanzar excepción cuando un método no puede cumplir con su responsabilidad, etc. Eso es lo que se está evaluando.
- La solución del examen consiste en la **implementación de un programa** que resuelva los requerimientos pedidos y sus **tests automatizados**.
- Este enunciado es acompañado con un archivo `.wtest` que tiene diseñado los test a realizar. Es importante aclarar que:
  - Estos tests se proponen para facilitar el desarrollo. Se puede diseñar otros si así se considera necesario.
  - El conjunto de tests propuesto es suficiente para este examen. Hay casos que no están contemplados por un tema de tiempo (hay muchas combinaciones). No hace falta agregar nuevos, pero tampoco se prohibe hacerlo.
  - Todos los objetos allí usados se asumen como instancias de una clase. Si el diseño de la solución utiliza objetos autodefinidos en algunos casos entonces se debe remover la declaración de la variable y la línea en que se sugiere la instanciación
  - Según el diseño de la solución, es probable que se requiera agregar más objetos a los sugeridos en los tests
  - Los tests están comentados de manera de poder _ir incorporándolos a medida que se avanza_ con la solución del ejercicio


## Contexto

Se necesita un sistema para estudiar y simular los efectos
de los distintos entretenimientos sobre las personas

# 1. Entretenimientos

Un entretenimiento es un lugar o evento al cual pueden asistir personas.

Un entretenimiento tiene una capacidad máxima, por lo tanto no se puede ingresar 
si éste ya está agotado. 

Además de la condición de capacidad, considerar los siguientes casos especiales de entretenimiento:
- Un parque permite el ingreso siempre y cuando esté abierto (se sabe de cada parque si está abierto o no)
- Un ecoparque necesita que esté abierto (como cualquier parque) y además requiere que la persona que desea ingresar esté vacunada (información que se conoce de cada persona).
- Un Espectáculo tiene una entrada que se debe pagar, por lo tanto pueden ingresar las personas que puedan pagar la entrada

Cuando una persona ingresa a un entretenimiento, se debe guardar en algún lugar, ya 
que es un requerimiento conocer las personas que están asistiendo a un entretenimiento

Además:
- Si es un espectáculo se paga la entrada (se conoce de cada persona el dinero disponible)
- Si se trata de un partido de fútbol, se debe pagar la entrada como cualquier espectáculo,
pero además la experiencia deportiva de la persona asistente se incrementa en una unidad.

Tanto el dinero como la experiencia deportiva iniciales se conocen para cada persona 

## Requerimientos:

- Que una persona asista a un entretenimiento (tener en cuenta todas las variantes). 
- Saber las personas que están asistiendo a un entretenimiento
- Saber el dinero de una persona 
- Saber la experiencia deportiva de una persona
- Abrir/Cerrar un parque

## Casos de prueba

Personas:

- Marie es una persona que tiene 1000 de dinero y está vacunada, su experiencia deportiva es 5
- Pierre es una persona que tiene 10 de dinero y no está vacunada, su experiencia deportiva es 3

Entretenimientos:

- El parque domínico es un parque con capacidad para 1 persona y está cerrado.	
- El zoológico es un ecoparque con capacidad para 2 personas y está cerrado.
- Les Luthiers brinda un espectáculo con capacidad para 2 personas y precio de entrada 20
- Independiente-Juventus es un partido de fútbol con capacidad para 2 personas y precio de entrada 5

Casos:

- Si Marie intenta ingresar al parque domínico no lo logrará porque está cerrado,
pero si el parque domínico se abre entonces sí podrá ingresar.
Luego si intenta ingresar Pierre no lo logrará porque está la capacidad llena.

- Si marie intenta ingresar al parque zoológico no lo logrará porque está cerrado,
pero si el zoológico se abre entonces sí podrá ingresar.
Luego si intenta ingresar Pierre no lo logrará porque no está vacunado.

- Si Pierre intenta ingresar al espectáculo de Les luthiers no lo logrará porque no puede pagar la entrada.
En cambio María sí logra ingresar y su dinero quedaría en 980.

- Tanto Pierre como Marie  entran sin problemas a ver Indepentiende-Juventus,
María queda con 995 de dinero y 6 de experiencia deportiva, mientras que Pierre queda con
5 de dinero y 4 de experiencia deportiva. 


# 2. Ciudad

De una ciudad se conoce las personas residentes y la oferta de entretenimientos

## Escenario de prueba
Los requerimienos que se determinarán a continuación se pueden probar con el siguiente escenario:

- Usar a Marie y Pierre del punto anterior
- Emanuel es una persona con 2000 de dinero y está vacunado. Su  experiencia deportiva es 20
- Luciana es una persona con 30 de dinero y está vacunada. Su  experiencia deportiva es 15
- Quilmes es una ciudad con Marie, Pierre, Emanuel y Luciana como habitantes, y su oferta
de entretenimientos cuenta con el zoológico, el espectáculo de Les Luthiers e Independiente-Juventus
- Avellaneda es una ciudad con Marie y Pierre, y su oferta
de entretenimientos cuenta sólo con el parque Domínico.

Nota:  Marie y Pierre están en ambas ciudades para evitar la cantidad de objetos 
a crear en los tests. Si eso no es posible en tu modelo, entonces crea dos personas
distintas con los mismos atributos para ponerlos en la ciudad de Avellaneda, y
ajustar el test 2.3 para el cálculo de las personas aburridas.

## 2.1 bono cultural

Las ciudades que tienen 2 o más entrentenimientos pueden darle un monto de dinero a 
cada uno de los residentes a modo de un bono cultural. 
El valor del monto se determina al momento de aplicarlo.

### Requerimiento
- Aplicar un bono cultural de un valor a determinar a todas las personas de una ciudad

### Casos de ejemplo:

- No se podría aplicar un bono de 10 pesos a la ciudad de avellaneda porque no tiene al menos 2 entretenimientos.
- Al aplicar un bono de 10 pesos a quilmes los nuevos valores de dinero son:
	- Marie: 1010 
	- Pierre: 20
	- Emanuel: 2010
	- Luciana: 40 


## 2.2 Interesantes

El conjunto de personas interesantes de una ciudad es el que se forma por aquellas
personas que son consideradas como la más interesante de cada entretenimiento.
La persona más interesante de cada entretenimiento es la que menos dinero posee,
salvo para los partidos de fútbol que es la persona con más experiencia deportiva

### Requerimiento
- Saber las personas interesantes de una ciudad

### Caso de ejemplo

Si se abre el zoológico e ingresan Marie y Emanuel. 
Luego asisten Luciana y Emanuel a Independiente-Juventus.
Finalmente luciana y Emanuel van a ver a Les Luthiers.

Entonces el conjunto de personas interesantes de Quilmes está formada por:
Marie (es quien tiene menos plata en el zoológico), 
Emanuel (es quien tiene más experiencia deportiva en Independiente-Juventus)
y Luciana (es quien tiene menos plata en Les Luthiers).


## 2.3 Aburridas

El conjunto de personas aburridas de la ciudad son aquellas 
que no están asistiendo a ningún entretenimiento en dicha ciudad.

### Requerimiento
- Saber las personas aburridas de una ciudad

### Caso de ejemplo

Se abre el zoológico e ingresan Marie y Emanuel, luego Emanuel
asiste a Independiente-Juventus. 
Entonces las personas aburridas de Quilmes son Luciana y Pierre,
mientras que las aburridas de Avellaneda son Marie y Pierre

Aclaración: En avellaneda todos están aburridos porque ninguno de sus ciudadanos
asisten al parque domínico, único entretenimiento de la ciudad. Marié está
en un entretenimento de otra ciudad, por eso no cuenta para este caso.

# 3. Satisfaccion

La satisfacción que un entretenimiento le da a una persona es un número que se calcula,
a priori, como la diferencia entre la diversión que le da a la persona y la dificultad
de asistir a la misma. `diversion - dificultad`

Tener en cuenta que:
 - La diversión es un número que se establece para cada entretenimiento
 - la dificultad de un espectáculo es el valor de la entrada dividido dos veces 
   la cantidad del dinero que tiene la persona, a todo eso se le suma 1: `(entrada / (2 * dinero)) + 1`
 - la dificultad de un partido de fútbol es muy parecida a la de los espectáculos,
 la única diferencia es que se usa 5 veces la cantidad de dinero: `(entrada / (5 * dinero)) + 1`
 - la dificultad de un parque (y por consiguiente de un ecoparte también) es 5
 - La **satisfacción** de un ecoparque es el doble de lo que daría un parque común con el mismo nivel de diversión
 
## Requerimiento

Calcular la satisfacción de cada variedad de entretenimiento

## Casos de ejemplos
Tener en cuenta los siguientes valores de diversión para los entretenimientos:
- Zoológico y Parque domínico: 15 
- Les luthier y Independiente-Juventus: 10

Entonces
- La satisfacción del parque domínico para Marie es 10
- La satisfacción del zoológico para Marie es 20
- La satisfacción del les luthier para Marie es 8.99
- La satisfacción de independiente-juventus para Marie es 8.999






