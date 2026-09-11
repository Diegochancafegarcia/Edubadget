# EduBudget — Avance APF1 (Android nativo)

App de control de gastos para estudiantes, hecha con **Android nativo
(Kotlin + XML)**, siguiendo los lineamientos del docente: layouts con
anclaje, botones con `onClick`, `ListView`, menú de Activity y ciclo de
vida completo.

## Cómo abrirlo

1. Abre **Android Studio**.
2. `File > Open...` y selecciona la carpeta `EduBudgetAndroid`.
3. Espera a que sincronice Gradle (la primera vez puede pedir descargar el
   Gradle Wrapper — dale "OK"/"Sync Now", solo necesita internet una vez).
4. Corre la app con el botón ▶ sobre un emulador o celular conectado.

## Estructura del proyecto

```
EduBudgetAndroid/
├── app/
│   ├── build.gradle
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/utp/edubudget/
│       │   ├── MainActivity.kt        # Pantalla de Inicio (ListView + menú)
│       │   ├── AddExpenseActivity.kt  # Formulario para registrar un gasto
│       │   ├── StatsActivity.kt       # Gráfico de barras por categoría
│       │   ├── Expense.kt             # Modelo de datos
│       │   ├── ExpenseRepository.kt   # "Base de datos" en memoria
│       │   └── ExpenseAdapter.kt      # Adapter del ListView
│       └── res/
│           ├── layout/                # activity_main, activity_add_expense, activity_stats, item_expense
│           ├── menu/main_menu.xml     # Menú de opciones (Estadísticas)
│           ├── values/                # colors.xml, strings.xml, themes.xml
│           └── drawable/              # fondos simples (tarjetas, barra de progreso)
```

## Qué hace cada pantalla

- **MainActivity (Inicio):** tarjeta de presupuesto con barra de progreso,
  `ListView` de gastos recientes (con un `ExpenseAdapter` personalizado), un
  botón `+` (`onClick`) que abre el formulario, y un menú de opciones
  (ícono de tres puntos) para ir a Estadísticas.
- **AddExpenseActivity:** formulario con `EditText` para el monto,
  `RadioGroup` para la categoría y botón "Guardar" con validación (el monto
  debe ser un número mayor a 0).
- **StatsActivity:** gráfico de barras hecho solo con `View` (sin librerías
  externas), calculado dinámicamente según los gastos registrados, más un
  resumen del total gastado vs. el límite mensual.

## Ciclo de vida

Las tres Activities sobrescriben `onCreate`, `onStart`, `onResume`,
`onPause`, `onStop` y `onDestroy`, cada uno con un `Log.d(...)`. Para verlos
en la práctica: corre la app, abre **Logcat** en Android Studio, filtra por
"MainActivity" (o el tag que quieras) y navega entre pantallas — vas a ver
en tiempo real cuándo se llama cada método.

## Qué falta (próximas entregas del curso)

- **APF2:** persistencia real con SQLite/Room (ahora mismo los datos viven
  en `ExpenseRepository`, en memoria, y se reinician al cerrar la app) y
  consumo de una API pública.
- **APF3:** cámara para adjuntar la foto de la boleta, permisos, y una
  notificación local cuando el gasto se acerque al límite mensual.
- **Proyecto final:** generación del APK firmado para entregar.
