# Classroom "Comunicación de Datos - Práctica": índice de fuentes

> Relevado el 27/09/2026 desde el Google Classroom **"Sistemas – Comunicación de Datos - Práctica"** (publica: *UTN FRBA Comunicaciones*), pestañas **Tablón** y **Trabajo de clase**.
> Ubicación sugerida en el repo: `programa/classroom-practica.md`.
>
> **Para qué sirve**: es el catálogo de todo el material del Classroom, con un **ID de cita** por fuente. Cuando se generen apuntes, ejercicios o simulacros, citar con ese ID, p. ej. `[CP-TP3-P]`. Así se sabe de qué archivo sale cada cosa y se puede buscar en el Classroom o en una copia local.
>
> **Importante**: los archivos **no** están en el repo, porque es público y el material tiene derechos de autor (libros, apuntes de la cátedra). Si se descargan para trabajar en local, guardarlos en una carpeta ignorada por git (p. ej. `fuentes/`, agregada a `.gitignore`) y respetar el nombre de archivo original que figura acá.

## Resumen del Classroom

- **Qué es**: el aula de la **práctica** de la cátedra. Reúne bibliografía, guías de Trabajos Prácticos (TP1 a TP9) con sus resoluciones, clases prácticas virtuales, videos, parciales y finales resueltos, y material de teoría de dos docentes (Ing. Luis Sens e Ing. Alejandro Arroyo Arzubi).
- **Antigüedad**: casi todo se publicó en 2020 (cursada virtual) y hay agregados de 2022 a 2025. El último es "Clases Practicas", del 28 de mayo (sin año visible; sería de 2026). **No hay cronograma ni fechas de la cursada 2026**: las fechas de entrega que aparecen son de 2020 y el único cronograma es el de 2022 (curso K4573).
- **Bibliografía oficial**: *Castro – Fusario, Comunicaciones* (versión nueva, publicada en 2024 como "Bibliografía Oficial de la Cátedra"). También está *Teleinformática* de Castro–Fusario, la versión anterior en Tomos I y II. Complementaria: *Stallings, Comunicaciones y Redes de Computadores*, 6.ª ed.
- **Convenciones de los TPs**:
  - Cada TP tiene una guía de **Teoría** (preguntas) y otra de **Práctica** (ejercicios), cada una con su **Resolución** ("Respuestas").
  - En las guías, **las preguntas en azul son las obligatorias** para presentar el TP.
  - El formato de entrega está en "Presentación de los TPs – Formato" `[CP-FORMATO-TP]`.
- **Contacto para errores en las resoluciones**: la cátedra pide avisarlos al mail publicado en el Classroom (comunicacionesutnfrba@gmail.com).
- **Consejos que dejó la cátedra**:
  - El final del 27/09/2023 tomó temas del Primer Parcial `[CP-FINAL-2023-09-27]`.
  - En el 2.º parcial del 07/11/2023, el ejercicio de 16-QAM se planteaba con 2 amplitudes y 8 fases por amplitud, se resolvía como el PSK y pedía diagrama vectorial y asignación de fases en código Gray (resultado comentado: Vt = 9600 bps, Vm = 2400 baudios) `[CP-2P-2023-11-07]`.

### Secuencia de TPs y temas

| TP | Tema (según el Classroom) | Unidad(es) de `lumen.json` (aprox.) |
|:-:|---|---|
| 1 | Repaso de electricidad y circuitos. Introducción a la teleinformática y la red Internet | u1 |
| 2 | Transmisión de datos, ancho de banda, velocidad de modulación y de transmisión; simulación del efecto del ancho de banda en la forma de onda | u2, u3 |
| 3 | Cálculo de enlaces, unidades de medida | u2 |
| 4 | Transmisión banda base y tasa de información; señales banda base y moduladas; códigos (HDB3, Manchester) | u2, u5 |
| 5 | Capacidad de los canales; relación con la tasa de información | u5, u6 |
| 6 | Tratamiento de errores en redes de datos: detección, corrección, protocolos | u6, u3 |
| 7 | Medios físicos de comunicación | u7 |
| 8 | Modulación y multiplexación digital (incluye PCM) | u4 |
| 9 | Trabajo de diseño: proyecto de red de cableado estructurado (EIA/TIA 568) | u7 |

---

## 1. Tablón

Todas las publicaciones son de *UTN FRBA Comunicaciones*.

### 1.1 Bibliografía oficial de la cátedra (22/08/2024)
| ID | Archivo | Nota |
|---|---|---|
| `[CP-LIBRO-CF]` | Castro-Fusario - Comunicaciones LIBRO DIGITAL.pdf | Libro, versión nueva. Bibliografía principal |

### 1.2 Presentación de los TPs – Formato (11/04/2020, mod. 18/04/2020)
| ID | Archivo |
|---|---|
| `[CP-FORMATO-TP]` | Presentacion de los TPs - Formato.pdf |

### 1.3 Conceptos básicos necesarios para la resolución de los TPs (11/04/2020, mod. 18/04/2020)
| ID | Archivo | Unidad |
|---|---|---|
| `[CP-CB-I]` | I - Introduccion y Señales.pdf | u1, u2 |
| `[CP-CB-II]` | II - Fourier y Velocidades.pdf | u2, u3 |
| `[CP-CB-III]` | III - Unidades de medida y Ancho de Banda.pdf | u2 |
| `[CP-CB-IV]` | IV - Banda Base.pdf | u2 |

### 1.4 Apuntes de la teoría – Ing. Luis Sens (18/04/2020, mod. 14/04/2021)
| ID | Archivo | Unidad (aprox.) |
|---|---|---|
| `[CP-SENS-TP1]` … `[CP-SENS-TP5]` | Comunicaciones-TP1.pdf … Comunicaciones-TP5.pdf | enunciados (mismos que `[CP-TP-OF-n]`) |
| `[CP-SENS-C01]` | Clase 1a Conceptos.pdf | u1 |
| `[CP-SENS-C02]` | Clase 2b Señales.pdf | u2 |
| `[CP-SENS-C03]` | Clase 03b Señales.pdf | u2 |
| `[CP-SENS-C04]` | Clase 4c Unidades.pdf | u2 |
| `[CP-SENS-C05]` | Clase 5b Banda base.pdf | u2 |
| `[CP-SENS-C06]` | Clase 6a Informacion.pdf | u5 |
| `[CP-SENS-C07]` | Clase 7a Medios.pdf | u7 |
| `[CP-SENS-C08]` | Clase 8a Medios.pdf | u7 |
| `[CP-SENS-C09]` | Clase 9a Modulacion.pdf | u4 |
| `[CP-SENS-C10]` | Clase 10a Transporte.pdf | u4 |
| `[CP-SENS-C11]` | Clase 11a Redes.pdf | u3 |
| `[CP-SENS-C12]` | Clase 12b Capa fisica.pdf | u8 |
| `[CP-SENS-C13]` | Clase 13a Redes.pdf | u3 |

### 1.5 Teleinformática de Castro y Fusario, Tomos I y II (versión anterior) (11/04/2020)
| ID | Archivo |
|---|---|
| `[CP-TELE-T1]` | Teleinformatica de Castro Tomo I.pdf |
| `[CP-TELE-T2]` | Teleinformatica de Castro Tomo II.pdf |

### 1.6 Teleinformática de Castro y Fusario, Tomo I (versión anterior, por capítulos) (12/04/2020)
| ID | Archivo |
|---|---|
| `[CP-TELE-CAP02]` | Castro 02 - Final.pdf |
| `[CP-TELE-CAP03]` | Castro 03 - Final.pdf |

### 1.7 Teleinformática de Castro y Fusario, resúmenes (versión anterior) (11/04/2020)
| ID | Archivo |
|---|---|
| `[CP-RES-01]` … `[CP-RES-06]` | Resumen Capitulo Nro 1.pdf … Resumen Capitulo Nro 6.pdf |
| `[CP-RES-07A]` / `[CP-RES-07B]` / `[CP-RES-07C]` | Resumen Capitulo Nro 7 Parte A.pdf / Parte B.pdf / Parte C.pdf |
| `[CP-RES-08]` … `[CP-RES-10]` | Resumen Capitulo Nro 8.pdf … Resumen Capitulo Nro 10.pdf |

### 1.8 Castro y Fusario, diapositivas (versión nueva) (11/04/2020)
| ID | Archivo |
|---|---|
| `[CP-DIAPO-01]` … `[CP-DIAPO-08]` | Capitulo_1.pdf … Capitulo_8.pdf (8 archivos, uno por capítulo) |

### 1.9 Stallings (11/04/2020)
| ID | Archivo |
|---|---|
| `[CP-STALLINGS]` | Comunicaciones y Redes de Computadores (W. Stallings - 6º Edicion).pdf |

---

## 2. Trabajo de clase

Ordenado por tema, como en el Classroom (de arriba hacia abajo).

### 2.1 Sin tema
| ID | Material (fecha) | Descripción | Archivos |
|---|---|---|---|
| `[CP-16PSK-16QAM]` | Comparación 16-PSK vs 16-QAM (17/06/2025) | Información generada con Python | Comparacion_16PSK_vs_16QAM.docx |
| `[CP-FINAL-2023-09-27]` | Final 27 de Set 2023 (28/09/2023) | "En este final se tomaron temas que entran en el Primer Parcial" | Final de Comunicaciones - 27 de Set.pdf |
| `[CP-VID-MANCH]` | Código Manchester y Manchester Diferencial (28/09/2023) | Video breve: Manchester, Manchester Diferencial y HDB3 | Manchester y Manchester Diferencial.mp4 |
| `[CP-TIPO-PARCIAL]` | Ejercicios Tipo Parcial y Final (mod. 25/09/2022) | Adicionales a la cartilla de TP | 2020 Primer Parcial.pdf; Final COMUNICACIONES 06Set2022.pdf |
| `[CP-CV-2022]` | Práctica – Clases Virtuales (mod. 24/08/2022) | Todas las clases virtuales | Clase TP Nro 2 final.pdf; Clase TP Nro 3 final.pdf; Clase TP Nro 4.pdf; Clase Consulta TP Nro 4 Codigos Banda Base final.pdf; Clase TP Nro 5.pdf; Clase TP Nro 6.pdf; Clase TP Nro 7.pdf; Clase TP Nro 8.pdf; 2020 Primer Parcial - Consulta.pdf |
| `[CP-TP-OF-1]` … `[CP-TP-OF-5]` | Trabajos Prácticos – Oficial (11/04/2020) | Enunciados originales de la cátedra | Comunicaciones-TP1.pdf … Comunicaciones-TP5.pdf |

### 2.2 Play List – Práctica
| ID | Material (fecha) | Recurso |
|---|---|---|
| `[CP-PLAYLIST]` | Play List - Practica (29/08/2024) | YouTube: https://www.youtube.com/playlist?list=PL3LDWR5IrXNrwnbJ-cA9VrzDDI6lbMqKO |

### 2.3 Clases Prácticas
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-CP-2026]` | Clases Practicas (28/05, sin año visible) | Clase Nro 2.pdf … Clase Nro 8.pdf; Clase Nro 7 - Ejercicio Nro 10.pdf; Clase Nro 8 - PCM.pdf |

### 2.4 Más Práctica 2025
| ID | Material (fecha) | Descripción | Archivos |
|---|---|---|---|
| `[CP-EJ-2025-05-06]` | Ejercicios 06 mayo 2025 (06/05/2025) | 1er parcial; cálculo de atenuación de la tabla sin la frecuencia | 1ER PARCIAL COMUNICACIONES .pdf; Calcular para 250 Mhz.pdf |

### 2.5 Parciales y Finales Arroyo Arzubi
| ID | Material (fecha) | Descripción | Archivos |
|---|---|---|---|
| `[CP-2P-2023-11-07]` | 2do Parcial - 07 Nov 2023 - Ejercicio (mod. 09/11/2023) | Solución del ejercicio 16-QAM (ver consejo en el resumen), firmado "JCL" | 2do Parcial 2023 2Q - Ejercicio - Solucion.png |
| `[CP-ARROYO-PF]` | Parciales y Finales Arroyo Arzubi (30/09/2023) | Parciales y finales desarrollados por el Ing. Arroyo Arzubi | 1er_Parcial_2022_Arroyo.pdf; 2do_Parcial_2022_Arroyo.pdf; Final 201909.pdf; Final 202012.pdf; Final 202102.pdf; Final 202209.pdf; Final 202302.pdf |

### 2.6 Material para la Práctica
| ID | Material (fecha) | Descripción | Archivos |
|---|---|---|---|
| `[CP-MP-TP1]` … `[CP-MP-TP5]` | Material para la Practica (28/09/2023) | Conceptos teóricos para la práctica, TP1 a TP5 | TP Nro 1 Introducción a la Teleinformática bis.pdf; TP Nro 2 BIS COMUNICACIONES AV - Fourier.pdf; TP Nro 2 COMUNICACIONES 1ra Parte.pdf / 2da Parte.pdf / 3ra Parte.pdf / 4ta Parte.pdf; TP Nro 3 CALCULO DE ENLACE.pdf; TP Nro 4 CODIFICACION Y TEORIA INFO.pdf; TP Nro 5 CAPACIDAD DE UN CANAL.pdf |

### 2.7 Práctica Virtual 2Q – 2023
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-PV-2023]` | Practica Virtual 2Q - 2023 (07/09/2023) | Clase Nro 2.pdf … Clase Nro 8.pdf; Clase Nro 7 - Ejercicio Nro 10.pdf; Clase Nro 8 - PCM.pdf (mismos nombres que `[CP-CP-2026]`) |

### 2.8 Teoría de la Materia – Ing. Alejandro Arroyo Arzubi (todo del 24/08/2022)
| ID | Material | Archivos | Unidad (aprox.) |
|---|---|---|---|
| `[CP-CRONO-2022]` | Cronograma de Comunicaciones Año 2022 2Q - K4573 | Cronograma de Comunicaciones Año 2022 -K4573.pdf | — (referencia de ritmo de cursada) |
| `[CP-INVESTIG-2022]` | Trabajos de investigación 2022 - 2Q | Trabajos de investigación 2022.pdf | — |
| `[CP-AA-UT1]` | UT 1 Introducción a la teleinformática y a las redes | Clase 1.pdf | u1 |
| `[CP-AA-UT2]` | UT 2 Transmisión de datos | Clase 2.pdf; Clase 3.pdf | u2, u3 |
| `[CP-AA-UT3]` | UT 3 Interfases digitales y Unidades de Transmisión | Clase 4.pdf; Clase 4 Bis.pdf | u8, u2 |
| `[CP-AA-UT4]` | UT 4 Señales de Banda Base e Introducción a TI | Clase 5.pdf | u2, u5 |
| `[CP-AA-UT5]` | UT 5 Canales de Comunicaciones | Clase 6.pdf | u6 |
| `[CP-AA-UT6]` | UT 6 Tratamiento de Errores | Clase 6 Bis.pdf | u6 |
| `[CP-AA-UT7G]` | UT 7 Medios de Comunicaciones – Guiados | Clase 7.pdf; Armado de cables.pdf; cableado.pdf; certificacion.pdf; Mediciones y certificaciones.pdf | u7 |
| `[CP-AA-UT7NG]` | UT 7 Medios de Comunicaciones – No Guiados | Clase 8.pdf | u7 |
| `[CP-AA-UT8-MOD]` | UT 8 Modulación y tecnologías de transporte de señales – Modulación | Clase 9.pdf | u4 |
| `[CP-AA-UT8-MODEM]` | UT 8 … – Módems | Clase 9bis.pdf | u8 |
| `[CP-AA-UT8-MUX]` | UT 8 … – Multiplexores | Clase 10.pdf | u4 |
| `[CP-AA-UT9]` | UT 9 Redes de Telecom | Clase 11.pdf | u3 |

> La numeración "UT" de Arroyo Arzubi (2022) **no coincide** con la de las unidades del programa 2023 de `lumen.json`. Usar la columna "Unidad" para relacionarlas.

### 2.9 Proyecto de una red de cableado estructurado (TP 9)
| ID | Material (fecha) | Descripción | Archivos |
|---|---|---|---|
| `[CP-TP9-TAREA]` | Tarea: TP Nro 9 – Trabajo de diseño (entrega 06/07/2020) | Diseño físico de una LAN según EIA/TIA 568 y la estructura edilicia dada. Conocimiento previo: norma EIA/TIA 568 | (consigna en la tarea) |
| `[CP-TP9-P]` | Trabajo Practico Nro. 9 - Practica (mod. 22/06/2020) | Ídem | Comunicaciones-TP9.pdf |
| `[CP-PLIEGOS]` | Modelos de Pliegos (mod. 14/10/2022) | Pliegos reales de cableado estructurado (ONTI/ETAP) | pliego_cableado_estructurado_etap_v23.0_modelo_9.doc / .pdf; ETAP-redes-v17-Circuito Cerrado TV.pdf; NACER2-122-LPN-B-Pliego-Ver_ETAP.pdf; PE-DIS-MEGC-DGAR-661-17-ANX_GobCABA.pdf; Pliego lic privada 8-19 conectividad.pdf; MD Cableado Estructurado.rar. Links: argentina.gob.ar/jefatura/innovacion-publica/onti (documentos ETAP v25, estándares de cableado estructurado) y comprar.gob.ar |

### 2.10 Modulación, multiplexación digital (TP 8)
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-TP8-ADIC]` | TP Nro 8 – Ejercicios Adicionales (10/06/2022): modulación PCM | Parte Practica - Nro 8 - Bis.pdf |
| `[CP-TP8-P]` | TP Nro 8 – Práctica (10/06/2020) | GUIA TP Nro 8 - Practica Preguntas.pdf |
| `[CP-TP8-T]` | TP Nro 8 – Teoría (10/06/2020) | GUIA TP Nro 8 - Teoria Preguntas.pdf |
| `[CP-TP8-T-R]` | TP Nro 8 – Teoría – Resolución (10/06/2020) | GUIA TP Nro 8 - Teoria Preguntas Respuestas.pdf |

### 2.11 Medios físicos de comunicación (TP 7)
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-TP7-TAREA]` | Tarea: TP Nro 7 – Práctica y Teoría (entrega 10/06/2020) | — |
| `[CP-TP7-P]` | TP Nro 7 – Práctica (03/06/2020) | GUIA TP Nro 7 - Practica Preguntas.pdf |
| `[CP-TP7-T]` | TP Nro 7 – Teoría (03/06/2020) | GUIA TP Nro 7 - Teoria Preguntas.pdf |
| `[CP-TP7-T-R]` | TP Nro 7 – Teoría – Resolución (03/06/2020) | GUIA TP Nro 7 - Teoria Preguntas Respuestas.pdf |

### 2.12 Tratamiento de los errores en las redes de datos (TP 6)
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-TP6-P-R]` | Resolución del TP Nro 6 – Práctica (06/05/2022) | GUIA TP Nro 6 - Practica Preguntas Respuestas.pdf |
| `[CP-TP6-TAREA]` | Tarea: TP Nro 6 – Práctica y Teoría (entrega 19/05/2020): detección y corrección de errores, protocolos y política de tratamiento de errores | — |
| `[CP-TP6-P]` | TP Nro 6 – Práctica (09/05/2020) | GUIA TP Nro 6 - Practica Preguntas.pdf |
| `[CP-TP6-T]` | TP Nro 6 – Teoría (09/05/2020) | GUIA TP Nro 6 - Teoria Preguntas.doc |
| `[CP-TP6-T-R]` | TP Nro 6 – Teoría – Resolución (09/05/2020) | GUIA TP Nro 6 - Teoria Preguntas Respuestas.pdf |

### 2.13 TP Nro 5 – Videos
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-TP5-VID]` | TP Nro. 5 - Videos Ejercicios 1 al 7 (30/09/2023) | TP Nro 5 - Ejercicio Nro 1.mp4 … Ejercicio Nro 7.mp4 |

### 2.14 Capacidad de los canales. Relación con la tasa de información (TP 5)
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-TP5-P-R]` | Resolución del TP Nro 5 – Práctica (06/05/2022) | GUIA TP Nro 5 - Practica Respuestas.pdf |
| `[CP-TP5-TAREA]` | Tarea: TP Nro 5 – Práctica y Teoría (entrega 13/05/2020) | — |
| `[CP-TP5-P]` | TP Nro 5 – Práctica (mod. 03/05/2020) | GUIA TP Nro 5 - Practica Preguntas.pdf |
| `[CP-TP5-T]` | TP Nro 5 – Teoría (03/05/2020) | GUIA TP Nro 5 - Teoria Preguntas.pdf |
| `[CP-TP5-T-R]` | TP Nro 5 – Teoría – Resolución (03/05/2020) | GUIA TP Nro 5 - Teoria Respuestas.pdf |

### 2.15 Transmisión banda base y tasa de información (TP 4)
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-VID-BB]` | Códigos Banda Base – HDB3 – Manchester y Manchester Diferencial (14/09/2023) | HDB3 Codificacion de senal Digital.mp4; Manchester y Manchester Diferencial.mp4 |
| `[CP-TP4-P-R]` | Resolución del TP Nro 4 – Práctica (06/05/2022) | GUIA TP Nro 4 - Practica Respuestas.pdf |
| `[CP-TP4-TAREA]` | Tarea: TP Nro 4 – Práctica y Teoría (entrega 06/05/2020): señales banda base y moduladas; tasa de información de fuentes | — |
| `[CP-TP4-P]` | TP Nro 4 – Práctica (26/04/2020) | GUIA TP Nro 4 - Practica Preguntas.pdf |
| `[CP-TP4-T]` | TP Nro 4 – Teoría (26/04/2020) | GUIA TP Nro 4 - Teoria Preguntas.pdf |
| `[CP-TP4-T-R]` | TP Nro 4 – Teoría – Resolución (29/04/2020) | GUIA TP Nro 4 - Teoria Respuestas.pdf |

### 2.16 Cálculo de Enlace (TP 3)
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-TP3-P-R]` | Resolución del TP Nro 3 – Práctica (06/05/2022) | GUIA TP Nro 3 - Practica Respuestas - final.pdf |
| `[CP-TP3-TAREA]` | Tarea: TP Nro 3 – Práctica (entrega 29/04/2020): cálculo de enlaces, unidades de medida | — |
| `[CP-TP3-P]` | TP Nro 3 – Práctica (18/04/2020) | GUIA TP Nro 3 - Practica Preguntas.pdf |

### 2.17 Velocidad de Modulación y Transmisión (TP 2)
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-TP2-P-R]` | Resolución del TP Nro 2 – Práctica (06/05/2022) | GUIA TP Nro 2 - Practica Respuestas 2P.pdf |
| `[CP-TP2-TAREA]` | Tarea: TP Nro 2 – Práctica y Teoría (entrega 22/04/2020): transmisión de datos, ancho de banda, Vm y Vt; simulación del efecto del ancho de banda | — |
| `[CP-TP2-P1]` | TP Nro 2 – Práctica (Primera Parte) (mod. 21/04/2020) | GUIA TP Nro 2 - Practica Preguntas 1P.pdf |
| `[CP-TP2-P2]` | TP Nro 2 – Práctica (Segunda Parte) (11/04/2020) | GUIA TP Nro 2 - Practica Preguntas 2P.pdf |
| `[CP-TP2-T]` | TP Nro 2 – Teoría (11/04/2020) | GUIA TP Nro 2 - Teoria Preguntas.pdf |
| `[CP-TP2-P1-R]` | TP Nro 2 – Práctica (Primera Parte) – Resolución (21/04/2020) | GUIA TP Nro 2 - Practica Respuestas 1P.pdf |
| `[CP-TP2-T-R]` | TP Nro 2 – Teoría – Resolución (mod. 26/04/2020) | GUIA TP Nro 2 - Teoria Respuestas.pdf |

### 2.18 Repaso Electricidad y Circuitos. Introducción Teleinformática (TP 1)
| ID | Material (fecha) | Archivos |
|---|---|---|
| `[CP-TP1-TAREA]` | Tarea: TP Nro 1 – Práctica y Teoría (entrega 18/04/2020): repaso de electricidad y circuitos; introducción a la teleinformática e Internet | — |
| `[CP-TP1-P]` | TP Nro 1 – Práctica (11/04/2020) | GUIA TP Nro 1 - Practica Preguntas.pdf |
| `[CP-TP1-P-R]` | TP Nro 1 – Práctica – Resolución (mod. 21/04/2020) | GUIA TP Nro 1 - Practica Respuestas.pdf |
| `[CP-TP1-T]` | TP Nro 1 – Teoría (mod. 11/04/2020) | GUIA TP Nro 1 - Teoria Preguntas.pdf |
| `[CP-TP1-T-R]` | TP Nro 1 – Teoría – Resolución (21/04/2020) | GUIA TP Nro 1 - Teoria Respuestas.pdf |

---

## 3. Guía rápida para el agente (uso en local)

- **Para explicar un tema**, priorizar:
  1. `[CP-LIBRO-CF]`, el libro oficial.
  2. Los apuntes de clase de Sens (`[CP-SENS-Cnn]`) o de Arroyo Arzubi (`[CP-AA-UTn]`).
  3. "Conceptos básicos" (`[CP-CB-*]`) y "Material para la práctica" (`[CP-MP-*]`).
- **Para ejercicios**: la guía de práctica del TP (`[CP-TPn-P]`) y su resolución (`[CP-TPn-P-R]`). Después, las clases prácticas (`[CP-CP-2026]`, `[CP-PV-2023]`, `[CP-CV-2022]`) y los videos (`[CP-TP5-VID]`, `[CP-VID-BB]`).
- **Para simulacros tipo parcial y final**: `[CP-ARROYO-PF]`, `[CP-TIPO-PARCIAL]`, `[CP-FINAL-2023-09-27]`, `[CP-EJ-2025-05-06]` y `[CP-2P-2023-11-07]`.
- **Cómo citar**: en apuntes y ejercicios propios, citar el ID y, si aplica, la página o el número de ejercicio, p. ej. `[CP-TP3-P, ej. 4]`. Redactar con palabras propias, sin copiar texto del material.
- **Pendiente**: cronograma 2026, fechas de parciales y régimen de aprobación. No están en este Classroom; pedirlos al estudiante o buscarlos en el aula de teoría.
