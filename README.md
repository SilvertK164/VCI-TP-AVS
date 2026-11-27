# Visión por Computadora I – Trabajos prácticos

Trabajos prácticos de **Visión por Computadora I**, Especialización en Inteligencia Artificial (CEIA), FIUBA.

## Integrantes

| Nombre | Usuario de GitHub |
|---|---|
| Hernando Alexis González | [halexisgonzalez](https://github.com/halexisgonzalez) |
| Victoria Villalba Tevez | [vivillalbatevez](https://github.com/vivillalbatevez) |
| Silvert Kevin Quispe Pacompia | [SilvertK164](https://github.com/SilvertK164) |

## Trabajos prácticos

| TP | Notebook | Temas |
|---|---|---|
| TP1 | [`TP01/TP1.ipynb`](TP01/TP1.ipynb) | White Patch (balance de blancos) e histogramas en escala de grises |
| TP2 | [`TP02/TP2.ipynb`](TP02/TP2.ipynb) | Detector de máximo enfoque en video con una métrica en el dominio de la frecuencia y *unsharp masking* |
| TP3 | *pendiente* | |

### TP1

- **Parte 1 (White Patch).** Implementación del algoritmo con el máximo de cada canal, resultados sobre
  las imágenes de `white_patch/`, análisis de las fallas (máximo definido por pocos píxeles, canal
  saturado, luz casi monocromática) y una variante más robusta que usa el percentil 99 en lugar del máximo.
- **Parte 2 (Histogramas).** Lectura en escala de grises de `img1_tp.png` e `img2_tp.png`, histogramas
  con 256 y 32 bins, comparación entre ambos (son idénticos: una imagen es la otra con los píxeles
  ordenados) y discusión sobre el uso de histogramas como *features* para clasificación/detección.

Las imágenes están copiadas en [`TP01/data/`](TP01/data/) desde
[`Material_TPs/TP1`](https://github.com/FIUBA-Posgrado-Inteligencia-Artificial/vision_computadora_I/tree/main/Material_TPs/TP1)
del repositorio de la cátedra, para que el notebook sea autocontenido.

### TP2

- **Métrica de enfoque.** Implementación de la métrica `FM` de *Image Sharpness Measure for Blurred
  Images in Frequency Domain* (De y Masilamani, 2013): proporción de coeficientes de la FFT cuya magnitud
  supera `max / 1000`.
- **Experimentos.** Medición frame a frame de `focus_video.mov` sobre el frame completo y sobre una ROI
  central del 10% del área. Para cada uno se detecta automáticamente el frame de máximo enfoque y la
  región de máximo enfoque (tramo continuo con `FM` ≥ 90% del máximo).
- **Puntos extra.** *Unsharp masking* sobre todos los frames y recálculo de la métrica: con el mismo
  umbral, la zona de enfoque se expande de 37 a 62 frames (frame completo) y de 9 a 35 frames (ROI).

Detalle de método y resultados en [`TP02/README.md`](TP02/README.md). El video está copiado en
[`TP02/Data/`](TP02/Data/) desde
[`Material_TPs/TP2`](https://github.com/FIUBA-Posgrado-Inteligencia-Artificial/vision_computadora_I/tree/main/Material_TPs/TP2).

## Cómo correrlo

Requisitos: Python 3.12 o superior.

### Con pip

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux / macOS
source .venv/bin/activate

pip install -r requirements.txt
jupyter lab
```

### Con uv

```bash
uv sync
uv run jupyter lab
```

Abrir el notebook del TP (`TP01/TP1.ipynb` o `TP02/TP2.ipynb`) y ejecutar las celdas en orden. Cada
notebook lee sus datos (`TP01/data/`, `TP02/Data/`) con rutas relativas a su propia carpeta, que es el
directorio de trabajo que usa Jupyter por defecto.

Para ejecutarlos de punta a punta sin abrir Jupyter:

```bash
cd TP01
jupyter nbconvert --to notebook --execute --inplace TP1.ipynb
cd ../TP02
jupyter nbconvert --to notebook --execute --inplace TP2.ipynb
```

## Dependencias

| Paquete | Uso |
|---|---|
| `numpy` | operaciones sobre arrays e histogramas |
| `opencv-python` | lectura de imágenes y video, filtrado gaussiano |
| `matplotlib` | visualización |
| `jupyter`, `ipykernel` | ejecución de los notebooks |

Las versiones mínimas están en [`pyproject.toml`](pyproject.toml) y las versiones exactas con las que
se ejecutó el notebook en [`requirements.txt`](requirements.txt).

## Estructura

```
├── TP01/
│   ├── TP1.ipynb          # notebook del TP1 (con salidas)
│   └── data/              # copia de Material_TPs/TP1 de la cátedra
│       ├── img1_tp.png
│       ├── img2_tp.png
│       ├── segmentacion.png  # no se usa en la consigna del TP1
│       └── white_patch/
├── TP02/
│   ├── README.md          # resumen del TP2: método, resultados y figuras
│   ├── TP2.ipynb          # notebook del TP2 (con salidas)
│   ├── Data/
│   │   └── focus_video.mov   # copia de Material_TPs/TP2 de la cátedra
│   └── figuras/           # figuras exportadas del notebook
├── pyproject.toml         # dependencias (versiones mínimas)
├── requirements.txt       # versiones exactas
└── .python-version
```
