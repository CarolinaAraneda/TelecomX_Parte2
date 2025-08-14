# TelecomX_Parte2
Identificar factores asociados a la fuga de clientes en Telecom X Con Machine Learning

## Descripción del Proyecto
El objetivo de este proyecto fue desarrollar y evaluar modelos de machine learning para predecir el **abandono de clientes** 
en una empresa de telecomunicaciones, identificando los factores más influyentes y proponiendo estrategias para reducir la fuga.

---

## Pasos Realizados

### Análisis Exploratorio de Datos (EDA)
- Revisión inicial de la estructura del dataset.
- Análisis de distribución de variables y detección de valores faltantes.
- Identificación del desbalance de clases:
  - **No abandono:** 73.46%
  - **Abandono:** 26.54%
- Detección de correlaciones entre variables numéricas y la variable objetivo.

### Limpieza y Preparación de Datos
- Eliminación de columnas irrelevantes para el análisis:
  - **`id_cliente`**: identificador único sin aporte predictivo.
  - **`cuentas_diarias`**: derivada de `cargo_mensual`, por lo que aportaba información redundante.
- Codificación de variables categóricas mediante **OneHotEncoder**.
- Separación de datos en conjuntos de entrenamiento, validación y prueba.
- Escalado de variables numéricas (cuando fue requerido por el modelo).

### Modelos Utilizados
Se probaron tres modelos de clasificación:

1. **DummyClassifier**  
   - Modelo base para medir el rendimiento mínimo esperado.
   - Exactitud: ~73.5%
   - Recall (abandono): 0% (clasifica siempre como “no abandono”).

2. **DecisionTreeClassifier**  
   - Exactitud: 78%
   - Recall (abandono): 39.5%
   - AUC-ROC: 0.66
   - Principales variables: Tenure, método de pago, tipo de contrato, cargo mensual.

3. **RandomForestClassifier** *(modelo optimizado)*  
   - Exactitud: ~78% en pruebas y **80.3%** en validación cruzada.
   - Recall (abandono): 35.3%
   - AUC-ROC: 0.65

### Importancia de Variables (RandomForest Optimizado)
| Ranking | Variable | Importancia (%) |
|---------|----------|-----------------|
| 1 | Tipo de contrato – Mensual | **29.08** |
| 2 | Meses de contrato (Tenure) | **15.95** |
| 3 | Tipo de internet – Fibra óptica | **11.29** |
| 4 | Cargo total acumulado | **9.60** |
| 5 | Método de pago – Cheque electrónico | **7.35** |
| 6 | Tipo de contrato – Anual (2 años) | **7.35** |
| 7 | Cargo mensual | **4.49** |
| 8 | Tipo de internet – No | 3.41 |
| 9 | Tipo de contrato – Anual (1 año) | 2.17 |
| 10 | Factura online | 1.69 |
| ... | Resto de variables | <1.7 cada una |

---

## 3. Conclusiones Clave
- **Tipo de contrato** y **tenure** son los factores más determinantes.
- Clientes con **fibra óptica** presentan mayor riesgo de fuga que otras tecnologías.
- Montos altos de facturación (mensual o acumulada) aumentan la probabilidad de abandono.
- El **método de pago** influye: pagos manuales (ej. cheque electrónico) tienen mayor asociación con la cancelación.

---

## Recomendaciones Estratégicas
1. Incentivar contratos anuales mediante beneficios y descuentos.
2. Implementar un programa de retención en los primeros 3 meses.
3. Mejorar la experiencia de clientes con fibra óptica.
4. Ofrecer ajustes de plan a clientes con cargos altos.
5. Fomentar métodos de pago automáticos.

---

## Tecnologías Utilizadas
- Python 3.x
- Pandas, NumPy
- Scikit-learn
- Matplotlib
