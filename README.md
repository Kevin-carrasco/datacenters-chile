# Data centers en Chile

Catastro y georreferenciación de data centers instalados, en construcción y planificados en Chile. El proyecto organiza una base construida a partir de fuentes públicas de la industria y de prensa especializada, y produce un sitio en Quarto con descriptivos y mapas interactivos de la ubicación de las instalaciones.

La estructura de carpetas sigue el protocolo IPO (Input-Processing-Output) de análisis reproducibles del Laboratorio de Ciencia Social Abierta (LISA-COES): <https://lisa-coes.github.io/ipo/>

## Estructura

```
├── input: información de entrada
│   ├── data
│   │   ├── original : base de datos original (Excel)
│   │   └── proc     : datos procesados (.rds)
│   ├── bib          : archivos de bibliografía
│   └── images       : imágenes externas
│
├── processing
│   ├── preparation.qmd : carga y limpieza de la base original
│   └── analysis.qmd    : descriptivos y mapas interactivos
│
├── output: productos generados por el código
│   ├── graphs : figuras
│   └── tables : tablas
│
├── index.qmd     : portada del sitio
├── _quarto.yml   : configuración del proyecto Quarto
└── README.md
```

## Reproducción

El proyecto se renderiza como un sitio web de Quarto. La opción `execute-dir: project` del archivo `_quarto.yml` fija el directorio de trabajo en la raíz, de modo que todas las rutas de los documentos se escriben desde ahí (por ejemplo, `input/data/original/`).

1. Abrir el archivo `datacenters-chile.Rproj`.
2. Renderizar `processing/preparation.qmd`, que genera los archivos `datacenters.rds` y `datacenters_geo.rds` en `input/data/proc/`.
3. Renderizar `processing/analysis.qmd` y `index.qmd`, que dependen de esos archivos.

También puede renderizarse el proyecto completo con `quarto render` desde la raíz. El sitio se escribe en la carpeta `docs/`, lista para publicarse en GitHub Pages.

### Paquetes

`readxl`, `dplyr`, `stringr`, `ggplot2`, `knitr`, `sf` y `mapgl`. Este último implementa el visor de mapas MapLibre en R y se instala desde CRAN con `install.packages("mapgl")`.

## Base de datos

Archivo original: `input/data/original/Data_centers_Chile_07062026.xlsx` (89 registros, 44 operadores).

| Variable | Descripción |
|---|---|
| `operador` | Empresa que opera la instalación |
| `data_center` | Nombre o identificador de la instalación |
| `direccion` | Dirección declarada |
| `comuna` | Comuna de emplazamiento |
| `region` | Región de emplazamiento |
| `geolocalizacion` | Latitud y longitud en un solo campo de texto |
| `estado` | Operativo, en construcción o planificado |
| `capacidad_MW` | Capacidad instalada en megawatts |
| `superficie_m2` | Superficie en metros cuadrados |
| `fuente`, `fuente2`, `fuente3` | Enlaces de verificación |

### Consideraciones sobre los datos

- 18 registros no tienen coordenadas y quedan fuera de los mapas. El listado se genera al final de `analysis.qmd`.
- La capacidad en megawatts está informada en 38 registros y la superficie en 41.
- Un registro venía con coma decimal en sus coordenadas; la corrección se realiza en `preparation.qmd` y no modifica el archivo original.
- Varias instalaciones comparten coordenadas porque corresponden a un mismo campus o dirección. En el mapa de la Región Metropolitana esto se maneja agrupando los puntos según el nivel de zoom.
- La categoría `Planned` del archivo original se traduce a `Planificado` durante la preparación.

## Trabajo pendiente

- Completar las coordenadas de los 18 registros sin georreferenciación.
- Homologar los nombres de comuna y región con la codificación oficial (CUT), lo que permitiría cruzar el catastro con cartografías comunales y con datos territoriales.
- Incorporar la fecha de entrada en operación para analizar la expansión en el tiempo.
- Documentar el criterio de inclusión de instalaciones planificadas y la fecha de corte del catastro.
