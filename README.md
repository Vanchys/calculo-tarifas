# 🚕 Calculadora de Tarifas

Calculadora web ligera, responsiva y en tiempo real para determinar el costo de viajes según el kilometraje, aplicando tarifas urbanas (Día, Noche, Madrugada) y tarifas foráneas fijas por tramo.

🌐 **Ver en línea (móvil y escritorio)**: [https://vanchys.github.io/calculo-tarifas/](https://vanchys.github.io/calculo-tarifas/)

---

## 📋 Reglas de Tarifas

### 1. Tarifas Urbanas (0.0 a 17.0 km)
- **Sub-mínimo (0.0 a 1.3 km)**:
  - 🌞 Día: $34 MXN
  - 🌙 Noche: $37 MXN
  - 🌌 Madrugada: $40 MXN
- **Mínimo estándar (1.31 a 1.7 km)**:
  - 🌞 Día: $39 MXN
  - 🌙 Noche: $42 MXN
  - 🌌 Madrugada: $45 MXN
- **Topes base de tabla fija y paso a precio por kilómetro**:
  - 🌞 **Día**: Tabla fija hasta **7.2 km** ($94 MXN); a partir de ahí, **$94 base + $13 / km** adicional hasta los 17 km.
  - 🌙 **Noche**: Tabla fija hasta **4.9 km** ($74 MXN); a partir de ahí, **$74 base + $15 / km** adicional hasta los 17 km.
  - 🌌 **Madrugada**: Tabla fija hasta **4.1 km** ($70 MXN); a partir de ahí, **$70 base + $17 / km** adicional hasta los 17 km.
- **Interpolación continua**: Para cualquier distancia con decimales (por ejemplo, `4.05 km`), el precio se calcula de forma continua peso a peso sin saltos.

### 2. Tarifas Foráneas (a partir de 17.01 km)
A partir de los 17.01 km, las tarifas urbanas quedan automáticamente **descartadas y tachadas**, aplicando el tarifario foráneo fijo por tramo:
- **Tarifa foránea 1 (17.01 – 25.9 km)**: $15 / km fijo
- **Tarifa foránea 2 (26.0 – 69.9 km)**: $14 / km fijo
- **Tarifa foránea 3 (70.0 – 139.9 km)**: $13 / km fijo
- **Tarifa foránea 4 (140.0 – 200.0 km)**: $12 / km fijo

---

## 🛠️ Tecnologías
- **HTML5 / CSS3**: Diseño responsivo y temas con modo oscuro.
- **Vanilla JavaScript**: Lógica de cálculo directo sin dependencias externas.
