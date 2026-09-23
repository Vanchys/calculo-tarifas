# Tarifario Final — Taxi NaVu v2

Este documento es la fuente de verdad **vigente** del tarifario de la modalidad Taxi NaVu: tarifas de ciudad, tarifas con recargo de lluvia y tarifas foráneas. Refleja exactamente lo que calcula `index.html` hoy (objetos `taxiConfigs`, `foraneaRangesByModality.taxi`, funciones `lookupUrbanRateByConfig`, `lookupUrbanRateWithRain` y `lookupForaneaRate`).

**Reemplaza, para efectos de precio, al tarifario de Taxi descrito en [Tarifas Modalidad Taxi.md](Tarifas%20Modalidad%20Taxi.md).** Ese documento marca varias de las cifras que aquí cambian como *"cifra final del fundador, que nadie corrija"* — las decisiones de este documento las tomó el usuario directamente en esta sesión (22-sep-2026), reabriendo esas cifras a propósito. Si `Tarifas Modalidad Taxi.md` sigue siendo la fuente de verdad del negocio, hay que sincronizarlo con este documento o marcarlo como superado.

---

## 1. Qué cambió frente al tarifario anterior de Taxi

| Parámetro | v1 (Tarifas Modalidad Taxi.md) | v2 (este documento, vigente) |
|---|---|---|
| Tope del sub-mínimo | 1.3 km | **1.5 km** |
| Tope del mínimo estándar | 1.7 km | **2.0 km** |
| $/km Día | $13/km *(igual al Ejecutivo)* | **$12/km** |
| $/km Noche | $14/km | $14/km *(sin cambio)* |
| $/km Madrugada | $16/km | $16/km *(sin cambio)* |
| $/km foráneo (los 4 rangos) | Igual al Ejecutivo | **−$1/km en cada rango** |
| Candado de monotonía en lluvia | No existía | **Aplicado** (ver [sección 4](#4-tarifario-de-ciudad-con-recargo-de-lluvia--taxi)) |

Con estos cambios, **el Taxi ya nunca cuesta exactamente igual que el Ejecutivo**, ni en ciudad ni en foráneo — antes sí se igualaba en Día y en todo el tramo foráneo. Ver la tabla comparativa completa en la [sección 6](#6-comparativo-taxi-vs-ejecutivo-ahorro).

---

## 2. Sub-mínimo y mínimo estándar

Los **precios** del sub-mínimo y del mínimo estándar son los mismos del Ejecutivo — no se tocaron en ningún ajuste de esta modalidad. Lo que sí cambió en Taxi son los **rangos**: ambos tramos cubren más kilómetros que en el Ejecutivo, decisión del 22-sep-2026.

### Sub-mínimo — precio fijo

| Horario | Rango Ejecutivo | Rango Taxi | Precio fijo (ambas modalidades) |
|---|---|---|---|
| Día | 0.0 – 1.3 km | **0.0 – 1.5 km** | $34 MXN |
| Noche | 0.0 – 1.3 km | **0.0 – 1.5 km** | $37 MXN |
| Madrugada | 0.0 – 1.3 km | **0.0 – 1.5 km** | $40 MXN |

### Mínimo estándar — precio fijo

| Horario | Rango Ejecutivo | Rango Taxi | Precio fijo (ambas modalidades) |
|---|---|---|---|
| Día | 1.31 – 1.7 km | **1.51 – 2.0 km** | $39 MXN |
| Noche | 1.31 – 1.7 km | **1.51 – 2.0 km** | $42 MXN |
| Madrugada | 1.31 – 1.7 km | **1.51 – 2.0 km** | $45 MXN |

---

## 3. Tarifario de ciudad — Taxi (0.0 – 17.0 km)

Cada horario se calcula en el mismo orden de 4 tramos que el Ejecutivo, con los topes del sub-mínimo y del mínimo movidos a 1.5 km y 2.0 km:

```
0.0 ──────  1.5 km   → Sub-mínimo (precio fijo)
1.51 ─────  2.0 km   → Mínimo estándar (precio fijo)
2.0  ────── tope base → Tramo escalonado ($1 cada 0.1 km, misma pendiente que el Ejecutivo)
tope base ─ 17.0 km   → Precio base + $/km adicional (Día $12 · Noche $14 · Madrugada $16)
```

### Tramo escalonado (2.0 km → tope base)

El precio sube $1 cada 0.1 km desde el mínimo estándar hasta el tope base de cada horario (misma pendiente que usa el Ejecutivo, $10/km). Lo que cambia el tope base entre modalidades es el precio por km del tramo final, no la pendiente de este tramo.

<details>
<summary>Tabla completa — Taxi Día normal (2.0 – 9.5 km)</summary>

| km | $ | km | $ | km | $ | km | $ |
|----|---|----|---|----|---|----|---|
| 2.1 | 40 | 4.0 | 59 | 5.9 | 78 | 7.8 | 97 |
| 2.2 | 41 | 4.1 | 60 | 6.0 | 79 | 7.9 | 98 |
| 2.3 | 42 | 4.2 | 61 | 6.1 | 80 | 8.0 | 99 |
| 2.4 | 43 | 4.3 | 62 | 6.2 | 81 | 8.1 | 100 |
| 2.5 | 44 | 4.4 | 63 | 6.3 | 82 | 8.2 | 101 |
| 2.6 | 45 | 4.5 | 64 | 6.4 | 83 | 8.3 | 102 |
| 2.7 | 46 | 4.6 | 65 | 6.5 | 84 | 8.4 | 103 |
| 2.8 | 47 | 4.7 | 66 | 6.6 | 85 | 8.5 | 104 |
| 2.9 | 48 | 4.8 | 67 | 6.7 | 86 | 8.6 | 105 |
| 3.0 | 49 | 4.9 | 68 | 6.8 | 87 | 8.7 | 106 |
| 3.1 | 50 | 5.0 | 69 | 6.9 | 88 | 8.8 | 107 |
| 3.2 | 51 | 5.1 | 70 | 7.0 | 89 | 8.9 | 108 |
| 3.3 | 52 | 5.2 | 71 | 7.1 | 90 | 9.0 | 109 |
| 3.4 | 53 | 5.3 | 72 | 7.2 | 91 | 9.1 | 110 |
| 3.5 | 54 | 5.4 | 73 | 7.3 | 92 | 9.2 | 111 |
| 3.6 | 55 | 5.5 | 74 | 7.4 | 93 | 9.3 | 112 |
| 3.7 | 56 | 5.6 | 75 | 7.5 | 94 | 9.4 | 113 |
| 3.8 | 57 | 5.7 | 76 | 7.6 | 95 | 9.5 | 114 |
| 3.9 | 58 | 5.8 | 77 | 7.7 | 96 |  |  |

</details>

<details>
<summary>Tabla completa — Taxi Noche normal (2.0 – 5.5 km)</summary>

| km | $ | km | $ | km | $ | km | $ |
|----|---|----|---|----|---|----|---|
| 2.1 | 43 | 3.0 | 52 | 3.9 | 61 | 4.8 | 70 |
| 2.2 | 44 | 3.1 | 53 | 4.0 | 62 | 4.9 | 71 |
| 2.3 | 45 | 3.2 | 54 | 4.1 | 63 | 5.0 | 72 |
| 2.4 | 46 | 3.3 | 55 | 4.2 | 64 | 5.1 | 73 |
| 2.5 | 47 | 3.4 | 56 | 4.3 | 65 | 5.2 | 74 |
| 2.6 | 48 | 3.5 | 57 | 4.4 | 66 | 5.3 | 75 |
| 2.7 | 49 | 3.6 | 58 | 4.5 | 67 | 5.4 | 76 |
| 2.8 | 50 | 3.7 | 59 | 4.6 | 68 | 5.5 | 77 |
| 2.9 | 51 | 3.8 | 60 | 4.7 | 69 |  |  |

</details>

<details>
<summary>Tabla completa — Taxi Madrugada normal (2.0 – 4.2 km)</summary>

| km | $ | km | $ | km | $ | km | $ |
|----|---|----|---|----|---|----|---|
| 2.1 | 46 | 2.7 | 52 | 3.3 | 58 | 3.9 | 64 |
| 2.2 | 47 | 2.8 | 53 | 3.4 | 59 | 4.0 | 65 |
| 2.3 | 48 | 2.9 | 54 | 3.5 | 60 | 4.1 | 66 |
| 2.4 | 49 | 3.0 | 55 | 3.6 | 61 | 4.2 | 67 |
| 2.5 | 50 | 3.1 | 56 | 3.7 | 62 |  |  |
| 2.6 | 51 | 3.2 | 57 | 3.8 | 63 |  |  |

</details>

### Tramo por km (tope base → 17.0 km)

Fórmula: `precio = precio_base + (km − tope_base) × $/km`

| Horario | Precio base | Tope base | $/km adicional |
|---|---|---|---|
| Día | $114 MXN | 9.5 km | $12/km |
| Noche | $77 MXN | 5.5 km | $14/km |
| Madrugada | $67 MXN | 4.2 km | $16/km |

**Ejemplo (Día, 10 km):** `$114 + (10 − 9.5) × $12 = $114 + $6 = $120 MXN`

> El tope base de Día se mueve de 7.2 km (Ejecutivo) a **9.5 km** en Taxi. No es un ajuste manual: es dónde se cruzan matemáticamente la recta del tramo escalonado y la recta `km × $12`, dado que el $/km de Día bajó pero la pendiente del escalonado ($10/km) no cambió.

---

## 4. Tarifario de ciudad con recargo de lluvia — Taxi

Mismo criterio que el Ejecutivo (el recargo compensa al conductor por manejar bajo lluvia, no depende de la categoría del servicio):

| Tramo | Recargo |
|---|---|
| Sub-mínimo (0.0 – 1.3 km) | **+$3** fijos |
| Mínimo estándar (1.31 – 2.0 km) | **+$4** fijos |
| Tramo escalonado (2.0 km → tope base) | **+$1 cada 0.5 km** acumulado desde 2.0 km |
| Tramo por km (tope base → 17.0 km) | **+$2/km** adicional |
| Foráneo (17.01 – 200 km) | **Sin cambio** — el recargo solo aplica a tarifas de ciudad |

> **Correcciones aplicadas en esta versión** (`index.html`):
> 1. **Tope de mínimo fijo en la función de lluvia** (`lookupUrbanRateWithRain`): se calculaba con el tope de mínimo fijo en 1.7 km sin importar la modalidad. Al extender el mínimo de Taxi a 2.0 km eso rompía el cálculo — el precio con lluvia en 1.8 km salía más barato que en 1.7 km. Se corrigió para que el recargo arranque siempre justo después del mínimo estándar de cada modalidad.
> 2. **Candado de monotonía** (`lookupUrbanRateWithRain`): el precio con lluvia ya no puede bajar del precio del mínimo estándar con lluvia. Justo después del tope del mínimo, el recargo de "+$1 cada 0.5 km" arrancaba en $1 mientras la tabla normal ya venía subiendo $1 cada 0.1 km, así que el precio con lluvia bajaba un par de celdas antes de volver a subir. Ahora el precio se sostiene plano en el valor del mínimo con lluvia ($43 Día · $46 Noche · $49 Madrugada, en ambas modalidades) hasta que la propia rampa lo supera de forma natural. Aplica igual al Ejecutivo — ver [TARIFAS_LLUVIA.md](TARIFAS_LLUVIA.md), que documentaba el hueco de 1.8–1.9 km sin corregir y queda desactualizado en ese punto.
> 3. **La pantalla no usaba el candado del punto 2** (`calculate()`): aunque `lookupUrbanRateWithRain` ya calculaba bien el precio del Taxi, la función que dibuja las tarjetas nunca la llamaba para el Taxi — "importaba" el recargo en pesos del Ejecutivo en ese mismo kilómetro y se lo sumaba al precio normal del Taxi. Eso funcionaba mientras las dos modalidades compartían los mismos rangos de mínimo, pero al extender el sub-mínimo y el mínimo del Taxi de forma independiente (1.5/2.0 km, ver sección 2) quedaron en tramos distintos en el mismo kilómetro, y el recargo importado volvía a romper la monotonía **en pantalla**, aunque el cálculo de fondo ya estuviera bien. Se corrigió para que el Taxi llame a `lookupUrbanRateWithRain(taxiConfigs[franja], km)` directamente, igual que el Ejecutivo.

<details>
<summary>Tabla completa — Taxi Día con lluvia (2.0 – 17.0 km)</summary>

| Km | Normal | Recargo | Con lluvia |
|----|--------|---------|------------|
| 2.0 | $39 | +$4 | **$43** |
| 2.1 | $40 | +$3 | **$43** |
| 2.2 | $41 | +$2 | **$43** |
| 2.3 | $42 | +$1 | **$43** |
| 2.4 | $43 | +$1 | **$44** |
| 2.5 | $44 | +$2 | **$46** |
| 2.6 | $45 | +$2 | **$47** |
| 2.7 | $46 | +$2 | **$48** |
| 2.8 | $47 | +$2 | **$49** |
| 2.9 | $48 | +$2 | **$50** |
| 3.0 | $49 | +$3 | **$52** |
| 3.1 | $50 | +$3 | **$53** |
| 3.2 | $51 | +$3 | **$54** |
| 3.3 | $52 | +$3 | **$55** |
| 3.4 | $53 | +$3 | **$56** |
| 3.5 | $54 | +$4 | **$58** |
| 3.6 | $55 | +$4 | **$59** |
| 3.7 | $56 | +$4 | **$60** |
| 3.8 | $57 | +$4 | **$61** |
| 3.9 | $58 | +$4 | **$62** |
| 4.0 | $59 | +$5 | **$64** |
| 4.1 | $60 | +$5 | **$65** |
| 4.2 | $61 | +$5 | **$66** |
| 4.3 | $62 | +$5 | **$67** |
| 4.4 | $63 | +$5 | **$68** |
| 4.5 | $64 | +$6 | **$70** |
| 4.6 | $65 | +$6 | **$71** |
| 4.7 | $66 | +$6 | **$72** |
| 4.8 | $67 | +$6 | **$73** |
| 4.9 | $68 | +$6 | **$74** |
| 5.0 | $69 | +$7 | **$76** |
| 5.1 | $70 | +$7 | **$77** |
| 5.2 | $71 | +$7 | **$78** |
| 5.3 | $72 | +$7 | **$79** |
| 5.4 | $73 | +$7 | **$80** |
| 5.5 | $74 | +$8 | **$82** |
| 5.6 | $75 | +$8 | **$83** |
| 5.7 | $76 | +$8 | **$84** |
| 5.8 | $77 | +$8 | **$85** |
| 5.9 | $78 | +$8 | **$86** |
| 6.0 | $79 | +$9 | **$88** |
| 6.1 | $80 | +$9 | **$89** |
| 6.2 | $81 | +$9 | **$90** |
| 6.3 | $82 | +$9 | **$91** |
| 6.4 | $83 | +$9 | **$92** |
| 6.5 | $84 | +$10 | **$94** |
| 6.6 | $85 | +$10 | **$95** |
| 6.7 | $86 | +$10 | **$96** |
| 6.8 | $87 | +$10 | **$97** |
| 6.9 | $88 | +$10 | **$98** |
| 7.0 | $89 | +$11 | **$100** |
| 7.1 | $90 | +$11 | **$101** |
| 7.2 | $91 | +$11 | **$102** |
| 7.3 | $92 | +$11 | **$103** |
| 7.4 | $93 | +$11 | **$104** |
| 7.5 | $94 | +$12 | **$106** |
| 7.6 | $95 | +$12 | **$107** |
| 7.7 | $96 | +$12 | **$108** |
| 7.8 | $97 | +$12 | **$109** |
| 7.9 | $98 | +$12 | **$110** |
| 8.0 | $99 | +$13 | **$112** |
| 8.1 | $100 | +$13 | **$113** |
| 8.2 | $101 | +$13 | **$114** |
| 8.3 | $102 | +$13 | **$115** |
| 8.4 | $103 | +$13 | **$116** |
| 8.5 | $104 | +$14 | **$118** |
| 8.6 | $105 | +$14 | **$119** |
| 8.7 | $106 | +$14 | **$120** |
| 8.8 | $107 | +$14 | **$121** |
| 8.9 | $108 | +$14 | **$122** |
| 9.0 | $109 | +$15 | **$124** |
| 9.1 | $110 | +$15 | **$125** |
| 9.2 | $111 | +$15 | **$126** |
| 9.3 | $112 | +$15 | **$127** |
| 9.4 | $113 | +$15 | **$128** |
| 9.5 | $114 | +$16 | **$130** |
| 9.6 | $115 | +$16 | **$131** |
| 9.7 | $116 | +$17 | **$133** |
| 9.8 | $118 | +$16 | **$134** |
| 9.9 | $119 | +$17 | **$136** |
| 10.0 | $120 | +$17 | **$137** |
| 10.1 | $121 | +$17 | **$138** |
| 10.2 | $122 | +$18 | **$140** |
| 10.3 | $124 | +$17 | **$141** |
| 10.4 | $125 | +$18 | **$143** |
| 10.5 | $126 | +$18 | **$144** |
| 10.6 | $127 | +$18 | **$145** |
| 10.7 | $128 | +$19 | **$147** |
| 10.8 | $130 | +$18 | **$148** |
| 10.9 | $131 | +$19 | **$150** |
| 11.0 | $132 | +$19 | **$151** |
| 11.1 | $133 | +$19 | **$152** |
| 11.2 | $134 | +$20 | **$154** |
| 11.3 | $136 | +$19 | **$155** |
| 11.4 | $137 | +$20 | **$157** |
| 11.5 | $138 | +$20 | **$158** |
| 11.6 | $139 | +$20 | **$159** |
| 11.7 | $140 | +$21 | **$161** |
| 11.8 | $142 | +$20 | **$162** |
| 11.9 | $143 | +$21 | **$164** |
| 12.0 | $144 | +$21 | **$165** |
| 12.1 | $145 | +$21 | **$166** |
| 12.2 | $146 | +$22 | **$168** |
| 12.3 | $148 | +$21 | **$169** |
| 12.4 | $149 | +$22 | **$171** |
| 12.5 | $150 | +$22 | **$172** |
| 12.6 | $151 | +$22 | **$173** |
| 12.7 | $152 | +$23 | **$175** |
| 12.8 | $154 | +$22 | **$176** |
| 12.9 | $155 | +$23 | **$178** |
| 13.0 | $156 | +$23 | **$179** |
| 13.1 | $157 | +$23 | **$180** |
| 13.2 | $158 | +$24 | **$182** |
| 13.3 | $160 | +$23 | **$183** |
| 13.4 | $161 | +$24 | **$185** |
| 13.5 | $162 | +$24 | **$186** |
| 13.6 | $163 | +$24 | **$187** |
| 13.7 | $164 | +$25 | **$189** |
| 13.8 | $166 | +$24 | **$190** |
| 13.9 | $167 | +$25 | **$192** |
| 14.0 | $168 | +$25 | **$193** |
| 14.1 | $169 | +$25 | **$194** |
| 14.2 | $170 | +$26 | **$196** |
| 14.3 | $172 | +$25 | **$197** |
| 14.4 | $173 | +$26 | **$199** |
| 14.5 | $174 | +$26 | **$200** |
| 14.6 | $175 | +$26 | **$201** |
| 14.7 | $176 | +$27 | **$203** |
| 14.8 | $178 | +$26 | **$204** |
| 14.9 | $179 | +$27 | **$206** |
| 15.0 | $180 | +$27 | **$207** |
| 15.1 | $181 | +$27 | **$208** |
| 15.2 | $182 | +$28 | **$210** |
| 15.3 | $184 | +$27 | **$211** |
| 15.4 | $185 | +$28 | **$213** |
| 15.5 | $186 | +$28 | **$214** |
| 15.6 | $187 | +$28 | **$215** |
| 15.7 | $188 | +$29 | **$217** |
| 15.8 | $190 | +$28 | **$218** |
| 15.9 | $191 | +$29 | **$220** |
| 16.0 | $192 | +$29 | **$221** |
| 16.1 | $193 | +$29 | **$222** |
| 16.2 | $194 | +$30 | **$224** |
| 16.3 | $196 | +$29 | **$225** |
| 16.4 | $197 | +$30 | **$227** |
| 16.5 | $198 | +$30 | **$228** |
| 16.6 | $199 | +$30 | **$229** |
| 16.7 | $200 | +$31 | **$231** |
| 16.8 | $202 | +$30 | **$232** |
| 16.9 | $203 | +$31 | **$234** |
| 17.0 | $204 | +$31 | **$235** |

</details>

<details>
<summary>Tabla completa — Taxi Noche con lluvia (2.0 – 17.0 km)</summary>

| Km | Normal | Recargo | Con lluvia |
|----|--------|---------|------------|
| 2.0 | $42 | +$4 | **$46** |
| 2.1 | $43 | +$3 | **$46** |
| 2.2 | $44 | +$2 | **$46** |
| 2.3 | $45 | +$1 | **$46** |
| 2.4 | $46 | +$1 | **$47** |
| 2.5 | $47 | +$2 | **$49** |
| 2.6 | $48 | +$2 | **$50** |
| 2.7 | $49 | +$2 | **$51** |
| 2.8 | $50 | +$2 | **$52** |
| 2.9 | $51 | +$2 | **$53** |
| 3.0 | $52 | +$3 | **$55** |
| 3.1 | $53 | +$3 | **$56** |
| 3.2 | $54 | +$3 | **$57** |
| 3.3 | $55 | +$3 | **$58** |
| 3.4 | $56 | +$3 | **$59** |
| 3.5 | $57 | +$4 | **$61** |
| 3.6 | $58 | +$4 | **$62** |
| 3.7 | $59 | +$4 | **$63** |
| 3.8 | $60 | +$4 | **$64** |
| 3.9 | $61 | +$4 | **$65** |
| 4.0 | $62 | +$5 | **$67** |
| 4.1 | $63 | +$5 | **$68** |
| 4.2 | $64 | +$5 | **$69** |
| 4.3 | $65 | +$5 | **$70** |
| 4.4 | $66 | +$5 | **$71** |
| 4.5 | $67 | +$6 | **$73** |
| 4.6 | $68 | +$6 | **$74** |
| 4.7 | $69 | +$6 | **$75** |
| 4.8 | $70 | +$6 | **$76** |
| 4.9 | $71 | +$6 | **$77** |
| 5.0 | $72 | +$7 | **$79** |
| 5.1 | $73 | +$7 | **$80** |
| 5.2 | $74 | +$7 | **$81** |
| 5.3 | $75 | +$7 | **$82** |
| 5.4 | $76 | +$7 | **$83** |
| 5.5 | $77 | +$8 | **$85** |
| 5.6 | $78 | +$9 | **$87** |
| 5.7 | $80 | +$8 | **$88** |
| 5.8 | $81 | +$9 | **$90** |
| 5.9 | $83 | +$8 | **$91** |
| 6.0 | $84 | +$9 | **$93** |
| 6.1 | $85 | +$10 | **$95** |
| 6.2 | $87 | +$9 | **$96** |
| 6.3 | $88 | +$10 | **$98** |
| 6.4 | $90 | +$9 | **$99** |
| 6.5 | $91 | +$10 | **$101** |
| 6.6 | $92 | +$11 | **$103** |
| 6.7 | $94 | +$10 | **$104** |
| 6.8 | $95 | +$11 | **$106** |
| 6.9 | $97 | +$10 | **$107** |
| 7.0 | $98 | +$11 | **$109** |
| 7.1 | $99 | +$12 | **$111** |
| 7.2 | $101 | +$11 | **$112** |
| 7.3 | $102 | +$12 | **$114** |
| 7.4 | $104 | +$11 | **$115** |
| 7.5 | $105 | +$12 | **$117** |
| 7.6 | $106 | +$13 | **$119** |
| 7.7 | $108 | +$12 | **$120** |
| 7.8 | $109 | +$13 | **$122** |
| 7.9 | $111 | +$12 | **$123** |
| 8.0 | $112 | +$13 | **$125** |
| 8.1 | $113 | +$14 | **$127** |
| 8.2 | $115 | +$13 | **$128** |
| 8.3 | $116 | +$14 | **$130** |
| 8.4 | $118 | +$13 | **$131** |
| 8.5 | $119 | +$14 | **$133** |
| 8.6 | $120 | +$15 | **$135** |
| 8.7 | $122 | +$14 | **$136** |
| 8.8 | $123 | +$15 | **$138** |
| 8.9 | $125 | +$14 | **$139** |
| 9.0 | $126 | +$15 | **$141** |
| 9.1 | $127 | +$16 | **$143** |
| 9.2 | $129 | +$15 | **$144** |
| 9.3 | $130 | +$16 | **$146** |
| 9.4 | $132 | +$15 | **$147** |
| 9.5 | $133 | +$16 | **$149** |
| 9.6 | $134 | +$17 | **$151** |
| 9.7 | $136 | +$16 | **$152** |
| 9.8 | $137 | +$17 | **$154** |
| 9.9 | $139 | +$16 | **$155** |
| 10.0 | $140 | +$17 | **$157** |
| 10.1 | $141 | +$18 | **$159** |
| 10.2 | $143 | +$17 | **$160** |
| 10.3 | $144 | +$18 | **$162** |
| 10.4 | $146 | +$17 | **$163** |
| 10.5 | $147 | +$18 | **$165** |
| 10.6 | $148 | +$19 | **$167** |
| 10.7 | $150 | +$18 | **$168** |
| 10.8 | $151 | +$19 | **$170** |
| 10.9 | $153 | +$18 | **$171** |
| 11.0 | $154 | +$19 | **$173** |
| 11.1 | $155 | +$20 | **$175** |
| 11.2 | $157 | +$19 | **$176** |
| 11.3 | $158 | +$20 | **$178** |
| 11.4 | $160 | +$19 | **$179** |
| 11.5 | $161 | +$20 | **$181** |
| 11.6 | $162 | +$21 | **$183** |
| 11.7 | $164 | +$20 | **$184** |
| 11.8 | $165 | +$21 | **$186** |
| 11.9 | $167 | +$20 | **$187** |
| 12.0 | $168 | +$21 | **$189** |
| 12.1 | $169 | +$22 | **$191** |
| 12.2 | $171 | +$21 | **$192** |
| 12.3 | $172 | +$22 | **$194** |
| 12.4 | $174 | +$21 | **$195** |
| 12.5 | $175 | +$22 | **$197** |
| 12.6 | $176 | +$23 | **$199** |
| 12.7 | $178 | +$22 | **$200** |
| 12.8 | $179 | +$23 | **$202** |
| 12.9 | $181 | +$22 | **$203** |
| 13.0 | $182 | +$23 | **$205** |
| 13.1 | $183 | +$24 | **$207** |
| 13.2 | $185 | +$23 | **$208** |
| 13.3 | $186 | +$24 | **$210** |
| 13.4 | $188 | +$23 | **$211** |
| 13.5 | $189 | +$24 | **$213** |
| 13.6 | $190 | +$25 | **$215** |
| 13.7 | $192 | +$24 | **$216** |
| 13.8 | $193 | +$25 | **$218** |
| 13.9 | $195 | +$24 | **$219** |
| 14.0 | $196 | +$25 | **$221** |
| 14.1 | $197 | +$26 | **$223** |
| 14.2 | $199 | +$25 | **$224** |
| 14.3 | $200 | +$26 | **$226** |
| 14.4 | $202 | +$25 | **$227** |
| 14.5 | $203 | +$26 | **$229** |
| 14.6 | $204 | +$27 | **$231** |
| 14.7 | $206 | +$26 | **$232** |
| 14.8 | $207 | +$27 | **$234** |
| 14.9 | $209 | +$26 | **$235** |
| 15.0 | $210 | +$27 | **$237** |
| 15.1 | $211 | +$28 | **$239** |
| 15.2 | $213 | +$27 | **$240** |
| 15.3 | $214 | +$28 | **$242** |
| 15.4 | $216 | +$27 | **$243** |
| 15.5 | $217 | +$28 | **$245** |
| 15.6 | $218 | +$29 | **$247** |
| 15.7 | $220 | +$28 | **$248** |
| 15.8 | $221 | +$29 | **$250** |
| 15.9 | $223 | +$28 | **$251** |
| 16.0 | $224 | +$29 | **$253** |
| 16.1 | $225 | +$30 | **$255** |
| 16.2 | $227 | +$29 | **$256** |
| 16.3 | $228 | +$30 | **$258** |
| 16.4 | $230 | +$29 | **$259** |
| 16.5 | $231 | +$30 | **$261** |
| 16.6 | $232 | +$31 | **$263** |
| 16.7 | $234 | +$30 | **$264** |
| 16.8 | $235 | +$31 | **$266** |
| 16.9 | $237 | +$30 | **$267** |
| 17.0 | $238 | +$31 | **$269** |

</details>

<details>
<summary>Tabla completa — Taxi Madrugada con lluvia (2.0 – 17.0 km)</summary>

| Km | Normal | Recargo | Con lluvia |
|----|--------|---------|------------|
| 2.0 | $45 | +$4 | **$49** |
| 2.1 | $46 | +$3 | **$49** |
| 2.2 | $47 | +$2 | **$49** |
| 2.3 | $48 | +$1 | **$49** |
| 2.4 | $49 | +$1 | **$50** |
| 2.5 | $50 | +$2 | **$52** |
| 2.6 | $51 | +$2 | **$53** |
| 2.7 | $52 | +$2 | **$54** |
| 2.8 | $53 | +$2 | **$55** |
| 2.9 | $54 | +$2 | **$56** |
| 3.0 | $55 | +$3 | **$58** |
| 3.1 | $56 | +$3 | **$59** |
| 3.2 | $57 | +$3 | **$60** |
| 3.3 | $58 | +$3 | **$61** |
| 3.4 | $59 | +$3 | **$62** |
| 3.5 | $60 | +$4 | **$64** |
| 3.6 | $61 | +$4 | **$65** |
| 3.7 | $62 | +$4 | **$66** |
| 3.8 | $63 | +$4 | **$67** |
| 3.9 | $64 | +$4 | **$68** |
| 4.0 | $65 | +$5 | **$70** |
| 4.1 | $66 | +$5 | **$71** |
| 4.2 | $67 | +$5 | **$72** |
| 4.3 | $69 | +$5 | **$74** |
| 4.4 | $70 | +$6 | **$76** |
| 4.5 | $72 | +$5 | **$77** |
| 4.6 | $73 | +$6 | **$79** |
| 4.7 | $75 | +$6 | **$81** |
| 4.8 | $77 | +$6 | **$83** |
| 4.9 | $78 | +$7 | **$85** |
| 5.0 | $80 | +$6 | **$86** |
| 5.1 | $81 | +$7 | **$88** |
| 5.2 | $83 | +$7 | **$90** |
| 5.3 | $85 | +$7 | **$92** |
| 5.4 | $86 | +$8 | **$94** |
| 5.5 | $88 | +$7 | **$95** |
| 5.6 | $89 | +$8 | **$97** |
| 5.7 | $91 | +$8 | **$99** |
| 5.8 | $93 | +$8 | **$101** |
| 5.9 | $94 | +$9 | **$103** |
| 6.0 | $96 | +$8 | **$104** |
| 6.1 | $97 | +$9 | **$106** |
| 6.2 | $99 | +$9 | **$108** |
| 6.3 | $101 | +$9 | **$110** |
| 6.4 | $102 | +$10 | **$112** |
| 6.5 | $104 | +$9 | **$113** |
| 6.6 | $105 | +$10 | **$115** |
| 6.7 | $107 | +$10 | **$117** |
| 6.8 | $109 | +$10 | **$119** |
| 6.9 | $110 | +$11 | **$121** |
| 7.0 | $112 | +$10 | **$122** |
| 7.1 | $113 | +$11 | **$124** |
| 7.2 | $115 | +$11 | **$126** |
| 7.3 | $117 | +$11 | **$128** |
| 7.4 | $118 | +$12 | **$130** |
| 7.5 | $120 | +$11 | **$131** |
| 7.6 | $121 | +$12 | **$133** |
| 7.7 | $123 | +$12 | **$135** |
| 7.8 | $125 | +$12 | **$137** |
| 7.9 | $126 | +$13 | **$139** |
| 8.0 | $128 | +$12 | **$140** |
| 8.1 | $129 | +$13 | **$142** |
| 8.2 | $131 | +$13 | **$144** |
| 8.3 | $133 | +$13 | **$146** |
| 8.4 | $134 | +$14 | **$148** |
| 8.5 | $136 | +$13 | **$149** |
| 8.6 | $137 | +$14 | **$151** |
| 8.7 | $139 | +$14 | **$153** |
| 8.8 | $141 | +$14 | **$155** |
| 8.9 | $142 | +$15 | **$157** |
| 9.0 | $144 | +$14 | **$158** |
| 9.1 | $145 | +$15 | **$160** |
| 9.2 | $147 | +$15 | **$162** |
| 9.3 | $149 | +$15 | **$164** |
| 9.4 | $150 | +$16 | **$166** |
| 9.5 | $152 | +$15 | **$167** |
| 9.6 | $153 | +$16 | **$169** |
| 9.7 | $155 | +$16 | **$171** |
| 9.8 | $157 | +$16 | **$173** |
| 9.9 | $158 | +$17 | **$175** |
| 10.0 | $160 | +$16 | **$176** |
| 10.1 | $161 | +$17 | **$178** |
| 10.2 | $163 | +$17 | **$180** |
| 10.3 | $165 | +$17 | **$182** |
| 10.4 | $166 | +$18 | **$184** |
| 10.5 | $168 | +$17 | **$185** |
| 10.6 | $169 | +$18 | **$187** |
| 10.7 | $171 | +$18 | **$189** |
| 10.8 | $173 | +$18 | **$191** |
| 10.9 | $174 | +$19 | **$193** |
| 11.0 | $176 | +$18 | **$194** |
| 11.1 | $177 | +$19 | **$196** |
| 11.2 | $179 | +$19 | **$198** |
| 11.3 | $181 | +$19 | **$200** |
| 11.4 | $182 | +$20 | **$202** |
| 11.5 | $184 | +$19 | **$203** |
| 11.6 | $185 | +$20 | **$205** |
| 11.7 | $187 | +$20 | **$207** |
| 11.8 | $189 | +$20 | **$209** |
| 11.9 | $190 | +$21 | **$211** |
| 12.0 | $192 | +$20 | **$212** |
| 12.1 | $193 | +$21 | **$214** |
| 12.2 | $195 | +$21 | **$216** |
| 12.3 | $197 | +$21 | **$218** |
| 12.4 | $198 | +$22 | **$220** |
| 12.5 | $200 | +$21 | **$221** |
| 12.6 | $201 | +$22 | **$223** |
| 12.7 | $203 | +$22 | **$225** |
| 12.8 | $205 | +$22 | **$227** |
| 12.9 | $206 | +$23 | **$229** |
| 13.0 | $208 | +$22 | **$230** |
| 13.1 | $209 | +$23 | **$232** |
| 13.2 | $211 | +$23 | **$234** |
| 13.3 | $213 | +$23 | **$236** |
| 13.4 | $214 | +$24 | **$238** |
| 13.5 | $216 | +$23 | **$239** |
| 13.6 | $217 | +$24 | **$241** |
| 13.7 | $219 | +$24 | **$243** |
| 13.8 | $221 | +$24 | **$245** |
| 13.9 | $222 | +$25 | **$247** |
| 14.0 | $224 | +$24 | **$248** |
| 14.1 | $225 | +$25 | **$250** |
| 14.2 | $227 | +$25 | **$252** |
| 14.3 | $229 | +$25 | **$254** |
| 14.4 | $230 | +$26 | **$256** |
| 14.5 | $232 | +$25 | **$257** |
| 14.6 | $233 | +$26 | **$259** |
| 14.7 | $235 | +$26 | **$261** |
| 14.8 | $237 | +$26 | **$263** |
| 14.9 | $238 | +$27 | **$265** |
| 15.0 | $240 | +$26 | **$266** |
| 15.1 | $241 | +$27 | **$268** |
| 15.2 | $243 | +$27 | **$270** |
| 15.3 | $245 | +$27 | **$272** |
| 15.4 | $246 | +$28 | **$274** |
| 15.5 | $248 | +$27 | **$275** |
| 15.6 | $249 | +$28 | **$277** |
| 15.7 | $251 | +$28 | **$279** |
| 15.8 | $253 | +$28 | **$281** |
| 15.9 | $254 | +$29 | **$283** |
| 16.0 | $256 | +$28 | **$284** |
| 16.1 | $257 | +$29 | **$286** |
| 16.2 | $259 | +$29 | **$288** |
| 16.3 | $261 | +$29 | **$290** |
| 16.4 | $262 | +$30 | **$292** |
| 16.5 | $264 | +$29 | **$293** |
| 16.6 | $265 | +$30 | **$295** |
| 16.7 | $267 | +$30 | **$297** |
| 16.8 | $269 | +$30 | **$299** |
| 16.9 | $270 | +$31 | **$301** |
| 17.0 | $272 | +$30 | **$302** |

</details>

### Recargo máximo posible por lluvia en Taxi

| Franja | Normal en 17.0 km | Con lluvia en 17.0 km | Recargo máximo |
|---|---|---|---|
| Día | $204 | $235 | **+$31** |
| Noche | $238 | $269 | **+$31** |
| Madrugada | $272 | $302 | **+$30** |

---

## 5. Tarifario foráneo — Taxi (17.01 – 200 km)

A partir de 17.01 km ya no hay tabla ni tramos: precio fijo por kilómetro, **−$1/km frente al Ejecutivo** en cada uno de los 4 rangos.

Fórmula: `precio = km × $/km` (redondeado)

| Rango | Ejecutivo $/km | Taxi $/km |
|---|---|---|
| Tarifa foránea 1 (17.01 – 25.9 km) | $15 | **$14** |
| Tarifa foránea 2 (26 – 69.9 km) | $14 | **$13** |
| Tarifa foránea 3 (70 – 139.9 km) | $13 | **$12** |
| Tarifa foránea 4 (140 – 200 km) | $12 | **$11** |

**Ejemplos:**
- 20 km → `20 × $14 = $280 MXN` (Tarifa foránea 1)
- 50 km → `50 × $13 = $650 MXN` (Tarifa foránea 2)
- 100 km → `100 × $12 = $1,200 MXN` (Tarifa foránea 3)
- 170 km → `170 × $11 = $1,870 MXN` (Tarifa foránea 4)
- Más de 200 km → se estima con el $/km del último rango ($11/km)

El recargo de lluvia **no aplica** en el tramo foráneo, en ninguna de las dos modalidades.

### Salto en la frontera de los 17 km (Taxi)

Al pasar de 17.0 km (ciudad) a 17.01 km (foránea) el tarifario cambia de golpe — la app debe mostrarlo con claridad, nombrando la tarifa foránea aplicable, para que no parezca un error.

| Franja | 17.0 km (ciudad, Taxi) | 17.01 km (foránea, Taxi) | Salto |
|---|---|---|---|
| Día | $204 | $238 | +$34 |
| Noche | $238 | $238 | +$0 |
| Madrugada | $272 | $238 | −$34 |

---

## 6. Comparativo Taxi vs Ejecutivo (ahorro)

Con las reglas de este documento, el Taxi nunca vuelve a costar lo mismo que el Ejecutivo una vez pasado el mínimo estándar (2.0 km): el ahorro arranca en $3 y crece hasta $17–18 en el km 17, y sigue creciendo en el tramo foráneo porque el $/km también es menor.

**Día**

| km | Ejecutivo | Taxi | Ahorro |
|----|-----------|------|--------|
| 1.0 | $34 | $34 | igual |
| 1.5 | $39 | $39 | igual |
| 2.0 | $42 | $39 | −$3 |
| 2.5 | $47 | $44 | −$3 |
| 3.0 | $52 | $49 | −$3 |
| 4.0 | $62 | $59 | −$3 |
| 5.0 | $72 | $69 | −$3 |
| 6.0 | $82 | $79 | −$3 |
| 7.0 | $92 | $89 | −$3 |
| 8.0 | $104 | $99 | −$5 |
| 10.0 | $130 | $120 | −$10 |
| 13.0 | $169 | $156 | −$13 |
| 15.0 | $195 | $180 | −$15 |
| 17.0 | $221 | $204 | −$17 |

**Noche**

| km | Ejecutivo | Taxi | Ahorro |
|----|-----------|------|--------|
| 1.0 | $37 | $37 | igual |
| 1.5 | $42 | $42 | igual |
| 2.0 | $45 | $42 | −$3 |
| 2.5 | $50 | $47 | −$3 |
| 3.0 | $55 | $52 | −$3 |
| 4.0 | $65 | $62 | −$3 |
| 5.0 | $76 | $72 | −$4 |
| 6.0 | $91 | $84 | −$7 |
| 7.0 | $106 | $98 | −$8 |
| 8.0 | $121 | $112 | −$9 |
| 10.0 | $151 | $140 | −$11 |
| 13.0 | $196 | $182 | −$14 |
| 15.0 | $226 | $210 | −$16 |
| 17.0 | $256 | $238 | −$18 |

**Madrugada**

| km | Ejecutivo | Taxi | Ahorro |
|----|-----------|------|--------|
| 1.0 | $40 | $40 | igual |
| 1.5 | $45 | $45 | igual |
| 2.0 | $48 | $45 | −$3 |
| 2.5 | $53 | $50 | −$3 |
| 3.0 | $58 | $55 | −$3 |
| 4.0 | $68 | $65 | −$3 |
| 5.0 | $85 | $80 | −$5 |
| 6.0 | $102 | $96 | −$6 |
| 7.0 | $119 | $112 | −$7 |
| 8.0 | $136 | $128 | −$8 |
| 10.0 | $170 | $160 | −$10 |
| 13.0 | $221 | $208 | −$13 |
| 15.0 | $255 | $240 | −$15 |
| 17.0 | $289 | $272 | −$17 |

---

## Fuente de la lógica

- `index.html`: objetos `taxiConfigs`, `taxiMinimums`, `TAXI_SUB_MIN_MAX_KM`, `TAXI_STD_MIN_MAX_KM`, `TAXI_RAMP_RATE_PER_KM`, `foraneaRangesByModality.taxi`; funciones `buildTaxiConfig`, `lookupUrbanRateByConfig`, `lookupUrbanRateWithRain`, `lookupForaneaRate`.
- `sw.js`: caché en `tarifas-cache-v13` (subir la versión cada vez que se edite el tarifario, para forzar refresco en dispositivos con la PWA instalada).
- ⚠️ **Nada de este documento está desplegado todavía.** Los cambios de esta sesión (modalidad Taxi completa, regla D, foráneos, sub-mínimo/mínimo extendidos, candado de monotonía) existen solo en el `index.html` y `sw.js` locales — el usuario pidió explícitamente no hacer `git push` por ahora.
- El tarifario del Ejecutivo **no se tocó** en ninguno de los cambios de este documento — sigue documentado en [TARIFAS.md](TARIFAS.md) y [TARIFAS_LLUVIA.md](TARIFAS_LLUVIA.md).
