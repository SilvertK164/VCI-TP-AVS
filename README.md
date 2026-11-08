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
| TP2 | *pendiente* | |
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

Abrir `TP01/TP1.ipynb` y ejecutar las celdas en orden. El notebook lee las imágenes de `TP01/data/`
con rutas relativas a su propia carpeta, que es el directorio de trabajo que usa Jupyter por defecto.

Para ejecutarlo de punta a punta sin abrir Jupyter:

```bash
cd TP01
jupyter nbconvert --to notebook --execute --inplace TP1.ipynb
```

## Dependencias

| Paquete | Uso |
|---|---|
| `numpy` | operaciones sobre arrays e histogramas |
| `opencv-python` | lectura de imágenes (`cv2.imread`) |
| `matplotlib` | visualización |
| `jupyter`, `ipykernel` | ejecución de los notebooks |

Las versiones mínimas están en [`pyproject.toml`](pyproject.toml) y las versiones exactas con las que
se ejecutó el notebook en [`requirements.txt`](requirements.txt).

## Estructura

```
├── TP01/
│   ├── TP1.ipynb          # notebook del TP1 (con salidas)
│   └── data/              # imágenes de la cátedra
│       ├── img1_tp.png
│       ├── img2_tp.png
│       └── white_patch/
├── pyproject.toml         # dependencias (versiones mínimas)
├── requirements.txt       # versiones exactas
└── .python-version
```
