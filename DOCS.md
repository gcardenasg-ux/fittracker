# FitTracker Pro - Documentacion Tecnica

## Informacion General

| Campo | Valor |
|-------|-------|
| Nombre | FitTracker Pro |
| Tipo | PWA (Progressive Web App) single-file |
| Archivo principal | `index.html` (~1009 lineas, ~77KB) |
| Idioma interfaz | Espanol (es-MX) |
| Hosting | GitHub Pages |
| URL publica | https://gcardenasg-ux.github.io/fittracker/ |
| Repositorio | https://github.com/gcardenasg-ux/fittracker |
| Rama principal | master |

---

## Stack Tecnologico

- **HTML5 / CSS3 / JavaScript vanilla** (sin frameworks)
- **Chart.js 4.4.0** (CDN) - graficas de progreso
- **Google Fonts** - Barlow Condensed (headings) + DM Sans (body)
- **Web Share API** - compartir backups en iOS/Android
- **Web Audio API** - beeps del temporizador
- **localStorage** - persistencia de datos en el navegador

No hay dependencias npm, no hay build step, no hay backend.

---

## Arquitectura del Archivo

El archivo `index.html` contiene todo en un solo archivo, organizado en 3 bloques:

### 1. CSS (lineas 1-215 aprox.)

```
:root              Variables de tema DARK (default)
[data-theme=light]  Variables de tema LIGHT
@media(prefers...)   Auto-deteccion de tema del sistema
Componentes         Estilos de cada seccion (ver lista abajo)
```

**Variables CSS principales:**
- `--bg`, `--s1`, `--s2`, `--s3` - fondos (del mas oscuro al mas claro)
- `--bo` - bordes
- `--am` - color acento (amber/naranja)
- `--gr` - verde (exito), `--re` - rojo (error)
- `--tx` - texto principal, `--mu` - texto muted
- `--fig` - color de figuras SVG stick, `--bench` - color de banco
- `--svg-bs`, `--svg-sk` - colores de diagramas musculares
- `--wkb1`, `--wkb2` - gradiente del banner de workout
- `--fh` - font heading (Barlow Condensed), `--fb` - font body (DM Sans)

### 2. HTML (lineas 216-295 aprox.)

```
toast           Notificacion flotante
gallery-overlay Galeria fullscreen de imagenes
app
  hdr           Header con logo + toggle de tema
  pwa-banner    Banner de instalacion PWA
  pages
    page-today     Pagina principal (workout del dia)
    page-progress  Progreso + Metas (sub-tabs)
    page-calendar  Calendario mensual
    page-history   Historial de sesiones
  timer-bar     Temporizador de descanso (fijo)
  exp-bar       Botones Importar/Exportar/Compartir
  sync-guide    Instrucciones de sincronizacion (colapsable)
  bnav          Navegacion inferior (4 botones)
```

### 3. JavaScript (lineas 296-1009 aprox.)

| Seccion | Funciones principales | Descripcion |
|---------|----------------------|-------------|
| SVG Helpers | `_l()`, `_ci()`, `_bn()` | Dibuja lineas, circulos, rectangulos SVG |
| Figure Builders | `standBody()`, `bentBody()`, `squatBody()`, `lyingBody()` | Figuras stick para posiciones de ejercicio |
| Exercise Photos | `EX_PHOTOS`, `photoSection()` | Mapeo de IDs a fotos del repositorio free-exercise-db |
| Gallery | `openGallery()`, `closeGallery()`, `galleryNav()` | Overlay fullscreen con swipe |
| Muscle Diagrams | `bodyFront()`, `bodyBack()`, `getDiag()` | SVGs de grupos musculares (frente/espalda) |
| Workout Data | `WK` objeto | 3 ciclos (A, B, C) con 22+ ejercicios |
| State & Storage | `aS()`, `sS()`, `persist()`, `loadSess()` | localStorage con clave `ft2` |
| Theme | `getTheme()`, `setTheme()`, `toggleTheme()` | Light/dark + auto-deteccion |
| Render Today | `renderToday()`, `renderCard()`, `renderSR()` | Pagina principal |
| Cardio | `renderCardioSection()`, `selCardioMachine()` | Seccion de cardio opcional |
| Interactions | `togDone()`, `addS()`, `updS()`, `finSess()` | Marcar series, agregar, guardar |
| Timer | `startTimer()`, `stopTimer()`, `pauseTimer()`, `beep()` | Temporizador con audio |
| Progress | `renderProg()`, `popSel()` | Graficas Chart.js |
| Goals | `checkAchievements()`, `renderGoals()`, `spawnConfetti()` | Sistema de logros |
| Calendar | `renderCalendar()`, `navCal()`, `calcStreak()` | Vista mensual + rachas |
| History | `renderHist()` | Historial de sesiones |
| Export/Import | `exportData()`, `importData()`, `shareData()` | Sync JSON + Web Share API |
| Navigation | `showPg()`, `showSubTab()` | Cambio de paginas/tabs |

---

## Estructura de Datos

### localStorage key: `ft2` (sesiones)

```json
[
  {
    "date": "2026-04-06",
    "wk": "A",
    "wkName": "EMPUJE + CORE",
    "done": 18,
    "total": 24,
    "note": "Me senti bien, subi peso en press",
    "data": {
      "db_bench": {
        "sets": [
          {"w": 30, "r": 12, "done": true},
          {"w": 30, "r": 10, "done": true},
          {"w": 30, "r": 8, "done": true}
        ]
      },
      "__note__": "Me senti bien...",
      "__cardio__": {
        "machine": "elliptical",
        "duration": 20,
        "distance": 3.5
      }
    }
  }
]
```

### localStorage key: `ft2_goals` (logros)

```json
{
  "achievements": ["first_workout", "streak_3"],
  "achievementDates": {
    "first_workout": "2026-04-01",
    "streak_3": "2026-04-04"
  }
}
```

### Otras claves de localStorage

| Clave | Tipo | Descripcion |
|-------|------|-------------|
| `ft2_theme` | string | `"dark"` o `"light"` (preferencia manual) |
| `ft2_pwa_dismissed` | string | `"1"` si cerro el banner PWA |
| `ft2_timer_default` | string | Segundos default del timer (ej: `"60"`) |
| `ft2_timer_auto` | string | Si existe, auto-start timer al completar set |

---

## Ciclos de Entrenamiento

### Rotacion Semanal

| Dia | Ciclo | Enfoque |
|-----|-------|---------|
| Domingo | Descanso | - |
| Lunes | A | Empuje + Core |
| Martes | B | Jalon + Core |
| Miercoles | C | Piernas + Postura |
| Jueves | A | Empuje + Core |
| Viernes | B | Jalon + Core |
| Sabado | C | Piernas + Postura |

### Ejercicios por Ciclo

**Ciclo A - Empuje + Core (8 ejercicios):**
Press de Banca, Press Inclinado, Press Militar, Elevacion Lateral, Extension Triceps, Plancha Frontal, Rueda Abdominal, Dead Bug

**Ciclo B - Jalon + Core (8 ejercicios):**
Remo Inclinado, Remo a Una Mano, Pajaro, Curl Biceps, Curl Martillo, Bird Dog, Face Pull, Rueda Abdominal

**Ciclo C - Piernas + Postura (7 ejercicios):**
Goblet Squat, Peso Muerto Rumano, Sentadilla Bulgara, KB Swing, Elevacion Talones, Puente Gluteo, Y-T-W

### Equipo Disponible

- Banco ajustable
- Mancuernas ajustables 5-55 lb
- Kettlebell ajustable 5-55 lb
- Eliptica, Caminadora, Bicicleta spinning
- Rueda abdominal con soporte para codos y rodillera

---

## Imagenes de Ejercicios

Las fotos vienen del repositorio open source:
```
https://raw.githubusercontent.com/yuhonas/free-exercise-db/main/exercises/{NOMBRE}/0.jpg
https://raw.githubusercontent.com/yuhonas/free-exercise-db/main/exercises/{NOMBRE}/1.jpg
```

El mapeo esta en el objeto `EX_PHOTOS` dentro del JavaScript. Si una imagen falla, el `onerror` la oculta automaticamente.

---

## Sistema de Logros

| ID | Nombre | Condicion |
|----|--------|-----------|
| first_workout | Primera Sesion | 1+ sesion guardada |
| streak_3 | Racha de 3 | 3 dias seguidos entrenando |
| streak_7 | Semana Completa | 7 dias seguidos |
| streak_30 | Mes Imparable | 30 dias seguidos |
| total_10 | 10 Sesiones | 10 sesiones totales |
| total_50 | 50 Sesiones | 50 sesiones totales |
| total_100 | Centenario | 100 sesiones totales |
| volume_10k | 10K lbs Vol. | 10,000 lbs de volumen acumulado |

---

## Deploy y Actualizaciones

### Prerrequisitos

- Git instalado
- GitHub CLI (`gh`) instalado y autenticado como `gcardenasg-ux`
- Repositorio: `gcardenasg-ux/fittracker` en branch `master`

### Proceso de actualizacion

```bash
cd C:/Tools/FitTracker
# Hacer cambios en index.html
git add index.html
git commit -m "Descripcion del cambio"
git push
```

GitHub Pages se reconstruye automaticamente en ~1 minuto.

### Verificar estado del deploy

```bash
"/c/Program Files/GitHub CLI/gh.exe" api repos/gcardenasg-ux/fittracker/pages
# Buscar: "status": "built"
```

---

## Posibles Mejoras Futuras

- Service Worker (`sw.js`) para cache offline completo
- Notificaciones push para recordatorios de entrenamiento
- Graficas de volumen semanal/mensual
- Editor de rutinas (crear/modificar ciclos)
- Registro de medidas corporales (peso, circunferencias)
- Modo tablet con layout de 2 columnas para iPad
- Tema personalizable (elegir color acento)
- Backup automatico periodico via Web Share API
