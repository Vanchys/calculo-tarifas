# Tarifas con recargo de lluvia — Calculadora de Tarifas

Este documento muestra las mismas tarifas de [TARIFAS.md](TARIFAS.md) pero con el recargo por lluvia aplicado. **Este archivo es solo de referencia visual — el recargo aún no está implementado en `index.html`.**

## Criterio del recargo (definido junto al usuario)

| Tramo | Recargo |
|-------|---------|
| Sub-mínimo (0.0 – 1.3 km) | **+$3** fijos |
| Mínimo estándar (1.31 – 1.7 km) | **+$4** fijos |
| Tabla fija (1.7 km → tope base) | **+$1 cada 0.5 km** acumulado desde 1.7 km |
| Cálculo por km (tope base → 17.0 km) | **+$2/km** adicional (equivalente a $1 cada 0.5 km) |
| Foráneo (17.01 – 200 km) | **Sin cambio** — el recargo de lluvia solo aplica a tarifas de ciudad (0–17 km) |

---

## 1. Tramos urbanos con lluvia (0.0 km – 17.0 km)

### Tramo 1 — Sub-mínimo (0.0 – 1.3 km)

| Horario    | Precio normal | Con lluvia (+$3) |
|------------|----------------|--------------------|
| Día        | $34 MXN        | **$37 MXN**        |
| Noche      | $37 MXN        | **$40 MXN**        |
| Madrugada  | $40 MXN        | **$43 MXN**        |

### Tramo 2 — Mínimo estándar (1.31 – 1.7 km)

| Horario    | Precio normal | Con lluvia (+$4) |
|------------|----------------|--------------------|
| Día        | $39 MXN        | **$43 MXN**        |
| Noche      | $42 MXN        | **$46 MXN**        |
| Madrugada  | $45 MXN        | **$49 MXN**        |

### Tramo 3 — Tabla fija con lluvia (1.7 km → tope base)

El recargo crece $1 cada 0.5 km acumulado desde 1.7 km (1.7–2.1 km = +$1, 2.2–2.6 km = +$2, 2.7–3.1 km = +$3, y así sucesivamente).

<details>
<summary>Tabla completa — Día con lluvia (1.7 – 7.2 km)</summary>

| km  | Normal | Recargo | Con lluvia |
|-----|--------|---------|------------|
| 1.7 | 39 | +1 | 40 |
| 1.8 | 40 | +1 | 41 |
| 1.9 | 41 | +1 | 42 |
| 2.0 | 42 | +1 | 43 |
| 2.1 | 43 | +1 | 44 |
| 2.2 | 44 | +2 | 46 |
| 2.3 | 45 | +2 | 47 |
| 2.4 | 46 | +2 | 48 |
| 2.5 | 47 | +2 | 49 |
| 2.6 | 48 | +2 | 50 |
| 2.7 | 49 | +3 | 52 |
| 2.8 | 50 | +3 | 53 |
| 2.9 | 51 | +3 | 54 |
| 3.0 | 52 | +3 | 55 |
| 3.1 | 53 | +3 | 56 |
| 3.2 | 54 | +4 | 58 |
| 3.3 | 55 | +4 | 59 |
| 3.4 | 56 | +4 | 60 |
| 3.5 | 57 | +4 | 61 |
| 3.6 | 58 | +4 | 62 |
| 3.7 | 59 | +5 | 64 |
| 3.8 | 60 | +5 | 65 |
| 3.9 | 61 | +5 | 66 |
| 4.0 | 62 | +5 | 67 |
| 4.1 | 63 | +5 | 68 |
| 4.2 | 64 | +6 | 70 |
| 4.3 | 65 | +6 | 71 |
| 4.4 | 66 | +6 | 72 |
| 4.5 | 67 | +6 | 73 |
| 4.6 | 68 | +6 | 74 |
| 4.7 | 69 | +7 | 76 |
| 4.8 | 70 | +7 | 77 |
| 4.9 | 71 | +7 | 78 |
| 5.0 | 72 | +7 | 79 |
| 5.1 | 73 | +7 | 80 |
| 5.2 | 74 | +8 | 82 |
| 5.3 | 75 | +8 | 83 |
| 5.4 | 76 | +8 | 84 |
| 5.5 | 77 | +8 | 85 |
| 5.6 | 78 | +8 | 86 |
| 5.7 | 79 | +9 | 88 |
| 5.8 | 80 | +9 | 89 |
| 5.9 | 81 | +9 | 90 |
| 6.0 | 82 | +9 | 91 |
| 6.1 | 83 | +9 | 92 |
| 6.2 | 84 | +10 | 94 |
| 6.3 | 85 | +10 | 95 |
| 6.4 | 86 | +10 | 96 |
| 6.5 | 87 | +10 | 97 |
| 6.6 | 88 | +10 | 98 |
| 6.7 | 89 | +11 | 100 |
| 6.8 | 90 | +11 | 101 |
| 6.9 | 91 | +11 | 102 |
| 7.0 | 92 | +11 | 103 |
| 7.1 | 93 | +11 | 104 |
| 7.2 | 94 | +12 | **106** |

</details>

<details>
<summary>Tabla completa — Noche con lluvia (1.7 – 4.9 km)</summary>

| km  | Normal | Recargo | Con lluvia |
|-----|--------|---------|------------|
| 1.7 | 42 | +1 | 43 |
| 1.8 | 43 | +1 | 44 |
| 1.9 | 44 | +1 | 45 |
| 2.0 | 45 | +1 | 46 |
| 2.1 | 46 | +1 | 47 |
| 2.2 | 47 | +2 | 49 |
| 2.3 | 48 | +2 | 50 |
| 2.4 | 49 | +2 | 51 |
| 2.5 | 50 | +2 | 52 |
| 2.6 | 51 | +2 | 53 |
| 2.7 | 52 | +3 | 55 |
| 2.8 | 53 | +3 | 56 |
| 2.9 | 54 | +3 | 57 |
| 3.0 | 55 | +3 | 58 |
| 3.1 | 56 | +3 | 59 |
| 3.2 | 57 | +4 | 61 |
| 3.3 | 58 | +4 | 62 |
| 3.4 | 59 | +4 | 63 |
| 3.5 | 60 | +4 | 64 |
| 3.6 | 61 | +4 | 65 |
| 3.7 | 62 | +5 | 67 |
| 3.8 | 63 | +5 | 68 |
| 3.9 | 64 | +5 | 69 |
| 4.0 | 65 | +5 | 70 |
| 4.1 | 66 | +5 | 71 |
| 4.2 | 67 | +6 | 73 |
| 4.3 | 68 | +6 | 74 |
| 4.4 | 69 | +6 | 75 |
| 4.5 | 70 | +6 | 76 |
| 4.6 | 71 | +6 | 77 |
| 4.7 | 72 | +7 | 79 |
| 4.8 | 73 | +7 | 80 |
| 4.9 | 74 | +7 | **81** |

</details>

<details>
<summary>Tabla completa — Madrugada con lluvia (1.7 – 4.1 km)</summary>

| km  | Normal | Recargo | Con lluvia |
|-----|--------|---------|------------|
| 1.7 | 45 | +1 | 46 |
| 1.8 | 46 | +1 | 47 |
| 1.9 | 47 | +1 | 48 |
| 2.0 | 48 | +1 | 49 |
| 2.1 | 49 | +1 | 50 |
| 2.2 | 50 | +2 | 52 |
| 2.3 | 51 | +2 | 53 |
| 2.4 | 52 | +2 | 54 |
| 2.5 | 53 | +2 | 55 |
| 2.6 | 54 | +2 | 56 |
| 2.7 | 55 | +3 | 58 |
| 2.8 | 56 | +3 | 59 |
| 2.9 | 57 | +3 | 60 |
| 3.0 | 58 | +3 | 61 |
| 3.1 | 59 | +3 | 62 |
| 3.2 | 60 | +4 | 64 |
| 3.3 | 61 | +4 | 65 |
| 3.4 | 62 | +4 | 66 |
| 3.5 | 63 | +4 | 67 |
| 3.6 | 64 | +4 | 68 |
| 3.7 | 65 | +5 | 70 |
| 3.8 | 66 | +5 | 71 |
| 3.9 | 67 | +5 | 72 |
| 4.0 | 68 | +5 | 73 |
| 4.1 | 70 | +5 | **75** |

</details>

### Tramo 4 — Cálculo por km con lluvia (tope base → 17.0 km)

Fórmula: `precio = precio_base_lluvia + (km − tope_base) × ($/km normal + $2)`

Donde `precio_base_lluvia` es el precio del tope base ya con su recargo (última fila de cada tabla del Tramo 3).

| Horario    | Precio base con lluvia | Tope base | $/km normal | $/km con lluvia |
|------------|--------------------------|-----------|---------------|--------------------|
| Día        | $106 MXN                 | 7.2 km    | $13/km        | **$15/km**         |
| Noche      | $81 MXN                  | 4.9 km    | $15/km        | **$17/km**         |
| Madrugada  | $75 MXN                  | 4.1 km    | $17/km        | **$19/km**         |

**Ejemplo (Día, 10 km, con lluvia):** `$106 + (10 − 7.2) × $15 = $106 + $42 = $148 MXN`
*(vs. $130 MXN sin lluvia — diferencia de $18)*

---

## 2. Tramo foráneo (17.01 km – 200 km) — sin cambio

El recargo de lluvia **no aplica** a partir de 17.01 km. Ahí ya no hay tarifas de ciudad, así que las tarifas foráneas se mantienen exactamente igual que en [TARIFAS.md](TARIFAS.md):

| Rango             | $/km    |
|-------------------|---------|
| 17.01 – 25.9 km   | $15/km  |
| 26 – 69.9 km      | $14/km  |
| 70 – 139.9 km     | $13/km  |
| 140 – 200 km      | $12/km  |
| Más de 200 km     | $12/km (estimado) |

---

## Resumen comparativo (recargo por tramo)

```
0.0 ────── 1.3 km    → +$3 fijos
1.31 ───── 1.7 km    → +$4 fijos
1.7 ────── tope base → +$1 cada 0.5 km acumulado (tabla recalculada)
tope base ─ 17.0 km   → +$2/km adicional
17.01 ───── 200 km    → sin cambio (foráneo se mantiene igual)
```

> Este documento es solo de referencia. Si decides implementarlo en la app, dímelo para agregar el modo lluvia a `index.html`.
