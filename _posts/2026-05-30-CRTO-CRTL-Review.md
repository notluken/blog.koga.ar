---
layout: post
title: "CRTO y CRTL: mi experiencia con las certificaciones de Zero-Point Security"
date: 2026-05-30
categories: [red-team, certificaciones]
tags: [crto, crtl, zero-point-security, cobalt-strike, red-team, active-directory]
image:
  path: /assets/banner_crtl_crto.png
  alt: "Cobalt Strike"
author: luken
---

Hoy quiero contarles mi experiencia con las dos certificaciones que ofrece Zero-Point Security, el **Certified Red Team Operator** (CRTO) y **Certified Red Team Leader** (CRTL).

 Si bien yo ya llevo un tiempo en el ambito profesional, casi 3 anios de experiencia como Analista e Ingeniero en Ciberseguridad, estas certificaciones complementan muy bien los conocimientos que aprendi en el Certified Pentetration Tester Specialist (CPTS) de HackTheBox, a esta ultima la aprobe hace un anio exacto, 3 de Mayo del 2025.

Inicialmente, compre el CRTL primero, para poder estudiar todo lo que era evasion de EDR. Ese fue mi gran error. 

---

## ¿Qué son el CRTO y el CRTL?

Las certificaciones que ofrece ZPS son dedicadas especialmente para "Operators" en engagements de Red Teaming, porque usamos una herramienta muy conocida que es Cobalt Strike. Un Command-and-Control (C2) muy conocido de codigo cerrado que ofrece en mi opinion, las mejores prestaciones para un red teamer. 

Como conte un poco mas arriba, mi error fue ir directo al CRTL, el cual, si bien al principio lo entendi, me faltaban todas las bases de Cobalt Strike. Como jamas habia usado un C2 (todo muy de manual, proxychains, socat, multiples ventanas de la kitty, gracias s4vitar) se me hacia un poco complicado entender los conceptos que el CRTL ya daba por hecho que tenias que saber. Por eso al inicio me costo mucho empezar, mas que nada tambien porque estaba recien empezando en el mundo del malware development. Eso, mas el trabajo, mas que KOGA empezo a funcionar, se me complicaba demasiado.

Asi que tome una decision: Comprar el CRTO. Y fue la mejor decision!

Entonces, que son las certificaciones? 

El CRTO, o Certified Red Team Operator, es el primer nivel de certificación de Zero-Point Security. Está pensado para quien quiere aprender a operar en un engagement de Red Team real usando Cobalt Strike como C2 principal. El curso cubre todo el ciclo de ataque: desde el acceso inicial hasta la dominancia de dominio, pasando por movimiento lateral, escalada de privilegios, Kerberos, pivoting y OPSEC básico. No es un curso de "cómo hackear cajas", es un curso de cómo operar en un entorno de Active Directory real de forma coordinada y silenciosa. Es el curso que te enseña a pensar como operador antes de enseñarte las técnicas.


El CRTL, o Certified Red Team Lead, es el segundo nivel y donde las cosas se ponen realmente interesantes. Si el CRTO te enseña a usar las herramientas, el CRTL te enseña a entender por qué funcionan, y más importante, por qué te detectan. El foco está en evasión de EDR moderna: cómo se construye un loader desde cero, qué es el código PIC y por qué importa, cómo funciona el sleep masking, el call stack spoofing, la evasión en load time, runtime y post-exploitation. El examen te pone frente a un entorno con Elastic Defend activo y te mide en cada categoría de detección por separado. No hay margen para el cargo culto: o entendés lo que estás haciendo, o el EDR te ve.


---

## El curso: Red Team Ops I y II

### Contenido y estructura
Ambos cursos están organizados en módulos que siguen el ciclo de ataque de forma lineal, desde el acceso inicial hasta la dominancia de dominio en el CRTO, y desde la infraestructura C2 hasta la evasión avanzada de EDR en el CRTL. Lo que más me gustó es que van siempre al punto. No hay relleno teórico por el gusto de tenerlo: cada concepto aparece en el momento en que lo necesitás para avanzar.
Del CRTO, los módulos que más me marcaron fueron los de Active Directory: constrained delegation, unconstrained delegation y RBCD. Por primera vez entendí realmente cómo funciona la cadena de confianza de Kerberos y cómo se abusa de ella de forma quirúrgica. También los Malware Essentials, que fueron mi primer contacto real con cómo se construye y ejecuta código malicioso de forma controlada.
Del CRTL, todo el bloque de evasión es otro nivel. Load-time, runtime y post-exploitation evasion están explicados de forma que te obligan a entender qué está pasando en memoria, en el call stack, en el EDR, antes de poder aplicar cualquier técnica. Y el módulo de drivers vulnerables fue una sorpresa: no esperaba que un curso de red team entrara tan profundo en ese territorio, y fue uno de los más enriquecedores de todo el camino.

### Lab environment
Es la primera vez que emulo TTPs en un entorno diseñado para eso, y lo que más me sorprendió fue cuánto se parece a entornos reales. No es un CTF. No hay flags escondidas en lugares artificiales ni caminos forzados. Es un dominio Windows con múltiples máquinas, servicios reales, configuraciones reales, y problemas reales. Mientras hacía los labs del CRTL pensaba en entornos de clientes que vi con KOGA, y la similitud era incómoda en el buen sentido.
El acceso es vía Snap Labs, comprás horas de lab y las usás cuando querés. El de RTO I tiene un dominio single-forest con workstations, servidores y un DC. El de RTO II agrega SQL servers, ADCS, Credential Guard activo y múltiples segmentos de red con restricciones de egress. No es un laboratorio que te sostiene la mano: si algo no funciona, tenés que entender por qué.

### Cobalt Strike como herramienta central
Antes de estos cursos había probado Havoc en algunos labs de Vulnlab y tocado Covenant por curiosidad, pero ninguno me convencía ni los entendía realmente. No tenía base de C2 real. Ese fue parte del problema cuando intenté empezar directo por el CRTL: el curso asume que sabés operar en CS, y yo no sabía ni para qué servía un listener SMB.
El CRTO te construye esa base desde cero. Te enseña a pensar en términos de beacons, listeners, pivoting por SMB, aggressor scripts y BOFs antes de que tengas que preocuparte por evasión. Para cuando llegás al CRTL ya tenés el modelo mental correcto y podés enfocarte en lo que importa: entender por qué CS hace lo que hace en memoria, cómo interactúa con el EDR, y cómo modificar ese comportamiento.
Los Malleable C2 profiles, el uso de BOFs en lugar de fork-and-run para reducir telemetría, la diferencia entre ejecutar desde el beacon versus spawnear un proceso hijo, todo eso el curso lo cubre con profundidad real. No como una lista de comandos, sino explicando el impacto de cada decisión en lo que ve el EDR.
    
---


## El examen CRTO
El formato del examen es diferente a lo que probablemente estás acostumbrado. No hay flags. No hay lista de objetivos con puntos. El objetivo es uno solo: comprometer un servidor específico dentro del entorno y dejar un archivo rto.txt como prueba. El examen te gradúa automáticamente cuando lo detecta. El primer intento tiene 48 horas de tiempo, los siguientes 24, pero podés pausar el lab y retomarlo dentro de una ventana de 7 días. Y los intentos son ilimitados.
Ese último punto es importante porque cambia completamente la relación con el examen. No hay presión de "si fallo, perdí todo". Hay presión de entender.

### Mi experiencia
Me llevó tres intentos. No voy a mentir con eso.
Lo que me trabó no fue una técnica específica que no supiera ejecutar. Fue la orientación. Saber qué camino tomar en un entorno que no conocés, con múltiples máquinas y vectores posibles, es una habilidad distinta a saber cómo funciona Kerberos. El curso te prepara bien, pero la diferencia entre leer sobre constrained delegation y tener que decidir en el examen si ese es el camino correcto en ese momento es considerable.
Entrás al examen con acceso a una máquina foothold ya comprometida donde implantás tu beacon. Desde ahí, a moverse.
### Nivel de dificultad

No es comparable directamente con el CPTS de HackTheBox, aunque tengo los dos. Son disciplinas distintas. El CPTS te da una IP y tenés que llegar a Domain Admin desde cero, con enumeración incluida. El CRTO asume que ya estás dentro y te pone a operar. Es más estrecho en scope y más profundo en lo que evalúa dentro de ese scope. Si venís del mundo del pentesting tradicional, el salto mental es real.

--- 

## El examen CRTL
El formato es el mismo que el CRTO, con la misma lógica de intentos ilimitados y el objetivo de escribir rto2.txt en un servidor específico. La diferencia no está en el formato sino en lo que el examen mide. El CRTL tiene una capa adicional: el entorno tiene un EDR activo, y al final del examen se evalúa automáticamente cuántas categorías de detección pudiste evitar. Pasás por el objetivo operacional y por la evasión al mismo tiempo.

### Mi experiencia
Me llevó dos intentos. Lo que cambió entre el primero y el segundo fue cómo configuraba y validaba la evasión antes de operar, pero eso lo voy a documentar en detalle en un cheatsheet separado para no dar spoilers del examen.
Lo que sí puedo decir es que en el CRTL me pasé más tiempo configurando la evasión, probando el payload contra el EDR y ajustando la configuración que ejecutando el path de ataque en sí. El objetivo operacional, una vez que tenés el beacon limpio, fluye. La parte difícil es llegar a tener ese beacon limpio. Y eso, en retrospectiva, es exactamente lo que el curso quiere que entiendas.

### Nivel de dificultad
El material te prepara bien para el path de ataque. Para la parte de evasión, el material también está, pero la brecha entre entender los conceptos y aplicarlos correctamente bajo presión es donde está el verdadero examen. Terminé el CRTL sabiendo exactamente qué había fallado y por qué, que es probablemente la mejor señal de que el examen está bien diseñado.

---


Perfecto. Acá van los dos bloques:

---

## Lo que más me gustó

**El material.** Los cursos de ZPS están escritos con una claridad que no es común en este campo. Cada concepto aparece cuando lo necesitás, explicado de forma que podés entender el por qué antes de ver el cómo. No es un dump de comandos con capturas de pantalla. Es material que se nota que fue escrito por alguien que entiende profundamente lo que está enseñando.

**Los labs.** Ya lo dije antes, pero vale repetirlo: nunca sentí que estaba en un CTF. Los entornos se parecen a lo que uno ve en clientes reales. Eso tiene un valor que no se puede fabricar artificialmente.

**El modelo de examen.** Intentos ilimitados con tiempo pausable es una decisión que cambia completamente la experiencia. Te saca la presión artificial y te deja enfocarte en aprender de los errores. Fallé, entendí por qué, volví. Eso es exactamente lo que debería ser un examen técnico.

**El precio.** Comparado con lo que ofrece el mercado, ZPS es difícil de justificar no comprar. Otras certificaciones cobran el doble o el triple por menos profundidad técnica y sin Cobalt Strike incluido. Acá el precio del lab incluye acceso a CS, que por sí solo cuesta cientos de dólares por mes. Es una de las pocas certs donde la relación precio/valor es genuinamente difícil de cuestionar.

**La comunidad.** El Discord de ZPS es uno de los mejores recursos del curso. Hay gente en todos los niveles, las preguntas se responden rápido, y el nivel de la comunidad es alto. Nunca me sentí solo en un punto difícil.

**El curso no te da todo masticado.** Esto podría sonar a crítica, pero es lo opuesto. Hay momentos donde el material te da el concepto y el entorno, y tenés que encontrar el camino vos. Eso es lo que hace que lo que aprendés se quede. Las cosas que más me costó conseguir son las que mejor recuerdo.

---

## ¿Vale la pena?

100% recomendado. Para saltar de Pentesting a Red Teaming, para mi es una de las mejores opciones.


---

## Recursos que usé

* https://racoten.github.io/Self-Taught-Course/Project/CrystalLoaders/CrystalLoaders_index.html 
* https://0xdbgman.github.io/posts/edr-internals-research-and-bypass/
* https://0xdbgman.github.io/posts/shellcode-loaders-the-art-of-execution/
* https://0xdbgman.github.io/posts/sec-controls-the-art-of-breaking-through/




