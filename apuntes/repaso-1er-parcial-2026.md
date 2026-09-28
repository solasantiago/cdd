# Repaso urgente — 1er parcial (mañana 19hs, Argentina)

## ESTADO ACTUAL / DÓNDE RETOMAR

> Si sos Claude leyendo esto al empezar una sesión nueva: el estudiante tiene el **1er parcial de Comunicación de Datos mañana a las 19hs**, arrancó a estudiar el 27/09/2026 ~19:11 sin haber estudiado nada antes. Está seguiendo el horario de abajo. Retomá exactamente donde quedó marcado, sin repetir teoría ya vista. Sin símbolos LaTeX ($), todo en texto plano (consola). Ir tema a tema, con ejercicios guiados paso a paso, actualizando los % de avance.

- **Hora del parcial:** mañana 19:00 (hora Argentina).
- **Tema en curso:** Tema 1 — Cálculo de enlace.
- **Punto exacto donde quedó:** resolviendo el ejercicio guiado (ver abajo). Ya calculó Paso 1 (Ptx = 13 dBm). Estaba resolviendo el Paso 2 (presupuesto de pérdidas = 13 − (−20)). Falta confirmar ese resultado y seguir con el Paso 3 (distancia máxima).
- **Temas 2 a 6:** todavía no arrancados (Fourier/ancho de banda/velocidad/multinivel, Capacidad de canal, Códigos de banda base, Errores, Simulacro final).
- **Trackers de avance:**
  - % sobre temas ideales para aprobar (6 bloques de alto impacto): 0/6
  - % sobre total de temas del parcial (~20 sub-temas de lumen.json: u1, u2, u3, u5, u6): 0/20

## Horario

```
19:30–22:00 (2h30)  Tema 1: Cálculo de enlace + Tema 2: Fourier/ancho de banda/velocidad/multinivel
22:00–23:00 (1h)    Viaje (perdido)
23:00–01:00 (2h)    Tema 3: Capacidad de canal (Shannon/Nyquist) + tasa de información
01:00–07:00 (6h)    Dormir
07:00–09:00 (2h)    Repaso rápido de lo visto anoche (refuerza memoria)
09:00–11:00 (2h)    Tema 4: Códigos de banda base (Manchester, HDB3)
11:00–12:30 (1.5h)  Tema 5: Errores (CRC, paridad) — más memorístico
12:30–13:30 (1h)    Comida/descanso
13:30–17:00 (3.5h)  Simulacro tipo parcial con ejercicios reales de /fuentes, cronometrado
17:00–18:00 (1h)    Repaso de errores del simulacro + hoja de fórmulas
18:00–19:00 (1h)    Viaje al parcial
```

---

## Tema 1: Cálculo de enlace (Empezamos 19:30)

Tres ideas y nada más:

1. dBm es una forma de expresar una potencia absoluta en escala logarítmica, tomando como referencia 1 milivatio:
   `dBm = 10 * log10(P_mW / 1)`
2. dB (sin la "m") es una relación, no una potencia absoluta. Se usa para pérdidas y ganancias (ej: "el cable pierde 3 dB por km"). La ventaja de trabajar en dB/dBm es que en vez de multiplicar potencias, sumás y restás los dB (porque son logaritmos).
3. La cuenta del enlace es así: `Potencia que llega al receptor (dBm) = Potencia transmitida (dBm) − pérdidas (dB) + ganancias (dB)`. El enlace "funciona" mientras esa potencia que llega sea mayor o igual a la sensibilidad del receptor. La distancia máxima es la distancia donde justo se llega, ni un poco más.

Ptx = potencia de transmisión: la potencia con la que el equipo transmisor manda la señal al enlace, antes de las pérdidas por cable, conectores, etc.

### Ejemplo resuelto (Final 27/09/23)

Datos:
- Ptx = 10 mW
- Sensibilidad Rx = -17 dBm
- Un amplificador que amplifica x100
- Conectores de 1 dB c/u (Tx, Rx, entrada y salida del ampli = 4 conectores)
- Cable de 2 dB/km en bobinas de 5 km con empalmes de 1 dB entre bobinas (la última bobina no necesita empalme).

```
Ptx en dBm = 10 log(10/1) = 10 dBm
Amplificación = 100 veces = 20 dB
Potencia disponible para pérdidas = Ptx + Ampli − Sensibilidad = 10 + 20 − (−17) = 47 dB
Pérdida de conectores = 4 × 1 dB = 4 dB
Potencia disponible para cable+empalmes = 47 − 4 = 43 dB
Cada tramo de 5 km = 10 dB (cable) + 1 dB (empalme) = 11 dB
Con 3 empalmes + 1 última bobina sin empalme: 3×11 + 10 = 43 dB ✓
→ Distancia máxima = 4 bobinas × 5 km = 20 km
```

### Ejercicio guiado (EN CURSO — retomar acá)

Datos: Ptx = 20 mW · Sensibilidad Rx = -20 dBm · Atenuación = 3 dB/km · Sin amplificadores ni conectores.

```
Paso 1: pasar la potencia de transmisión a dBm
Ptx(dBm) = 10 * log10(20 / 1) = 10 * 1.30 = 13 dBm   [HECHO, confirmado por el estudiante]

Paso 2: presupuesto de pérdidas disponible
Presupuesto = Ptx(dBm) − Sensibilidad(dBm) = 13 − (−20) = ¿?  dB   [PENDIENTE DE CONFIRMAR]

Paso 3: distancia máxima
Distancia = Presupuesto / atenuación_por_km   [PENDIENTE]
```
