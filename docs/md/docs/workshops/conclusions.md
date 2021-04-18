# CONCLUSIONES Y TRABAJO FUTURO

## Luma 
El método de escala de grises hecho con LUMA, nos muestra una forma más efectiva para hallar otros tipos de grises para cuando una imagen se encuentra ultra saturada o con mucho brillo, ya que este le da un peso específico a cada uno de los valores del espectro RGB. Para trabajos futuros sería bastante interesante encontrar que valores según la cantidad de brillo se debe aplicar en la fórmula. 

## negativos

## Máscaras de convolución
La aplicación de filtros en las imágenes, en especial las máscaras de convolución consiste en modificar las matrices de la imagen digitalizada. A parte de poner un filtro a la imagen, también se puede hacer un análisis del procesamiento de la imagen mediante el filtro. Como trabajo futuro está la coincidencia de patrones, ubicando el objeto y luego haciendo mediciones sobre él en la imágen,permitiendo hacer un reconocimiento de objetos para identificar al deseado.

## ASCII 
El concepto del ASCII arte nace como una forma de representar imágenes o figuras como una composición de caracteres definidos bajo los 95 caracteres imprimibles (de un total de 128) del estándar ASCII de 1963. Para lograr este objetivo en el taller presente se transformó a imagen original a blanco y negro utilizando el método de promedio RGB, (Aunque es posible utilizar de otros como luma) ya que una vez teniendo la imagen convertida el valor de RGB para cada sección definida de la imagen corresponde a la intensidad lumínica en dicha sección por lo que se pueden imprimir caracteres del tamaño de la región leída donde por intuición estos tengan una mayor o menor área (la cual mientras sea mayor simula una luminosidad menor) por ejemplo se interpreta que el carácter “@” es mas oscuro o con mayor superficie que “-“ por lo que fueron usados para diferentes niveles de iluminación.
Aunque satisfactorios los resultados del taller se pueden mejorar mediante la experimentación sobre los factores de fuente de letra, tamaño de letra, separación de caracteres y selección de caracteres según se vea conveniente.


## MOSAICO
El mosaico o fotomosaico consiste en que, dada una imagen principal, esta se pueda recomponer a partir de un conjunto de imágenes pequeñas que reemplacen secciones rectangulares de la imagen original, dando la impresión de un mosaico tradicional pero donde la imagen original aún es visible o entendible. Para nuestro taller utilizamos una base de datos local de imágenes organizadas según su valor RGB e intensidad lumínica, con las cuales sustituimos cuadrantes específicos de la imagen original cuyo valor RGB e iluminación correspondiera lo más preciso posible (realizando este proceso por cada cuadrante hasta completar la imagen), el resultado fueron interpretaciones fidedignas para el caso de imágenes con tonalidades puras de rojo, verde, amarillo, azul y grises, pero la calidad se reducía a medida que existían todos más intermedios.
Tomando en cuenta estos resultados una posible mejora a futuro es la implementación de una base de datos con un mayor número de imágenes para aumentar la precisión de color al momento de realizar las sustituciones, además de la implementación de conceptos de transparencia para que (como se puede observar en las imágenes más famosas de este tipo en internet) sea posible apreciar con mayor facilidad la imagen original en el fondo del mosaico.


## Conclusión General

> :ToCPrevNext