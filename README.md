# 🚕 Calculadora de Tarifas

Calculadora web ligera, responsiva y en tiempo real para determinar el costo de viajes según el kilometraje, en dos modalidades (**NaVu Ejecutivo** y **NaVu Taxi**), con y sin recargo por lluvia, aplicando tarifas urbanas (Día, Noche, Madrugada) y tarifas foráneas fijas por tramo.

🌐 **Ver en línea (móvil y escritorio)**: [https://vanchys.github.io/calculo-tarifas/](https://vanchys.github.io/calculo-tarifas/)

---

## 📋 Reglas de Tarifas

La app muestra dos bloques de tarjetas por cada horario: **NaVu Ejecutivo** y **NaVu Taxi**, cada una con su precio normal y, al lado, su precio con recargo de lluvia.

### 1. Tarifas Urbanas (0.0 a 17.0 km)

**NaVu Ejecutivo**
- **Sub-mínimo (0.0 a 1.3 km)**: 🌞 Día $34 · 🌙 Noche $37 · 🌌 Madrugada $40
- **Mínimo estándar (1.31 a 1.7 km)**: 🌞 Día $39 · 🌙 Noche $42 · 🌌 Madrugada $45
- **Topes base de tabla fija y paso a precio por kilómetro**:
  - 🌞 Día: tabla fija hasta **7.2 km** ($94); de ahí, **$94 base + $13/km** hasta los 17 km.
  - 🌙 Noche: tabla fija hasta **4.9 km** ($74); de ahí, **$74 base + $15/km** hasta los 17 km.
  - 🌌 Madrugada: tabla fija hasta **4.1 km** ($70); de ahí, **$70 base + $17/km** hasta los 17 km.

**NaVu Taxi** (siempre un poco más barata que el Ejecutivo desde el mínimo)
- **Sub-mínimo (0.0 a 1.5 km)** y **mínimo estándar (1.51 a 2.0 km)**: mismos precios que el Ejecutivo, con más kilómetros cubiertos.
- **Topes base y $/km**:
  - 🌞 Día: tabla fija hasta **9.5 km** ($114); de ahí, **$12/km**.
  - 🌙 Noche: tabla fija hasta **5.5 km** ($77); de ahí, **$14/km**.
  - 🌌 Madrugada: tabla fija hasta **4.2 km** ($67); de ahí, **$16/km**.

**Interpolación continua**: para cualquier distancia con decimales (por ejemplo, `4.05 km`), el precio se calcula de forma continua peso a peso sin saltos, en ambas modalidades.

### 2. Recargo por lluvia ☔

Cada tarjeta muestra, al lado del precio normal, el precio con lluvia. El recargo compensa al conductor por manejar bajo peores condiciones, no depende de la categoría del servicio:
- Sub-mínimo: **+$3** fijos.
- Mínimo estándar: **+$4** fijos.
- Tabla fija y precio por km: **+$1 cada 0.5 km** acumulado desde el tope del mínimo (equivalente a +$2/km).
- El precio con lluvia **nunca baja** del precio del mínimo con lluvia — se sostiene plano hasta que el recargo acumulado lo supera de forma natural.
- No aplica en tramo foráneo (17.01 km en adelante).

### 3. Tarifas Foráneas (a partir de 17.01 km)

A partir de los 17.01 km, las tarifas urbanas quedan automáticamente **descartadas y tachadas** en ambas modalidades, y aparece la tarjeta foránea aplicable de cada una:

| Rango | NaVu Ejecutivo | NaVu Taxi |
|---|---|---|
| 17.01 – 25.9 km | $15/km | $14/km |
| 26.0 – 69.9 km | $14/km | $13/km |
| 70.0 – 139.9 km | $13/km | $12/km |
| 140.0 – 200.0 km | $12/km | $11/km |

El recargo por lluvia no aplica en este tramo, en ninguna de las dos modalidades.

---

## 📱 Aplicación Instalable (PWA)
La aplicación está configurada como una **Progressive Web App (PWA)**:
- Se puede instalar directamente en la pantalla de inicio desde **Google Chrome** en celular y computadora.
- Funciona **sin conexión a internet (offline)** gracias al Service Worker integrado.
- Abre a pantalla completa con aspecto nativo.

---

## 🛠️ Tecnologías
- **HTML5 / CSS3**: Diseño responsivo para celular, tablet y escritorio con tema oscuro.
- **Vanilla JavaScript**: Lógica de cálculo directo e interpolación sin librerías externas.
- **PWA**: Web App Manifest (`manifest.json`) y Service Worker (`sw.js`).
