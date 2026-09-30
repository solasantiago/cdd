# Comunicación de Datos: guía de estudio

El libro de la materia, en el orden de la cursada 2026: un capítulo por TP, cada uno en su archivo. Cada bloque es un tipo de ejercicio o de pregunta que toman, con teoría mínima, un ejemplo real resuelto, un ejercicio guiado, práctica y un cierre para memorizar y autoevaluarte. Las respuestas están al final de cada capítulo. Para imprimir: `python3 guia-pdf.py [capítulos]` (queda en `guias/pdf/`).

## Índice

Las estrellas dicen cuánto aparece cada bloque en los parciales reales relevados:
- **Capítulos 1 a 6** (1er parcial): 8 parciales. Son los Temas 1 a 4 (Classroom, 2020), el 2020 2Q, el 2022 de Arroyo Arzubi, el del 08/10/2024 y el de esta cursada (28/09/2026, Tema B).
- **Bloque 6.2 y capítulos 7 a 9** (2do parcial): 4 parciales. Son los Temas 1 y 2 de 2020, el 2022 de Arroyo Arzubi y el de 2023, del que solo se conoce el ejercicio de 16-QAM.

📌 2026 marca lo que se tomó en el parcial de esta cursada.

| Capítulo | Bloque | Frecuencia | Estado |
|---|---|:-:|---|
| [1. Introducción a la teleinformática e Internet](cap-01-introduccion.md) (TP 1) | 1.1 Teleinformática, redes, OSI e Internet | ★★☆☆☆ (2 de 8) | listo |
| [2. Transmisión de datos](cap-02-transmision.md) (TP 2) | 2.1 Velocidades, multinivel y sincronismo 📌 2026 | ★★★★☆ (5 de 8) | listo |
| | 2.2 Fourier del tren de pulsos y ancho de banda 📌 2026 | ★★★★☆ (5 de 8) | listo |
| | 2.3 Señales y modos de transmisión | ☆☆☆☆☆ (0 de 8) | listo |
| [3. Cálculo de enlaces e interfaces](cap-03-enlace.md) (TP 3) | 3.1 Cálculo de enlace 📌 2026 | ★★★★★ (8 de 8) | listo |
| | 3.2 Interfaces de capa física | ★★☆☆☆ (2 de 8) | listo |
| [4. Banda base y tasa de información](cap-04-banda-base.md) (TP 4) | 4.1 Códigos banda base 📌 2026 | ★★☆☆☆ (2 de 8) | listo |
| | 4.2 Información, entropía y tasa de información | ★★★★☆ (5 de 8) | listo |
| [5. Capacidad de los canales](cap-05-capacidad.md) (TP 5) | 5.1 Capacidad: Nyquist y Shannon 📌 2026 | ★★★★☆ (5 de 8) | listo |
| | 5.2 Atenuación, distorsión y ruido | ☆☆☆☆☆ (0 de 8) | listo |
| [6. Tratamiento de errores y protocolos](cap-06-errores.md) (TP 6) | 6.1 Detección y corrección de errores 📌 2026 | ★★☆☆☆ (3 de 8) | listo |
| | 6.2 Protocolos: conexión y calidad de servicio | ★★★☆☆ (2 de 4) | listo |
| [7. Medios físicos](cap-07-medios.md) (TP 7) | 7.1 Medios de cobre: par trenzado y coaxil | ★★★☆☆ (2 de 4) | listo |
| | 7.2 Fibra óptica | ★★★★☆ (3 de 4) | listo |
| | 7.3 Radioenlaces, antenas y satélites | ★★★☆☆ (2 de 4) | listo |
| [8. Cableado estructurado](cap-08-cableado.md) (TP 8) | 8.1 Estructura y diseño (EIA/TIA 568) | ☆☆☆☆☆ (0 de 4) | listo |
| | 8.2 Armado y certificación | ☆☆☆☆☆ (0 de 4) | listo |
| [9. Modulación, PCM y multiplexación](cap-09-modulacion.md) (TP 9) | 9.1 Modulación analógica: AM, FM y PM | ★★☆☆☆ (1 de 4) | listo |
| | 9.2 Modulación digital: ASK, FSK, PSK y QAM | ★★★★★ (4 de 4) | listo |
| | 9.3 PCM: digitalización de señales | ★★☆☆☆ (1 de 4) | listo |
| | 9.4 Multiplexación: FDM, TDM, PDH y SDH | ★★★☆☆ (2 de 4) | listo |

## Cursada 2026

Según la planificación del curso K3571, 2º cuatrimestre de 2026 (teoría los lunes, práctica los miércoles, 19 h; docentes: Fusario, Buscaglia y Leppen):

- **Orden de los TP:** 1 introducción, 2 transmisión de datos, 3 cálculo de enlaces, 4 banda base y tasa de información, 5 capacidad de canales (con la teoría de errores), 6 errores y protocolos, 7 medios físicos, **8 cableado estructurado** y **9 modulación, PDH, SDH y SONET**. En 2020 los TP 8 y 9 iban al revés: las guías viejas de modulación dicen "TP 8".
- **Parciales:** dos, presenciales, con problemas, puntos teóricos a desarrollar y/o multiple choice. El 1er parcial fue el lunes 28/09 (semana 8). El **2do parcial es en la semana 12, lunes 26/10**.
- **Recuperatorios:** dos por parcial, presenciales, los miércoles de las semanas 13 a 16. Por las semanas de la planificación: el 1er recuperatorio del 1er parcial sería el **04/11** y el 2do, el **11/11**; los del 2do parcial, el **18/11** y el **25/11**. (Las fechas salen de contar semanas desde el 1er parcial: confirmalas con la cátedra).
- **Aprobación:** cada instancia se califica de 1 a 10 y se aprueba con 6. **Regularizar:** asistir a las clases virtuales, aprobar los dos parciales (o sus recuperatorios) y aprobar el 75 % de los TP, subidos en forma individual. **Promoción:** 8 o más en los dos parciales, o en un recuperatorio de un solo parcial. Si no se promociona, final presencial.

## Modalidad 2026

El 1er parcial de esta cursada (28/09/2026, Tema B) tuvo 7 ítems, sobre 10 puntos:

- **4 preguntas de teoría, de 1 punto cada una:**
  - Deducir Shannon-Hartley a partir de la capacidad del canal ideal (Nyquist), con sus parámetros y las unidades para que dé bits/s (5.1).
  - Las cuatro causas de errores y las políticas de tratamiento de errores (6.1).
  - Qué es el BER y si CRC y checksum solo detectan o también corrigen (6.1).
  - Qué relación tiene la transmisión multinivel con el ancho de banda y la velocidad (2.1).
- **3 problemas, de 2 puntos cada uno:**
  - Potencia necesaria en un enlace con amplificador (3.1).
  - Espectro de Fourier con gráfico, ancho de banda, cantidad de armónicas y Cn máximo (2.2).
  - Manchester y Manchester diferencial dibujados, y qué ventajas dan y por qué (4.1).
- **La consigna avisa** que un ítem suma solo si está completo y correcto, y que "la interpretación es parte de la evaluación".

Frente a los parciales viejos cambian tres cosas: hay mucha más teoría (4 de 7 ítems), la teoría pide razonar (deducir, relacionar, justificar) y no solo definir, y los problemas piden gráficos y el porqué.

**Qué esperar** (es una inferencia, no algo que haya dicho la cátedra):
- **Recuperatorio:** la misma estructura y los mismos capítulos (1 a 6).
- **2do parcial:** probablemente también teoría razonada más problemas con gráfico. Los 2dos parciales viejos son casi todo teoría y cálculos cortos, y el único problema fijo es la modulación digital con diagrama vectorial (PSK o QAM, con código Gray), que apareció en todos.

## Ruta del recuperatorio (capítulos 1 a 6)

Primero lo que se tomó en 2026, después el resto por estrellas:

1. 📌 3.1 Cálculo de enlace ★★★★★: problema.
2. 📌 2.2 Fourier ★★★★☆: problema con gráfico del espectro.
3. 📌 4.1 Códigos banda base ★★☆☆☆: problema con dibujo y ventajas.
4. 📌 2.1 Velocidades y multinivel ★★★★☆: teoría (multinivel, ancho de banda y velocidad).
5. 📌 5.1 Capacidad ★★★★☆: teoría (deducir Shannon desde Nyquist). Va después de 2.1 porque la usa.
6. 📌 6.1 Errores ★★☆☆☆: teoría (causas, políticas, BER, detectar o corregir).
7. 4.2 Información y tasa de información ★★★★☆.
8. 1.1 Teleinformática y OSI ★★☆☆☆ y 3.2 Interfaces ★★☆☆☆.
9. 2.3 Señales y modos ☆☆☆☆☆ y 5.2 Perturbaciones ☆☆☆☆☆.

## Ruta del 2do parcial (6.2 y capítulos 7 a 9)

Por estrellas sobre los 2dos parciales. Cuando se sepa cómo fue el de esta cursada, se marca con 📌 y se reordena:

1. 9.2 Modulación digital ★★★★★: problema con diagrama vectorial y código Gray.
2. 7.2 Fibra óptica ★★★★☆: teoría (pérdidas, ventanas, LED y láser).
3. 7.3 Radioenlaces ★★★☆☆: cálculos cortos (antenas, bandas, retardo del satélite).
4. 9.4 Multiplexación ★★★☆☆: el E1 a partir de PCM, SDH contra PDH. Va después de 9.3, porque usa PCM.
5. 7.1 Medios de cobre ★★★☆☆ y 6.2 Protocolos ★★★☆☆: teoría.
6. 9.3 PCM ★★☆☆☆ y 9.1 Modulación analógica ★★☆☆☆.
7. 8.1 y 8.2 Cableado estructurado ☆☆☆☆☆: no apareció en los viejos, pero es el TP 8 de esta cursada.

En los 2dos parciales viejos también aparecieron temas del 1er parcial: el CRC (6.1) y las capas del OSI con la encriptación (1.1), ambos en 2022.
