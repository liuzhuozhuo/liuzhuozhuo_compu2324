# Física Computacional 2023/24

Códigos y resultados de las entregas de la asignatura de Física Computacional (curso 2023/24).
Cada carpeta es un proyecto independiente, numerado y nombrado según el problema físico que resuelve.

| Carpeta | Problema | Método | Entrega original |
|---|---|---|---|
| [`01-solar-system`](01-solar-system) | Órbitas del sistema solar (heliocéntrico y geocéntrico), conservación de la energía y periodos | Algoritmo de Verlet en C | Obligatoria 1 |
| [`02-ising-model`](02-ising-model) | Modelo de Ising 2D: magnetización frente a temperatura para distintos tamaños de red | Monte Carlo (Metropolis) | Obligatoria 2 |
| [`03-schrodinger-equation`](03-schrodinger-equation) | Ecuación de Schrödinger 1D con un potencial barrera, conservación de la norma | Método de Crank–Nicolson | Obligatoria 3 |
| [`04-earth-moon-rocket`](04-earth-moon-rocket) | Viaje de un cohete de la Tierra a la Luna (problema de tres cuerpos) | Runge–Kutta 4 con paso adaptativo | Obligatoria 4 |
| [`05-lennard-jones-gas`](05-lennard-jones-gas) | Gas de partículas con potencial de Lennard-Jones: distribución de velocidades, presión, temperatura crítica | Dinámica molecular (Verlet) + optimización/paralelización | Voluntario 1 |
| [`06-double-pendulum`](06-double-pendulum) | Péndulo doble: mapas de Poincaré, estabilidad y coeficientes de Lyapunov | Runge–Kutta 4 | Voluntario 2 |
| [`c-utils`](c-utils) | Funciones auxiliares en C (vectores, números aleatorios) | – | – |

## Estructura de cada proyecto

```
NN-proyecto/
├── *.c / *.py / *.ipynb   código de simulación, análisis y animación
├── data/                  datos generados por la simulación
├── figures/               gráficas
├── videos/                animaciones (no incluidas en git, ver abajo)
├── report/                memoria en LaTeX (main.tex + main.pdf), en los voluntarios
└── benchmark/ · optimization/   pruebas de rendimiento
```

Los scripts `.py` de animación se ejecutan desde la raíz del repositorio
(p. ej. `python 01-solar-system/animacion_planetas.py`); los notebooks y los programas en C,
desde la carpeta de su proyecto (p. ej. `cd 01-solar-system && gcc planet_orbits.c -lm && ./a.out`).

## Archivos pesados (vídeos y datos grandes)

Los vídeos `.mp4` y los ficheros de datos de más de ~1 MB no están en el repositorio,
sino como archivos de la [release `data-v1`](https://github.com/liuzhuozhuo/liuzhuozhuo_compu2324/releases/tag/data-v1).
Cada `.zip` conserva las rutas del repositorio, así que basta con descomprimirlo en la raíz:

```bash
# todo
for f in $(curl -s https://api.github.com/repos/liuzhuozhuo/liuzhuozhuo_compu2324/releases/tags/data-v1 \
           | grep -o 'https://[^"]*\.zip'); do curl -sLO "$f"; done
unzip -o '*.zip'

# o solo uno, p. ej. los vídeos del modelo de Ising
curl -LO https://github.com/liuzhuozhuo/liuzhuozhuo_compu2324/releases/download/data-v1/02-ising-model-videos.zip
unzip -o 02-ising-model-videos.zip
```

| Archivo | Contenido |
|---|---|
| `01-solar-system-videos.zip` | Animaciones de las órbitas (heliocéntricas y geocéntricas, también con condiciones en el afelio) |
| `01-solar-system-data.zip` | Energía por planeta y energía total (`data/energy*.txt`) |
| `02-ising-model-videos.zip` | Evolución de la red de espines para N = 8…240 y T = 0.5…4.5 |
| `03-schrodinger-equation-videos.zip` | Evolución de la función de onda para λ = 0.3 y 1 |
| `04-earth-moon-rocket-videos.zip` | Trayectoria del cohete |
| `04-earth-moon-rocket-data.zip` | Trayectorias calculadas (`data/datos*.txt`) |
| `05-lennard-jones-gas-videos.zip` | Animaciones de las partículas para cada apartado |
| `05-lennard-jones-gas-data.zip` | Posiciones y velocidades de cada simulación (`data/*/posiciones_*.txt`, `velocidades_*.txt`) |

## Créditos
El código original de `animacion_planetas.py` ha sido tomado de https://github.com/jbermejovega/fisicacomputacional,
y se ha modificado ligeramente para ajustarlo a las necesidades de cada apartado.

Se ha empleado también Copilot para ciertas recomendaciones y autocompletar al programar, sobre todo en los voluntarios.
