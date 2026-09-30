# Capítulo 8: Cableado estructurado (TP 8)

## 8.1 Estructura y diseño (EIA/TIA 568) ☆☆☆☆☆ (0 de 4)

Temas en Lumen: `u7-par-trenzado-cableado-estructurado`

No apareció en los 2dos parciales relevados, pero en 2026 es el TP 8 (el trabajo de diseño de una red de cableado) y la teoría se da antes del 2do parcial, así que puede aparecer como pregunta.

### 1. Conceptos

**Cableado estructurado.** Es el sistema de cableado de telecomunicaciones de un edificio, pensado para ser **general**: soporta voz, datos y video de distintos fabricantes sin tener que modificarlo. Antes había redes separadas para cada servicio; ahora convergen en una sola. Lo normalizan la **EIA/TIA 568** (asociaciones de industrias de electrónica y de telecomunicaciones de EE.UU.) y, para los recorridos y espacios, la EIA/TIA 569.

**Los subsistemas.**
```
  Puesto de trabajo ── cableado horizontal ── IDF (armario de piso)
                                                │
                                        cableado vertical (backbone)
                                                │
                    instalaciones de entrada ── MDF (sala de equipos) ── campus
```
- **Puesto de trabajo:** donde el usuario conecta sus equipos. Lleva **dos bocas** de telecomunicaciones (jacks RJ-45) y cuatro tomas eléctricas con tierra independiente. El tendido eléctrico va separado del de datos.
- **Cableado horizontal:** del puesto de trabajo al armario de piso. Se recomienda UTP (Cat 5e o superior). Va por bandejas, piso técnico, cablecanal o cielorraso.
- **IDF** (intermediate distribution frame), gabinete o armario de telecomunicaciones: donde el cableado horizontal se conecta con los equipos, con patch panels y patch cords.
- **Cableado vertical o troncal (backbone):** une los armarios de piso con la sala de equipos, en estrella. Se recomienda **fibra óptica multimodo** para datos y cables multipares para telefonía.
- **MDF** (main distribution frame) o sala de equipos: el corazón de la red, con routers, switches, servidores, la central telefónica y la UPS. Solo admite equipos de telecomunicaciones, y se diseña pensando en el crecimiento.
- **Instalaciones de entrada:** donde entran los servicios externos (proveedor de Internet, telefonía).
- **Campus:** el cableado entre edificios.
- **Documentación:** planos con la ubicación de bocas, bandejas, ductos y armarios; el sistema de rótulos; el detalle de las terminaciones y de los hilos de fibra; los tableros eléctricos y las bajadas a tierra.

**Distancias máximas.**
```
Canal horizontal completo:        100 m = 90 m de cable fijo + 10 m de patch cords
                                  (según la clase: 3 m del lado del usuario y 7 m en el armario)
Vertical con UTP:                 100 m
Vertical con fibra MM 62,5/125:   2.000 m
```
En el cableado horizontal **no se permiten empalmes, derivaciones ni puentes**: cada boca tiene su cable entero hasta el armario. Hay que alejarlo de fuentes de interferencia (motores, ascensores, transformadores).

**Data center.** La norma TIA 942 define las salas de servidores, de comunicaciones y de energía, con niveles (Tier) de confiabilidad.

**El trabajo de diseño (TP 8).** Se diseña el cableado de un edificio con los planos que da el docente: fibra multimodo de 8 hilos en el vertical y UTP Cat 6 en el horizontal, sin equipos activos. Los entregables son los planos (sala de equipos, armarios, montantes, puestos de trabajo, tableros), la memoria descriptiva de los materiales, el cómputo de materiales, los costos de materiales, mano de obra y certificación, y el **costo por boca**.

**Cómputo del cable horizontal** (material propio, con reglas usuales de diseño). Como no se puede empalmar, cada cable sale entero de una caja:
```
Longitud promedio = (tramo más corto + tramo más largo) / 2 × 1,10     (10 % de holgura)
Cables por caja   = 305 m / longitud promedio   (redondeando para abajo: los sobrantes no se empalman)
Cajas             = bocas / cables por caja     (redondeando para arriba)
Chequeo: tramo más largo × 1,10 ≤ 90 m. Si no, hace falta otro armario de piso.
```

**Los tipos de pregunta que toman:** los subsistemas y qué va en cada uno, las distancias máximas y qué medio va en cada tramo. En el TP: el cómputo de materiales y el costo por boca.

### 2. Ejemplo resuelto (material propio, estilo del TP 8)

> Un piso tiene 20 puestos de trabajo con 2 bocas cada uno. El puesto más cercano al armario está a 10 m de cable y el más lejano a 60 m. El UTP viene en cajas de 305 m. Calcular las bocas, la longitud promedio, las cajas de cable y los patch panels de 24 puertos que hacen falta, y verificar la distancia máxima.

Se cuentan las bocas, se saca la longitud promedio con la holgura y se ve cuántos cables enteros salen de cada caja.

```
Paso 1: bocas
  20 puestos × 2 = 40 bocas

Paso 2: longitud promedio con 10 % de holgura
  (10 + 60) / 2 × 1,10 = 35 × 1,10 = 38,5 m

Paso 3: cables por caja (enteros)
  305 / 38,5 = 7,9  →  7 cables por caja

Paso 4: cajas
  40 / 7 = 5,7  →  6 cajas  (6 × 305 = 1.830 m)

Paso 5: patch panels de 24 puertos
  40 / 24 = 1,7  →  2 patch panels

Paso 6: distancia máxima
  60 × 1,10 = 66 m ≤ 90 m ✓

Control: 40 cables × 38,5 m = 1.540 m ≤ 1.830 m comprados ✓
```

### 3. Ejercicio guiado (material propio, estilo del TP 8)

> Un piso tiene 16 puestos con 2 bocas cada uno. El tramo más corto mide 8 m y el más largo 72 m. Con cajas de 305 m y patch panels de 24 puertos, calcular lo mismo que en el ejemplo.

```
Paso 1: bocas
  → ________

Paso 2: longitud promedio con holgura
  → ________

Paso 3: cables por caja
  → ________

Paso 4: cajas
  → ________

Paso 5: patch panels
  → ________

Paso 6: distancia máxima
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: armario lejano (material propio)

> En otro piso, el puesto más lejano queda a 85 m de cable del armario. ¿Cumple la norma? Si no, ¿qué se hace?

#### Ejercicio extra 2: teoría (material propio sobre la clase)

> Describir los subsistemas del cableado estructurado según la EIA/TIA 568 y qué medio se recomienda en cada uno.

#### Ejercicio extra 3: teoría (material propio sobre la clase)

> ¿Cuál es la longitud máxima del canal horizontal y cómo se reparte? ¿Por qué no se permiten empalmes en el cableado horizontal?

### 5. Cierre

**Fórmulas** (para memorizar)
```
Puesto de trabajo → horizontal (UTP, ≤ 90 m) → IDF → vertical (fibra MM) → MDF → entrada
Canal horizontal: 100 m = 90 m fijos + 10 m de patch cords.  Vertical: UTP 100 m, fibra MM 2.000 m
Puesto: 2 bocas RJ-45 + 4 tomas eléctricas.   Sin empalmes en el horizontal
Longitud promedio = (mín + máx) / 2 × 1,10;  cables por caja = 305 / promedio (para abajo)
Normas: EIA/TIA 568 (cableado), 569 (recorridos), TIA 942 (data center)
```

**Trampas**
- **Redondear para arriba los cables por caja.** Un cable no se puede empalmar: lo que sobra de la caja no sirve.
- **Tomar 100 m para el cable fijo.** Son 90 m; los otros 10 m son patch cords.
- **Poner UTP en un vertical largo.** El vertical entre pisos lejanos va en fibra multimodo.
- **Olvidar la holgura** en el cómputo.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Qué diferencia hay entre el IDF y el MDF? ¿Qué los une?
2. (Ejercicio) 30 bocas, tramo más corto 20 m y más largo 50 m, cajas de 305 m. ¿Cuántas cajas hacen falta? (material propio)

## 8.2 Armado y certificación ☆☆☆☆☆ (0 de 4)

Temas en Lumen: `u7-par-trenzado-cableado-estructurado`

Tampoco apareció en los 2dos parciales relevados. Es la parte práctica del TP: armar los cables y certificar la instalación.

### 1. Conceptos

**Conector RJ-45 y las normas T568A y T568B.** El UTP de 4 pares se termina en un conector RJ-45 de 8 pines. Hay dos órdenes de colores normalizados (TIA/EIA 568):
```
Pin      1          2        3          4      5          6        7          8
T568A    bl-verde   verde    bl-naranja azul   bl-azul    naranja  bl-marrón  marrón
T568B    bl-naranja naranja  bl-verde   azul   bl-azul    verde    bl-marrón  marrón
```
(bl = blanco con el color). La diferencia entre las dos es que se intercambian los pares naranja y verde. Al armar, se quitan unos 2 cm de vaina y se destrenzan los hilos lo mínimo posible, nunca más de 13 mm.

**Cable directo y cable cruzado.**
- **Directo** (straight-through): la misma norma en los dos extremos. Une equipos **distintos**: switch con PC o servidor, hub con PC, router con switch o hub.
- **Cruzado** (crossover): T568A en un extremo y T568B en el otro. Une equipos **iguales**: switch con switch, hub con hub, router con router, PC con PC, y también router con PC.

**Certificación.** Se mide cada enlace con un equipo certificador para comprobar que cumple su categoría. Los parámetros:
- **Mapa de cableado:** que cada pin llegue al pin correcto. Fallas: pares invertidos (los dos hilos de un par intercambiados), pares cruzados (un par llega a los pines de otro), **pares divididos** (hilos de dos pares mezclados: hay continuidad, pero se pierde el trenzado y sube la diafonía), cortos y abiertos.
- **Resistencia** de cada par, en corriente continua.
- **Longitud** y **retardo de propagación** (en ns), y la **diferencia de retardo** entre pares (delay skew).
- **Impedancia característica:** si se refleja el 15 % o más de la señal de prueba, hay una anomalía.
- **Atenuación** (dB): la pérdida a lo largo del cable. Cuanto menos, mejor; depende de la construcción, la longitud y la frecuencia.
- **NEXT** (dB): diafonía en el extremo cercano, entre cada par de pares (6 combinaciones). Se mide en los dos extremos. Cuanto más alto, mejor: indica la calidad de los componentes y de la instalación.
- **FEXT**: diafonía en el extremo lejano. **PSNEXT**: la suma de la diafonía que recibe un par de los otros tres.
- **ACR** (relación atenuación-diafonía): una variante de la relación señal a ruido. Indica el ancho de banda utilizable: por encima de la frecuencia en que ACR = 0 dB, ya no se distingue la señal del ruido.

$$ACR\,[\text{dB}] = NEXT\,[\text{dB}] - \text{Atenuación}\,[\text{dB}]$$

- **Pérdida de retorno (RL):** la diferencia entre la señal de prueba y la reflejada por las variaciones de impedancia.
- **Capacidad marginal:** la menor diferencia entre un parámetro medido y su límite; cuanto más alta, mejor.

**Los tipos de pregunta que toman:** qué cable (directo o cruzado) va entre dos equipos, las normas T568A y T568B, y qué mide cada parámetro de certificación.

### 2. Ejemplo resuelto (material propio sobre la clase)

> Se quiere conectar: a) una PC a un switch; b) dos switches entre sí; c) dos PC directamente. Indicar qué cable se usa en cada caso y cómo se arma.

Regla: equipos distintos, cable directo; equipos iguales, cable cruzado.

```
Paso 1: PC con switch
  Equipos distintos → cable directo: T568B en los dos extremos (o T568A en los dos).

Paso 2: switch con switch
  Equipos iguales → cable cruzado: T568A en un extremo y T568B en el otro.

Paso 3: PC con PC
  Equipos iguales → cable cruzado.

Paso 4: cómo se arma
  Se quitan unos 2 cm de vaina, se ordenan los hilos según la norma, se destrenzan
  lo mínimo (menos de 13 mm), se insertan en la ficha RJ-45, se controla el orden y
  se crimpa.

Control: los directos tienen la misma norma en las dos puntas; los cruzados, una
de cada una ✓
```

### 3. Ejercicio guiado (material propio sobre la clase)

> Un certificador mide en un enlace Cat 5e un NEXT de 38 dB y una atenuación de 21 dB a 100 MHz. Calcular el ACR e interpretarlo. ¿Qué otros parámetros mide la certificación?

```
Paso 1: ACR
  → ________

Paso 2: interpretación
  → ________

Paso 3: otros parámetros de la certificación
  → ________
```

### 4. Práctica

Intentá responder cada una en dos o tres líneas antes de mirar las respuestas.

1. ¿Qué diferencia hay entre las normas T568A y T568B? ¿Importa cuál se usa?
2. ¿Qué es un par dividido y por qué el mapa de cableado solo con continuidad no alcanza para detectarlo?
3. ¿Qué indica un NEXT bajo? ¿Y un ACR de 0 dB?
4. ¿Qué cable usarías entre un router y un switch? ¿Y entre dos routers?

### 5. Cierre

**Fórmulas**

$$ACR = NEXT - \text{Atenuación} \quad [\text{dB}]$$

```
T568B: bl-naranja, naranja, bl-verde, azul, bl-azul, verde, bl-marrón, marrón
T568A: igual, con los pares verde y naranja intercambiados
Directo (misma norma en las dos puntas): equipos distintos.  Cruzado (A-B): equipos iguales
Certificación: mapa, resistencia, longitud, retardo y diferencia de retardo, impedancia,
               atenuación, NEXT, FEXT, PSNEXT, ACR, pérdida de retorno, capacidad marginal
```

**Trampas**
- **Creer que un NEXT alto es malo.** El NEXT se expresa como la diferencia entre la señal y la diafonía: cuanto más alto, menos diafonía.
- **Confundir par invertido con par dividido.** El invertido cambia los dos hilos de un par; el dividido mezcla hilos de dos pares.
- **Usar cable directo entre dos equipos iguales.** Va cruzado.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Qué es el ACR y qué indica?
2. (Pregunta) Nombrá cinco parámetros de certificación y qué mide cada uno.

## Respuestas del capítulo 8

### 8.1 Ejercicio guiado

```
Paso 1: 16 × 2 = 32 bocas
Paso 2: (8 + 72) / 2 × 1,10 = 40 × 1,10 = 44 m
Paso 3: 305 / 44 = 6,9  →  6 cables por caja
Paso 4: 32 / 6 = 5,3  →  6 cajas  (1.830 m)
Paso 5: 32 / 24 = 1,3  →  2 patch panels
Paso 6: 72 × 1,10 = 79,2 m ≤ 90 m ✓

Control: 32 × 44 = 1.408 m ≤ 1.830 m ✓
```

### 8.1 Ejercicio extra 1

```
85 × 1,10 = 93,5 m > 90 m  →  no cumple (y aun sin holgura queda al límite).
Hay que acercar el armario de piso o agregar otro armario (IDF) para esa zona,
unido al MDF por el cableado vertical.
```

### 8.1 Ejercicio extra 2

Los subsistemas son: el **puesto de trabajo** (dos bocas RJ-45 por puesto y tomas eléctricas); el **cableado horizontal**, del puesto al armario de piso, en UTP (Cat 5e o superior), de hasta 90 m; el **armario de piso o IDF**, con patch panels y patch cords; el **cableado vertical o troncal**, del IDF a la sala de equipos, en fibra óptica multimodo para datos y multipares para telefonía; la **sala de equipos o MDF**, con los equipos de red y servidores; las **instalaciones de entrada**, donde llegan los servicios externos; el **cableado de campus**, entre edificios; y la **documentación**.

### 8.1 Ejercicio extra 3

El canal horizontal completo mide como máximo 100 m: 90 m de cable fijo más 10 m de patch cords (según la clase, 3 m del lado del usuario y 7 m en el armario). No se permiten empalmes, derivaciones ni puentes porque cada unión agrega pérdidas, reflexiones por cambios de impedancia y diafonía, y el enlace dejaría de cumplir su categoría.

### 8.1 Autoevaluación

```
1. El IDF es el armario de cada piso, donde termina el cableado horizontal. El MDF es
   la sala de equipos principal del edificio. Los une el cableado vertical (backbone),
   en estrella desde el MDF, normalmente en fibra multimodo.

2. Promedio: (20 + 50) / 2 × 1,10 = 38,5 m  →  305 / 38,5 = 7,9 → 7 por caja
   30 / 7 = 4,3  →  5 cajas
```

### 8.2 Ejercicio guiado

```
Paso 1: ACR = NEXT − atenuación = 38 − 21 = 17 dB

Paso 2: interpretación
  La señal que llega supera en 17 dB a la diafonía: hay buena relación entre señal
  y ruido a 100 MHz. Si el ACR llegara a 0 dB, no se distinguiría la señal del ruido.

Paso 3: otros parámetros
  Mapa de cableado, resistencia, longitud, retardo y diferencia de retardo,
  impedancia característica, FEXT, PSNEXT, pérdida de retorno y capacidad marginal.
```

### 8.2 Práctica

```
1. Cambia el orden de los pares naranja y verde. Cualquiera sirve, pero hay que usar la
   misma en toda la instalación (y en las dos puntas de un cable directo).
2. Es cuando se mezclan hilos de dos pares distintos. Hay continuidad pin a pin, pero
   los hilos que viajan juntos no forman un par trenzado: se pierde la cancelación y
   sube la diafonía. Se detecta midiendo NEXT, no solo continuidad.
3. Un NEXT bajo indica mucha diafonía: mala calidad de componentes o de instalación
   (por ejemplo, pares destrenzados de más). Un ACR de 0 dB indica que la señal llega
   al nivel de la diafonía: por encima de esa frecuencia el enlace no sirve.
4. Router con switch: directo (equipos distintos). Router con router: cruzado.
```

### 8.2 Autoevaluación

```
1. ACR = NEXT − atenuación, en dB. Es una variante de la relación señal a ruido: indica
   cuánto supera la señal a la diafonía, y con eso el ancho de banda utilizable.

2. Por ejemplo: mapa de cableado (que cada pin llegue a su par), longitud, atenuación
   (pérdida a lo largo del cable), NEXT (diafonía en el extremo cercano) y pérdida de
   retorno (reflexiones por variaciones de impedancia).
```
