# Capítulo 1: Introducción a la teleinformática e Internet (TP 1)

## 1.1 Teleinformática, redes, OSI e Internet ★★☆☆☆ (2 de 8)

Temas en Lumen: `u1-informatica-telecomunicaciones-teleinformatica`, `u1-transmision-datos-definicion-concepto`, `u1-circuito-teleinformatico-sobre-redes`, `u1-enlace-circuito-datos`, `u1-internet-historia-equipos-organizacion`, `u3-protocolos-arquitecturas-comunicaciones`, `u3-tipos-enlaces-topologias-red`

Es teoría para desarrollar. Apareció en los dos parciales más recientes: las capas del OSI y la capa 2 (2022), y las técnicas de conmutación (2024).

### 1. Conceptos

**Teleinformática.** Es la unión de las telecomunicaciones y la informática. Estudia cómo transmitir información (voz, datos y video) entre equipos distantes a través de redes. El problema que resuelve: que una computadora pueda dialogar con equipos lejanos como si estuvieran conectados localmente. Para comunicar hacen falta, por lo menos, un emisor, un receptor y un medio.

**Transmisión de datos.** Es la transferencia de información codificada desde un punto a otro, o a varios, mediante señales eléctricas, ópticas, electroópticas o electromagnéticas.

**Circuito teleinformático básico.** Es lo que une un equipo fuente con un equipo colector:
```
 ┌─────┐       ┌─────┐                     ┌─────┐       ┌─────┐
 │ ETD │──ID───│ ECD │═══ línea de com. ═══│ ECD │───ID──│ ETD │
 └─────┘       └─────┘                     └─────┘       └─────┘
 fuente        └────────── circuito de datos ─────────┘  colector
 └───────────────────────── enlace de datos ─────────────────────┘
```
- **ETD** (equipo terminal de datos; en inglés, DTE): genera o recibe los datos. Por ejemplo, una computadora.
- **ECD** (equipo de comunicación de datos; en inglés, DCE): adapta la señal al medio. Por ejemplo, un módem.
- **ID** (interfaz digital): la conexión entre el ETD y el ECD. Por ejemplo, la RS-232 (bloque 3.2).
- **Circuito de datos:** los ECD y la línea. Su misión es entregarle al ETD colector las señales con la misma forma e información que mandó el ETD fuente.
- **Enlace de datos:** todo el camino, de ETD a ETD.

**Qué ECD va según la señal y el canal.**
- Señal digital y canal analógico: un módem, que modula.
- Señal digital y canal digital: un módem banda base, que no modula y solo codifica (bloque 4.1).
- Señal analógica (voz) y canal digital: un codec, que digitaliza con muestreo, cuantificación y codificación.
- Señal analógica y canal analógico: va directo.

**Red.** Es el conjunto de recursos de comunicaciones e informática que forman un sistema para transmitir información entre usuarios distantes. Se clasifican:
- **Por extensión:** **LAN** (un edificio o edificios cercanos, alta velocidad, propia de la organización), **MAN** (un área metropolitana) y **WAN** (un área geográfica grande, que usa al menos en parte circuitos de un proveedor de telecomunicaciones).
- **Por topología:** bus, anillo, estrella (como una central telefónica) y malla (todos con todos).

**Técnicas de conmutación** (clase de teoría 1). Es la pregunta de teoría 1 del parcial 2024. Conmutar es establecer, cada vez que hace falta, el camino entre dos equipos de la red a través de nodos (centrales telefónicas, routers, switches). Hay tres técnicas básicas:
1. **De circuitos:** los conmutadores establecen un camino físico para cada comunicación, y los recursos quedan reservados todo el tiempo que dura, se usen o no. Tiene tres fases: establecimiento, transferencia y desconexión. Los extremos se llaman llamante y llamado. Ejemplo: la red telefónica.
2. **De mensajes:** cada mensaje completo lleva la dirección de origen y de destino. Los nodos lo **almacenan y retransmiten**: lo guardan en una cola y lo reenvían en el momento más oportuno, decidiendo el camino. No hay camino reservado.
3. **De paquetes:** el transmisor divide el mensaje en paquetes chicos, y a cada uno le agrega la información para encaminarlo y para rearmar el mensaje en el destino. Solo funciona con señales digitales. Tiene dos modos:
   - **Datagrama:** cada paquete viaja por su cuenta y los nodos deciden la ruta de cada uno, como en la conmutación de mensajes. No orientado a la conexión.
   - **Circuito virtual:** primero se establece una ruta lógica y todos los paquetes la siguen, en orden. Orientado a la conexión.

**Internet.** Es una red internacional formada por muchas redes independientes, operadas en forma autónoma e interconectadas con protocolos normalizados (TCP/IP), que permiten la comunicación entre dos equipos (host a host). Sus componentes son los **routers**, que encaminan los paquetes entre redes; los **nodos** o hosts, que son los equipos con dirección IP; y los **enlaces**. Su topología es una **malla irregular**. Historia (clase de teoría 1):
```
1969  se crea ARPANET, con fines de defensa y académicos; usa conmutación de paquetes
1974  aparecen los protocolos TCP/IP
1984  se divide en dos: la académica (sigue como ARPANET) y la militar (MILNET)
1995  pasa a llamarse Internet
```
(Material propio: los estándares salen de la IETF como documentos RFC, la IANA/ICANN asigna direcciones y dominios, y en Latinoamérica las direcciones IP las administra LACNIC).

**Modelo OSI.** Es una norma de ISO para comunicar sistemas abiertos y heterogéneos (equipos de distintos fabricantes). Divide la comunicación en 7 capas. Cada capa usa los servicios de la de abajo y le da servicios a la de arriba:
```
7  Aplicación     servicios para el usuario y las aplicaciones
6  Presentación   formato de los datos: compresión, cifrado
5  Sesión         manejo del diálogo entre los extremos
4  Transporte     integridad de extremo a extremo; segmenta y rearma (TCP, UDP)
3  Red            enrutamiento entre redes; direcciones (IP)
2  Enlace         tramas; detección y control de errores entre nodos vecinos (HDLC)
1  Física         transmite los bits por el medio: tensiones, conectores (RS-232)
```
- **Protocolo:** reglas para comunicarse entre capas **iguales** de los dos extremos.
- **Interfaz:** conexión entre capas **contiguas** del mismo equipo.
- **Encapsulado:** cada capa le agrega su cabecera a lo que le pasa la de arriba. La capa 2 agrega cabecera y cola, y eso es la **trama**. En el destino, cada capa saca la suya. Salvo la física, ninguna capa se comunica directo con su par.

**La capa 2 (enlace), en detalle** (clase de teoría 1). Es la pregunta 1 del parcial 2022.
- **Servicio** que le da a la capa 3: establecer, mantener y liberar las conexiones de la capa de red, con control de errores y de flujo.
- **Funciones:**
  - Delimitar la secuencia de bits en **tramas**, asegurando la transparencia (que los datos puedan tener cualquier combinación de bits sin confundirse con los delimitadores).
  - Resolver los problemas de tramas **dañadas, perdidas y duplicadas**: detecta y corrige los errores (capítulo 6).
  - Permitir la transferencia **ordenada** de las tramas y controlar el **flujo** de información.
  - Llevar la **dirección de destino**.
- **Ejemplo:** el protocolo HDLC. La capa de enlace y la física son las mínimas necesarias para transferir datos.

**Los tipos de pregunta que toman:** enunciar y explicar (capas del OSI, funciones de una capa, técnicas de conmutación), definir (teleinformática, Internet, protocolo) y graficar (circuito teleinformático).

### 2. Ejemplo resuelto (1er parcial 2022, Ej 1)

> Enuncie las capas del Modelo OSI y enumere el servicio y las funciones de la capa dos. (Desarrollar la respuesta en no menos de 15 renglones).

Pide dos cosas: las siete capas, con una línea cada una, y el detalle de la capa 2. Conviene arrancar con qué es el OSI, para ubicar.

```
Paso 1: qué es el modelo OSI
  "Es una norma de ISO para comunicar sistemas abiertos de distintos fabricantes.
   Divide la comunicación en 7 capas: cada una usa los servicios de la de abajo y le
   da servicios a la de arriba, y se comunica con su par del otro extremo mediante
   un protocolo."

Paso 2: las siete capas, de abajo hacia arriba
  1 Física: transmite los bits por el medio (niveles de tensión, conectores; RS-232).
  2 Enlace: arma las tramas y controla errores y flujo entre nodos vecinos (HDLC).
  3 Red: encamina los paquetes entre redes, con direcciones (IP).
  4 Transporte: integridad de extremo a extremo; segmenta y rearma (TCP, UDP).
  5 Sesión: organiza el diálogo entre los extremos.
  6 Presentación: formato de los datos (compresión, cifrado).
  7 Aplicación: servicios para el usuario y las aplicaciones.

Paso 3: servicio de la capa 2
  "Le da a la capa de red el establecimiento, mantenimiento y liberación de las
   conexiones, con control de errores y de flujo."

Paso 4: funciones de la capa 2
  - Delimita la secuencia de bits en tramas (cabecera y cola), con transparencia.
  - Detecta y corrige errores: resuelve tramas dañadas, perdidas y duplicadas.
  - Entrega las tramas en orden y controla el flujo.
  - Lleva la dirección de destino.
  Ejemplo: HDLC. Con la capa física, es lo mínimo para transferir datos.

Control: ¿están las 7 capas, el servicio y al menos 3 funciones? ✓
```

### 3. Ejercicio guiado (1er parcial 08/10/2024, Teoría 1)

> Dentro de las funciones ejecutadas por las redes está la conmutación. ¿Cuáles son las técnicas básicas de conmutación que conoce? Explique cada una.

Armalo como el ejemplo: una frase que defina, las técnicas con su explicación y un cierre que compare.

```
Paso 1: qué es conmutar
  → ________

Paso 2: conmutación de circuitos (camino, recursos, fases)
  → ________

Paso 3: conmutación de mensajes (almacenar y retransmitir)
  → ________

Paso 4: conmutación de paquetes y sus dos modos
  → ________

Paso 5: cierre comparando
  → ________
```

### 4. Práctica

Preguntas reales de la guía del TP 1 y de la teoría. Intentá responder cada una en dos o tres líneas antes de mirar las respuestas.

1. Indicar qué disciplinas abarca la teleinformática. (TP 1)
2. Indicar cuáles son las redes que dieron origen a Internet. (TP 1)
3. ¿Qué equipos principales integran la red Internet y cuál es su topología? (TP 1)
4. Dibujá el circuito teleinformático básico y marcá el circuito de datos y el enlace de datos.
5. ¿Qué diferencia hay entre un protocolo y una interfaz en el modelo OSI?
6. ¿Qué ECD usarías para mandar datos digitales por un canal analógico? ¿Y voz por un canal digital?
7. Enumere las capas del modelo OSI. ¿En qué capa se realiza la encriptación? (2do parcial 2022, Ej 5)

### 5. Cierre

**Fórmulas** (para memorizar)
```
OSI (de abajo hacia arriba): Física, Enlace, Red, Transporte, Sesión, Presentación, Aplicación
Capa 2: servicio = establecer, mantener y liberar conexiones de la capa 3, con control de
        errores y flujo; funciones = tramas con transparencia, errores (daño, pérdida,
        duplicado), orden y flujo, dirección de destino; ejemplo HDLC
Conmutación: de circuitos (camino reservado; 3 fases), de mensajes (almacenar y
             retransmitir), de paquetes (datagrama o circuito virtual)
ETD ─ID─ ECD ═ línea ═ ECD ─ID─ ETD;  circuito de datos = ECD + línea;  enlace = ETD a ETD
Internet: ARPANET 1969, TCP/IP 1974, MILNET 1984; routers, hosts y enlaces; malla irregular
```

**Trampas**
- **Desordenar las capas del OSI.** Una regla para acordarse, de abajo hacia arriba: "Física, Enlace, Red, Transporte" son las de la red; "Sesión, Presentación, Aplicación" son las del usuario.
- **Confundir circuito de datos con enlace de datos.** El circuito son los ECD y la línea; el enlace va de ETD a ETD.
- **Confundir protocolo con interfaz.** El protocolo es entre capas iguales de los dos extremos; la interfaz, entre capas vecinas del mismo equipo.
- **Decir que en la conmutación de paquetes hay un camino reservado.** Eso es la de circuitos; en el circuito virtual hay una ruta lógica, pero no recursos reservados.
- **Responder corto.** El parcial 2022 pedía no menos de 15 renglones por respuesta.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Qué diferencia hay entre la conmutación de circuitos y la de paquetes?
2. (Pregunta) Nombrá las 7 capas del OSI en orden y dos funciones de la capa 2.

## Respuestas del capítulo 1

### 1.1 Ejercicio guiado

```
Paso 1: qué es conmutar
  "Es establecer, cada vez que hace falta, el camino entre dos equipos de la red a
   través de los nodos (centrales, routers, switches). Hay tres técnicas básicas."

Paso 2: de circuitos
  Los conmutadores establecen un camino físico para cada comunicación, y sus recursos
  quedan reservados mientras dura, se usen o no. Tres fases: establecimiento,
  transferencia y desconexión. Ejemplo: la red telefónica.

Paso 3: de mensajes
  Cada mensaje completo lleva origen y destino. Los nodos lo almacenan en una cola y
  lo retransmiten en el momento oportuno, eligiendo el camino. No se reserva nada.

Paso 4: de paquetes
  El mensaje se divide en paquetes, cada uno con la información para encaminarlo y
  rearmar el mensaje en el destino. Solo con señales digitales. Dos modos:
  datagrama (cada paquete por su cuenta, sin conexión) y circuito virtual (se
  establece una ruta lógica y todos los paquetes la siguen, en orden).

Paso 5: cierre
  "La de circuitos garantiza el camino pero desperdicia recursos cuando no se habla;
   la de mensajes y la de paquetes comparten los enlaces entre muchos usuarios, y la
   de paquetes, con mensajes chicos, reduce las demoras en los nodos."
```

### 1.1 Práctica

```
1. Las telecomunicaciones y la informática: la transmisión de información (voz,
   datos, video) entre equipos distantes a través de redes.
2. ARPANET (de DARPA, la agencia de defensa de EE.UU.) y MILNET, su parte militar,
   que se separó en 1984.
3. Routers (encaminan paquetes entre redes), nodos o hosts (equipos con IP) y
   enlaces. Topología: malla irregular.
4. ETD ─ID─ ECD ═ línea ═ ECD ─ID─ ETD. Circuito de datos: los dos ECD y la línea.
   Enlace de datos: todo, de ETD a ETD.
5. El protocolo son las reglas entre capas iguales de los dos extremos; la interfaz
   es la conexión entre capas contiguas del mismo equipo.
6. Datos digitales por canal analógico: un módem, que modula. Voz por canal
   digital: un codec, que muestrea, cuantifica y codifica.
7. Física, Enlace, Red, Transporte, Sesión, Presentación y Aplicación. La
   encriptación (cifrado) se hace en la capa 6, Presentación, que se ocupa del
   formato de los datos: compresión y cifrado.
```

### 1.1 Autoevaluación

```
1. En la de circuitos se reserva un camino físico con todos sus recursos durante
   toda la comunicación (establecimiento, transferencia, desconexión). En la de
   paquetes el mensaje se divide en paquetes que comparten los enlaces con otros
   usuarios; los nodos los encaminan (datagrama) o siguen una ruta lógica
   (circuito virtual), sin reservar recursos.

2. Física, Enlace, Red, Transporte, Sesión, Presentación, Aplicación.
   Capa 2: arma las tramas con transparencia; detecta y corrige errores (tramas
   dañadas, perdidas o duplicadas); entrega en orden y controla el flujo; lleva la
   dirección de destino.
```
