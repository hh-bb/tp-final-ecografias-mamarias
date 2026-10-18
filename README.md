# TP Final Integrador — Clasificación de ecografías mamarias (BUSI)
Grupo 38 · Diplomatura en Ciencia de Datos y Análisis Avanzado · UTN BA

## Qué hace
Clasifica ecografías en Normal / Benigno / Maligno. Criterio rector: **Recall de la clase Maligno ≥ 90 %** (minimizar falsos negativos),
con selección de modelo y umbral en validación y test usado una sola vez.
Modelos: Random Forest + GLCM, CNN desde cero, ResNet50 (Transfer Learning + fine-tuning). Incluye Grad-CAM vs. máscaras manuales.

## Cómo ejecutarlo
1. `pip install -r requirements.txt` (Python 3.10+).
2. Dataset: se descarga solo con `kagglehub` (BUSI, CC0, `aryashah2k/breast-ultrasound-images-dataset`).
   Si ya lo tenés descargado: `export BUSI_PATH=/ruta/a/Dataset_BUSI_with_GT`.
3. Abrir `TP_Final_Grupo38.ipynb` y ejecutar todas las celdas (en CPU tarda decenas de minutos; GPU recomendada, p. ej. Colab).
4. Salidas: carpeta `figuras/` y `resultados.json` (todas las cifras del informe salen de ahí).

Corrida de humo (solo verifica que el código corre, **no** da resultados válidos): `MODO_PRUEBA=1 jupyter nbconvert --to notebook --execute TP_Final_Grupo38.ipynb`.

## Referencia externa
La comparación de negocio usa como referencia de la literatura a Azarpey, N. (2023). *Sensitivity and specificity of ultrasound and mammography for detection of breast malignancy: a systematic review and meta-analysis*. Oncology and Radiotherapy, 17(9), 333–339: sensibilidad combinada de la ecografía 87 % (IC95 80–92 %) y especificidad 75 % (IC95 61–84 %), sobre 28 estudios. Se usa el 80 % (límite inferior del IC95) como piso conservador. Es un promedio de estudios con distintos lectores y equipos, no un radiólogo individual, por lo que la comparación es orientativa. Estos valores están como constantes al inicio del notebook (`SENS_LIT`, `ESPEC_LIT`) y se guardan en `resultados.json` (clave `referencia_literatura`).

## Reproducibilidad
Semilla fija (42) para splits, Random Forest y TensorFlow. Split estratificado 70/15/15 tras eliminar duplicados con pHash.
Los resultados pueden variar levemente entre hardware/versiones de TensorFlow (la GPU no es bit a bit determinista): el informe usa la ejecución cuyo notebook con salidas se incluye en el repositorio (`TP_Final_Grupo38_ejecutado.ipynb`) y su `resultados.json`.

## En Google Colab
Subir el notebook, *Entorno de ejecución → Ejecutar todo*, y descargar `resultados.json` y `figuras/` (ver última celda de descarga). El notebook ejecutado se baja con *Archivo → Descargar → .ipynb*.

## Aviso
Proyecto académico. No es un dispositivo médico ni sustituye el criterio de un radiólogo.
