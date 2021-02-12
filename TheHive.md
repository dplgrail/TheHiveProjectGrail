## Wazuh

Es una solución de monitoreo de seguridad de código abierto que recopila y analiza datos de seguridad del host. Es una bifurcación del proyecto OSSEC más antiguo y más conocido.
El componente del servidor Wazuh se integra estrechamente con Elasticsearch y Kibana, mientras que el agente es capaz de realizar muchas tareas relacionadas con la seguridad, como el análisis de registros, la detección de rootkits, la detección de puertos de escucha y la supervisión de la integridad de los archivos. Para este proyecto, utilizaremos estas capacidades para generar alertas.

## Elasticsearch

Elasticsearch actuará como nuestro repositorio de registros. Es increíblemente potente y versátil, y cuando se combina con Logstash para la ingestión de registros y Kibana para la visualización, proporciona una plataforma sólida para todo tipo de datos.

## ElastAlert

ElastAlert es un proyecto de código abierto iniciado por los ingenieros de Yelp para proporcionar un mecanismo de alerta para Elasticsearch. Es un proyecto independiente que no necesita ejecutarse en el mismo servidor. Simplemente consulta Elasticsearch a través de la API REST y tiene numerosos resultados para alertar sobre una coincidencia. Una de esas salidas alimentará la información a TheHive. Así es como distinguimos el ruido de los eventos importantes en los registros y generamos alertas.

## TheHive

TheHive se describe a sí misma como “una plataforma de respuesta a incidentes de seguridad gratuita, escalable y de código abierto, diseñada para facilitar la vida de cualquier profesional de seguridad de la información que se ocupe de incidentes de seguridad que deben investigarse y actuar rápidamente”.
En esencia, es una plataforma de gestión de alertas para gestionar una alerta de incidente desde la creación hasta el cierre.

## Corteza

Cortex es otro producto de software del mismo equipo que TheHive y complementa ese producto con el enriquecimiento de datos. Cortex permite el uso de "analizadores" (113 al momento de escribir este artículo) para obtener información adicional sobre los indicadores que ya están presentes en sus registros. Permite la consulta de servicios de terceros sobre indicadores como IP, URL y hash de archivo, y etiquetará la alerta con esta información adicional. No es necesario enviar un hash de archivo manualmente a VirusTotal cuando un analizador lo hará automáticamente por usted y etiquetará la alerta con los resultados.

## MISP

MISP es una plataforma de intercambio de amenazas de código abierto mantenida por CIRCL que, entre muchos otros usos, permite al operador suscribirse a fuentes de inteligencia de amenazas. Estos feeds pueden ser suscripciones pagas o feeds mantenidos por la comunidad de varias organizaciones, y son nuestra principal fuente de enriquecimiento de datos.