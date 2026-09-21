# Tarifas — Calculadora de Tarifas

Este documento muestra de forma visual de dónde salen los precios que calcula `index.html`, organizados por tramo y horario.

---

## 1. Tramos urbanos (0.0 km – 17.0 km)

Cada horario (Día, Noche, Madrugada) se calcula en 4 tramos, en este orden:

### Tramo 1 — Sub-mínimo (0.0 – 1.3 km)
Precio fijo, sin importar la distancia exacta dentro del rango.

| Horario    | Precio fijo |
|------------|-------------|
| Día        | $34 MXN     |
| Noche      | $37 MXN     |
| Madrugada  | $40 MXN     |

### Tramo 2 — Mínimo estándar (1.31 – 1.7 km)
Precio fijo, sin importar la distancia exacta dentro del rango.

| Horario    | Precio fijo |
|------------|-------------|
| Día        | $39 MXN     |
| Noche      | $42 MXN     |
| Madrugada  | $45 MXN     |

### Tramo 3 — Tabla fija con interpolación (1.7 km → tope base)
A partir de 1.7 km se usa una tabla de puntos fijos (uno por cada 0.1 km) tomada del tarifario oficial. Si el usuario ingresa un decimal intermedio (ej. 4.05 km), el precio se interpola linealmente entre los dos puntos más cercanos, peso a peso.

**Tope base por horario** (último punto de la tabla, donde termina este tramo):

| Horario    | Tope base (km) | Precio en el tope |
|------------|-----------------|--------------------|
| Día        | 7.2 km          | $94 MXN            |
| Noche      | 4.9 km          | $74 MXN            |
| Madrugada  | 4.1 km          | $70 MXN            |

<details>
<summary>Tabla completa — Día (1.7 – 7.2 km)</summary>

| km  | $  | km  | $  | km  | $  |
|-----|----|-----|----|-----|----|
| 1.7 | 39 | 3.6 | 58 | 5.5 | 77 |
| 1.8 | 40 | 3.7 | 59 | 5.6 | 78 |
| 1.9 | 41 | 3.8 | 60 | 5.7 | 79 |
| 2.0 | 42 | 3.9 | 61 | 5.8 | 80 |
| 2.1 | 43 | 4.0 | 62 | 5.9 | 81 |
| 2.2 | 44 | 4.1 | 63 | 6.0 | 82 |
| 2.3 | 45 | 4.2 | 64 | 6.1 | 83 |
| 2.4 | 46 | 4.3 | 65 | 6.2 | 84 |
| 2.5 | 47 | 4.4 | 66 | 6.3 | 85 |
| 2.6 | 48 | 4.5 | 67 | 6.4 | 86 |
| 2.7 | 49 | 4.6 | 68 | 6.5 | 87 |
| 2.8 | 50 | 4.7 | 69 | 6.6 | 88 |
| 2.9 | 51 | 4.8 | 70 | 6.7 | 89 |
| 3.0 | 52 | 4.9 | 71 | 6.8 | 90 |
| 3.1 | 53 | 5.0 | 72 | 6.9 | 91 |
| 3.2 | 54 | 5.1 | 73 | 7.0 | 92 |
| 3.3 | 55 | 5.2 | 74 | 7.1 | 93 |
| 3.4 | 56 | 5.3 | 75 | 7.2 | 94 |
| 3.5 | 57 | 5.4 | 76 |     |    |

</details>

<details>
<summary>Tabla completa — Noche (1.7 – 4.9 km)</summary>

| km  | $  | km  | $  |
|-----|----|-----|----|
| 1.7 | 42 | 3.4 | 59 |
| 1.8 | 43 | 3.5 | 60 |
| 1.9 | 44 | 3.6 | 61 |
| 2.0 | 45 | 3.7 | 62 |
| 2.1 | 46 | 3.8 | 63 |
| 2.2 | 47 | 3.9 | 64 |
| 2.3 | 48 | 4.0 | 65 |
| 2.4 | 49 | 4.1 | 66 |
| 2.5 | 50 | 4.2 | 67 |
| 2.6 | 51 | 4.3 | 68 |
| 2.7 | 52 | 4.4 | 69 |
| 2.8 | 53 | 4.5 | 70 |
| 2.9 | 54 | 4.6 | 71 |
| 3.0 | 55 | 4.7 | 72 |
| 3.1 | 56 | 4.8 | 73 |
| 3.2 | 57 | 4.9 | 74 |
| 3.3 | 58 |     |    |

</details>

<details>
<summary>Tabla completa — Madrugada (1.7 – 4.1 km)</summary>

| km  | $  |
|-----|----|
| 1.7 | 45 |
| 1.8 | 46 |
| 1.9 | 47 |
| 2.0 | 48 |
| 2.1 | 49 |
| 2.2 | 50 |
| 2.3 | 51 |
| 2.4 | 52 |
| 2.5 | 53 |
| 2.6 | 54 |
| 2.7 | 55 |
| 2.8 | 56 |
| 2.9 | 57 |
| 3.0 | 58 |
| 3.1 | 59 |
| 3.2 | 60 |
| 3.3 | 61 |
| 3.4 | 62 |
| 3.5 | 63 |
| 3.6 | 64 |
| 3.7 | 65 |
| 3.8 | 66 |
| 3.9 | 67 |
| 4.0 | 68 |
| 4.1 | 70 |

</details>

### Tramo 4 — Cálculo por km (tope base → 17.0 km)
Superado el tope base, ya no hay tabla: se suma el precio base más un costo fijo por cada km adicional.

Fórmula: `precio = precio_base + (km − tope_base) × precio_por_km`

| Horario    | Precio base | Tope base | $/km adicional |
|------------|-------------|-----------|------------------|
| Día        | $94 MXN     | 7.2 km    | $13/km           |
| Noche      | $74 MXN     | 4.9 km    | $15/km           |
| Madrugada  | $70 MXN     | 4.1 km    | $17/km           |

**Ejemplo (Día, 10 km):** `$94 + (10 − 7.2) × $13 = $94 + $36.4 = $130 MXN`

---

## 2. Tramo foráneo (17.01 km – 200 km)

A partir de **17.01 km**, las tarifas urbanas quedan descartadas (se muestran tachadas en la app) y aplica un precio fijo por kilómetro, sin tabla ni tramos.

Fórmula: `precio = km × precio_por_km` (redondeado)

| Rango             | $/km    |
|-------------------|---------|
| 17.01 – 25.9 km   | $15/km  |
| 26 – 69.9 km      | $14/km  |
| 70 – 139.9 km     | $13/km  |
| 140 – 200 km      | $12/km  |
| Más de 200 km     | $12/km (estimado, fuera de rango oficial) |

**Ejemplo (20 km):** `20 × $15 = $300 MXN`

---

## Resumen del flujo de cálculo

```
0.0 ────── 1.3 km   → Sub-mínimo (precio fijo)
1.31 ───── 1.7 km   → Mínimo estándar (precio fijo)
1.7 ────── tope base → Tabla fija oficial (interpolación lineal)
tope base ─ 17.0 km  → Precio base + $/km adicional
17.01 ───── 200 km   → Tarifa foránea por rango ($/km fijo)
```

> Fuente de la lógica: `index.html` (objeto `urbanConfigs` y `foraneaRanges`, función `lookupUrbanRateByConfig` y `lookupForaneaRate`).
