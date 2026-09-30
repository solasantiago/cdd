# Capítulo 7: Medios físicos (TP 7)

## 7.1 Medios de cobre: par trenzado y coaxil ★★★☆☆ (2 de 4)

Temas en Lumen: `u7-par-trenzado-cableado-estructurado`, `u7-cables-multipares`, `u7-cable-coaxial`

Teoría. Apareció en los dos temas del 2do parcial 2020: las categorías del UTP y por qué es balanceado, y la impedancia característica del coaxil.

### 1. Conceptos

**Propiedades eléctricas de una línea.** Todo cable se comporta como un circuito con cuatro parámetros **primarios**, repartidos a lo largo de su longitud: la resistencia R y la inductancia L en serie, y la capacidad C y la conductancia G en paralelo, entre los conductores. De ellos salen los parámetros **secundarios**: la impedancia característica y la velocidad de propagación.

**Impedancia característica (Z0).** Es la relación entre la tensión aplicada y la corriente absorbida por un cable de **longitud infinita**. Un cable de longitud real, terminado en una carga igual a Z0, se comporta como si fuera infinito: toda la potencia llega a la carga. Si las impedancias del transmisor, del cable y del receptor no son iguales, parte de la señal se **refleja** y degrada la transmisión.

Z0 depende solo de la construcción del cable: el material, el dieléctrico que separa los conductores y los diámetros del conductor interior y exterior (eléctricamente, de R, L y C). **No depende de la longitud ni de la frecuencia de trabajo.** Los coaxiles típicos son de 50 Ω (datos y radio) y 75 Ω (TV).

**Frecuencia a la que la línea es resistiva.** La impedancia es $Z = R + j(X_L - X_C)$. Es puramente resistiva cuando $X_L = X_C$, o sea cuando $\omega L = 1/(\omega C)$:

$$f = \frac{1}{2\pi\sqrt{L \cdot C}}$$

**Velocidad de propagación.** Depende de la constante dieléctrica del aislante, y se da como porcentaje de la velocidad de la luz en el vacío.

**Par trenzado.** Cada circuito son dos conductores aislados y trenzados entre sí. Al trenzarlos, las interferencias externas inducen lo mismo en los dos hilos y se cancelan, y baja la diafonía con los pares vecinos. Los cables de datos tienen **4 pares** y hay tres tipos:
- **UTP** (unshielded twisted pair): sin blindaje.
- **FTP** (foiled twisted pair): una hoja de aluminio envuelve los cuatro pares, contra la interferencia externa.
- **STP** (shielded twisted pair): cada par tiene su blindaje, contra la interferencia de los otros pares.

**Línea balanceada.** En el par trenzado cada circuito tiene su par exclusivo: por un hilo va la señal y por el otro el retorno, en contrafase. La señal es la **diferencia de potencial entre los dos hilos** (transmisión diferencial), así que el ruido que entra igual en los dos se anula. En una línea **desbalanceada**, como el coaxil, el retorno es la malla, que se comparte con tierra.

**Categorías del UTP** (norma TIA; la ISO las llama clases). La categoría depende de las características eléctricas del cable (atenuación, capacidad, impedancia, diafonía), que fijan hasta qué frecuencia y velocidad funciona a una longitud dada:
```
Cat 1    telefonía analógica; no apto para datos (un par)
Cat 2    telefonía analógica y digital, hasta 4 Mbps
Cat 3    LAN Token Ring (4 Mbps) o Ethernet (10 Mbps)
Cat 4    Token Ring (16 Mbps) o Ethernet (10 Mbps)
Cat 5    Fast Ethernet (100 Mbps), 100 MHz
Cat 5e   algunas aplicaciones a 1 Gbps
Cat 6    diseñada para 1 Gbps; 6A, 7 y 7A para aplicaciones especiales
```

**Cables multipares.** Reúnen muchos pares (de 6 a 2200) con una cubierta y un código de colores para identificar cada par. Se usan para telefonía y datos, y los cables telefónicos responden bien en la banda vocal.

**Coaxil.** Dos conductores concéntricos: un conductor central, un aislante (dieléctrico), una malla (conductor exterior) y una cubierta. Se nombran con la norma MIL-C-17 como **RG-número/U** (por ejemplo, RG-213/U). Para elegir uno se miran tres parámetros: la impedancia característica, la frecuencia de trabajo y la atenuación máxima (en dB cada 100 m o por km, según la frecuencia; ver la tabla del bloque 3.1). Hoy se usa para conectar transmisores con su antena y para la TV por cable; en redes de datos y enlaces interurbanos lo reemplazaron el par trenzado y la fibra.

**Líneas abiertas y cables submarinos de cobre.** Las líneas abiertas (alambres desnudos en postes) se abandonaron por su costo de mantenimiento, su poco ancho de banda y el ruido que captan. Los cables submarinos de cobre (desde 1850) fueron reemplazados por los de fibra.

**Los tipos de pregunta que toman:**
1. **Teoría:** de qué depende la categoría del UTP, sus pares y por qué es balanceado; qué define la impedancia característica y si cambia con la frecuencia.
2. **Cálculo corto:** la frecuencia a la que una línea es resistiva, o la potencia que llega por un coaxil (bloque 3.1).

### 2. Ejemplo resuelto (2do parcial 2020, Tema 2, Ej 5)

> ¿De qué factor depende la categoría de un cable UTP? Indicar los pares que componen el cable, si son balanceados o desbalanceados, y por qué lo son.

Pide tres cosas: la categoría, los pares y el balanceo con su porqué.

```
Paso 1: de qué depende la categoría
  "De sus características eléctricas: atenuación, capacidad, impedancia y diafonía.
   Fijan hasta qué frecuencia y velocidad funciona el cable a una longitud máxima
   dada. Por ejemplo, Cat 5: 100 Mbps y 100 MHz; Cat 6: 1 Gbps."

Paso 2: los pares
  "Tiene 4 pares trenzados (8 hilos). En Fast Ethernet se usan 2 pares (uno para
   transmitir y otro para recibir); en Gigabit Ethernet, los 4."

Paso 3: balanceado, y por qué
  "Son balanceados: cada circuito tiene su par exclusivo, con la señal por un hilo y
   el retorno por el otro, en contrafase. La señal es la diferencia entre los dos
   hilos, así que el ruido que se induce igual en ambos se cancela; el trenzado
   refuerza esa cancelación."

Control: ¿están la categoría, los 4 pares y el porqué del balanceo? ✓
```

### 3. Ejercicio guiado (2do parcial 2020, Tema 1, Ej 2)

> ¿Cuáles son los factores que definen la impedancia característica en un cable coaxil? Al aumentar la frecuencia de trabajo, ¿aumenta la impedancia característica? ¿Por qué?

```
Paso 1: qué es la impedancia característica
  → ________

Paso 2: de qué depende (factores constructivos)
  → ________

Paso 3: ¿cambia con la frecuencia? ¿Por qué?
  → ________

Paso 4: por qué importa (adaptación de impedancias)
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: línea resistiva (TP 7, teoría, Ej 5)

> Dada una línea telefónica con L = 2 µH/km y C = 0,058 µF/km, ¿a qué frecuencia la impedancia es resistiva?

#### Ejercicio extra 2: teoría (TP 7, teoría, Ej 3)

> ¿Qué objetivo persigue la categorización de los cables UTP? ¿Qué categorías conoce? Mencione las principales características de cada una.

#### Ejercicio extra 3: teoría (material propio)

> Compará UTP, FTP y STP, y explicá por qué se trenzan los pares.

### 5. Cierre

**Fórmulas**

$$f_{\text{resistiva}} = \frac{1}{2\pi\sqrt{L C}} \qquad Z = R + j(X_L - X_C) \qquad X_L = \omega L, \quad X_C = \frac{1}{\omega C}$$

```
Z0: tensión / corriente en un cable infinito; depende de materiales, dieléctrico y
    diámetros; NO de la longitud ni de la frecuencia. Coaxil: 50 Ω (datos), 75 Ω (TV)
UTP: 4 pares, balanceado.  UTP sin blindaje / FTP aluminio general / STP cada par
Cat 5: 100 Mbps, 100 MHz.  Cat 5e y 6: 1 Gbps.   Coaxil: RG-número/U
```

**Trampas**
- **Decir que Z0 aumenta con la frecuencia o con la longitud.** Es una propiedad constructiva: no cambia. Lo que sí sube con la frecuencia es la atenuación.
- **Decir que el UTP es desbalanceado.** Es balanceado: cada circuito tiene su par. El desbalanceado es el coaxil.
- **Confundir FTP con STP.** FTP tiene una sola hoja para los cuatro pares; STP blinda cada par.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Qué es una línea balanceada y por qué rechaza el ruido?
2. (Ejercicio) Una línea tiene L = 0,5 mH/km y C = 50 nF/km. ¿A qué frecuencia es resistiva? (material propio)

## 7.2 Fibra óptica ★★★★☆ (3 de 4)

Temas en Lumen: `u7-fibra-optica-principios-tipos`, `u7-perdidas-fibras-opticas-sistemas`

Apareció en tres de los cuatro 2dos parciales relevados: las pérdidas en la fibra (2022), por qué usar la tercera ventana con láser (2020, Tema 1) y por qué no usar LED (2020, Tema 2).

### 1. Conceptos

**Qué es.** Un hilo de vidrio (silicio) muy fino que transporta luz infrarroja, no visible. Revolucionó las telecomunicaciones por su capacidad, que llega a varios Tbps. Se tiende en cables aéreos, subterráneos y submarinos, y llega hasta el hogar y el puesto de trabajo.

**Construcción.** Dos capas de silicio con distinto índice de refracción: el **núcleo** (core), que conduce la luz, y el **revestimiento** (cladding), más un recubrimiento plástico que la protege.
```
Recubrimiento: 245 µm      Revestimiento: 125 µm
Núcleo: 9 µm (monomodo)    50 o 62,5 µm (multimodo)
```

**Principio: reflexión total.** La luz entra al núcleo y rebota en la unión con el revestimiento, que tiene un índice de refracción menor. Si el ángulo es el adecuado, no sale: se refleja entera (ley de Snell, $n_1 \operatorname{sen}\theta_1 = n_2 \operatorname{sen}\theta_2$). El **cono de aceptación** agrupa las direcciones de entrada con reflexión total, y su ángulo es la **apertura** de la fibra.

**Tipos.**
- **Monomodo:** el núcleo es tan fino (unos 9 µm) que solo se propaga un modo (un camino). No hay dispersión modal: sirve para grandes distancias (cientos de km) y altas velocidades. Se usa con láser.
- **Multimodo:** núcleo más grueso; la luz va por muchos caminos. Hay dispersión modal. Distancias cortas (menos de 2 km); más fácil de conectar; se usa con LED. Puede ser de **índice escalón** (barata, poco ancho de banda) o de **índice gradual** (más cara, más ancho de banda).

**Ventanas.** La atenuación depende de la longitud de onda y es mínima en tres zonas, las ventanas:
```
1ª ventana: 850 nm      2ª ventana: 1310 nm      3ª ventana: 1550 nm (la de menor atenuación)
```
La frecuencia sale de $f = c / \lambda$, con $c = 3 \times 10^8$ m/s. Por ejemplo, 850 nm corresponden a $3 \times 10^8 / 850 \times 10^{-9} \approx 3{,}5 \times 10^{14}$ Hz.

**Pérdidas en la fibra.** Es la pregunta de 2022. Bajan la potencia de la luz; la atenuación típica es de 0,2 dB/km en monomodo y 0,4 dB/km en multimodo.
1. **Por absorción:** las impurezas que se agregan al silicio para lograr índices distintos absorben parte de la luz.
2. **Por dispersión de Rayleigh:** el silicio se trabaja en estado plástico y al solidificarse quedan irregularidades submicroscópicas que desvían la luz.
3. **Por curvaturas e imperfecciones:** dobleces y discontinuidades hacen que la luz se escape.
4. **Por dispersión modal** (multimodo): los modos recorren caminos distintos y llegan en tiempos distintos; el pulso se ensancha y baja su amplitud.
5. **Por dispersión cromática:** si el emisor no es monocromático, las distintas longitudes de onda viajan a distinta velocidad; el pulso se ensancha, aunque menos que con la modal.
6. **Por acoplamiento:** en las uniones transmisor-fibra, fibra-fibra y fibra-receptor. Empalme por fusión: 0,1 dB; empalme mecánico: 0,5 dB; conector: 0,5 dB.

**Ancho de banda.** La dispersión ensancha los pulsos y limita la velocidad. Por eso el ancho de banda de una fibra se da como producto **ancho de banda × distancia**, en GHz·km:

$$\Delta f_{\text{disponible}} = \frac{\text{ancho de banda [GHz·km]}}{\text{longitud [km]}}$$

**Emisores: LED y láser.**
- **LED:** emite varias longitudes de onda a la vez (luz no coherente, no monocromática). Por la dispersión cromática, los pulsos se ensanchan y pierden amplitud. Es barato y se usa en multimodo a distancias cortas.
- **Láser:** luz coherente y monocromática, más potencia y más confiable. Casi no tiene dispersión cromática. Se usa en monomodo, sobre todo en la tercera ventana, que tiene la menor atenuación: así se llega más lejos.

**Detectores.** Semiconductores con juntura P-N que generan una corriente proporcional a los fotones que reciben: el diodo **PIN**, el fotodiodo de avalancha **APD** (mucho más eficiente) y el **PIN/FET**.

**Enlace de fibra.** Se calcula con la misma ecuación del bloque 3.1: potencia del transmisor, menos conectores, fibra, empalmes y factor de diseño, igual a la sensibilidad del receptor.

**Cables submarinos de fibra.** Muchas fibras, capas de polietileno contra el agua, un tubo de cobre que alimenta los repetidores y alambres de acero para la resistencia mecánica. Tienen amplificadores cada 40 a 60 km.

**Los tipos de ejercicio que toman:**
1. **Teoría:** las pérdidas, los tipos de fibra, las ventanas, LED contra láser.
2. **Cálculo:** un enlace de fibra (potencia o sensibilidad) y el ancho de banda disponible; la frecuencia de una ventana.

### 2. Ejemplo resuelto (2do parcial 2022, Ej 3)

> Explique cuáles son las pérdidas en las fibras ópticas. (Desarrollar la respuesta en no menos de 15 renglones).

Conviene definir la atenuación, dar un orden de magnitud y después cada pérdida con su causa.

```
Paso 1: qué es la atenuación en la fibra
  "Es la pérdida de potencia óptica de la luz a lo largo de la fibra. Se mide en
   dB/km y depende de la longitud de onda: es mínima en las ventanas (850, 1310 y
   1550 nm). Valores típicos: 0,2 dB/km en monomodo y 0,4 dB/km en multimodo."

Paso 2: pérdidas propias del material
  Absorción: las impurezas agregadas para lograr índices distintos absorben luz.
  Rayleigh: irregularidades submicroscópicas del vidrio desvían la luz.

Paso 3: pérdidas por la instalación
  Curvaturas y dobleces: la luz se escapa del núcleo.
  Acoplamiento: en empalmes (fusión 0,1 dB, mecánico 0,5 dB), conectores (0,5 dB)
  y en las uniones con el emisor y el detector.

Paso 4: pérdidas por dispersión (ensanchan el pulso)
  Modal: en multimodo, los modos llegan en tiempos distintos.
  Cromática: si la fuente no es monocromática, cada longitud de onda viaja a su
  velocidad. Las dos limitan el ancho de banda (GHz·km).

Control: ¿están las del material, las de instalación y las de dispersión? ✓
```

### 3. Ejercicio guiado (TP 7, Ej 10)

> Enlace de fibra óptica monomodo con ancho de banda de 10 GHz·km, carretes de 400 m y 10 km de distancia. Empalme mecánico = 0,5 dB, conector = 0,6 dB (uno en el Tx y otro en el Rx), atenuación de la fibra = 0,3 dB/km, sensibilidad del receptor = −55 dBm, factor de diseño = 10 dB. a) Calcular la potencia necesaria en el transmisor, en watts. b) Calcular el ancho de banda disponible.

Es un enlace del bloque 3.1 (tipo 2, potencia necesaria) más el ancho de banda de la fibra.

```
Paso 1: pérdidas (conectores, empalmes, fibra, FD)
  → ________

Paso 2: potencia del transmisor en dBm
  → ________

Paso 3: potencia en mW y en W
  → ________

Paso 4: ancho de banda disponible
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: tercera ventana (2do parcial 2020, Tema 1, Ej 3)

> ¿Por qué es más conveniente generar pulsos de luz con un láser que opere en la tercera ventana de atenuación de la fibra óptica?

#### Ejercicio extra 2: LED y láser (2do parcial 2020, Tema 2, Ej 3)

> ¿Por qué no es conveniente generar pulsos de luz con un LED en lugar de un láser en un sistema de comunicaciones optoelectrónico? Describa este último.

#### Ejercicio extra 3: ventanas y frecuencias (TP 7, teoría, Ej 1)

> ¿A qué frecuencias corresponden las longitudes de onda de la primera, segunda y tercera ventana en que trabajan las fibras ópticas?

### 5. Cierre

**Fórmulas**

$$f = \frac{c}{\lambda} \qquad c = 3 \times 10^8\ \text{m/s} \qquad \Delta f_{\text{disp}} = \frac{\text{GHz·km}}{\text{km}} \qquad n_1 \operatorname{sen}\theta_1 = n_2 \operatorname{sen}\theta_2$$

```
Ventanas: 850, 1310 y 1550 nm (la 3ª, la de menor atenuación)
Monomodo: núcleo 9 µm, láser, largas distancias.  Multimodo: 50/62,5 µm, LED, < 2 km
Pérdidas: absorción, Rayleigh, curvaturas, dispersión modal y cromática, acoplamiento
Empalme fusión 0,1 dB, mecánico 0,5 dB, conector 0,5 dB.  Detectores: PIN, APD, PIN/FET
```

**Trampas**
- **Decir que la monomodo tiene dispersión modal.** Tiene un solo modo: no la tiene.
- **Confundir las dos dispersiones.** La modal es por los caminos (multimodo); la cromática, por las longitudes de onda (fuente no monocromática).
- **Olvidar dividir por la longitud** el ancho de banda en GHz·km.
- **Pasar la potencia a W sin pasar por mW.** De dBm se vuelve a mW, y después a W (÷ 1000).

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué el láser en la tercera ventana llega más lejos que un LED?
2. (Ejercicio) Una fibra multimodo de 500 MHz·km mide 2 km. ¿Qué ancho de banda ofrece? ¿Y la frecuencia de la luz de 1310 nm? (material propio)

## 7.3 Radioenlaces, antenas y satélites ★★★☆☆ (2 de 4)

Temas en Lumen: `u7-radiocomunicaciones-propagacion-ondas`, `u7-microondas-antenas`, `u7-comunicaciones-satelitales`, `u7-guia-onda-laser`, `u7-redes-inalambricas-voz-datos`

Apareció en los dos temas de 2020, con varias preguntas cortas cada uno: la longitud de una antena, las bandas del espectro, la propagación ionosférica y el retardo de un satélite. Los cálculos de radioenlaces son la práctica del TP 7.

### 1. Conceptos

**Longitud de onda.** Una onda electromagnética viaja por el aire o el vacío a $c = 3 \times 10^8$ m/s. Su longitud de onda es:

$$\lambda = \frac{c}{f} \qquad\qquad \lambda\,[\text{m}] = \frac{300}{f\,[\text{MHz}]}$$

**Bandas del espectro de radio.** Cada banda abarca un factor 10 en frecuencia (y en longitud de onda):
```
Banda   Frecuencia          Longitud de onda     Uso típico
VLF     3 a 30 kHz          100 a 10 km
LF      30 a 300 kHz        10 a 1 km
MF      300 kHz a 3 MHz     1 km a 100 m         radio AM (onda media)
HF      3 a 30 MHz          100 a 10 m           onda corta (reflexión ionosférica)
VHF     30 a 300 MHz        10 a 1 m             FM, TV
UHF     300 MHz a 3 GHz     1 m a 10 cm          TV digital, celulares, microondas
SHF     3 a 30 GHz          10 a 1 cm            microondas, satélites
EHF     30 a 300 GHz        1 cm a 1 mm          microondas
```
(Los límites de cada banda son los normalizados por la UIT; la cátedra los usa en las preguntas).

**Propagación.** Según la frecuencia, la onda llega de tres formas:
- **Onda terrestre** (hasta 2 MHz): viaja pegada a la superficie. Radio AM, hasta unos 300 km. Antena: **monopolo vertical de λ/4**.
- **Onda reflejada o ionosférica** (de 2 a 20 MHz, la HF): rebota en la ionosfera, las capas de la atmósfera ionizadas por el Sol, y puede dar la vuelta al mundo. Depende de la hora y la época; por encima de una frecuencia crítica ya no rebota. Antena: **dipolo horizontal de λ/2**.
- **Onda directa** (de 20 a 800 MHz y microondas): en línea recta, sin tocar el terreno. FM (88 a 108 MHz), TV. Alcance de unos 60 km, limitado por la curvatura de la Tierra.

**Antenas.** Para un buen rendimiento, la antena mide una fracción de la longitud de onda: **media onda** (λ/2, dipolo) o **cuarto de onda** (λ/4, monopolo). Las **parabólicas** concentran la energía en un haz; su ganancia crece con el diámetro D:

$$G_a\,[\text{dB}] = 10 \log_{10}\left(\frac{0{,}6\,\pi^2 D^2}{\lambda^2}\right)$$

Pueden ser **omnidireccionales** (irradian igual en todas las direcciones) o **direccionales** (un haz angosto, con poca potencia).

**Alcance visual.** La **distancia al horizonte** es hasta dónde llega una onda en línea recta desde una antena de altura H hasta rozar la Tierra. La atmósfera curva un poco la onda hacia abajo y la estira. El **alcance visual** entre dos antenas es la suma de sus distancias al horizonte:

$$D_H = 3{,}61\sqrt{H} \ \ \text{(sin difracción)} \qquad D_H = 4{,}14\sqrt{H} \ \ \text{(con la curvatura por la atmósfera)} \qquad AV = D_{H1} + D_{H2}$$

con $D_H$ en km y H en metros.

**Microondas.** De 300 MHz a 50 GHz (UHF, SHF, EHF). Enlaces punto a punto con visión directa entre dos antenas; si no se ven, se ponen **repetidoras** (pasivas, que solo reflejan, o activas, que amplifican). El ENACOM asigna las frecuencias según la distancia (23 GHz para menos de 5 km, 7/8 GHz para más de 12 km). Hoy son digitales, con PSK y QAM (capítulo 9).

**Ecuación del radioenlace.** Es la del bloque 3.1, con las antenas y el espacio libre:

$$P_{tx} - L_{\text{cable Tx}} + G_{\text{ant Tx}} - L_p + G_{\text{ant Rx}} - L_{\text{cable Rx}} - FD = S_{rx}$$

**Pérdida en el espacio libre.** Crece con la frecuencia y con la distancia:

$$L_p\,[\text{dB}] = 32{,}4 + 20 \log_{10} f\,[\text{MHz}] + 20 \log_{10} d\,[\text{km}]$$

**Satélites.** Son repetidoras en órbita, para llegar a puntos sin alcance visual.
```
Órbita                 Altura          Retardo aprox.   Características
Geoestacionaria (GEO)  36.000 km       unos 250-300 ms  gira con la Tierra; 3 cubren el planeta
Media (MEO)            más de 2.000 km unos 70 ms       6 a 8 h por vuelta
Baja (LEO)             unos 800 km     unos 10 ms       90 min por vuelta; muchos satélites
Bandas: C (3,4 a 8,4 GHz), Ku (12,4 a 18), K (18 a 26,5), Ka (26,5 a 40)
```
El retardo del geoestacionario genera ecos en telefonía y obliga a usar canceladores de eco. Para calcularlo, la señal sube y baja: $t = 2H / c$ como mínimo.

**Láser en el aire.** Enlaces ópticos punto a punto, sin cable, dentro de una ciudad: mucha capacidad, pero solo unos pocos kilómetros.

**Los tipos de ejercicio que toman:**
1. **Cálculos cortos:** la longitud de una antena, las longitudes de onda de una banda, el retardo de un satélite.
2. **Radioenlace:** la sensibilidad o la potencia con la ecuación del radioenlace.
3. **Alcance visual:** la distancia entre antenas, o la altura mínima.
4. **Teoría:** tipos de propagación, satélites, microondas.

### 2. Ejemplo resuelto (TP 7, Ej 1 y 2)

> Un transceptor de 35 W opera a 400 MHz y se conecta a su antena con 30 m de coaxil RG-213/U (15,5 dB/100 m a 400 MHz). a) ¿Qué potencia llega a la antena? b) El receptor usa el mismo coaxil y la misma distancia a su antena (30 m). Las dos antenas tienen 30 dB de ganancia y están separadas 1 km. Calcular la sensibilidad del receptor (sin factor de diseño).

Es un radioenlace (tipo 2): se arma la ecuación del radioenlace término por término. La potencia está en W, la frecuencia en MHz y la distancia en km, como pide la fórmula de $L_p$.

```
Paso 1: pérdida de cada cable
  30 m × 15,5 dB / 100 m = 4,65 dB

Paso 2: a) potencia en la antena
  35 W / 10 ^ (4,65 / 10) = 35 / 2,917 ≈ 12 W

Paso 3: Ptx en dBm
  35 W = 35.000 mW  →  10 · log10(35.000) = 45,44 dBm

Paso 4: pérdida en el espacio libre
  Lp = 32,4 + 20 · log10(400) + 20 · log10(1) = 32,4 + 52,04 + 0 = 84,44 dB

Paso 5: b) ecuación del radioenlace
  Srx = 45,44 − 4,65 + 30 − 84,44 + 30 − 4,65 = 11,70 dBm

Control: 45,44 + 60 (antenas) − 93,74 (pérdidas) = 11,70 dBm ✓
```

### 3. Ejercicio guiado (2do parcial 2020, Tema 1, Ej 4)

> Comparar el retardo aproximado de una señal de datos transmitida de Buenos Aires a Madrid (10.000 km): a) por un satélite geoestacionario; b) por un cable submarino.

Se toma la velocidad de la luz para los dos medios (en la fibra es algo menor, pero no cambia la conclusión). El satélite obliga a subir 36.000 km y bajar otros 36.000.

```
Paso 1: distancia que recorre la señal por satélite
  → ________

Paso 2: retardo por satélite
  → ________

Paso 3: retardo por cable
  → ________

Paso 4: conclusión
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: antena de Wi-Fi (2do parcial 2020, Tema 1, Ej 5)

> ¿Qué longitud deberá tener la antena de un router Ethernet inalámbrico IEEE 802.11 que opera en 5 GHz? (Tomá una antena de λ/4).

#### Ejercicio extra 2: banda UHF (2do parcial 2020, Tema 2, Ej 1)

> Indicar las longitudes de onda de los extremos de la banda UHF del espectro electromagnético.

#### Ejercicio extra 3: onda ionosférica (2do parcial 2020, Tema 1, Ej 7)

> Indicar las longitudes de onda de los extremos de la banda del espectro para la cual se produce la onda reflejada o ionosférica.

#### Ejercicio extra 4: alcance visual (TP 7, Ej 7)

> ¿Cuál será la distancia del enlace visual para dos antenas de 20 m de altura, teniendo en cuenta la curvatura de las ondas por la atmósfera?

#### Ejercicio extra 5: altura con una antena limitada (TP 7, Ej 8 y 9)

> Un enlace en UHF de 50 km necesita que las antenas se vean. a) ¿A qué altura mínima deben estar las dos, si son iguales? No se considera la difracción. b) ¿Y la otra, si una no puede superar los 10 m?

#### Ejercicio extra 6: antena de FM (TP 7, Ej 5)

> Un receptor de FM usa una antena de 75 cm. ¿De qué tipo de antena se trata? La banda de FM va de 88 a 108 MHz.

### 5. Cierre

**Fórmulas**

$$\begin{aligned}
\lambda &= \frac{c}{f} \qquad \lambda\,[\text{m}] = \frac{300}{f\,[\text{MHz}]} \qquad \text{antenas: } \lambda/2 \text{ (dipolo)}, \ \lambda/4 \text{ (monopolo)} \\[4pt]
L_p &= 32{,}4 + 20\log_{10} f\,[\text{MHz}] + 20\log_{10} d\,[\text{km}] \\[4pt]
S_{rx} &= P_{tx} - L_{\text{cable}} + G_{\text{Tx}} - L_p + G_{\text{Rx}} - L_{\text{cable}} - FD \\[4pt]
D_H &= 3{,}61\sqrt{H} \ \text{(sin difracción)}, \quad 4{,}14\sqrt{H} \ \text{(con atmósfera)} \qquad AV = D_{H1} + D_{H2} \qquad t_{\text{sat}} = \frac{2H}{c}
\end{aligned}$$

```
HF 3-30 MHz (100 a 10 m, ionosférica)   VHF 30-300 MHz   UHF 300 MHz-3 GHz (1 m a 10 cm)
GEO 36.000 km (≈ 250-300 ms), MEO > 2.000 km (≈ 70 ms), LEO ≈ 800 km (≈ 10 ms)
```

**Trampas**
- **Dividir mal por 4.** 6 cm / 4 = 1,5 cm, no 15 cm (hay una resolución que circula con ese error).
- **Usar f en Hz o d en m en $L_p$.** La fórmula pide MHz y km.
- **Calcular el retardo del satélite con 36.000 km.** La señal sube y baja: son 72.000 km como mínimo.
- **Olvidar la raíz en el alcance visual.** Es $4{,}14\sqrt{H}$, con H en metros.
- **Sumar las ganancias de las antenas como factores.** Van en dB, sumadas en la ecuación.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Por qué la onda de HF puede dar la vuelta al mundo y la de VHF no?
2. (Ejercicio) ¿Cuánto mide una antena de media onda para 150 MHz? ¿Y la pérdida en el espacio libre a 150 MHz y 10 km? (material propio)

## Respuestas del capítulo 7

### 7.1 Ejercicio guiado

```
Paso 1: qué es
  "Es la relación entre la tensión aplicada y la corriente absorbida por un cable de
   longitud infinita. Un cable real terminado en una carga igual a Z0 se comporta
   como infinito."

Paso 2: de qué depende
  De las características constructivas: el material de los conductores, el
  dieléctrico que los separa y los diámetros del conductor interior y de la malla
  (eléctricamente, de R, L y C por unidad de longitud).

Paso 3: frecuencia
  No: la impedancia característica no depende de la frecuencia ni de la longitud,
  porque depende solo de parámetros constructivos, que son fijos una vez fabricado
  el cable. Con la frecuencia lo que aumenta es la atenuación.

Paso 4: por qué importa
  Para máxima eficiencia, las impedancias del transmisor, del cable y del receptor
  tienen que ser iguales; si no, hay reflexiones que degradan la señal.
```

### 7.1 Ejercicio extra 1

```
Resistiva cuando XL = XC  →  f = 1 / (2π · √(L · C))
L · C = 2 × 10^−6 × 0,058 × 10^−6 = 1,16 × 10^−13
√(1,16 × 10^−13) ≈ 3,406 × 10^−7
f = 1 / (2π × 3,406 × 10^−7) ≈ 467.300 Hz ≈ 467 kHz
```

### 7.1 Ejercicio extra 2

La categorización fija qué características eléctricas (atenuación, capacidad, impedancia, diafonía) garantiza cada tipo de cable, y con eso hasta qué frecuencia y velocidad funciona a una longitud dada: así se elige el cable según la red. Categorías: 1 (telefonía, no datos), 2 (hasta 4 Mbps), 3 (Token Ring 4 Mbps o Ethernet 10 Mbps), 4 (Token Ring 16 Mbps), 5 (Fast Ethernet, 100 Mbps, 100 MHz), 5e (algunas aplicaciones a 1 Gbps), 6 (1 Gbps), y 6A, 7 y 7A para aplicaciones especiales.

### 7.1 Ejercicio extra 3

```
UTP: sin blindaje, el más barato; para interiores.
FTP: una hoja de aluminio que envuelve los cuatro pares; protege de la interferencia externa.
STP: cada par blindado; protege además de la interferencia entre pares.
Se trenzan para que la interferencia externa se induzca igual en los dos hilos y se
cancele (el par es balanceado), y para bajar la diafonía entre pares vecinos.
```

### 7.1 Autoevaluación

```
1. Es una línea en la que cada circuito tiene su par: la señal va por un hilo y vuelve
   por el otro, en contrafase, y se lee como la diferencia entre los dos. El ruido
   entra igual en ambos hilos y en la diferencia se cancela.

2. L · C = 0,5 × 10^−3 × 50 × 10^−9 = 2,5 × 10^−11  →  √ ≈ 5 × 10^−6
   f = 1 / (2π × 5 × 10^−6) ≈ 31.800 Hz ≈ 31,8 kHz
```

### 7.2 Ejercicio guiado

```
Paso 1: pérdidas
  Conectores: 2 × 0,6                             =  1,2 dB
  Carretes: 10.000 / 400 = 25  →  24 empalmes × 0,5 = 12 dB
  Fibra: 10 km × 0,3 dB/km                         =  3 dB
  FD                                               = 10 dB
  Total                                            = 26,2 dB

Paso 2: Ptx = Srx + pérdidas = −55 + 26,2 = −28,8 dBm

Paso 3: 10 ^ (−2,88) ≈ 0,00132 mW = 1,32 µW = 1,32 × 10^−6 W

Paso 4: ancho de banda disponible = 10 GHz·km / 10 km = 1 GHz

Control: −28,8 − 26,2 = −55 dBm = Srx ✓
```

### 7.2 Ejercicio extra 1

La atenuación de la fibra depende de la longitud de onda, y la tercera ventana (1550 nm) es la de menor atenuación de las tres: con la misma potencia, la señal llega más lejos, o hacen falta menos repetidores. El láser conviene porque emite luz coherente y monocromática, con más potencia: casi no hay dispersión cromática, así que los pulsos no se ensanchan y se mantiene el ancho de banda.

### 7.2 Ejercicio extra 2

El LED emite varias longitudes de onda a la vez (luz no coherente, no monocromática). Como en la fibra cada longitud de onda viaja a una velocidad distinta, hay dispersión cromática: los pulsos se ensanchan y pierden amplitud, lo que limita el ancho de banda y la distancia. El **láser** genera luz por emisión estimulada: un átomo excitado, al recibir otro fotón, emite un fotón igual. Así da una luz coherente y monocromática, con más potencia y más confiable; se usa en fibras monomodo y en largas distancias.

### 7.2 Ejercicio extra 3

```
f = c / λ,  con c = 3 × 10^8 m/s
1ª ventana, 850 nm:   3 × 10^8 / 850 × 10^−9  ≈ 3,53 × 10^14 Hz ≈ 353 THz
2ª ventana, 1310 nm:  3 × 10^8 / 1310 × 10^−9 ≈ 2,29 × 10^14 Hz ≈ 229 THz
3ª ventana, 1550 nm:  3 × 10^8 / 1550 × 10^−9 ≈ 1,94 × 10^14 Hz ≈ 194 THz
```

### 7.2 Autoevaluación

```
1. El láser da luz monocromática y potente, sin dispersión cromática, y la tercera
   ventana es la de menor atenuación: la señal llega más lejos sin ensancharse.
   El LED emite varias longitudes de onda: dispersión cromática y menos alcance.

2. 500 MHz·km / 2 km = 250 MHz.   f = 3 × 10^8 / 1310 × 10^−9 ≈ 229 THz
```

### 7.3 Ejercicio guiado

```
Paso 1: distancia por satélite
  Sube 36.000 km y baja 36.000 km: 72.000 km como mínimo.

Paso 2: retardo por satélite
  t = 72.000 km / 300.000 km/s = 0,24 s = 240 ms

Paso 3: retardo por cable
  t = 10.000 km / 300.000 km/s ≈ 0,033 s ≈ 33 ms

Paso 4: conclusión
  El satélite geoestacionario tiene unas 7 veces más retardo que el cable: la señal
  recorre mucha más distancia. En telefonía obliga a usar canceladores de eco.
```

### 7.3 Ejercicio extra 1

```
λ = 3 × 10^8 / 5 × 10^9 = 0,06 m = 6 cm
λ/4 = 1,5 cm
(La resolución que circula dice 15 cm, pero 6 cm / 4 = 1,5 cm).
```

### 7.3 Ejercicio extra 2

```
UHF: 300 MHz a 3 GHz
λ = 300 / 300 MHz = 1 m     λ = 300 / 3.000 MHz = 0,1 m = 10 cm
Va de 1 m a 10 cm.
```

### 7.3 Ejercicio extra 3

```
La onda ionosférica se da en HF, de 3 a 30 MHz:
λ = 300 / 3 = 100 m     λ = 300 / 30 = 10 m
Va de 100 m a 10 m.
```

### 7.3 Ejercicio extra 4

```
DH = 4,14 · √20 = 4,14 × 4,472 ≈ 18,5 km
AV = 2 × 18,5 ≈ 37 km
```

### 7.3 Ejercicio extra 5

```
a) Antenas iguales: AV = 50 km  →  DH = 25 km cada una
   25 = 3,61 · √H  →  √H = 6,93  →  H ≈ 48 m
   (Con Pitágoras y el radio de la Tierra, 6.370 km:
    H = √(25² + 6.370²) − 6.370 ≈ 0,049 km = 49 m; da casi lo mismo).
b) H1 = 10 m  →  DH1 = 3,61 · √10 ≈ 11,4 km
   DH2 = 50 − 11,4 = 38,6 km  →  38,6 = 3,61 · √H2  →  √H2 ≈ 10,7  →  H2 ≈ 114 m
```

### 7.3 Ejercicio extra 6

```
Frecuencia media de FM: (88 + 108) / 2 = 98 MHz
λ = 300 / 98 ≈ 3,06 m ≈ 3 m
75 cm ≈ λ/4 → es una antena de cuarto de onda (monopolo).
```

### 7.3 Autoevaluación

```
1. La HF (3 a 30 MHz) rebota en la ionosfera y vuelve a la Tierra, y puede encadenar
   varios rebotes. La VHF atraviesa la ionosfera: solo llega por onda directa, hasta
   el horizonte.

2. λ = 300 / 150 = 2 m  →  media onda: 1 m
   Lp = 32,4 + 20 · log10(150) + 20 · log10(10) = 32,4 + 43,5 + 20 ≈ 95,9 dB
```
