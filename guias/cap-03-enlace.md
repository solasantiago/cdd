# Capítulo 3: Cálculo de enlaces e interfaces (TP 3)

## 3.1 Cálculo de enlace ★★★★★ (8 de 8) 📌 2026

Temas en Lumen: `u2-espectro-electromagnetico-unidades-medida`, `u2-transmision-medios-conductores-dielectricos`

Aparece en todos los parciales relevados. En 2026 fue un problema de 2 puntos: la potencia necesaria en un enlace con amplificador.

### 1. Conceptos

**Qué es un enlace.** Un transmisor (Tx) manda una señal por un medio (cable coaxil, fibra) hasta un receptor (Rx). En el camino la señal pierde potencia: la atenúa el cable y la debilitan los conectores y los empalmes. El enlace funciona si al receptor le llega suficiente potencia.

**Potencia de transmisión (Ptx).** Es la potencia con la que el Tx manda la señal al enlace, antes de las pérdidas.

**Sensibilidad del receptor (Srx).** Es la potencia mínima que el receptor puede detectar. Si llega menos, no entiende la señal.

**El decibel (dB).** Mide una relación entre dos potencias, no una potencia en sí:
$$G_{\text{dB}} = 10 \cdot \log_{10}\left(\frac{P_{\text{salida}}}{P_{\text{entrada}}}\right)$$
Sirve para expresar ganancias y pérdidas. Conviene memorizar estos valores:
$$\begin{array}{rlcrl} \times 2 & \rightarrow +3\ \text{dB} & \qquad\qquad & \div 2 & \rightarrow -3\ \text{dB} \\ \times 10 & \rightarrow +10\ \text{dB} & & \div 10 & \rightarrow -10\ \text{dB} \\ \times 100 & \rightarrow +20\ \text{dB} & & \div 100 & \rightarrow -20\ \text{dB} \end{array}$$
Por ejemplo, "un amplificador que amplifica 10 veces" es una ganancia de 10 dB.

**El dBm.** Es una potencia absoluta, medida contra 1 mW:
$$P_{\text{dBm}} = 10 \cdot \log_{10}\left(\frac{P_{\text{mW}}}{1\ \text{mW}}\right) \qquad\qquad P_{\text{mW}} = 10^{\,P_{\text{dBm}}/10} \quad \text{(para volver a mW)}$$
$$\begin{array}{llll} 1\ \text{mW} = 0\ \text{dBm} \qquad & 10\ \text{mW} = 10\ \text{dBm} \qquad & 100\ \text{mW} = 20\ \text{dBm} \qquad & 1\ \text{W} = 30\ \text{dBm} \\ 0{,}1\ \text{mW} = -10\ \text{dBm} & 0{,}01\ \text{mW} = -20\ \text{dBm} & 1\ \mu\text{W} = -30\ \text{dBm} & \end{array}$$
Antes de meter un dato en la fórmula, pasalo a mW: 10.000 µW son 10 mW y 50 W son 50.000 mW.

**Por qué se suma en vez de multiplicar.** Cada elemento del enlace **multiplica** la potencia que le entra por un factor. Si el factor es menor que 1, es una pérdida; si es mayor que 1, es una ganancia. Si hacés la cuenta en mW, tenés que multiplicar todos esos factores. Si los pasás a dB, alcanza con sumarlos.

*Ejemplo.* Un transmisor envía una señal de **10 mW**. La señal pasa por un cable que la deja en la décima parte (factor **x0,1**, una pérdida) y después por un amplificador que la multiplica por cien (factor **x100**, una ganancia). La potencia está en **mW**. La pérdida y la ganancia son **factores**: dicen cuántas veces cambia la potencia y no tienen unidad. Vamos a calcular cuánta potencia llega al receptor de dos formas y a ver que dan lo mismo.

```
Tx (10 mW) ──→ cable (x0,1) ──→ amplificador (x100) ──→ Rx
```

*Forma 1: en mW, multiplicando.* Se aplica cada factor, en orden, a la potencia:
$$\begin{aligned} \text{Después del cable:}\quad & 10\ \text{mW} \times 0{,}1 = 1\ \text{mW} \\ \text{Después del amplificador:}\quad & 1\ \text{mW} \times 100 = 100\ \text{mW} \quad \leftarrow \text{llega esto} \end{aligned}$$

*Forma 2: en dB, sumando.* La potencia se pasa a dBm, cada factor se pasa a dB y se suma todo:
$$\begin{aligned} P_{tx} &= 10\log_{10} 10 = 10\ \text{dBm} \\ \text{Cable} &= 10\log_{10} 0{,}1 = -10\ \text{dB} && \text{factor} < 1 \Rightarrow \text{dB negativo: pérdida} \\ \text{Amplificador} &= 10\log_{10} 100 = +20\ \text{dB} && \text{factor} > 1 \Rightarrow \text{dB positivo: ganancia} \\[4pt] \text{Llega} &= 10\ \text{dBm} - 10\ \text{dB} + 20\ \text{dB} = 20\ \text{dBm} \end{aligned}$$

*Control.* $20\ \text{dBm} = 10^{20/10}\ \text{mW} = 100\ \text{mW}$. Da lo mismo que en la forma 1 ✓.

**De dónde sale.** La potencia que llega es el producto 10 × 0,1 × 100. Si le aplicás $10\log_{10}$ a ese producto, la propiedad $\log(a \cdot b \cdot c) = \log a + \log b + \log c$ lo parte en tres términos, y cada uno es el valor en dB (o dBm) de un elemento:
$$\underbrace{10\log_{10}(10 \times 0{,}1 \times 100)}_{20\ \text{dBm}} = \underbrace{10\log_{10} 10}_{10\ \text{dBm}} + \underbrace{10\log_{10} 0{,}1}_{-10\ \text{dB}} + \underbrace{10\log_{10} 100}_{+20\ \text{dB}}$$

**Para qué sirve.** En un enlace real hay muchos elementos: 6 bobinas, 5 empalmes, 4 conectores... Un conector de 1 dB multiplica por 0,794 ($10^{-1/10}$). Multiplicar quince factores como ese a mano es un lío, pero en dB alcanza con restar 1 dB quince veces: −15 dB.

Entonces:
- dBm ± dB da dBm: es una potencia a la que le sumás o le restás ganancias o pérdidas (en mW, la multiplicás por un factor).
- dBm − dBm da dB: la diferencia entre dos potencias es una relación. Así se saca el presupuesto de pérdidas: $P_{tx}\,[\text{dBm}] - S_{rx}\,[\text{dBm}]$ = cuántos dB podés perder. (La diapositiva de la cátedra lo escribe "dBm ± dBm = dB", pero la que vas a usar es la resta).
- dBm + dBm no tiene sentido. Nunca sumes dos potencias en dBm. Sumar dB equivale a multiplicar, y dos potencias no se multiplican entre sí. Ejemplo: dos señales de 10 mW juntas dan 10 + 10 = 20 mW = 13 dBm, **no** 10 dBm + 10 dBm = 20 dBm (que serían 100 mW).

**Qué pierde potencia en el enlace:**
- **Conectores**: van a la salida del Tx, a la entrada del Rx y, si el enunciado lo dice, a la entrada y salida de cada amplificador. Contá los que dice el enunciado, porque es el error más común.
- **Cable**: la pérdida depende de la longitud (ej. 2 dB/100 m). $\text{Pérdida} = L \times \alpha$ (longitud por atenuación).
- **Bobinas y empalmes**: el cable viene en bobinas de largo fijo, y entre bobina y bobina hay un empalme. Con $n$ bobinas hay **$n - 1$ empalmes**, haya o no amplificador.
- **Factor de diseño (FD)**: margen de seguridad en dB. Se suma como si fuera una pérdida más.

**Qué agrega potencia:** los amplificadores, con su ganancia en dB.

**La ecuación del enlace** (la única que necesitás):
$$P_{tx}\,[\text{dBm}] \;-\; \text{Pérdidas}\,[\text{dB}] \;+\; \text{Ganancias}\,[\text{dB}] \;=\; S_{rx}\,[\text{dBm}]$$

$$\text{Pérdidas} = \text{conectores} + \text{cable} + \text{empalmes} + FD$$

**Presupuesto de pérdidas.** Es la diferencia Ptx − Srx, más las ganancias si hay amplificador. Dice cuántos dB puede perder la señal en el camino y seguir llegando con la potencia mínima que necesita el receptor. Se le dice "presupuesto" (en inglés, *link budget*) porque funciona como plata para gastar: el Tx te da una cantidad de dB, el Rx te exige que llegue al menos Srx, y lo que hay entre los dos es lo que podés "gastar" en conectores, cable, empalmes y FD. Cada elemento gasta una parte. Si gastás más de lo que tenés, al Rx le llega menos que Srx y el enlace no funciona.

*Ejemplo.* Un Tx envía **10 dBm** y el Rx tiene una sensibilidad de **−15 dBm**. Las dos son potencias en dBm, y la resta entre ellas da dB:
$$\text{Presupuesto} = P_{tx} - S_{rx} = 10\ \text{dBm} - (-15\ \text{dBm}) = 25\ \text{dB}$$

$$\text{conectores} + \text{cable} + \text{empalmes} + FD \;\le\; 25\ \text{dB}$$
No es una fórmula nueva: es la ecuación del enlace, reordenada ($P_{tx} - S_{rx} + \text{Ganancias} = \text{Pérdidas totales}$). La **longitud máxima** es la longitud con la que gastás todo el presupuesto, justo.

**Longitud máxima: la última bobina se corta.** Primero ves cuántas bobinas enteras entran, cada una con su cable y su empalme. Si sobran dB, con ellos entra un pedazo más de cable: la última bobina no hace falta usarla entera. Así lo resuelve el parcial Temas 1 a 4 (2020), Tema 4, Ej 3: 4 bobinas enteras de 1 km más 600 m, total 4.600 m.

**Atenuación según la frecuencia (tabla).** A veces no te dan la atenuación del cable, sino una tabla con la atenuación a distintas frecuencias, y la frecuencia de trabajo no está en la tabla. Se saca con una regla de tres entre las dos frecuencias vecinas (interpolación lineal). Así lo resuelve la cátedra:
$$a(f) = a_1 + (a_2 - a_1)\cdot\frac{f - f_1}{f_2 - f_1}$$

Con la tabla 100 MHz → 7 dB/100 m y 200 MHz → 10,5 dB/100 m, a 110 MHz:

$$a(110) = 7 + (10{,}5 - 7)\cdot\frac{110 - 100}{200 - 100} = 7 + 0{,}35 = 7{,}35\ \text{dB/100 m}$$

**Cómo se dibuja el enlace.** En los parciales no piden dibujarlo (lo único que piden dibujar en el 1er parcial son los códigos banda base, como Manchester). Pero conviene hacer un esquema rápido antes de las cuentas, por dos razones:
- A veces el enunciado **te da el enlace dibujado** en vez de describirlo ("Para el siguiente enlace: ..."), y tenés que saber leerlo. Pasa en la clase de consulta del 1er parcial 2020 y en los ejercicios 4 y 9 del TP 3.
- Dibujado, es más difícil olvidarte de un conector o contar mal los empalmes. En el parcial resuelto, un alumno arrancó el Tema 1 así.

Los símbolos que usa la cátedra son estos (en papel, los conectores van como cuadraditos rellenos y el amplificador, como un triángulo que apunta hacia el Rx):
```
┌────┐                                    ┌────┐
│ Tx │  caja: transmisor / receptor       │ Rx │
└────┘                                    └────┘
  ■     conector (anotás al lado su pérdida, ej. 0,6 dB)
  ●     empalme, entre bobina y bobina (ej. 0,5 dB)
 ───    cable: arriba la longitud, abajo la atenuación (ej. 0,3 dB/km)
  ▷     amplificador: lleva un conector a la entrada y otro a la salida
 └─┘    llave: marca el largo de una bobina, o abajo de todo el FD
```

Por ejemplo, un enlace de fibra de 1,2 km con bobinas de 400 m, un conector en el Tx y otro en el Rx y FD = 10 dB se dibuja así:
```
┌────┐ 0,6 dB                          0,6 dB ┌────┐
│ Tx │■────────────●────────────●────────────■│ Rx │
└────┘   400 m  0,5 dB       0,5 dB           └────┘
Ptx = ?       1.200 m, 0,3 dB/km            Srx = −55 dBm
      └───────────── FD = 10 dB ──────────────┘
```
Leyéndolo contás directo: 2 conectores, 3 bobinas y por eso 2 empalmes (●).

Con un amplificador en el medio queda cortado en dos tramos:
```
┌────┐                       ┌────┐
│ Tx │■── L1 ──■ ▷ ■── L2 ──■│ Rx │     4 conectores: Tx, entrada ampli, salida ampli, Rx
└────┘                       └────┘
```

**Los tipos de ejercicio que toman.** La ecuación del enlace tiene cuatro términos. Te dan todos menos uno y piden el que falta:
1. **La sensibilidad del receptor**: te dan el enlace completo; calculás las pérdidas y despejás Srx.
2. **La potencia necesaria en el transmisor**: igual, pero despejás Ptx.
3. **La longitud máxima (o la cantidad de empalmes)**: te dan Ptx y Srx; con el presupuesto ves cuántas bobinas entran.
4. **Si el receptor detecta la señal**: calculás cuánto llega y lo comparás con Srx.

El tipo 2 es el que se tomó en 2026. Variantes que aparecieron: la atenuación sale de una tabla según la frecuencia (2024) y el cambio de impedancia de la antena (2020 2Q).

### 2. Ejemplo resuelto (1er parcial, Temas 1 a 4 (2020), Tema 2, Ej 1)

> Hallar la sensibilidad del receptor en dBm y mW. Enlace de 1200 m con bobinas de coaxil de 200 m. Un amplificador eleva la potencia 10 veces. Hay conectores en la entrada y la salida del amplificador, a la salida del Tx y a la entrada del Rx. Datos: Ptx = 10.000 µW, empalme = 1 dB, conector = 1 dB, FD = 4 dB, coaxil = 2 dB/100 m.

Es del tipo 1: te dan el enlace completo y piden Srx. La potencia viene en µW (hay que pasarla a mW), la ganancia del amplificador como factor (x10) y las pérdidas en dB.

```
Paso 1: Ptx a dBm
  10.000 µW = 10 mW  →  10 * log10(10) = 10 dBm

Paso 2: ganancias
  Amplificador x10  →  10 dB

Paso 3: pérdidas
  Conectores: Tx + Rx + entrada ampli + salida ampli = 4 × 1 dB  =  4 dB
  Bobinas: 1200 / 200 = 6 bobinas  →  6 − 1 = 5 empalmes × 1 dB  =  5 dB
  Cable: 1200 m × (2 dB / 100 m)                                  = 24 dB
  Factor de diseño                                                 =  4 dB
  Pérdidas totales                                                 = 37 dB

Paso 4: ecuación del enlace
  Srx = Ptx − Pérdidas + Ganancias = 10 − 37 + 10 = −17 dBm

Paso 5: pasar a mW
  Srx = 10 ^ (−17 / 10) = 10 ^ (−1,7) ≈ 0,02 mW = 20 µW

Control, en mW multiplicando factores:
  10 mW × 10 (ampli) × 10 ^ (−37/10) (pérdidas) = 100 × 0,0002 = 0,02 mW ✓
```

### 3. Ejercicio guiado (1er parcial, Temas 1 a 4 (2020), Tema 1, Ej 1)

> Hallar la **longitud máxima** de un enlace de coaxil hecho con bobinas de 200 m. Hay conectores a la salida del Tx y a la entrada del Rx. Datos: Ptx = 10 mW, empalme = 1 dB, conector = 1 dB, FD = 4 dB, coaxil = 2 dB/100 m, sensibilidad del Rx = 31,62 µW.

Es del tipo 3: te dan la sensibilidad y hay que sacar la longitud. La idea es calcular el presupuesto, descontarle lo que se pierde sí o sí (conectores y FD) y ver cuántas bobinas entran con lo que sobra. Ojo: Srx está en µW.

```
Paso 1: pasar Ptx y Srx a dBm
  → ________

Paso 2: presupuesto de pérdidas (no hay amplificador)
  → ________

Paso 3: restar las pérdidas fijas (conectores y FD) y ver cuánto queda
  → ________

Paso 4: cuánto cuesta una bobina (cable + empalme) y cuántas entran
  → ________

Paso 5: longitud máxima
  → ________

Control: calculá cuánto llega con esa longitud y comparalo con Srx
  → ________
```

### 4. Práctica

#### Ejemplo resuelto 2: longitud máxima con amplificador (Final 27/09/2023)

> Ptx = 10 mW, Srx = −17 dBm, un amplificador x100, 4 conectores de 1 dB (Tx, Rx, entrada y salida del ampli), cable de 2 dB/km en bobinas de 5 km, empalmes de 1 dB. Hallar la longitud máxima.

Es del tipo 3, con amplificador: su ganancia se suma al presupuesto.

```
Paso 1: Ptx a dBm
  10 * log10(10) = 10 dBm

Paso 2: ganancias
  Amplificador x100  →  20 dB

Paso 3: presupuesto de pérdidas
  Ptx + Ganancias − Srx = 10 + 20 − (−17) = 47 dB

Paso 4: restar pérdidas fijas
  Conectores: 4 × 1 dB = 4 dB  →  quedan 47 − 4 = 43 dB para cable y empalmes

Paso 5: cuántas bobinas entran
  Cada bobina: 5 km × 2 dB/km = 10 dB de cable
  n bobinas cuestan: 10·n + 1·(n − 1)  (n − 1 empalmes)
  n = 4  →  40 + 3 = 43 dB  ✓ (justo, no sobra nada)

Paso 6: longitud máxima
  4 bobinas × 5 km = 20 km

Control: 10 + 20 − (4 + 40 + 3) = −17 dBm = Srx ✓
```

#### Ejemplo resuelto 3: atenuación por tabla (1er parcial 08/10/2024, Práctica 1)

> Enlace por cable coaxil RG 213/U de 300 m. Ptx = 150 W, frecuencia de operación 110 MHz, Srx = 2 mW. La atenuación sale de la tabla: 10 MHz → 2; 50 MHz → 4,9; 100 MHz → 7; 200 MHz → 10,5; 400 MHz → 15,5; 1000 MHz → 26 (en dB/100 m). ¿El receptor detecta la potencia que llega? ¿Cuántos mW llegan?

Es del tipo 4. La potencia está en W (hay que pasarla a mW), 110 MHz no está en la tabla (hay que interpolar) y no hay conectores, empalmes ni FD.

```
Paso 1: Ptx a dBm
  150 W = 150.000 mW  →  10 * log10(150.000) = 51,76 dBm

Paso 2: atenuación a 110 MHz (entre 100 y 200 MHz)
  De 7 a 10,5 dB/100 m sube 3,5 en 100 MHz  →  en 10 MHz sube 0,35
  7 + 0,35 = 7,35 dB/100 m

Paso 3: pérdida del cable
  300 m × 7,35 dB / 100 m = 22,05 dB

Paso 4: potencia que llega
  51,76 − 22,05 = 29,71 dBm  →  10 ^ 2,971 ≈ 935 mW

Paso 5: comparar con Srx
  Srx = 2 mW = 10 * log10(2) = 3,01 dBm
  29,71 dBm > 3,01 dBm  →  sí, lo detecta (sobran 26,7 dB)

Control, en W: 150 W × 10 ^ (−22,05/10) = 150 × 0,00624 = 0,935 W ✓
```

#### Ejemplo resuelto 4: cambio de impedancia (1er parcial 2020 2Q, Ej 1)

> Un equipo de radio se conecta a su antena con una línea coaxial de 50 m que atenúa 10 dB/100 m a 400 MHz. El transmisor entrega 50 W a 400 MHz y la antena es de 50 Ω. a) Calcular la potencia aplicada a la antena. b) ¿Cuál será la potencia si se cambia la antena por una de 75 Ω?

La parte a) es del tipo 4. La parte b) se resuelve con un criterio de la cátedra que no sale de la ecuación del enlace: la resolución publicada suma una corrección de $10\log_{10}(75/50)$ dB, "según se vio en teoría". Si te lo toman, resolvelo así.

```
Paso 1: Ptx a dBm
  50 W = 50.000 mW  →  10 * log10(50.000) = 46,99 dBm

Paso 2: pérdida del cable
  50 m × 10 dB / 100 m = 5 dB

Paso 3: a) potencia en la antena de 50 Ω
  46,99 − 5 = 41,99 dBm  →  10 ^ 4,199 ≈ 15.810 mW = 15,81 W

Paso 4: b) corrección por impedancia (criterio de la cátedra)
  10 * log10(75 / 50) = 1,76 dB
  41,99 + 1,76 = 43,75 dBm  →  ≈ 23,71 W

Control de a), en W: 50 W × 10 ^ (−5/10) = 50 × 0,316 = 15,81 W ✓
```

#### Ejercicio extra 1: sin conectores ni bobinas (material propio)

> Ptx = 20 mW, Srx = −20 dBm, atenuación = 3 dB/km, sin amplificadores ni conectores. Hallar la longitud máxima.

#### Ejercicio extra 2: potencia necesaria (1er parcial 2022, Ej 4)

> Enlace de fibra óptica monomodo de 10 km, con carretes de 400 m. Empalme mecánico = 0,5 dB, conector = 0,6 dB (uno en el Tx y otro en el Rx), atenuación de la fibra = 0,3 dB/km, Srx = −55 dBm, FD = 10 dB. Calcular la potencia necesaria en el transmisor, en mW.

#### Ejercicio extra 3: sensibilidad con amplificador (1er parcial, Temas 1 a 4 (2020), Tema 3, Ej 1)

> Enlace de fibra de 4 km armado con bobinas de 500 m. Un amplificador x10, con un conector a la entrada y otro a la salida; también hay conectores a la salida del Tx y a la entrada del Rx. Ptx = 1 mW, empalme = 1 dB, conector = 0,5 dB, FD = 3 dB, fibra = 2 dB/km. Hallar la sensibilidad del receptor en dBm y mW.

#### Ejercicio extra 4: longitud máxima con bobina cortada (1er parcial, Temas 1 a 4 (2020), Tema 4, Ej 3)

> Ptx = 0,010 W, cable = 0,5 dB/100 m, FD = 1 dB, conectores = 1 dB (uno en el Tx y otro en el Rx), empalmes = 1 dB, Srx = −10 dBm. Hay un amplificador que amplifica 10 veces y las bobinas son de 1 km. Hallar: a) Ptx en dBm; b) la longitud máxima; c) la cantidad de empalmes; d) Srx en watts.

#### Ejercicio extra 5: potencia necesaria con amplificador (1er parcial 28/09/2026, Tema B, Ej 5)

> ¿Qué potencia de transmisión (en dBm y mW) deberá tener un transmisor para establecer un enlace por una línea de 10.000 m, donde la atenuación del cable es de 2 dB/1000 m? La sensibilidad del receptor es 0,158 mW. Se usa un amplificador en la mitad del enlace que amplifica la potencia 100 veces; además se emplean dos conectores de 1 dB y un factor de diseño de 5 dB. La bobina del cable coaxil tiene 5 km, y la atenuación de cada empalme es 1 dB.

**Más práctica:** los ejercicios 1 y 3 a 9 de "2020 Primer Parcial" (ejercicios tipo parcial del Classroom) y la guía del TP 3.

### 5. Cierre

**Fórmulas**

$$\begin{aligned}
P_{\text{dBm}} &= 10\log_{10} P_{\text{mW}} \qquad\qquad P_{\text{mW}} = 10^{\,P_{\text{dBm}}/10} \\[4pt]
G_{\text{dB}} &= 10\log_{10}\frac{P_{sal}}{P_{ent}} \qquad \times 2 \to +3\ \text{dB} \quad \times 10 \to +10\ \text{dB} \quad \times 100 \to +20\ \text{dB} \\[4pt]
S_{rx} &= P_{tx} - \text{Pérdidas} + \text{Ganancias} \\[4pt]
\text{Pérdidas} &= \text{conectores} + L\cdot\alpha + (n-1)\cdot e + FD \\[4pt]
\text{Presupuesto} &= P_{tx} - S_{rx} + \text{Ganancias} \\[4pt]
a(f) &= a_1 + (a_2-a_1)\,\frac{f-f_1}{f_2-f_1}
\end{aligned}$$

$$1\ \text{mW} = 0\ \text{dBm} \qquad 10\ \text{mW} = 10\ \text{dBm} \qquad 1\ \text{W} = 30\ \text{dBm} \qquad 1\ \mu\text{W} = -30\ \text{dBm}$$

**Trampas**
- **Sumar dos potencias en dBm.** dBm + dBm no existe. A una potencia en dBm solo se le suman o restan dB.
- **Meter µW o W en la fórmula del dBm.** La fórmula pide mW: 31,62 µW son 0,03162 mW y 150 W son 150.000 mW.
- **Contar mal los conectores.** Van los que dice el enunciado: Tx y Rx siempre, y entrada y salida del amplificador solo si lo menciona.
- **Poner tantos empalmes como bobinas.** Con $n$ bobinas hay $n - 1$ empalmes.
- **Tomar el FD como ganancia.** Es un margen de seguridad y se suma a las pérdidas.
- **Dejar afuera la bobina cortada.** Si después de las bobinas enteras sobran dB, entra un pedazo más de cable.
- **Confundir dB/100 m con dB/km.** 2 dB/100 m son 20 dB/km.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué en el enlace se suman dB en vez de multiplicar potencias? ¿Y por qué no se pueden sumar dos potencias en dBm?
2. (Ejercicio) Enlace de fibra de 6 km con bobinas de 2 km. Empalmes de 0,5 dB, 2 conectores de 1 dB, FD = 3 dB, atenuación = 0,5 dB/km, Srx = −30 dBm. ¿Qué potencia mínima necesita el transmisor, en dBm y en mW? (material propio)

## 3.2 Interfaces de capa física ★★☆☆☆ (2 de 8)

Temas en Lumen: `u8-interfaces-capa-fisica`, `u8-norma-v-24-rs`, `u8-interfaces-rs-449-x`

Pregunta de teoría. Apareció en los dos parciales más recientes (2022 y 2024), y con la misma consigna.

### 1. Conceptos

**Dónde está la interfaz.** En el circuito teleinformático (capítulo 1), la interfaz digital (ID) es la conexión entre el ETD (la computadora, que genera o recibe los datos) y el ECD (el módem, que adapta la señal a la línea). Es la capa 1 del modelo OSI.

**Qué define una norma de interfaz.** Cuatro aspectos:
- **Mecánicos:** el conector, macho o hembra, y la cantidad de pines.
- **Eléctricos:** los niveles de tensión, y si la transmisión es desbalanceada (todos los circuitos vuelven por una tierra común) o balanceada (cada circuito tiene su propio retorno).
- **Funcionales o lógicos:** qué señal va por cada pin.
- **De procedimiento:** en qué orden se usan las señales.

Las normas que empiezan con V o con X son de la UIT-T. Las RS son de la EIA (EE.UU.).

**RS-232 / V.24.**
- Es una interfaz **serie**, entre ETD y ECD, de hasta **15 m** y **20 kbps**. Permite full duplex, con o sin sincronismo.
- **Mecánica:** conector **DB-25**, o **DB-9** cuando no se usan todas las señales.
- **Eléctrica**, según la cátedra. Ojo: el 0 es la tensión positiva y el 1, la negativa.
```
Transmisor:   0 → más de +5 V        1 → menos de −5 V
Receptor:     0 → más de +3 V        1 → menos de −3 V
Máximo: ±25 V.   Margen de 2 V, pensado para la caída de tensión en 15 m
```
- **Señales principales y su sentido.** El sentido sale de quién necesita avisar qué: la PC (ETD) manda los datos y pide permiso; el módem (ECD) recibe de la línea y avisa su estado.
```
Señal                               Sentido       Pin DB-25
TD   datos transmitidos             ETD → ECD     2
RD   datos recibidos                ECD → ETD     3
RTS  pedido de emisión              ETD → ECD     4
CTS  preparado para emitir          ECD → ETD     5
DSR  módem listo                    ECD → ETD     6
DTR  terminal lista                 ETD → ECD     20
DCD  detección de portadora         ECD → ETD     8
RI   indicador de llamada           ECD → ETD     22
     tierra de señalización         (común)       7
     tierra de protección           (común)       1
```
Los pines, salvo el 2, el 3 y el 7, son material propio: no están en el resumen de la cátedra.
- **Cable mínimo** entre una PC y un módem: TD (pin 2), RD (pin 3) y la tierra de señalización (pin 7).

**Otras interfaces** (según la tabla del resumen):
```
X.21      sincrónica, conector DB-15, 64 kbps
V.35      sincrónica, conector de 34 pines, 48 kbps
RS-449    pensada para reemplazar a la RS-232, hasta 2 Mbps
USB       bus serie universal para periféricos; versiones cada vez más rápidas (1.0 a 3.2)
```

**Los tipos de pregunta que toman:**
1. **Señales y sentido:** "¿Cuáles son las principales señales de la RS-232 / V.24? Indique el sentido de cada una" (2022 y 2024).
2. **Describir una interfaz** por sus aspectos: generalidades, mecánicos, eléctricos y funcionales.

### 2. Ejemplo resuelto (1er parcial 2022, Ej 2; 1er parcial 08/10/2024, Teoría 3)

> En la interfaz digital serie estándar RS-232 / V.24, ¿cuáles son las principales señales? Indique el sentido de las mismas: ETD → ECD o ECD → ETD.

El parcial 2022 pedía desarrollar cada respuesta en no menos de 15 renglones. Conviene arrancar ubicando la interfaz y después dar las señales agrupadas por función, cada una con su sentido.

```
Paso 1: ubicar la interfaz
  La RS-232 (EIA), equivalente a la V.24 (UIT-T), es la interfaz serie entre el ETD
  (computadora) y el ECD (módem). Define aspectos mecánicos, eléctricos y funcionales.

Paso 2: señales de datos
  TD, datos transmitidos: ETD → ECD (pin 2).
  RD, datos recibidos:    ECD → ETD (pin 3).

Paso 3: señales de control del diálogo
  RTS, pedido de emisión:      ETD → ECD. La PC avisa que quiere transmitir.
  CTS, preparado para emitir:  ECD → ETD. El módem le contesta que puede.

Paso 4: señales de estado
  DTR, terminal lista:  ETD → ECD.
  DSR, módem listo:     ECD → ETD.
  DCD, portadora detectada:  ECD → ETD. El módem recibe señal de la línea.
  RI, llamada entrante:      ECD → ETD.

Paso 5: tierras
  Tierra de señalización (pin 7): el retorno común de todos los circuitos.
  Tierra de protección: la del chasis.

Control: cada señal que "pide" o "manda datos" sale del ETD, y cada una que
"avisa un estado" del módem o de la línea sale del ECD ✓
```

### 3. Ejercicio guiado (pregunta tipo sobre la clase de capa física, material propio)

> Describir la interfaz RS-232 / V.24: generalidades, y aspectos mecánicos, eléctricos y funcionales.

Se arma por partes, una por cada aspecto que define una norma de interfaz.

```
Paso 1: generalidades (qué conecta, distancia, velocidad, modo)
  → ________

Paso 2: aspectos mecánicos
  → ________

Paso 3: aspectos eléctricos (niveles del Tx y del Rx, máximo, tipo de transmisión)
  → ________

Paso 4: aspectos funcionales (señales)
  → ________

Paso 5: cierre (cable mínimo PC-módem)
  → ________
```

### 4. Práctica

Intentá responder cada una en dos o tres líneas antes de mirar las respuestas.

1. ¿Qué cuatro aspectos define una norma de interfaz? Explicá cada uno.
2. ¿Qué diferencia hay entre una transmisión balanceada y una desbalanceada? ¿Cuál es la RS-232?
3. ¿Por qué el receptor RS-232 acepta ±3 V si el transmisor manda más de ±5 V?
4. ¿Qué organismo emite la V.24 y cuál la RS-232?
5. Compará X.21 y V.35: modo, conector y velocidad.

### 5. Cierre

**Fórmulas** (para memorizar)
```
RS-232 / V.24: serie, ETD ↔ ECD, hasta 15 m y 20 kbps, DB-25 o DB-9
Tx: 0 → > +5 V   1 → < −5 V        Rx: 0 → > +3 V   1 → < −3 V        máx ±25 V

ETD → ECD:  TD (2), RTS (4), DTR (20)
ECD → ETD:  RD (3), CTS (5), DSR (6), DCD (8), RI (22)
Tierra de señalización: pin 7.   Cable mínimo: 2, 3 y 7.
```

**Trampas**
- **Invertir el sentido de RTS y CTS.** RTS pide (sale de la PC) y CTS responde (sale del módem).
- **Confundir ETD con ECD.** El ETD es el terminal (la PC) y el ECD, el equipo de comunicación (el módem).
- **Decir que el 1 es la tensión positiva.** En RS-232 es al revés: el 1 es negativo.
- **Responder con una lista suelta.** Si piden desarrollar, agrupá las señales por función (datos, control, estado, tierras) y explicá cada grupo.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Qué cuatro aspectos define una norma de interfaz?
2. (Pregunta de parcial) Nombrá seis señales de la RS-232, con su sentido.

## Respuestas del capítulo 3

### 3.1 Ejercicio guiado

```
Paso 1: Ptx y Srx a dBm
  Ptx = 10 mW                  →  10 * log10(10)      =  10 dBm
  Srx = 31,62 µW = 0,03162 mW  →  10 * log10(0,03162) = −15 dBm
        (0,03162 = 10 ^ −1,5, así que el log da −1,5 y × 10 = −15)

Paso 2: presupuesto de pérdidas
  Ptx − Srx = 10 − (−15) = 25 dB

Paso 3: pérdidas fijas
  Conectores: Tx + Rx = 2 × 1 dB = 2 dB;  FD = 4 dB
  Quedan para cable y empalmes: 25 − 2 − 4 = 19 dB

Paso 4: bobinas
  Cable de una bobina: 200 m × (2 dB / 100 m) = 4 dB
  Con n bobinas se pierde: 4·n (cable) + 1·(n − 1) (empalmes) = 5·n − 1
  n = 4  →  5·4 − 1 = 19 dB  ✓ entra justo, no sobra nada para un pedazo más

Paso 5: longitud máxima
  4 bobinas × 200 m = 800 m

Control: 10 − (2 conectores + 16 cable + 3 empalmes + 4 FD) = 10 − 25 = −15 dBm = Srx ✓
```

### 3.1 Ejercicio extra 1

```
Ptx = 10 * log10(20) = 13 dBm
Presupuesto = 13 − (−20) = 33 dB
Longitud máxima = 33 dB / 3 dB/km = 11 km

Control: 13 − 11 × 3 = −20 dBm = Srx ✓
```

### 3.1 Ejercicio extra 2

```
Conectores: 2 × 0,6              =  1,2 dB
Carretes: 10.000 / 400 = 25  →  24 empalmes × 0,5  = 12 dB
Fibra: 10 km × 0,3 dB/km         =  3 dB
FD                               = 10 dB
Pérdidas totales                 = 26,2 dB

Ptx = Srx + Pérdidas = −55 + 26,2 = −28,8 dBm
Ptx = 10 ^ (−2,88) ≈ 0,00132 mW = 1,32 µW

Control: −28,8 − 26,2 = −55 dBm = Srx ✓
```

### 3.1 Ejercicio extra 3

```
Ptx = 1 mW = 0 dBm.   Ganancia: x10 → 10 dB
Conectores: 4 × 0,5 dB           =  2 dB
Bobinas: 4.000 / 500 = 8  →  7 empalmes × 1 dB = 7 dB
Fibra: 4 km × 2 dB/km            =  8 dB
FD                               =  3 dB
Pérdidas totales                 = 20 dB

Srx = 0 − 20 + 10 = −10 dBm = 10 ^ (−1) mW = 0,1 mW

Control en mW: 1 × 10 × 10 ^ (−20/10) = 10 × 0,01 = 0,1 mW ✓
```

### 3.1 Ejercicio extra 4

```
a) Ptx = 0,010 W = 10 mW = 10 dBm

Presupuesto = Ptx − Srx + Ganancias = 10 − (−10) + 10 = 30 dB
Pérdidas fijas: 2 conectores × 1 dB + FD 1 dB = 3 dB  →  quedan 27 dB
Cada bobina de 1 km cuesta 5 dB de cable + 1 dB de empalme = 6 dB
27 / 6 = 4,5  →  4 bobinas enteras (24 dB) y sobran 3 dB
Con 3 dB entran 3 / 5 dB/km = 0,6 km más de cable

b) Longitud máxima = 4 km + 0,6 km = 4.600 m
c) Empalmes: 5 bobinas (4 enteras + la cortada) → 4 empalmes
d) Srx = −10 dBm = 0,1 mW = 0,0001 W = 10 ^ −4 W

Control: 10 + 10 − (2 + 1 + 4,6 × 5 + 4) = 20 − 30 = −10 dBm = Srx ✓
```

### 3.1 Ejercicio extra 5

```
Srx = 0,158 mW  →  10 * log10(0,158) = −8,01 dBm
Ganancia: x100 → 20 dB
Conectores: 2 × 1 dB (el enunciado dice dos: Tx y Rx)  =  2 dB
Bobinas: 10 km / 5 km = 2  →  1 empalme × 1 dB          =  1 dB
Cable: 10 km × 2 dB/km                                  = 20 dB
FD                                                      =  5 dB
Pérdidas totales                                        = 28 dB

Ptx = Srx + Pérdidas − Ganancias = −8,01 + 28 − 20 ≈ 0 dBm = 1 mW

Control: 0 − 28 + 20 = −8 dBm ≈ 0,158 mW = Srx ✓
(Que dé 1 mW redondo confirma que se cuenta 1 empalme, aunque el amplificador
esté justo donde se unen las dos bobinas).
```

### 3.1 Autoevaluación

```
1. Cada elemento multiplica la potencia por un factor. El logaritmo de un producto
   es la suma de los logaritmos, así que en dB los factores se suman. Dos potencias
   en dBm no se suman porque sumar dB es multiplicar, y dos potencias no se
   multiplican entre sí: 10 mW + 10 mW = 20 mW = 13 dBm, no 20 dBm.

2. Conectores 2 dB + empalmes (3 bobinas → 2 × 0,5) 1 dB + fibra 6 × 0,5 = 3 dB
   + FD 3 dB = 9 dB de pérdidas.
   Ptx = Srx + Pérdidas = −30 + 9 = −21 dBm = 10 ^ (−2,1) ≈ 0,0079 mW ≈ 7,9 µW
```

### 3.2 Ejercicio guiado

```
Paso 1: generalidades
  Interfaz serie, entre un ETD (computadora) y un ECD (módem). Hasta 15 m y 20 kbps.
  Full duplex, con o sin sincronismo. Es la misma norma que la V.24 de la UIT-T.

Paso 2: aspectos mecánicos
  Conector DB-25 (25 pines); también se usa el DB-9 cuando no hacen falta todas las señales.

Paso 3: aspectos eléctricos
  Transmisor: 0 → más de +5 V; 1 → menos de −5 V.
  Receptor:   0 → más de +3 V; 1 → menos de −3 V.
  Máximo ±25 V. El margen de 2 V cubre la caída de tensión en los 15 m.
  Transmisión desbalanceada: todos los circuitos vuelven por la tierra de señalización.

Paso 4: aspectos funcionales (señales)
  TD / RD: datos transmitidos y recibidos.
  RTS → / ← CTS: la PC pide transmitir y el módem le contesta que puede.
  DTR / DSR: terminal lista / módem listo.
  DCD: el módem detectó portadora.    RI: el módem detectó una llamada.
  Tierra de protección y tierra de señalización.

Paso 5: cierre
  Cable mínimo PC-módem: TD (pin 2), RD (pin 3) y tierra de señalización (pin 7).
```

### 3.2 Práctica

```
1. Mecánicos (conector y pines), eléctricos (niveles de tensión, balanceada o no),
   funcionales (qué señal va por cada pin) y de procedimiento (en qué orden se usan).
2. Desbalanceada: todos los circuitos comparten un retorno común (la tierra).
   Balanceada: cada circuito tiene su propio retorno, y resiste mejor el ruido.
   La RS-232 es desbalanceada.
3. Por la caída de tensión en el cable: el margen de 2 V asegura que, después de
   15 m, el receptor siga distinguiendo el 0 del 1.
4. La V.24 es de la UIT-T; la RS-232, de la EIA (EE.UU.).
5. Las dos son sincrónicas. X.21: conector DB-15, 64 kbps. V.35: conector de 34
   pines, 48 kbps.
```

### 3.2 Autoevaluación

```
1. Mecánicos, eléctricos, funcionales y de procedimiento (ver práctica 1).
2. Cualquier seis de: TD (ETD → ECD), RD (ECD → ETD), RTS (ETD → ECD),
   CTS (ECD → ETD), DTR (ETD → ECD), DSR (ECD → ETD), DCD (ECD → ETD),
   RI (ECD → ETD).
```
