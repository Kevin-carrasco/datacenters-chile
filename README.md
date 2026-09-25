# Data centers en Chile

Catastro y georreferenciación de data centers instalados, en construcción y planificados en Chile. El proyecto organiza una base construida a partir de fuentes públicas de la industria y de prensa especializada, y produce un sitio en Quarto con descriptivos y mapas interactivos de la ubicación de las instalaciones.

Informe disponible acá: [https://kevin-carrasco.github.io/datacenters-chile/](https://kevin-carrasco.github.io/datacenters-chile/)

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

