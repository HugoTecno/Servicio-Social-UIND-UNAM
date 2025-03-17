# Paso 1: Cargar datos y verificar
from google.colab import drive
import pandas as pd

# Montar Google Drive
drive.mount('/content/drive', force_remount=True)

# Cargar archivo
file_path = "/content/drive/My Drive/Colab Notebooks/Datos Katona_Control.xlsx"
df = pd.read_excel(file_path)

# Mostrar primeras filas y dimensiones
print(" Primeras filas:")
print(df.head())

print(f"Dimensiones originales: {df.shape}")

# Seleccionar solo las columnas de interés
columnas_interes = [
    "apellido_paterno_paciente", "nombre_paciente", "apellido_materno_paciente", "dat_ter_tipo_terapia","clave_paciente", 
    "edad_corregida", "cont_cef_sem_cons", "hit_mot_gru_sed_sem_cons", 
    "hit_mot_gru_rea_pro_sem_cons", "hit_mot_gru_arra_sem_cons", "hit_mot_gru_gat_sem_cons"
]

df_seleccionado = df[columnas_interes].copy()

# Guardar en un nuevo archivo Excel
output_path = "/content/drive/My Drive/Colab Notebooks/Datos_Normales.xlsx"
df_seleccionado.to_excel(output_path, index=False)

print(f" Archivo guardado en: {output_path}")  

# Diccionario con los nuevos nombres de las columnas
nuevos_nombres = {
    "cont_cef_sem_cons": "Control Cefálico",
    "hit_mot_gru_sed_sem_cons": "Sentado con reacción de protección delantera",
    "hit_mot_gru_rea_pro_sem_cons": "Reacciones de protección laterales y delanteras",
    "hit_mot_gru_arra_sem_cons": "Patrón de arrastre",
    "hit_mot_gru_gat_sem_cons": "Gateo en diferentes niveles"
}

# Renombrar las columnas en el DataFrame
df_seleccionado.rename(columns=nuevos_nombres, inplace=True)

# Mostrar primeras filas para verificar cambios
print("DataFrame con los nuevos nombres de columnas:")
print(df_seleccionado.head())

# Guardar en un nuevo archivo Excel con los nombres corregidos
output_path = "/content/drive/My Drive/Colab Notebooks/Datos_Normales_Renombrados.xlsx"
df_seleccionado.to_excel(output_path, index=False)

print(f"Archivo guardado en: {output_path}")

# Exportar lista de paciente con Nan y en que hitos no han consolidiado
import pandas as pd

# Filtrar solo las filas con al menos un NaN
nan_rows = df[df.isna().any(axis=1)].copy()

# Contar la cantidad de NaN en cada fila
nan_rows["num_nan"] = nan_rows.isna().sum(axis=1)

# Ordenar por clave de paciente y cantidad de NaN (ascendente)
nan_rows_sorted = nan_rows.sort_values(by=["clave_paciente", "num_nan"])

# Eliminar duplicados, quedándonos con el que tenga menos NaN
nan_rows_limpio = nan_rows_sorted.drop_duplicates(subset=["clave_paciente"], keep="first")

# Crear una columna que indique qué categorías tienen NaN
nan_rows_limpio["columnas_con_nan"] = nan_rows_limpio.apply(lambda row: row.index[row.isna()].tolist(), axis=1)

# Seleccionar solo las columnas clave y la información sobre los NaN
df_seleccionado = nan_rows_limpio[["apellido_paterno_paciente", "nombre_paciente", "apellido_materno_paciente","dat_ter_tipo_terapia", "clave_paciente", "columnas_con_nan"]]

# Guardar en un nuevo archivo Excel
output_path = "/content/drive/My Drive/Colab Notebooks/Pacientes_NormalesCon_NaN_SinDuplicados.xlsx"
df_seleccionado.to_excel(output_path, index=False)

print(f" Archivo guardado en: {output_path}")

