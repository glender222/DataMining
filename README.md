# Minería de datos — Detección de lavado de activos (IBM AML)

## Estructura

```
DataMining/
├── datos/                     # NO se sube a git (pesado); se regenera con el notebook
│   ├── 00_fuente/             # CSV sucio del equipo. Solo lectura: nunca se modifica
│   ├── 01_original/           # dataset_original.csv  → ventana de trabajo sin cambios
│   ├── 02_proceso/            # dataset_proceso.csv   → limpieza + transformaciones
│   └── 03_final/              # dataset_final.csv     → listo para modelar
├── notebooks/
│   └── Parcial_Unidad_3_Colab.ipynb   # pipeline de preparación (corre en Colab y en local)
├── informes/                  # entregables para el docente
│   ├── Proyecto_final_mineria_datos.docx
│   └── Presentacion_proyecto_v3.pptx
├── logs/                      # salida de cada ejecución (no se sube a git)
├── materiales/                # material del curso: notebooks de clase, fichas, plantillas
├── archivo/                   # versiones anteriores, solo para consulta
│   └── version_duckdb_simulada/
├── requirements.txt
└── iniciar_jupyter.sh
```

## Flujo de los datos

```
00_fuente ──► 01_original ──► 02_proceso ──► 03_final ──► informes/
 (sucio)      (ventana 1,02M)   (limpio)      (analítico)
```

Reglas que seguimos:

1. **La fuente es inmutable.** Nadie edita `00_fuente`; todo se deriva de ahí con código.
2. **Cada etapa es una carpeta numerada.** El número indica el orden, así se ve qué depende de qué.
3. **Los datos no van a git, el código sí.** Cualquier dataset se reconstruye corriendo el notebook.
4. **Lo viejo va a `archivo/`**, no se mezcla con lo vigente.

## Cómo ejecutar

1. Coloca `LI-Small_Trans_sucio.csv` en `datos/00_fuente/`.
2. Ejecuta el pipeline completo:

```bash
cd notebooks
../.venv/bin/jupyter nbconvert --to notebook --execute --inplace Parcial_Unidad_3_Colab.ipynb > ../logs/ejecucion_parcial_unidad_3.log 2>&1
```

O de forma interactiva con `./iniciar_jupyter.sh` (abre la dirección local que muestre la terminal).

En Colab, el mismo notebook busca el CSV en `MyDrive/MineriaData/` y guarda los resultados en `MyDrive/MineriaData/salida/`.

## Entorno

Python 3.13: `python -m venv .venv && .venv/bin/pip install -r requirements.txt`.
