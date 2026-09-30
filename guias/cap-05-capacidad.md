# Capítulo 5: Capacidad de los canales (TP 5)

## 5.1 Capacidad: Nyquist y Shannon ★★★★☆ (5 de 8) 📌 2026

Temas en Lumen: `u6-capacidad-canal-teorema-shannon`, `u5-capacidad-canal-tasa-informacion`, `u6-tipos-canales-ideales-reales`

Apareció en los cuatro temas de 2020 como problema. En 2026 fue teoría: deducir Shannon-Hartley a partir del canal ideal, con sus parámetros y unidades. Usa las velocidades del bloque 2.1 y la tasa de información del bloque 4.2.

### 1. Conceptos

**Ancho de banda (Δf).** Es el rango de frecuencias que el canal deja pasar, en Hz: la frecuencia de corte superior menos la inferior. Un canal telefónico deja pasar de 300 a 3300 Hz, así que tiene $\Delta f = 3000$ Hz. Cuanto más ancho de banda, más pulsos por segundo se pueden mandar.

$$\Delta f = FCS - FCI\ [\text{Hz}]$$

**Canal ideal, sin ruido: Nyquist.** Si el canal no tiene ruido, lo único que limita es el ancho de banda. Un canal de $\Delta f$ Hz aguanta como mucho $2\Delta f$ pulsos por segundo. Si cada pulso tiene n niveles, lleva $\log_2 n$ bits (bloque 2.1):

$$V_{m,\text{máx}} = 2\,\Delta f\ [\text{baudios}] \qquad\qquad C = 2\,\Delta f \cdot \log_2 n\ [\text{bps}]$$

Sin ruido, la capacidad subiría sin límite con solo agregar niveles. En la realidad, el ruido no deja distinguir niveles muy juntos, y ahí entra Shannon.

**Canal real, con ruido: Shannon-Hartley.** Da la capacidad máxima de un canal con ruido blanco gaussiano, uses los niveles que uses:

$$C = \Delta f \cdot \log_2\left(1 + \frac{S}{N}\right)\ [\text{bps}]$$

Ojo: **S/N va en veces**, no en dB. Si te la dan en dB, primero pasala a veces.

**De Nyquist a Shannon.** Es la pregunta 1 del parcial 2026, y así lo deduce la cátedra en la clase práctica del TP 5. Se parte de la capacidad del canal ideal con la mayor cantidad de niveles que el ruido todavía deja distinguir:

$$C = V_{t,\text{máx}} \cdot \log_2 n_{\text{máx}} \qquad \text{con} \qquad V_{t,\text{máx}} = 2\,\Delta f \qquad \text{y} \qquad n_{\text{máx}} = \left(1 + \frac{S}{N}\right)^{1/2}$$

El $n_{\text{máx}}$ sale de comparar amplitudes: la señal más el ruido llega a una amplitud proporcional a $\sqrt{S + N}$, y dos niveles se distinguen si los separa por lo menos la amplitud del ruido, $\sqrt{N}$. Entonces entran $\sqrt{(S + N)/N} = \sqrt{1 + S/N}$ niveles. Reemplazando:

$$C = 2\,\Delta f \cdot \log_2\left(1 + \frac{S}{N}\right)^{1/2} = 2\,\Delta f \cdot \frac{1}{2}\log_2\left(1 + \frac{S}{N}\right) = \Delta f \cdot \log_2\left(1 + \frac{S}{N}\right)$$

**Parámetros y unidades** (la otra parte de la pregunta de 2026): $\Delta f$ es el ancho de banda del canal, en **Hz**. $S$ es la potencia media de la señal y $N$ la potencia media del ruido, **en la misma unidad** (por ejemplo, los dos en W), así que $S/N$ va **en veces**, sin unidad, y nunca en dB. Con el logaritmo en **base 2**, C da en **bits por segundo**.

**Relación señal a ruido (S/N).** Es la potencia de la señal dividida por la potencia del ruido. Se da en veces o en dB, con el mismo decibel del bloque 3.1:

$$S/N\,[\text{dB}] = 10 \log_{10}(S/N) \qquad\qquad S/N = 10^{\,S/N[\text{dB}]/10}$$

```
10 dB = 10 veces       20 dB = 100 veces       24 dB ≈ 251 veces
30 dB = 1000 veces     40 dB = 10.000 veces    −3 dB = 0,5 veces
```

"La señal supera al ruido 1000 veces" quiere decir S/N = 1000, o sea 30 dB. Si te dan tensiones en vez de potencias (por ejemplo, señal de 10 V y ruido de 5 mV), usá $20 \log_{10}(V_s/V_n)$, porque la potencia va con el cuadrado de la tensión.

**log2 con la calculadora.** Se hace con log10: $\log_2 x = \log_{10} x / 0{,}301$. Por ejemplo, $\log_2 1001 \approx 9{,}97 \approx 10$, porque $2^{10} = 1024$. Para despejar al revés: si $\log_2(1 + S/N) = 8$, entonces $1 + S/N = 2^8 = 256$.

**Cómo se une con la fuente.** Para que la fuente entre en el canal, su tasa tiene que ser, como mucho, la capacidad. En los ejercicios se iguala tasa = C y se despeja lo que falta:
- Si te dan S/N, o te piden S/N: Shannon.
- Si el canal no tiene ruido, o te piden cantidad de niveles: Nyquist.

(En la clase de consulta 2020, sin dato de S/N, la cátedra usó Nyquist con n = cantidad de niveles de gris).

**Los tipos de ejercicio que toman:**
1. **Te dan Δf y S/N:** piden la capacidad (Shannon) y a veces cuántos niveles harían falta sin ruido (Nyquist).
2. **Te dan una fuente (baudios, código, niveles) y Δf:** sacás Vt como en el bloque 2.1, la igualás a C y despejás S/N en dB.
3. **Imágenes:** calculás la tasa de información (bloque 4.2) y de ahí el ancho de banda o la S/N.
4. **Teoría:** deducir Shannon desde Nyquist, con parámetros y unidades (2026).

### 2. Ejemplo resuelto (1er parcial, Temas 1 a 4 (2020), Tema 1, Ej 3)

> Una fuente transmite con código polar RZ a 8.000 baudios. Calcular la relación señal a ruido necesaria del canal, en dB, si el ancho de banda del canal es 0,5 kHz.

Es del tipo 2. El dato de la fuente es Vm, en baudios. Como es RZ, hay que volver a T para sacar Vt (bloque 2.1). No dice niveles, así que es binaria. Después, Vt es la capacidad que tiene que tener el canal, y de Shannon se despeja S/N.

```
Paso 1: duración del pulso
  d = 1 / Vm = 1 / 8.000 = 125 µs

Paso 2: período y FRP (polar RZ → d = T/2 → T = 2 · d)
  T = 250 µs   →   FRP = 1 / T = 4.000 pps

Paso 3: velocidad de transmisión (binaria: log2 2 = 1)
  Vt = 4.000 × 1 = 4.000 bps

Paso 4: Shannon con C = Vt (Δf = 0,5 kHz = 500 Hz)
  4.000 = 500 · log2(1 + S/N)   →   log2(1 + S/N) = 4.000 / 500 = 8

Paso 5: S/N en veces
  1 + S/N = 2^8 = 256   →   S/N = 255

Paso 6: S/N en dB
  10 · log10(255) ≈ 24,07 dB

Control: 500 · log2(1 + 255) = 500 × 8 = 4.000 bps ✓
```

### 3. Ejercicio guiado (1er parcial, Temas 1 a 4 (2020), Tema 3, Ej 4)

> Imagen de TV en blanco y negro con 25 cuadros por segundo. Cada cuadro tiene 300 líneas horizontales por 400 verticales, y cada píxel puede tomar 16 niveles de gris. El nivel de compresión es del 80 %. Calcular la tasa de transmisión y la relación señal a ruido del canal en dB, si el ancho de banda es de 240 kHz.

Es del tipo 3. Con los datos de la imagen sacás la tasa (bloque 4.2). El ancho de banda está en kHz: pasalo a Hz. Después igualás tasa = C en Shannon y despejás S/N.

```
Paso 1: bits por píxel
  → ________

Paso 2: bits por cuadro
  → ________

Paso 3: tasa sin comprimir
  → ________

Paso 4: compresión del 80 % (¿cuánto queda?)
  → ________

Paso 5: Shannon con C = tasa, y despejar log2(1 + S/N)
  → ________

Paso 6: S/N en veces
  → ________

Paso 7: S/N en dB
  → ________

Control: calculá C con la S/N que obtuviste
  → ________
```

### 4. Práctica

#### Ejemplo resuelto 2: imagen, Shannon y FRP (1er parcial, Temas 1 a 4 (2020), Tema 2, Ej 2)

> 25 cuadros por segundo de 600 × 500 píxeles, con 128 niveles de gris y compresión al 50 %. Calcular la tasa final en Mbps, el ancho de banda del canal si la señal supera al ruido 1000 veces, y la FRP y la velocidad de modulación con polar RZ.

Es del tipo 3, y al final vuelve al bloque 2.1: con la tasa se saca la FRP (binaria: un bit por pulso) y, como es RZ, la Vm es el doble.

```
Paso 1: bits por píxel
  128 niveles   →   log2 128 = 7 bits

Paso 2: tasa sin comprimir
  600 × 500 × 7 × 25 = 52.500.000 bps   (52,5 Mbps)

Paso 3: compresión al 50 %
  52,5 / 2 = 26,25 Mbps

Paso 4: ancho de banda con Shannon (S/N = 1000)
  log2(1 + 1000) ≈ 10
  Δf = 26.250.000 / 10 = 2.625.000 Hz   (≈ 2,6 MHz)

Paso 5: FRP (binaria: un bit por pulso)
  FRP = 26,25 Mpps

Paso 6: velocidad de modulación (polar RZ → el doble de la FRP)
  Vm = 2 × 26,25 = 52,5 Mbaudios

Control: 2.625.000 Hz × 10 = 26,25 Mbps ✓
```

#### Ejercicio extra 1: capacidad y niveles (1er parcial, Temas 1 a 4 (2020), Tema 4, Ej 4)

> Canal de 10 kHz con relación señal a ruido de 24 dB. a) Calcular la capacidad del canal. b) Calcular cuántos niveles de señalización harían falta si el canal no tuviera ruido.

#### Ejercicio extra 2: duplicar la capacidad (TP 5, Ej 3)

> Canal de 4 kHz con S/N = 20 dB. Queremos duplicar la capacidad usando el mismo canal. ¿Cuántas veces hay que aumentar la potencia de la señal? ¿Cuál es la nueva S/N en dB?

#### Ejercicio extra 3: el ruido duplica a la señal (TP 5, Ej 5)

> En un canal la potencia de ruido duplica a la potencia de señal, y la capacidad de transmisión requerida es de 64 kbps. ¿Cuál es la S/N en dB? ¿Cuál sería el ancho de banda requerido?

#### Ejercicio extra 4: con tensiones (TP 5, Ej 6)

> Se mide una línea telefónica de 3,1 kHz de ancho de banda. Cuando la señal es de 10 V, el ruido es de 5 mV. ¿Cuál es la tasa de datos máxima que soporta la línea?

#### Ejercicio extra 5: teoría (1er parcial 28/09/2026, Tema B, Ej 1)

> A partir de la expresión de la capacidad de un canal ideal (sin ruido), hallar la expresión de Shannon-Hartley, e indicar qué parámetros se emplean en esta expresión y cuáles son las unidades que se deben utilizar para que el resultado de la capacidad se exprese en bits/seg.

### 5. Cierre

**Fórmulas**

$$\begin{aligned}
\Delta f &= FCS - FCI \qquad V_{m,\text{máx}} = 2\,\Delta f \qquad C_{\text{Nyquist}} = 2\,\Delta f \log_2 n \\[4pt]
C &= \Delta f \log_2\left(1 + \frac{S}{N}\right) \qquad n_{\text{máx}} = \sqrt{1 + S/N} \\[4pt]
S/N\,[\text{dB}] &= 10 \log_{10}(S/N) \qquad S/N = 10^{\,\text{dB}/10} \qquad \text{con tensiones: } 20 \log_{10}(V_s/V_n)
\end{aligned}$$

```
10 dB = 10     20 dB = 100     24 dB ≈ 251     30 dB = 1000     −3 dB = 0,5
log2 x = log10 x / 0,301       2^8 = 256       2^10 = 1024
```

**Trampas**
- **Meter la S/N en dB en Shannon.** Va en veces: pasala primero.
- **Olvidar el 1 +.** Es $\log_2(1 + S/N)$; al despejar, $S/N = 2^{C/\Delta f} - 1$.
- **Usar Nyquist cuando hay ruido.** Si te dan S/N, es Shannon.
- **Olvidar pasar kHz a Hz.**
- **Con tensiones, usar 10 log.** Si te dan voltios, es $20 \log_{10}$ (o elevás al cuadrado la relación).
- **En la deducción, poner $n_{\text{máx}} = 1 + S/N$.** Es la raíz: $n_{\text{máx}} = (1 + S/N)^{1/2}$, y de ahí sale el 2 que se simplifica.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué en un canal ideal la capacidad podría crecer sin límite y en uno real no? ¿Qué parámetros usa Shannon y en qué unidades?
2. (Ejercicio) Canal telefónico de 3 kHz con S/N = 30 dB. Calculá la capacidad, y cuántos niveles harían falta para lograrla con Nyquist. (material propio)

## 5.2 Atenuación, distorsión y ruido ☆☆☆☆☆ (0 de 8)

Temas en Lumen: `u6-ruido-distorsion-relacion-senal`, `u6-normas-calidad-canales-eco`

No apareció en los parciales relevados como pregunta propia, pero es la base de Shannon (el ruido térmico) y de las causas de errores (bloque 6.1, que sí se tomó en 2026).

### 1. Conceptos

**Perturbaciones.** Son los tres fenómenos que deforman la señal en el canal: la atenuación, la distorsión y el ruido.

**Atenuación.** La señal pierde potencia con la distancia (bloque 3.1). Además, no atenúa igual todas las frecuencias, y eso deforma la señal. Se corrige con un **ecualizador**, que compensa las frecuencias que el canal atenúa de más.

**Distorsión por retardo.** Las distintas frecuencias viajan a distinta velocidad y llegan desfasadas. En datos, un bit se mete en el siguiente. También se corrige con ecualización.

**Ruido.** Es toda perturbación no deseada que **se suma** a la señal. A diferencia de la distorsión, no la produce la señal misma: viene de afuera. Se puede reducir, pero no eliminar. Tipos:
- **Térmico** (blanco o gaussiano): lo produce la agitación de los electrones con la temperatura. Está en todas las frecuencias, siempre. Es el que pone el límite de Shannon. Su potencia es:

$$N = k \cdot T \cdot \Delta f\ [\text{W}] \qquad k = 1{,}38 \times 10^{-23}\ \text{J/K (constante de Boltzmann)}, \quad T \text{ en Kelvin}$$

- **Intermodulación:** aparece en sistemas no lineales. Dos frecuencias se mezclan y generan frecuencias nuevas ($f_1 + f_2$, $f_1 - f_2$...) que caen sobre otras señales.
- **Diafonía** (crosstalk): una señal se mete en la del cable vecino por acoplamiento. Se mide en el extremo cercano (NEXT, la más fuerte) o en el lejano (FEXT). Se reduce trenzando los pares.
- **Impulsivo:** picos cortos, de gran amplitud e irregulares, por ejemplo por tormentas o motores. En voz casi no molesta, pero en datos es el peor, porque arruina varios bits seguidos.

**Ruido y distorsión, la diferencia.** La distorsión es una deformación de la propia señal que produce el canal (por atenuación o retardo distintos según la frecuencia), y es predecible: se corrige con ecualización. El ruido es ajeno a la señal, aleatorio, y se le suma: solo se puede reducir.

**Los tipos de pregunta que toman:** diferenciar ruido de distorsión, describir los tipos de ruido, y el ruido térmico como límite de la capacidad.

### 2. Ejemplo resuelto (pregunta tipo de teoría, material propio sobre la clase de canales)

> Explicar la diferencia entre ruido y distorsión, y los tipos de ruido.

Una respuesta bien armada define cada uno, marca la diferencia clave y después enumera los tipos con su causa.

```
Paso 1: definir la distorsión
  "Es una deformación de la señal que produce el propio canal: atenúa o retarda
   distinto cada frecuencia, y las componentes llegan cambiadas o desfasadas."

Paso 2: definir el ruido
  "Es una señal no deseada, ajena a la transmitida, que se le suma en el camino."

Paso 3: la diferencia clave
  "La distorsión es predecible y se corrige con ecualización. El ruido es aleatorio:
   se puede reducir, pero no eliminar."

Paso 4: los tipos de ruido, con su causa
  Térmico: agitación de los electrones por la temperatura; en todas las frecuencias.
  Intermodulación: mezcla de frecuencias en sistemas no lineales.
  Diafonía: acoplamiento entre cables vecinos; se reduce trenzando.
  Impulsivo: picos cortos y fuertes (tormentas, motores); el peor para los datos.
```

### 3. Ejercicio guiado (material propio)

> Calcular la potencia de ruido térmico de un canal telefónico de 3.100 Hz a 290 K, en W y en dBm. Si la señal llega con −60 dBm, ¿cuál es la S/N en dB?

Primero la fórmula del ruido térmico, después se pasa a dBm (bloque 3.1) y la S/N en dB es una resta.

```
Paso 1: N = k · T · Δf, en W
  → ________

Paso 2: N en mW y en dBm
  → ________

Paso 3: S/N en dB (dBm − dBm = dB)
  → ________
```

### 4. Práctica

Intentá responder cada una en dos o tres líneas antes de mirar las respuestas.

1. ¿Qué es la ecualización y contra qué perturbaciones sirve?
2. ¿Por qué el ruido impulsivo es peor para los datos que para la voz?
3. ¿Qué es la diafonía y cómo se reduce en el par trenzado?
4. ¿Por qué el ruido térmico no se puede eliminar?

### 5. Cierre

**Fórmulas**

$$N = k \cdot T \cdot \Delta f \qquad k = 1{,}38 \times 10^{-23}\ \text{J/K} \qquad S/N\,[\text{dB}] = S\,[\text{dBm}] - N\,[\text{dBm}]$$

```
Perturbaciones: atenuación, distorsión (se corrigen con ecualización), ruido (se reduce)
Ruido: térmico, intermodulación, diafonía (NEXT, FEXT), impulsivo
```

**Trampas**
- **Decir que la distorsión es un tipo de ruido.** La distorsión la produce el canal sobre la propia señal; el ruido se suma desde afuera.
- **Decir que el ruido se elimina.** Se reduce; el térmico siempre está.
- **Usar la temperatura en °C en $kT\Delta f$.** Va en Kelvin: 17 °C son 290 K.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Qué diferencia hay entre ruido y distorsión? ¿Cuál se corrige con ecualización?
2. (Pregunta) Nombrá los cuatro tipos de ruido y la causa de cada uno.

## Respuestas del capítulo 5

### 5.1 Ejercicio guiado

```
Paso 1: bits por píxel
  16 niveles   →   log2 16 = 4 bits

Paso 2: bits por cuadro
  300 × 400 = 120.000 píxeles × 4 bits = 480.000 bits

Paso 3: tasa sin comprimir
  480.000 bits × 25 cuadros/s = 12.000.000 bps   (12 Mbps)

Paso 4: compresión del 80 % (queda el 20 %)
  12.000.000 × 0,2 = 2.400.000 bps   (2,4 Mbps)

Paso 5: Shannon con C = tasa (Δf = 240 kHz = 240.000 Hz)
  2.400.000 = 240.000 · log2(1 + S/N)   →   log2(1 + S/N) = 10

Paso 6: S/N en veces
  1 + S/N = 2^10 = 1024   →   S/N = 1023

Paso 7: S/N en dB
  10 · log10(1023) ≈ 30,1 dB

Control: 240.000 · log2(1024) = 240.000 × 10 = 2.400.000 bps ✓
```

### 5.1 Ejercicio extra 1

```
a) S/N = 10 ^ 2,4 ≈ 251
   C = 10.000 · log2(252) ≈ 10.000 × 7,98 ≈ 79.800 bps   (≈ 80 kbps)
b) Nyquist: 79.800 = 2 × 10.000 · log2 n   →   log2 n ≈ 3,99 ≈ 4   →   n = 16 niveles

Control: 2 × 10.000 × log2 16 = 80.000 bps ≈ C ✓
```

### 5.1 Ejercicio extra 2

```
S/N = 100   →   C = 4.000 · log2(101) ≈ 4.000 × 6,66 ≈ 26.630 bps
C nueva ≈ 53.260 bps   →   log2(1 + S/N nueva) = 2 × 6,66 = 13,32
1 + S/N nueva = 101² = 10.201   →   S/N nueva = 10.200
La potencia de la señal tiene que subir 10.200 / 100 = 102 veces
S/N nueva = 10 · log10(10.200) ≈ 40,1 dB
(Duplicar el log2 equivale a elevar al cuadrado lo de adentro: (1 + S/N)²)
```

### 5.1 Ejercicio extra 3

```
S/N = S / N = 1/2 = 0,5 veces   →   10 · log10(0,5) ≈ −3 dB
64.000 = Δf · log2(1 + 0,5) = Δf × 0,585   →   Δf ≈ 109.400 Hz ≈ 109,4 kHz

Control: 109.400 × 0,585 ≈ 64.000 bps ✓
(Con más ruido que señal igual se puede transmitir, pero con mucho ancho de banda)
```

### 5.1 Ejercicio extra 4

```
Son tensiones: S/N [dB] = 20 · log10(10 / 0,005) = 20 · log10(2.000) ≈ 66 dB
En veces (de potencia): (10 / 0,005)² = 2.000² = 4.000.000
C = 3.100 · log2(4.000.001) ≈ 3.100 × 21,93 ≈ 68.000 bps   (≈ 68 kbps)
```

### 5.1 Ejercicio extra 5

La capacidad de un canal ideal, sin ruido, con señal de $n$ niveles es la de Nyquist: $C = V_{t,\text{máx}} \log_2 n = 2\,\Delta f \log_2 n$. Si hay ruido, no se pueden usar niveles arbitrariamente juntos: la cantidad máxima de niveles distinguibles es $n_{\text{máx}} = \sqrt{(S + N)/N} = (1 + S/N)^{1/2}$, porque la amplitud de señal más ruido es proporcional a $\sqrt{S + N}$ y cada nivel tiene que separarse del siguiente por lo menos en la amplitud del ruido, $\sqrt{N}$. Reemplazando:

$$C = 2\,\Delta f \log_2 (1 + S/N)^{1/2} = \Delta f \log_2(1 + S/N)$$

**Parámetros y unidades:** $\Delta f$, el ancho de banda del canal, en Hz; $S$ y $N$, las potencias medias de la señal y del ruido blanco gaussiano, en la misma unidad (W), así que $S/N$ va en veces (no en dB); con logaritmo en base 2, $C$ resulta en bits/s.

### 5.1 Autoevaluación

```
1. En un canal ideal basta con agregar niveles: C = 2 Δf log2 n crece con n. En uno
   real, el ruido no deja distinguir niveles muy juntos y la capacidad queda limitada
   por Shannon. Parámetros: Δf en Hz, S/N en veces (potencias en la misma unidad);
   C en bps.

2. S/N = 1000  →  C = 3.000 · log2(1001) ≈ 3.000 × 9,97 ≈ 29.900 bps (≈ 30 kbps)
   Nyquist: 29.900 = 2 × 3.000 · log2 n  →  log2 n ≈ 4,98 ≈ 5  →  n = 32 niveles
```

### 5.2 Ejercicio guiado

```
Paso 1: N = k · T · Δf
  N = 1,38 × 10^−23 × 290 × 3.100 ≈ 1,24 × 10^−17 W

Paso 2: en mW y dBm
  1,24 × 10^−17 W = 1,24 × 10^−14 mW
  10 · log10(1,24 × 10^−14) ≈ −139,1 dBm

Paso 3: S/N en dB
  −60 dBm − (−139,1 dBm) ≈ 79,1 dB
```

### 5.2 Práctica

```
1. Es compensar las frecuencias que el canal atenúa o retarda de más, para que todas
   lleguen parejas. Sirve contra la atenuación dependiente de la frecuencia y contra
   la distorsión por retardo; no sirve contra el ruido.
2. Porque son picos cortos: en la voz se oyen como un chasquido, pero en datos cada
   pico arruina varios bits seguidos.
3. Es el acoplamiento de la señal de un cable en el vecino. En el par trenzado se
   reduce trenzando los conductores: las inducciones se compensan.
4. Porque lo produce la agitación térmica de los electrones, que existe a cualquier
   temperatura por encima del cero absoluto.
```

### 5.2 Autoevaluación

```
1. La distorsión es una deformación de la propia señal que produce el canal; el ruido
   es una señal ajena que se suma. La que se corrige con ecualización es la distorsión.
2. Térmico (agitación de electrones por temperatura), intermodulación (mezcla de
   frecuencias en sistemas no lineales), diafonía (acoplamiento entre cables
   vecinos) e impulsivo (picos por tormentas, motores, conmutaciones).
```
