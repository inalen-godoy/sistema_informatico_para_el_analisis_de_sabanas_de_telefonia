# Sistema Informático para el Análisis de Sábanas de Telefonía

El análisis de sábanas de telefonía celular constituye un área de relevancia para las investigaciones penales. Este tipo de evidencia digital ha tomado cada vez más importancia debido a que toda persona utiliza redes de telefonía celular para la comunicación.

El análisis de dicha información presenta ciertos desafíos ya que requiere de un conocimiento específico en la temática y de ciertos datos que proporcionan las empresas prestatarias. En este contexto, en el estado del arte no se observan opciones exclusivamente dedicadas a este tipo de pericias. En muchos casos, los analistas deben realizar dichas tareas empleando procesos manuales con mínima asistencia tecnológica. 

En este trabajo se presenta una herramienta open source con el objetivo de facilitar las tareas a los analistas. Entre otras cosas, el sistema permite:
- Cargar sábanas de telefonía en lotes.
- Visualizar los registros de comunicaciones y las áreas de cobertura de las antenas que gestionan dichas comunicaciones, representadas en un mapa satelital.
- Mantener una base de datos de antenas que se retroalimenta con la información de los registros cargados de datos de emplazamiento.
- Herramientas interactivas que facilitan un análisis geoespacial más intuitivo.
- Facilitar un análisis geoespacial más intuitivo mediante herramientas interactivas.

En síntesis, esta herramienta constituye un aporte significativo a la labor de análisis, ofreciendo un soporte tecnológico para analizar evidencia digital en procesos judiciales.

## Contexto académico
Este proyecto comenzó a desarrollarse en el marco de la Práctica Profesional Supervisada realizada en el Departamento de Investigación de Delitos Complejos del Poder Judicial de San Luis, y posteriormente continuó como parte del Proyecto Integrador de la carrera Ingeniería en Informática de la Universidad Nacional de San Luis.

## Autora

- Inalen Godoy.  
- Técnico Universitario en Web.  
- Estudiante de Ingeniería en Informática.  
- Universidad Nacional de San Luis.
- [LinkedIn](https://www.linkedin.com/in/inal%C3%A9n-godoy-79238b13a/)

## Dirección académica

- Directora: Dra. Garis Ana Gabriela.
- Co-Director: Dr. Miranda Enrique Alfredo.

## Tutor institucional

- Ing. David Alejandro Fuentes — DIDC, Poder Judicial de San Luis.
 
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
  - Service: Contiene servicios de aplicación y de QGIS. Los servicios de aplicación contienen la lógica de negocio del sistema y coordinan las operaciones entre los distintos componentes del modelo. Por su parte, los servicios de QGIS encapsulan el acceso a la API de PyQGIS para realizar operaciones geoespaciales, tales como la generación y gestión de los elementos geográficos que representan antenas y emplazamientos en el mapa.
  - Repository: Encapsulan el acceso a datos, aislando la lógica de negocio de la persistencia. Para la lectura y escritura de archivos en formato JSON se utiliza la biblioteca estándar JSON, mientras que la interacción con la base de datos se realiza a través del componente Database, permitiendo almacenar y recuperar la información asociada a las entidades del sistema.
  - Factory: Centralizan la creación de objetos del dominio, y facilita la instanciación de los diferentes tipos de lectores de sábanas de telefonía.
  - Strategies: Implementan algoritmos intercambiables para la lectura de sábanas de telefonía según la empresa y el formato de archivo. Para ello se utilizan las bibliotecas Pandas y Camelot, destinadas a la lectura de archivos Excel y PDF, respectivamente.
  - Entities: Representa a las entidades del dominio que modelan la información gestionada por el sistema.
  - Database: Gestiona la conexión con la base de datos PostGis, en la cual almacena la información geoespacial de antenas y emplazamientos. 
* `/Views`: Provee una interfaz gráfica de usuario (GUI) mediante la cuál el analista puede interactuar con las distintas funcionalidades que provee el sistema. Se implementó mediante PyQt y widgets específicos de PyQGIS, que permiten la construcción de la GUI y la visualización de mapas, capas vectoriales y ráster. 
* `/Controllers`: Es el intermediario entre el modelo y la vista, gestionando eventos generados por el usuario e invocando peticiones al modelo. 
* `/Resources`: Contiene recursos auxiliares utilizados por la aplicación, incluyendo íconos, archivos de interfaz gráfica y archivos JSON con información geográfica utilizada por el sistema.
  
## Documentation
El funcionamiento de los distintos módulos del sistema se encuentra documentado a través de una serie de videos explicativos, en los cuales se presenta de manera detallada el proceso de utilización de la herramienta. Estos materiales forman parte de la documentación del sistema, y se encuentran disponible en:

[Documentation](https://drive.google.com/drive/folders/1XyNMOh3Fewj9Q-2PcdP7JpQ2pkv5i0Qu?usp=sharing)

## Licencia
GNU GPL v3

