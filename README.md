# Spectral Random Hydraulic Conductivity Field Generator (3D)

> Basado en el toolbox MATLAB de **Wolfgang Nowak** (IWS, Universidad de Stuttgart)  
> Based on **Wolfgang Nowak**'s MATLAB toolbox (IWS, University of Stuttgart)

---

## Tabla de Contenidos / Table of Contents

- [Español](#español)
  - [¿Qué es este proyecto?](#qué-es-este-proyecto)
  - [Instalación y uso — Windows](#instalación-y-uso--windows-paso-a-paso)
  - [Personalizar parámetros](#cómo-personalizar-los-parámetros)
  - [Archivos de salida](#archivos-de-salida)
  - [Referencias](#referencias)
- [English](#english)
  - [What is this project?](#what-is-this-project)
  - [Installation and usage — Windows](#installation-and-usage--windows-step-by-step)
  - [Customize parameters](#how-to-customize-parameters)
  - [Output files](#output-files)
  - [References](#references-1)

---

# Español

## ¿Qué es este proyecto?

Este repositorio contiene un notebook de Jupyter que genera **campos tridimensionales aleatorios de conductividad hidráulica** para acuíferos heterogéneos. La conductividad hidráulica K controla qué tan fácilmente fluye el agua a través del subsuelo y varía espacialmente varios órdenes de magnitud en acuíferos naturales.

El notebook implementa el **método espectral de incrustación circulante** (Dietrich & Newsam, 1993), el algoritmo más eficiente para generar este tipo de campos en dominios 3D regulares. El método trabaja con el **logaritmo natural** de K (ln K), porque esta variable sigue una distribución aproximadamente normal (Gaussiana), lo que permite usar geoestadística clásica.

### ¿Para qué sirve?

Los campos generados se usan como entrada para:

- Modelos de flujo subterráneo (MODFLOW, FEFLOW, OpenGeoSys)
- Simulaciones de transporte de contaminantes
- Análisis de incertidumbre y riesgo en acuíferos
- Optimización de redes de pozos de remediación

### Contenido del repositorio

```
kfield-generator/
├── generacion_Kfield.ipynb    ← Notebook principal (ejecutar este)
├── requirements.txt            ← Dependencias Python
└── modules/
    ├── __init__.py
    ├── config_structs.py       ← Estructuras de datos (Grid, Model)
    └── generate_randomfield.py ← Generador espectral (algoritmo central)
```

---

## Instalación y uso — Windows (paso a paso)

### Paso 1 — Verificar si Python está instalado

Abre el **Símbolo del sistema**:
- Presiona la tecla `Windows`, escribe `cmd` y presiona `Enter`.

En la ventana negra que se abre, escribe lo siguiente y presiona `Enter`:

```
python --version
```

- Si ves algo como `Python 3.11.0` → Python ya está instalado. Pasa al Paso 3.
- Si ves un error → sigue el Paso 2.

---

### Paso 2 — Instalar Python

1. Abre tu navegador y ve a: **https://www.python.org/downloads/**
2. Haz clic en el botón amarillo **"Download Python 3.x.x"**
3. Ejecuta el archivo `.exe` descargado
4. ⚠️ **MUY IMPORTANTE:** en la primera pantalla del instalador, marca la casilla **"Add Python to PATH"** antes de hacer clic en cualquier botón

```
┌────────────────────────────────────────────────────────┐
│  Install Python 3.x.x                                  │
│                                                        │
│  ☑ Add Python 3.x to PATH   ← MARCAR ESTA CASILLA     │
│                                                        │
│  [ Install Now ]   [ Customize installation ]          │
└────────────────────────────────────────────────────────┘
```

5. Haz clic en **"Install Now"**
6. Espera a que termine y cierra el instalador
7. **Cierra y vuelve a abrir** el Símbolo del sistema
8. Verifica con `python --version` — ahora debe mostrar la versión instalada

---

### Paso 3 — Descargar el proyecto

**Opción A — Sin Git (recomendada para principiantes):**

1. Ve a: **https://github.com/abelardo1685/kfield-generator**
2. Haz clic en el botón verde **`< > Code`**
3. Selecciona **"Download ZIP"**
4. Cuando termine la descarga, haz clic derecho en el archivo ZIP → **"Extraer todo..."**
5. Elige una ubicación fácil de recordar, por ejemplo:
   ```
   C:\Users\TuNombre\Documents\kfield-generator
   ```
6. Haz clic en **"Extraer"**

**Opción B — Con Git (si ya lo tienes instalado):**

En el Símbolo del sistema:
```
git clone https://github.com/abelardo1685/kfield-generator.git
```

---

### Paso 4 — Abrir el Símbolo del sistema en la carpeta del proyecto

1. Abre el **Explorador de archivos** (tecla `Windows + E`)
2. Navega hasta la carpeta donde extrajiste el proyecto (p.ej. `Documents\kfield-generator`)
3. Haz clic en la **barra de direcciones** (donde dice la ruta, p.ej. `Este equipo > Documentos > kfield-generator`)
4. Escribe `cmd` y presiona `Enter`

Se abrirá el Símbolo del sistema ya posicionado en la carpeta correcta. El prompt debe mostrar algo como:

```
C:\Users\TuNombre\Documents\kfield-generator>
```

---

### Paso 5 — Crear un entorno virtual

Un **entorno virtual** es una instalación de Python aislada, solo para este proyecto. Evita conflictos con otros programas que usen Python en tu computadora.

Escribe el siguiente comando y presiona `Enter`:

```
python -m venv venv
```

Espera 5–10 segundos. Se creará una carpeta llamada `venv` dentro del proyecto. **No la borres.**

---

### Paso 6 — Activar el entorno virtual

Escribe:

```
venv\Scripts\activate
```

Sabrás que funcionó porque el prompt cambia y aparece `(venv)` al inicio:

```
(venv) C:\Users\TuNombre\Documents\kfield-generator>
```

> ⚠️ **Importante:** debes repetir este paso (`venv\Scripts\activate`) cada vez que abras una nueva ventana del Símbolo del sistema para trabajar con este proyecto.

---

### Paso 7 — Instalar las dependencias

Con el entorno activado (el prompt debe mostrar `(venv)`), escribe:

```
pip install -r requirements.txt
```

Este comando descarga e instala automáticamente todos los paquetes necesarios (NumPy, SciPy, Matplotlib, Jupyter). Puede tardar entre 2 y 10 minutos dependiendo de tu conexión a internet.

Verás mensajes de descarga en la pantalla — es completamente normal. Al finalizar correctamente verás una línea similar a:

```
Successfully installed jupyter-1.1.1 matplotlib-3.10.8 numpy-2.4.1 scipy-1.17.0 ...
```

---

### Paso 8 — Abrir Jupyter Lab

Con el entorno activado, escribe:

```
jupyter lab
```

Ocurrirá lo siguiente:
1. Verás varios mensajes en el Símbolo del sistema — déjalo abierto, no lo cierres
2. Tu navegador web (Chrome, Edge, Firefox) se abrirá automáticamente con la interfaz de Jupyter Lab

Si el navegador **no** se abre automáticamente:
- Busca en el Símbolo del sistema una línea que diga algo como:
  ```
  http://localhost:8888/lab?token=abc123...
  ```
- Copia esa dirección completa y pégala en tu navegador

---

### Paso 9 — Abrir el notebook

En el panel izquierdo de Jupyter Lab verás los archivos del proyecto. Haz **doble clic** en:

```
generacion_Kfield.ipynb
```

El notebook se abrirá en el panel central con todas las secciones documentadas.

---

### Paso 10 — Ejecutar el notebook

**Opción A — Ejecutar todo de una vez (recomendado la primera vez):**

1. En el menú superior, haz clic en **"Run"**
2. Selecciona **"Run All Cells"**
3. Espera mientras las celdas se ejecutan en orden (el símbolo `[*]` indica que está corriendo; se convierte en un número cuando termina)

**Opción B — Ejecutar celda por celda (para explorar):**

1. Haz clic sobre la primera celda de código
2. Presiona **`Shift + Enter`** para ejecutarla y pasar a la siguiente
3. Repite para cada celda en orden de arriba hacia abajo

> El tiempo total de ejecución es aproximadamente **15–30 segundos** con los parámetros por defecto.

---

### ✅ ¡Listo! ¿Qué verás al terminar?

Al ejecutar el notebook completo aparecerán:

1. **Gráfica del variograma** — covarianza y semivariograma teóricos en las direcciones x e y
2. **Mapa de una realización** — cortes horizontales (tope, medio, base) y secciones verticales del acuífero
3. **Mosaico del ensemble** — múltiples realizaciones comparadas con la misma escala de color
4. **Estadísticas** — mapas de media y varianza + histograma de distribución de ln(K)
5. **Realizaciones guardadas** — archivo `.npz` en la carpeta `Kfields_output/`

---

### 🔧 Solución de problemas comunes

| Problema | Causa probable | Solución |
|----------|----------------|----------|
| `python` no reconocido | Python no está en PATH | Reinstala Python marcando "Add Python to PATH" |
| `venv\Scripts\activate` da error | PowerShell bloqueado | Usa `cmd` en lugar de PowerShell |
| `pip install` falla | Sin conexión a internet | Verifica tu conexión y vuelve a intentarlo |
| El navegador no abre | Puerto ocupado | Busca la URL con token en el Símbolo del sistema |
| `ModuleNotFoundError` al ejecutar | Entorno no activado | Cierra Jupyter, activa el entorno y ábrelo de nuevo |

---

## ¿Cómo personalizar los parámetros?

Todos los parámetros están en la **Sección 1** del notebook (Celda 4), bajo el encabezado:

```
# ╔══════════════════════════════════════════════════╗
# ║   PARÁMETROS DE ENTRADA — modifica aquí         ║
# ╚══════════════════════════════════════════════════╝
```

Los más importantes son:

| Parámetro | Qué controla | Valor por defecto |
|-----------|--------------|-------------------|
| `n_pts_y`, `n_pts_x`, `n_pts_z` | Número de nodos de la grilla 3D | 60 × 60 × 20 |
| `d_pts_y`, `d_pts_x`, `d_pts_z` | Tamaño de celda [m] | 5 × 5 × 2 m |
| `lnK_mean` | Media de ln(K) → conductividad promedio | -4.0 |
| `lnK_variance` | Varianza → grado de heterogeneidad | 1.0 |
| `lambda_y`, `lambda_x`, `lambda_z` | Longitudes de correlación [m] | 30, 60, 5 m |
| `kappa` | Suavidad del variograma (0.5 = exponencial) | 0.5 |
| `n_realizations` | Realizaciones a visualizar | 6 |
| `N_save` | Realizaciones a guardar en disco | 5 |

Después de modificar, vuelve a ejecutar todo: **Run → Run All Cells**.

---

## Archivos de salida

El notebook crea la carpeta `Kfields_output/` con archivos `.npz` (NumPy comprimido):

```
kfield-generator/
└── Kfields_output/
    └── Kfield_3D_N5_20260516_140000.npz
```

Para cargar el archivo en otro script Python:

```python
import numpy as np

data    = np.load('Kfields_output/Kfield_3D_N5_20260516_140000.npz')
lnK_ens = data['lnK_ensemble']   # shape: (N, ny+1, nx+1, nz+1)
K_ens   = data['K_ensemble']     # K en m/s
x_vec   = data['x_vec']          # coordenadas x [m]
y_vec   = data['y_vec']          # coordenadas y [m]
z_vec   = data['z_vec']          # coordenadas z [m]

# Ejemplo: primera realización, capa superficial (z=0)
lnK_real1_superficie = lnK_ens[0, :, :, 0]
```

---

## Referencias

1. **Dietrich, C.R. & Newsam, G.N. (1993).** A fast and exact method for multidimensional Gaussian stochastic simulations. *Water Resources Research*, 29(8):2861–2869. https://doi.org/10.1029/93WR01070
2. **Dietrich, C.R. & Newsam, G.N. (1997).** Fast and exact simulation of stationary Gaussian processes through circulant embedding of the covariance matrix. *SIAM J. Sci. Comput.*, 18(4):1088–1107. https://doi.org/10.1137/S1064827592240555
3. **Nowak, W., Tenkleve, S. & Cirpka, O.A. (2003).** Efficient computation of linearized cross-covariance and auto-covariance matrices of interdependent quantities. *Mathematical Geology*, 35(1):53–66. https://doi.org/10.1023/A:1022365112368
4. **Kitanidis, P.K. (1997).** *Introduction to Geostatistics: Applications in Hydrogeology*. Cambridge University Press. ISBN: 978-0521587471
5. **Zinn, B. & Harvey, C.F. (2003).** When good statistical models of aquifer heterogeneity go bad. *Water Resources Research*, 39(3):1051. https://doi.org/10.1029/2001WR001146
6. **Freeze, R.A. (1975).** A stochastic-conceptual analysis of one-dimensional groundwater flow in nonuniform homogeneous media. *Water Resources Research*, 11(5):725–741. https://doi.org/10.1029/WR011i005p00725

---

# English

## What is this project?

This repository contains a Jupyter notebook that generates **3D random hydraulic conductivity fields** for heterogeneous aquifers. Hydraulic conductivity K controls how easily water flows through the subsurface, and varies spatially by several orders of magnitude in natural aquifers.

The notebook implements the **spectral circulant embedding method** (Dietrich & Newsam, 1993), the most computationally efficient algorithm for generating such fields on regular 3D grids. The method works with the **natural logarithm** of K (ln K), because this variable follows an approximately Gaussian distribution, enabling the use of classical geostatistics.

### Applications

- Groundwater flow models (MODFLOW, FEFLOW, OpenGeoSys)
- Contaminant transport simulations
- Aquifer uncertainty and risk analysis
- Remediation well network optimization

### Repository structure

```
kfield-generator/
├── generacion_Kfield.ipynb    ← Main notebook (run this)
├── requirements.txt            ← Python dependencies
└── modules/
    ├── __init__.py
    ├── config_structs.py       ← Data structures (Grid, Model)
    └── generate_randomfield.py ← Spectral generator (core algorithm)
```

---

## Installation and usage — Windows (step by step)

### Step 1 — Check if Python is installed

Open the **Command Prompt** (press `Windows` key, type `cmd`, press `Enter`):

```
python --version
```

- If you see `Python 3.x.x` → Python is installed. Skip to Step 3.
- If you get an error → follow Step 2.

---

### Step 2 — Install Python

1. Go to: **https://www.python.org/downloads/**
2. Click the yellow **"Download Python 3.x.x"** button
3. Run the downloaded `.exe` file
4. ⚠️ **CRITICAL:** on the first installer screen, check **"Add Python to PATH"** before clicking anything else
5. Click **"Install Now"** and wait
6. Close and reopen Command Prompt, then verify with `python --version`

---

### Step 3 — Download the project

**Option A — Without Git (recommended for beginners):**

1. Go to: **https://github.com/abelardo1685/kfield-generator**
2. Click the green **`< > Code`** button → **"Download ZIP"**
3. Right-click the ZIP → **"Extract All..."** → choose a folder like `Documents\kfield-generator`

**Option B — With Git:**
```
git clone https://github.com/abelardo1685/kfield-generator.git
```

---

### Step 4 — Open Command Prompt in the project folder

1. Open **File Explorer** and navigate to the project folder
2. Click the **address bar** at the top, type `cmd`, press `Enter`

The prompt should show:
```
C:\Users\YourName\Documents\kfield-generator>
```

---

### Step 5 — Create a virtual environment

```
python -m venv venv
```

This creates an isolated Python installation for this project only. A `venv` folder will appear — do not delete it.

---

### Step 6 — Activate the virtual environment

```
venv\Scripts\activate
```

The prompt will change to show `(venv)` at the start:
```
(venv) C:\Users\YourName\Documents\kfield-generator>
```

> You must run this command every time you open a new Command Prompt window.

---

### Step 7 — Install dependencies

```
pip install -r requirements.txt
```

Downloads and installs NumPy, SciPy, Matplotlib, and Jupyter. Takes 2–10 minutes. When done you will see:
```
Successfully installed jupyter-... matplotlib-... numpy-... scipy-...
```

---

### Step 8 — Open Jupyter Lab

```
jupyter lab
```

Your browser will open automatically at `http://localhost:8888/lab`. If not, copy the URL with token shown in the Command Prompt and paste it into your browser.

---

### Step 9 — Open the notebook

In the left panel of Jupyter Lab, double-click:
```
generacion_Kfield.ipynb
```

---

### Step 10 — Run the notebook

**Run all at once:** menu **Run** → **Run All Cells**

**Run cell by cell:** click a cell → press **`Shift + Enter`**

Total execution time: ~15–30 seconds with default parameters.

---

### ✅ What you will see

1. Theoretical variogram plots
2. 3D ln(K) and K maps (horizontal slices + vertical cross-sections)
3. Ensemble mosaic (multiple realizations)
4. Ensemble mean, variance and histogram
5. Saved `.npz` file in `Kfields_output/`

---

### 🔧 Troubleshooting

| Problem | Likely cause | Solution |
|---------|-------------|---------|
| `python` not recognized | Not in PATH | Reinstall Python checking "Add to PATH" |
| `activate` fails in PowerShell | Execution policy | Use `cmd` instead of PowerShell |
| `pip install` fails | No internet | Check connection and retry |
| Browser does not open | Port busy | Copy the URL+token from the terminal |
| `ModuleNotFoundError` | Env not active | Re-activate: `venv\Scripts\activate` |

---

## How to customize parameters?

All parameters are in **Section 1** of the notebook (Cell 4):

| Parameter | Controls | Default |
|-----------|----------|---------|
| `n_pts_y`, `n_pts_x`, `n_pts_z` | Grid size | 60 × 60 × 20 |
| `d_pts_y`, `d_pts_x`, `d_pts_z` | Cell size [m] | 5 × 5 × 2 m |
| `lnK_mean` | ln(K) mean → average conductivity | -4.0 |
| `lnK_variance` | Variance → heterogeneity degree | 1.0 |
| `lambda_y`, `lambda_x`, `lambda_z` | Correlation lengths [m] | 30, 60, 5 m |
| `kappa` | Variogram smoothness (0.5 = exponential) | 0.5 |
| `n_realizations` | Realizations to visualize | 6 |
| `N_save` | Realizations to save to disk | 5 |

---

## Output files

```python
import numpy as np

data    = np.load('Kfields_output/Kfield_3D_N5_YYYYMMDD_HHMMSS.npz')
lnK_ens = data['lnK_ensemble']   # shape: (N, ny+1, nx+1, nz+1)
K_ens   = data['K_ensemble']     # K in m/s
x_vec   = data['x_vec']
y_vec   = data['y_vec']
z_vec   = data['z_vec']
```

---

## References

1. **Dietrich & Newsam (1993).** *Water Resour. Res.*, 29(8). https://doi.org/10.1029/93WR01070
2. **Dietrich & Newsam (1997).** *SIAM J. Sci. Comput.*, 18(4). https://doi.org/10.1137/S1064827592240555
3. **Nowak et al. (2003).** *Math. Geol.*, 35(1). https://doi.org/10.1023/A:1022365112368
4. **Kitanidis (1997).** *Introduction to Geostatistics*. Cambridge University Press.
5. **Zinn & Harvey (2003).** *Water Resour. Res.*, 39(3). https://doi.org/10.1029/2001WR001146
6. **Freeze (1975).** *Water Resour. Res.*, 11(5). https://doi.org/10.1029/WR011i005p00725

---

*Developed at UNAM — Posgrado en Ciencias de la Tierra*  
*Author: Abelardo Rodriguez Pretelin — abelardo.rodriguez.pretelin@gmail.com*
