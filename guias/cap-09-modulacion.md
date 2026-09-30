# Capítulo 9: Modulación, PCM y multiplexación (TP 9)

## 9.1 Modulación analógica: AM, FM y PM ★★☆☆☆ (1 de 4)

Temas en Lumen: `u4-clasificacion-tecnicas-modulacion`, `u4-modulacion-amplitud-frecuencia-fase`

Apareció en el 2do parcial 2020, Tema 1: reconocer el tipo de modulación en un gráfico y sacar la amplitud, la frecuencia y la fase de la portadora. Es la base de la modulación digital (9.2).

### 1. Conceptos

**Modulación.** Es modificar alguna característica de una onda **portadora** en función de otra onda, la **moduladora**, que lleva la información. El resultado es la onda **modulada**, que es la que se transmite. La **demodulación** es el proceso inverso: recuperar la moduladora de la modulada. Se modula porque la señal útil no tiene una frecuencia apta para el canal.

**La portadora.** Es una senoidal de frecuencia apta para el canal, con tres características que se pueden variar:

$$e(t) = A \cdot \operatorname{sen}(\omega_c t + \varphi) \qquad \omega_c = 2\pi f_c$$

Según cuál se varíe, la modulación es de amplitud (A), de frecuencia ($\omega_c$) o de fase ($\varphi$).

**Clasificación** (clase de modulación):
```
Portadora senoidal (onda continua):
  moduladora analógica:  AM, FM, PM
  moduladora digital:    ASK, FSK, PSK, QAM  (bloque 9.2)
Portadora de pulsos:
  analógica:  PAM (amplitud), PDM (duración), PPM (posición del pulso)
  digital:    PCM, modulación delta, delta diferencial  (bloque 9.3)
```

**AM (modulación de amplitud).** Varía la amplitud de la portadora siguiendo a la moduladora; la moduladora queda como la **envolvente** de la modulada. La frecuencia de la moduladora tiene que ser mucho menor que la de la portadora. En el espectro aparecen **dos bandas laterales**, a los dos lados de la portadora: la modulación traslada la moduladora a frecuencias más altas (teorema de la modulación), y el ancho de banda es el doble del de la moduladora:

$$\Delta f_{AM} = 2 f_m \qquad \text{bandas: } f_c - f_m \text{ a } f_c + f_m$$

La usan las radios de onda media. Si en vez de variar el nivel se suprime la portadora para mandar el 0, es la **ASK** (bloque 9.2).

**FM (modulación de frecuencia).** Varía la frecuencia de la portadora. La frecuencia instantánea se aparta de la de la portadora hasta una **desviación máxima** $\Delta f$, que es proporcional a la amplitud de la moduladora. El **índice de modulación** es $\beta = \Delta\omega / \omega_a$. Si β es chico (banda angosta), el ancho de banda es $2 f_m$, como en AM. Si es grande (banda ancha), se usa la **regla de Carson**:

$$B = 2\,(\Delta f + f_m)$$

con $\Delta f$ la desviación máxima y $f_m$ la máxima frecuencia de la moduladora. Es la modulación **menos afectada por el ruido**: la información va en la frecuencia, y el ruido cambia sobre todo la amplitud. A cambio, usa más ancho de banda.

**PM (modulación de fase).** Varía la fase de la portadora; la amplitud y la frecuencia quedan constantes. Con moduladora digital es la PSK (bloque 9.2).

**Los tipos de ejercicio que toman:**
1. **Reconocer** el tipo de modulación en un gráfico o una expresión, y dar la amplitud, la frecuencia y la fase de la portadora.
2. **Ancho de banda** de una señal AM o FM.
3. **Teoría:** clasificación de las técnicas, y cuál es la menos afectada por el ruido.

### 2. Ejemplo resuelto (guía de modulación, TP 8 de 2020, teoría, Ej 3)

> Una portadora de 100 MHz se modula en frecuencia con una señal senoidal de 10 kHz, de manera que la desviación máxima de frecuencia es de 1 MHz. Determinar el ancho de banda aproximado de la señal de FM, y el ancho de banda si la amplitud de la señal moduladora se duplica.

Es de FM de banda ancha (la desviación es mucho mayor que la moduladora): regla de Carson. La desviación es proporcional a la amplitud de la moduladora.

```
Paso 1: Carson
  B = 2 × (Δf + fm) = 2 × (1 MHz + 10 kHz) = 2 × 1.010 kHz = 2.020 kHz

Paso 2: con el doble de amplitud
  Δf = k · A: si A se duplica, Δf pasa a 2 MHz
  B = 2 × (2 MHz + 10 kHz) = 4.020 kHz

Control: la portadora (100 MHz) no aparece en el ancho de banda: solo fija dónde está ✓
```

### 3. Ejercicio guiado (material propio)

> Una portadora de 1 MHz se modula en AM con una señal de voz de hasta 4 kHz. ¿Qué frecuencias ocupa la señal modulada y cuál es su ancho de banda? ¿Qué tipo de señal es la moduladora, la portadora y la modulada?

```
Paso 1: bandas laterales
  → ________

Paso 2: ancho de banda
  → ________

Paso 3: tipo de cada señal (analógica o digital)
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: reconocer la modulación (2do parcial 2020, Tema 1, Ej 6, adaptado)

> El original traía un gráfico. Dada la señal $e(t) = 10\,[1 + 0{,}5 \operatorname{sen}(2\pi \cdot 1000\,t)] \cdot \operatorname{sen}(2\pi \cdot 10^6\,t)$ V, indicar qué tipo de modulación es, la amplitud máxima de la portadora, la frecuencia de la portadora y la fase de la señal modulada.

#### Ejercicio extra 2: teoría (guía de modulación, TP 8 de 2020, teoría, Ej 8)

> ¿Qué tipos de modulación se ven menos afectados por el ruido, y por qué?

#### Ejercicio extra 3: teoría (guía de modulación, TP 8 de 2020, teoría, Ej 6)

> Confeccione un cuadro de los tipos de modulación indicando, para cada uno, si la moduladora, la portadora y la modulada son analógicas o digitales.

### 5. Cierre

**Fórmulas**

$$e(t) = A \operatorname{sen}(\omega_c t + \varphi) \qquad f_c = \frac{\omega_c}{2\pi} \qquad \Delta f_{AM} = 2 f_m \qquad B_{FM} = 2(\Delta f + f_m) \qquad \beta = \frac{\Delta\omega}{\omega_a}$$

```
AM: varía la amplitud (envolvente = moduladora), 2 bandas laterales
FM: varía la frecuencia; la menos afectada por el ruido; más ancho de banda
PM: varía la fase.   Pulsos analógica: PAM, PDM, PPM;  digital: PCM, delta
```

**Trampas**
- **Sumar la portadora al ancho de banda.** El ancho de banda depende de la moduladora (y de la desviación en FM), no de la frecuencia de la portadora.
- **Olvidar el 2 de las dos bandas laterales.** En AM es $2 f_m$.
- **Creer que la desviación de FM depende de la frecuencia de la moduladora.** Depende de su amplitud.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué FM resiste mejor el ruido que AM? ¿Qué paga a cambio?
2. (Ejercicio) Una radio FM tiene desviación máxima de 75 kHz y audio de hasta 15 kHz. ¿Qué ancho de banda ocupa? (material propio)

## 9.2 Modulación digital: ASK, FSK, PSK y QAM ★★★★★ (4 de 4)

Temas en Lumen: `u4-modulacion-amplitud-frecuencia-fase`, `u8-modems-funciones-clasificacion`, `u8-modulacion-qam-codificacion-entrelazada`, `u8-modems-v-34-56k`

Es el tema más tomado del 2do parcial: apareció en todos los relevados. En 2022, el módem PSK de 9600 bps y 2400 baudios; en 2020, un ejemplo de 8-PSK y uno de 16-PSK; en 2023, el 16-QAM.

### 1. Conceptos

**Las tres señales.** En la modulación digital la **moduladora es digital** (los datos), la **portadora es analógica** (una senoidal) y la **modulada es analógica** (lo que sale del módem a la línea).

**ASK (por desplazamiento de amplitud).** La portadora aparece con su amplitud para el 1 y se suprime para el 0. La usaban los sistemas telegráficos.

**FSK (por desplazamiento de frecuencia).** Cada valor de bit se manda con una frecuencia distinta, corrida $\pm\Delta f$ de la portadora. Por ejemplo, el 0 en $f_c + 200$ Hz y el 1 en $f_c - 200$ Hz.

**PSK (por desplazamiento de fase).** Cada símbolo es una fase distinta de la portadora. En **2-PSK** una llave electrónica elige entre la portadora y su versión invertida (180°). En **M-PSK** la fase toma M valores separados:

$$\theta = \frac{2\pi}{M} \qquad (8\text{-PSK: } 45°, \quad 16\text{-PSK: } 22{,}5°)$$

En la PSK convencional la fase se mide contra la portadora sin modular; en la **diferencial**, contra la fase del símbolo anterior.

**Velocidad.** Cada símbolo lleva $\log_2 M$ bits, como en el multinivel (bloque 2.1):

$$V_t = V_m \cdot \log_2 M \qquad \text{(4-PSK: } V_t = 2 V_m\text{; 8-PSK: } 3 V_m\text{; 16: } 4 V_m\text{)}$$

Con la misma Vm (y el mismo ancho de banda), más estados dan más Vt, pero los estados quedan más juntos y el ruido los confunde más: sube la tasa de error.

**Código de Gray.** Las secuencias de bits se asignan a las fases de modo que **dos fases vecinas difieran en un solo bit**. Así, si el ruido hace confundir una fase con su vecina, se equivoca un solo bit. Entre fases opuestas cambian dos bits. Para 8-PSK, la cátedra usa:
```
000 → 0°     001 → 45°     011 → 90°     010 → 135°
110 → 180°   111 → 225°    101 → 270°    100 → 315°
```

**Diagrama vectorial (constelación).** Cada estado es un punto: la distancia al centro es la amplitud y el ángulo es la fase. En PSK todos los puntos están sobre un mismo círculo.
```
8-PSK:                      011 (90°)
               010 (135°)       ●       001 (45°)
                      ●                 ●
         110 (180°) ●───────────┼───────────● 000 (0°)
                      ●                 ●
               111 (225°)       ●       100 (315°)
                            101 (270°)
```

**QAM (modulación de amplitud en cuadratura).** Combina fase y amplitud: los puntos de la constelación ya no están en un solo círculo. Con 16 estados lleva 4 bits por símbolo. En la resolución del 2do parcial 2023, la cátedra armó el 16-QAM con **2 amplitudes y 8 fases** (cada 45°), y asignó los 16 estados en código Gray. La cátedra también compara 16-PSK con 16-QAM:
```
                       16-PSK                 16-QAM
Bits por símbolo       4                      4
Tasa de error          mayor                  menor (puntos más separados)
Robustez al ruido      menor                  mayor
Eficiencia espectral   buena                  mejor
Complejidad y costo    baja, más barato       alta, más caro
```

**Módems.** Un módem (modulador-demodulador) convierte los datos digitales de la computadora en una señal analógica apta para la línea, y al revés. Sus funciones básicas son codificar y modular, y las especiales, detectar y corregir errores y comprimir. Los de banda vocal están normalizados en la serie V de la UIT-T, desde 300 bps (V.21, con FSK) hasta 56 kbps (V.90 y V.92, asimétricos, con QAM y codificación entrelazada, *trellis coded modulation*).

**ADSL y cable módem.**
- **ADSL:** Internet sobre el mismo par de cobre del teléfono. Es **asimétrico**: más velocidad de bajada que de subida. Usa DMT (u OFDM): divide el ancho de banda en muchas subportadoras, cada una modulada con QAM o PSK. Su velocidad no depende de cuántos usuarios haya conectados.
- **Cable módem:** Internet sobre la red de TV por cable, hoy híbrida (fibra y coaxil). El medio se comparte entre los usuarios de la zona.

**Los tipos de ejercicio que toman:**
1. **Te dan Vt y Vm:** piden qué M-PSK hace falta ($\log_2 M = V_t / V_m$), el desfasaje, la tabla de fases en Gray y el diagrama vectorial.
2. **Te dan el tipo de modulación:** piden qué señales son analógicas o digitales, la relación Vt/Vm, las fases y el diagrama.
3. **QAM:** la tabla de amplitudes y fases, y la comparación con PSK.
4. **FSK:** cuántos canales entran en un ancho de banda.

### 2. Ejemplo resuelto (2do parcial 2022, Ej 1)

> Se quiere transmitir por un canal telefónico a 9600 bps y se cuenta con un módem de 2400 baudios que opera con transmisión multinivel y modulación PSK. Hallar: qué tipo de modulación PSK debe emplearse para transmitir a la velocidad requerida, y el diagrama vectorial con la asignación de fases.

Es del tipo 1. De $V_t = V_m \log_2 M$ sale M; de M, el desfasaje; y la tabla se arma en Gray.

```
Paso 1: cantidad de estados
  9.600 = 2.400 · log2 M   →   log2 M = 4   →   M = 16   →   16-PSK

Paso 2: desfasaje entre estados
  θ = 360° / 16 = 22,5°

Paso 3: tabla de fases en código Gray (4 bits; vecinos difieren en 1 bit)
  0000 →   0°      0110 →  90°      1100 → 180°      1010 → 270°
  0001 →  22,5°    0111 → 112,5°    1101 → 202,5°    1011 → 292,5°
  0011 →  45°      0101 → 135°      1111 → 225°      1001 → 315°
  0010 →  67,5°    0100 → 157,5°    1110 → 247,5°    1000 → 337,5°

Paso 4: diagrama vectorial
  16 puntos sobre un mismo círculo (misma amplitud), cada 22,5°, empezando en 0°
  con 0000 y girando en sentido antihorario según la tabla.

Control: 2.400 baudios × 4 bits = 9.600 bps ✓; 0000 y 1000 (0° y 337,5°) también
son vecinos y difieren en 1 bit ✓
```

### 3. Ejercicio guiado (guía de modulación, TP 8 de 2020, práctica, Ej 4; 2do parcial 2020, Tema 1, Ej 8)

> Se tiene un módem con modulación 8-PSK. Indicar: a) de la moduladora, la portadora y la modulada, cuáles son analógicas y cuáles digitales; b) una asignación de fases a las secuencias de bits y el diagrama de fases; c) qué relación hay entre la velocidad de modulación y la de transmisión.

```
Paso 1: tipo de cada señal
  → ________

Paso 2: bits por símbolo y desfasaje
  → ________

Paso 3: tabla de fases en código Gray
  → ________

Paso 4: diagrama de fases
  → ________

Paso 5: relación entre Vt y Vm
  → ________
```

### 4. Práctica

#### Ejemplo resuelto 2: 16-QAM (2do parcial 2023, 2Q)

> Un módem de 2400 baudios debe transmitir a 9600 bps con modulación QAM de 2 amplitudes y 8 fases. Armar la tabla de estados en código Gray y el diagrama vectorial.

Es del tipo 3. Da 16 estados, como el 16-PSK, pero repartidos en dos círculos. Así lo resolvió la cátedra.

```
Paso 1: estados
  9.600 / 2.400 = 4 bits por símbolo   →   M = 16   →   16-QAM (2 amplitudes × 8 fases)

Paso 2: tabla (secuencia de Gray de 4 bits, recorriendo fase y amplitud)
  0000 →   0°, A1     0110 →  90°, A1     1100 → 180°, A1     1010 → 270°, A1
  0001 →   0°, A2     0111 →  90°, A2     1101 → 180°, A2     1011 → 270°, A2
  0011 →  45°, A1     0101 → 135°, A1     1111 → 225°, A1     1001 → 315°, A1
  0010 →  45°, A2     0100 → 135°, A2     1110 → 225°, A2     1000 → 315°, A2

Paso 3: diagrama vectorial
  Dos círculos (A1 el interior, A2 el exterior) y 8 rayos cada 45°: en cada rayo,
  un punto sobre cada círculo. 16 puntos en total.

Control: 2.400 × 4 = 9.600 bps ✓
```

#### Ejercicio extra 1: desfasaje en 16-PSK (guía de modulación, TP 8 de 2020, práctica, Ej 2 y 3)

> Un módem trabaja con 16-PSK. Calcular el desfasaje entre estados y la relación entre la Vt y la Vm.

#### Ejercicio extra 2: 4-PSK (guía de modulación, TP 8 de 2020, práctica, Ej 7)

> Un canal soporta como máximo 1200 baudios y se quiere transmitir a 2400 bps. a) ¿Qué modulación de fase hace falta? b) Proponer una asignación de fases en código Gray. c) ¿Qué relación hay entre Vt y Vm? d) ¿Qué señales son analógicas y cuáles digitales?

#### Ejercicio extra 3: canales FSK (guía de modulación, TP 8 de 2020, práctica, Ej 6)

> En una modulación FSK el 0 se transmite con un desvío de +200 Hz y el 1 con −200 Hz. Entre canales se dejan libres 100 Hz. ¿Cuántas comunicaciones simultáneas entran en un canal telefónico de 4 kHz? ¿Cuál es el ancho de banda de cada una?

#### Ejercicio extra 4: teoría (material propio sobre la clase)

> Compare 16-PSK con 16-QAM. Explique qué es el ADSL y en qué se diferencia del cable módem.

### 5. Cierre

**Fórmulas**

$$V_t = V_m \log_2 M \qquad \theta = \frac{2\pi}{M} = \frac{360°}{M} \qquad \log_2 M = \frac{V_t}{V_m}$$

```
Moduladora: digital.  Portadora: analógica.  Modulada: analógica
ASK: amplitud (1 con portadora, 0 sin).  FSK: frecuencia.  PSK: fase.  QAM: fase + amplitud
Gray: fases vecinas difieren en 1 bit (opuestas, en 2)
8-PSK Gray: 000 0°, 001 45°, 011 90°, 010 135°, 110 180°, 111 225°, 101 270°, 100 315°
16-QAM (cátedra 2023): 2 amplitudes × 8 fases
```

**Trampas**
- **Usar niveles como bits.** 16-PSK son 16 estados = 4 bits; la Vt es 4 veces la Vm, no 16.
- **Asignar las fases en binario común.** Con 000, 001, 010, 011... dos fases vecinas pueden diferir en 2 bits (001 y 010). Va en Gray.
- **Decir que la modulada es digital.** La modulada es analógica: es una senoidal.
- **Dibujar el QAM en un solo círculo.** Si hay 2 amplitudes, son dos círculos.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Para qué sirve el código de Gray en la asignación de fases?
2. (Ejercicio) Un módem de 1600 baudios debe dar 4800 bps con PSK. ¿Qué modulación hace falta, con qué desfasaje? (material propio)

## 9.3 PCM: digitalización de señales ★★☆☆☆ (1 de 4)

Temas en Lumen: `u4-muestreo-cuantificacion-codificacion`, `u4-modulacion-pulsos-analogica-digital`, `u4-pcm-variantes`

Apareció como teoría en el 2do parcial 2022 (los pasos para digitalizar una señal analógica), y es la base del E1 (bloque 9.4). La práctica del TP 9 tiene varios ejercicios de PCM.

### 1. Conceptos

**Digitalizar.** Es convertir una señal analógica (voz, música, video) en una digital. Tiene tres pasos: **muestreo**, **cuantificación** y **codificación**. La **PCM** (modulación por pulsos codificados; en castellano, MIC) es la transmisión de información analógica como señal digital mediante esos tres pasos, en forma continua.

**1. Muestreo: teorema de Nyquist.** Se toman valores de la señal a intervalos regulares. Si la señal tiene su energía hasta una frecuencia máxima $f_{\text{máx}}$ y se muestrea a una frecuencia igual o mayor que el doble, se puede recuperar entera con un filtro pasabajos:

$$f_s \ge 2\,f_{\text{máx}} \qquad T_s = \frac{1}{f_s}$$

La frecuencia mínima, $2 f_{\text{máx}}$, es la frecuencia de Nyquist. Lo que queda después de muestrear son pulsos cuya amplitud es la de la señal en cada instante: una señal **PAM**.

**2. Cuantificación.** Cada muestra, que puede tomar cualquier valor, se aproxima al **nivel** más cercano de un conjunto finito (normalmente una potencia de 2: 64, 128 o 256 niveles). La diferencia entre la muestra y su nivel es el **error (o ruido) de cuantificación**: se pierde información, pero el oído no la nota si los niveles son suficientes.
- **Uniforme:** todos los escalones iguales. El error es constante, así que para señales chicas es grande en proporción.
- **No uniforme:** escalones chicos cerca de cero y grandes en los extremos, para que la relación señal a ruido de cuantificación sea pareja. Se logra con **compansión** (comprimir en la fuente y expandir en el destino) con una ley logarítmica: la **ley A** (Europa) o la **ley µ** (EE.UU.), de la norma G.711 de la UIT-T.

**3. Codificación.** Cada nivel se reemplaza por un código binario de $n$ bits, con $2^n \ge$ niveles.

**Velocidad de salida.**

$$V_t = f_s \cdot n \quad [\text{bps}] \qquad n = \log_2(\text{niveles}) \qquad T_{\text{bit}} = \frac{1}{V_t}$$

**PCM de voz.** La voz se filtra a 4 kHz, así que se muestrea a 8.000 muestras por segundo (una cada 125 µs):
```
Europa:    256 niveles → 8 bits   →  8.000 × 8 = 64 kbps
EE.UU.:    128 niveles → 7 bits   →  8.000 × 7 = 56 kbps
```

**Etapas.** El transmisor PCM tiene un filtro pasabajos, un muestreador, un cuantificador y un codificador. El receptor regenera los pulsos, los decodifica y reconstruye la señal con un filtro.

**Otras modulaciones por pulsos.** Analógicas: PAM (varía la amplitud del pulso), PDM (su duración) y PPM (su posición). Digitales, además de PCM: la **modulación delta**, que manda solo si la señal sube o baja un escalón, y la delta adaptativa, que ajusta el escalón.

**Los tipos de ejercicio que toman:**
1. **Teoría:** los pasos de la digitalización (2022), la cuantificación no uniforme.
2. **Cálculo:** la frecuencia de muestreo, los bits por muestra, la velocidad de salida y el tiempo de bit.
3. **Tabla de cuantificación:** los niveles de tensión y su código.

### 2. Ejemplo resuelto (guía de modulación, TP 8 de 2020, teoría, Ej 4 y 5)

> La señal $e(t) = 7 \operatorname{sen}(2000\pi\,t)$ V se digitaliza con un CODEC de 15 niveles cuánticos uniformes. Hallar: a) la frecuencia de muestreo mínima; b) el período de la señal y el de muestreo; c) los niveles de cuantificación y su código, dejando una combinación de reserva; d) el tiempo de bit y la velocidad de salida.

Es de cálculo con tabla. La frecuencia sale de la pulsación ($\omega = 2\pi f$). Con 15 niveles hacen falta 4 bits, y sobra una combinación.

```
Paso 1: frecuencia de la señal
  ω = 2000π  →  f = ω / 2π = 1.000 Hz

Paso 2: a) muestreo mínimo (Nyquist)
  fs = 2 × 1.000 = 2.000 muestras/s

Paso 3: b) períodos
  De la señal: Tm = 1 / 1.000 = 1 ms       De muestreo: Ts = 1 / 2.000 = 0,5 ms

Paso 4: c) niveles, de −7 V a +7 V, cada 1 V (15 niveles, 4 bits)
  −7 V → 0000   −6 V → 0001   −5 V → 0010   −4 V → 0011   −3 V → 0100
  −2 V → 0101   −1 V → 0110    0 V → 0111   +1 V → 1000   +2 V → 1001
  +3 V → 1010   +4 V → 1011   +5 V → 1100   +6 V → 1101   +7 V → 1110
  Reserva: 1111

Paso 5: d) velocidad y tiempo de bit
  Vt = 2.000 × 4 = 8.000 bps       Tbit = 1 / 8.000 = 125 µs

Control: 2^4 = 16 ≥ 15 niveles, y sobra 1 código ✓
```

### 3. Ejercicio guiado (2do parcial 2022, Ej 4)

> Explique cada uno de los pasos para digitalizar una señal analógica. (Desarrollar la respuesta en no menos de 15 renglones).

```
Paso 1: qué es digitalizar y para qué (PCM)
  → ________

Paso 2: muestreo (teorema de Nyquist)
  → ________

Paso 3: cuantificación (error, uniforme y no uniforme)
  → ________

Paso 4: codificación y velocidad de salida
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: capacidad del vínculo (guía de modulación, TP 8 de 2020, práctica, Ej 1)

> Una señal analógica pasa por un filtro de 4000 Hz y entra a un modulador PCM que toma muestras cada 125 µs, con 128 niveles de cuantificación. Hallar la capacidad del vínculo de salida. ¿Cuál sería con 256 niveles?

#### Ejercicio extra 2: varias señales (guía de modulación, TP 8 de 2020, práctica, Ej 10)

> Se quieren transmitir 12 señales analógicas de Δf = 2 kHz con PCM, con 6 bits por muestra. Calcular la capacidad necesaria.

#### Ejercicio extra 3: video (guía de modulación, TP 8 de 2020, práctica, Ej 9)

> Se quieren transmitir 2 señales de TV digitalizadas con PCM de 512 niveles por muestra. Cada señal ocupa hasta 6 MHz. Calcular la capacidad del canal.

#### Ejercicio extra 4: con Shannon (guía de modulación, TP 8 de 2020, teoría, Ej 2)

> Una señal analógica se muestrea a $f_s = 3\,\Delta f_{\text{máx}}$, con 64 niveles de cuantificación. Si el ancho de banda del canal es la mitad del necesario, ¿qué relación S/N hace falta?

### 5. Cierre

**Fórmulas**

$$f_s \ge 2 f_{\text{máx}} \qquad V_t = f_s \cdot n \qquad n = \log_2(\text{niveles}) \qquad T_{\text{bit}} = \frac{1}{V_t} \qquad T_s = \frac{1}{f_s}$$

```
Pasos: muestreo (Nyquist) → cuantificación (error; uniforme o no uniforme, ley A / µ)
       → codificación
Voz: 8.000 muestras/s (una cada 125 µs); Europa 8 bits = 64 kbps; EE.UU. 7 bits = 56 kbps
Pulsos analógica: PAM, PDM, PPM.  Digital: PCM, delta, delta adaptativa
```

**Trampas**
- **Muestrear a $f_{\text{máx}}$.** Es al menos el doble.
- **Tomar los niveles como bits.** 128 niveles son 7 bits.
- **Olvidar multiplicar por la cantidad de señales** cuando se transmiten varias.
- **Decir que la cuantificación no pierde información.** Siempre hay error de cuantificación.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Para qué sirve la cuantificación no uniforme?
2. (Ejercicio) Una señal de audio de hasta 20 kHz se digitaliza al mínimo de Nyquist con 65.536 niveles. ¿Qué velocidad de salida da? (material propio)

## 9.4 Multiplexación: FDM, TDM, PDH y SDH ★★★☆☆ (2 de 4)

Temas en Lumen: `u4-multiplexacion-fdm-tdm`, `u4-pdh-sdh-sonet`, `u4-tdm-estadistica-stdm`

Apareció en los dos temas de 2020: cómo se obtiene la velocidad del E1 a partir de PCM (en los dos) y las ventajas del SDH frente al PDH (Tema 2).

### 1. Conceptos

**Multiplexar.** Es mandar varias señales (subcanales) por un solo canal de comunicaciones. En el otro extremo, el demultiplexor las separa.

**FDM (por división de frecuencia).** Divide el ancho de banda del canal en subcanales, cada uno en su franja de frecuencias, modulando cada señal con una portadora distinta. Entre subcanales se dejan **bandas de guarda**. En telefonía, cada canal tiene 4 kHz (la voz útil va de 300 a 3400 Hz), y **12 canales forman un grupo primario** (48 kHz); los grupos se van combinando en jerarquías superiores de hasta 2.700 canales. La señal que sale es **analógica**. Una variante moderna es la **OFDM**: muchas subportadoras ortogonales, muy juntas pero sin interferirse, cada una con QAM o PSK (Wi-Fi, ADSL).

**TDM (por división de tiempo).** Cada subcanal usa **todo el ancho de banda, una parte del tiempo**: el multiplexor le da una ranura de tiempo (slot) fija, arma una **trama** con un slot de cada uno más bits de sincronismo, y la manda. El transmisor y el receptor tienen que estar sincronizados. La señal que sale es **digital**. Las ranuras pueden llevar un bit de cada terminal (entramado de bits) o un carácter entero (entramado de caracteres, que necesita almacenar).

**El E1 (norma europea).** Junta 32 canales PCM de 64 kbps en TDM: 30 de voz, uno de sincronismo y uno de señalización. La trama dura 125 µs (una muestra de cada canal) y tiene 32 × 8 = 256 bits:

$$V_{E1} = 32 \times 8 \text{ bits} \times 8.000 \text{ tramas/s} = 32 \times 64 \text{ kbps} = 2.048 \text{ kbps}$$

**El T1 (norma americana).** Junta 24 canales de voz; cada trama lleva 24 × 8 bits más 1 bit de trama (193 bits): $193 \times 8.000 = 1.544$ kbps.

**PDH (jerarquía digital plesiócrona).** Es la primera generación de TDM de alta capacidad: combina E1 en niveles superiores. Se llama plesiócrona (casi sincrónica) porque cada equipo tiene su propio reloj, con una tolerancia amplia, y para igualarlos se **rellenan bits**. Por eso las velocidades no son múltiplos exactos, y para sacar un E1 de un nivel alto hay que demultiplexar todo. Niveles europeos (UIT-T G.702):
```
E1   2,048 Mbps      30 canales
E2   8,448 Mbps      120 canales
E3   34,368 Mbps     480 canales
E4   139,264 Mbps    1.920 canales
```

**SDH (jerarquía digital sincrónica).** Es la segunda generación: toda la red usa un **reloj común**, las velocidades son **múltiplos exactos** y se **intercalan bytes** en vez de rellenar bits. Transporta las señales PDH dentro de **contenedores virtuales**. La trama básica es la **STM-1**: 270 columnas por 9 filas de bytes (2.430 bytes), 8.000 tramas por segundo:

$$V_{STM\text{-}1} = 2.430 \text{ bytes} \times 8 \text{ bits} \times 8.000 = 155{,}52 \text{ Mbps}$$

Tiene cinco niveles: STM-1, 4, 16, 64 y 256 (cada uno, 4 veces el anterior). Sus ventajas frente a PDH: es sincrónica y con tiempos muy precisos, las velocidades son múltiplos exactos, se puede extraer o insertar un tributario sin demultiplexar todo, y lleva bytes de gestión y supervisión en el encabezado.

**SONET.** Es la versión americana del SDH, con otras tramas y velocidades: empieza en STS-1 (51,84 Mbps), y los niveles ópticos se llaman OC-n (OC-3 = 155,52 Mbps, igual que STM-1).

**STDM (TDM estadística).** Aprovecha los tiempos muertos: en vez de un slot fijo por terminal, reparte los slots según la actividad de cada uno. La trama tiene menos slots que canales de entrada ($s < n$), y la suma de las velocidades de entrada puede superar a la de salida. Aprovecha mejor el canal, pero es más cara.

**Concentrador.** Reparte un canal de salida entre n entradas cuya capacidad sumada es mayor ($C_c \le \sum C_i$). Cuanto menor es la salida, más se ahorra, a costa de la calidad del servicio.

**Redes ópticas.** Nodos unidos por fibra que transportan, multiplexan y enrutan, y sobre las que funcionan SDH, IP y otros protocolos como capa física.

**Los tipos de ejercicio que toman:**
1. **Cálculo:** la velocidad del E1 (o del T1) a partir de PCM, y a veces su ancho de banda; la velocidad de la STM-1.
2. **Teoría:** ventajas del SDH frente al PDH; FDM contra TDM y STDM; multiplexor contra concentrador.

### 2. Ejemplo resuelto (2do parcial 2020, Temas 1 y 2; guía de modulación, TP 8 de 2020, práctica, Ej 8)

> Detallar cómo se obtiene la velocidad E1 en el sistema PDH a partir del sistema PCM. Calcular también el ancho de banda del canal que permite transmitir los 30 canales de voz más 2 de señalización y sincronismo.

Se parte de un canal PCM de voz y se multiplica por los 32 canales de la trama TDM. Para el ancho de banda, la cátedra usa un ciclo por bit (como el atajo del bloque 2.2).

```
Paso 1: un canal PCM de voz
  Voz filtrada a 4 kHz → muestreo a 8.000 muestras/s (Nyquist), 256 niveles = 8 bits
  8.000 × 8 = 64.000 bps = 64 kbps

Paso 2: la trama E1 (TDM)
  30 canales de voz + 1 de sincronismo + 1 de señalización = 32 canales
  Trama de 125 µs con 32 × 8 = 256 bits

Paso 3: velocidad del E1
  32 × 64 kbps = 2.048 kbps ≈ 2 Mbps

Paso 4: ancho de banda (criterio de la cátedra)
  Por canal: 8 bits cada 125 µs = 64.000 Hz;  total: 32 × 64 kHz = 2,048 MHz

Control: 256 bits × 8.000 tramas/s = 2.048.000 bps ✓
```

### 3. Ejercicio guiado (material propio sobre la clase de PCM)

> Calcular la velocidad del T1 americano, sabiendo que junta 24 canales de voz de 8 bits por muestra, a 8.000 muestras por segundo, y que cada trama agrega 1 bit de sincronismo. ¿Cuántos bits tiene la trama y cuánto dura?

```
Paso 1: bits por trama
  → ________

Paso 2: duración de la trama
  → ________

Paso 3: velocidad del T1
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: STM-1 (material propio sobre la clase)

> La trama STM-1 del SDH tiene 270 columnas por 9 filas de bytes, y se transmiten 8.000 tramas por segundo. Calcular su velocidad. ¿Cuántos E1 caben, en bruto, en esa velocidad?

#### Ejercicio extra 2: teoría (2do parcial 2020, Tema 2, Ej 10)

> Indique qué ventajas presenta el sistema digital SDH en comparación con el PDH.

#### Ejercicio extra 3: teoría (guía de modulación, TP 8 de 2020, teoría, Ej 9 y 10)

> ¿Qué tipo de señal se obtiene después de multiplexar con FDM y con TDM? Compare FDM, TDM, STDM y el concentrador.

#### Ejercicio extra 4: grupo primario (material propio sobre la clase)

> ¿Qué ancho de banda ocupa un grupo primario FDM de canales telefónicos? ¿Cuántos grupos primarios entran en 240 kHz?

### 5. Cierre

**Fórmulas**

$$V_{\text{canal}} = 8.000 \times 8 = 64 \text{ kbps} \qquad V_{E1} = 32 \times 64 = 2.048 \text{ kbps} \qquad V_{T1} = 193 \times 8.000 = 1.544 \text{ kbps}$$

$$V_{STM\text{-}1} = 270 \times 9 \times 8 \times 8.000 = 155{,}52 \text{ Mbps} \qquad \text{STDM: } s < n \qquad \text{concentrador: } C_c \le \sum C_i$$

```
FDM: frecuencias, bandas de guarda, salida analógica; grupo primario 12 × 4 kHz = 48 kHz
TDM: slots fijos en una trama, salida digital.  STDM: slots según la actividad
PDH: plesiócrona, relleno de bits; E1 2,048 / E2 8,448 / E3 34,368 / E4 139,264 Mbps
SDH: sincrónica, intercalado de bytes, múltiplos exactos; STM-1 155,52 Mbps
SONET: STS-1 51,84 Mbps; OC-3 = STM-1
```

**Trampas**
- **Calcular el E1 con 30 canales.** Son 32: 30 de voz más sincronismo y señalización.
- **Decir que el TDM divide el ancho de banda.** Divide el tiempo: cada canal usa todo el ancho de banda en su slot.
- **Decir que PDH es sincrónica.** Es plesiócrona (casi sincrónica); la sincrónica es SDH.
- **Confundir STDM con concentrador.** El STDM reparte según la actividad sin perder datos; el concentrador comparte una salida menor que la suma de las entradas, a costa de la calidad.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué en PDH hay que demultiplexar todo para sacar un E1, y en SDH no?
2. (Ejercicio) ¿Qué velocidad tendría una trama TDM de 16 canales PCM de 8 bits, sin bits extra? (material propio)

## Respuestas del capítulo 9

### 9.1 Ejercicio guiado

```
Paso 1: bandas laterales
  Inferior: 1.000 − 4 = 996 kHz a 1.000 kHz.  Superior: 1.000 a 1.004 kHz.
  La señal ocupa de 996 kHz a 1.004 kHz.

Paso 2: ancho de banda
  2 × fm = 2 × 4 kHz = 8 kHz

Paso 3: tipo de cada señal
  Moduladora (la voz): analógica.  Portadora: analógica.  Modulada: analógica.
```

### 9.1 Ejercicio extra 1

```
Es AM: la amplitud de la portadora varía siguiendo 1 + 0,5 · sen(2π·1000 t).
Amplitud de la portadora sin modular: 10 V (con la modulación varía entre 5 V y 15 V).
Frecuencia de la portadora: fc = ωc / 2π = 2π · 10^6 / 2π = 1 MHz
Fase: 0 (no hay término de fase sumado)
```

### 9.1 Ejercicio extra 2

La FM, porque la información va en la frecuencia de la portadora y no en su amplitud: el ruido altera sobre todo la amplitud, y esos cambios casi no afectan a la señal demodulada. El costo es un mayor ancho de banda (regla de Carson).

### 9.1 Ejercicio extra 3

```
Modulación            Moduladora   Portadora              Modulada
AM, FM, PM            analógica    analógica (senoidal)   analógica
ASK, FSK, PSK, QAM    digital      analógica (senoidal)   analógica
PAM, PDM, PPM         analógica    pulsos                 pulsos (analógica)
PCM, delta            analógica    pulsos                 digital
```

### 9.1 Autoevaluación

```
1. Porque la información va en la frecuencia y el ruido afecta sobre todo la amplitud.
   Paga con más ancho de banda.
2. B = 2 × (75 + 15) = 180 kHz
```

### 9.2 Ejercicio guiado

```
Paso 1: moduladora digital; portadora analógica; modulada analógica

Paso 2: 8 estados → log2 8 = 3 bits por símbolo;  θ = 360° / 8 = 45°

Paso 3: tabla en Gray
  000 →   0°    001 →  45°    011 →  90°    010 → 135°
  110 → 180°    111 → 225°    101 → 270°    100 → 315°

Paso 4: diagrama
                            011 (90°)
               010 (135°)       ●       001 (45°)
                      ●                 ●
         110 (180°) ●───────────┼───────────● 000 (0°)
                      ●                 ●
               111 (225°)       ●       100 (315°)
                            101 (270°)
  (8 puntos sobre un círculo, cada 45°; los vecinos difieren en 1 bit)

Paso 5: Vt = Vm · log2 8 = 3 Vm
```

### 9.2 Ejercicio extra 1

```
θ = 360° / 16 = 22,5°  (π/8)
Vt = Vm · log2 16 = 4 Vm
```

### 9.2 Ejercicio extra 2

```
a) 2.400 = 1.200 · log2 M  →  log2 M = 2  →  M = 4  →  4-PSK (QPSK)
b) θ = 90°:   00 → 0°    01 → 90°    11 → 180°    10 → 270°
c) Vt = 2 Vm
d) Moduladora digital; portadora analógica; modulada analógica
```

### 9.2 Ejercicio extra 3

```
Cada comunicación ocupa de −200 Hz a +200 Hz alrededor de su portadora: 400 Hz
Más 100 Hz libres entre canales: 500 Hz por comunicación
4.000 Hz / 500 Hz = 8 comunicaciones simultáneas, de 400 Hz cada una
```

### 9.2 Ejercicio extra 4

Las dos llevan 4 bits por símbolo (16 estados), así que a igual Vm dan la misma Vt. En 16-PSK los 16 puntos están en un solo círculo, muy juntos (cada 22,5°); en 16-QAM se reparten en fase y amplitud, más separados, así que QAM tiene menos tasa de error, más robustez al ruido y mejor eficiencia espectral, pero es más compleja y cara.

El **ADSL** da Internet sobre el mismo par de cobre del teléfono, en forma asimétrica (más bajada que subida), con modulación DMT (muchas subportadoras con QAM); su velocidad no depende de los otros usuarios. El **cable módem** usa la red de TV por cable (fibra y coaxil), cuyo medio comparten todos los usuarios de la zona, así que la velocidad varía según cuántos estén conectados.

### 9.2 Autoevaluación

```
1. Para que fases vecinas difieran en un solo bit: si el ruido hace confundir un
   símbolo con su vecino, se equivoca un bit y no varios.
2. 4.800 / 1.600 = 3 bits → M = 8 → 8-PSK, con 360° / 8 = 45° entre fases.
```

### 9.3 Ejercicio guiado

```
Paso 1: qué es
  "Digitalizar es convertir una señal analógica en una secuencia de bits, para
   transmitirla como señal digital (PCM). Tiene tres pasos."

Paso 2: muestreo
  Se toman valores de la señal a intervalos regulares. Por Nyquist, si la señal
  llega hasta fmáx, alcanza con muestrear a fs ≥ 2 fmáx para recuperarla con un
  filtro pasabajos. Queda una señal PAM (pulsos con la amplitud de cada muestra).
  Ejemplo: voz filtrada a 4 kHz → 8.000 muestras/s.

Paso 3: cuantificación
  Cada muestra se aproxima a uno de un conjunto finito de niveles (potencia de 2).
  Se comete un error de cuantificación (ruido). Uniforme: escalones iguales;
  no uniforme: escalones chicos cerca de cero (compansión, ley A o µ, G.711), para
  que la relación señal a ruido de cuantificación sea pareja.

Paso 4: codificación
  Cada nivel se reemplaza por un código de n bits (2^n ≥ niveles). La velocidad
  de salida es fs · n: para voz, 8.000 × 8 = 64 kbps.
```

### 9.3 Ejercicio extra 1

```
Muestras cada 125 µs  →  fs = 8.000 muestras/s (Nyquist para 4 kHz ✓)
128 niveles → 7 bits  →  8.000 × 7 = 56 kbps
256 niveles → 8 bits  →  8.000 × 8 = 64 kbps
```

### 9.3 Ejercicio extra 2

```
fs = 2 × 2 kHz = 4.000 muestras/s;  por señal: 4.000 × 6 = 24 kbps
12 señales × 24 kbps = 288 kbps
```

### 9.3 Ejercicio extra 3

```
fs = 2 × 6 MHz = 12 Msps;  512 niveles → 9 bits
Por señal: 12 × 9 = 108 Mbps;  2 señales: 216 Mbps
```

### 9.3 Ejercicio extra 4

```
6 bits por muestra (64 niveles);  Vt = 3 Δf × 6 = 18 Δf
Canal: Δf' = Δf / 2
Shannon: 18 Δf = (Δf / 2) · log2(1 + S/N)   →   log2(1 + S/N) = 36
S/N = 2^36 − 1 ≈ 6,87 × 10^10   →   10 · log10(6,87 × 10^10) ≈ 108,4 dB
```

### 9.3 Autoevaluación

```
1. Para que la relación señal a ruido de cuantificación sea pareja: las señales
   chicas tienen escalones chicos (poco error) y las grandes, escalones grandes.
2. fs = 2 × 20 kHz = 40.000 muestras/s;  65.536 niveles = 16 bits
   Vt = 40.000 × 16 = 640 kbps
```

### 9.4 Ejercicio guiado

```
Paso 1: 24 canales × 8 bits + 1 bit de sincronismo = 193 bits por trama
Paso 2: una muestra de cada canal cada 1 / 8.000 s = 125 µs
Paso 3: 193 bits × 8.000 tramas/s = 1.544.000 bps = 1.544 kbps ≈ 1,5 Mbps
```

### 9.4 Ejercicio extra 1

```
270 × 9 = 2.430 bytes por trama
2.430 × 8 bits × 8.000 tramas/s = 155.520.000 bps = 155,52 Mbps
En bruto: 155,52 / 2,048 ≈ 75 E1 (en la práctica entran 63, por el encabezado y
los contenedores)
```

### 9.4 Ejercicio extra 2

El SDH es **sincrónico**: toda la red usa un reloj común, con tiempos muy precisos, mientras que el PDH es plesiócrono y necesita rellenar bits para compensar los relojes. En SDH las velocidades son **múltiplos exactos** entre niveles y se **intercalan bytes**, así que se puede extraer o insertar una señal tributaria (por ejemplo, un E1) **sin demultiplexar todo**; en PDH hay que bajar nivel por nivel. Además, el SDH transporta las señales PDH en contenedores virtuales y lleva en su encabezado bytes de gestión y supervisión de la red.

### 9.4 Ejercicio extra 3

Con **FDM** la señal resultante es analógica; con **TDM**, digital. **FDM** asigna a cada subcanal una franja fija de frecuencias, con bandas de guarda; es barata y apta para largas distancias, pero desperdicia ancho de banda. **TDM** da a cada subcanal todo el ancho de banda en un slot de tiempo fijo, lo use o no. **STDM** asigna los slots según la actividad de cada terminal, con menos slots que entradas; aprovecha mejor el canal pero es más cara. El **concentrador** comparte una salida de capacidad menor que la suma de las entradas: ahorra costos a cambio de calidad de servicio.

### 9.4 Ejercicio extra 4

```
Grupo primario: 12 canales × 4 kHz = 48 kHz
240 kHz / 48 kHz = 5 grupos primarios (60 canales)
```

### 9.4 Autoevaluación

```
1. En PDH cada nivel rellena bits para igualar relojes, así que un E1 no está en una
   posición fija de la trama de nivel alto: hay que demultiplexar nivel por nivel.
   En SDH todo es sincrónico y con intercalado de bytes: el E1 está en una posición
   conocida y se puede sacar directamente.
2. 16 × 64 kbps = 1.024 kbps
```
