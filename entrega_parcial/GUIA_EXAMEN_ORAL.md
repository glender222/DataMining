# Guía para el examen oral

## ¿Qué problema aborda el equipo?
Apoyar a analistas AML para priorizar la revisión de operaciones potencialmente asociadas al lavado. El conjunto es sintético y una etiqueta positiva no constituye una prueba legal.

## ¿Qué contiene el archivo original?
LI-Small tiene 6.924.049 transacciones, 11 columnas y fechas del 1 al 17 de septiembre de 2022. Tiene 3.565 etiquetas positivas (aproximadamente 0,0515 %), cero nulos y 8 duplicados exactos. El original se mantiene sin modificar.

## ¿Por qué aparece una entrada simulada?
Para demostrar la limpieza se agregó deliberadamente ruido a una copia: 2 nulos, un formato con espacios, un monto negativo, un monto extremo y una fila duplicada. Son problemas creados para el ejercicio, no hallazgos de la fuente original. La copia tiene 6.924.050 filas y una columna de control.

## ¿Cómo se trataron los nulos?
El monto nulo se imputó con la mediana de pagos en USD (886,36) y el formato de pago nulo con la moda (Cheque). La copia simulada pasó de 2 nulos a 0 en proceso.

## ¿Qué ocurrió con los duplicados?
La copia simulada pasó de 9 a 8 duplicados exactos al retirar únicamente la fila añadida deliberadamente. Los 8 duplicados preexistentes se conservaron porque no existe un identificador único de transacción que permita confirmar que son errores.

## ¿Cómo se corrigieron las inconsistencias y valores inválidos?
Se quitaron espacios externos del formato de pago y el monto negativo simulado se reemplazó por la mediana de USD. Ambos conteos pasaron de 1 a 0. En datos reales, habría que comprobar si los montos negativos representan reversos antes de imponer esa regla.

## ¿Qué se hizo con el extremo simulado?
Se reemplazó el valor extremo introducido por el límite superior IQR para pagos en USD: 12.770,895. Se conservaron los demás valores atípicos, pues un monto extremo no prueba que sea incorrecto. En el original el IQR identificó 428.762 candidatos atípicos en USD.

## ¿Qué variables se crearon y cuáles se excluyeron?
Se obtuvieron hora y día de semana de Timestamp, se codificó el formato de pago en siete indicadores y se definieron tramos de monto en la moneda original. Se excluyeron identificadores de bancos y cuentas, así como campos de recepción por cautela temporal. La etiqueta es el objetivo, no un predictor.

## ¿Por qué el final tiene más duplicados?
El final contiene 284.698 coincidencias sobre sus 13 columnas. Como se excluyeron identificadores, operaciones distintas pueden tener iguales las variables restantes. No se eliminaron transacciones originales: se conserva el número de filas original.

## ¿Cómo se verificó el pipeline?
Se reconstruyó la entrada simulada desde el original y se aplicó otra vez el pipeline. La comparación exacta con el proceso seleccionado produjo cero diferencias. El original conserva su hash SHA-256.

## ¿Qué falta antes del modelado?
La mediana, moda e IQR se calcularon sobre todo el original solo para mostrar el ejercicio. Para modelar, se debe separar temporalmente y aprender estos parámetros únicamente con el entrenamiento para evitar fuga. Además, se requiere evaluar con precision, recall y PR-AUC y validar con datos reales antes de un uso operativo.
