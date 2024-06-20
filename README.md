# Rag Acredita

Obtención de todos los textos posibles legales e internos del centro
Obtención de textos al respecto en castellano de Internet, extracción de texto de vídeos.
Transformar de pdf a txt
Separar valenciano y castellano
traducir a castellano lo de valenciano
generar títulos para párrafos
generar resúmenes de capítulos más largos
generar preguntas sobre los textos con LLMs
generar preguntas por humanos
contestar preguntas por parte de humanos


## Memoria del proyecto

El proceso de acreditación de competencias es complejo. Por esta razón, es imprescindible consultar a expertos que puedan interpretar adecuadamente los textos legales y los documentos presentados por los candidatos. Además, la integración de los procesos de admisión de alumnos, las leyes educativas y la interpretación de todos los documentos relacionados con el funcionamiento del centro educativo en el mismo sistema de Recuperación de Información Guiada (RAG) resulta de gran interés. El objetivo es desarrollar un chatbot que asista a alumnos y orientadores en la búsqueda de información, proporcionando una interfaz en lenguaje natural capaz de comprender cualquier forma de expresión escrita.

### 1. Objetivos del Proyecto

Crear un sistema RAG que permita:

* Recuperar información relevante sobre el programa "Acredita" y otros aspectos de orientación profesional.
* Consultar reglamentos, procesos de matriculación, leyes educativas, y otros documentos relacionados con el funcionamiento del centro.
* Facilitar el acceso a la información de manera rápida y precisa para usuarios del centro educativo.

### 2. Arquitectura del Sistema

El sistema estará compuesto por los siguientes componentes:

* Extracción y Preprocesamiento de Documentos PDF y otros
* Segmentación y Asignación de Títulos a los Párrafos
* Vectorización y Almacenamiento en una Base de Datos Vectorial
* Interfaz de Consulta

### 3. Extracción y preprocesamiento de documentos PDF y otros.

Se han conseguido todos los documentos que se han considerado relevantes de: https://gestoreducatiu.gva.es/va/ así como la documentación que poseemos sobre Acredita como son las órdenes y leyes y cursos para preparar a los evaluadores. Por otro lado, para tener esa información en otras palabras y resumida, se han buscado textos en foros y blogs que resultan relevantes a primera vista. 

Estos documentos han de ser pasados a texto, separado el texto en valenciano del castellano y traducido al castellano en caso de que sea necesario. En este proceso se limpiarán de caracteres innecesarios y se segmentarán. 

Con los textos legales se pueden seguir varias estrategias:
* Dejarlos como están pero segmentados por párrafos en función de los token o otras características técnicas del proyecto.
* Generar títulos en forma de preguntas que sean respondidas por cada párrafo. Esos títulos contendrán todo el contexto posible como el documento de origen y la sección del documento en la que se encuentran.
* Generar resúmenes de todo el texto con modelos de lenguaje como mt5
* Generar resúmenes de los párrafos con modelos más precisos de atención plena. 

```bash
pdftotext -layout 2014_7890.pdf - | gawk '{print substr($0, 79, 90)}' | sed 's/^ *//g' | sed ':a;N;$!ba;s/-\n//g'

```

#### 3.1 Creación de baterías de preguntas y respuestas.

Consideramos que, además de los textos legales, hay que hacer y responder muchas preguntas por parte de humanos. Esto ayudará a entender mejor los textos y a detectar las principales dudas de los alumnos y evaluadores.
Generaremos preguntas a partir de los textos con modelos de lenguaje comerciales y serán respondidas por humanos expertos. 

#### 3.2 Tokenización y vectorización

### 4. Almacenamiento en la base de datos vectorial

### 5. Consulta del RAG
