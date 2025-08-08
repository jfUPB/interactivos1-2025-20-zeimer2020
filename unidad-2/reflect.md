# Unidad 2


## 🤔 Fase: Reflect


### Actividad 6

#### Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?
Maquina de estados: Forma de controlar un sistema segun el paso en que esta y lo que sucede.
4 partes: Pasos, eventos, cambios, acciones.

#### Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?
Utilidad: Permite manejar varias tareas sin detener el programa; evita que sleep () bloquee respuestas.

#### Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?
Nueva funcion (shake): Agregar que si se agita durante la cuenta el tiempo se reduzca a la mitad.

#### Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.
el vector de prueba: Lista de entradas y salidas esperadas para confirmar que funciona bien.

#### ¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?
Fue mas dificil hacer el fregado diagrama, odio hacer cosas asi


#### Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?
Un bug hacia que no cambiara de estado; pensar en estados y eventos me mostro donde la transicion fallaba.

#### El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?
Empece con una version basica y fui agregando funciones paso a paso.

#### Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?
Lo usaria en un juego interactivo con varios niveles y eventos.

### Actividad 7

La actividad de mi compañero estaba muy completa

### Actividad 8


siendo honesto y yendome a terminos generales esta fue hasta ahora la mejor unidad pq pude entender muy bien como funcionaba el tema de los estados y los intervalos, eso si odio los diagramas




