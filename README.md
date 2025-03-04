# Fiesta del cóctel
## Introducción
En entornos sociales como un cóctel, donde múltiples personas conversan simultáneamente, captar la voz de un hablante específico representa un desafío debido a la superposición de señales sonoras. Este problema es conocido como el "problema de la fiesta de cóctel", un fenómeno que no solo experimentamos los seres humanos al tratar de concentrarnos en una conversación específica, sino que también es un reto en el procesamiento de señales de audio.

Para la implementación del código, se usaron cinco librerías esenciales:

##### •	librosa: Análisis y procesamiento de señales de audio, extracción de características y visualización.
##### •	numpy: Una biblioteca fundamental para la computación matemática, que proporciona soporte para arreglos y matrices.
##### •	soundfile: Lectura y escritura de archivos de audio en diferentes formatos.
##### •	sklearn.decomposition.FastICA: Separación de señales mixtas utilizando Análisis de Componentes Independientes (ICA).
##### •	scipy.fft.fft: Transformación de señales del dominio temporal al de frecuencia usando la Transformada Rápida de Fourier (FFT).

## Análisis
### Configuración del sistema.

Para analizar este fenómeno, en el laboratorio se diseñó un experimento en el que tres micrófonos fueron ubicados en el centro de una sala (configurados con una frecuencia de muestreo de 44 kHz y un nivel de cuantificación de 160 kbps), capturando la mezcla de voces de tres personas situadas a diferentes distancias: 1 metro, 0.9 metros y 0.7 metros respectivamente. Además, los participantes se encontraban mirando en diferentes direcciones, lo que añade variabilidad en la captación de las señales sonoras por parte de los micrófonos.

<p align="center">
  <img src="https://github.com/user-attachments/assets/892fdc21-814d-493f-8ae3-cb2b81568bf8" alt="post_reducido_github" width="400"/>
  
> *Ubicación de personas, micrófonos y distancias, en la fiesta del cóctel.*

### Captura de la señal

Cada una de las participantes, pronunció una frase distinta durante 5 segundos aproximadamente. Los micrófonos captaron la mezcla de estas voces, registrando los datos para su análisis.

#### Frases pronunciadas
###### • Paula: "La carrera no siempre la gana el más rápido, sino el que nunca deja de avanzar."
###### • Alejandra: "El pasado puede doler, pero tú decides si huir o aprender de él."
###### • Valentina: "Ohana significa familia, y la familia no se olvida ni se abandona."

### Procesamiento digital de señales
#### Representación en el dominio del tiempo

Para analizar la captura, se graficaron las señales de cada micrófono en función del tiempo. Estas señales contienen una superposición de las voces de los participantes, lo que dificulta la identificación de cada fuente sonora.

Es por ello que se utiliza el Análisis de Componentes Independientes (ICA) visto como un método de procesamiento de señales que permite separar fuentes sonoras mezcladas, asumiendo que son estadísticamente independientes. En este caso, ICA se utilizó para extraer las voces individuales de cada participante a partir de la mezcla de señales grabadas por los micrófonos.

![z](https://github.com/user-attachments/assets/ee1450ec-3def-4cfd-bf43-a6a812ed9b08)
![zz](https://github.com/user-attachments/assets/f5c79a88-3bcf-4da0-95be-7c49727fc2b9)
![zzz](https://github.com/user-attachments/assets/06c159d5-10c0-4c0a-a64c-82b9c78afdab)
> *Forma de onda de la señal original y con ICA*
> 
> **-	Eje Vertical (Amplitud):** Representa la amplitud de la señal de audio captada por el micrófono. La amplitud está directamente relacionada con la intensidad del sonido, donde valores más altos indican sonidos más fuertes.

> **-	Eje Horizontal (Tiempo):** Muestra el transcurso del tiempo durante la grabación. Este eje permite observar cómo varía la amplitud de la señal a lo largo del tiempo, proporcionando una visión dinámica de la evolución del sonido.

Como se observa en las gráficas anteriores, hay un aumento en la amplitud cuando se utiliza el ICA, este aumento se debe a que al hacer este análisis de separación de fueentes sonoras, no se preserva la escala original de las señales, ya que su objetivo principal es maximizar la independencia estadística entre los componentes separados. Como consecuencia, algunas señales pueden aparecer amplificadas debido a la redistribución de la energía en el proceso de separación.

#### Análisis en el dominio de la frecuencia con la Transformada de Laplace

Para analizar cómo se distribuyen las frecuencias en las señales originales y separadas, se aplicó la Transformada de Laplace, que permite observar la respuesta en el dominio de la frecuencia. Para ello:
 
• Se tomó cada señal en el dominio del tiempo.

• Se aplicó la Transformada de Laplace para obtener la representación en frecuencia.

• Se graficó el espectro de cada señal antes y después de ICA.

![y](https://github.com/user-attachments/assets/97653d09-bb87-45c1-ab82-b9db63079140)
![yy](https://github.com/user-attachments/assets/85c1c30d-cda1-4e35-ba11-0891addce17f)
![yyy](https://github.com/user-attachments/assets/3d873307-ccab-4471-a1e2-5034aa7b93de)
> *Dominio de la Frecuencia de la señal original y con ICA*
> 
> **- Eje Horizontal (Frecuencia):** Representa las frecuencias en hertzios (Hz) presentes en la señal.
> 
> **- Eje Vertical (Magnitud):** Muestra la magnitud de cada componente de frecuencia en la señal.
  
Después de aplicar ICA, se observó un aumento en la magnitud del espectro. Esto ocurre porque el algoritmo enfatiza ciertas frecuencias para mejorar la separación, lo que puede generar un aumento en la energía de la señal en algunas bandas de frecuencia.

#### Evaluación de calidad mediante SNR (Signal-to-Noise Ratio)

El Signal-to-Noise Ratio (SNR) mide la relación entre la potencia de la señal útil y el ruido presente en la grabación. Un SNR más alto indica que la señal deseada ha sido mejor recuperada con menos interferencia. En cuanto a los resultados obtenidos en la relación señal/ruido (SNR) para cada uno de los tres micrófonos, se muestra:

![XX](https://github.com/user-attachments/assets/5fa1e416-7bb5-4b11-9ffc-dc0c7be42e89)
> *SNR de cada micrófono, de la señal original y con ICA*

En todos los casos, el SNR ICA es mayor que el SNR Original, lo que confirma que la técnica ICA mejoró la calidad de las señales separadas, viendo así que las mejoras en el SNR oscilan entre 32.49 dB y 33.73 dB, lo que representa una reducción significativa del ruido e interferencias.

#### Fuente más afectada por ruido:

###### • Paula tenía el SNR más bajo originalmente (136.623 dB), lo que sugiere que su señal estaba más contaminada por ruido o interferencias. Después de la separación, su SNR aumentó a 169.13 dB, mostrando una mejora de 32.507 dB.

#### Fuente con mejor calidad inicial:

###### • Valentina tenía el SNR original más alto (139.537 dB), lo que indica que su voz ya era relativamente más clara antes de la separación. Su mejora tras ICA fue de 32.49 dB, lo que la mantiene dentro del rango de mejora observado en las demás fuentes.

El uso de ICA para la separación de fuentes en el problema de la "fiesta de cóctel" fue altamente efectivo, logrando un incremento significativo en la relación señal-ruido (SNR) en todos los casos. Esto demuestra que la técnica mejora la inteligibilidad de las señales al reducir interferencias y ruido, lo que la hace útil para aplicaciones como reconocimiento de voz, mejora de audio y cancelación de ruido.

## Sección de Preguntas

### ¿Cómo afecta la posición relativa de los micrófonos y las fuentes sonoras en la efectividad de la separación de señales?

La disposición de los micrófonos y las fuentes sonoras juega un papel crucial en la efectividad del proceso de separación de señales.
Si los micrófonos están muy cerca entre sí o mal distribuidos, la información capturada será redundante, lo que puede dificultar la aplicación del Análisis de Componentes Independientes (ICA) y reducir la calidad de la separación.

Una distribución estratégica de los micrófonos (distancias variables, diferentes ángulos de captación y separación suficiente entre ellos) mejora la capacidad del sistema para distinguir las señales individuales. Además, la orientación de las fuentes sonoras (las personas que hablan) también influye: si todas están dirigidas hacia un mismo micrófono, este captará señales muy similares, dificultando su separación.

Es por ello que en nuestro análisis, se observa que al separar los audios, Alejandra es la voz que mejor se escucha al decir su frase, puesto que ella estaba frente al micrófono, a diferencia de Paula y Valentina, que estaban ubicadas mirando a la izquierda y derecha, respectivamente. 

#### ¿Qué mejoras implementaría en la metodología para obtener mejores resultados?

Para optimizar la separación de señales y mejorar la calidad del audio recuperado, se podrían implementar las siguientes mejoras:

 •  Aumentar la cantidad de micrófonos: Utilizar más de tres micrófonos permitiría capturar una mayor diversidad de mezclas de señales, lo que facilitaría la separación de las fuentes de sonido con mayor precisión.
 
 •  Optimizar la distribución de micrófonos: Colocar los micrófonos en posiciones estratégicas, asegurando que cada uno registre una mezcla diferente de las señales, maximizando la independencia entre ellas.
 
 •  Utilizar filtros de reducción de ruido y técnicas de normalización antes de aplicar ICA para mejorar la calidad de la separación.
 
 •  Evaluar diferentes algoritmos de separación: Comparar ICA con otras técnicas como NMF (Non-Negative Matrix Factorization) o Redes Neuronales para determinar cuál ofrece mejores resultados en distintos escenarios.
 
 •  Medir la calidad de la separación: Implementar métricas adicionales como Índice de Distorsión de Señal (SDR) y Índice de Interferencia de Señal (SIR) para evaluar objetivamente el desempeño del algoritmo.

## Instrucciones

**1. Grabación de audios:**

• Se grabaron 3 audios desde el micrófono del celular, siguiendo los parámtros antes mencionados.

• Los audios fueron descargados en formato mp3 y transferidos a Google Colab.

**2. Proceso de análisis:**

• Los audios se descargaron y se llevaron a Colab para su procesamiento.

• Todo el análisis se realizó mediante código, lo que permitió evaluar los datos de manera precisa.

###### Importación de librerías: Carga las librerías necesarias para el procesamiento de audio y análisis.
###### Función calcular_snr: Define una función para calcular la relación señal-ruido (SNR).
###### Cargar archivos de audio: Carga tres archivos de audio en formato .mp3.
###### Corte de señales al mismo tamaño: Recorta las señales al tamaño mínimo entre ellas.
###### Aplicación de ICA: Aplica ICA para separar las señales mixtas en fuentes independientes.
###### Cálculo del ruido: Calcula el ruido como la diferencia entre las señales originales y las separadas.
###### Cálculo del SNR: Calcula el SNR para las señales originales y las separadas por ICA.
###### Guardar audios separados: Guarda las señales separadas por ICA en archivos .mp3.
###### Graficar formas de onda: Muestra las formas de onda antes y después de aplicar ICA.
###### Graficar espectros de frecuencia: Muestra los espectros de frecuencia antes y después de ICA.

***Nota importante: Cada vez que abras el archivo en Google Colab, será necesario cargar nuevamente el archivo de datos. Una vez cargado, podrás acceder al análisis.***


**3. Parámetros clave:**

• Se utilizó la fórmula del SNR (Signal-to-Noise Ratio), que es un parámetro esencial en este análisis, la transformada de Fourier y el Análisis de componentes independientes ICA.

**4. Herramientas y librerías necesarias:**

• Se usó Python y un compilador (en este caso, Google Colab).

## Requisitos

• Tener Python 3.9 instalado y utilizar Google Colab (o cualquier compilador compatible).

• Tener acceso a los audios para cargar en Google Colab o el compilador elegido.

• Contar con las librerías necesarias instaladas para ejecutar el código correctamente (especificadas en el inicio del artículo).

## Usar

Por favor, cite este artículo:

Huertas, V.; Ramírez, P.; Delgado, A. Análisis estadístico de la señal. 6 de febrero de 2025.

## Información de contacto

• est.laurav.huertas@unimilitar.edu.co
• est.deisy.aramirez@unimilitar.edu.co
• est.paulav.gomez@unimilitar.edu.co


