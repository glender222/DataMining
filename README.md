# Detección de transacciones asociadas al lavado de activos

Proyecto académico de minería de datos. Incluye comprensión del negocio, análisis de calidad y preparación reproducible de IBM AML-Data, además de la ficha y una presentación preliminar.

## Contenido

- `entrega_parcial/Parcial_Unidad_3_completo.ipynb`: notebook ejecutada. Esta versión pública conserva resultados agregados; se omitieron las salidas con registros individuales.
- `entrega_parcial/GUIA_EXAMEN_ORAL.md`: explicación de las decisiones y resultados.
- `entrega_proyecto_final/`: ficha y presentación preliminar.
- `materiales/`: plantillas, diccionarios, transcripción y notebooks de clase. Las notebooks de clase se incluyen sin sus salidas guardadas.

## Datos y reproducción

Los archivos de datos no están incluidos. Para ejecutar la notebook, consigue `LI-Small_Trans.csv` de [IBM AML-Data](https://github.com/IBM/AML-Data) y coloca una copia sin modificaciones en `entrega_parcial/datos/original.csv`. El archivo empleado por el equipo tiene SHA-256 `f7a9940339c78b5d1476071505b5867c0f5319640b9c4279d13f531bf965319d`.

La notebook crea una entrada con problemas **simulados** y documentados, además de los archivos de proceso y final. El original no se modifica. Para el ejercicio, los parámetros de imputación y del IQR se calcularon sobre todo el conjunto; antes de entrenar un modelo se deben ajustar usando exclusivamente los datos de entrenamiento.

Con Python 3.13:

```bash
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
./iniciar_jupyter.sh
```

Abre la notebook desde la carpeta `entrega_parcial`. Requiere espacio libre para los CSV generados y los archivos temporales de DuckDB. Algunas notebooks de clase contienen rutas específicas de Colab o de otros servidores y requieren adaptación para ejecutarse localmente.
