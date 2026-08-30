# Sistema Informático para el Análisis de Sábanas de Telefonía

El análisis de sábanas de telefonía celular constituye un área de relevancia para las investigaciones penales. Este tipo de evidencia digital ha tomado cada vez más importancia debido a que toda persona utiliza redes de telefonía celular para la comunicación.

El análisis de dicha información presenta ciertos desafíos, ya que requiere conocimientos específicos sobre telecomunicaciones, geolocalización y evidencia digital, además del acceso a datos técnicos proporcionados por las empresas prestatarias. Si bien existen herramientas orientadas al análisis de telecomunicaciones y a la representación geoespacial de estos registros, muchas de ellas presentan limitaciones vinculadas a su alto costo de licenciamiento, restricciones de acceso institucional, dependencia de software propietario o falta de adaptación a las necesidades particulares del ámbito judicial local. En consecuencia, en numerosos casos los analistas continúan realizando estas tareas mediante procesos manuales o con mínima asistencia tecnológica.

En este trabajo se presenta una herramienta open source con el objetivo de facilitar las tareas a los analistas. Entre otras cosas, el sistema permite:
- Cargar sábanas de telefonía en lotes.
- Visualizar los registros de comunicaciones y las áreas de cobertura de las antenas que gestionan dichas comunicaciones representadas en un mapa satelital.
- Mantener una base de datos (BD) de antenas que se retroalimenta con la información de los registros cargados de datos de emplazamientos de antenas.
- Facilitar un análisis geoespacial más intuitivo mediante distintas herramientas interactivas.

Asimismo, la herramienta fue validada mediante una encuesta aplicada a 13 analistas especializados, quienes, a partir de una demostración, consideraron que la solución propuesta responde adecuadamente a las necesidades del entorno judicial. 

En síntesis, esta herramienta constituye un aporte significativo a la labor de análisis, ofreciendo un soporte tecnológico para analizar evidencia digital en procesos judiciales.

## 🧩 Funcionalidades y documentación
- **Módulo de Gestión de antenas:** Este módulo concentra operaciones vinculadas a la administración de emplazamientos de antenas.
    - Gestionar antenas:
        - Registro de antenas de forma manual o en lotes.
        - Visualización cartográfica.
        - Modificación o eliminación de antenas.
        - Búsquedas avanzadas mediante atributos o restringido a un área geográfica.
        - Gestión de duplicados con información conflictiva.
- **Módulo de Análisis de sábanas:** Este módulo proporciona funcionalidades destinadas al análisis de registros de comunicaciones.
    - Gestionar casos: Posibilita crear un nuevo caso, modificarlo, o consultar uno ya existente.
    - Cargar sábana: Registra sábanas de telefonía de forma manual o en lotes, según sea el caso puede realizar alguna de las siguientes tareas:
        - Registrar las antenas faltantes: Realiza el alta de aquellas antenas que se encuentran especificadas en la sábana cargada y no se encuentran registradas en la BD.
        - Completar datos de las ya existentes: Actualiza información faltante de antenas ya registradas en la BD cuando dichos datos se encuentran especificados en la sábana cargada.
        - Registrar duplicados: Identifica duplicados de emplazamientos de antenas con información conflictiva, evitando la sobreescritura de los datos existentes en la BD y almacenando la información para su posterior gestión.
        - Registrar la sábana y añadir sus eventos.
    - Mostrar en mapa eventos registrados: Resalta el evento y visualiza la antena asociada.
    - Mostrar en mapa antenas y emplazamientos: Proporciona herramientas para navegación en el mapa e identificación de antenas.
    - Agregar acotaciones a eventos: Facilita añadir notas a eventos o separadores dentro de una misma sábana.
    - Marcar en mapa elementos de interés para la investigación: Marca puntos o delimita zonas mediante puntos o figuras geométricas respectivamente.
    - Análisis de llamadas: Permite identificar eventos de llamada y muestra en el mapa la zona de cobertura de la antena a la que se conectó el emisor y el receptor de una llamada.
    - Medir en mapa distancia entre puntos y áreas de interés: Mide distancia entre puntos, y el área de un polígono en el mapa.
    - Mostrar mapa de intensidad de eventos: Visualiza gráficamente la concentración del tráfico de llamadas y datos.
    - Filtrar eventos de interés: Aplica distintos tipos de filtrado a los eventos de las sábanas.


El funcionamiento de los distintos módulos del sistema se encuentra documentado a través de una serie de videos explicativos, en los cuales se presenta de manera detallada el proceso de utilización de la herramienta. Estos materiales forman parte de la documentación del sistema, y se encuentran disponibles en:

[Documentation](https://drive.google.com/drive/folders/1XyNMOh3Fewj9Q-2PcdP7JpQ2pkv5i0Qu?usp=sharing)


## 🖼️ Vistas de la aplicación
- Módulo de análisis de sábanas de telefonía.
<img width="1917" height="1027" alt="Captura de pantalla 2026-05-18 011635" src="https://github.com/user-attachments/assets/12b4f6f9-00ba-4831-a339-da51ad52b7f5" />
<img width="1920" height="1027" alt="Captura de pantalla 2026-05-18 015303" src="https://github.com/user-attachments/assets/ac3cd016-8a7c-4d57-a72f-58bf7fd2aa2a" />

- Módulo de gestión de antenas.
<img width="1920" height="1027" alt="Captura de pantalla 2026-05-15 181826" src="https://github.com/user-attachments/assets/92bf1abe-7495-48e6-a026-3a34df798d75" />

## 🛠️ Tecnologías utilizadas
* **Frontend:** PyQt, Qt Designer.
* **Backend:** PyQGIS, Camelot, Pandas.
* **Gestor de Base de Datos:** PostgreSQL/PostGIS.

## ⚙️ Aspectos Técnicos
* **Arquitectura:** Modelo-Vista-Controlador.
* **Patrones de diseño:**  Singleton, Strategy, Simple Factory y Repository.
  
## 📂 Estructura del Proyecto
Cada componente del patrón MVC se estructuró de la siguiente manera:
* `/Models`: Gestionó la representación de la información y la lógica de negocio. Se organiza en los siguientes subcomponentes, cada uno con una funcionalidad específica:
  * `/Service`: Contiene servicios de aplicación y de QGIS. Los servicios de aplicación contienen la lógica de negocio del sistema y coordinan las operaciones entre los distintos componentes del modelo. Por su parte, los servicios de QGIS encapsulan el acceso a la API de PyQGIS para realizar operaciones geoespaciales, tales como la generación y gestión de los elementos geográficos que representan antenas y emplazamientos en el mapa.
  * `/Repository`: Encapsulan el acceso a datos, aislando la lógica de negocio de la persistencia. Para la lectura y escritura de archivos en formato JSON se utiliza la biblioteca estándar JSON, mientras que la interacción con la base de datos se realiza a través del componente Database, permitiendo almacenar y recuperar la información asociada a las entidades del sistema.
  * `/Factory`: Centralizan la creación de objetos del dominio, y facilita la instanciación de los diferentes tipos de lectores de sábanas de telefonía.
  * `/Strategies`: Implementan algoritmos intercambiables para la lectura de sábanas de telefonía según la empresa y el formato de archivo. Para ello se utilizan las bibliotecas Pandas y Camelot, destinadas a la lectura de archivos de planilla de cálculo y PDF, respectivamente.
  * `/Entities`: Representa a las entidades del dominio que modelan la información gestionada por el sistema.
  * `/Database`: Gestiona la conexión con la base de datos PostGIS, en la cual almacena la información geoespacial de antenas y emplazamientos. 
* `/Views`: Provee una interfaz gráfica de usuario (GUI) mediante la cual el analista puede interactuar con las distintas funcionalidades que provee el sistema. Se implementó mediante PyQt y widgets específicos de PyQGIS, que permiten la construcción de la GUI y la visualización de mapas, capas vectoriales y ráster. 
* `/Controllers`: Es el intermediario entre el modelo y la vista, gestionando eventos generados por el usuario e invocando peticiones al modelo. 
* `/Resources`: Contiene recursos auxiliares utilizados por la aplicación, incluyendo iconos, archivos de interfaz gráfica y archivos JSON con información geográfica utilizada por el sistema.

## 🎓 Contexto académico 
Este proyecto comenzó a desarrollarse en el marco de la Práctica Profesional Supervisada realizada en el Departamento de Investigación de Delitos Complejos (DIDC) del Poder Judicial de San Luis, y posteriormente continuó como parte del Proyecto Integrador de la carrera Ingeniería en Informática de la Facultad de Ciencias Físico Matemáticas y Naturales de la Universidad Nacional de San Luis (UNSL).

<img height="30" alt="ggg" src="https://github.com/user-attachments/assets/ce3c887c-5956-4029-b44f-41e255550901" />

## Autora
- Inalen Godoy.  
- Técnico Universitario en Web.  
- Ingeniera en Informática.
- UNSL.
- [LinkedIn](https://www.linkedin.com/in/inalen-godoy-79238b13a/)

## Dirección académica

- Directora: Dra. Garis Ana Gabriela - UNSL - [LinkedIn](https://www.linkedin.com/in/ana-gabriela-garis/)
- Co-Director: Dr. Miranda Enrique Alfredo - UNSL - [LinkedIn](https://www.linkedin.com/in/eamiranda-ok/)

## Tutor institucional

- Ing. David Alejandro Fuentes - DIDC, Poder Judicial de San Luis.

## Publicaciones
Se participó del 13° Congreso Nacional de Ingeniería Informática y Sistemas de Información, CoNaIISI 2025, organizado por la Red RIISIC y la Universidad Tecnológica Nacional. En dicho evento se presentó el trabajo titulado "Sistema Informático para el Peritaje de Comunicaciones Móviles", en la categoría Trabajo de I+D+i de Estudiantes extra-cátedra. La propuesta fue aceptada para su exposición oral, y posteriormente fue seleccionada entre los 3 mejores trabajos del simposio.

## Licencia
GNU GPL v3

