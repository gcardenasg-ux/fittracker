# FitTracker Pro - Guia de Usuario

## Instalacion

### En iPhone o iPad

1. Abre **Safari** (debe ser Safari, no Chrome ni otro navegador)
2. Ve a: **https://gcardenasg-ux.github.io/fittracker/**
3. Toca el boton **Compartir** (cuadro con flecha hacia arriba)
4. Desplazate y selecciona **"Agregar a pantalla de inicio"**
5. Escribe el nombre **"FitTracker"** y toca **Agregar**

La app aparece como icono en tu pantalla de inicio y se abre sin barra de navegador, como app nativa.

> **Importante:** Repite estos pasos tanto en tu iPhone como en tu iPad. Cada dispositivo tiene su propia copia de la app.

### En computadora (Windows/Mac)

Simplemente abre en cualquier navegador: https://gcardenasg-ux.github.io/fittracker/

---

## Uso Diario

### Registrar un Entrenamiento

1. Abre la app - automaticamente muestra el workout del dia
2. El primer ejercicio aparece expandido. Los demas se abren tocandolos
3. Para cada serie:
   - Ingresa el **peso** en libras
   - Ingresa las **repeticiones**
   - Toca la casilla **checkmark** para marcar como completada
4. Si necesitas mas series, toca **"+ Agregar serie"**
5. Al terminar, agrega notas opcionales y toca **"TERMINAR SESION"**

### Cardio (Opcional)

Debajo de los ejercicios hay una seccion de cardio:
1. Selecciona la maquina (Eliptica, Caminadora o Bicicleta)
2. Ingresa duracion en minutos y distancia opcional

### Temporizador de Descanso

1. Toca **"TEMPORIZADOR DE DESCANSO"** debajo de los ejercicios
2. Selecciona el tiempo: 30s, 60s, 90s o 120s
3. Suena un beep y vibra cuando termina
4. El timer tambien se activa automaticamente al completar una serie

### Cambiar Dia

La franja de dias en la parte superior permite ver el workout de otro dia. Toca el dia que quieras revisar.

### Cambiar Tema (Claro/Oscuro)

Toca el icono de sol/luna en la esquina superior derecha del header. La app tambien detecta automaticamente si tu dispositivo esta en modo oscuro o claro.

---

## Navegacion

La barra inferior tiene 4 pestanas:

| Icono | Nombre | Funcion |
|-------|--------|---------|
| Rayo | **HOY** | Workout del dia, registro de series |
| Grafica | **PROGRESO** | Graficas de peso y volumen por ejercicio + Metas y Logros |
| Calendario | **CALENDARIO** | Vista mensual, rachas, estadisticas |
| Reloj | **HISTORIAL** | Todas las sesiones pasadas |

### Progreso y Metas

En la pestana PROGRESO hay dos sub-pestanas:
- **PROGRESO**: Selecciona un ejercicio para ver graficas de peso maximo y volumen total por sesion
- **METAS**: Sesiones de la semana, racha actual/mejor, y logros desbloqueados

---

## Sincronizacion entre iPhone y iPad

> **Los datos de entrenamiento se guardan localmente en cada dispositivo.** Para que tu iPhone y tu iPad tengan los mismos datos, necesitas exportar e importar manualmente.

### Opcion 1: Via iCloud Drive (Recomendada)

**Exportar desde el dispositivo con datos mas recientes:**

1. Abre FitTracker en tu iPhone (o el dispositivo que tenga los datos)
2. Toca **COMPARTIR** en la barra inferior de la app
3. Se abre el menu de compartir de iOS
4. Selecciona **"Guardar en Archivos"**
5. Navega a **iCloud Drive** y elige una carpeta (ej: "FitTracker Backups")
6. Toca **Guardar**

**Importar en el otro dispositivo:**

1. Abre FitTracker en tu iPad (o el dispositivo destino)
2. Toca **IMPORTAR** en la barra inferior
3. Se abre el selector de archivos
4. Navega a **iCloud Drive** > la carpeta donde guardaste
5. Selecciona el archivo `FitTracker_Backup_YYYY-MM-DD.json`
6. Aparece un mensaje: "X sesiones importadas"

> **Los datos se FUSIONAN, no se reemplazan.** Si ya tenias sesiones en el iPad, se mantienen y se agregan las nuevas del iPhone. No hay riesgo de perder datos.

### Opcion 2: Via Google Drive

**Exportar:**

1. Toca **COMPARTIR** en FitTracker
2. En el menu de compartir, selecciona **Google Drive**
3. Elige la carpeta y guarda

**Importar:**

1. Abre la app **Google Drive** en el otro dispositivo
2. Busca el archivo `FitTracker_Backup_YYYY-MM-DD.json`
3. Tocalo > Compartir > Copiar a Archivos (o descargalo)
4. En FitTracker, toca **IMPORTAR** y selecciona el archivo

### Opcion 3: Via AirDrop (rapido, sin nube)

1. En el dispositivo con datos, toca **COMPARTIR**
2. Selecciona **AirDrop** en el menu de compartir
3. Elige tu otro dispositivo
4. En el dispositivo receptor, abre el archivo con FitTracker o guardalo y luego usa **IMPORTAR**

### Frecuencia Recomendada de Sincronizacion

- **Despues de cada sesion de entrenamiento:** Exporta/comparte los datos
- **Antes de entrenar en otro dispositivo:** Importa el ultimo backup
- **Minimo una vez por semana** para mantener ambos dispositivos al dia

### Que pasa si entreno en ambos dispositivos sin sincronizar?

No hay problema. Cuando importes, los datos se fusionan inteligentemente:
- Sesiones de fechas diferentes se agregan sin conflicto
- Si hay una sesion del mismo dia y mismo workout en ambos dispositivos, la version importada reemplaza la local

---

## Preguntas Frecuentes

**La app funciona sin internet?**
Si. Una vez cargada, funciona sin conexion. Las unicas funciones que requieren internet son las fotos de los ejercicios.

**Se pierden mis datos si cierro la app?**
No. Los datos se guardan automaticamente en el almacenamiento local del navegador cada vez que modificas algo.

**Puedo perder mis datos?**
Si limpias los datos de Safari (borrar historial y datos de sitios web), se pierden los datos locales. Por eso es importante hacer backups regulares con EXPORTAR o COMPARTIR.

**Como hago backup de seguridad?**
Toca COMPARTIR o EXPORTAR regularmente y guarda el archivo en iCloud Drive. El archivo tiene nombre con fecha: `FitTracker_Backup_2026-04-06.json`.

**Como cambio el peso sugerido de un ejercicio?**
Simplemente escribe el nuevo peso en el campo. La proxima vez que hagas ese ejercicio, el ultimo peso que usaste aparecera.

**Puedo agregar mis propios ejercicios?**
En esta version no. Los ejercicios estan predefinidos en el codigo. Contacta al desarrollador para agregar ejercicios personalizados.

**Las fotos de ejercicios no cargan.**
Verifica que tengas conexion a internet. Las fotos se descargan de GitHub cada vez que abres un ejercicio.
