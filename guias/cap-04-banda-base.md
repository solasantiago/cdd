# Capítulo 4: Banda base y tasa de información (TP 4)

## 4.1 Códigos banda base ★★☆☆☆ (2 de 8) 📌

Temas en Lumen: `u2-transmision-banda-base`, `u2-codigos-banda-base-normalizados`

Apareció en el parcial 2020 2Q y en 2026. En 2026 fue un problema de 2 puntos: dibujar Manchester y Manchester diferencial, y explicar qué facilidades dan y por qué.

### 1. Conceptos

**Transmisión en banda base.** Es mandar la señal digital tal cual por el medio, como niveles de tensión, sin modularla sobre una portadora. Se usa en distancias cortas y en redes LAN, y es barata porque no hay que modular. La otra opción es la transmisión modulada, con una portadora (como un módem sobre la línea telefónica), que entra en el 2do parcial. El equipo que adapta la señal a la línea sin modular es el **módem banda base**: pasa los bits a un **código de línea**.

**Qué se le pide a un código de línea.**
- **Que no tenga componente continua:** que el valor medio de la señal sea 0. Si tiene continua, desperdicia potencia y no pasa por transformadores.
- **Que sea autosincronizante:** que tenga transiciones seguido, así el receptor saca el reloj de la propia señal. En una racha larga de bits iguales, sin transiciones, el receptor pierde la cuenta de los bits.
- **Que no pida mucho ancho de banda:** pulsos más cortos, o más cambios por bit, piden más ancho de banda (bloque 2.2).

**Los códigos básicos.**
```
Unipolar NRZ:    1 → +V todo el bit                      0 → 0 V
Polar NRZ:       1 → +V todo el bit                      0 → −V todo el bit
Unipolar RZ:     1 → +V la mitad del bit y vuelve a 0    0 → 0 V
Polar RZ:        1 → +V la mitad del bit                 0 → −V la mitad del bit
                 (siempre vuelve a 0)
Bipolar (AMI):   0 → 0 V                                 1 → alterna: +V, −V, +V, −V...
Bipolar RZ:      como AMI, pero los pulsos duran la mitad del bit
```

**Cómo se comparan** (resumido del resumen de la cátedra):

| Código | Sincronismo | Ancho de banda |
|---|---|---|
| Unipolar y polar NRZ | Malo: con rachas de 1 o de 0 no hay transiciones | El menor |
| Unipolar RZ | Con los 1 sí, con rachas de 0 no | Mayor que NRZ |
| Polar RZ | Con los 1 y con los 0: es autosincronizante | Mayor que NRZ |
| AMI (bipolar NRZ) | Con los 1 sí, con rachas de 0 no (lo arregla HDB3) | Bajo, similar a NRZ |
| Bipolar RZ | Igual que AMI | Mayor que AMI |
| Manchester y Manchester diferencial | Autosincronizantes: transición en todos los bits | El doble que NRZ |

La componente continua: los unipolares la tienen siempre. AMI no la tiene, porque los unos alternan y se compensan. Manchester tampoco, porque cada bit pasa media celda arriba y media abajo.

**HDB3.** Arregla el problema de AMI con las rachas de ceros. Es AMI, pero cada grupo de **4 ceros seguidos** se reemplaza por una de estas dos secuencias:
```
000V   → si desde la última violación hubo una cantidad IMPAR de unos
R00V   → si hubo una cantidad PAR de unos (cero unos cuenta como par)

V (violación): pulso con la MISMA polaridad que el pulso anterior. Rompe la alternancia
               a propósito, y así el receptor sabe que no es un 1 de verdad.
R (relleno):   pulso que SÍ respeta la alternancia. V va con la misma polaridad que R.

Las violaciones van alternando entre sí (+, −, +...), así no se acumula continua.
Después de una V, el siguiente 1 alterna respecto de esa V.
Antes de la primera violación, se cuentan los unos desde el principio de la secuencia.
```

**Manchester (bifase).** Siempre hay una transición en la **mitad** de cada bit, y esa transición es el dato. Según la cátedra:
```
1 → transición ascendente en la mitad: primera mitad en −V, segunda en +V   (↑)
0 → transición descendente en la mitad: primera mitad en +V, segunda en −V  (↓)
```
Si vienen dos bits iguales seguidos, en el borde entre ellos hay un salto extra para poder repetir la transición. Como cada bit pasa media celda en +V y media en −V, **la componente continua siempre es nula** (en el TP 4 piden demostrarlo; la demostración es esta).

**Manchester diferencial.** También hay transición en la mitad de **todos** los bits, pero no importa si sube o si baja. El dato está en el **inicio** del bit:
```
0 → hay transición al inicio del bit (además de la del medio)
1 → no hay transición al inicio: arranca en el nivel donde terminó el bit anterior
```
Como cada bit depende del anterior, para dibujarlo hay que suponer un nivel de arranque.

**Qué facilidades dan Manchester y Manchester diferencial, y por qué.** Es la segunda parte del ejercicio 7 de 2026:
1. **Sincronismo:** hay una transición en la mitad de cada bit, así que el receptor saca el reloj de la propia señal, aunque vengan rachas largas de unos o de ceros.
2. **Sin componente continua:** cada bit pasa media celda en +V y media en −V, así que el valor medio es 0. No desperdicia potencia y pasa por transformadores.
3. **Detección de errores:** si en la mitad de un bit falta la transición, el receptor sabe que hubo un error.
4. **Manchester diferencial, además:** el dato está en si hay o no transición al inicio, no en si sube o baja. Por eso, si se invierten los cables (la polaridad), se sigue leyendo bien.

El costo: como la señal cambia hasta dos veces por bit, pide **el doble de ancho de banda** que NRZ.

**Cómo dibujarlos en el parcial.**
1. Marcá la celda de cada bit con rayitas verticales y escribí el bit arriba.
2. Manchester: en la mitad de cada celda dibujá la flecha (↑ para 1, ↓ para 0). Después uní: si dos flechas seguidas terminan y arrancan en niveles distintos, poné un salto en el borde.
3. Manchester diferencial: en cada borde decidí si hay salto (0) o no (1), y después poné siempre el salto del medio.
4. AMI y HDB3: primero escribí arriba de cada bit el símbolo (+, −, 0, V, R), y recién después dibujá.

**Los tipos de ejercicio que toman:**
1. **Dibujar** una secuencia con Manchester, Manchester diferencial, AMI o HDB3 (2020 2Q, 2026, TP 4).
2. **Teoría:** qué facilidades da cada código y por qué (componente continua, sincronismo, ancho de banda), para qué sirve HDB3 y qué es la transmisión en banda base.

### 2. Ejemplo resuelto (1er parcial 2020 2Q, Ej 2, Manchester)

> Representar la señal con el código Manchester para la secuencia: 1010 1111 0000 1111 0000 0000.

Se aplica la regla bit por bit: el 1 sube en la mitad y el 0 baja en la mitad. En los dibujos, cada celda entre rayitas es un bit.

```
Paso 1: flecha de cada bit (1 → ↑, 0 → ↓)
  1 0 1 0   1 1 1 1   0 0 0 0   1 1 1 1   0 0 0 0   0 0 0 0
  ↑ ↓ ↑ ↓   ↑ ↑ ↑ ↑   ↓ ↓ ↓ ↓   ↑ ↑ ↑ ↑   ↓ ↓ ↓ ↓   ↓ ↓ ↓ ↓

Paso 2: bordes
  Entre un 1 y un 0 (o un 0 y un 1): no hay salto,
  porque uno termina donde arranca el otro.
  Entre dos bits iguales: hay salto en el borde, para poder repetir la transición.

Paso 3: dibujo, bits 1 a 12
          1     0     1     0     1     1     1     1     0     0     0     0
   +V     ┌─────┐     ┌─────┐     ┌──┐  ┌──┐  ┌──┐  ┌─────┐  ┌──┐  ┌──┐  ┌──┐
    0     │     │     │     │     │  │  │  │  │  │  │     │  │  │  │  │  │  │
   −V ────┘     └─────┘     └─────┘  └──┘  └──┘  └──┘     └──┘  └──┘  └──┘  └───
       |     |     |     |     |     |     |     |     |     |     |     |     |

        bits 13 a 24
          1     1     1     1     0     0     0     0     0     0     0     0
   +V     ┌──┐  ┌──┐  ┌──┐  ┌─────┐  ┌──┐  ┌──┐  ┌──┐  ┌──┐  ┌──┐  ┌──┐  ┌──┐
    0     │  │  │  │  │  │  │     │  │  │  │  │  │  │  │  │  │  │  │  │  │  │
   −V ────┘  └──┘  └──┘  └──┘     └──┘  └──┘  └──┘  └──┘  └──┘  └──┘  └──┘  └───
       |     |     |     |     |     |     |     |     |     |     |     |     |

Control: todos los bits tienen transición en la mitad; los 1 suben y los 0 bajan ✓
```

### 3. Ejercicio guiado (1er parcial 2020 2Q, Ej 2, Manchester diferencial)

> Representar la señal con Manchester diferencial para la secuencia: 0101 0101 0011 0011 0000 1111 0011 0011 0101.

Primero se decide, bit por bit, si hay salto al inicio (solo en los 0). Después se agrega siempre el salto del medio. Se supone que la línea viene en −V.

```
Paso 1: nivel de arranque (supuesto)
  → ________

Paso 2: ¿salto al inicio? Escribí S (sí) o − (no) debajo de cada bit
  bits:    0 1 0 1 0 1 0 1 0 0 1 1   0 0 1 1 0 0 0 0 1 1 1 1   0 0 1 1 0 0 1 1 0 1 0 1
  → ________

Paso 3: niveles de los primeros cuatro bits (primera mitad / segunda mitad)
  → ________

Paso 4: dibujo completo, en tres renglones de 12 bits
  → ________

Control: ¿todos los bits tienen salto en la mitad, y solo los 0 en el borde izquierdo?
  → ________
```

### 4. Práctica

#### Ejemplo resuelto 2: AMI y HDB3 (material propio)

> Codificar la secuencia 1 0000 11 0000 1 0000 con AMI y con HDB3.

Es de dibujo. Primero AMI (los unos alternan) y después HDB3 (se reemplazan los grupos de 4 ceros).

```
Paso 1: AMI: los 0 van en 0 V y los 1 alternan
  bits:  1 0 0 0 0 1 1 0 0 0 0 1 0 0 0 0
  AMI:   + 0 0 0 0 − + 0 0 0 0 − 0 0 0 0
          1     0     0     0     0     1     1     0
   +V ───────┐                             ┌─────┐
    0        └───────────────────────┐     │     └──────
   −V                                └─────┘
       |     |     |     |     |     |     |     |     |

          0     0     0     1     0     0     0     0
   +V
    0 ───────────────────┐     ┌────────────────────────
   −V                    └─────┘
       |     |     |     |     |     |     |     |     |

Paso 2: HDB3: buscar los grupos de 4 ceros y contar los unos desde la última violación
  Grupo 1 (bits 2 a 5):    antes hubo 1 uno (impar)             → 000V
  Grupo 2 (bits 8 a 11):   desde la última V hubo 2 unos (par)  → R00V
  Grupo 3 (bits 13 a 16):  desde la última V hubo 1 uno (impar) → 000V

Paso 3: polaridades
  bit 1 (1):       +
  bits 2 a 5:      0 0 0 V   → V igual al pulso anterior (+)   → 0 0 0 V+
  bit 6 (1):       alterna respecto de V+                      → −
  bit 7 (1):       +
  bits 8 a 11:     R 0 0 V   → R alterna (−) y V igual a R     → R− 0 0 V−
  bit 12 (1):      alterna respecto de V−                      → +
  bits 13 a 16:    0 0 0 V   → V igual al pulso anterior (+)   → 0 0 0 V+

  HDB3:  + 0 0 0 V+ − + R− 0 0 V− + 0 0 0 V+

Paso 4: dibujo HDB3
          1     0     0     0     0     1     1     0
   +V ───────┐                 ┌─────┐     ┌─────┐
    0        └─────────────────┘     │     │     │
   −V                                └─────┘     └──────
       |     |     |     |     |     |     |     |     |

          0     0     0     1     0     0     0     0
   +V                    ┌─────┐                 ┌──────
    0  ┌───────────┐     │     └─────────────────┘
   −V ─┘           └─────┘
       |     |     |     |     |     |     |     |     |

Control: las violaciones son +, −, + → alternan ✓
```

#### Ejercicio extra 1: Manchester y Manchester diferencial (TP 4, teoría, Ej 3)

> Dibujar la secuencia 0 1 1 0 0 1 1 0 1 1 1 1 1 0 0 0 0 con Manchester y con Manchester diferencial (arrancando desde −V).

#### Ejercicio extra 2: HDB3 (TP 4, teoría, Ej 5)

> Codificar con HDB3: 1 0 0 1 0 0 0 0 0 1 1 0 0 0 0 1 1 1 0 0 0 0 0 0 0 0 0 1 0 0 0 0 1 1

Ojo con la racha de 9 ceros: son 4 + 4 + 1.

#### Ejercicio extra 3: dibujo y facilidades (1er parcial 28/09/2026, Tema B, Ej 7)

> Dada la secuencia binaria 0100110, graficar el código Manchester y el Manchester diferencial, e indicar qué facilidades se obtienen con la utilización de dichos códigos banda base y por qué.

### 5. Cierre

**Fórmulas** (para memorizar)
```
Manchester:             1 → ↑ en la mitad (−V a +V)     0 → ↓ en la mitad (+V a −V)
Manchester diferencial: 0 → salto al inicio             1 → sin salto al inicio
                        (siempre hay salto en la mitad)
AMI:  0 → 0 V;  1 → alterna +V, −V
HDB3: 4 ceros → 000V (impar de unos desde la última V) o R00V (par)
      V = misma polaridad que el pulso anterior;  R respeta la alternancia
Facilidades de Manchester: sincronismo, sin continua, detecta errores; costo: doble ancho de banda
```

**Trampas**
- **Invertir la convención de Manchester.** Según la cátedra, el 1 sube en la mitad y el 0 baja. Escribila arriba del dibujo antes de empezar.
- **Olvidar el salto del borde entre dos bits iguales** en Manchester.
- **En Manchester diferencial, mirar si la transición sube o baja.** Lo que importa es si hay salto al inicio del bit.
- **En HDB3, contar los unos desde el principio en vez de desde la última violación.**
- **Dar las facilidades sin el porqué.** El ejercicio de 2026 pedía las dos cosas.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué Manchester no tiene componente continua y por qué es autosincronizante?
2. (Ejercicio) Dibujá 11001 en Manchester y en Manchester diferencial, arrancando desde −V. (material propio)

## 4.2 Información, entropía y tasa de información ★★★★☆ (5 de 8)

Temas en Lumen: `u5-medida-informacion`, `u5-entropia-tasa-informacion`

Aparece en casi todos los parciales, en dos formas: la tasa de una imagen o un video (2020, 2020 2Q, 2024) y la información y entropía de una fuente (2022). Cuando además piden la S/N o el ancho de banda del canal, se combina con Shannon (bloque 5.1).

### 1. Conceptos

**Cantidad de información.** Cuanto menos probable es un mensaje, más información da cuando llega. Un símbolo que tiene probabilidad p aporta:

$$I = \log_2 \frac{1}{p}\ [\text{Shannon}] \qquad\qquad \text{con } N \text{ símbolos equiprobables: } p = \frac{1}{N} \ \Rightarrow\ I = \log_2 N$$

Un Shannon es un bit de información. Por ejemplo, un píxel con 256 niveles de gris equiprobables aporta $\log_2 256 = 8$ Shannon. Un símbolo seguro ($p = 1$) aporta $\log_2 1 = 0$: por eso una fuente con un solo símbolo no es fuente de información. (La base del logaritmo da la unidad: en base 2 es el Shannon, en base 10 el Hartley y en base e el Nat).

**log2 con la calculadora.** Casi ninguna calculadora tiene log2, así que se hace con log10:

$$\log_2 x = \frac{\log_{10} x}{\log_{10} 2} = \frac{\log_{10} x}{0{,}301}$$

Por ejemplo, $\log_2 1001 = 3{,}0004 / 0{,}301 \approx 9{,}97 \approx 10$ (porque $2^{10} = 1024$). Para despejar al revés: si $\log_2 x = 8$, entonces $x = 2^8 = 256$.

**Entropía (H).** Es la información promedio que da cada símbolo de la fuente. Se pesa la información de cada símbolo por su probabilidad y se suma:

$$H = \sum_i p_i \cdot \log_2 \frac{1}{p_i}\ [\text{Shannon/símbolo}]$$

Es máxima cuando todos los símbolos son equiprobables, y ahí vale $H = \log_2 N$.

**Entropía de una fuente binaria.** Con dos símbolos de probabilidades $p$ y $1 - p$ (fuente de memoria nula: cada símbolo no depende de los anteriores):

$$H(p) = p \log_2 \frac{1}{p} + (1 - p) \log_2 \frac{1}{1 - p}$$

Vale 0 cuando $p = 0$ o $p = 1$ (la fuente es segura), y es máxima, 1 Shannon, cuando $p = 0{,}5$. El gráfico, que pidieron en 2022, es una campana simétrica:
```
 H(p) [Shannon]
  1 ┤            ● ● ●
    │        ●           ●
    │     ●                 ●
0,5 ┤   ●                     ●
    │  ●                       ●
    │ ●                         ●
  0 ●─────────────┬──────────────●──→ p
    0            0,5             1
```

**Tasa de información.** Es cuánta información por segundo genera la fuente, en bits por segundo:

$$R = H \cdot (\text{símbolos por segundo})\ [\text{bps}]$$

**Tasa de información de imágenes.** Cada píxel es un símbolo, y sus niveles de gris equiprobables dan $\log_2(\text{niveles})$ bits:
```
bits por píxel   = log2(niveles de gris)
bits por cuadro  = líneas × puntos por línea × bits por píxel
tasa  [bps]      = bits por cuadro × cuadros por segundo
```

**Compresión.** Si la imagen se comprime "al 50 %", la tasa queda en la mitad. En el parcial 2020, Tema 3, dice "nivel de compresión del 80 %", y las cuentas cierran quedándose con el 20 %: se saca lo que dice el porcentaje. Con 50 %, las dos lecturas dan lo mismo.

**Una imagen en palabras.** Si un texto se arma con palabras de un vocabulario de N palabras equiprobables, cada palabra aporta $\log_2 N$ bits. Para describir una imagen con palabras hacen falta tantas palabras como para juntar la misma información:

$$\text{palabras} = \frac{\text{información de la imagen}}{\log_2 N}$$

**Los tipos de ejercicio que toman:**
1. **Imágenes o video:** calculás la información por cuadro y la tasa. Si piden la S/N o el ancho de banda del canal, se sigue con Shannon (bloque 5.1).
2. **Información y entropía de una fuente:** con las probabilidades de cada símbolo, a veces sacadas de una secuencia.
3. **Teoría:** qué es la entropía y la tasa de información, y el gráfico de la entropía de una fuente binaria.

### 2. Ejemplo resuelto (1er parcial 2020 2Q, Ej 2)

> Se transmiten 15 imágenes de TV por segundo de 640 × 480 píxeles, donde cada punto tiene 256 niveles equiprobables de brillo. Calcular la velocidad del canal para enviar esta información.

Es del tipo 1. Los niveles equiprobables dan los bits por píxel, y los píxeles por imagen por las imágenes por segundo dan la tasa. No hay compresión.

```
Paso 1: información de un píxel
  256 niveles equiprobables  →  log2 256 = 8 Shannon

Paso 2: información de una imagen
  640 × 480 = 307.200 píxeles × 8 = 2.457.600 Shannon

Paso 3: tasa de información
  2.457.600 × 15 imágenes/s = 36.864.000 bps ≈ 36,86 Mbps

Control: 36.864.000 / 15 / 8 = 307.200 píxeles = 640 × 480 ✓
```

### 3. Ejercicio guiado (1er parcial 08/10/2024, Práctica 2)

> Una imagen tiene 800 líneas horizontales y 300 puntos discretos por línea, y cada punto tiene 16 niveles equiprobables de brillo. Se dispone de un vocabulario de 170.000 palabras equiprobables. Calcular la cantidad de palabras que serían necesarias para describir la imagen y la velocidad de transmisión de un enlace que permita transmitir un video compuesto por 300 imágenes en 10 minutos.

Es del tipo 1, con palabras. La imagen y la palabra se miden con la misma vara: la información en Shannon. El tiempo está en minutos: pasalo a segundos.

```
Paso 1: información de la imagen
  → ________

Paso 2: información de una palabra (usá log2 x = log10 x / 0,301)
  → ________

Paso 3: cantidad de palabras
  → ________

Paso 4: velocidad del enlace (300 imágenes en 10 minutos)
  → ________

Control: multiplicá las palabras por la información de cada una
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: información y entropía (1er parcial 2022, Ej 5; TP 4, Ej 2)

> Dado un tren de pulsos con la secuencia 010101000001, calcular la información suministrada por la aparición de un uno o de un cero, y la entropía de la fuente.

#### Ejercicio extra 2: teoría (1er parcial 2022, Ej 3)

> ¿Qué entiende por entropía y tasa de información? Grafique la entropía de una fuente binaria de memoria nula.

#### Ejercicio extra 3: tasa con compresión (material propio)

> Un video tiene 30 cuadros por segundo de 1000 × 800 píxeles, con 64 niveles de gris equiprobables, y se comprime al 75 % (queda el 25 %). Calcular la tasa de información antes y después de comprimir.

### 5. Cierre

**Fórmulas**

$$\begin{aligned}
I &= \log_2 \frac{1}{p} \qquad (N \text{ equiprobables: } I = \log_2 N) \qquad \log_2 x = \frac{\log_{10} x}{0{,}301} \\[4pt]
H &= \sum p_i \log_2 \frac{1}{p_i} \qquad H_{\text{máx}} = \log_2 N \qquad \text{binaria: máx } 1 \text{ en } p = 0{,}5 \\[4pt]
\text{tasa} &= \text{líneas} \times \text{puntos} \times \log_2(\text{niveles}) \times \text{cuadros/s} \qquad \text{palabras} = \frac{I_{\text{imagen}}}{\log_2 N}
\end{aligned}$$

**Trampas**
- **Usar la cantidad de niveles como bits.** 256 niveles son 8 bits, no 256.
- **Leer mal la compresión.** "Al 80 %" en el Tema 3 quiere decir que queda el 20 %.
- **Olvidar pasar minutos a segundos** en la tasa de un video.
- **Calcular la entropía sin pesar por la probabilidad.** H es un promedio: cada información va multiplicada por su p.
- **Graficar la entropía binaria con el máximo en otro lado.** Es 1 Shannon en $p = 0{,}5$, y 0 en los extremos.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué un símbolo seguro no aporta información? ¿Cuándo es máxima la entropía de una fuente?
2. (Ejercicio) Una fuente emite 4 símbolos con probabilidades 1/2, 1/4, 1/8 y 1/8. Calculá la información de cada uno y la entropía. (material propio)

## Respuestas del capítulo 4

### 4.1 Ejercicio guiado

```
Paso 1: nivel de arranque
  La línea viene en −V.

Paso 2: salto al inicio (0 → S, 1 → −)
  bits:    0 1 0 1 0 1 0 1 0 0 1 1   0 0 1 1 0 0 0 0 1 1 1 1   0 0 1 1 0 0 1 1 0 1 0 1
  inicio:  S − S − S − S − S S − −   S S − − S S S S − − − −   S S − − S S − − S − S −

Paso 3: niveles de los primeros bits (primera mitad / segunda mitad)
  bit 1 (0): salta de −V a +V; en la mitad baja         → +V / −V
  bit 2 (1): no salta, sigue en −V; en la mitad sube    → −V / +V
  bit 3 (0): salta de +V a −V; en la mitad sube         → −V / +V
  bit 4 (1): no salta, sigue en +V; en la mitad baja    → +V / −V

Paso 4: dibujo, bits 1 a 12, 13 a 24 y 25 a 36
          0     1     0     1     0     1     0     1     0     0     1     1
   +V  ┌──┐     ┌──┐  ┌─────┐  ┌──┐     ┌──┐  ┌─────┐  ┌──┐  ┌──┐     ┌─────┐
    0  │  │     │  │  │     │  │  │     │  │  │     │  │  │  │  │     │     │
   −V ─┘  └─────┘  └──┘     └──┘  └─────┘  └──┘     └──┘  └──┘  └─────┘     └───
       |     |     |     |     |     |     |     |     |     |     |     |     |

          0     0     1     1     0     0     0     0     1     1     1     1
   +V  ┌──┐  ┌──┐     ┌─────┐  ┌──┐  ┌──┐  ┌──┐  ┌──┐     ┌─────┐     ┌─────┐
    0  │  │  │  │     │     │  │  │  │  │  │  │  │  │     │     │     │     │
   −V ─┘  └──┘  └─────┘     └──┘  └──┘  └──┘  └──┘  └─────┘     └─────┘     └───
       |     |     |     |     |     |     |     |     |     |     |     |     |

          0     0     1     1     0     0     1     1     0     1     0     1
   +V  ┌──┐  ┌──┐     ┌─────┐  ┌──┐  ┌──┐     ┌─────┐  ┌──┐     ┌──┐  ┌─────┐
    0  │  │  │  │     │     │  │  │  │  │     │     │  │  │     │  │  │     │
   −V ─┘  └──┘  └─────┘     └──┘  └──┘  └─────┘     └──┘  └─────┘  └──┘     └───
       |     |     |     |     |     |     |     |     |     |     |     |     |

Control: todos los bits tienen salto en la mitad,
         y solo los 0 tienen salto en el borde izquierdo ✓
```

### 4.1 Ejercicio extra 1

```
Manchester:
          0     1     1     0     0     1     1     0     1
   +V ────┐     ┌──┐  ┌─────┐  ┌──┐     ┌──┐  ┌─────┐     ┌───
    0     │     │  │  │     │  │  │     │  │  │     │     │
   −V     └─────┘  └──┘     └──┘  └─────┘  └──┘     └─────┘
       |     |     |     |     |     |     |     |     |     |

          1     1     1     1     0     0     0     0
   +V ─┐  ┌──┐  ┌──┐  ┌──┐  ┌─────┐  ┌──┐  ┌──┐  ┌──┐
    0  │  │  │  │  │  │  │  │     │  │  │  │  │  │  │
   −V  └──┘  └──┘  └──┘  └──┘     └──┘  └──┘  └──┘  └───
       |     |     |     |     |     |     |     |     |

Manchester diferencial (arrancando desde −V):
          0     1     1     0     0     1     1     0     1
   +V  ┌──┐     ┌─────┐  ┌──┐  ┌──┐     ┌─────┐  ┌──┐     ┌───
    0  │  │     │     │  │  │  │  │     │     │  │  │     │
   −V ─┘  └─────┘     └──┘  └──┘  └─────┘     └──┘  └─────┘
       |     |     |     |     |     |     |     |     |     |

          1     1     1     1     0     0     0     0
   +V ────┐     ┌─────┐     ┌──┐  ┌──┐  ┌──┐  ┌──┐  ┌───
    0     │     │     │     │  │  │  │  │  │  │  │  │
   −V     └─────┘     └─────┘  └──┘  └──┘  └──┘  └──┘
       |     |     |     |     |     |     |     |     |
```

### 4.1 Ejercicio extra 2

```
Grupos: bits 5 a 8    (antes, 2 unos: par → R00V)
        bits 12 a 15  (2 unos desde la V: par → R00V)
        bits 19 a 22  (3 unos: impar → 000V)
        bits 23 a 26  (0 unos: par → R00V)
        bits 29 a 32  (1 uno: impar → 000V)
HDB3: + 0 0 − R+ 0 0 V+ 0 − + R− 0 0 V− + − + 0 0 0 V+ R− 0 0 V− 0 + 0 0 0 V+ − +
Violaciones: V+, V−, V+, V−, V+ → alternan ✓

Símbolos: + 0 0 − R+ 0 0 V+ 0 − + R−
          1     0     0     1     0     0     0     0     0     1     1     0
   +V ───────┐                 ┌─────┐           ┌─────┐           ┌─────┐
    0        └───────────┐     │     └───────────┘     └─────┐     │     │
   −V                    └─────┘                             └─────┘     └──────
       |     |     |     |     |     |     |     |     |     |     |     |     |

Símbolos: 0 0 V− + − + 0 0 0 V+ R− 0
          0     0     0     1     1     1     0     0     0     0     0     0
   +V                    ┌─────┐     ┌─────┐                 ┌─────┐
    0  ┌───────────┐     │     │     │     └─────────────────┘     │     ┌──────
   −V ─┘           └─────┘     └─────┘                             └─────┘
       |     |     |     |     |     |     |     |     |     |     |     |     |

Símbolos: 0 V− 0 + 0 0 0 V+ − +
          0     0     0     1     0     0     0     0     1     1
   +V                    ┌─────┐                 ┌─────┐     ┌──────
    0 ───────┐     ┌─────┘     └─────────────────┘     │     │
   −V        └─────┘                                   └─────┘
       |     |     |     |     |     |     |     |     |     |     |
```

### 4.1 Ejercicio extra 3

```
Manchester (1 → ↑, 0 → ↓):
         0     1     0     0     1     1     0
   +V  ───┐     ┌─────┐  ┌──┐     ┌──┐  ┌─────┐
    0     │     │     │  │  │     │  │  │     │
   −V     └─────┘     └──┘  └─────┘  └──┘     └──
       |     |     |     |     |     |     |     |

Manchester diferencial (la línea venía en −V: el primer 0 salta a +V al inicio):
         0     1     0     0     1     1     0
   +V  ───┐     ┌──┐  ┌──┐  ┌─────┐     ┌──┐  ┌──
    0     │     │  │  │  │  │     │     │  │  │
   −V     └─────┘  └──┘  └──┘     └─────┘  └──┘
       |     |     |     |     |     |     |     |
```

Facilidades y por qué:
1. **Sincronismo:** hay una transición en la mitad de cada bit, así que el receptor recupera el reloj de la señal aunque vengan rachas de bits iguales.
2. **Sin componente continua:** cada bit pasa media celda en +V y media en −V; el valor medio es 0, no se desperdicia potencia y la señal pasa por transformadores.
3. **Detección de errores:** si falta la transición del medio, el receptor sabe que hubo un error.
4. **Manchester diferencial, además:** como el dato está en si hay salto al inicio y no en el sentido del salto, no le afecta que se inviertan los cables.

El costo de las dos: el doble de ancho de banda que NRZ.

### 4.1 Autoevaluación

```
1. Sin continua: cada bit pasa media celda en +V y media en −V, así que el valor medio
   es 0. Autosincronizante: tiene transición en la mitad de todos los bits, y el
   receptor saca el reloj de ahí.

2. Manchester (1 ↑, 0 ↓): mitades  − + | − + | + − | + − | − +
   Manchester diferencial desde −V: mitades  − + | + − | + − | + − | − +
   (bit 1 = 1: sin salto al inicio; bit 2 = 1: sin salto; bits 3 y 4 = 0: saltan
   al inicio; bit 5 = 1: sin salto. Siempre hay salto en la mitad).
```

### 4.2 Ejercicio guiado

```
Paso 1: información de la imagen
  16 niveles equiprobables → log2 16 = 4 Shannon por punto
  800 × 300 = 240.000 puntos × 4 = 960.000 Shannon

Paso 2: información de una palabra
  log2 170.000 = log10 170.000 / log10 2 = 5,2304 / 0,30103 ≈ 17,375 Shannon

Paso 3: cantidad de palabras
  960.000 / 17,375 ≈ 55.251 palabras

Paso 4: velocidad del enlace
  300 imágenes × 960.000 bits = 288.000.000 bits
  10 minutos = 600 s   →   288.000.000 / 600 = 480.000 bps = 480 kbps

Control: 55.251 palabras × 17,375 Shannon ≈ 960.000 Shannon ✓
```

### 4.2 Ejercicio extra 1

```
8 ceros y 4 unos sobre 12   →   P(0) = 8/12 = 2/3    P(1) = 4/12 = 1/3
I(0) = log2(3/2) ≈ 0,585 Shannon      I(1) = log2(3) ≈ 1,585 Shannon
H = 2/3 × 0,585 + 1/3 × 1,585 ≈ 0,39 + 0,53 = 0,92 Shannon/símbolo

Control: H < 1, que es el máximo de una fuente binaria (con P = 0,5) ✓
```

### 4.2 Ejercicio extra 2

La **entropía** es la información promedio que entrega cada símbolo de una fuente: la información de cada símbolo, $\log_2(1/p)$, pesada por su probabilidad y sumada, $H = \sum p \log_2(1/p)$, en Shannon por símbolo. Es máxima cuando los símbolos son equiprobables. La **tasa de información** es la información que genera la fuente por segundo: la entropía por la cantidad de símbolos por segundo, en bps.

Para una fuente binaria de memoria nula, $H(p) = p \log_2(1/p) + (1-p)\log_2(1/(1-p))$: el gráfico es una campana simétrica que vale 0 en $p = 0$ y en $p = 1$ (la fuente es segura) y tiene su máximo, 1 Shannon, en $p = 0{,}5$ (ver el dibujo de los conceptos).

### 4.2 Ejercicio extra 3

```
Bits por píxel: log2 64 = 6
Tasa sin comprimir: 1000 × 800 × 6 × 30 = 144.000.000 bps = 144 Mbps
Comprimida al 75 % (queda el 25 %): 144 × 0,25 = 36 Mbps
```

### 4.2 Autoevaluación

```
1. Porque su probabilidad es 1 y log2(1/1) = 0: no dice nada que no se supiera.
   La entropía es máxima cuando todos los símbolos son equiprobables (H = log2 N).

2. I = log2(1/p):  1/2 → 1 Shannon;  1/4 → 2;  1/8 → 3;  1/8 → 3
   H = 1/2 × 1 + 1/4 × 2 + 1/8 × 3 + 1/8 × 3 = 0,5 + 0,5 + 0,375 + 0,375 = 1,75 Shannon/símbolo
   (menor que log2 4 = 2, porque no son equiprobables)
```
