1. Que es un LLM?
Es un paquete de software que consta de dos archivos que se ejecutan de forma autónoma:
El archivo de parámetros
El archivo de ejecución
Su función principal es predecir la siguiente palabra en un secuencia de texto. Para logra lo anterior el modelo debe aprender sobre todo ( el mundo, la historia, la lógica y el lenguaje) comprimiendo toda esa información  en sus parámetros.

2. Por que alucina?
Esto pasa principalmente por varias razones:
Un LLM no es una base de datos de hechos, sino un proceso de predicción de la siguiente palabra que funciona mediante una compresión con perdida de internet. En palabras mas sencillas, es tanta la información de tipo texto que se guardan en un archivo de parámetros mucho mas pequeño, que se hace difícil tener una copia exacta. Esto se conoce en ingles como (Lossy Compression).
Naturaleza de sueño o imitación: El modelo esta diseñado para imitar la distribución de documentos con los que fue entrenado, esto se puede traducir en soñar con documentos de internet de acuerdo a lo que le parece mas " razonable " de acuerdo a sus probabilidades estadísticas.
Prioridad en el patrón sobre el dato: Debido a que su función es predecir la siguiente palabra, si el modelo necesita completar un dato especifico, generará algo que tenga la forma correcta y los dígitos esperados, aunque el numero sea totalmente inventado, porque se ve "bien" en ese contexto.
Conocimiento imperfecto e inescrutable: El conocimiento en un LLM no está almacenado de formal lógica como en un software tradicional.

3. Que es el contexto y por que es limitado?
El contexto se define como la memoria de trabajo del modelo, siendo el equivalente a la memoria RAM en un sistema operativo tradicional. Pero el contexto lo podemos dividir en 3 conceptos:
Memoria de trabajo inmediata: Es donde el LLM mantiene la información activa para poder procesar una tarea y predecir la siguiente palabra en una secuencia.
Espacio de lectura: Es todo lo que el modelo lee en el momento debe estar dentro de esta ventana para que el modelo pueda utilizarlo.
Función de paginación: Actua coordinando esta memoria, moviendo información relevante hacia adentro o hacia afuera de la ventana de contexto para resolver problemas específicos
y es limitado por 3 razones principales:
Es un recurso finito, ya que la ventana de contexto tiene un limite de máximo de palabras que puede procesar a la vez. Es lo que conocemos como TOKENS
Su capacidad de predicción se basa en la palabra que genera basándose en la información que cabe dentro de ese limite. Esto puede asociarse a cuando una computadora se queda sin memoria RAM y su costo computacional

4. Pre-training ( Que es) : fase inicial, es donde el LLM descarga y procesa una cantidad masiva de TEXTO de internet ( 10TB O 15 billones de tokens) para que la red neuronal aprenda a predecir la siguiente palabra, la data, por lo general, viene principalmente de rastreos web como Common Crawl, Wikipedia, etc ( La idea es obtener información de alta fidelidad y calidad), aquí es donde empezamos a notar el famosos Compresion con perdida (Lossy compression).

5. Modelo base/instruido:
El base resulta ser un simulador de documentos de internet, si se hace una pregunta puede responder con otra o pensar/soñar con un texto similar a la web porque no sabe ser un asistente.
El instruido ( o asistente) resulta de entrenar el modelo con datos específicos de preguntas y respuestas humanas, esto hace que se vuelva útil, amable y veraz y siga instrucciones especificas

6. Supervised Fine tunning ( SFT): Es el proceso por el cual se toma la modelo  base, se entrena con un conjunto de datos muchoa mas pequeño ( 100k ejemplos) pero de muy alta calidad. Estas preguntas y respuestas ya se basan en el concepto humano Pregunta/respuesta. Ya hay mayor limpieza de los datos y el llm empieza a aprender por imitación.
Que es RLHF: Significa Aprendizaje por Refuerzo a partir de Retroalimentación Humana. Existe porque en dominios subjetivos o creativos (como escribir poemas o chistes) es difícil escribir una respuesta "perfecta" para el entrenamiento supervisado, pero es muy fácil para un humano comparar y ordenar varias respuestas generadas por el modelo. Se entrena un "modelo de recompensa" que imita estas preferencias humanas para guiar al LLM hacia respuestas que los humanos prefieren.

8. LLM Autoregresivo: Esto significa que genera texto palabra por palabra ( Token por token) de manera secuencial, donde cada nueva palabra se añade al final ed la secuencia y se vuelve a introducir en el modelo como parte del contexto para predecir la siguiente.

9. Temperatura & Como afecta la salida? Es el factor que controa la aleatoriedad en el muestreo na temperatura baja hace que el modelo elija siempre la palabra más probable (siendo más determinista y predecible), mientras que una temperatura alta hace que el "lanzamiento de moneda" sea más sesgado hacia palabras menos probables, resultando en una salida más creativa o diversa, pero con mayor riesgo de errores.
Analogia : Lanzamiento de una moneda:
Cuando un LLM tiene que elegir la siguiente palabra para continuar un texto, no tiene una única opción fija. En su lugar, calcula una lista de palabras posibles y sus probabilidades, y luego realiza un sorteo; es decir, lanza una moneda cargada donde las palabras con más sentido tienen una probabilidad mucho más alta de salir ganadoras. La temperatura es simplemente el control que decide qué tan cargada está esa moneda:
Temperatura Fría (Baja): La moneda está extremadamente cargada hacia la palabra más obvia, segura y lógica.
¿Qué pasa? El modelo casi nunca se arriesga; siempre elegirá la palabra más predecible. Esto es ideal para tareas que requieren respuestas exactas e inequívocas (como matemáticas o código de programación). Sin embargo, el texto puede volverse monótono o repetitivo.
Temperatura Caliente (Alta): La moneda se vuelve más equilibrada, aplanando las diferencias.
¿Qué pasa? Las palabras menos comunes o más inusuales ahora tienen una oportunidad real de salir elegidas en el sorteo. Esto hace que el texto sea mucho más creativo, variado y sorprendente, pero aumenta considerablemente el riesgo de que el modelo pierda el sentido de la coherencia o empiece a inventar datos (alucinar). En pocas palabras, la temperatura controla el nivel de audacia, creatividad y aleatoriedad del modelo al momento de elegir cada palabra

10. ¿Qué es un token y por qué no es una palabra? Los tokens son las unidades o "átomos" de texto que el modelo procesa. No son palabras exactas porque se utiliza un algoritmo llamado Byte Pair Encoding (BPE) para dividir el texto de manera eficiente: palabras comunes pueden ser un solo token, pero palabras raras o complejas se dividen en varios (por ejemplo, "ubiquitous" son 3 tokens).Esto permite manejar un vocabulario finito (como 100,000 tokens en GPT-4) y representar cualquier cadena de texto

11. ¿Qué NO puede hacer un LLM por diseño?
No tiene identidad persistente ni memoria a largo plazo: Es una función matemática sin estado (stateless) que se reinicia en cada interacción; no "aprende" de tu conversación después de que esta termina. No puede realizar computación arbitraria en un solo paso: Tiene una cantidad fija de cómputo por token (limitada por sus capas); si le pides resolver un problema matemático complejo en una sola palabra, fallará porque necesita generar tokens intermedios ("pensar") para distribuir el esfuerzo computacional. No tiene acceso innato a la verdad: Solo predice patrones estadísticos y no puede verificar hechos a menos que se le conecte a herramientas externas como un navegador

