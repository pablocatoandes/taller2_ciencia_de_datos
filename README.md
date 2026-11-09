# Taller 2: predicción de abandono de clientes para FinAlpes

MINE-4101 Ciencia de Datos Aplicada, Universidad de los Andes, semestre 2026-20.

## Integrantes

- Julio Cesar Cardenas Ortiz
- Pablo Andres Casas Tovar 

## Alcance

Prueba de concepto de un modelo que predice qué clientes de un banco van a abandonarlo, para focalizar una campaña de retención. El modelo se entrena con 10.000 clientes de un banco europeo y su valor se evalúa para el caso del enunciado: un banco colombiano con 20.000 clientes, 15% de abandono anual, una oferta que retiene al 30% de quienes iban a irse y que se paga por cada cliente contactado, e ingreso anual por cliente entre COP 500.000 y 900.000.

## Principales hallazgos

- Contactar cada año al 23% de los clientes con mayor riesgo deja un beneficio neto estimado de COP 1.071 millones en el escenario base; ofrecer el beneficio a todos los clientes perdería COP 419 millones.
- La inversión de COP 72 millones se recupera en menos de un mes en el escenario base y en unos 3,6 meses en el pesimista.
- Se recomienda la red neuronal sin variables derivadas, con un umbral de contacto de 25%. Una retención vale casi cinco veces lo que cuesta una oferta mal dirigida, así que conviene detectar más clientes aunque aumenten las falsas alarmas.
- El mayor riesgo del programa es el costo de la oferta: si los clientes retenidos se quedan solo dos años, la campaña pierde dinero con ofertas desde el 40% del ingreso anual. Mientras no se mida la permanencia real, la oferta no debería superar el 30%.
- El número de productos, la edad y la actividad del cliente son las variables que más pesan en el riesgo. El género también aparece y no debe usarse para decidir a quién se ofrece un beneficio.

## Estructura del repositorio

- `Taller_2_Entregable.ipynb`: notebook único con todo el análisis, puntos 1 a 5 del enunciado.
- `churn.csv`: dataset usado.
- `Informe_Ejecutivo.pdf`: punto 6 del enunciado, insights y recomendación para el negocio.
- `README.md`: este documento, que incluye la declaración de uso de IA generativa (punto 7).

## Organización del notebook

1. Entendimiento y preparación de los datos: calidad de datos, recorte de valores fuera de rango, indicadores de abandono por segmento, codificación y variables derivadas.
2. Entrenamiento de modelos: división estratificada 60/20/20, imputación con la mediana de entrenamiento, dos redes neuronales (configuración 1) y un árbol de decisión frente a un ensamble de regresión logística, árbol y KNN (configuración 2), con los hiperparámetros de estos tres elegidos por validación cruzada.
3. Análisis cuantitativo: métricas en prueba con su lectura de negocio, intervalos de confianza por bootstrap, pruebas A/B independientes y pareadas, y McNemar.
4. Análisis cualitativo y explicabilidad: curvas ICE, LIME y SHAP.
5. Generación de valor y caso de negocio: valor esperado con la tasa de abandono del banco, umbral de decisión, resultado esperado, análisis de sensibilidad, limitaciones, conclusiones y un anexo con el caso de la práctica de clase.

## Ejecución

1. Clonar el repositorio y dejar `churn.csv` en la misma carpeta del notebook.
2. Instalar las dependencias (siguiente sección).
3. Abrir `Taller_2_Entregable.ipynb` y ejecutar todas las celdas en orden (Kernel > Restart & Run All).

La ejecución completa toma unos 7 minutos en CPU; el cálculo de SHAP es la parte más lenta, cerca de 3 minutos. El notebook fija semillas, pero las redes neuronales pueden variar en algunos decimales entre equipos por diferencias de TensorFlow y del hardware.

## Dependencias

Probado con Python 3.13. Las instrucciones `pip` también están comentadas en la primera celda del notebook.

```
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn tensorflow keras lime shap jupyter
```

Versiones con las que se verificó la ejecución completa: pandas 3.0.5, numpy 2.5.3, matplotlib 3.11.2, seaborn 0.13.2, scipy 1.18.1, statsmodels 0.15.0, scikit-learn 1.9.1, tensorflow 2.21.0, keras 3.15.1, lime 0.2.0.1 y shap 0.54.1.

## Declaración de uso de IA generativa

Modelos usados: Gemini Flash y Copilot disponibles en VSCode.

Porcentaje de ayuda: 30%.

El notebook base, la estructura del análisis y los métodos parten de las prácticas de clase y del trabajo de los integrantes. La IA se usó para:
- Revisar el pipeline en orden y señalar errores lógicos o malas prácticas en la que los autores hayan incurrido en la base de codigo inicial.
- Proponer correcciones de código, proponer estructura de codigo mas eficientes a la original, como por ejemplo ahorrar lineas para obtener un mismo resultado. 
- Construir con los integrantes el análisis de valor de la sección 5 y buscar fuentes para los supuestos económicos (TRM, tasa de política monetaria, tarifa de SMS y salarios de referencia).
- Redactar y corregir los textos del notebook y del informe ejecutivo, verificando cada cifra contra las salidas del notebook.

Las decisiones de modelado y de negocio fueron de los integrantes, entre ellas mantener el recorte de valores fuera de rango en lugar de convertirlos en nulos, valorar al cliente retenido por su permanencia y no por un año de ingreso, usar tres escenarios (pesimista, valor esperado y optimista), calcula un tiempo esperado de retencion de cliente atraves de distribución geométrica y no agregar cálculos que no estuvieran en el notebook. Los integrantes revisaron y ejecutaron el notebook completo.


