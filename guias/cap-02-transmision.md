# Capítulo 2: Transmisión de datos (TP 2)

## 2.1 Velocidades, multinivel y sincronismo ★★★★☆ (5 de 8) 📌 2026

Temas en Lumen: `u3-medidas-velocidad-bps-baudios`, `u3-transmision-multinivel-compresion-datos`, `u3-transmision-serie-paralelo-asincronica`

En los parciales viejos es un problema de cuentas. En 2024 y 2026 lo tomaron como teoría: las medidas de velocidad, los tipos de sincronismo y la relación del multinivel con el ancho de banda y la velocidad.

### 1. Conceptos

**Pulso, período (T) y FRP.** Los datos viajan como un tren de pulsos: cada cierto tiempo, el transmisor pone un nivel de tensión en la línea. El **período T** es cada cuánto sale un pulso nuevo, en segundos. La **FRP** (frecuencia de repetición de pulsos) es cuántos pulsos salen por segundo, en pps:

$$FRP = \frac{1}{T}\ [\text{pps}] \qquad\qquad T = \frac{1}{FRP}\ [\text{s}]$$

**Duración del pulso (d).** Es lo que dura el elemento de señal más corto, y depende del código de línea:
- **NRZ** (no retorna a cero): el nivel se mantiene todo el período, así que $d = T$.
- **RZ** (retorna a cero): a la mitad del período la señal vuelve a 0, así que $d = T/2$.

En el dibujo se ven los mismos bits (1 0 1 1) mandados de las dos formas. El período T es igual en las dos; lo que cambia es cuánto dura el nivel:
```
Bits: 1       0       1       1
NRZ polar (d = T): el nivel dura todo el período
  +V  ┌───────┐       ┌───────────────┐
   0 ─┘       │       │               └─
  −V          └───────┘
      |<- T ->|
      |<- d ->|

RZ polar (d = T/2): a la mitad del período vuelve a 0
  +V  ┌───┐           ┌───┐   ┌───┐
   0 ─┘   └───┐   ┌───┘   └───┘   └─────
  −V          └───┘
      |<- T ->|
      |<d>|
```

**Velocidad de modulación (Vm).** Es cuántos elementos de señal por segundo tiene que aguantar la línea. Se mide en **baudios** y sale de la duración del pulso más corto:

$$V_m = \frac{1}{d}\ [\text{baudios}] \qquad\qquad \text{NRZ: } V_m = \frac{1}{T} = FRP \qquad \text{RZ: } V_m = \frac{1}{T/2} = 2 \cdot FRP$$

**Multinivel (n niveles).** Si la señal puede tomar n niveles de tensión en vez de 2, cada pulso lleva más de un bit: $\log_2 n$ bits por pulso. $\log_2 n$ responde a qué potencia hay que elevar 2 para llegar a n:
```
n = 2   → log2 2  = 1 bit por pulso  (binaria)
n = 4   → log2 4  = 2 bits           (dibits)
n = 8   → log2 8  = 3 bits           (tribits)
n = 16  → log2 16 = 4 bits           (cuadribits)
```

**Velocidad de transmisión (Vt).** Es cuántos bits por segundo se mandan, lleven o no información. Se mide en **bps**. En cada período sale un pulso, y cada pulso lleva $\log_2 n$ bits:

$$V_t = \frac{1}{T} \cdot \log_2 n = FRP \cdot \log_2 n\ [\text{bps}] \qquad\qquad \text{con } m \text{ líneas iguales en paralelo: } V_{t,\text{total}} = m \cdot FRP \cdot \log_2 n$$

Ojo: **Vt se calcula con T (la FRP), no con d.** En NRZ binaria dan lo mismo (Vt = Vm). En RZ, Vm es el doble de la FRP, pero Vt no cambia. Así lo resuelve la cátedra en los parciales.

**Las cuatro medidas de velocidad** (clase de teoría, UT 2). Es la respuesta a "¿qué medidas de velocidad conoce?" (1er parcial 2024):
1. **Velocidad de modulación** (baudios): la inversa del intervalo más corto entre dos instantes significativos de la señal, $1/d$. Mide cuántas veces por segundo cambia la señal.
2. **Velocidad de transmisión** (bps): todos los bits que salen por segundo, lleven información o no (arranque, parada, paridad, cabeceras).
3. **Velocidad de transferencia de datos** (bps): el promedio de bits **de datos** por segundo, sin contar los de control. También puede darse en caracteres por minuto, bloques por hora, etc.
4. **Velocidad real (o efectiva) de transferencia de datos** (bps): los bits de datos por segundo que el receptor **acepta como válidos**. Descuenta lo que hay que retransmitir por errores. Con ella se calcula cuánto tarda de verdad un archivo: tiempo = longitud del archivo / velocidad real.

**Multinivel, ancho de banda y velocidad.** Es la pregunta 4 del parcial 2026. El ancho de banda que necesita una señal depende de cuántas veces por segundo cambia, o sea de la Vm: $\Delta f = 1/d$ (bloque 2.2), y un canal de $\Delta f$ Hz aguanta como mucho $V_m = 2\Delta f$ (Nyquist, capítulo 5). El multinivel mete $\log_2 n$ bits en cada pulso, así que **sube la Vt sin subir la Vm**, y por lo tanto sin pedir más ancho de banda:

$$V_t = V_m \cdot \log_2 n \quad \text{(en NRZ)}$$

El límite: con más niveles, los niveles quedan más juntos y el ruido los confunde más fácil. Por eso no se pueden agregar niveles sin fin (Shannon, capítulo 5).

**Tiempo de transmisión.** Es lo que tarda en salir un mensaje completo. Si el mensaje está en bytes, primero se pasa a bits (× 8):

$$\text{Tiempo} = \frac{\text{bits totales}}{V_t}$$

**Sincrónica y asincrónica.** Son dos formas de mandar los datos en serie:
- **Asincrónica (start-stop):** se manda carácter por carácter, y cada uno lleva bits de control. Tiene 1 bit de arranque (start), los bits de datos, a veces 1 de paridad y 1 o 2 de parada (stop). Entre un carácter y el siguiente puede haber cualquier pausa. Es barata, pero gasta muchos bits en control.
- **Sincrónica:** se mandan bloques grandes (de 128 a 1024 bytes) con un reloj común entre el Tx y el Rx. La cabecera es chica comparada con el bloque, así que en los ejercicios se toman todos los bits como datos, salvo que el enunciado te dé la cabecera.

**Los tres tipos de sincronismo** (clase de teoría, UT 2). Es la respuesta a "¿cuántos tipos de sincronismo conoce?" (1er parcial 2024):
1. **De bit:** el receptor tiene que saber en qué momento leer cada bit. Su reloj muestrea la línea mucho más rápido que la Vm (8 o 9 veces), para detectar enseguida cada cambio de 1 a 0 o de 0 a 1. Lo necesitan el receptor, para leer bien los datos, y el repetidor regenerativo, para rehacer los pulsos.
2. **De byte (o de carácter):** determina dónde empieza y dónde termina cada carácter. Es clave en la transmisión **asincrónica**, y lo dan los bits de arranque y de parada.
3. **De bloque:** determina dónde empieza y dónde termina cada bloque. Es clave en la transmisión **sincrónica**.

**Rendimiento.** Es qué parte de lo transmitido son datos útiles. Los bits de arranque, parada y paridad, y las cabeceras, **no** cuentan como datos:

$$\eta = \frac{\text{bits de datos}}{\text{bits totales}} \times 100\ [\%]$$

*Ejemplo de la cátedra.* Un carácter asincrónico con 1 bit de arranque, 7 de datos, 1 de paridad y 2 de parada suma 11 bits, de los cuales 7 son datos: 7/11 = 64 %. En cambio, un bloque sincrónico de 1024 bytes con 10 de cabecera supera el 99 %.

**Los tipos de ejercicio que toman:**
1. **Te dan la FRP (o T), el código (NRZ o RZ) y los niveles:** piden Vm, Vt y el tiempo que tarda un mensaje.
2. **Asincrónica o sincrónica con cabecera:** te dan cómo es el carácter o la trama y cuántos hay; piden tiempo, Vm y rendimiento.
3. **Teoría:** las medidas de velocidad, los tipos de sincronismo o la relación del multinivel con el ancho de banda y la velocidad.

### 2. Ejemplo resuelto (1er parcial, Temas 1 a 4 (2020), Tema 1, Ej 2)

> Un enlace tiene 8 líneas entre el Tx y el Rx. En cada línea se transmite con FRP = 2 Mpps, con código polar RZ y 16 niveles de tensión por pulso. Hallar la velocidad de modulación de cada línea, la velocidad total de transmisión del enlace y el tiempo de transmisión de un mensaje de 10.000.000 de bytes con transmisión sincrónica.

Es del tipo 1. Hay 8 líneas iguales que transmiten a la vez. La FRP está en pulsos por segundo, y el mensaje, en bytes. Como es RZ, d es la mitad de T. Como hay 16 niveles, cada pulso lleva 4 bits. Y como es sincrónica, no hay bits de control que descontar.

```
Paso 1: período
  T = 1 / FRP = 1 / 2.000.000 pps = 0,5 µs

Paso 2: duración del pulso (polar RZ → d = T/2)
  d = 0,5 µs / 2 = 0,25 µs

Paso 3: velocidad de modulación de cada línea
  Vm = 1 / d = 1 / 0,25 µs = 4.000.000 baudios  (4 Mbaudios)

Paso 4: velocidad de transmisión
  Por línea: Vt = FRP · log2 16 = 2.000.000 × 4 = 8.000.000 bps  (8 Mbps)
  Total:     8 líneas × 8 Mbps = 64 Mbps

Paso 5: tiempo de transmisión (sincrónica: todos los bits son del mensaje)
  Bits = 10.000.000 bytes × 8 = 80.000.000 bits
  Tiempo = 80.000.000 bits / 64.000.000 bps = 1,25 s

Control: 64 Mbps × 1,25 s = 80 Mbit = 10 MB ✓
```

### 3. Ejercicio guiado (1er parcial, Temas 1 a 4 (2020), Tema 3, Ej 2)

> Transmisión asincrónica. Cada carácter lleva 1 bit de arranque, 1 de stop, 1 de paridad y 7 de datos. Se mandan 18.000 caracteres con código polar RZ y dos niveles de tensión (+5 V para el 1 y −5 V para el 0). El período de la señal es 416,6 µs. Hallar el tiempo de transmisión, la velocidad de modulación y el rendimiento.

Es del tipo 2 (asincrónica). El dato de tiempo es el período T, en µs. Hay dos niveles, así que cada pulso lleva 1 bit, y cada carácter tiene bits de control además de los datos.

```
Paso 1: bits por carácter y bits totales
  → ________

Paso 2: FRP, duración del pulso y velocidad de modulación (polar RZ)
  → ________

Paso 3: velocidad de transmisión (2 niveles)
  → ________

Paso 4: tiempo de transmisión
  → ________

Paso 5: rendimiento
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: rendimiento asincrónico (Ejercicios tipo parcial 2020, Ej 2)

> Calcular el rendimiento de una transmisión asincrónica cuando el programa de comunicaciones está configurado con 7 bits de datos y 2 bits de parada.

#### Ejercicio extra 2: sincrónica con cabecera y multinivel (Ejercicios tipo parcial 2020, Ej 11)

> ¿Cuál será el tiempo total de transmisión en un enlace sincrónico de 2400 baudios, de una trama de 1024 bytes de datos y 24 bytes de control (header y trailer), si se emplea una codificación multinivel de 16 estados? Defina velocidad de transmisión y velocidad de modulación. Calcular el rendimiento de la transmisión. (Tomá la señal como NRZ.)

#### Ejercicio extra 3: teoría (1er parcial 08/10/2024, Teoría 2 y 4)

> a) ¿Cuántos tipos de sincronismo conoce? Explique cada uno. b) ¿Qué medidas de velocidad conoce? Describa cada una.

#### Ejercicio extra 4: teoría (1er parcial 28/09/2026, Tema B, Ej 4)

> La transmisión multinivel, ¿qué relación tiene con el ancho de banda del medio de comunicación y con la velocidad de transmisión?

### 5. Cierre

**Fórmulas**

$$\begin{aligned}
FRP &= 1/T \qquad V_m = 1/d \qquad (\text{NRZ: } d = T; \ \text{RZ: } d = T/2) \\[4pt]
V_t &= FRP \cdot \log_2 n \qquad V_{t,\text{total}} = m \cdot FRP \cdot \log_2 n \\[4pt]
\text{Tiempo} &= \frac{\text{bits totales}}{V_t} \qquad \eta = \frac{\text{bits de datos}}{\text{bits totales}}
\end{aligned}$$

```
Niveles:  2 → 1 bit   4 → 2 bits   8 → 3 bits   16 → 4 bits
Velocidades: de modulación (baudios), de transmisión, de transferencia de datos, real
Sincronismo: de bit, de byte (asincrónica), de bloque (sincrónica)
```

**Trampas**
- **Calcular la Vt con d en RZ.** La Vt sale de la FRP (1/T). La d solo sirve para la Vm.
- **Creer que el multinivel sube la Vm.** Sube la Vt; la Vm (y el ancho de banda) quedan igual.
- **Olvidar pasar bytes a bits.** Un mensaje de 10.000.000 bytes son 80.000.000 bits.
- **Contar la paridad o el stop como datos.** En el rendimiento, solo cuentan los bits de datos.
- **Confundir velocidad de transmisión con velocidad de transferencia.** La primera cuenta todos los bits; la segunda, solo los de datos.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué el multinivel permite transmitir más rápido por el mismo canal? ¿Qué lo limita?
2. (Ejercicio) Se transmite con FRP = 1200 pps, código polar RZ y 8 niveles. Calculá Vm, Vt y cuánto tarda un archivo de 9.000 bytes en transmisión sincrónica. (material propio)

## 2.2 Fourier del tren de pulsos y ancho de banda ★★★★☆ (5 de 8) 📌 2026

Temas en Lumen: `u2-senales-periodicas-serie-fourier`, `u2-ancho-banda-efecto-sobre`

Apareció en los cuatro temas de 2020 y en 2026, donde fue un problema de 2 puntos que además pedía **graficar el espectro**.

### 1. Conceptos

**Señal periódica.** Es una señal que se repite igual cada T segundos. Su frecuencia es $f = 1/T$, en Hz, y su pulsación angular es $\omega = 2\pi f$, en rad/s.

**Serie de Fourier.** Cualquier señal periódica se puede armar sumando senoidales. Una tiene frecuencia $f_0 = 1/T$ y se llama **fundamental**. Las otras están en $2f_0, 3f_0, 4f_0 \dots$ y se llaman **armónicas**. Cada armónica tiene su amplitud. En comunicaciones importa cuánta amplitud tiene cada una, porque el medio tiene que dejar pasar las importantes para que el receptor pueda reconstruir la señal.

**El tren de pulsos.** Es la señal digital del bloque 2.1: pulsos de amplitud A, que duran d y se repiten cada T.
```
  A   ┌────┐              ┌────┐              ┌────┐
      │    │              │    │              │    │
  0 ──┘    └──────────────┘    └──────────────┘    └─────
      |<d >|
      |<------- T ------->|
```
Los datos salen así:

$$T = \frac{1}{FRP} \qquad\qquad d = \frac{1}{V_m} \qquad\qquad f_0 = \frac{1}{T} = FRP\ [\text{Hz}]$$

**Espectro de amplitud (Cn).** La serie compleja de Fourier de un tren de pulsos con simetría par da la amplitud de cada armónica n:

$$C_n = \frac{A \cdot d}{T} \cdot \frac{\operatorname{sen}(n \pi d / T)}{n \pi d / T}$$

El segundo factor es la función $\operatorname{sen}(x)/x$, que se llama seno cardinal o sinc. Vale 1 en $x = 0$, después oscila achicándose, y **vale cero cada vez que x es un múltiplo de π**. Por eso el espectro tiene forma de "lóbulos": uno principal grande y después otros cada vez más chicos.

**Valor máximo de Cn.** Está en $n = 0$, donde $\operatorname{sen}(x)/x = 1$. Es la componente continua, o sea el valor medio de la señal:

$$C_{n,\text{máx}} = C_0 = \frac{A \cdot d}{T}$$

**El espectro dibujado.** Con $d = T/4$ las armónicas quedan así. Cada barra es una armónica, y entre una y otra hay $f_0$:
```
   |Cn|
 A·d/T ┤ █
       │ █   █
       │ █   █
       │ █   █   █
       │ █   █   █
       │ █   █   █
       │ █   █   █   █           █
       │ █   █   █   █       █   █   █
       └─┴───┴───┴───┴───┴───┴───┴───┴───┴──→ f
         0   f0  2f0 3f0 4f0 5f0 6f0 7f0 8f0
         └─ lóbulo principal ─┘
         primer cero en n = T/d = 4   →   f = 4 · f0 = 1/d
```

**Cómo graficarlo en el parcial.** En 2026 lo pidieron. Marcá cuatro cosas:
1. Los ejes: $|C_n|$ en vertical y la frecuencia en horizontal.
2. La altura máxima, $A \cdot d / T$, en $f = 0$.
3. Las barras separadas $f_0$, cada vez más bajas, siguiendo la envolvente $\operatorname{sen}(x)/x$.
4. El primer cero en $f = 1/d$ (la armónica $n = T/d$), y marcá ahí el ancho de banda.

**Cantidad de armónicas.** El receptor necesita las armónicas del lóbulo principal, o sea desde 0 hasta el primer cero ($x$ entre 0 y π). El primer cero está donde $n \pi d / T = \pi$:

$$n = \frac{T}{d} \qquad \text{(cantidad mínima de armónicas a transmitir)}$$

**Ancho de banda necesario.** Las n armónicas, separadas $f_0$, ocupan:

$$\Delta f = n \cdot f_0 = \frac{T}{d} \cdot \frac{1}{T} = \frac{1}{d}\ [\text{Hz}]$$

Atajo: el ancho de banda en Hz da el mismo número que la Vm en baudios, porque los dos son $1/d$. Cuanto más corto el pulso, más ancho de banda. Por eso RZ, que parte el pulso a la mitad, pide el doble que NRZ.

**Si el canal corta antes.** Si el medio no deja pasar todas las armónicas del lóbulo principal, los pulsos llegan redondeados y deformados, y el receptor puede confundir un bit con otro.

**Los tipos de ejercicio que toman:**
1. **Numérico:** te dan la FRP (o T), la Vm (o d) y A. Piden $f_0$, cantidad de armónicas, ancho de banda y Cn máximo, y a veces el gráfico del espectro (2026).
2. **Teórico:** te dan el dibujo de un tren de pulsos de simetría par. Piden la expresión de Cn, cómo se determinan las armónicas entre 0 y π, la expresión del ancho de banda y $f_0$. Hay que escribir las fórmulas de arriba, con una o dos líneas de explicación cada una.

### 2. Ejemplo resuelto (1er parcial, Temas 1 a 4 (2020), Tema 1, Ej 4)

> Señal digital con FRP = 10 Kpps, velocidad de modulación = 0,2 MBaudios y amplitud del pulso A = 1000 mV. Con el espectro de amplitud de la serie compleja de Fourier, calcular el ancho de banda necesario para transmitir la señal, la cantidad mínima de armónicas a transmitir y el valor máximo de Cn.

Es del tipo 1. La FRP da T y la fundamental. La Vm da d. Con T y d sale todo lo demás. La amplitud está en mV: pasala a V.

```
Paso 1: período y fundamental
  T = 1 / 10.000 = 0,0001 s = 100 µs          f0 = 10.000 Hz = 10 kHz

Paso 2: duración del pulso
  d = 1 / 200.000 = 0,000005 s = 5 µs

Paso 3: cantidad de armónicas
  n = T / d = 100 µs / 5 µs = 20 armónicas

Paso 4: ancho de banda
  Δf = n · f0 = 20 × 10 kHz = 200 kHz

Paso 5: Cn máximo
  A = 1000 mV = 1 V
  Cn máx = A · d / T = 1 V × 5 µs / 100 µs = 0,05 V

Control: 1 / d = 1 / 5 µs = 200.000 Hz = 200 kHz, igual que el paso 4 ✓
```

### 3. Ejercicio guiado (1er parcial, Temas 1 a 4 (2020), Tema 3, Ej 3)

> Hallar el ancho de banda que debería tener un canal si se transmite un tren de pulsos con período de 100 µs y velocidad de modulación de 100 KBaudios. ¿Cuál es la velocidad de transmisión en bps, si la transmisión es serie y se usan 16 niveles de tensión por pulso?

Es del tipo 1, más una Vt del bloque 2.1. T te lo dan, y d sale de la Vm.

```
Paso 1: fundamental
  → ________

Paso 2: duración del pulso
  → ________

Paso 3: cantidad de armónicas
  → ________

Paso 4: ancho de banda
  → ________

Paso 5: velocidad de transmisión (ojo: con T, no con d)
  → ________

Control: calculá 1 / d y comparalo con el paso 4
  → ________
```

### 4. Práctica

#### Ejercicio extra 1 (1er parcial, Temas 1 a 4 (2020), Tema 2, Ej 3)

> Transmisión con velocidad de modulación de 20.000 baudios y FRP de 5 KPPS. Hallar el ancho de banda necesario y la velocidad final de transmisión si se usan 8 niveles de tensión por pulso. En ese caso, ¿cuál es la velocidad de modulación? La frecuencia fundamental es 5 kHz.

#### Ejercicio extra 2 (clase de consulta 2020, Ej 22)

> Canal serie con cuatribits (16 niveles) y pulsos de ancho T = 833,32 µs (NRZ: d = T). Calcular Vt y Vm, cuánto tarda en transmitir 10.000 caracteres de 8 bits y el ancho de banda de la señal.

#### Ejercicio extra 3: teórico (1er parcial, Temas 1 a 4 (2020), Tema 4, Ej 1)

> Dado un tren de pulsos de simetría par: 1) hallar la expresión del espectro de amplitud Cn de la serie compleja de Fourier; 2) detallar cómo se determina el número de armónicas entre 0 y π; 3) hallar la expresión del ancho de banda que debería tener el medio; 4) determinar la frecuencia fundamental f0.

Escribí la respuesta como en el parcial: la fórmula y una o dos líneas que la expliquen.

#### Ejercicio extra 4: con gráfico (1er parcial 28/09/2026, Tema B, Ej 6)

> Dados FRP = 100 pps, velocidad de modulación = 2000 baudios y amplitud del pulso A = 1 V, realizar el gráfico de amplitud del espectro de Fourier. Calcular el ancho de banda, la cantidad de armónicas y el valor de la amplitud máxima de Cn.

### 5. Cierre

**Fórmulas**

$$\begin{aligned}
T &= 1/FRP \qquad d = 1/V_m \qquad f_0 = 1/T \\[4pt]
C_n &= \frac{A d}{T} \cdot \frac{\operatorname{sen}(n\pi d/T)}{n\pi d/T} \qquad C_{\text{máx}} = C_0 = \frac{A d}{T} \\[4pt]
n &= \frac{T}{d} \qquad \Delta f = n \cdot f_0 = \frac{1}{d}
\end{aligned}$$

**Trampas**
- **Tomar d de la FRP.** La FRP da T; d sale de la Vm.
- **Calcular Cn máx con n = 1.** El máximo está en n = 0: es el valor medio $A d / T$.
- **Olvidar pasar unidades.** mV a V, Kpps a pps, µs a s.
- **Graficar sin los datos clave.** Faltan puntos si no marcás la altura $A d / T$, la separación $f_0$ y el primer cero en $1/d$.
- **Decir que el multinivel cambia el ancho de banda.** El ancho de banda depende de d (de la Vm), no de los niveles.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué se transmiten solo las armónicas del lóbulo principal? ¿Qué pasa si el canal corta antes?
2. (Ejercicio) Tren de pulsos con T = 200 µs, d = 20 µs y A = 5 V. Calculá $f_0$, la cantidad de armónicas, el ancho de banda y Cn máximo. (material propio)

## 2.3 Señales y modos de transmisión ☆☆☆☆☆ (0 de 8)

Temas en Lumen: `u2-senales-analogicas-digitales`, `u1-modos-explotacion-sistemas-teleinformaticos`

No apareció en los parciales relevados, pero es la base de los bloques anteriores y aparece en las preguntas de teoría del TP 2.

### 1. Conceptos

**Señales analógicas y digitales.** Una señal analógica es continua: puede tomar infinitos valores, y la información está en la forma de la onda. Una señal digital toma una cantidad finita de niveles, y la información está en los pulsos. La calidad de un canal analógico se mide con la relación señal a ruido (S/N); la de un canal digital, con el BER (bits errados sobre bits transmitidos).

**Ventajas de la transmisión digital** (TP 2):
1. Es menos vulnerable al ruido, porque el receptor solo tiene que distinguir entre pocos niveles.
2. Tiene menos errores.
3. Su alcance es teóricamente infinito, gracias a los repetidores regenerativos.
4. Es más barata.
5. Su calidad se mide fácil, con el BER.

**Repetidor regenerativo.** Es el equivalente digital del amplificador. No amplifica: detecta cada pulso (si llega con un mínimo de energía y de forma, por encima del umbral de detección) y genera uno nuevo y limpio. Así el ruido se elimina en cada regeneración. En cambio, el amplificador analógico amplifica también el ruido y le suma el suyo, así que no se pueden poner infinitos y el alcance analógico es finito.

**Modos de transmisión según el sentido.**
- **Simplex:** en un solo sentido, como la radio.
- **Half duplex (semidúplex):** en los dos sentidos, pero de a uno por vez, como un walkie-talkie.
- **Full duplex (dúplex):** en los dos sentidos a la vez, como el teléfono.

**Serie y paralelo.** En serie los bits van de a uno por una sola línea: sirve para distancias largas y es más lento. En paralelo van varios bits a la vez por varias líneas: es más rápido, pero solo sirve para distancias cortas, porque cada línea va a su ritmo y los bits se desfasan. La asincrónica y la sincrónica son formas de transmitir en serie (bloque 2.1).

**Qué limita la velocidad de un canal** (TP 2): el ancho de banda (Nyquist), el ruido (Shannon), la distorsión, los errores (que obligan a retransmitir) y los bits de control, que bajan el rendimiento.

**Los tipos de pregunta que toman:** definir y comparar (analógica y digital, serie y paralelo), enumerar ventajas o factores, y graficar (señal analógica y digital).

### 2. Ejemplo resuelto (TP 2, teoría, Preguntas 2 y 3)

> Indicar las cinco ventajas más notables de la transmisión digital frente a la analógica. ¿Qué funciones cumple un repetidor regenerativo?

Una respuesta teórica bien armada abre con una frase que define, sigue con los puntos numerados, cada uno con su porqué, y cierra con una comparación.

```
Paso 1: arrancar definiendo
  "En la transmisión digital, la señal toma una cantidad finita de niveles
   y la información va en los pulsos, no en la forma de la onda."

Paso 2: las cinco ventajas, cada una con su porqué
  1. Menos vulnerable al ruido: el receptor solo decide entre pocos niveles.
  2. Menor tasa de error, por lo mismo.
  3. Alcance teóricamente infinito: los repetidores regenerativos rehacen los pulsos.
  4. Menor costo.
  5. Calidad medible con el BER (bits errados / bits totales).

Paso 3: repetidor regenerativo
  "Es el equivalente digital del amplificador. Recibe la señal distorsionada y, si los
   pulsos llegan con un mínimo de energía y forma (sobre el umbral de detección),
   genera pulsos nuevos, iguales a los de la fuente. Así elimina el ruido en cada tramo."

Paso 4: cerrar comparando
  "El amplificador analógico, en cambio, amplifica la señal junto con el ruido y le
   suma su propio ruido, por eso el alcance analógico es finito."
```

### 3. Ejercicio guiado (TP 2, teoría)

> Indicar los factores que limitan la velocidad efectiva de transmisión de datos en una línea.

Armalo como el ejemplo: una frase que defina, los factores con su porqué y un cierre.

```
Paso 1: qué es la velocidad efectiva
  → ________

Paso 2: factores que vienen del canal (dos)
  → ________

Paso 3: factores que vienen de los errores y del protocolo (tres)
  → ________

Paso 4: cierre (qué se puede hacer con cada uno)
  → ________
```

### 4. Práctica

Intentá responder cada una en dos o tres líneas antes de mirar las respuestas.

1. Graficá una señal analógica y una digital e indicá sus principales características. (TP 2)
2. Dá un ejemplo de transmisión simplex, uno de half duplex y uno de full duplex.
3. ¿Por qué la transmisión en paralelo solo sirve para distancias cortas?
4. ¿Con qué se mide la calidad de un canal analógico? ¿Y la de uno digital?

### 5. Cierre

**Fórmulas** (para memorizar)
```
Analógica: continua, infinitos valores, calidad con S/N
Digital:   niveles finitos, información en los pulsos, calidad con el BER
Simplex: un sentido.  Half duplex: dos sentidos, de a uno.  Full duplex: dos a la vez.
Límites de la velocidad: ancho de banda, ruido, distorsión, errores, bits de control
```

**Trampas**
- **Decir que el repetidor amplifica.** Regenera: detecta el pulso y genera uno nuevo.
- **Confundir half duplex con full duplex.** Half duplex usa los dos sentidos, pero nunca a la vez.
- **Poner solo la lista.** Si piden explicar, cada ventaja o factor va con su porqué.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué el alcance de la transmisión digital es teóricamente infinito y el de la analógica no?
2. (Pregunta) Compará la transmisión serie con la paralelo: cómo viajan los bits, velocidad y distancia.

## Respuestas del capítulo 2

### 2.1 Ejercicio guiado

```
Paso 1: bits por carácter y bits totales
  1 arranque + 7 datos + 1 paridad + 1 stop = 10 bits por carácter
  18.000 caracteres × 10 bits = 180.000 bits

Paso 2: FRP, duración del pulso y velocidad de modulación
  FRP = 1 / 416,6 µs ≈ 2.400 pps
  Polar RZ → d = T / 2 = 208,3 µs  →  Vm = 1 / d ≈ 4.800 baudios

Paso 3: velocidad de transmisión (2 niveles → 1 bit por pulso)
  Vt = FRP · log2 2 = 2.400 × 1 = 2.400 bps

Paso 4: tiempo de transmisión
  Tiempo = 180.000 bits / 2.400 bps = 75 s

Paso 5: rendimiento
  η = 7 bits de datos / 10 bits = 70 %

Control: 2.400 bps × 75 s = 180.000 bits ✓
```

### 2.1 Ejercicio extra 1

```
Bits por carácter: 1 arranque + 7 datos + 2 parada = 10 bits (no dice paridad)
η = 7 / 10 = 70 %
```

### 2.1 Ejercicio extra 2

```
Definiciones: Vm = cambios de la señal por segundo (baudios, 1/d);
              Vt = bits por segundo (bps), Vt = Vm · log2 n en NRZ.
16 estados → 4 bits por pulso  →  Vt = 2.400 × 4 = 9.600 bps
Bits de la trama: (1024 + 24) bytes × 8 = 8.384 bits
Tiempo = 8.384 / 9.600 ≈ 0,873 s
η = 1024 / 1048 ≈ 97,7 %

Control: 9.600 bps × 0,873 s ≈ 8.384 bits ✓
```

### 2.1 Ejercicio extra 3

a) Tres tipos. **De bit:** el reloj del receptor muestrea la línea 8 o 9 veces más rápido que la Vm para detectar cada transición y leer cada bit en el momento justo; también lo usa el repetidor regenerativo. **De byte (carácter):** marca el comienzo y el fin de cada carácter; es el que importa en la asincrónica, con los bits de arranque y parada. **De bloque:** marca el comienzo y el fin de cada bloque; es el que importa en la sincrónica.

b) Cuatro medidas. **De modulación** (baudios): $1/d$, cuántas veces por segundo cambia la señal. **De transmisión** (bps): todos los bits por segundo, con información o sin ella. **De transferencia de datos** (bps): solo los bits de datos por segundo. **Real o efectiva** (bps): los bits de datos que el receptor acepta como válidos, descontando retransmisiones; con ella se calcula el tiempo real de un archivo.

### 2.1 Ejercicio extra 4

El ancho de banda que necesita una señal depende de su velocidad de modulación: el pulso más corto dura $d$ y la señal ocupa $\Delta f = 1/d$; visto desde el canal, uno de $\Delta f$ Hz admite como mucho $V_m = 2\Delta f$ (Nyquist). El multinivel usa $n$ niveles para que cada pulso lleve $\log_2 n$ bits, así que $V_t = V_m \cdot \log_2 n$: **aumenta la velocidad de transmisión sin aumentar la de modulación, y por lo tanto sin pedir más ancho de banda al medio**. El límite es el ruido: cuantos más niveles, más juntos quedan y más fácil es confundirlos, y la capacidad máxima la fija Shannon.

### 2.1 Autoevaluación

```
1. Porque cada pulso lleva log2 n bits: sube la Vt sin subir la Vm, y el ancho de
   banda depende de la Vm. Lo limita el ruido: con muchos niveles, quedan tan juntos
   que el receptor los confunde (Shannon).

2. T = 1 / 1200 ≈ 833 µs; RZ → d ≈ 417 µs → Vm = 2.400 baudios
   Vt = 1200 × log2 8 = 1200 × 3 = 3.600 bps
   Tiempo = 9.000 × 8 / 3.600 = 20 s
```

### 2.2 Ejercicio guiado

```
Paso 1: fundamental
  T = 100 µs = 0,0001 s   →   f0 = 1 / 0,0001 s = 10.000 Hz

Paso 2: duración del pulso
  d = 1 / 100.000 = 0,00001 s = 10 µs

Paso 3: cantidad de armónicas
  n = T / d = 100 µs / 10 µs = 10 armónicas

Paso 4: ancho de banda
  Δf = n · f0 = 10 × 10.000 Hz = 100.000 Hz = 100 kHz

Paso 5: velocidad de transmisión (16 niveles = 4 bits)
  Vt = (1 / T) · log2 16 = 10.000 × 4 = 40.000 bps

Control: 1 / d = 1 / 10 µs = 100 kHz, igual que el paso 4 ✓
```

### 2.2 Ejercicio extra 1

```
T = 1 / 5.000 = 200 µs        d = 1 / 20.000 = 50 µs
n = 200 / 50 = 4 armónicas    Δf = 4 × 5 kHz = 20 kHz
Vt = 5.000 × log2 8 = 5.000 × 3 = 15.000 bps
La Vm sigue en 20.000 baudios: el multinivel sube la Vt, pero no cambia la Vm

Control: 1 / d = 1 / 50 µs = 20 kHz ✓
```

### 2.2 Ejercicio extra 2

```
Vm = 1 / 833,32 µs ≈ 1.200 baudios
Vt = 1.200 × 4 = 4.800 bps
Tiempo = 10.000 × 8 bits / 4.800 bps ≈ 16,67 s
Δf = 1 / d ≈ 1.200 Hz
```

### 2.2 Ejercicio extra 3

1. $C_n = \dfrac{A d}{T} \cdot \dfrac{\operatorname{sen}(n\pi d/T)}{n\pi d/T}$: el valor medio $A d / T$ multiplicado por una función $\operatorname{sen}(x)/x$, que se anula cuando x es múltiplo de π.
2. Se toman las armónicas del lóbulo principal, hasta el primer cero: $n \pi d / T = \pi$, o sea $n = T/d$.
3. $\Delta f = n \cdot f_0 = (T/d)(1/T) = 1/d$.
4. $f_0 = 1/T$: la inversa del período, igual a la FRP.

### 2.2 Ejercicio extra 4

```
Paso 1: T = 1 / 100 pps = 10 ms        f0 = 100 Hz
Paso 2: d = 1 / 2.000 baudios = 0,5 ms
Paso 3: n = T / d = 10 / 0,5 = 20 armónicas
Paso 4: Δf = n · f0 = 20 × 100 Hz = 2.000 Hz  (= 1 / d ✓)
Paso 5: Cn máx = A · d / T = 1 V × 0,5 / 10 = 0,05 V

Gráfico: barras cada 100 Hz, la primera de 0,05 V en f = 0, cada vez más bajas
siguiendo sen(x)/x, y el primer cero en 2.000 Hz (la armónica 20).

   |Cn|
 0,05 V ┤ █
        │ █ █ █
        │ █ █ █ █ █
        │ █ █ █ █ █ █ █
        │ █ █ █ █ █ █ █ █ █ █
        │ █ █ █ █ █ █ █ █ █ █ █ █ █ █ █              ▪ ▪ ▪
        └─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─────→ f
          0      500     1000     1500     2000 Hz
          └───────── lóbulo principal ──────────┘
                           Δf = 2 kHz
```

### 2.2 Autoevaluación

```
1. Porque ahí está casi toda la energía de la señal: con esas armónicas el receptor
   reconstruye los pulsos. Si el canal corta antes, los pulsos llegan redondeados y
   deformados, y puede confundir un bit con otro.

2. f0 = 1 / 200 µs = 5 kHz;  n = 200 / 20 = 10 armónicas;
   Δf = 10 × 5 kHz = 50 kHz (= 1 / 20 µs ✓);  Cn máx = 5 × 20 / 200 = 0,5 V
```

### 2.3 Ejercicio guiado

```
Paso 1: qué es la velocidad efectiva
  "Es la cantidad de bits de datos por segundo que el receptor acepta como válidos."

Paso 2: factores del canal
  El ancho de banda: limita la velocidad de modulación (Nyquist).
  El ruido: limita cuántos niveles se pueden distinguir (Shannon).

Paso 3: factores de los errores y del protocolo
  La distorsión: deforma los pulsos y genera errores.
  Los errores: obligan a retransmitir, y lo retransmitido no suma.
  Los bits de control (arranque, parada, paridad, cabeceras): bajan el rendimiento.

Paso 4: cierre
  "Para acercarse al máximo se usan multinivel (más bits por pulso), ecualización
   (contra la distorsión) y transmisión sincrónica (menos bits de control)."
```

### 2.3 Práctica

```
1. Analógica: una curva continua (como una senoidal), infinitos valores posibles, la
   información en la forma de la onda. Digital: escalones entre pocos niveles, la
   información en los pulsos.
2. Simplex: la radio o la TV. Half duplex: un walkie-talkie. Full duplex: el teléfono.
3. Porque cada línea tiene su propio retardo: en distancias largas los bits de un
   mismo carácter llegan desfasados y se mezclan con los del siguiente.
4. Analógico: con la relación señal a ruido (S/N). Digital: con el BER.
```

### 2.3 Autoevaluación

```
1. Porque el repetidor regenerativo rehace los pulsos limpios en cada tramo y el ruido
   no se acumula. El amplificador analógico amplifica el ruido junto con la señal y
   le suma el suyo, así que el ruido crece con la distancia.

2. Serie: los bits de a uno por una línea; más lenta, sirve para distancias largas.
   Paralelo: varios bits a la vez por varias líneas; más rápida, solo para distancias
   cortas por el desfasaje entre líneas.
```
