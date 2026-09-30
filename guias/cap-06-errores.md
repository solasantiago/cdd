# Capítulo 6: Tratamiento de errores (TP 6)

## 6.1 Detección y corrección de errores ★★☆☆☆ (3 de 8) 📌 2026

Temas en Lumen: `u6-tipos-errores-tasa-error`, `u6-deteccion-errores-paridad-crc`, `u6-correccion-errores-codigos-autocorrectores`

En 2020 fue un problema (CRC en el Tema 2, checksum en el Tema 4). En 2026 fueron dos preguntas de teoría: las causas de errores y las políticas de tratamiento, y el BER y si CRC y checksum solo detectan o también corrigen.

### 1. Conceptos

**Error de transmisión.** Es toda alteración de un mensaje recibido que hace que no sea una réplica fiel del transmitido y cambia la interpretación de la información: un 0 llega como 1, o al revés.

**Causas de los errores.** Son las perturbaciones del canal (bloque 5.2) y sus limitaciones:
1. **Atenuación:** la señal pierde amplitud a lo largo del canal, y cerca del receptor se confunde con el ruido.
2. **Distorsión:** el canal deforma la señal (por atenuación o retardo distintos según la frecuencia), y un bit se mete en el siguiente.
3. **Ruido:** térmico, diafonía, intermodulación e impulsivo; se suma a la señal y puede cambiar bits.
4. **Ancho de banda insuficiente:** si el canal corta armónicas del lóbulo principal, los pulsos llegan deformados (bloque 2.2).
5. **Tasa de información mayor que la capacidad del canal** (Shannon, bloque 5.1).

Ojo: en 2026 la consigna pedía "las cuatro causas", pero en el material de la cátedra no aparece una lista cerrada de cuatro; los resúmenes de la cursada dan estas cinco (alguno agrega la pérdida de sincronismo). En el parcial, nombrá las tres perturbaciones (atenuación, distorsión y ruido) y las dos limitaciones del canal, cada una con su porqué.

**Tipos de errores** (clase de errores, UT 6), según cómo se reparten en el tiempo:
- **Aislados o simples:** afectan un solo bit por vez y son independientes entre sí.
- **En ráfagas:** afectan varios bits consecutivos, en momentos imprevisibles (típico del ruido impulsivo).
- **Agrupados:** aparecen en tandas de cierta duración, pero no necesariamente en bits seguidos.

**Tasa de error (BER).** Mide la calidad de un canal digital: cuántos bits llegan mal sobre el total transmitido.

$$BER = \frac{\text{bits erróneos}}{\text{bits transmitidos}}$$

Cuanto más chico, mejor. Ejemplos: 20 bits erróneos en 200.000 dan $BER = 10^{-4}$, o sea 1 bit mal cada 10.000 (TP 6). Para una LAN Ethernet se espera un BER del orden de $10^{-9}$, así que $10^{-4}$ sería una red con muchísimos paquetes perdidos (TP 6, según la resolución de la cursada).

**Políticas de tratamiento de errores** (clase de errores, UT 6). Son cuatro:
1. **Ignorarlos,** porque otra capa del protocolo se encarga de ellos.
2. **Detectarlos y avisar** que hubo un error.
3. **Detectarlos y pedir la retransmisión** del mensaje.
4. **Detectarlos y corregirlos** en el receptor.

**La idea: redundancia.** El transmisor le aplica un algoritmo a los datos y agrega bits de control, que son redundantes: no llevan información. El receptor le aplica el mismo algoritmo a lo que recibió. Si le da igual que los bits de control, acepta los datos; si no, detectó un error. Cuantos más bits de control, más protección, pero menos eficiencia (bloque 2.1).

**Paridad (vertical, VRC).** Se agrega un bit a cada carácter para que la cantidad total de unos quede par (paridad par) o impar (paridad impar).
```
Datos 0110 (tienen dos unos)   →   paridad par:   0   →   01100
                               →   paridad impar: 1   →   01101
```
Detecta si cambió 1 bit, o cualquier cantidad impar. Si cambian 2, la cantidad de unos sigue siendo par y no se da cuenta. Tampoco corrige, porque no sabe cuál bit cambió.

**Paridad longitudinal (LRC, BCC).** En un bloque de varios caracteres, además de la paridad de cada carácter, se saca una paridad por columna: una con el primer bit de todos los caracteres, otra con el segundo, y así. Con esos bits se arma un carácter de control al final del bloque, el **BCC**. Detecta más errores que la paridad sola.

**CRC (control por redundancia cíclica).** Es el más usado: lo usan Ethernet, PPP, HDLC y Frame Relay. Trata el mensaje como un polinomio de bits y lo divide por un **polinomio generador G(x)** que conocen los dos extremos.
```
G(x) a binario: un 1 por cada potencia de x que aparece y un 0 por cada una que falta
  x⁴ + x + 1  =  1·x⁴ + 0·x³ + 0·x² + 1·x + 1   →   10011
  Grado r = 4 (la potencia más alta) = cantidad de bits del resto
```
La división es **en módulo 2**: en vez de restar se hace **XOR** bit a bit, sin pedir prestado ni llevarse nada.
```
0 XOR 0 = 0     1 XOR 1 = 0     0 XOR 1 = 1     1 XOR 0 = 1
(iguales → 0, distintos → 1)
```
El procedimiento:
```
Transmisor:
  1. Agregar r ceros al final del mensaje M(x)
  2. Dividir por G(x) en módulo 2: poner G debajo del primer 1 que queda y hacer XOR;
     repetir hasta que lo que queda sea más corto que G
  3. Lo que queda es el resto R(x): tiene r bits
     (completalo con ceros adelante si hace falta)
  4. Se transmite T(x) = el mensaje con el resto en lugar de los ceros

Receptor:
  5. Divide T(x) por el mismo G(x)
  6. Resto cero → sin errores.   Resto distinto de cero → hubo error
```

**Rendimiento sincrónico.** Es qué parte de lo que se manda son datos:

$$\eta = \frac{\text{bits del mensaje}}{\text{bits transmitidos}} \times 100\ [\%]$$

**Checksum (suma de verificación).** Lo usan TCP, IP, UDP e ICMP. Así lo resuelve la cátedra en el TP 6:
```
Transmisor:
  1. Sumar las palabras de a una, en binario
  2. Si una suma da un bit de más (acarreo), se saca y se le suma al resultado
     (en la resolución de la cátedra: "por carrier: 1")
  3. Al resultado final se le saca el complemento a 1 (se invierte cada bit):
     ese es el checksum
  4. Se mandan las palabras y el checksum

Receptor:
  5. Suma todas las palabras y el checksum, de la misma forma
  6. Si da todos unos (1111) → sin errores
```
Es simple, pero débil: si dos errores se compensan en la suma, no los ve.

**¿CRC y checksum detectan o corrigen?** Es la pregunta 3 de 2026. **Solo detectan:** el receptor sabe que el bloque llegó con algún error, pero no cuál bit está mal. Para corregir hay que pedir la retransmisión (ARQ) o usar un código autocorrector, que sí ubica el bit (FEC).

**Corrección de errores.** Hay dos formas:
- **Hacia atrás (ARQ):** el receptor detecta el error y pide que le repitan el bloque. Contesta **ACK** si llegó bien o **NAK** si llegó con error. Tiene dos variantes. En **parada y espera** (stop and wait), el transmisor manda un bloque y espera la respuesta antes de mandar el siguiente. En **ventana deslizante**, manda varios bloques antes de esperar. Es punto a punto, y además sirve como control de flujo.
- **Hacia adelante (FEC):** el receptor corrige solo, con códigos autocorrectores como Hamming. Se usa cuando no se puede pedir retransmisión, por ejemplo en una transmisión simplex.

**Distancia Hamming.** Es la cantidad de bits en que difieren dos palabras. Por ejemplo, 10110 y 10011 difieren en 2 posiciones: distancia 2. La **distancia mínima** ($d_{\text{mín}}$) de un código es la menor distancia entre dos de sus palabras:

$$\text{detecta hasta } d_{\text{mín}} - 1 \text{ errores} \qquad\qquad \text{corrige hasta } \left\lfloor \frac{d_{\text{mín}} - 1}{2} \right\rfloor \text{ errores}$$

Por ejemplo, con $d_{\text{mín}} = 3$ detecta 2 y corrige 1.

**Código de Hamming.** Es un código autocorrector: corrige 1 bit errado. Los bits de paridad van en las posiciones que son potencias de 2 (1, 2, 4, 8...), y los datos en las demás. Cada paridad controla las posiciones que, escritas en binario, tienen ese bit en 1:
```
Posición:    1    2    3    4    5    6    7
Contenido:   p1   p2   d    p4   d    d    d        (4 datos + 3 paridades = 7 bits)

p1 controla las posiciones 1, 3, 5, 7   (las impares)
p2 controla las posiciones 2, 3, 6, 7
p4 controla las posiciones 4, 5, 6, 7
```
En recepción se recalcula cada paridad. Las que fallan se suman por su número de posición, y el resultado dice qué bit está mal: si fallan p1 y p4, el error está en el bit 1 + 4 = 5, y se corrige invirtiéndolo. Para m bits de datos, la cantidad de paridades r es la menor que cumple $2^r \ge m + r + 1$ (con m = 4 da r = 3).

**Los tipos de ejercicio que toman:**
1. **CRC:** te dan M(x) y G(x). Piden lo que se transmite, la verificación en el receptor y el rendimiento sincrónico. O te dan lo que se recibió y preguntan si hubo error.
2. **Checksum:** te dan palabras de 4 bits. Piden el checksum, la verificación en el receptor y las conclusiones.
3. **Teoría:** causas de los errores, políticas de tratamiento, BER con ejemplos, si CRC y checksum detectan o corrigen, protocolos que usan cada uno y cuándo se usan códigos correctores.

### 2. Ejemplo resuelto (1er parcial, Temas 1 a 4 (2020), Tema 2, Ej 4)

> Mensaje M(x) = 1 0 1 1 0 1 0 1 1 0 1 y polinomio generador G(x) = x⁴ + x + 1. Aplicar el método CRC: determinar la información a transmitir, verificar en el receptor que la transmisión no tuvo errores y calcular el rendimiento sincrónico.

Es del tipo 1. El mensaje tiene 11 bits. G tiene grado 4, así que se agregan 4 ceros y el resto tiene 4 bits. En cada renglón se pone G debajo del primer 1 que queda y se hace XOR. Los ceros que quedan adelante se descartan.

```
Paso 1: G(x) a binario
  x⁴ + x + 1   →   10011       grado r = 4

Paso 2: agregar 4 ceros al mensaje
  10110101101   →   101101011010000

Paso 3: dividir en módulo 2
  101101011010000
  10011                     ← XOR
  -----
    1011011010000
    10011                   ← XOR
    -----
      10111010000
      10011                 ← XOR
      -----
        100010000
        10011               ← XOR
        -----
           100000
           10011            ← XOR
           -----
              110
  Lo último (110) ya es más corto que G: es el resto. Con 4 bits: R(x) = 0110

Paso 4: lo que se transmite (el resto en lugar de los 4 ceros)
  T(x) = 10110101101 0110  =  101101011010110

Paso 5: el receptor divide T(x) por el mismo G(x)
  101101011010110
  10011                     ← XOR
  -----
    1011011010110
    10011                   ← XOR
    -----
      10111010110
      10011                 ← XOR
      -----
        100010110
        10011               ← XOR
        -----
           100110
           10011            ← XOR
           -----
                0
  Resto = 0000   →   sin errores ✓

Paso 6: rendimiento sincrónico
  11 bits de mensaje / 15 bits transmitidos × 100 ≈ 73,3 %
```

### 3. Ejercicio guiado (1er parcial, Temas 1 a 4 (2020), Tema 4, Ej 2)

> Obtener el mensaje a transmitir con el método CHECKSUM para estas palabras de 4 bits: A = 0011, B = 1011, C = 0110, D = 0010. Repetir el procedimiento del lado del receptor. Extraer conclusiones.

Es del tipo 2. Se suman las palabras de a una, en binario; si alguna suma se pasa de 4 bits, el acarreo se vuelve a sumar. Al final se saca el complemento a 1.

```
Paso 1: A + B
  → ________

Paso 2: + C (¿hay acarreo?)
  → ________

Paso 3: + D
  → ________

Paso 4: complemento a 1 → checksum
  → ________

Paso 5: lo que se transmite
  → ________

Paso 6: el receptor suma las 4 palabras y el checksum
  → ________

Paso 7: rendimiento sincrónico y conclusión
  → ________
```

### 4. Práctica

#### Ejercicio extra 1: CRC en el receptor (clase de consulta 2020, Ej 24)

> Se recibe la secuencia T = 1010011101. Aplicar el método CRC con el polinomio generador G(x) = x⁴ + x² + 1 e indicar si hubo errores. Marcar los bits de T que corresponden al resto.

#### Ejercicio extra 2: paridad (material propio)

> Agregar al carácter 1010001 el bit de paridad par y el de paridad impar. Con paridad par: si llega 1110001 más el bit de paridad, ¿el receptor detecta el error? ¿Y si llega 1100001 más el bit de paridad?

#### Ejercicio extra 3: Hamming (material propio)

> Codificar los datos 1011 con Hamming de 7 bits y paridad par (los datos van, en orden, en las posiciones 3, 5, 6 y 7). Después, suponer que llega 0110111 y encontrar el bit errado.

#### Ejercicio extra 4: teoría (1er parcial 28/09/2026, Tema B, Ej 2)

> Detalle las causas de errores en los canales de comunicaciones, e indique las políticas de tratamiento de errores en los protocolos de comunicaciones.

#### Ejercicio extra 5: teoría (1er parcial 28/09/2026, Tema B, Ej 3)

> ¿Cómo se define la tasa de errores (BER)? Cite ejemplos. Los métodos CRC y suma de verificación, ¿posibilitan detectar si hay error en un paquete de datos o permiten determinar cuáles son los bits erróneos para luego corregirlos? Explique brevemente.

#### Ejercicio extra 6: teoría (TP 6, teoría)

> Cite cuatro protocolos que usen CRC y cuatro que usen suma de verificación. ¿Cuándo se emplean códigos correctores de errores?

### 5. Cierre

**Fórmulas**

$$BER = \frac{\text{bits erróneos}}{\text{bits transmitidos}} \qquad \eta = \frac{\text{bits de datos}}{\text{bits transmitidos}} \qquad 2^r \ge m + r + 1$$

$$\text{detecta } d_{\text{mín}} - 1 \qquad \text{corrige } \left\lfloor (d_{\text{mín}} - 1)/2 \right\rfloor$$

```
XOR: iguales → 0, distintos → 1
CRC: agregar r ceros (r = grado de G), dividir en módulo 2, el resto reemplaza los ceros
Checksum: sumar con acarreo vuelto a sumar, complemento a 1; el receptor debe dar 1111
Hamming: paridades en 1, 2, 4; bit errado = suma de las posiciones de las paridades que fallan
Políticas: ignorar, detectar y avisar, detectar y pedir retransmisión, detectar y corregir
CRC: Ethernet, PPP, HDLC, Frame Relay.   Checksum: TCP, IP, UDP, ICMP
```

**Trampas**
- **Agregar ceros de menos en CRC.** Se agregan tantos como el grado de G (x⁴ → 4 ceros), no tantos como bits tiene G.
- **Restar en vez de hacer XOR.** En módulo 2 no se pide prestado.
- **En el checksum, olvidar sumar el acarreo** o el complemento a 1 del final.
- **Decir que CRC o checksum corrigen.** Solo detectan; corregir es de ARQ (retransmitiendo) o de FEC (Hamming).
- **Dar las políticas o las causas sin explicar.** En 2026 cada ítem sumaba solo si estaba completo.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Qué es el BER? ¿Por qué el CRC no permite corregir el error, y qué se hace entonces?
2. (Ejercicio) Aplicá CRC al mensaje 1101 con G(x) = x³ + x + 1: calculá lo que se transmite. (material propio)

## 6.2 Protocolos: conexión y calidad de servicio ★★★☆☆ (2 de 4)

Temas en Lumen: `u3-protocolos-arquitecturas-comunicaciones`, `u3-protocolos-enlace-orientados-caracter`

Las estrellas de este bloque se cuentan sobre los 2dos parciales (4 relevados): apareció en los dos temas de 2020. En 2026 la planificación da los protocolos de comunicación junto con el TP 6, después del 1er parcial, así que entra en el 2do.

### 1. Conceptos

**Protocolo.** Es el conjunto de reglas con que se comunican las capas iguales de los dos extremos (capítulo 1): el formato de los mensajes, qué significa cada campo y en qué orden se intercambian.

**Orientado a la conexión.** Antes de mandar datos se establece la conexión con el otro extremo y se verifica que responde. Tiene tres fases: **establecimiento, transferencia y liberación**. Los datos llegan en orden y confirmados. Ejemplos: TCP, la telefonía (conmutación de circuitos) y el circuito virtual. Ventaja: es **confiable**, asegura que la información llegue. Desventaja: agrega demora (establecer la conexión) y bits de control; es menos eficiente.

**No orientado a la conexión.** Cada paquete (datagrama) viaja por su cuenta, sin establecer nada antes y sin confirmación. Ejemplos: IP y UDP. Ventaja: es **simple y rápido**. Desventaja: no garantiza la entrega ni el orden; si hace falta, lo resuelve otra capa o la aplicación. Por eso se combinan: TCP (orientado) funciona sobre IP (no orientado).

**Calidad de servicio (QoS).** Es el conjunto de parámetros que la red se compromete a cumplir para un tráfico: el **retardo de tránsito**, la variación del retardo, la pérdida y la tasa de errores, el ancho de banda, y el control de flujo y de errores.
- **Con QoS:** la red clasifica el tráfico, le da prioridad al que la necesita (voz, video) y le reserva recursos. Ejemplos: Frame Relay, ATM, IP con mecanismos de QoS. Ventaja: tráfico priorizado y confiable. Desventaja: exige más a la red (procesamiento, configuración) y es más cara.
- **Sin QoS ("mejor esfuerzo", best effort):** la red hace lo posible para entregar cada paquete, sin garantías de retardo ni de entrega; las validaciones quedan a cargo de la aplicación. Ejemplos: IP básico y UDP (por ejemplo, las consultas DNS). Ventaja: simplicidad. Desventaja: el tráfico sensible (voz) puede degradarse.

Ojo: una resolución que circula dice que la QoS "indica el mejor esfuerzo". Es al revés: el mejor esfuerzo es justamente la ausencia de QoS.

**Protocolos de enlace orientados al carácter y al bit** (material propio sobre la clase). Los **orientados al carácter**, como BSC, delimitan los mensajes con caracteres de control (por ejemplo, STX y ETX, que marcan el comienzo y el fin del texto): dependen del código de caracteres. Los **orientados al bit**, como HDLC, delimitan las tramas con una bandera (01111110) y aseguran la transparencia agregando un 0 después de cinco unos seguidos en los datos (inserción de bits): mandan cualquier secuencia de bits.

**Los tipos de pregunta que toman:** definir y comparar orientado y no orientado a la conexión, y con y sin calidad de servicio, con ejemplos, ventajas y desventajas.

### 2. Ejemplo resuelto (2do parcial 2020, Tema 1, Ej 10)

> Defina protocolo orientado a la conexión y no orientado a la conexión, cite un ejemplo de cada uno. Detalle ventajas y desventajas de los mismos.

Pide cuatro cosas por cada uno: definición, ejemplo, ventaja y desventaja. Conviene cerrar diciendo cómo se combinan.

```
Paso 1: orientado a la conexión
  "Antes de transferir datos se establece la conexión con el otro extremo; tiene
   fases de establecimiento, transferencia y liberación, y entrega los datos en
   orden y confirmados. Ejemplo: TCP (o la telefonía)."
  Ventaja: confiable, asegura la entrega.  Desventaja: más demora y overhead.

Paso 2: no orientado a la conexión
  "Cada paquete (datagrama) se envía por su cuenta, sin establecer conexión ni
   confirmar la entrega. Ejemplo: IP (o UDP)."
  Ventaja: simple y rápido.  Desventaja: no garantiza entrega ni orden.

Paso 3: cierre
  "Se combinan: TCP, orientado a la conexión, funciona sobre IP, que no lo es; así
   la red es simple y la confiabilidad la dan los extremos."

Control: ¿hay definición, ejemplo, ventaja y desventaja de cada uno? ✓
```

### 3. Ejercicio guiado (2do parcial 2020, Tema 2, Ej 7)

> Defina protocolo con calidad de servicio y sin calidad de servicio, cite un ejemplo de cada uno. Detalle ventajas y desventajas de los mismos.

```
Paso 1: qué es la calidad de servicio (parámetros)
  → ________

Paso 2: con QoS (definición, ejemplo, ventaja, desventaja)
  → ________

Paso 3: sin QoS (definición, ejemplo, ventaja, desventaja)
  → ________
```

### 4. Práctica

Intentá responder cada una en dos o tres líneas antes de mirar las respuestas.

1. ¿Por qué TCP funciona sobre IP si uno es orientado a la conexión y el otro no?
2. ¿Qué diferencia hay entre un protocolo de enlace orientado al carácter y uno orientado al bit? Dá un ejemplo de cada uno.
3. ¿Qué tráfico necesita calidad de servicio y por qué?

### 5. Cierre

**Fórmulas** (para memorizar)
```
Orientado a la conexión: establecimiento, transferencia, liberación; confiable (TCP)
No orientado: datagramas independientes; simple, sin garantías (IP, UDP)
QoS: retardo, variación del retardo, pérdida y errores, ancho de banda, flujo
Sin QoS = mejor esfuerzo (best effort)
Enlace: orientado al carácter (BSC, STX/ETX) y al bit (HDLC, bandera 01111110)
```

**Trampas**
- **Decir que el mejor esfuerzo es un tipo de QoS.** Es la ausencia de QoS.
- **Poner IP como orientado a la conexión.** IP no lo es; TCP sí.
- **Olvidar las ventajas y desventajas.** La consigna las pide explícitamente.

**Autoevaluación** (sin mirar el bloque; cada ítem vale 1, 0,5 o 0)
1. (Concepto) ¿Qué gana y qué pierde un protocolo orientado a la conexión?
2. (Pregunta) Nombrá tres parámetros de calidad de servicio y un ejemplo de tráfico que la necesite.

## Respuestas del capítulo 6

### 6.1 Ejercicio guiado

```
Paso 1: A + B
     0011
   + 1011
   ------
     1110          (entra en 4 bits: no hay acarreo)

Paso 2: + C
     1110
   + 0110
   ------
    10100          (se pasó a 5 bits: el 1 de adelante es el acarreo)
     0100 + 1  =  0101

Paso 3: + D
     0101 + 0010 = 0111

Paso 4: complemento a 1 (se invierte cada bit)
     0111   →   1000          ← checksum

Paso 5: lo que se transmite
     0011  1011  0110  0010  1000

Paso 6: el receptor suma las 4 palabras (le da 0111) y le suma el checksum
     0111 + 1000 = 1111          (todos unos → sin errores ✓)

Paso 7: rendimiento y conclusión
  16 bits de datos / 20 bits transmitidos × 100 = 80 %
  Con 4 bits de redundancia el receptor verifica que no hubo errores. Pero el método
  es débil: si A llegara como 0010 y D como 0011, la suma daría igual y el error no
  se detectaría.
```

### 6.1 Ejercicio extra 1

```
G(x) = x⁴ + x² + 1 = 1·x⁴ + 0·x³ + 1·x² + 0·x + 1   →   10101    grado 4
1010011101
10101                     ← XOR
-----
    111101
    10101                 ← XOR
    -----
     10111
     10101                ← XOR
     -----
        10
Resto = 0010 (distinto de cero)   →   hubo error en la transmisión
El resto que agregó el transmisor son los últimos 4 bits de T:  101001 1101
```

### 6.1 Ejercicio extra 2

```
1010001 tiene 3 unos   →   paridad par: 1 (queda 10100011)    paridad impar: 0
Llega 1110001 + 1: hay 5 unos en total, impar   →   detecta el error
Llega 1100001 + 1: cambiaron 2 bits (el 2º y el 3º); hay 4 unos, par   →   NO lo detecta
```

### 6.1 Ejercicio extra 3

```
Posición 3 = 1, 5 = 0, 6 = 1, 7 = 1
p1 = paridad de (1, 0, 1) = 0
p2 = paridad de (1, 1, 1) = 1
p4 = paridad de (0, 1, 1) = 0
Palabra: p1 p2 d p4 d d d = 0 1 1 0 0 1 1   →   0110011
Llega 0110111:
  p1 revisa 1, 3, 5, 7 = 0, 1, 1, 1   →   tres unos, impar   →   falla
  p2 revisa 2, 3, 6, 7 = 1, 1, 1, 1   →   cuatro unos, par   →   bien
  p4 revisa 4, 5, 6, 7 = 0, 1, 1, 1   →   tres unos, impar   →   falla
Fallan p1 y p4   →   bit errado = 1 + 4 = 5   →   se invierte y queda 0110011 ✓
```

### 6.1 Ejercicio extra 4

**Causas.** Las perturbaciones del canal: la **atenuación** (la señal pierde amplitud y cerca del receptor se confunde con el ruido), la **distorsión** (el canal atenúa o retarda distinto cada frecuencia y deforma los pulsos, que se meten unos en otros) y el **ruido** (térmico, diafonía, intermodulación, impulsivo, que se suma a la señal y puede cambiar bits). Y las limitaciones: un **ancho de banda insuficiente** (se pierden armónicas y los pulsos llegan deformados) y una **tasa de información mayor que la capacidad** del canal (Shannon).

**Políticas.** Ignorar los errores (otra capa se ocupa), detectarlos y avisar, detectarlos y pedir la retransmisión (ARQ, con ACK y NAK) y detectarlos y corregirlos en el receptor (FEC, con códigos autocorrectores como Hamming).

### 6.1 Ejercicio extra 5

El **BER** es la relación entre los bits recibidos con error y el total de bits transmitidos: $BER = \text{bits erróneos} / \text{bits transmitidos}$. Mide la calidad de un canal digital. Ejemplos: 20 bits erróneos en 200.000 dan $10^{-4}$ (1 cada 10.000); en una LAN Ethernet se espera del orden de $10^{-9}$.

**CRC y checksum solo detectan.** El receptor recalcula el control y, si no coincide, sabe que el paquete tiene algún error, pero no cuáles son los bits erróneos. Por eso no pueden corregir: el paquete se descarta y se pide la retransmisión (ARQ). Para ubicar y corregir el bit hacen falta códigos autocorrectores, como Hamming (FEC).

### 6.1 Ejercicio extra 6

CRC: Ethernet, PPP, HDLC y Frame Relay. Suma de verificación: TCP, IP, UDP e ICMP. Los códigos correctores se usan cuando no se puede pedir la retransmisión del paquete dañado: por ejemplo, en una transmisión simplex, o cuando el retardo de ida y vuelta es muy grande.

### 6.1 Autoevaluación

```
1. BER = bits erróneos / bits transmitidos. El CRC solo dice que el bloque tiene algún
   error, no cuál bit está mal, así que no puede corregir: se descarta el bloque y se
   pide retransmisión (o se usa un código autocorrector como Hamming).

2. G = 1011, grado 3 → agregar 3 ceros: 1101000
   1101000
   1011            ← XOR
   ----
    110000
    1011           ← XOR
    ----
     11100
     1011          ← XOR
     ----
      1010
      1011         ← XOR
      ----
         1
   Resto = 001   →   se transmite 1101 001 = 1101001
```

### 6.2 Ejercicio guiado

```
Paso 1: qué es
  "Es el conjunto de parámetros que la red se compromete a cumplir para un tráfico:
   retardo de tránsito, variación del retardo, pérdida y tasa de errores, ancho de
   banda, y control de flujo y de errores."

Paso 2: con QoS
  La red clasifica el tráfico, lo prioriza y le reserva recursos.
  Ejemplo: Frame Relay o ATM (o IP con mecanismos de QoS).
  Ventaja: tráfico sensible priorizado y confiable.
  Desventaja: exige más a la red (procesamiento, configuración) y cuesta más.

Paso 3: sin QoS
  Mejor esfuerzo: la red hace lo posible, sin garantías; la aplicación valida.
  Ejemplo: IP básico, o UDP en las consultas DNS.
  Ventaja: simplicidad.  Desventaja: el tráfico sensible puede degradarse.
```

### 6.2 Práctica

```
1. Porque se reparten el trabajo: IP lleva cada paquete sin conexión (simple, en
   toda la red), y TCP arma la conexión confiable solo entre los dos extremos
   (confirma, reordena y retransmite).
2. El orientado al carácter delimita los mensajes con caracteres de control (BSC:
   STX, ETX) y depende del código; el orientado al bit usa una bandera (HDLC:
   01111110) e inserción de bits, así que transmite cualquier secuencia.
3. La voz y el video en tiempo real: necesitan poco retardo y poca variación del
   retardo; un paquete que llega tarde ya no sirve.
```

### 6.2 Autoevaluación

```
1. Gana confiabilidad (entrega ordenada y confirmada); pierde eficiencia (demora
   para establecer la conexión y bits de control).
2. Retardo, variación del retardo y pérdida de paquetes; por ejemplo, la voz sobre IP.
```
