# Repaso urgente — 1er parcial (mañana 19hs, Argentina)

## ESTADO ACTUAL / DÓNDE RETOMAR

> Si sos Claude leyendo esto al empezar una sesión nueva: el estudiante tiene el **1er parcial de Comunicación de Datos el 28/09/2026 a las 19:00**. El plan original (arrancar 27/09 19:30) se cayó por un imprevisto; **se replanificó y se arrancó de cero el 27/09 a las 23:40**. Seguí el horario de abajo y retomá donde quedó marcado, sin repetir teoría ya vista. Sin símbolos LaTeX ($), todo en texto plano (consola). Ir bloque a bloque, con ejercicios guiados paso a paso, actualizando los trackers.

- **Hora del parcial:** 28/09/2026 19:00 (hora Argentina).
- **Bloque en curso:** A — Cálculo de enlace. Formato por bloque: conceptos teóricos → ejemplo resuelto → ejercicio guiado por partes (el estudiante no vio nada de la materia; no hacer diagnóstico).
- **Cómo escribir cada bloque en este archivo:** igual que el Bloque A. Subsecciones `### 1. Conceptos`, `### 2. Ejemplo resuelto`, `### 3. Ejercicio guiado` (y `### 4. Práctica extra` si hay); cada concepto arranca con su nombre en negrita; fórmulas y tablas de valores en bloques de código; ejemplos y ejercicios por pasos numerados dentro de un bloque de código; resoluciones en un `<details>` al final. Guardá la teoría acá apenas la des en el chat, así no se pierde si se cierra la sesión.
- **Punto exacto donde quedó:** A, ejercicio guiado (1er parcial Tema 1 Ej 1, longitud máxima coaxil 200 m), Paso 1: pasar Ptx y Srx a dBm.
- **Trackers de avance (bloques A–G):** 0/7

### Qué entra y por qué este orden

Alcance según la planificación de la cátedra (2024, curso K4152; confirmar que 2026 es igual): el 1er parcial entra hasta el **TP 6 inclusive**, y es de **problemas + puntos teóricos a desarrollar**. Teoría dada antes del parcial: intro a teleinformática, OSI e Internet; señales, FRP, velocidades, multinivel, sincrónica/asincrónica, tipos y modos de transmisión, Fourier; enlaces, dB/dBm, códigos banda base, tasa de información; canales (atenuación, ruido, distorsión), Nyquist, Shannon; detección y corrección de errores; capa física (RS-232, V.35, X.21, USB); medios de cobre. Modulación, PCM, multiplexación y PDH/SDH van al 2do parcial.

Los 1eros parciales viejos (Temas 1 a 4, `[CP-TIPO-PARCIAL]`, `[CP-ARROYO-PF]`) traen 4 problemas:

| Bloque | Tema | Aparece |
|:-:|---|---|
| A | Cálculo de enlace (longitud máxima o sensibilidad; bobinas, empalmes, conectores, factor de diseño, amplificador; cambio de impedancia) | en todos, siempre es el ejercicio 1 |
| B | Velocidades: FRP, Vm (baudios), Vt (bps), multinivel, tiempo de transmisión, sincrónica/asincrónica, rendimiento | en casi todos |
| C | Capacidad: Nyquist, Shannon, S/N en dB, tasa de información de imágenes (píxeles, niveles, compresión) | en casi todos |
| D | Fourier del tren de pulsos: Cn, f0, cantidad de armónicas, ancho de banda | 2 de 4 temas |
| E | Errores: CRC, checksum, paridad, Hamming | 2 de 4 temas |
| F | Códigos banda base: Manchester, Manchester diferencial, HDB3 (dibujar) | parcial 2020 |
| G | Teoría a desarrollar: OSI/Internet, modos de transmisión, ruido/distorsión, interfaces de capa física | según planificación |

A → B → C van de noche porque son cuentas encadenadas (C usa B). D es el más conceptual: mejor descansado. G es memorístico: después de comer.

## Horario (replanificado 27/09 23:40)

```
23:45–00:30  A  Cálculo de enlace
00:30–01:45  B  Velocidades, multinivel, sincrónica/asincrónica
01:45–02:00     Pausa
02:00–03:15  C  Capacidad (Nyquist/Shannon) + tasa de información
03:15–03:30     Cierre: hoja de fórmulas A-C
03:30–08:00     Dormir (4h30 = 3 ciclos; no bajar de acá)
08:15–09:00     Repaso: un ejercicio de A, B y C sin mirar
09:00–10:15  D  Fourier: Cn, armónicas, ancho de banda
10:15–11:30  E  Errores: CRC, checksum, paridad, Hamming
11:30–12:15  F  Códigos banda base
12:15–13:00     Comer
13:00–14:00  G  Teoría a desarrollar
14:00–16:30     Simulacro: un 1er parcial completo + 1 pregunta teórica, cronometrado
16:30–17:30     Corrección + completar hoja de fórmulas
17:30–18:00     Colchón / último vistazo a la hoja
18:00–19:00     Viaje al parcial
```

## Bloque A: Cálculo de enlace

### 1. Conceptos

**Qué es un enlace.** Un transmisor (Tx) manda una señal por un medio (cable coaxil, fibra) hasta un receptor (Rx). En el camino la señal pierde potencia: la atenúa el cable y la debilitan los conectores y los empalmes. El enlace funciona si al receptor le llega suficiente potencia.

**Potencia de transmisión (Ptx).** Es la potencia con la que el Tx manda la señal al enlace, antes de las pérdidas.

**Sensibilidad del receptor (Srx).** Es la potencia mínima que el receptor puede detectar. Si llega menos, no entiende la señal.

**El decibel (dB).** Mide una relación entre dos potencias, no una potencia en sí:
```
G(dB) = 10 * log10(P_salida / P_entrada)
```
Sirve para expresar ganancias y pérdidas. Conviene memorizar estos valores:
```
x2    →  +3 dB        /2    →  -3 dB
x10   → +10 dB        /10   → -10 dB
x100  → +20 dB        /100  → -20 dB
```
Por ejemplo, "un amplificador que amplifica 10 veces" es una ganancia de 10 dB.

**El dBm.** Es una potencia absoluta, medida contra 1 mW:
```
P(dBm) = 10 * log10(P en mW / 1 mW)
P(mW)  = 10 ^ (P(dBm) / 10)          ← para volver a mW
```
```
1 mW = 0 dBm     10 mW = 10 dBm     100 mW = 20 dBm     1 W = 30 dBm
0,1 mW = -10 dBm     0,01 mW = -20 dBm     1 µW = 0,001 mW = -30 dBm
```
Antes de meter un dato en la fórmula, pasalo a mW: 10.000 µW son 10 mW y 50 W son 50.000 mW.

**Por qué se suma en vez de multiplicar.** Cada elemento multiplica la potencia: el cable la multiplica por 0,1 y el amplificador por 10. El logaritmo convierte esas multiplicaciones en sumas: log(a·b) = log a + log b. Entonces:
- dBm ± dB da dBm (una potencia a la que le sumás o restás ganancias o pérdidas).
- dBm + dBm no tiene sentido. Nunca sumes dos potencias en dBm.

**Qué pierde potencia en el enlace:**
- **Conectores**: van a la salida del Tx, a la entrada del Rx y a la entrada y salida de cada amplificador. Contalos bien, porque es el error más común.
- **Cable**: la pérdida depende de la longitud (ej. 2 dB/100 m). Pérdida = longitud × atenuación.
- **Bobinas y empalmes**: el cable viene en bobinas de largo fijo, y entre bobina y bobina hay un empalme. Con n bobinas hay **n − 1 empalmes**.
- **Factor de diseño (FD)**: margen de seguridad en dB. Se suma como si fuera una pérdida más.

**Qué agrega potencia:** los amplificadores, con su ganancia en dB.

**La ecuación del enlace** (la única que necesitás):
```
Ptx(dBm) − Pérdidas totales(dB) + Ganancias(dB) = Srx(dBm)

Pérdidas totales = conectores + cable + empalmes + factor de diseño
```

**Los dos tipos de ejercicio que toman:**
1. **Te dan la longitud y piden la sensibilidad**: calculás las pérdidas y despejás Srx.
2. **Te dan la sensibilidad y piden la longitud máxima**: calculás cuántos dB te quedan para el cable y los empalmes, y de ahí cuántas bobinas entran. La longitud máxima es aquella en la que la potencia llega justo igual a Srx.

### 2. Ejemplo resuelto (1er parcial, Tema 2, Ejercicio 1)

> Hallar la sensibilidad del receptor en dBm y mW. Enlace de 1200 m con bobinas de coaxil de 200 m. Un amplificador eleva la potencia 10 veces. Hay conectores en la entrada y la salida del amplificador, a la salida del Tx y a la entrada del Rx. Datos: Ptx = 10.000 µW, empalme = 1 dB, conector = 1 dB, FD = 4 dB, coaxil = 2 dB/100 m.

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
```

### 3. Ejercicio guiado (1er parcial, Tema 1, Ejercicio 1)

> Hallar la **longitud máxima** de un enlace de coaxil hecho con bobinas de 200 m. Hay conectores a la salida del Tx y a la entrada del Rx. Datos: Ptx = 10 mW, empalme = 1 dB, conector = 1 dB, FD = 4 dB, coaxil = 2 dB/100 m, sensibilidad del Rx = 31,62 µW.

Es del tipo 2: te dan la sensibilidad y hay que sacar la longitud. Vamos paso a paso.

```
Paso 1: pasar Ptx y Srx a dBm (ojo: Srx está en µW, primero llevala a mW)   ← ACÁ QUEDAMOS
Paso 2: presupuesto de pérdidas = Ptx − Srx
Paso 3: restar las pérdidas fijas (conectores + FD) → lo que queda para cable y empalmes
Paso 4: ver cuántas bobinas entran (cada bobina suma su cable, y entre bobinas va un empalme)
Paso 5: longitud máxima = bobinas × 200 m
```

### 4. Práctica extra

#### Ejemplo resuelto 2: longitud máxima con amplificador (Final 27/09/23)

> Ptx = 10 mW, Srx = −17 dBm, un amplificador x100, 4 conectores de 1 dB (Tx, Rx, entrada y salida del ampli), cable de 2 dB/km en bobinas de 5 km, empalmes de 1 dB. Hallar la longitud máxima.

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
  n = 4  →  40 + 3 = 43 dB  ✓ (justo)

Paso 6: longitud máxima
  4 bobinas × 5 km = 20 km
```

#### Ejercicio extra: sin conectores ni bobinas

> Ptx = 20 mW, Srx = −20 dBm, atenuación = 3 dB/km, sin amplificadores ni conectores. Hallar la longitud máxima.

```
Paso 1: Ptx a dBm = 10 * log10(20) = 13 dBm   [hecho]
Paso 2: presupuesto de pérdidas = Ptx − Srx = ¿?
Paso 3: longitud máxima = presupuesto / atenuación por km = ¿?
```

<details>
<summary>Resoluciones (mirá solo después de intentarlo)</summary>

```
Ejercicio guiado:
  Ptx = 10 dBm;  Srx = 31,62 µW = 0,03162 mW → 10 * log10(0,03162) = −15 dBm
  Presupuesto = 10 − (−15) = 25 dB
  Fijas: 2 conectores + FD = 2 + 4 = 6 dB  →  quedan 19 dB
  Bobina de 200 m = 4 dB;  n bobinas: 4·n + (n − 1) = 5·n − 1
  n = 4 → 19 dB ✓  →  longitud máxima = 4 × 200 m = 800 m

Ejercicio extra:
  Presupuesto = 13 − (−20) = 33 dB  →  33 / 3 = 11 km
```

</details>
