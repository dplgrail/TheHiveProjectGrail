[TOC]



# Elastic Stack

## 1. Introducción de Elastic Stack

Elastic Stack es un motor de busqueda que se compone de un conjunto de herramientas que está centrada en la monitorización, analitica de logs, explotación de la información, etc.

Lo que compone Elastic Stack es de 4 componentes:

1. **Beats**: Se encarga de recolectar información, de cualquier tipo (logs, sistemas, redes, base de datos, etc.)
2. **Logstash**: Se encarga de tratar esa información. También puede recolectar información pero lo complementamos con Beats para no sobrecargar Logstash. Lo que hará Logstash es tratar de procesar, transformar, eliminar, etc. para dejarlo a nuestro gusto.
3. **Elasticsearch**: Es el corazón de Elastic Stack. Se encarga de almacenar toda la información que Beats y Logstash han recolectado de otras fuentes y la indexa de alguna manera como si fuera una base de datos.
4. **Kibana**: Es la interfaz gráfica de Elasticsearch, es decir, nos mostrará toda la información procesada que Elasticsearch ha procesado de una manera global para que nos sea más fácil localizar la información.

![img](https://lh6.googleusercontent.com/MIZacqSDzUW_afEUxC_uGBJgI3bVODO8UoAnH17Yy7QWvZoIj5fO7JUkR6_yMQ4fbHQcXRhpkXbI7IBR4lzecBr08i1LKdIdSCDDp9-_1bIyJJ8mid-aP5uPNxxbh0fnP5YiHvXD)

## 2. Instalación de Elastic Stack

### 2.1. Instalación de Beats

#### 2.1.1. Instalación en Linux

1. Podemos hacerlo de dos maneras:
   1.1. Ir a la pagina principal de Elastic Stack, apartado de Beats y descargarnos el que necesitemos con extensión .tar.gz (Linux 32-BIT/Linux 64-BIT): *https://www.elastic.co/es/downloads/beats*

   1.2. Con la comanda **wget** descargarnos el fichero copiando la ruta del fichero con botón derecho sobre el que nos queramos descargar, en este caso Filebeat, y nos quedaría así:

   `$ wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.10.2-linux-x86_64.tar.gz`

2. Descomprimimos el fichero.tar.gz con la comanda **tar**:

   `$ tar -xzvf filebeat-7.10.2-linux-x86_64.tar.gz `

   Donde las opciones `-x`, es indicarle que extraiga, `z` es para que filtre a traves de gzip, `v ` es para que muestre lo que esta extraiendo en tiempo real y `f` decirle que es un fichero.

3. Nos quedaria de esta manera:

4. Para arrancarlo, ejecutamos la siguiente comanda en la terminal dentro del directorio descomprimido:

   `$ ./filebeat -c filebeat.yml`

   Con la opción `-c` le decimos que pase el fichero de configuración .yml .

#### 2.1.2. Instalación en Windows

1. Vamos a la pagina principal de Elastic Stack, apartado de Beats y descargarnos el que necesitemos con extension .zip (Windows Zip 32-BIT/Windows Zip 64-BIT): *https://www.elastic.co/es/downloads/beats*

2. Extraemos toda el contenido clicando botón derecho sobre el .zip y damos a "Extraer Todo"

3. Para arrancarlo, ejecutamos la siguiente comanda en la terminal dentro del directorio descomprimido:

   `C:\> .\filebeat.exe -c filebeat.yml`

### 2.2. Instalación de Logstash

#### 2.2.1. Instalación en Linux

1. Podemos hacerlo de dos maneras:

   1.1. Ir a la pagina principal de Elastic Stack, apartado de Logstash y descargarnos el que necesitemos con extension .tar.gz (Linux X86_64): *https://www.elastic.co/es/downloads/logstash*

   1.2. Con la comanda **wget** descargarnos el fichero copiando la ruta del fichero con botón derecho sobre el que nos querramos descargar y nos quedaria asi:

   `$ wget https://artifacts.elastic.co/downloads/logstash/logstash-7.10.2-linux-x86_64.tar.gz`

2. Descomprimimos el fichero.tar.gz con la comanda **tar**:

   `$ tar -xzvf logstash-7.10.2-linux-x86_64.tar.gz `

3. Para arrancarlo, ejecutamos la siguiente comanda en la terminal dentro del directorio descomprimido:

   `$ bin/logstash -f config/logstash-sample.conf`

   Con la opción `-f` le decimos que pase el fichero de configuración .conf .

#### 2.2.2. Instalación en Windows

1. Vamos a la pagina principal de Elastic Stack, apartado de Logstash y descargarnos el que necesitemos con extension .zip (Windows): *https://www.elastic.co/es/downloads/logstash*

2. Extraemos toda el contenido clicando botón derecho sobre el .zip y damos a "Extraer Todo"

3. Para arrancarlo, ejecutamos la siguiente comanda en la terminal dentro del directorio descomprimido:

   `C:\> .\bin\logstash.bat -f .\config\logstash-sample.conf `

   Con la opción `-f` le decimos que pase el fichero de configuración .conf .

### 2.3. Instalación de Elasticsearch

#### 2.3.1. Instalación en Linux

1. Podemos hacerlo de dos maneras:

   1.1. Ir a la pagina principal de Elastic Stack, apartado de Elasticsearch y descargarnos el que necesitemos con extension .tar.gz (Linux X86_64): *https://www.elastic.co/es/downloads/elasticsearch*

   1.2. Con la comanda **wget** descargarnos el fichero copiando la ruta del fichero con botón derecho sobre el que nos querramos descargar y nos quedaria asi:

   `$ wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.10.2-linux-x86_64.tar.gz`

2. Una vez descargado, descomprimimos el fichero.tar.gz con la comanda **tar**:

   `$ tar -xzvf elasticsearch-7.10.2-linux-x86_64.tar.gz `


4. Para arrancarlo, ejecutamos la siguiente comanda en la terminal dentro del directorio descomprimido:

   `$ bin/elasticsearch`

#### 2.3.2. Instalación en Windows

1. Vamos a la pagina principal de Elastic Stack, apartado de Elasticsearch y descargarnos el que necesitemos con extension .zip (Windows): *https://www.elastic.co/es/downloads/logstash*

2. Extraemos toda el contenido clicando botón derecho sobre el .zip y damos a "Extraer Todo"

3. Para arrancarlo, ejecutamos la siguiente comanda en la terminal dentro del directorio descomprimido:

   `C:\> .\bin\elasticsearch.bat `

### 2.4. Instalación de Kibana

#### 2.4.1. Instalación en Linux

1. Podemos hacerlo de dos maneras:

   1.1. Ir a la pagina principal de Elastic Stack, apartado de Kibana y descargarnos el que necesitemos con extension .tar.gz (Linux 64-BIT): *https://www.elastic.co/es/downloads/kibana*

   1.2. Con la comanda **wget** descargarnos el fichero copiando la ruta del fichero con botón derecho sobre el que nos querramos descargar y nos quedaria asi:

   `$ wget https://artifacts.elastic.co/downloads/kibana/kibana-7.10.2-linux-x86_64.tar.gz`

2. Una vez descargado, descomprimimos el fichero.tar.gz con la comanda **tar**:

   `$ tar -xzvf kibana-7.10.2-linux-x86_64.tar.gz `


4. Para arrancarlo, ejecutamos la siguiente comanda en la terminal dentro del directorio descomprimido:

   `$ bin/kibana`

#### 2.4.2. Instalación en Windows

1. Vamos a la pagina principal de Elastic Stack, apartado de Kibana y descargarnos el que necesitemos con extension .zip (Windows): *https://www.elastic.co/es/downloads/kibana*

2. Extraemos toda el contenido clicando botón derecho sobre el .zip y damos a "Extraer Todo".

3. Para arrancarlo, ejecutamos la siguiente comanda en la terminal dentro del directorio descomprimido:

   `C:\> .\bin\kibana.bat `

## 3. Instalación con Docker

1. Para la instalación de docker, necesitamos instalar docker. Para eso ejecutamos la siguiente comanda:

   `$ sudo apt install docker docker-compose`

2. Añadiremos nuestro usuario como parte del grupo docker

   `$ sudo usermod -aG docker $USER`

3. El siguiente paso es hacer el docker-compose y para ello ejecutamos la seguiente comanda:

   ````bash
   $ cat << END > /home/$USER/Elastic_Stack_Docker/docker-compose.yml
   version: ‘3.7’
   
   services:
     
     elasticsearch:
       image: docker.elastic.co/elasticsearch/elasticsearch:7.10.2
       ulimits: #Numero de ficheros que puede mantener abierto dentro del sistema
         memlock:
           soft: -1 #Ilimitado, es decir, sin restricciones
           hard: -1
       environment:
         - bootstrap.memory_lock=true
         - “ES_JAVA_OPTS=-Xms512m -Xmx512m”
         - discover.type=single-node
       volumes:
         - ~/Elastic_Stack_Docker/elasticsearch/data:/usr/share/elasticsearch/data
       ports:
         - 9200:9200
         - 9300:9300
   
     logstash:
       image: docker.elastic.co/logstash/logstash:7.10.2
       volumes:
         - ~/Elastic_Stack_Docker/logstash/pipeline:/usr/share/logstash/pipeline
     kibana:
       image: docker.elastic.co/kibana/kibana:7.10.2
       ports:
         - 5601:5601
   END
   ````

4. Finalmente ejecutamos este docker compose de la siguiente manera:

   `$ docker-compose up -d`

## 4. Configuración básica

### 4.1. Beats (FileBeat)

Para que funcione de manera básica Filebeat, modificamos lo siguiente en el fichero filebeat.yml:

```YAML
Apartado # ======= Filebeat inputs =========
En caso de que este apagado, lo cambiamos:
# enabled: false --> enabled: true
Cambiamos o añadimos una ruta más en la parte de paths (rutas) 
paths:
  - ../logs/*.log # Con el * le decimos todo lo que venga antes del .log

Apartado # ======== Outputs ==========
Comentamos la salida de elasticsearch y descomentamos la salida de logstash
Subapartado # ---------- Elasticsearch Output-------
output.elasticsearch: --> # output.elasticsearch:
  hosts: ["localhost:9200"] --> # hosts: ["localhost:9200"]
Subapartado # ----------- Logstash Output -------
# output.logstash: --> output.logstash:
  # hosts: ["localhost:5044"] --> hosts: ["localhost:5044"]
```

Para más información, en el documento filebeat.reference.yml muestra lo que se puede añadir

### 4.2. Beats (MetricBeat)

Para que funcione de manera basica metricbeat, modificamos lo siguiente en el fichero metricbeat.yml:

```YAML
Apartado # ======== Dashboards =======
Encender la configuración de los dashboards
# setup.dashboards.enabled: false --> setup.dashboards.enabled: true

Apartado # ======== Outputs ==========
Comentamos la salida de logstash y descomentamos la salida de elasticsearch ya que con este componente no pasa por logstash sino directamente por elasticsearch
Subapartado # ---------- Elasticsearch Output -------
# output.elasticsearch: --> output.elasticsearch:
  # hosts: ["localhost:9200"] --> hosts: ["localhost:9200"]
Subapartado # ----------- Logstash Output -------
output.logstash: --> # output.logstash:
  hosts: ["localhost:5044"] --> # hosts: ["localhost:5044"]
  
Apartado #============ X-Pack Monitoring ==========
Encendemos la monitorización
# monitoring.enabled: false --> monitoring.enabled: true
```

Para más información, en el documento metricbeat.reference.yml muestra lo que se puede añadir

### 4.3. Beats (PacketBeat)

Para que funcione de manera básica Packetbeat, modificamos lo siguiente en el fichero packetbeat.yml:

```YAML
Apartado # ======= Network device =========
Para que este componente pueda ver todo el trafico de todas las interfaces de red
packetbeat.interfaces.device: eno4 --> packetbeat.interfaces.device: any

Apartado # ======== Dashboards =======
Encender la configuración de los dashboards
# setup.dashboards.enabled: false --> setup.dashboards.enabled: true

Apartado # ======== Outputs ==========
Comentamos la salida de logstash y descomentamos la salida de elasticsearch ya que con este componente no pasa por logstash sino directamente por elasticsearch
Subapartado # ---------- Elasticsearch Output -------
# output.elasticsearch: --> output.elasticsearch:
  # hosts: ["localhost:9200"] --> hosts: ["localhost:9200"]
Subapartado # ----------- Logstash Output -------
output.logstash: --> # output.logstash:
  hosts: ["localhost:5044"] --> # hosts: ["localhost:5044"]

Apartado #============ X-Pack Monitoring ==========
Encendemos la monitorización
# monitoring.enabled: false --> monitoring.enabled: true
```

Para más información, en el documento packetbeat.reference.yml muestra lo que se puede añadir.

### 4.4. Logstash

La configuración básica de Logstash para su funcionalidad. En este caso le decimos que la entrada seria de Beats por el puerto 5044 y lo redireccionaría hacia elasticsearch por el puerto 9200

```bash
input {
	beats {
		port => 5044
	}
}

output {
	elasticsearch{
		port => 9200
	}
}
```

### 4.5. Elasticsearch

Para Elasticsearch, no hace falta ninguna configuración especial salvo que se necesite un cluster o que el nodo principal sea seguro. Nos basta con ejecutar la siguiente comanda dentro del directorio de elasticsearch:

`~/elasticsearch$ bin/elasticsearch`

### 4.6. Kibana

Para kibana, no hace falta ninguna configuración especial ya que ya contiene las opciones necesarias para arrancarlo. Nos basta con ejecutar la siguiente comanda dentro del directorio de kibana:

`~/kibana$ bin/kibana`

### 4.7. Prueba de funcionamiento

Para comprobar que nuestro Elastic Stack funciona correctamente, vamos a hacer una prueba de funcionamiento. Para ello, vamos a generar un log aleatorio para que, en este caso filebeat se los pase a elasticsearch para poder verlos en kibana. En este caso solo vamos a usar filebeat porque es el mas sencillo.

Como no tenemos unos servicios con logs generados, vamos a hacer nuestro propio log. Un ejemplo seria el siguiente:

```bash
$ cat << END >> Elastic_Stack/logs/example.log
Hola
Adios
Buenos dias
Buenas tardes
END
```

Ejecutamos las comandas para el funcionamiento de Elastic Stack dentro de sus respectivos directorios:

`$ ./filebeat test config` --> Para comprovar que el fichero esta bien (Figura 1.1)

![image-20210208114645118](C:\Users\cosmin.bora\AppData\Roaming\Typora\typora-user-images\image-20210208114645118.png)

`$ ./filebeat test output` --> Para comprovar que se comunica con elasticsearch

![image-20210208114840713](C:\Users\cosmin.bora\AppData\Roaming\Typora\typora-user-images\image-20210208114840713.png)

`$ ./filebeat setup` --> Para que nos cree el indice de entrada

`$ ./filebeat -e -c filebeat.yml ` --> Con la opcion `-e` nos mostrará lo que hara filebeat en tiempo real

`$ bin/logstash -f config/logstash-sample.conf` --> Iniciamos logstash con su respectiva configuración

`$ bin/elasticsearch` --> Iniciamos elasticsearch

`bin/kibana` --> Iniciamos kibana



## 5. Configuración avanzada

https://www.elastic.co/es/blog/how-to-ingest-data-into-elasticsearch-service

### 5.1. Inputs

Un input es un tipo de entrada que pertenece a logstash y sirve para que le indiquemos de que fuente especifica necesite que lea. En la siguiente dirección hay una lista de los siguientes tipos de las fuentes especificas mencionadas anteriormente: https://www.elastic.co/guide/en/logstash/current/input-plugins.html

Logstash permite muchos tipos de entradas pero el que vamos a ver y el mas común es el de **beats**:

```bash
input {
    beats {
        port => 5044
    }
}
```

Con esto mostramos la configuración más sencilla y la que logstash proporciona como la configuración simple llamada ***logstash-sample.conf***. Le estamos indicando aquí que la entrada estándar sea beats, es decir, que todo lo procedente de Beats lo deje pasar, y el puerto por defecto de beats el 5044. (En caso de que deseemos otro puerto, en la configuración .yml de beats, cambiar el puerto del ***output Logstash*** por el puerto deseado y en esta configuración de Logstash poner el puerto puesto en la configuración .yml).

### 5.2. Filter

El filter (o filtro) es el procesamiento de estos datos si nuestros requesitos son extrictos, es decir, si nosotros queremos que los datos solo sean informativos, lo haremos de tal manera que la información procedente de la entrada definida se filtre y solo nos muestre esto. En la siguiente dirección hay una lista de los filtros posibles: https://www.elastic.co/guide/en/logstash/current/filter-plugins.html

De ejemplo usaremos un filtro común llamado **grok** que funciona con regex (patrones) y tendremos un ejemplo de un log y un ejemplo del filtro para este log:

`55.3.244.1 GET /index.html 15824 0.043`

```bash
input {
    beats {
        port => 5044
    }
}

filter {
	grok{
		match => { "message" => "%{IP:client} %{WORD:method} %{URIPATHPARAM:request} %{NUMBER:bytes} %{NUMBER:duration}" }
	}
}
```

Aqui lo que estamos diciendo que todo lo que venga de beats (va a ir linea por linea en caso de que tenga una gran cantidad de logs ya que lo tiene que indexar) lo indexe de tal forma que el primer campo es la **IP** del cliente y el campo donde se guarda se llama **client**; Seguidamente tenemos el metodo de envio (GET/POST) de tipo **WORD** y lo guarda en el campo **method**; que es lo que ha visitado, que ha sido el index.html que es de tipo **URIPATHPARAM** y lo guarda en el campo **request**; el numero de bytes que es de tipo **NUMBER** y el campo se llama **bytes**; Y finalmente tenemos la duración, de tipo **NUMBER** y el campo se llama **duration**

Todos estos tipos mencionados anteriormente son patrones creados por Elastic Stack y invocandolos de la forma que esta en el ejemplo funciona. En la siguiente dirección hay una lista de los patrones existentes de logstash: https://github.com/logstash-plugins/logstash-patterns-core/blob/master/patterns/grok-patterns

### 5.3. Outputs

Finalmente tenemos los outputs que es la salida estándar de Logstash, es decir, hacia donde ha de enviar esta información. Normalmente la salida es Elasticsearch por el puerto 9200 pero tenemos muchas opciones y en el enlace siguiente las tenemos: https://www.elastic.co/guide/en/logstash/current/output-plugins.html

```bash
output {
	elasticsearch{
		port => 9200
		index => "%{[some_field][sub_field]}-%{+YYYY.MM.dd}"
	}
}
```

En este ejemplo le estamos indicando que la salida es elasticsearch donde le indicamos el puerto a conectarse, que es el 9200, i a la hora de la creacion del indice, siga el siguiente patrón.

### 5.4. Modulos

Elastic Stack nos ofrece una lista de modulos que nos puede dar información sobre ellos (servicios, rendimiento, etc.). Algunos de los modulos son Apache, MySQL, AWS, System, Nginx y muchos más.

Para poder ver esos modulos, ejecutamos lo siguiente:

`$ ./filebeat modules list`

Nos aparecerán como dos apartados: ***Enabled*** que son los que estan encendidos y los ***Disabled*** que son los que estan apagados. Para enceder o apagar algun modulo que no nos interese, ejecutamos la siguiente comanda:

`$ ./filebeat modules enable/disable [modulo]`

Para modificar algunos de sus parámetros, vamos al directorio **modules.d/** y con un editor de texto modificamos el modulo con .yml. Para más información en el siguiente enlace de filebeat: *https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-modules.html*

Aqui tenemos dos ejemplos de como serian los modulos de nginx (primera foto filebeat y seguna foto metricbeat). Packetbeat no ofrece modulos.

En caso de que algo no vaya bien, vamos a "**Home**" --> **Ingest your data**" --> "**Add data**" --> "**Apache Logs**" y os mostrara como un seguimiento de lo que tendriamos que tener. En el siguiente link teneis más información del modulo de apache: *https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-module-apache.html*

### 5.5. Autenticación en Kibana

Principalmente, en Kibana no viene ningun usuario predefinido, es decir, poniendo en el navegador http://localhost:5601 ya nos muestra toda la información. Para ello vamos a activar la autentificación de usuarios. Para ello, Kibana tiene que estar encendido ya que con el apagado no va a funcionar. Para encenderlo, ejecutamos la siguiente comanda:

`~/kibana$ bin/kibana`

En otra terminal, vamos al directorio respectivo de elasticsearch y aplicando la siguiente comanda hacemos una copia de seguridad del original por si modificamos algo que nos destruya Elasticsearch y añadimos/modificamos lo siguiente:

```bash
~/elasticsearch/config$ cp elasticsearch.yml elasticsearch.yml.back && cat << END >> elasticsearch.yml
# ---------------- X-Pack Security ---------------------------
xpack.security.enabled: true
discovery.type: single-node
END
```

Con la opción **xpack.security.enabled: true** lo que le decimos es que encienda la opción de seguridad ya que a parte dentro de esta esta la configuración de los usuarios. Con la opción **discovery.type: single-node** le decimos que Elasticsearch forma un cluster de un solo nodo. En caso de que esta opción nos de problemas, quitarlo o comentarlo con el **\#**

A continuación, siguiendo dentro del directorio de Elasticsearch, ejecutamos la seguiente comanda:

`~/elasticsearch$ bin/elasticsearch-setup-passwords interactive`

Con esta comanda encendemos todos los usuarios y le definimos las contraseñas.

Seguidamente, en el archivo kibana.yml descomentaremos el usuario con su contraseña poniendole en este caso el de superusuario que se llama **elastic**:

```bash
~/kibana$ sed -i 's/#elasticsearch.username: "kibana_system"/elasticsearch.username: "elastic"/g'
~/kibana$ sed -i 's/#elasticsearch.password: "kibana_system"/elasticsearch.password: "elastic"/g'
```

Finalmente, si vemos que cuando ponemos http://localhost:5601 en el navegador nos sale, significa que lo tenemos:

Y para iniciar sesión, nos mostrará la ventana donde pondremos como **Username** ***elastic*** y **Password** ***elastic***.

*INFO: https://www.elastic.co/guide/en/cloud-enterprise/current/ece-manage-system-passwords.html#ece-retrieve-passwords*

#### 5.5.1. Roles

*INFO: https://www.elastic.co/guide/en/elasticsearch/reference/current/built-in-roles.html*

Elastic Stack ya nos proporciona unos roles creados con unas funciones determinadas. Los roles son los siguientes:

##### <u>Reservados</u>

- `APM`
  - `apm_system`
    - Otorga el acceso necesario para que el usuario del sistema APM envíe datos a nivel del sistema (como la supervisión) a Elasticsearch.
  - `apm_user`
    - Otorga los privilegios necesarios para los usuarios de APM (que son los privilegios `read` y `view_index_metadata` en los índices `apm-*` y  `.ml-anomalies*`).

- `BEATS`
  - `beats_admin`
    - Otorga acceso al índice `.management-beats`, que contiene información de configuración para Beats.
  - `beats_system`
    - Otorga el acceso necesario para que el usuario del sistema Beats envíe datos a nivel del sistema (como la supervisión) a Elasticsearch. Este rol no proporciona acceso a los índices de beats y no es adecuado para escribir resultados de beats en Elasticsearch. Este rol no debe asignarse a los usuarios ya que los permisos otorgados pueden cambiar entre versiones.

- `KIBANA`
  - `kibana_system`
    - Otorga el acceso necesario para que el usuario del sistema Kibana lea y escriba en los índices de Kibana, administre las plantillas de índice y los tokens y verifique la disponibilidad del clúster de Elasticsearch. Este rol otorga acceso de lectura a los índices de`.monitoring-*` y acceso de lectura y escritura a los índices de `.reporting-*`. Para obtener más información, consulte [Configurar la seguridad en Kibana](https://www.elastic.co/guide/en/kibana/7.11/using-kibana-with-security.html). Este rol no debe asignarse a los usuarios ya que los permisos otorgados pueden cambiar entre versiones.
  - `kibana_admin`
    - Otorga acceso a todas las funciones de Kibana. Para obtener más información sobre la autorización de Kibana, consulte [Autorización de Kibana](https://www.elastic.co/guide/en/kibana/7.11/xpack-security-authorization.html) .

- `INGESTA`
  - `enrich_user`
    - Otorga acceso para administrar **todos **los índices de enriquecimiento ( `.enrich-*`) y **todas** las operaciones en las canalizaciones del nodo de ingesta.
  - `ingest_admin`
    - Otorga acceso para administrar **todas **las plantillas de índice y **todas **las configuraciones de canalización de ingesta. Esta función **no** proporciona la capacidad de crear índices; esos privilegios deben definirse en un rol separado.

- `LOGSTASH`

  - `logstash_admin`
    - Otorga acceso a los índices `.logstash*` para administrar configuraciones y otorga el acceso necesario para las API específicas de logstash expuestas por el complemento logstash x-pack.
  - `logstash_system`
    - Otorga el acceso necesario para que el usuario del sistema Logstash envíe datos a nivel del sistema (como el monitoreo) a Elasticsearch. Para obtener más información, consulte [Configuración de seguridad en Logstash](https://www.elastic.co/guide/en/logstash/7.11/ls-security.html). Este rol no debe asignarse a los usuarios ya que los permisos otorgados pueden cambiar entre versiones. Este rol no proporciona acceso a los índices de logstash y no es adecuado para su uso dentro de una canalización de Logstash.
  - `machine_learning_admin`
    - Proporciona todos los privilegios del rol `machine_learning_user` más el uso completo de la API de aprendizaje automático. Las subvenciones `manage_ml ` se agrupan privilegios de acceso de lectura a los índices `.ml-anomalies*`, `.ml-notifications*`, `.ml-state*`, `.ml-meta*` y acceso de escritura a los índices `.ml-annotations*`. Los administradores de aprendizaje automático también necesitan privilegios de índice para los índices y roles de origen y destino que otorgan acceso a Kibana. Consulte [Privilegios de seguridad de aprendizaje automático](https://www.elastic.co/guide/en/machine-learning/7.11/setup.html#setup-privileges) .
  - `machine_learning_user`
    - Otorga los privilegios mínimos necesarios para ver la configuración, el estado y el trabajo del aprendizaje automático con los resultados. Esta función otorga privilegios `monitor_ml` de clúster, acceso de lectura a los índices `.ml-notifications` y  `.ml-anomalies*` (que almacenan los resultados del aprendizaje automático) y acceso de escritura a los índices `.ml-annotations*`. Los usuarios de aprendizaje automático también necesitan privilegios de índice para los índices y roles de origen y destino que otorgan acceso a Kibana. Consulte [Privilegios de seguridad de aprendizaje automático](https://www.elastic.co/guide/en/machine-learning/7.11/setup.html#setup-privileges) .
  - `monitoring_user`
    - Otorga los privilegios mínimos requeridos para cualquier usuario de monitoreo de X-Pack que no sean los requeridos para usar Kibana. Este rol otorga acceso a los índices de monitoreo y otorga los privilegios necesarios para leer la información básica del clúster. Esta función también incluye todos los [privilegios de Kibana](https://www.elastic.co/guide/en/kibana/7.11/kibana-privileges.html) para las funciones de supervisión de Elastic Stack. Los usuarios de supervisión también deben tener asignado el rol `kibana_admin` u otro rol con [acceso a la instancia de Kibana](https://www.elastic.co/guide/en/kibana/7.11/xpack-security-authorization.html).
  - `remote_monitoring_agent`
    - Otorga los privilegios mínimos necesarios para escribir datos en los índices de supervisión (`.monitoring-*`). Este rol también tiene los privilegios necesarios para crear índices en Metricbeat (`metricbeat-*`) y escribir datos en ellos.

  - `remote_monitoring_collector`
    - Otorga los privilegios mínimos necesarios para recopilar datos de supervisión para Elastic Stack.
  - `reporting_user`
    - Otorga los privilegios específicos necesarios para los usuarios de informes de X-Pack, que son distintos de los necesarios para utilizar Kibana. Esta función otorga acceso a los índices de informes y cada usuario tiene acceso solo a sus propios informes. A los usuarios de informes también se les deben asignar roles adicionales que otorguen [acceso a Kibana](https://www.elastic.co/guide/en/kibana/7.11/xpack-security-authorization.html) , así como acceso de lectura a los [índices](https://www.elastic.co/guide/en/elasticsearch/reference/current/defining-roles.html#roles-indices-priv) que se utilizarán para generar informes.
  - `snapshot_user`
    - Otorga los privilegios necesarios para crear instantáneas de **todos** los índices y ver sus metadatos. Esta función permite a los usuarios ver la configuración de los repositorios de instantáneas existentes y los detalles de las instantáneas. No otorga autoridad para eliminar o agregar repositorios o restaurar instantáneas. Tampoco permite cambiar la configuración del índice o leer o actualizar el flujo de datos o los datos del índice.
  - `superuser`
    - Otorga acceso completo al clúster, incluidos todos los índices y datos. Un usuario con el `superuser` rol también puede administrar usuarios y roles y [suplantar](https://www.elastic.co/guide/en/elasticsearch/reference/current/run-as-privilege.html) a cualquier otro usuario en el sistema. Debido a la naturaleza permisiva de este rol, tenga especial cuidado al asignarlo a un usuario.
  - `transform_admin`
    - Otorga el privilegio del clúster `manage_transform`, que le permiten administrar transformaciones. Esta función también incluye todos los [privilegios de Kibana](https://www.elastic.co/guide/en/kibana/7.11/kibana-privileges.html) para las funciones de aprendizaje automático.
  - `transform_user`
    - Otorga el privilegio del clúster `monitor_transform`, que le permiten utilizar transformaciones. Esta función también incluye todos los [privilegios de Kibana](https://www.elastic.co/guide/en/kibana/7.11/kibana-privileges.html) para las funciones de aprendizaje automático.
  - `transport_client`
    - Otorga los privilegios necesarios para acceder al clúster a través de Java Transport Client. El cliente de transporte de Java obtiene información sobre los nodos en el clúster mediante la *API Node Liveness* y la *API de estado* del *clúster* (cuando el rastreo está habilitado). Asigne a sus usuarios este rol si utilizan Transport Client.
    - El uso de Transport Client de manera efectiva significa que los usuarios tienen acceso al estado del clúster. Esto significa que los usuarios pueden ver los metadatos de todos los índices, plantillas de índices, asignaciones, nodos y básicamente todo lo relacionado con el clúster. Sin embargo, esta función no otorga permiso para ver los datos en todos los índices.
  - `watcher_admin`
    - Permite a los usuarios crear y ejecutar todas las acciones de Watcher. Otorga acceso de lectura al índice `.watches`. También otorga acceso de lectura al historial de reproducciones y al índice de reproducciones activadas.
  - `watcher_user`
    - Otorga acceso de lectura al índice `.watches`, la acción de visualización y las estadísticas del observador.

##### <u>Obsoletos</u>

- `KIBANA`

  - `data_frame_transforms_admin`
    - Otorga el privilegio del clúster `manage_data_frame_transforms`, que le permiten administrar transformaciones. Esta función también incluye todos los [privilegios de Kibana](https://www.elastic.co/guide/en/kibana/7.11/kibana-privileges.html) para las funciones de aprendizaje automático. [ 7.5.0 ] En desuso en 7.5.0. Reemplazado por [`transform_admin`](https://www.elastic.co/guide/en/elasticsearch/reference/current/built-in-roles.html#built-in-roles-transform-admin).
  - `data_frame_transforms_user`
    - Otorga el privilegio del clúster `monitor_data_frame_transforms`, que le permiten utilizar transformaciones. Esta función también incluye todos los [privilegios de Kibana](https://www.elastic.co/guide/en/kibana/7.11/kibana-privileges.html) para las funciones de aprendizaje automático. [ 7.5.0 ] En desuso en 7.5.0. Reemplazado por[`transform_user`](https://www.elastic.co/guide/en/elasticsearch/reference/current/built-in-roles.html#built-in-roles-transform-user).
  - `kibana_dashboard_only_user`
    - (Esta función está en desuso, utilice los [privilegios de funciones de Kibana](https://www.elastic.co/guide/en/kibana/7.11/kibana-privileges.html#kibana-feature-privileges) en su lugar). Otorga acceso de solo lectura al panel de Kibana en todos los [espacios de Kibana](https://www.elastic.co/guide/en/kibana/7.11/xpack-spaces.html). Este rol no tiene acceso a herramientas de edición en Kibana.

  - `kibana_user`
    - (Esta función está obsoleta, utilice la función [`kibana_admin`](https://www.elastic.co/guide/en/elasticsearch/reference/current/built-in-roles.html#built-in-roles-kibana-admin) en su lugar). Otorga acceso a todas las funciones de Kibana. Para obtener más información sobre la autorización de Kibana, consulte [Autorización de Kibana](https://www.elastic.co/guide/en/kibana/7.11/xpack-security-authorization.html).

#### 5.5.2. Usuarios

INFO: https://www.elastic.co/guide/en/elasticsearch/reference/current/built-in-users.html

##### <u>Reservados</u>

- `apm_system`
  - El usuario que usa el servidor APM cuando almacena información de monitoreo en Elasticsearch.
- `beats_system`
  - El usuario que utilizan los Beats al almacenar información de supervisión en Elasticsearch.
- `elastic`
  - Un [superusuario](https://www.elastic.co/guide/en/elasticsearch/reference/current/built-in-roles.html) incorporado .
- `kibana_system`
  - El usuario que usa Kibana para conectarse y comunicarse con Elasticsearch.
- `logstash_system`
  - El usuario que Logstash usa cuando almacena información de monitoreo en Elasticsearch.
- `remote_monitoring_user`
  - El usuario que usa Metricbeat al recopilar y almacenar información de monitoreo en Elasticsearch. Tiene el `remote_monitoring_agent`y `remote_monitoring_collector`funciones integradas.

##### <u>Obsoletos</u>

- `kibana`

#### 5.5.3. Creación de usuarios en Kibana

Para la creacion de usuarios en Kibana, Vamos al apartado de **Management (Administración)** --> **Stack Management (Gestión de la Administración)** --> Sección **Security (Seguridad)** --> **Users (Usuarios)** y nos saldría una ventana como esta:

Vamos en la casilla superior derecha y clicamos en **Create User (Creación del usuario)** donde nos pedirá una información.

En el apartado de roles dependiendo de que funciones tiene el usuario al crearse mirar sección **5.5.1. Roles**

### 5.7. Modo seguro: HTTPS con SSL/TLS

Elastic Stack permite el cifrado de datos SSL (Secure Sockets Layer) que es un protocolo para mantener segura una conexión a Internet y TLS (Transport Layer Security) que protege cualquier tipo de dato que se envie entre dos sistemas (en este caso entre el usuario y el servidor). Para hacerlo seguro, vamos a aplicar las siguientes comandas:

1. Creamos el certificado autofirmado y se nos generara un certificado llamado **elastic-stack-ca.p12**:

```bash
~/elasticsearch$ bin/elasticsearch-certutil  ca
```

```bash
Please enter the desired output file [elastic-stack-ca.p12]: <ENTER>
Enter password for elastic-stack-ca.p12 : <ENTER> (opcional añadir contraseña)
```

2. Creamos el certificado para el nodo Elasticsearch con el certificado autofirmado creado anteriormente:

```bash
~/elasticsearch$ bin/elasticsearch-certutil cert --ca elastic-stack-ca.p12
```

```bash
Enter password for CA (elastic-stack-ca.p12) : <ENTER> (opcional puedes añadir contraseña)
Please enter the desired output file [elastic-certificates.p12]: <ENTER>
Enter password for elastic-certificates.p12 : <ENTER< (opcional puedes añadir contraseña)
```

3. Nos copiamos el certificado generado dentro del directorio **config** (<u>MUY IMPORTANTE</u>, ya que sino no funcionara), cambiamos el propietario a root y damos permisos

```bash
cp elastic-certificates.p12 ~/elasticsearch/config
sudo chown root ~/elasticsearch/elastic-certificates.p12
sudo chmod 660 ~/elasticsearch/elastic-certificates.p12
```

4. Generamos un certificado

```bash
~/elasticsearch$ bin/elasticsearch-certutil  http
```

```bash
Generate a CSR? [y/N] <ENTER>

Use an existing CA? [y/N]y

CA Path: /home/server/Elastic_Stack/elasticsearch-7.10.2/config/elastic-stack-ca.p12
Password for elastic-stack-ca.p12: <ENTER>

For how long should your certificate be valid? [5y] 5y

Generate a certificate per node? [y/N] <ENTER>

Is this correct [Y/n] <ENTER>

Is this correct [Y/n] <ENTER>

Key Name: elasticsearch
Subject DN: CN=elasticsearch
Key Size: 2048

Do you wish to change any of these options? [y/N] <ENTER>

Provide a password for the "http.p12" file:  [<ENTER> for none] <ENTER> (opcional añadir contraseña)

What filename should be used for the output zip file? [/usr/share/elasticsearch/elasticsearch-ssl-http.zip] <ENTER>
```

5. Descomprimimos el archivo .zip y tendremos un directorio llamado elasticsearch, nos copiamos el certificado generado dentro del directorio **config** de nuestro elasticsearch (<u>MUY IMPORTANTE</u>, ya que sino no funcionara), cambiamos el propietario a root y damos permisos.

```bash
unzip elasticsearch-ssl-http.zip
cp http.p12 ~/elasticsearch/config
sudo chown root ~/elasticsearch/config/http.p12
sudo chmod 660 ~/elasticsearch/config/http.p12
```

6. Generamos un certificado para kibana.

```bash
bin/elasticsearch-certutil ca --pem
unzip elastic-stack-ca.zip
---------------------- A partir de aqui iria en la parte del fichero de configuración
nano config/kibana.yml
server.ssl.enabled: true
server.ssl.certificate: /home/server/Elastic_Stack/elasticsearch-7.10.2/ca/ca.crt
server.ssl.key: /home/server/Elastic_Stack/elasticsearch-7.10.2/ca/ca.key
```

```bash
Please enter the desired output file [elastic-stack-ca.zip]: <OPCIONAL>
```

7. Una vez generados y modificados, añadiremos estas líneas al fichero de configuración elasticsearch.yml

```bash
~/elasticsearch/config$ cat << END >> elasticsearch.yml
#-------------- Security Features --------------
xpack.security.enabled: true
discovery.type: single-node
xpack.security.transport.ssl.enabled: true
xpack.security.transport.ssl.verification_mode: certificate
xpack.security.transport.ssl.keystore.path: elastic-certificates.p12
xpack.security.transport.ssl.truststore.path: elastic-certificates.p12
xpack.security.http.ssl.enabled: true
xpack.security.http.ssl.keystore.path: "http.p12"
END
```

8. En el fichero de Kibana llamado kibana.yml

```bash
~/kibana/config$ sed -i 's/#elasticsearch.hosts: "localhost:9200"/elasticsearch.hosts: ["https://localhost:9200"]/g' kibana.yml

~/kibana/config$ sed -i 's/#elasticsearch.username: "kibana_system"/elasticsearch.username: "elastic"/g' kibana.yml
~/kibana/config$ sed -i 's/#elasticsearch.password: "kibana_system"/elasticsearch.password: "elastic"/g' kibana.yml

~/kibana/config$ sed -i 's/#server.ssl.enabled: false/server.ssl.enabled: true/g' kibana.yml

~/kibana/config$ sed -i 's/#server.ssl.certificate: \/path\/to\/your\/client.crt/server.ssl.certificate: \/home\/server\/Elastic_Stack\/kibana-7.10.2-linux-x86_64\/config\/ca\/ca.crt/g' kibana.yml

~/kibana/config$ sed -i 's/#server.ssl.key: \/path\/to\/your\/client.key/server.ssl.key:\/home\/server\/Elastic_Stack\/kibana-7.10.2-linux-x86_64\/config\/ca\/ca.key\/g' kibana.yml

~/kibana/config$ sed -i 's/#elasticsearch.ssl.certificateAuthorities: [ "/path/to/your/CA.pem" ]/elasticsearch.ssl.certificateAuthorities: [ "/home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca/ca.crt" ]/g' kibana.yml

~/kibana/config$ sed -i 's/#elasticsearch.ssl.verificationMode: full/elasticsearch.ssl.verificationMode: none/g' kibana.yml
```

9. En los ficheros de Beats (filebeat, metricbeat, etc) llamados <componente>.yml

```bash
#----------- Kibana ---------
sed -i 's/host: "localhost:5601"/host: "https://localhost:5601"/g' <ruta>.yml
sed -i 's/#setup.kibana.ssl.enabled: false/setup.kibana.ssl.enabled: true/g' <ruta>.yml
sed -i 's/#ssl.certificate_authorities: ["/etc/pki/root/ca.pem"]/ssl.certificate_authorities ["/home/server/Elastic_Stack/kibana/config/ca/ca.crt"]/g' <ruta>.yml

sed -i 's/#ssl.certificate: "/etc/pki/client/cert.pem"/ssl.certificate: "/home/server/Elastic_Stack/kibana-7.10.2/config/ca/ca.crt"/g' <ruta>.yml

sed -i 's/#ssl.key: "/etc/pki/client/cert.key"/ssl.key: "/home/server/Elastic_Stack/kibana-7.10.2-linux/config/ca/ca.key"/g' <ruta>.yml

sed -i 's/#ssl.verification_mode: full/ssl.verification_mode: none/g' <ruta>.yml

# ------- Output Elasticsearch --------
sed -i 's/#protocol: "https"/protocol: "https"/g' <ruta>.yml

sed -i 's/#username: "elastic"/username: "elastic"/g' <ruta>.yml
sed -i 's/#password: "changeme"/password: "elastic"/g' <ruta>.yml

sed -i 's/#ssl.verification_mode: full/ssl.verification_mode: none/g' <ruta>.yml
```

Más información en: https://techexpert.tips/es/elasticsearch-es/elasticsearch-habilite-el-cifrado-tls-y-la-comunicacion-https/

### 5.8. Prueba de funcionamiento

Probar de hacer el paso de datos,

https://www.youtube.com/watch?v=i4T1PNQZsiY

https://www.youtube.com/watch?v=31wJJPZgWrQ

Captura de paquetes con wireshark: https://www.elastic.co/es/blog/analyzing-network-packets-with-wireshark-elasticsearch-and-kibana

https://www.datio.com/security/inspeccion-de-trafico-cifrado-tls-ssl/

### 5.9. Instalacion con Docker (Aplicando todo lo anterior)

info: https://www.elastic.co/guide/en/elasticsearch/reference/master/docker.html

Primera parte, crear el .env

```bash
cat << END > .env
VERSION=7.11.0
CLUSTER_NAME=es-docker-cluster
CERTS_DIR=/usr/share/elasticsearch/config/certificates
NETWORK=elastic
END
```

Segunda parte, crear el docker-compose.yml

```bash
~$ cat << END > docker-compose.yml
version: '2.2'

services:

  es01:
    image: docker.elastic.co/elasticsearch/elasticsearch:\${VERSION}
    container_name: es01
    environment:
      - node.name=es01
      - cluster.name=\${CLUSTER_NAME}
      - discovery.seed_hosts=es02,es03
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data01:/usr/share/elasticsearch/data
    ports:
      - 9200:9200
    networks:
      - \${NETWORK}

  es02:
    image: docker.elastic.co/elasticsearch/elasticsearch:\${VERSION}
    container_name: es02
    environment:
      - node.name=es02
      - cluster.name=\${CLUSTER_NAME}
      - discovery.seed_hosts=es01,es03
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data02:/usr/share/elasticsearch/data
    networks:
      - \${NETWORK}

  es03:
    image: docker.elastic.co/elasticsearch/elasticsearch:\${VERSION}
    container_name: es03
    environment:
      - node.name=es03
      - cluster.name=\${CLUSTER_NAME}
      - discovery.seed_hosts=es01,es02
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data03:/usr/share/elasticsearch/data
    networks:
      - \${NETWORK}

  kib01:
    image: docker.elastic.co/kibana/kibana:\${VERSION}
    container_name: kib01
    ports:
      - 5601:5601
    environment:
      ELASTICSEARCH_URL: http://es01:9200
      ELASTICSEARCH_HOSTS: '["http://es01:9200","http://es02:9200","http://es03:9200"]'
    networks:
      - \${NETWORK}

volumes:
  data01:
    driver: local
  data02:
    driver: local
  data03:
    driver: local

networks:
  \${NETWORK}:
    driver: bridge
END
```

Tercera parte, indicar las instancias para la creación de certificados:

```bash
~$ cat << END > instances.yml
instances:
  - name: es01
    dns:
      - es01
      - localhost
    ip:
      - 127.0.0.1

  - name: es02
    dns:
      - es02
      - localhost
    ip:
      - 127.0.0.1

  - name: es03
    dns:
      - es03
      - localhost
    ip:
      - 127.0.0.1

  - name: 'kib01'
    dns:
      - kib01
      - localhost
END
```

Cuarta parte, crear un fichero .yml para la creación de los certificados:

```bash
~$ cat << END > create-certs.yml
version: '2.2'

services:

  create_certs:
    image: docker.elastic.co/elasticsearch/elasticsearch:\${VERSION}
    container_name: create_certs
    command: >
      bash -c '
        yum install -y -q -e 0 unzip;
        if [[ ! -f /certs/bundle.zip ]]; then
          bin/elasticsearch-certutil cert --silent --pem --in config/certificates/instances.yml -out /certs/bundle.zip;
          unzip /certs/bundle.zip -d /certs;
        fi;
        chown -R 1000:0 /certs
      '
    working_dir: /usr/share/elasticsearch
    volumes:
      - certs:/certs
      - .:/usr/share/elasticsearch/config/certificates
    networks:
      - \${NETWORK}

volumes:
  certs:
    driver: local

networks:
  \${NETWORK}:
    driver: bridge
END
```

 Finalmente, creamos el fichero .yml para la configuración de HTTPS/SSL/TLS

```bash
~$ cat << END > elastic-docker-tls.yml
version: '2.2'

services:

  es01:
    image: docker.elastic.co/elasticsearch/elasticsearch:\${VERSION}
    container_name: es01
    environment:
      - node.name=es01
      - cluster.name=\${CLUSTER_NAME}
      - discovery.seed_hosts=es02,es03
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - xpack.license.self_generated.type=trial 
      - xpack.security.enabled=true
      - xpack.security.http.ssl.enabled=true 
      - xpack.security.http.ssl.key=$CERTS_DIR/es01/es01.key
      - xpack.security.http.ssl.certificate_authorities=$CERTS_DIR/ca/ca.crt
      - xpack.security.http.ssl.certificate=$CERTS_DIR/es01/es01.crt
      - xpack.security.transport.ssl.enabled=true 
      - xpack.security.transport.ssl.verification_mode=certificate 
      - xpack.security.transport.ssl.certificate_authorities=$CERTS_DIR/ca/ca.crt
      - xpack.security.transport.ssl.certificate=$CERTS_DIR/es01/es01.crt
      - xpack.security.transport.ssl.key=$CERTS_DIR/es01/es01.key
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data01:/usr/share/elasticsearch/data
      - certs:\${CERTS_DIR}
    ports:
      - 9200:9200
    networks:
      - \${NETWORK}

    healthcheck:
      test: curl --cacert $CERTS_DIR/ca/ca.crt -s https://localhost:9200 >/dev/null; if [[ $$? == 52 ]]; then echo 0; else echo 1; fi
      interval: 30s
      timeout: 10s
      retries: 5

  es02:
    image: docker.elastic.co/elasticsearch/elasticsearch:\${VERSION}
    container_name: es02
    environment:
      - node.name=es02
      - cluster.name=\${CLUSTER_NAME}
      - discovery.seed_hosts=es01,es03
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - xpack.license.self_generated.type=trial
      - xpack.security.enabled=true
      - xpack.security.http.ssl.enabled=true
      - xpack.security.http.ssl.key=$CERTS_DIR/es02/es02.key
      - xpack.security.http.ssl.certificate_authorities=$CERTS_DIR/ca/ca.crt
      - xpack.security.http.ssl.certificate=$CERTS_DIR/es02/es02.crt
      - xpack.security.transport.ssl.enabled=true
      - xpack.security.transport.ssl.verification_mode=certificate
      - xpack.security.transport.ssl.certificate_authorities=$CERTS_DIR/ca/ca.crt
      - xpack.security.transport.ssl.certificate=$CERTS_DIR/es02/es02.crt
      - xpack.security.transport.ssl.key=$CERTS_DIR/es02/es02.key
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data02:/usr/share/elasticsearch/data
      - certs:\${CERTS_DIR}
    networks:
      - \${NETWORK}

  es03:
    image: docker.elastic.co/elasticsearch/elasticsearch:\${VERSION}
    container_name: es03
    environment:
      - node.name=es03
      - cluster.name=\${CLUSTER_NAME}
      - discovery.seed_hosts=es01,es02
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - xpack.license.self_generated.type=trial
      - xpack.security.enabled=true
      - xpack.security.http.ssl.enabled=true
      - xpack.security.http.ssl.key=$CERTS_DIR/es03/es03.key
      - xpack.security.http.ssl.certificate_authorities=$CERTS_DIR/ca/ca.crt
      - xpack.security.http.ssl.certificate=$CERTS_DIR/es03/es03.crt
      - xpack.security.transport.ssl.enabled=true
      - xpack.security.transport.ssl.verification_mode=certificate
      - xpack.security.transport.ssl.certificate_authorities=$CERTS_DIR/ca/ca.crt
      - xpack.security.transport.ssl.certificate=$CERTS_DIR/es03/es03.crt
      - xpack.security.transport.ssl.key=$CERTS_DIR/es03/es03.key
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data03:/usr/share/elasticsearch/data
      - certs:\${CERTS_DIR}
    networks:
      - \${NETWORK}
      
  kib01:
    image: docker.elastic.co/kibana/kibana:\${VERSION}
    container_name: kib01
    depends_on: {"es01": {"condition": "service_healthy"}}
    ports:
      - 5601:5601
    environment:
      SERVERNAME: localhost
      ELASTICSEARCH_URL: https://es01:9200
      ELASTICSEARCH_HOSTS: https://es01:9200
      ELASTICSEARCH_USERNAME: kibana_system
      ELASTICSEARCH_PASSWORD: CHANGEME
      ELASTICSEARCH_SSL_CERTIFICATEAUTHORITIES: $CERTS_DIR/ca/ca.crt
      SERVER_SSL_ENABLED: "true"
      SERVER_SSL_KEY: $CERTS_DIR/kib01/kib01.key
      SERVER_SSL_CERTIFICATE: $CERTS_DIR/kib01/kib01.crt
    volumes:
      - certs:\${CERTS_DIR}
    networks:
      - \${NETWORK}
volumes:
  data01:
    driver: local
  data02:
    driver: local
  data03:
    driver: local
  certs:
    driver: local

networks:
  \${NETWORK}:
    driver: bridge
END
```

Una vez creados los ficheros, para su ejecución ejecutamos las siguientes comandas por este orden:

1. Ejecutamos el docker-compose, con el up lo levantamos y con la opción -d le ejecutamos en segundo plano, y después con la comanda **curl** vemos que los nodos estan funcionando correctamente.

   `$ docker-compose up -d`

   `$ curl -X GET "localhost:9200/_cat/nodes?v&pretty"`

2. Con la comanda docker-compose creamos los certificados para los nodos y kibana

`$ docker-compose -f create-certs.yml run --rm create_certs`

3. Aplicamos los cambios necesarios para que los nodos sean seguros

`$ docker-compose -f elastic-docker-tls.yml up -d`

4. Activamos los usuarios con la comanda de elasticsearch llamada **elasticsearch-setup-passwords** donde nos generara las contraseñas de manera aleatoria con la opción **auto**.

```bash
$ docker exec es01 /bin/bash -c "bin/elasticsearch-setup-passwords \
auto --batch --url https://es01:9200"
```

En caso de que nosotros queramos una contraseña en concreto cambiamos la opción anterior por la opción **interactive**

```bash
$ docker exec es01 /bin/bash -c "bin/elasticsearch-setup-passwords \
interactive --batch --url https://es01:9200"
```

5. Una vez activados, cambiamos la contraseña que hemos configurado primeramente por la que hemos configurado anteriormente con elasticsearch. En caso de que sea generada aleatoriamente o puesta por nosotros, la ponemos en el campo llamado **CONTRASEÑA ADQUIRIDA**

`$ sed -i 's/ELASTICSEARCH_PASSWORD: CHANGEME/ELASTICSEARCH_PASSWORD: <CONTRASEÑA_ADQUIRIDA>/g' "elastic-docker-tls.yml"`

6. Finalmente paramos Elastic Stack y volvemos a iniciar el fichero de la seguridad de Elastic Stack

`$ docker-compose stop | docker-compose -f elastic-docker-tls.yml up -d`

Poniendo el siguiente enlace entramos en Kibana: https://localhost:5601

#### 5.9.1. Errores

En caso de que nos salte este error es porque la memoria virtual de nuestro equipo es demasiado pequeña. Elasticsearch usa un directorio [`mmapfs`](https://www.elastic.co/guide/en/elasticsearch/reference/current/index-modules-store.html#mmapfs) por defecto para almacenar sus índices. Es probable que los límites predeterminados del sistema operativo en el recuento de mmap sean demasiado bajos, lo que puede resultar en excepciones de memoria insuficiente. Para ello, podemos ejecutar dos comandas:

	1. Temporal --> `sudo bash -c 'echo "262144" > /proc/sys/vm/max_map_count'` # Este modifica el fichero max_map_count
	2. Definitiva --> `sysctl -w vm.max_map_count=262144` # Este lo modifica en el fichero /etc/sysctl.conf

## 6. Creación de un cluster

Primero explicar que un cluster son varias maquinas funcionando de manera conjunta para un determinado fin. En un cluster se constituye de nodos y el mas comun es el **master** (principales o maestros) y se encarga de gestionar el estado del cluster y ademas se encarga de hacer las tareas mas ligeras (crear indices, etc.). Otro tipo de nodos son de **data**, que son aquellos que tienen la capacidad de almacenar sharts y replicas (documentos, datos, etc.); El **ingest/client** lo que permite es definir pipelines para pre-procesar la información que llega a Elasticsearch; El coord(inación) es todos aquellos nodos que se les deshabilita la opción de ser maestros, la opcion de almacenar datos y la opcion de labores de **ingest/client**; Y un ultimo nodo seria el tribe, que su función es coordinar busquedas entre diferentes clusters de elasticsearch.

![image-20210219112404070](C:\Users\cosmin.bora\AppData\Roaming\Typora\typora-user-images\image-20210219112404070.png)

Para la creación de un cluster de dos nodos, hay que cambiar y añadir algunas opciones en la configuración de elasticsearch. Supongamos que tenemos dos nodos, la inicial (master) tiene la IP 10.100.10.3 y el segundo nodo tiene la IP 10.100.10.3. Entonces su configuración seria la siguiente:

1. **Para el primer nodo**

```bash
~/elasticsearch/config$ cp elasticsearch.yml elasticsearch.yml.back && cat << END > elasticsearch.yml
# ---------------------------------- Cluster -----------------------------------
cluster.name: Elastic-Cluster
# ------------------------------------ Node ------------------------------------
node.name: node-1
# ---------------------------------- Network -----------------------------------
network.host: ["localhost","10.100.10.3"]
# --------------------------------- Discovery ----------------------------------
discovery.seed_hosts: ["10.100.10.3", "10.100.10.4"]
cluster.initial_master_nodes: ["10.100.10.3", "10.100.10.4"]
# ----------------------- X-Pack Security --------------------------------------
# En caso de hacer Elasticsearch seguro (HTTPS/SSL/TLS) Apartado 5.7. Modo seguro: HTTPS con SSL/TLS
xpack.security.enabled: true
xpack.security.transport.ssl.enabled: true
xpack.security.transport.ssl.verification_mode: certificate
xpack.security.transport.ssl.keystore.path: elastic-certificates.p12
xpack.security.transport.ssl.truststore.path: elastic-certificates.p12
xpack.security.http.ssl.enabled: true
xpack.security.http.ssl.keystore.path: "http.p12"
END
```

Lo que hacemos aqui es: nos hacemos una copia del fichero original en caso de seguridad y después en la configuración de elasticsearch (elasticsearch.yml): en **cluster.name** indicamos el nombre del cluster al que va a pertenecer; en **node.name** indicamos el nombre de este nodo, es decir, como se va a llamar; en **network.host** indicamos las redes/IPs que queramos que pertenezcan a este nodo; en **discovery.seed_hosts** indicamos que hosts, en este caso se indican con IPs y en caso de tener un servidor DNS se le asigna el FQDN (Fully Qualified Domain Name); Y finalmente en **cluster.initial_master_nodes** indicamos los nodos que va a pertenecer el cluster y también se ponen las IPs. En el apartado de **X-Pack Security** indicamos toda la parte de seguridad;

En caso de filebeat o cualquier componente, para que funcione con un cluster, en el primer nodo, el principal, seria lo siguiente:

```bash
#====================== Kibana ===================================
host: "localhost:5601"
# En caso de hacerlo seguro, configurar lo siguiente
host: "https://localhost:5601"
  setup.kibana.ssl.enabled: true
  ssl.certificate_authorities: ["/home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca/ca.crt"]
  ssl.certificate: "/home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca/ca.crt"
  ssl.key: "/home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca/ca.key"
  ssl.verification_mode: none
#---------------------- Elasticsearch Output ---------------------
output.elasticsearch:
  hosts: ["10.100.10.3:9200"]
# En caso de hacerlo seguro, configurar lo siguiente
output.elasticsearch:
  hosts: ["10.100.10.3:9200"]
  protocol: https
  username: "elastic"
  password: "elastic"
  ssl.verification_mode: none
```

2. **Para el segundo nodo**

En la configuración de elasticsearch para el segundo nodo seria la siguiente:

```bash
~/elasticsearch/config$ cp elasticsearch.yml elasticsearch.yml.back && cat << END > elasticsearch.yml
# ---------------------------------- Cluster -----------------------------------
cluster.name: Elastic-Cluster
# ------------------------------------ Node ------------------------------------
node.name: node-2
# ---------------------------------- Network -----------------------------------
network.host: ["localhost","10.100.10.4"]
# --------------------------------- Discovery ----------------------------------
discovery.seed_hosts: ["10.100.10.3", "10.100.10.4"]
cluster.initial_master_nodes: ["10.100.10.3", "10.100.10.4"]
# ----------------------- X-Pack Security --------------------------------------
# En caso de hacer Elasticsearch seguro (HTTPS/SSL/TLS) Apartado 5.7. Modo seguro: HTTPS con SSL/TLS
xpack.security.enabled: true
xpack.security.transport.ssl.enabled: true
xpack.security.transport.ssl.verification_mode: certificate
xpack.security.transport.ssl.keystore.path: elastic-certificates.p12
xpack.security.transport.ssl.truststore.path: elastic-certificates.p12
xpack.security.http.ssl.enabled: true
xpack.security.http.ssl.keystore.path: "http.p12"
END
```

En caso de filebeat o cualquier componente, para que funcione con un cluster, en el segundo nodo, seria lo siguiente:

```bash
~/filebeat/config$ cp filebeat.yml filebeat.yml.back && cat << END > filebeat.yml
#====================== Kibana ===================================
host: "10.100.10.3:5601"
# En caso de hacerlo seguro, configurar lo siguiente
host: "https://10.100.10.3:5601"
  setup.kibana.ssl.enabled: true
  ssl.certificate_authorities: ["/home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca.crt"]
  ssl.certificate: "/home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca.crt"
  ssl.key: "/home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca.key"
  ssl.verification_mode: none
#---------------------- Elasticsearch Output ---------------------
output.elasticsearch:
  hosts: ["10.100.10.4:9200"]
# En caso de hacerlo seguro, configurar lo siguiente
output.elasticsearch:
  hosts: ["10.100.10.4:9200"]
  protocol: https
  username: "elastic"
  password: "elastic"
  ssl.verification_mode: none
```

Y finalmente para la configuración de kibana, en el primer nodo, la configuración seria la siguiente:

```bash
~/kibana/config$ cp kibana.yml kibana.yml.back && cat << END > kibana.yml
server.host: "0.0.0.0" (Probar sin esta configuracion)
elasticsearch.hosts: ["http://10.100.10.3:9200","http://10.100.10.4:9200"]

# En caso de hacerlo seguro
server.host: "0.0.0.0" (Probar sin esta configuracion)
elasticsearch.hosts: ["https://10.100.10.3:9200","https://10.100.10.4:9200"]
elasticsearch.username: "elastic"
elasticsearch.password: "elastic"
server.ssl.enabled: true
server.ssl.certificate: /home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca/ca.crt
server.ssl.key: /home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca/ca.key
elasticsearch.ssl.certificateAuthorities: [ "/home/server/Elastic_Stack/kibana-7.10.2-linux-x86_64/config/ca/ca.crt" ]
elasticsearch.ssl.verificationMode: none
```

Mas info en: https://www.elastic.co/guide/en/elasticsearch/reference/current/important-settings.html#heap-size-settings

## 7. Generación de reglas

Para crear una regla, lo unico que hemos de añadir al fichero de configuración de kibana, que es kibana.yml, es lo siguiente:

```bash
~/kibana/config$ cat << END >> kibana.yml
xpack.encryptedSavedObjects.encryptionKey: "1234QWerTYuiOPasDFghJKlzXCvbNM56"
END
```

Y con ello podremos acceder. Para acceder, nos vamos a la parte de **Security** --> **Deteccions **--> **Manage rules** y tendremos a la vista todas las reglas posibles.

Mas info: https://www.elastic.co/guide/en/kibana/7.x/alert-action-settings-kb.html

## 8. Posibles vulnerabilidades de Elastic Stack

https://book.hacktricks.xyz/pentesting/9200-pentesting-elasticsearch#basic-information

https://subscription.packtpub.com/book/networking_and_servers/9781787121829/5/ch05lvl1sec65/elasticsearch-exploit

https://www.largnet.ca/largblog/lets-hack-into-an-elk-server

https://medium.com/@bromiley/exploiting-elasticsearch-c83825708ce1

https://www.rapid7.com/db/modules/exploit/multi/elasticsearch/search_groovy_script/

https://book.hacktricks.xyz/pentesting/pentesting-network/nmap-summary-esp

https://core.ac.uk/download/pdf/250406391.pdf

https://www.elastic.co/es/blog/using-nmap-logstash-to-gain-insight-into-your-network

http://polux.unipiloto.edu.co:8080/00004741.pdf

https://github.com/elastic/detection-rules

https://qbox.io/blog/how-to-index-nmap-port-scan-results-into-elasticsearch

https://sigma.socprime.com/#!/

https://www.elastic.co/es/blog/elastic-security-opens-public-detection-rules-repo

https://www.elastic.co/es/blog/no-experience-required-ransomware-2017-and-beyond

### 8.1. Detección de Nmap

Un ejemplo seria Nmap. La función de Nmap es saber que puertos estan abiertos, si son vulnerables, vulnerabilidades del equipo, servicios activos, etc. Ejecutamos una comanda que consiste en saber la version de los servicios activos, detectar si tiene vulnerablildades, saber el sistema operativo, no aplicamos DNS y generamos una salida de fichero llamado nmapscan que nos muestre lo que ha recolectado.

`nmap -sV -sC -O -n -oA nmapscan <IP>`

Para verlo podemos ir a la parte de **Discover** y filtrar por IP, **source.ip: <IP_HACKER>** o por protocolo http, **event.dataset: "http"**.

Otra forma de verlo es en la parte del **SIEM**, **Deteccions** y nos mostrara un poco mas especifico sobre el acto.

## 9. SIEM

Elastic Stack incluye una opción llamada SIEM o Gestión de Eventos e Información de Seguridad (Security Information and Event Management) es un conjunto de herramientas que nos permite monitorizar (redes, puertos, IPs, servicios, etc.), hacer búsquedas de amenazas, y muchas más cosas. Normalmente ya viene instalado a partir de las versiones 7.6.X pero siempre es recomendable tener la maxima version ya que van mejorando y van añadiendo modulos, interfaces, etc.

Dentro de este SIEM tenemos diferentes apartados:



# 1. TheHive Project

Es una solución 4 en 1 plataforma que da respuesta a incidentes de seguridad alias Sirpa. Es OpenSorce y gratis (GPL). Es escalable (se puede integrar con otras soluciones como The Mispá, The Cortex.

Está enfocada para mejorar la vida del zocos, CERTs (equipo de respuestas a emergencias informáticas en un centro de operaciones de seguridad; una especie de central de alarmas en materia de ciberseguridad.), CSIRT ... -> profesionales de ciberseguridad

Nos ayuda a organizar cuando iniciamos el análisis de un incidente de seguridad.

### 1.1 Comunidad

Antes usan Slack pero historial de búsquedas limitado, después Keybase (plataforma de chat interna diaria en uso). Actualmente la comunidad se encuentra en servidor de Discord.

## 2. TheHive

- Es una muy buena herramienta para poder tener una respuesta frente a las amenazas que detecten los analizadores que tengamos con TheHive. (Cortex i MISP) En el SIEMonster podremos encontrarnos que se integra con Cortex, MISP, OpenCTI y PatrOwl.

## 3. Cortex

- La función de Cortex es analizar y hacer la función de análisis forense de los datos que le lleguen de TheHive pero de forma digital. Puede responder activamente frente amenazas e interactuar con los "Responders" que tiene implementado Cortex. 

## 4. MISP

- MISP es una plataforma de amenazas para que empresas y entidades puedan almacenar y correlacionar indicadores de ataques dirigidos para que posteriormente MISP pueda usar ese almacenamiento y compararlos con los datos recibidos por ejemplo de TheHive y analizarlos.  Puede utilizar los IoC y la información para detectar y prevenir ataques, como fraudes o amenazas contra organizaciones. 

  #### **RESUMEN**

  *TheHive, Cortex y MISP son tres productos de código abierto y gratuitos que pueden ayudarnos a combatir las amenazas y mantener a raya a los "malos".*
  *TheHive, como SIRP, nos permite investigar incidentes de seguridad de forma rápida y colaborativa. Varios analistas pueden trabajar simultáneamente en tareas y casos. Si bien los casos se pueden crear desde cero, TheHive puede recibir alertas de diferentes fuentes gracias a los alimentadores de alertas que consumen eventos de seguridad generados por múltiples fuentes y los alimentan TheHive utilizando la biblioteca TheHive4py mencionada. TheHive también se puede sincronizar con una o varias instancias MISP para recibir eventos nuevos y actualizados que aparecerán en el panel de alertas con todas las otras alertas generadas por otras fuentes. Posteriormente, los analistas pueden obtener una vista previa de las nuevas alertas para decidir si se debe actuar o no. Si es así, se pueden transformar en casos de investigación utilizando plantillas.*
  *Para analizar los observables recopilados de una investigación y / o importados de un evento MISP, TheHive puede confiar en uno o varios motores de análisis Cortex.* 

  *Cortex es otro producto independiente, el único propósito es permitirnos analizar observables a escala gracias a su gran cantidad de analizadores, módulos de expansión MISPy cualquier analizador desarrollado. Cortex tiene una API REST que se puede utilizar para potenciar otros productos de seguridad, como software de "análisis", SIRPalternativo o MISP.*
  *La popular plataforma de uso compartido de amenazas, puede de hecho enriquecer los atributos gracias a Cortex, ya que tiene una integración nativa con él. Para que como ya hemos visto, la colaboración es clave en ciberseguridad.*

  ### Función esquematizada:

  ![img](https://lh5.googleusercontent.com/Fk95t8Rc0IcEyoCa6Lc4Bwh4sYUfYGkmmBGNz99HkZ2sqaEtV_c6mzTb_XblaxsMB8_PUnO258oH408TbkgTCS0UpD_5Frq-CyKkN1WuVyum0ESFlE0iCqB3VPOpIhIcFLUkIAby)



Test amb VirtualMachine 4.0

Importació del entorn de proves:

Descripció OVA

La OVA - té el sigüent software:

OS Ubuntu 20.0

4JRE 8

TheHive 4.0.0

Base de dades BerkeleyDB

Cortex 3.0.

Elasticsearch 6.

TheHive4py

Cortex4py 2.0.

CortexAnalyzer

Docker
Enllaç de la documentacióhttps://github.com/TheHive-Project/TheHiveDocs/blob/master/training-material.md Enllaç de la OVAhttps://download.thehive-project.org/thehive-training-4.0.ova **hash SHA256** de la OVA: *530639b1c4793216ed025063dc79806607884be00e8a1bcd6fc643751d84e7ed*ImportacióUn cop descarregat el fitxer es comprova la **Integritat de el fitxer** amb el hash.Al **Windows** s'obriria el **PowerShell** i executem:Get-FileHash .\thehive-training-4.0.ova -Algorithm SHA256(donde pone *.\thehive-training-4.0.ova,* ponemos la ruta i el nombre del archivo)![img](https://lh5.googleusercontent.com/88DAysmIKp5QuvQqoVhnNuTVy_m1QlVSGci-k948jxWwkaiBD5q_FSzoEhlA9bzG4EJCX_HhiD_fJ860qy50I4HJILjGjpWiY34htkpKQ9HnihLA2N_zFgeKEF6-xtgGp0Sg_q1Q)A **Linux** s'obriria el terminal executant la següent comanda:sha256sum -c (fichero)
**Importació de l'OVA** (en aquest cas serà en un VirtualBox)Un cop el virtualbox arrencat li donem arxiu on sortirà un desplegable i seleccionem importar servei virtualitzat.![img](https://lh5.googleusercontent.com/1vbqbI7w_gbC83ofCObKpoVfoYjZc0yghfnujtweJ8fTul3D9g1hNuHT1aSs2P5E0jJEPgDTRnVtId2cRdQtfb9V-v7PYtuLc7VmEd5Z2SdPRf_OeJk5XoVfPaseQTTSuaH8XWHh)

Ens sortirà la següent pantalla.![img](https://lh5.googleusercontent.com/_7dgECcagQrXZOmQyMLSPCG8SeReDqaxznwZ0UDyH6ukxzk9Sx98FAXwkUPCdJ-x2dBf-1DlRt8myfdqfxJnnS-TnS_f5KF81sQQeEXQVuFCk5aMljPlaB2XGOv0omiDNpFAPb0k)Li donem a el “**logotip**” de la carpeta per seleccionar el fitxer.![img](https://lh3.googleusercontent.com/TQwBYf3ZjgXEKQ06fEgiR3-GPdHCIBw27hfUogtaETedb7UC8Gjgo0Mptfb6_KZx38o_eBgbewriP6gmqVO4JWAHaYN2Pv7RlWjrJswMyjHUt_glDSu_EqHTRZ0oF1DGPIUZzLpk)Li donem a “**Següent”**:Ens apareixerà la següent pantalla amb informació de la configuració de la màquina virtual:![img](https://lh4.googleusercontent.com/6nrJoQ4xqsAQSFeOge_03oOAvxhQ31JZcWj-tIN_d2oFqkltVdQhDOxe8vW1pYdgYWMThUrZ6x-PLLUDtMZMJcFcIfWxESiKpzHMk9rsLf2prK9vbK4To9oSL2M62obex3hlS2PP)
Li donem a importar i tindrem disponible la màquina virtual de TheHive Project.Redirecció de ports per a l'accés a TheHiveRevisant la documentació veiem que per accedir a TheHive es fa via HTTPperò la màquina està en NAT, el que significa que hem de fer una redirecció de ports.És igual si la màquina està apagada o encesa (com és el meu cas). S'ha d'anar a Configuració de la màquina virtual.


En cas d'una màquina encesa accedirem a la pestanya superior de la virtualització on posa Màquina, després a Configuració.

 ![img](https://lh4.googleusercontent.com/h_L-3SuUj6IjAldS4ozJJhMgiEd7VQrnNeNKNMcHFGoJHuUpaVA5UMEMTx8z3VEsc99g8iGVHl5eTGM7o4x99xgyYC1i1lEpDLFuyqjta0Q4f_30l6JvlFvoGD8Mtd1F51GAkC6v)
En cas de la màquina apagada o des del menú de virtualbox clic dret a el nom de la màquina i configuració.![img](https://lh6.googleusercontent.com/-bOBz0BWwYpvUYCsf3feRvTsXhVoerXxCiCi2_9oq7R1lLmw554AwPqbOMFJTPgPy37Fab6INo5BwZuE6ghtIW_7ojgiU15hdnPCD8TsbgAZ9rzmvrisV8Ck1bLAZDXZIqbiO4WM)
Ens apareixerà una nova finestra on anirem a xarxes, donem a Avançades i a el botó de reenviament de ports.

![img](https://lh5.googleusercontent.com/DjYi7NUr617517PiW_2Ruvy-BHVNs5qSQfgpg2GBXrtFAUlqce1U-MZ6piHfWnPoLDQ4mnTuYACuYAiI2tir_zIgnLa4xSeVwgAPQbXvhPp03yS5CYK_5UQjpCaPjLSLOaShGNak)

Ens apareixerà la següent finestra, on ja està configurat el reenviament de ports per a connexió SSH a la màquina, per accedir a la màquina via ssh es farà **ssh thehive@localhost:2222**. La contrasenya és “**thehive1234****”.**![img](https://lh6.googleusercontent.com/xKhNMmRLNAUqVCnNDicrcZp4xi7Fvesf9g97PxP9-rHxveg2DoLI57ZnUGXJs1rQZUsDdK63Llj1P3bIKUx5bXDjJZ1GeNYuR0TYeEJeUhFac4k8BSe3NfpCoI4rR0USwxodJF1t)

Per afegir una nova regla se li dóna a el botó amb el símbol "+" de color verd.Cal omplir els camps:**Nom**: ha de ser identificatiu, per saber perquè es fa**Protocol**: en aquest cas el deixarem per defecte, però podem indicar-li el protocol concret**IP** **amfitrió**: La ip d'una màquina física, real, en aquest cas li donem la 127.0.0.1 (localhost), no posar IP li estem indicant que qualsevol equip pot fer connexió**Port d'amfitri**ó: el port on la màquina real es posarà a l'escolta.**IP convidat**: aquí indiquem la IP de la màquina virtual, no posar la IP diem que qualsevol IP que tingui la màquina és vàlida.**Port de Convidat**: Indiquem el port on la màquina ha d'escoltar o tingui un servei actiu.
Amb aquesta informació podem fer les redireccions de:**TheHive**: *http://(ip):9000* → un cop aplicada la regla la petició serà http: // localhost: 9000**Cortex**: *http://(ip:9001* → un cop aplicada la regla la petició serà http: // localhost: 9001
![img](https://lh3.googleusercontent.com/MtbRuHCv0MjoJv0h6E6xxU0iQ8SWzxqgLiOkEens8Lym_40xJrwnhzONFaGVkvk3JpOrrhfj_TKFEZCkFQink3tMzmcIOgjZ4clmullg3iinuOHUFhugeHWcPB5q9qIVLjyQa1Ve)**Credenciales:**

|         | Usuario       | Contraseña  |
| ------- | ------------- | ----------- |
| SSH     | thehive       | thehive1234 |
| TheHive | admin         | secret      |
| Cortex  | thehive/admin | thehive1234 |

Prueba:![img](https://lh4.googleusercontent.com/PdOj0X3uVdxBX3FsulN6ZEYJss5jxkIZPS_9vAzNPk6OHOPBUel3m_IrTkKYTTKgdzeTzpUlQ59RB8PkQG5jvhYz6c98qKLf6FIbWQOGgLxwBm1HAVWsSq3-7229x7hfhNwwHmCh)

## Patrowl

- Es una plataforma para organizar operaciones de seguridad como vulnerabilidades, revisión de código, verificaciones de cumplimientos, amenazas u operaciones de caza o inteligencia.
- PatrOwl lo usaremos para que esté integrado con Cortex y TheHive. 

## Snort
- Snort no esta dentro de SIEMonster dado que se han decantado más por Suricata.
- En nuestro caso ese será nuestro objetivo, hacer que Snort sea nuestro IDS (sistema de detección de intrusos) con el que vamos a recoger las alertas de que han intentado entrar en nuestra network por algunas de las vias que tenemos bloqueadas o no queremos que estén activas. 

![img](https://manuelfrancoblog.files.wordpress.com/2017/10/snorttm.png?w=640)

- Estos datos obtenidos los integraremos a Kibana para verlos de forma grafica y más sencillo para analizar y pasarlos a TheHive para que con los dos analizadores (Cortex y MISP) puedan analizar si realmente es una amenaza o una falsa alarma.

<img src="https://ciberseguridad.blog/content/images/2018/09/TheHive_Cortex_MISP.jpg" style="width: 700px;"/>

## Instalación y configuración

### Proxmox HA

![img](https://lh6.googleusercontent.com/XVb4ieD6ZAzXx01Ka8an_MbEiNbveFD20rMYL7xspfeyNFrjW7HoBIQZnyMMdzQQq0b-n8bBakeedqvWUHYwTk4tncYhq4pGmTkmbZlD0ilH3u_xz2LAq1n-pR2j9R4TLiL9JPog)

### Creación máquinas **Proxmox**:

![img](https://lh5.googleusercontent.com/qbe4EJcEx-JOpUIBEczxRlOE7ZvHjhlrzxiou5t7XmDv4S_2ey0fotrWOtwdN5L9DJjEa79n9NB1p1VbyZRnxbs-YbW0clO6YTV277MR2TKheDTTrJnsdMuELotmnLAA3MaOFCO2)

Tenemos nuestros tres **nodos** arrancando y procedemos a instalar, hay que seguir esta sucesión de capturas:**![img](https://lh4.googleusercontent.com/6inqGgPZbs0-pONwyf2zViqLqtzIZRzFUJnqEriv7DgRhWrqXG6M6HGEEBW_9uka7EOa-oOe73Jpq6WGkilb1KGNwD0umPq517ClMoxOJzf4sW_nf6XS0Ulbu9vT4ekm9yH6e9LY)**

#### **![img](https://lh6.googleusercontent.com/ZIWCfQLBdlLA5rQzlaLJqw6WkNUAtoBz_x9iH3OR4pPsU4fDOZomhu_PTleycPSG1uqvlxR7BcgMQBd5naKpQ53CyNqr-QhjQWPqc7sVfO2g1JgKex0NcW38GUncTYY50lkd6Uu0)****![img](https://lh4.googleusercontent.com/RjNA0ktvEBr2-b9qW-4nC6La1thJpTYbang74W7eL8TcLdRN3qTuIYt0OukHiuvS41diPNZYiO8D8Ecd5o3jYLmkw6jLj_37abyBQGKSRfpd_TRWVadXiTK6y6s9gh-1gLV0gq8C)![img](https://lh5.googleusercontent.com/AbORke6K3pnAWs-animtBCvM5q4Obx5dPvNH3S2jwqexWuiwYkiRpnjUpkivlsCSO7Au4t7jN24Z9ZbZVm4UuJd2wsxojd-B9TUrI9QcKYVrzaqUK9RN23K0pm8xuvadPhn315DQ)![img](https://lh6.googleusercontent.com/CQmZBw0qpGKgKiAGYxy58218MkcBt94PigNS-0Qw-6F8mzZEt-Qqz5WgFDwiJ5smTBB3yeRzUEojqGcxUDwDHZRDC8FHGikYf_IaWMyQZNB1IpRfrI8AKtHuFFpLpTWtW2B_CLEo)En este apartado se escojen los valores de red en cada nodo:

**![img](https://lh5.googleusercontent.com/NtNO_JdDLqruqK0o_g2iKjlDiP8rqtHmrQAEEaqCnBXZ39PDLTRux7f86HT5VwYFutbr4aubK2tYR-vbuhtuL1b-FHy-4-5uUW4Ti4zjT2ePMIhYoZzEO1NW24DmukGNk2T-BqpH)**![img](https://lh5.googleusercontent.com/UDG-f6eKaUXNi3ZRQ-MD0xkKVc5ygRbUPytv01U7-EKBjt0wcqBFVgpaDbwdA0gBYQ45rL3ToWC0yg835DZUZVJpXHe3qyJH4xtKcTiCv2GJPqEOojCFzA0ezFnQmz71LH2hG0Lq)![img](https://lh4.googleusercontent.com/X7bU-RTGNF_xRVzGMkjkSH5SM5KgSn2ufeTLlYdqSyWaM7ASSL7yrpijl7Af0QT5EWlIEQSPShw_i41xsiW66mXE9ktjJIDGdyt6B-EYvuPoT8IC2CNgxB5lRo8YcDmTJwOdei11)![img](https://lh6.googleusercontent.com/WYdcfmXT6oH4NqTZRsc-s4zzOXJ9WuLdLbmExb2VB9S4IPbfWn8feWh3fN0XdEhKDz43Q8zjl0YyB3gg6UnOqS40bh6Ugoka_6KTlM_eZ_Ol4nLrhYvvCxiaVMP8Serq8XNRKWnB)![img](https://lh3.googleusercontent.com/DbogIFKgbJmBQWcOtg3-TVEwf_hu_chi5u703VGQVAccReKdjLFY48NqsCnEliNZrwpkXNUaRcFpBpsLr6DinYOOmlpAbEWsOP36iBJK2zZqAAUJOJkf_-1C5-rFQfx8CJ8KOfNh)![img](https://lh3.googleusercontent.com/YaTj4kSbJkYlWey2toP8CEv3wSt6BEoSNGDhptlTbC16BWBStPNm-aVrKRmUffyz3gTlLB9tKmaIxhDWRBGydHQ9E83FbWY3Ds4HlDIktmN99TQ8r2TxZRFNM3jiA0DJpSUCmTJ3)**
**![img](https://lh5.googleusercontent.com/9XuLsoi95Cwnmazpw25v-ve2U_OKRK6JCfpbOc859j4y3ZJ9IH3dgpg4zET1wJsWagcZA1fPJ2PmWGHGkhLrPNO4p5Mp5IbZcx9dLT7waJ__xAvddUNjoI-x-3fkVXk_yk8zKmvg)**

![img](https://lh5.googleusercontent.com/bXWjvLKZWyLFGVlehWSh6bdShbBWkAo1SUC0R8g4DJwWbS7HsHhddSLZo0srMsa_vidcI8bR-3a95S0SrlmqlYkoDPmRdqD5y-oqozLEXPgkJDRa4pTdwF382xK_hgbQccVxLBYr)![img](https://lh6.googleusercontent.com/Levqr8E7yQEViAaXkjHzLZK_VB_erdoGKYRcOX_yg1cqHMO7b6cHvGwTA3S_DPjfK1EKKtIgT-5HjXwQvenl74iCWgj3CH6YGjQxtY9uDMTLQiiXXF9iY86MJ3hWRLoAlaqP2NGT)![img](https://lh6.googleusercontent.com/P6jle_HQ3h4fnNgSmcBfarsLz7lpPNVOZMaE85QCDm2UReIMFIhlTwug_TvUIedWBjAxKsKT8unJgecDP83ZTXxSFGibO85roxqA1WKPdvphpmMk4M-52o8DHe3Q-8_kU2WYHDfR)Ens anem a “Network” i escollim la segona targeta de xarxa que está vinculada a enp0s3.

**![img](https://lh4.googleusercontent.com/cboRw0LOyX14q5J2IOvq3gNVFtRbdB-skqUdNggh0tR5ypyShwZWcRcwIt2k15UCoCGkZNpecAH9gBgA_NYZK6sVko9Yjtentw0x6ZcO0D3R40ygMldUD9RS8ZfK9R5bnz2-FRd5)**Posem la IP i el seu CIDR. Lo que és una interfície física ho connectarem en el mateix segment de xarxa. Si tenim per exemple una VLAN en el nostre switch ho fem perquè es connectin per veure en el segment de xarxa 10.10.10.200***

***![img](https://lh3.googleusercontent.com/C6H5kB2VCdj-VInKit5uxfJkp-MAvXM2QIAFv1WXJroOnWwgvb453WBLri7ZKKloYycaKZd-DBgVlhRUmvL5oDj8m3siC9sKLeyVrivyGZl6RB8eeGRRHs2x2zRBFVGXecXPGL0V)***

***Ens quedaría així.![img](https://lh6.googleusercontent.com/aDn9kXvaFjBknD1NR3-XnkPBkwkQzFZmBT6c8EOWWR5t9ysft_u6BI2ZHDf2Y6kQENHCjixeQEQSeWpGMY7y2VWvpihD_i5j6p8xO1kB-sCT9zMiEHFBEpsiVK2Pyi1-IB0-RQOJ)Fem lo mateix pel node2:![img](https://lh6.googleusercontent.com/IjjgAm9xGEGHHrlVB6vHwCRaTDiAipb2BfwlbpEqtH0lvlqEsaJs627KRg6DzErfgbEn6-nOE-DjR-alejDsXRaK0ciYNlJQ-zrxh-ySpEH2Ajcife0tWQSJl-dbqjgIicZ6DAwR)***

***I pel node3:![img](https://lh3.googleusercontent.com/muc0rjIp6jJnt1igDYYCx86HFJp-4I0n8XX2Mptk2Je2xQLdepHB2cztaux5XnSr9QEa4z841yxML_xT7skzvsCk7wvn-VW5L2sBMP9mdXE43xw0_8X3o7ADkxpyuB4Ldpkext_N)Terminem de confiurar la part de enp0s9 (producció).![img](https://lh5.googleusercontent.com/vulhWXVmvMdHdXQGFwWLhopKs0Fsbb3Zeq9olwVY7tNVZSjClnMg7f-MkHwRsz-KDCpygiqhblHE76oNe9GPgBE2I7nmvM5cRl8LAXdI4LNCHiT9joWpdjFAkBJDyfi8mc2gS5Oq)Reiniciem tots els nodes a “Reboot”.![img](https://lh4.googleusercontent.com/MDS46JTpDrrKbvG04fZAqbyrkBtyEEOoV6MrdNsHneQ9h1SeuMCLqn76NGsyBWKS8wEl94z13z7jnwX4-I1kW5OuUPiEOeoJz2vp8NFrbzKx_BzmPN1WZtnvthMmqpVBp2Gu1BeP)***

***Ara creem el primer cluster en la secció de “Datacenter” i “Cluster”.**![img](https://lh3.googleusercontent.com/B0iikRkFtZonwHV__7lweToKk30y_3nIAo10qFth5HWmnWbPZlWCC0b6CijbvQmA-qZCa6kkKg41pE8niUiAvje4BQCTbA7e8TZrxDb8CSRBtKJMTV0phgP0ti3oxq_CxVHJadhc)**Com podem apreciar no estàn actives les xarxes.![img](https://lh6.googleusercontent.com/82Zq2BifwFUvubLYZ973Q4ttgp2VuyrqIvnHH_LadZKx0I3uZXjbZasDirz0X-aPh3JWTWcn6Hp1SBoYpZMVMnGf2y0UdoydFIWMYFAwY4-jHsPLHYW1ziF36Gmiqafx-0VnccuC)*

*Hem d’anar al node de nou i a la part de “*Network*” activarl-es en “*Autostart*”.![img](https://lh6.googleusercontent.com/Y7VNKgCSEURZQJFAcbfVeLUY1dmGBPyrziJq4UuMtjw7uh9qIzSoE70kT54E5yFKeHwAgy-oJtrIkuspsT94PpfwoC41xjYJUtnpE5eea5sHd8NRj_w0SMmjrKRnZ-Cspne6Y-x4)*

*Un cop totes estàn en mode “*Autostart*” hem de reiniciar els nodes.![img](https://lh4.googleusercontent.com/8vMc_IsOxpRXc4LdUNznMGF1nnvA2mlTXEkl9f3gCQFVAnoLmaz1AWF_HpiVvjnQ56yAS4mteaAPtiECv5ZFKQHlIcETj4dFBBzF8h1KGRQBcj0FVrqzvINTjB6p1tnG4GblyxoC)

El tema del DNS per sortida a l'exterior i descarregar paquets.![img](https://lh4.googleusercontent.com/1bNB407YFGbu8XCQxdGppd25cLmj55T9m0VPmUPq_-XmCPdK02rPoBKzNcBUaTStWL_JXLL_ZBW5bYef9jz5P4WSg09VJqGicykT0JPueHQWC7zoqRQ51lN6clPczGi-RKLmRIhK)

### Creamos el cluster

Ara sí, anem a crear el cluster:![img](https://lh3.googleusercontent.com/Eox_H2f6_ZyXnWl9x75PmRQagcHTS4w6IDBKcXoxvTF_s1DMhHHM_3JZoOEA1_02oF89ttHe7ANvAl4kVdpwdN2ZK-rxzeTMYmLVfajA-Kb9NhyUQSh9I5eMRw0tfwHdJfUXvEXb)

Ara ja ens sortiran de forma activades.![img](https://lh3.googleusercontent.com/ouRs3x5pKVEqXXIXO5rj22bPYordbIlFN8XDDUyDueoDXF9csCsr34AESkXv-9E3XC6prUDgRy2QSRBD--gLK152hGKDZZpOL5bylYDhYUmbpNNTGjxlXfvydJarN36RGnBe9nS0)

### Unimos nodos

Ens anem a "Join Information” i copiem la informació de unificació.![img](https://lh5.googleusercontent.com/zB38HXQERmbx4T0pBkaY_OaRsOgu72upPGZzSeMbdHVCJ_SKIsiyOoQNF2pIT7qluNMYd77x1gmR449WE9Z3qrVEfhtHv8zETUshhAehfO6BXp-pWwNV_lpyBLXLGb4gkKNj94Wv)Ara en el següent node (.202) ens anem a "Join Cluster”![img](https://lh3.googleusercontent.com/2Slj31Y4fb5fvDN6GdEcUD0NgsjclXSsP8zheTLqhcp4iAaRd0AZo362k_fPf33JD6PPugClsYdgsxU_wdOd63-1JiiWmgprqVvX2PsFSYrNTAMcJ2E2zs1VMU63LWfnGPe_v27V)

Inserim les dades adients:![img](https://lh4.googleusercontent.com/cwfOQICavz7B49Se5RCUg_JM0wO-bK_6AWiEZGfcS6t3EVleih1J1ZAE6VuJG8SLhJwf9-CwsYq_8k6rLugRUuQehcrQkH9b8T8Z_iUV3uZ95B8nT55-KLhjKAQUWfjYNo88ypGI)Les integracions van bé.

![img](https://lh5.googleusercontent.com/bUyjih8UOTsqOQKX3FIXck7Zr-kQFHdp3zNr7j7iIXJaG7XGZiMz7ZUfMRSaQodAwM1UP4TxFkr7EIkF4HWPeoHhbfEqBCTIIzFu6cKYaP9q8rdo7IfMQE7rgSc4-0pKwm1GqwZk)

Reiniciem els nodes perquè s'ens carreguin i ja els tenim.![img](https://lh5.googleusercontent.com/aZR4brGI39D7ymgioOEn_4hIIsZJXlNDbKC6h-3VVAyK9XY1xmLxNKBCLgiM92kysX_bU2GuWz00efnc6qIkIKXLlZ0LaAC_4lqT3jsKm6XCD6Hsc-izSheomDlT_83h98ox503J)

### Instalamos CEPH

Ja tenim els servidors unificats i tenim el cluster.Ara toca creat un CEPH perquè es comparteixi l'enmagatzemament.Ens requerrirà instal·lació per poder continuar.![img](https://lh3.googleusercontent.com/qtSlFI9MOhwxEY8aWrQMZdmSjDZLhnYtltKQPEWlA2AdyCy13_18wAzUds44PxMdMYyI-YHQDwqYg3VV3zqVLtTzo_JfzhrJ0Se_jSzaAvUtBicEZOZWkBClKIbGVPRRw8PpyBOq)Premem "Start”.![img](https://lh6.googleusercontent.com/AU1oXviTcGJ-5fp3WjzAKpuMS9Zekpvs1Wt1jc_wzGYC-LVrZ-rQp4N_T5-KFutJB8uENZK-mwnCmnQXz8jZLBsFyK1wFUctH0BNIN4g2A9fI4n7XSeKW8243LmSd_h8mHDAmN9q)![img](https://lh6.googleusercontent.com/pFmPSj5fJk7OGWxXkYcRXakzwc1cbPmzNl1auIDso5rAP3XaYXhI98Gaa8NJ3rLzW5an7glXBoUULOc090G6E_UotIqCDvaoXcgymrcWnNGt6vxGS9qHyY1UvLAcormAKtqmFWtw)

Ara toca escollir la xarxa d'Administració i no pas la que ens dona ja predeterminada.I en la part de clúster escollim la part de Cluster al nostre disseny de xarxa.![img](https://lh3.googleusercontent.com/eyWgN5mYVJX11uPdJQvk9cDiDyDM1JTrOOQSTU4XCIcipNWBnl4D4rRsKd2xGKn2jSn8v37XNBIN25FuoCxgCBb57jYhUBNq9pA5Hl2IdU2Y_lhLxxJABZRvNy_jT3L9SlWGPejH)

Ens quedaría així.![img](https://lh4.googleusercontent.com/M68cBWNXwFF2xBm1Lr5KOMVfQ6haNcB1EdZBVf8FYvtnFL4naaDoh8hW_tx7o1Uzk4MvkCIxcBcJjWUH7ddSyJvt8PjR7QiyTi1IRU7yFPtqyPxC3of_7vmFQhSNEg2h8Ae5h0Xj)Instal·lació completa.![img](https://lh6.googleusercontent.com/U2H5PnFqIAhXchMfMQwh9KmxKunRiRfx6alLLdJE0RsAe3D4mVx1PNMGfRRXWs98gj0o0fJsiExc6B7TymgGav48bRtg53NpZhnLDr6tteKWHeNt-UxtAoqVxCzVElINePfypMm3)

Caldría instal·lar-ho en els altres nodes restants el **CEPH**. Ara tenim els tres **monitors** creats i es repliquen als nodes restants:![img](https://lh6.googleusercontent.com/Mk1dsZzEOMCbt8XUXvDuqwNvv3y5iqqmfkkMU40m_paDj6XRmupgmxiogzD2vStEtvf6-44o8kG6oMt2QLCtpdLV-qDDxVf94ZDhOKoIfca6DtjcTRnG-XNXmLtjcm404XMYkOuQ)

### Creamos discos compartidos

Ara anem a crear els discos que estaran compartits en el emmagatzematge compartit que va a ser HDD. Anirem al primer servidor i anem a la part de **OSD.**![img](https://lh3.googleusercontent.com/gf9XKf7c9EVpnLSthbt9d21LnkasZo7OZKxX1Eq98mjkYK1U4tWBHpUP_rX4WholOXMsL1AhWkYWwSdpkNmMeNVq2PoozsunaK1rsG_68TN2tub6nTbJfqsoo5ZWO1pBpo_HS_9j)

A continuació, ens diu que hem de fer modificacions en RAID per temes de conflictes.![img](https://lh6.googleusercontent.com/DM_imDLpmoKdeD2C8KMVcGo6NLhFgRNAYK20y_a_9hYaGH2ARCgCkM2_T-TF1tUZqra80I_Q8JfDlYysgRmAsdMT2dsev3D1a_7o1JpIdOx5TSOb2nf7ikzBzTYspSmAB3T9tD5o)![img](https://lh3.googleusercontent.com/KC35SHkoonY6bJiJt1Qatbbu5uIRIHQCGIAgBH_ZoyEKfQASFMeHGlxSQsPDmG8oiPRao4Tr6q4pfjUYhq5lSSbdeBFHMHweLmbj4YZN4m0rgIJ_9_I9-xSrWsRLL-aW_o0sIYXF)

**En el **node2**:![img](https://lh3.googleusercontent.com/fNySB6UEnccW2HgBoT_XG_LqyE0ALYx00Vt5Q-QPj-g41zNpd8k5SlaxX7ryeJ_Bc2qkHhYSRY627cLuGzX-WajlIjgemvTZXV0qU3wjTGbI8v72dHz5Cx_K7uXRngAHnS4D7BNC)![img](https://lh3.googleusercontent.com/K_qLpL0CulZgkupeKwn2ABLOKP_45eZkRkDs8jSTDrYBZXJEQEtqfB5XKddjP-gt9hHPdr-WzzQfh3ZqPkSeD_jst9oab8B45-zZWseKFaC-Bk0Kri5JgZ_AjQGdRByHKtXOMk7g)En el **node3**:![img](https://lh6.googleusercontent.com/5kqZY3aDIwz13trN-jtrjRxblHK_XIobXSfKVoDtACWS1XQ3iAVFrAhkf6L_62GvEACsmOW328iS6LQ1BY7BytaBzhHSmvaDHAkYZKz9hCizFhdZZomb3h64JhGuCEsqAhgbsenG)![img](https://lh3.googleusercontent.com/WPXNg3sUXKGIIqD7tCpvIKHMhmHO40tLy0vXu5auf9eHcF6aDKI45TWQg159YB8Fn6zpYY9SPzEUEXb-UCtomLd3HrsZtKZ5Wg_KKDFOtGZYML08RkzytEeAH9zRwb5CpgCcmSAl)Podem apreciar que els **OSD** han estat ja creats.
![img](https://lh3.googleusercontent.com/llIOCVtI73io3VM213f8KN2gf_HP-uPcHnz24jhgbEVPIyqzHqJ_2XY32Wji-LSPPhWeJRU--FlMQ3mwgdWSeMakSXdxVvlAJxzNBhgU32C6XsQcaaTXq-iXHCWjSinmpy-I8iaf)El **pve2** és el **manager** que controla tot ara i es poden tancar les altres finestres amb els nodes adients.![img](https://lh5.googleusercontent.com/I0Y441IKAvuSovoyQND3ACO2CA11dDP2_QXMzFApei5J-xnYQ6aPMLlqO8pPocxhY65PlAwT4CXMjUDdi62DLvliKc9v5J6lkJRg2JQF31glU3MuUetapHp7qF9C0zRzmhyWAoFd)

### Creamos Pool

Ens anem a l'apartat de **Pools** per l’emmagatzematge.![img](https://lh5.googleusercontent.com/WMZHH94V0PuibgYVRAnti6htz0_z2MoUfTnhIie1L8JpA7qkA0AM32x92F6-ufzufJoLvxPi4SP3Kz_e-8vFBOf1u7LOdUVT88ymfGoqhQZwwifvBGKgxCIG5yQMaoeGcFF56E1c)Assignem 2 servidores mínim en termes de répliques, etc. i 3 servidors.![img](https://lh6.googleusercontent.com/-g80l1Q3dEjyJKAWMUGPkdcucrDXHyJkTBUwa7XKMBRqEVG_5lsQA27zKxVgcRffEMep_1hFP1tw-k6y6m2_XhuXVFFP7Fu2wMpSox61Loh4bHojOaM0TwjSHenvCfIchJJMhR1Z)

Esperem que es termini de crear.

![img](https://lh4.googleusercontent.com/d8jdK3EJ5R1kKZ1vT7XlGWjfM0inAAjDlg0oFSaxXrK50H3Uv9Mn5WpUkERHJMiYGPgU-ctr3gyvOSomKXGSmFS6THJtlpD3a3OE7SwwQV5C1spHRBu70rN3K9e1fg8APNcLpxLG)

Ara ja tenim l'emmagatzematge compartir per aquests servidors creats al cluster.![img](https://lh4.googleusercontent.com/dJ6treSZLiqXEz_DzndaY4D1Qf9R95d1X4eMKyDm7DJF86fRzE561TdG5l0o3ZbHLSyBcYG67csCyFkNOkzZdbaloSU7-X5myS12-q7uOpLFUFabGrxcxrxU9Pfu1MsEgmsGhIVk)Ara anem a crear un grup d'Alta Disponibilitat i poder inserir els tres nodes que tenim. Cal deixar constància que quan es fa això, un node pot tenir més càrrega o més disponibilitat, és a dir, se li aplica més prioritat a l’hora de HA.
Ens anem a “**Crea**".

![img](https://lh6.googleusercontent.com/9W88QNUEnXRJozzKOScKDmwgfBxe6FVYMPPy42aLX9I3oETdSYPoqhNqzk6mB67OAvmpBXPRpd0ocx6l7QsBBKGthEnTDitrHf5UrXw37kA2slVE6gO5YQ7ETpOZoi3GtSuyE7vp)

Assignem un nom adient i la prioritat als nodes.![img](https://lh5.googleusercontent.com/UrVRNBihQAgRvNOUAb5yo7AeV6LH7AXCcjbdPzhrTXfZ1DW7vnXJUB8BY-6C7aLX0RuHW6uJynVeirb-aUkTjdUg5vMHVCO6SvU79ukzDYQCojNthR7Wye-e5bV1uxTYB5ZZbYzQ)

Això ja ens permet tenir un grup i assignar-lo.

### Comprovación Migración:

Podem apreciar que la màquina principal està en un node.



![image-20210611202517381](C:\Users\dpl\AppData\Roaming\Typora\typora-user-images\image-20210611202517381.png)

Aquest node cau, o la màquina.

![image-20210611202612928](C:\Users\dpl\AppData\Roaming\Typora\typora-user-images\image-20210611202612928.png)

Aquest node cau i es migra la informació a l'altre node. 

![image-20210611202534505](C:\Users\dpl\AppData\Roaming\Typora\typora-user-images\image-20210611202534505.png)



- Para instalar todas las herramientas que vamos a usar hem decidir usar Docker y los contenedores de cada herramienta, dado que es un método muy simple y además muy ágil para poder poner todo en marcha. También usaré Scrips para Snort 3.0 y ElastAlert.

### Snort 3.0

- Para instalar SNORT 3.0 he utilizado el siguiente script: 
```bash
#!/bin/bash
#Variables declarations
snort_interface="enp0s3"
#home_net=`hostname -I | awk '{print $1}'`
home_net="172.20.16.206/32"

#Update & Upgrade our environment
sudo apt-get update
sudo apt-get upgrade -y

echo "#### SNORT 3.O ENVIROMENT ####"

#Install all the necesary packages 
sudo apt install -y build-essential libpcap-dev libpcre3-dev libnet1-dev zlib1g-dev luajit hwloc libdnet-dev libdumbnet-dev bison flex liblzma-dev openssl libssl-dev pkg-config libhwloc-dev cmake cpputest libsqlite3-dev uuid-dev libcmocka-dev libnetfilter-queue-dev libmnl-dev autotools-dev libluajit-5.1-dev libunwind-dev

#Crate tha enviroment
mkdir snort-files
cd snort-files

#We clone the Snort3 l & enter libdaq
git clone https://github.com/snort3/libdaq.git
cd libdaq

#Configure and install libdaq
./bootstrap
./configure
sudo make
sudo make install
cd ..

#We get the gperftools for Snort3, enter on the folder and configure them
wget https://github.com/gperftools/gperftools/releases/download/gperftools-2.8/gperftools-2.8.tar.gz
tar xzf gperftools-2.8.tar.gz
cd  gperftools-2.8/
./configure
sudo make
sudo make install
cd ..

echo "#### SNORT 3.O INSTALL SERVICE ####"

#We clone the git with Snort3 & configure them
git clone git://github.com/snortadmin/snort3.git
cd snort3/
./configure_cmake.sh --prefix=/usr/local --enable-tcmalloc

#Build Snort3
cd build
sudo make
sudo make install

#Update shared libraries
sudo ldconfig

echo "#### SNORT 3.O CONFIGURE THE SERVICE ####"

#Configure netword interface
sudo ip link set dev ${snort_interface} promisc on
sudo ip add sh ${snort_interface}

#Disable Interface
ethtool -k ${snort_interface} | grep receive-offload
sudo ethtool -K ${snort_interface} gro off lro off

#Create and enable a systemd service unit
sudo bash -c "cat << END > /etc/systemd/system/snort3-nic.service
[Unit]
Description=Set Snort 3 NIC in promiscuous mode and Disable GRO, LRO on boot
After=network.target
[Service]
Type=oneshot
ExecStart=/usr/sbin/ip link set dev ${snort_interface} promisc on
ExecStart=/usr/sbin/ethtool -K ${snort_interface} gro off lro off
TimeoutStartSec=0
RemainAfterExit=yes
[Install]
WantedBy=default.target
END"

#Reload systemd configuration settings
sudo systemctl daemon-reload

#Start and enable the serice
sudo systemctl enable --now snort3-nic.service

#Create the snort3 rules folder
sudo mkdir /usr/local/etc/rules

#Download Snort 3 community rules & extract them
wget https://www.snort.org/downloads/community/snort3-community-rules.tar.gz
sudo tar xzf snort3-community-rules.tar.gz -C /usr/local/etc/rules/
#ls /usr/local/etc/rules/snort3-community-rules/

#Configure /usr/local/snort/snort.lua
-- sed -i "s/HOME_NET = 'any'/HOME_NET = \'$home_net\'/g" /usr/local/snort/snort.lua

#Define the location the Snort Rules
sed i 's/ips =
{
    -- use this to enable decoder and inspector alerts
    --enable_builtin_rules = true,
    -- use include for rules files; be sure to set your path
    -- note that rules files can include other rules files/ips =
{
    -- use this to enable decoder and inspector alerts
    --enable_builtin_rules = true,
    -- use include for rules files; be sure to set your path
    -- note that rules files can include other rules files
    include = '/usr/local/etc/rules/snort3-community-rules/snort3-community.rules'
}/g' /usr/local/etc/snort/snort_defaults.lua

echo "#### SNORT 3.O INSTALLING OPENAPPID ####"

#Download the pakages
wget https://snort.org/downloads/openappid/17843 -O OpenAppId-17843.tgz
tar -xzvf OpenAppId-17843.tgz
sudo cp -R odp /usr/local/lib/

#Copy and configure the location of the OpenAppID
sed -i 's/appid =
{
    -- appid requires this to use appids in rules
    --app_detector_dir = 'directory to load appid detectors from'
}/appid =
{
    -- appid requires this to use appids in rules
    --app_detector_dir = 'directory to load appid detectors from'
    app_detector_dir = '/usr/local/lib',
    log_stats = true,
}/g' /usr/local/etc/snort/snort.lua

#Create Snort3 log directory
sudo mkdir /var/log/snort

#Check the Snort3 configuration
sudo snort -c /usr/local/etc/snort/snort.lua

#Create a rule to detect ping tests
sudo bash -c 'cat << END >> /usr/local/etc/rules/local.rules
alert icmp any any -> $HOME_NET any (msg:"ICMP connection test"; sid:1000001; rev:1;)
END'

#Check the local rules
sudo snort -c /usr/local/etc/snort/snort.lua -R /usr/local/etc/rules/local.rules
sudo snort -c /usr/local/etc/snort/snort.lua -R /usr/local/etc/rules/local.rules -i ${snort_interface} -A alert_fast -s 65535 -k none

echo "####SNORT 3.O LOGGING"
#Configure the events loggings
sed -i 's/--alert_fast = { }/alert_fast = { 
        file = true, 
        packet = false,
        limit = 10,
}/g' /usr/local/etc/snort/snort.lua

#Check for the configuration
sudo snort -c /usr/local/etc/snort/snort.lua

#Runing the comand with the option -l /var/log/snort
sudo snort -c /usr/local/etc/snort/snort.lua -R /usr/local/etc/rules/local.rules -i ${snort_interface} -s 65535 -k none -l /var/log/snort/
```

- Una vez tengamos SNORT configurado e instalado simplemente deberemos crear las reglas para que estas puedan enviar un alerta siempre que sea necesario.
- Vamos a explicar que es y como se hace una regla. Las reglas de SNORT son las que se encargan de detectar lo que nosotros le hemos idicado en la diga, de un trafico elegido. Esta regla una vez vea una situación del trafico que sea compatible con los parámetros de la regla de SNORT lanzará las alerta al fichero de logs de SNORT que se encuentra en la ruta siguiente "/var/log/snort/" y el fichero se llama alert_fast.txt en mi caso, puede tener más nombres.
- En el fichero de log veremos lo siguiente donde se nos dará la siguiente información de la alerta: Fecha > Numero de Identificación de la Regla > Mensaje de Alerta > Prioridad > Protocolo > IP de origen con su Puerto > IP de destino con su Puerto. En la siguiente imagen podemos verlo más gráficamente:

![img](https://lh6.googleusercontent.com/px38Hg18Sy5zx-Mriug5N_G05jq8mIfTUW5v9KZ3IZR2b5xN1fQRDs8gZAhDpv54Fh66gt5aVxq5DcwwyScDG3hklbF2gtdH2dgfsLA0Q1mLp6QREyAFZqiubYu1QDUNrnQjD9lz)

- Para crear una regla necesitaremos entrar en la ruta siguiente y acceder al fichero con ese nombre "/usr/local/etc/rules/local.rules" y allí podremos crear las reglas que veamos necesarias para nuestra necesidad. Principalmente tenemos esta regla

```txt
  alert icmp any any -> $HOME_NET any (msg:"ICMP connection test"; sid:1000001; rev:001;)
```

- Para crear una regla debemos tener clara de que queremos que se nos informe y de cuales son nuestras necesidades principales. También tenemos que tener claro como se crea una regla y su estructura, para ello podemos utilizar como referencia la siguiente imagen: 

![img](https://lh3.googleusercontent.com/iRMafaPFZBw42toysppR6G48UrkiYNQ7TpHnTKAd6_gq_JWWr8xf5oVbqDhnd-tzOxV22p-E405ViPy-H48oOP8yo38PF3TbkO2195otA1XshYkk-8tCaWGLJpTpMnLhbXGo0KnW)

- Vemos que la acción en este caso es *alert* pero tiene más opciones como pueden ser, el mismo alert (genera una alerta utilizando el método de alerta seleccionado y luego registra el paquete), log (registra el paquete), pass (ignorar el paquete), drop (bloquea y registra el paquete), reject (bloquear el paquete, lo registra y envía un restablecimiento de TCP si el protocolo es TCP o un mensaje de puerto ICMP inaccesible si el protocolo es UDP) y sdrop (bloquea el paquete pero no lo registra).

#### Puesta en Marcha

- Una vez tengamos el Snort configurado y con las reglas creadas simplemente vamos a iniciarlo con la siguiente comanda:

```bash
sudo snort -c /usr/local/etc/snort/snort.lua -R /usr/local/etc/rules/local.rules -i ens18 -s 65535 -k none -l /var/log/snort/
```

![image-20210611221507716](C:\Users\dpl\AppData\Roaming\Typora\typora-user-images\image-20210611221507716.png)

- Una vez iniciemos Snort 3.0 visualizaremos lo siguiente por terminal:

  ![img](https://lh4.googleusercontent.com/84efF3TnWuw1BGS30RnkaSc5EYhY_QJjMYvAZ3MoNphsW-9ZYa8WVfA6gAwtS_LMhS-zMBvTYhOzAGsI9-BTtMpV3C7n1JN2sBGB3BS7XonL_xn4vVAyw_aXDHHd7xDmF03Jsnuc)

- Una vez tengamos ya Snort 3.0 iniciado podremos visualizar como en la ruta "/var/log/snort/" se nos ha creado el fichero llamado "alert_fast.txt", en su interior contendrá las alertas que Snort a creado por la detección que ha tenido. 

- Con la siguiente comanda podremos visualizar las últimas 10 alertas:

```bash
sudo tail alert_fast.txt
```

**![img](https://lh5.googleusercontent.com/Kkl1Ky9v6mOwdLakcGrEH4xcigCfYYe4-dj1A6RZCe-mAjKa8x4soplBDrqURsOkW2Z5GVTHyw0HMMLPlNafKR27wFN6hw_T_9RLFrX8uW8L47yAOg-A2uCJIQ35J6SdjPWyVqQW)**

## Contenedores

- Para la creación de contenedores primeramente vamos a crear el entorno para Docker y el Docker-Compose que serán los que nos ayudarán y se encargarán a subir los contenedores e iniciar los servicios.

### Docker
- Para instalar todo bien necesitaremos actualizar todo los programas de nuestra máquina virtual.
```bash
sudo apt-get update
```
```bash
sudo apt-get upgrade
```
- Una vez tengamos la máquina actualizada ya podremos instalar docker con la siguiente comanda:
```bash
sudo apt-get install -y docker.io
```

### Instalación THP con Docker-compose
- Para instalarlo usaremos el Curl para instalar la última versión de docker-compose dado que con sudo apt-get install nos instalará la 1.25.0 y nos interesa la 1.26.0 como mínimo

- Empezaremos instalando Curl por si no lo tenemos.
```bash
sudo apt-get install -y curl
```
- Y una vez tengamos el Curl solo deberemos insertar este comando:
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
- Darle permisos de ejecución:
```bash
sudo chmod +x /usr/local/bin/docker-compose
```
- Y ya tendríamos el docker-compose con la versión 1.26.0
```bash
docker-compose --version
```
```tex
docker-compose version 1.26.0, build d4451659
```
- Ya con el docker-compose funcionando vamos a crear el fichero docker-compose.yml donde le indicamos la imagen del contenedor y su configuración necesaria para que funcione. Instalaremos  y levantaremos los contenedores de TheHive que depende de Cassandra, Cortex que dependerá de Elasticsearch, MISP y sus módulos que dependerá de MySQL y Redis y para acabar Kibana que también dependerá de Elasticsearch.

```yaml
version: "3.8"
services:
  elasticsearch:
    image: 'docker.elastic.co/elasticsearch/elasticsearch:7.11.1'
    container_name: elasticsearch
    restart: unless-stopped
    ports:
      - '0.0.0.0:9200:9200'
    environment:
      - http.host=0.0.0.0
      - discovery.type=single-node
      - cluster.name=hive
      - script.allowed_types= inline
      - thread_pool.search.queue_size=100000
      - thread_pool.write.queue_size=10000
      - gateway.recover_after_nodes=1
      - xpack.security.enabled=false
      - bootstrap.memory_lock=true
      - 'ES_JAVA_OPTS=-Xms256m -Xmx256m'
    ulimits:
      nofile:
        soft: 65536
        hard: 65536
    volumes:
      - ./vol/elasticsearch_data:/usr/share/elasticsearch/data
      - ./vol/elasticsearch_logs:/usr/share/elasticsearch/logs

  kibana:
    image: 'docker.elastic.co/kibana/kibana:7.11.1'
    container_name: kibana
    restart: unless-stopped
    depends_on:
      - elasticsearch
    ports:
      - '5601:5601'

  filebeat:
    image: 'docker.elastic.co/beats/filebeat:7.11.1'
    container_name: filebeat
    user: root
    environment:
      - filebeat
    depends_on:
      - "elasticsearch"
    volumes:
      - "./filebeat.yml:/usr/share/filebeat/filebeat.yml"
      - "./test.json:/usr/share/filebeat/sample.json"
      - "/var/lib/docker/containers:/usr/share/filebeat/dockerlogs:ro"
      - "/var/run/docker.sock:/var/run/docker.sock"
      - "/var/log/snort/alert_fast.txt:/var/log/snort/alert_fast.txt"
    command: ./filebeat -e -c filebeat.yml

  cortex:
    image: 'thehiveproject/cortex:latest'
    container_name: cortex
    restart: unless-stopped
    volumes:
      - ./cortex/application.conf:/etc/cortex/application.conf
      - /var/run/docker.sock:/var/run/docker.sock
      - /tmp:/tmp
    environment:
      - http_proxy=${http_proxy}
      - https_proxy=${https_proxy}      
    depends_on:
      - elasticsearch
    ports:
      - '0.0.0.0:9001:9001'

  cassandra:
    image: cassandra:3.11
    container_name: cassandra
    restart: unless-stopped
    hostname: cassandra
    environment:
      - MAX_HEAP_SIZE=1G
      - HEAP_NEWSIZE=1G
      - CASSANDRA_CLUSTER_NAME=thp
    volumes:
      - ./vol/cassandra-data:/var/lib/cassandra/data

  thehive:
    image: 'thehiveproject/thehive4:latest'
    container_name: thehive
    restart: unless-stopped
    depends_on:
      - cassandra
    ports:
      - '0.0.0.0:9000:9000'
    volumes:
      - ./thehive/application.conf:/etc/thehive/application.conf
      - ./vol/data:/opt/data
      - ./vol/index:/opt/index
    command: '--no-config --no-config-secret'

  redis:
    image: redis:latest
    container_name: redis
    restart: unless-stopped

  db:
    image: mysql:latest
    container_name: db
    restart: unless-stopped
    command: --default-authentication-plugin=mysql_native_password
    restart: unless-stopped
    environment:
      - "MYSQL_USER=misp"
      - "MYSQL_PASSWORD=example"
      - "MYSQL_ROOT_PASSWORD=password"
      - "MYSQL_DATABASE=misp"
    volumes:
      - ./vol/mysql:/var/lib/mysql
    cap_add:
      - SYS_NICE

  misp:
    image: coolacid/misp-docker:core-latest
    container_name: misp
    restart: unless-stopped
    depends_on:
      - redis
      - db
    ports:
      - "80:80"
      - "443:443"
    environment:
      - "HOSTNAME=https://10.200.0.29"
      - "REDIS_FQDN=redis"
      - "INIT=true"
      - "CRON_USER_ID=1"
      - "DISIPV6=true"

  misp-modules:
    image: coolacid/misp-docker:modules-latest
    container_name: misp-modules
    environment:
      - "REDIS_BACKEND=redis"
    depends_on:
      - redis
      - db
```

```tex
image: imágenes necesarias para crear los contenedores
container_name: indicamos el nombre que va a tener el contenedor
environment: son las variables necesarias para que funcione el contenedor
depends_on: creamos una dependencia entre contenedores
ports: indicamos el puerto público para un enlace de puerto
restart: en caso de problemas con el contenedor, indicamos el reinicio
volumes: mapeamos un directorio a otro dentro de contenedor
cap_add: permite cambiar las prioridades de programación
command: lanzamos el comando que permite ejecutar el servicio
```
- Para poder iniciar el levantamiento de contenedores deberemos utilizar el comando siguiente en la ruta donde tengamos el docker-compose.yml: 
```bash
docker-compose up
```
```txt
-d: Realizar el levantamiento de contenedores en segundo plano
```
- Una vez levantados los contenedores podremos observar la siguiente ruta:

```
  .
  ├── cortex
  │   └── application.conf
  ├── docker-compose.yml
  ├── filebeat.yml
  ├── README.md
  ├── thehive
  │   └── application.conf
  └── vol
    ├── cassandra-data
    ├── data
    ├── elasticsearch_data
    ├── elasticsearch_logs
    ├── index
    ├── mysql
```

- Podemos confirmar que los contenedores están levantados y en pleno funcionamiento de la siguiente manera (docker ps -a): 

![img](https://lh5.googleusercontent.com/9YgUXXjGx5TT-eHx7EP-SJes_Jti05S9VCBklDTI7zxBS5U1ZcvhGajVqfE9gQLZIDbuI4OfdPauG2HyS148Fwa3C5pMC9Gr-70z0OnrwajDxGAhhbq55gi3pDTCWyQqDqiYdNbz)

- Ahora querremos poder conectarnos por web a los servicios que hemos instalado las <a name="crd">credenciales</a> y las URL's de acceso son las siguiente.


```txt
ELASTICSEARCH: http://localhost:9200 / No requiere ni usuario ni contraseña

KIBANA: http://localhost:5601 / No requiere ni usuario ni contraseña

THEHIVE: http://localhost:9000 / user: admin@thehive.local / pass: secret

CORTEX: http://localhost:9001 / Crearemos el usuario cuando se nos solicite

MISP: http://localhost:443 / user: admin@admin.test / pass: admin
```

### TheHive, Cortex y MISP

#### Configuración TheHive

- Una vez entremos a la URL de TheHive que tenemos en la [tabla](#crd) nos aparecerá una ventana para iniciar la sesión con los credenciales que se indican en la misma [tabla](#crd) que el URL.

![img](https://lh3.googleusercontent.com/wCeWNwwfczrmh7hvmVpN8LpF647KhbSVPnPHstlMU82DZOmkScp2fqePxxrS8j6Nwh8wZoecQnh__CPYcoNxG_HcZ6UfxSG_b9czimb0JlHNWKD2mOft4Y_AnWoJv_AuQSoUSXt9)


- Una vez dentro podremos ver la interfaz gráfica de TheHive y podremos ver que tenemos una gran variedad de posibilidades que hacer.

![img](https://lh4.googleusercontent.com/V3u2XAsDwgR28mf7pgARg1fmG-tnPfPyMIrWcdF9z5PvkneBztuDATpPUIkz_CY7tcxW3C03avt1IrMvuctKZezEFU6nnp4Bc5wVZBY2W-8alp_LCaOlKFlSOB-3gCQEKbp0E-Ol)


#### Configuración Cortex

- Cuando entremos en la URL de Cortex que tenemos en la [tabla](#crd), se nos pedirá que la base de datos de Cortex se actualice, para ello le daremos a "Update Database".

![img](https://lh3.googleusercontent.com/V9AacR9SVCLzRjGAl-8eU6L9yB0rJf8pvgxdv9YssJrjwlzyF7C9x1Lq1Hn-hdKmi9vjITIqKDK1gPeB5I8hlDV7zxgZS1s7fgvSOulsDYHHr80VwuTnQNNZX89jOHYtn7IUE9zp)

- Una vez hecho nos redirigirá a una ventana donde deberemos crear un nuevo usuario para Cortex.

![img](https://lh6.googleusercontent.com/l0QLMhOQRGHBnDogYsQuxKRx_PXYpKTLBjNADaQxKOZkvKSzKQb-pjmgYYRtS1q7x4a_AnlJPYEL8EdWNfkAZlIFrq5bXslTbp6H2peHdoW6xReNJXdBoQK4vggFuELOB2ncjSEu)


- Ya con la cuenta creada nos enviará al Log-In dónde deberemos iniciar la cuenta que hemos creado anteriormente.  

![img](https://lh4.googleusercontent.com/GXuisDdD_7HQsu5iLb9KvaHfT7vAWM1zruKWct-lV-TGcHSXioiDx5U2iz0cz0KmP99E7DWcPqA7UbNM8juFDYRwLYBDdwD5e_xXuoa88jfntuRKD7L8uV3_awYWFUwBhGxb6jQS)

- Una vez dentro ya podremos ver el entorno gráfico de Cortex con la organización “cortex” que viene por defecto la otra es una nueva que debemos crear para la integración.

![img](https://lh3.googleusercontent.com/rGXVBvyxHAQ2a3o0-ocFEOyRh1cc_aSO7d6cTv-ncYHDk1tOJXjk-VqTGHmhivPWZSHhNgTCx7-VLedDKTmK3bj910EMqyPisFlVsp7QTrLalWQZPHiwN8IOqiZoNMu_ftDmYpBl)

#### Configuración MISP
- Con MISP vamos a ir a la URL que tenemos en la [tabla](#crd) principalmente nos saltará el riesgo de seguridad pero podemos avanzar tranquilos porque es nuestro servicio.

  ![img](https://lh5.googleusercontent.com/4sGVuayacNEzeG8iUJnbGf2FpuB02VxN7hlPbYc3KznWz6pdNTWTebvIQL90NzDjzPFJxMJK1W1nW0y1jZh65TTex5x_CDYmWdDcGq0ObRZUmqvGW-CEhJA5zm2Se-T1Sb4B-C6r)

- Una vez aceptado el avanzar nos aparecerá también un Log-In donde tendremos que introducir los datos del usuario de MISP que tenemos en la [tabla](#crd) de arriba.

![img](https://lh6.googleusercontent.com/258hLJ1Xn0FsH6x5FxLESYhpXKDFN5bUdhM8kK-j2o4TMoIqv9v5Wi-sQ58-ZxkDa2lvYM-1A6GHZpYMs8za0K1A_Dpk4OGwg7AADVqLnF0Lbj4IVTBBp_kb0iij1BsIn5BFSmkd)

- Una vez dentro se nos solicitará que cambiemos la contraseña por una más segura.

![img](https://lh4.googleusercontent.com/teIXWo_x1DOFoHcoI7OPDbvj3D8kllcoNPe4DjxAwAnih50EOQ1DXQeu5M5F-1UPP3xSV9DCAYaSDc6IijX21TBVaeZXMiDmMJ_blfxNs4ZBXrcsBPt41fA--YFo-yz0KBcr_DgA)

- Ya con la nueva contraseña ya creada nos dejará acceder a todo el contenido de MISP, principalmente nos enviará a la Lista de Eventos.

![img](https://lh4.googleusercontent.com/iJtXRpcBC-e1Th9ERGvb3BHtSkpE5a--ME26KBJHTMGDq-x8BjIKeE2BvgoV017fUO3z1DSDP0w6nPOlQRKgZVczhY_7FhwifMcSnHhznFrnyahAjaP-62APff8c1lHk69KREYjA)

### Integraciones
- Una vez tengamos nuestros servicios instalados y configurados deberemos proceder a integrarlos entre sí para que reciban información y realicen la función que les pertoca.
- Principalmente debemos saber que principalmente los servicios irán enfocados a TheHive que es quien recibirá la información y este las enviará a los diferentes analizadores. 
- Para ello deberemos crear un usuario para TheHive, Cortex y MISP si queremos realizar la integración correctamente. Lo podemos hacer de la siguiente manera.

#### Cortex

- Empezaremos con Cortex donde crearemos una nueva organización con el nombre de nuestra empresa para poder organizarlo todo mucho mejor y entenderlo más fácilmente.
- Deberemos ir a la URL de Cortex y seleccionar “+Add organization” y procederá a abrir una ventana donde configurar la nueva organización.

![img](https://lh6.googleusercontent.com/mXi2k12wbUJB4bgWkD_8NYX8pqNihuKIVxRU6x1q3zEAR2P-LV1iSzv4573GNp2CJy1PksMwb75WlWABOKDGDVTEBJNon8UYzu5aULxV30cYtONI7aZk0q4kYQS82keCjYjr1lrF)

- Una vez creada, entraremos y deberemos crear un usuario que será el que se encargará de la integración. Para ello seleccionamos a “+Add user” y configuraremos el nuevo usuario.

![img](https://lh5.googleusercontent.com/ooEGNXMm5PGVZJd4axA2_hxPYC4EZOwTjd4IYxNg-zVkOUBdfRKZfb7UbO_zr1Gmuk9cyPyraHHvjen0NrgZmIgUSMDMLOLCbdspL0n-Piw49j0G0FX8U1STehTwOS6a1Zi7NGLp)

- Ya con el nuevo usuario creado veremos que aparece en nuestra organización y le daremos una contraseña en "New password"  y una API key con la opción de “Create API Key” para el nuevo usuario, esto lo que hace es generarnos una para este usuario.

![img](https://lh6.googleusercontent.com/htx8mWg4zi5LoPYeorB15ZXbpYmXRe5HSYsWi23ZdB8Vx0EQsb6Br2PzqYr9l9ynP6dI6Q_5UCotkhsaAkPqqcAAmhror_jkCJWJf6W6H9p7hbTj8vs50X0BzMCqz0fVQZqktLZn)

![img](https://lh6.googleusercontent.com/hBM4R6Ew19PWvNXuf3TIQSbTsuO1rbr9ziihE26xRt1dM5xYjCdYadahMNGxfAB3mISILqIZVlu8pz_XFkfavkGHA8xAzwzDYLgorXdDL-_GPpFsZnsvrHNmYT8iAUlPgAUIgDN0)

- Ya con la API Key la podremos revelar en “Reveal” para poder introducirla en nuestro fichero de configuración de TheHive en el apartado de cortex como veremos a continuación. Con “nano application.conf” podemos acceder al fichero de configuración y modificarlo. 
- En el apartado de play.modules.enabled donde ponga "cortex" y en el apartado de "key" introduciremos la key que hemos copiado del nuevo usuario.

![img](https://lh6.googleusercontent.com/Ef7QwHHwFf8qiUgC4OZmbgzOAarBtoyeRHOABpaM0fiWAymKnpH1g6mh0zwA-RFaVrm6VBM3vqlzY3fAkVWaj13myd49-5qh5VyYV1x8BkHsEB3pMWmeuy9oTuzjsc4JEYjo-Frv)

![img](https://lh6.googleusercontent.com/mUTQrQL2S1PGR2NedUSP_c98dcC3mI2SeD68zgiwmAZiv5wyJCnDmEN0ZfA5vcQ5bt0wtrVph2pFYqV0lVfUW2OwKUnEfHyjU3dkMFPQsjCQUb4OPQX1DEGygh05nB85bsgTqauu)

- Una vez tengamos la API configurada ya podremos ver la integración positiva en TheHive con un círculo verde en la parte inferior derecha. 

![img](https://lh6.googleusercontent.com/Iz1lkUX8TgVInF7LrSIv6Vsw-k0zx5CftDpRuC7rtX6EQL21qhMZ_YUhBSQiydTbUMyhzQYh3gn5BlKixqYR351h2SoxgJRzSE1H1oruzlKzjo9FctWMJqYXCYxJoiCLpnOlNe5A)

- Para acabar la configuración de Cortex deberemos activar un par de analizadores para hacer pruebas y hacer la comprobación de la integración. Para ello iniciaremos sesión con el nuevo usuario que hemos creado. Veremos que tenemos todo vacío y estamos dentro de la organización en la que nos hemos añadido. 

![img](https://lh3.googleusercontent.com/ujp62ozF_31a1WLsDxuj-r7QEz8QcXCNDAHw6JoLCt-shicMQ7t99785D6QsXGrB1nZaaZOoC-6KKnNX7I8AlBgcoSSsVu3ESae4gy9N8S8SWvhmPBbdMunfHJT6cgWnRJWaUp0q)

- Para activar los analizadores iremos a “Organization” y una vez dentro iremos a “Analyzers” donde nos aparecerán una gran cantidad de analizadores (Nosotros elegiremos VirusTotal).

![img](https://lh6.googleusercontent.com/0L3413oZrV4sd1vnEOE2cssaiLouYDKyMgHaiPtwTmYh-mL1_Yr0TJlRFBXHhbJvydWF8jI5L1GOhhn5raelZBChKCk-Rrr-jVBSVu3UG86D-wYLZQEeoOYz_IceHlfvlM7DO5YJ)

![img](https://lh3.googleusercontent.com/niJLb6_9l-3lUBZdi2DuHjqtQxcv1k0O9T5zhTSmyLSNBYrKY3barc2ixX8xSN3VDOyVBomfJqiZTv772R_EzBhZ50UnTxTxz0u9W667kEO-1U3TSsbYr-vu8STpWDpf58D2_O4D)

- Para activar los dos analizadores simplemente seleccionaremos “+ Enable” y se nos desplegará una ventana para la configuración del analizador  y usaremos la siguiente configuración para los dos analizadores. 
- Para poder finalizar la configuración se necesitará tener una cuenta de VirusTotal, con la cual te generarán una API Key personal.

![img](https://lh6.googleusercontent.com/4aKpdeKbaIz8D4oaC2f3EisK933S_uOeyHcjLubeTHsk-e98OkYo50ad5abCm1pjdUwq2SqzhZrcJ8DszfTqZIhXgmuE94jq6n2shgBAJVxZhoCejCyKPbWw2yTohUGEdouSLvXR)

- Una vez hecho veremos que tenemos los dos analizadores ya activados.

![img](https://lh3.googleusercontent.com/5EZ-z2-w_HAx19UBEEsAC_haACjPdVkErvAluNF5tkH72ZwBjDmZ-riiT2o0IwylD-IaU9Dn-G7dc6_RClMKekZuSpwv0QninPD5GXdtAtitpHt8RR4Hu-TzHJaVXltkbqFsXmh8)


#### MISP
- Con MISP deberemos realizar una configuración parecida a la de Cortex pero simplemente vamos a “Event Actions > Automation” y allí tendremos la API Key que al igual que Cortex la introducimos en el fichero de configuración de TheHive en el apartado de MISP.

![img](https://lh4.googleusercontent.com/6KUBiZXDq8WhHTJJ8BmuBsvQ54SXkyc55jN-6T3C7jaIFUDx5CVcy3sbzKh0OlueAzWdDWyqAGR0K00ZltydGUKBLvJ6T3_dqpEQWINymsfADHL9R8W8S7ndbVn0NBF61Z8p9fO_)

![img](https://lh4.googleusercontent.com/tB9cTCFfBZATE96ZQH7XXenmX2zk_k6M0PtdcPJgePScwy5qKzdPVqJKU-sa6E6JVnD57de3QCYdzfR25pa8vrlYgXglzVY0n286mEATFwoM-WDcBulANl_LK5DAkYtAO0XNt4iQ)

- Una vez integrado MISP veremos que en la interfaz gráfica de TheHive ahora podemos ver un icono más en verde que será el de MISP indicándonos que ya está integrado. 

![img](https://lh6.googleusercontent.com/TsjiU-NDCgWHuiHNgraS6qD5bv5h8P3D5ilaNr00bIoL7ADLGkb1fKwElzTQ7Pz8oi8tcikSbHGuNPC8lMEe3wNyXnYCxQYYP1ydf7rVnCzHTiOWyVt48WAWHr_AnhvU52bKTbvB)

![img](https://lh6.googleusercontent.com/4ArxQBNQg5O987K35jaU_tYk0IsdZPYER6jy5OOCJozAFf82mJrPQIst_skIV7AGnS3yFVQk5neroGB_L0BbhWwwZxaUsqWx2HVq3152uNDe18cmwQRDi2iCuxaIpwXxG73bTsWF)

#### Pruebas
- Para hacer las pruebas iremos a TheHive y crearemos una nueva organización con el botón "+ New Organisation" y un nuevo usuario para esa misma organización.  

![img](https://lh5.googleusercontent.com/FYdOtN5NDDMhErV1VgKuFPhjzlu9x383FzathPnYtW9bqNDh2QWobZKVprUQ6WRaE62otiZUR2EPdsDBKxh-nK2hrgBUQ5DAk0gQO-BDgTa-UCEMmlcHniX-BSeVlE09ueowYPkm)

- Dentro de la nueva organización creada creamos el usuario con el botón "+ Create new user".

![img](https://lh5.googleusercontent.com/bx-EZ4g5OhyH7omCArvp6GqarpWwiBp7Nvyi8gPg16BzH-o1G1kXR-GZq4nNhYuEjVzY_K9cslj9Dy0p7d3WqLCVN4f1FygaNSmZXt3MJg4LLJ2VSGRkreQgvQBXdYQe2jcUtskK)

- Y una vez hecho le daremos una nueva contraseña con "New password" que una vez hecho pasará a ser "Edit password" y ya podremos iniciar la sesión con este nuevo usuario y acceder a la organización desde dentro.

  ![img](https://lh4.googleusercontent.com/r1533v-jbLFk5SRF8ETn8i9oiNnqXk6Z3xW_6inT1HOxTUnCJC5zi5t-UcprEoaeEuOea2BTVwEde7wW9Zji78YYve41wjDsW9xXyGM7twYB7mhpzyHBj6JqbYVG6YSdOU_t6Lrk)

  ![img](https://lh6.googleusercontent.com/ovw1LZgCuR0_I4lh0sZ_uZaf-9Wrt49jQF3oJbWwxH4UXRSnmvgEOFV5oik4KHYg40XX2GrqrrcCcb-eZB2XGJWDG-5aMo5wTYe4aE5IiLQ4GpjlvYftUdc9h99Ia1tD72Lba1N0)

- Una vez dentro crearemos un nuevo caso con la opción “+ New Case” y nos saldrá la ventana de configuración del caso.

![img](https://lh5.googleusercontent.com/Rixbs2zDgriIGW26EZr08Q8k-eKedLN4ze7S67lT7aJU9M16jR4nIH9Ls69uzCeIGIcOV8Mm66B0meLRL3o95ssCzLL2yoZC7rmQgi-oT-JRzUZznII9Gw2o9QSnpwcJt-mFTy4x)

![img](https://lh5.googleusercontent.com/mHYu5qQPqt6EBwfCiVyDsQ_EqvmE9juH4w3pLW3xk_zFJO46K2zciv7ZPOKncVrBjpjCARr-TOClPgJHdZcXiOO2hKaObn93eqMS7WoM_WnlbVA3UTCVsfbIvskmMYG8R8lvO306)

- Dentro del caso iremos al apartado llamado “Observables” y seleccionamos “+ Add observables” y nos saldrá la ventana para la configuración del observable.

![img](https://lh5.googleusercontent.com/u_hmkrTIw6QO7YlTzggSlp86UpgSyCt_rf8lc-sQHI1bqiKLYevOR2Z6HBzYCXY9Eo-AI3FQfjrCUtqAr9YMIt7iRWJylUFio1_ORwzwSRWWqExZMhsdlgwDj-9YCzTEFEjykeeF)

![img](https://lh6.googleusercontent.com/W2Ort7n8-MoGNh4ubDp95wTCMEwKBsWE8tq6avBwRhlbZ_AiRVE2WX-YqCXXClc9hy3Pb61uxLY8Kk24hof0cCGOJTJ3JeXi_wcpDxvagrHIIX-Ahod37CoIKwly_qhe855hMcmJ)

- Una vez creado el observable podremos seleccionarlo e ir al apartado de “1 selected observable” y le daremos a “Run analyzers” y nos saldrán los analizadores que tenemos disponibles. En nuestro caso solo VirusTotal.

![img](https://lh4.googleusercontent.com/pCGJLRD1V1zEQ_voeYrGie5C6lWOUyKtttmQBbvRlPNJbp4mCOIixGbWtGnI_vdXSfqGYxuhFA8bjPY9z7zOC8uEVQ-HiokBCkJPhpPgRAko5Rl8x1vU7pDPZkqVUYyhcuNuzySt)

![img](https://lh4.googleusercontent.com/-PgXWAAXXFnDAtGhiZ5XjFM9jg-6Bbf6Hf7dJIde9i8xmXxDMc3Sj6oy1WmAYgqDgjB6I5Fi6XIa-t6RhbIb6Ly15rqQ0KaOtU8Od0W4n6Qg3AbXtTTeaTuCPar02WbTB9zdpAqZ)

- Una vez tengamos ya corriendo el analizador Cortex automáticamente creará un un nuevo análisis con los datos que hemos configurado en TheHive y empezará inmediatamente a analizar el dominio en este caso que le hemos dado.
- Tardará un rato pero al final podremos ver que podrá “Success” y eso nos dará vía libre de ver que ha funcionado bien. Entraremos dentro del análisis y podremos ver el reporte que ha hecho el analizador.

![img](https://lh5.googleusercontent.com/l06vH5-iXDzu0CapoJq_7ABuvPCbS1kevad5c_MHvMgowzRi1Obrg97JoBShJPPi2E4kwPQvDshw_VANWT8ZWTKTZ8zou_5PDlgc9pDLGqEmU9f42WgSXps8sUQH6DkUVvy3FdSF)

![img](https://lh6.googleusercontent.com/O-i2-Qz1UpUecqElrCbTaMRmpUjtV_fnCN14Jig0CykWVRvlo2Wm85ssC5DEEwdxIIIUALlWbVOQEfoGWjsI_satA0ODydxjE1Xbhzpu1OXIvjdL5u4ZybrsyC7q6jq4Z_rqsb8G)

![img](https://lh5.googleusercontent.com/97xWEsj1-Kd7AUlxuCJlHeNKAw3HOT9N4goxl_n5GwwpHrIX-luDr-8FSqDFzgTzUOj9MwOFYdw76B0R4EaBxx75n4XUy9yKemrinKz-2a7GmI4WtgOE9Io73_XVPCpGjlncQnF-)

- Por otra parte TheHive aparecerá el resultado del reporte con los resultados críticos y que pueden suponer una amenaza en rojo como podemos ver en la imagen.

![img](https://lh5.googleusercontent.com/eicQTUuHBcmTfw3vbMHfLu12UrXVSxOgllAmQi4w7l449QET2Z1AuoJbtC_T9m1TslkX01h7dRU7MIJGvg0XQcEPJ7K7TSRWEOz0vuJfopIFsu19_gvl-Fek5cWoeLtZ-CUvznMS)

- Esta notificación en rojo la podremos seleccionar para que nos aparezca el reporte de Cortex pero visto directamente desde TheHive.

![img](https://lh3.googleusercontent.com/-QuTfntUJRqeztDQFS5hH4bDbAjEjnKM0CkJwe1KAwZ0xtUqYmCA2G-pKvuIudhyoXO0inUdczV0_s8Biyg4FOCqkqomzSrvmQScMVpRrBL8O0S8bcuqkQB9WYF9zuX7AhOaE1Q9)

### ElastAlert

- Nuestro objetivo es automatizar todo el análisis de Cortex con TheHive y por ello queremos enviar los datos recogidos por Snort y enviarlos a TheHive con la siguiente ruta "Snort > Filebeat > Elasticsearch > Elastalert > TheHive".

#### Instalación y Configuración

- Para ello vamos a necesitar configurar Elastalert siguiendo los siguientes pasos:
- Primeramente vamos a necesitar realizar la instalación de ElastAlert.

```bash
#Install all the packages for Ubuntu
sudo apt-get install -y pip python-dev libffi-dev libssl-dev

```

- https://elastalert2.readthedocs.io/en/latest/running_elastalert.html#as-a-python-package

- **Instalación (Debian)**

  ```
  1. wget https://github.com/Yelp/elastalert/archive/v0.2.1.tar.gz -O - | sudo tar -xz -C /opt/ # Download a stable release from the Elastalert repository and place it in whichever directory you wish. We will use /opt/ for this demostration.
  2. sudo apt-get install python3.6-venv  # Install a virtual enviroment
  3. cd /opt/elastalert{version} && python3.6 -m venv venv #  Create a virtual environment within the project directory
  4. . /opt/elastalert/venv/bin/activate #  Activate the virtual environment
  5. python setup.py install #  Install the provided Python package
  6. git clone https://github.com/Nclose-ZA/elastalert_hive_alerter.git #  Clone the Nclose Hive Alerter master branch
  7. python elastalert_hive_alerter/setup.py install #  Install the Nclose Hive Alerter python package
  ```

  ------

  **Instale el respondedor de TheHive (para suprimir eventos de la instancia web de TheHive)**

  ```
  1. Copie `thehive_suppressor` en el directorio apropiado en su instancia de theHive (generalmente ubicado en` /opt/Cortex-Analyzers/responders/ObservableHashCreator` en implementaciones de Docker). 
  2. Inicie sesión en Cortex. Vaya a `Organización`,` Configuración de respondedores` y debería ver el `ObservableHashCreator` si lo anterior se siguió correctamente. Configure los requisitos necesarios.
  ```

  ------

  **Ejemplo de uso de alertas**

  Configure la alerta en el archivo de reglas:

  ```
  alerta: "elastalert_hive_alerter.hive_alerter.HiveAlerter"
  ```

  Configure los detalles de conexión para TheHive (los campos obligatorios se muestran primero) en el archivo de configuración o en el archivo de reglas:

  ```
  hive_connection: 
    hive_host: https://10.200.0.29:9000
    hive_port: <9000> 
    hive_apikey: <hive_apikey> 
  #NOSOTROS GRAIL NO HAY EN ESTE LAB
    hive_proxies: 
      http: '' 
      https: ''
  ```

  Configure la alerta proporcionando los parámetros consumidos por TheHive4Py (los campos obligatorios se muestran primero) en el archivo de reglas:

  ```
  hive_alert_config: 
    title: 'grail' ## Esto se establecerá de forma predeterminada en {rule [index] _rule [name]} si no se proporciona 
    tipo: 'external' 
    source: 'instance1' 
    description: '{match [field1]} {rule [name ]} Descripción de la muestra ' 
  
    severity: 2 
    tags: [' NMAP ','name'] 
    tlp: 3 
    status:'Nuevo' 
    follow: True
  ```

  Si lo desea, los campos de datos coincidentes se pueden asignar a los tipos observables de TheHive utilizando el formato de cadena de Python en el archivo de reglas:

  ```
  hive_observable_data_mapping: 
    - dominio: "{coincidencia [campo1]} _ {regla [nombre]}" 
    - dominio: "{coincidencia [campo]}" 
    - ip: "{coincidencia [campo_ip]}"
  ```

  ![img](https://lh6.googleusercontent.com/75XyWSaDrhoM6nnssHIZNkxyCKZu6w7WxhGSyfWdl2Fpf7_VuREbq8stpOCuSeAPeauokRY0gY0UZOJZON-hrjC9RN4GfNkrWpr0-zX454Rdvc5HpWLhaSlUFlv73t3CiU76jEey)

  Después llamando a python3 con el servicio de **ElastAlert** y el fichero de configuración procedemos a trabajar.

  # Grafana

  

  Es una herramienta OpenSource con licencia Apache 2.0 que fue anunciada el 21 de enero de 2014.

  Tiene el objetivo de monitorizar diferentes aspectos del servidor como de fuentes externas usando dashboards.

  Por ejemplo, podremos observar bajadas o despuntes de nuestros gráficos según el comportamiento del servidor.

  También nos será de utilidad en el factor empresarial, ya que nos permitirá controlar la actividad de empresas en la red, como tener el listado de que direcciones IP se comunican con dicha empresa y a través de que protocolo.

  

  ## 1.1) Grafana Cloud

  Existe esta funcionalidad pero aun no la hemos tocado.

  

  ## 1.2) Grafana Enterprise

  Versión comercial que nos permite usar data sources de pago como por ejemplo **MongoDB** o **Oracle Database** al ser dedicados estrictamente a empresarial.

  En un termino resumido seria la misma base que conoceremos de Grafana en esta documentación con más **características extras**.

  Puntos ventajosos de esa versión:

  - El soporte será muy destacado -> 24x7x365 

  - Administración de cluster

  - Escalable, ajustándose a los volúmenes de datos requeridos por el cliente.

    

  ````href
  https://grafana.com/docs/grafana/latest/basics/
  ````

  

  

  # 2) Que es un DataSource?

  

  Es una fuente de origen donde Grafana podrá extraer información y ser mostrada en los dashboards.

  En otras palabras es un punto de conexión donde Grafana necesitara saber como llegar al datasources para posteriormente conectarse y empezar a analizar los datos.

  Algunos de los datasources que tenemos gratuitamente son **MySQL**, **PostgreSQL**, **MongoDB**, **ElasticSearch** o **InfluxDB**...

  

  <div style="display:flex">
     <div>
         <img src="https://lh5.googleusercontent.com/xqsVjdDODhUMqSEZhdhaYQRsJycmvguJVjFdF6duN2iVRf22DxvG50Rq2B4mtG4OJ3uDlco0M01TUv3xz7OM732gS-EsnxNVZEJy4Y3RuTcK5X0cDmbcHduRDF8ZBy0z_xC1964wbXE" width="60%">
      </div>
      <div>
          <img src="https://www.gokhan-gokalp.com/wp-content/uploads/2018/02/elasticsearch-logo.jpg" width="60%">
      </div>
  </div>

  

  


  # 3) Dashboard vs Panel

  **Dashboard** -> Donde almacenamos los datos extraídos de los datasource.

  **Paneles ->** Donde podremos elegir que datos queremos y cómo los queremos (usando tipos de visualizaciones), para ser almacenados en los **Dashboards**.

  ![img](https://lh6.googleusercontent.com/DifUAttnwp2entvNSLWf-dcSYlAIF69W_QYBTlsVTkv5UtTgvCX8RV2OX_HYFeGzb2oWvAdlOaAOO1BTVz4MBl0oCzlfxVcOB28ajLTlIdv55DGx3hWx64ZQvYNXGoTlE3YbMo0MnSo)

  

  ```href
  https://grafana.com/docs/grafana/latest/dashboards/
  https://grafana.com/docs/grafana/latest/panels/
  ```

  

  # 4) Queries

  

  Es el idioma utilizado para que podamos comunicarnos con nuestros datasources.

  Podemos hacer un total de 26 consultas por cada panel.

  

  ## 4.1) Editor de consultas

  Es el apartado que nosotros podemos escribir nuestras consultas personalizadas según el datasource que hayamos elegido.

  Esto seria un ejemplo de **Query Editor** basándose en el datasource **InfluxDB**.

  En pocas palabras, **InfluxDB** nos permite extraer métricas de nuestro sistema, como el consumo de CPU o memoria, procesos que estén corriendo, etc..

  


  ![img](https://grafana.com/static/img/docs/queries/influxdb-query-editor-7-2.png)

  

  Por cada datasource que escojamos tendrán diferentes sintaxis de consultas.

  Por ejemplo, en caso de que elijamos **PostGreSQL**, podríamos poner lo siguiente, debido a que está basado en SQL.

  ```sql
  SELECT hostname FROM host  WHERE region IN($region)
  ```

  

  ## 4.2) Selector de DataSource

  

  Es una lista desplegable que tiene el objetivo de escoger el datasource que previamente te hayas conectado a partir de Grafana.

  ![img](https://lh4.googleusercontent.com/-mscA8Wc8o8cnF3gsd5afbHGYCBRzFosIAAcSziAMF3L5BwdUQcEyGHBUXraZo1aG_8AdguSCTNdjEyd2jZjSyR623cAQMH5gknNXHMq0GnWetXRkCJ5hDAgSmvI3ws_40YPWg-g)

  

  De forma adicional de los datasources que hayas configurado en Grafana, existen tres principales que vendrán por defecto.

  - **Grafana** -> Tiene el propósito de ser utilizado para hacer pruebas de testing de datos aleatorios que son inventados por la misma aplicación.

  - **Mixed** ->  Nos permite realizar consultas de múltiples datasources en el mismo panel.

    ​	Por ejemplo, con **Mixed** podemos tener una consulta de **MySQL** + una consulta de **PostGreSQL** juntas.

    ​    En relación al orden de las consultas,  obtendrá el datasource que hayas escogido previamente antes de **Mixed** y la segunda query el nuevo datasource añadido.

    

  - **Dashboard** -> Tiene el objetivo de  agregar los resultados de un panel en el mismo dashboard.

  

  ## 4.3) Opciones de consulta

  

  ![img](https://lh6.googleusercontent.com/H4t55mW4iBi2UWhV1Z4tkjEAh5D8NkAJjsAbu_d2t_0LOYOxy74r9hgRnBYxW9ch8SvuaUldJQQHV_Yu3Gpc31m9uqSJpOoc_-FXP9H1ULI8CmKFJ7zSeP5L2_IWXgslES0ovraN)

    

    Grafana establece de color gris oscuro los valores que viene por defecto con cada opción, y de color gris los que hayamos modificado nosotros manualmente.

  

  - **Max data points** -> Nos permite limitar la cantidad de puntos de datos que serán escritos en nuestro panel.
  - **Min Interval** -> Permite indicar la frecuencia de tiempo mínimo que los puntos serán dibujos en el panel.
  - **Interval** -> Indica el tiempo que irá agrupando los puntos. 
  - **Relative time / Time shift** -> Nos permite mostrar métricas de franjas de tiempo o días concretas, en la imagen de arriba, nos mostrara por defecto los datos de hace 1 hora.

  - **Query inspector** -> Podemos ver la consulta solicitada por nosotros enviada al servidor y la respuesta.

  

  ## 4.4) Lista de editor de consultas

  

  ![img](https://lh3.googleusercontent.com/uBDqn6gZkU1hkR4SPrPhrlf5BBuYbw6jgAZ4om02m65yv1gSamzPeyobYCKARmfFH10T3q_FeXwC4QXCnH4RWqxinRZa9fNSJbtd72YP2BWhIx_-kYCM6MwvV9nS5E06YEPjs2QI)

  1. Nos permite duplicar una consulta existente.
  2. Permite ocultar la consulta para que de ese modo no sea ejecutada por Grafana.
  3. Elimina la consulta.
  4. Permite ordenar las consultas.

  Links

  ```href
  #Consultas
  https://grafana.com/docs/grafana/latest/panels/queries/
  ```

  

  # 5) Instalación en Docker

  

  El primer paso que haremos será obtener el docker-compose de Grafana.

  ```yaml
  version: "3.8"    ##Version del esquema de docker compose
  
  services:
    grafana: 
     #Imagen de Grafana con la version 7.5.7
      image: grafana/grafana:7.5.7
     #Nombre del contenedor
      container_name: grafana
     #Usuario con privilegios de ejecutar el container
      user: root
  
     #Puerto expuesto de Grafana
      ports:
        - "3000:3000"
        
       #Volumen para la persistencia de datos
      volumes:
        - grafana-data:/var/lib/grafana
  
      #Declaración de red
      network_mode: bridge
  
  #Declaración del volumen
  volumes:
    grafana-data:
  ```

  

  Finalmente, verificamos como realmente Grafana esta corriendo sin problemas, a partir de **docker ps**.

  

  ![img](https://lh6.googleusercontent.com/BQXfNjzJRIccoX5SIa30LVfYKJNnaTi9x7xVy639S5ragNcNO1f0WW06MreXrVicqc7vy_NjgIZq-90jJP7Qngv0tjpCssrcJ1Uzvlbmw0V3Ou3OHQJnqMGyMn1NSFBCp8nyLYQ7)

  

  A partir de aquí, podemos acceder a Grafana a partir de nuestro navegador, escribiendo http://@IP:3000.

  Principalmente, tendremos que acceder con el usuario **admin** y contraseña **admin**, que en el paso siguiente nos obligará a cambiarla por una más segura.

  

  ![img](https://lh3.googleusercontent.com/pZ9kJVuiJe7obMUi0NpJqOkDyUIkRwfTKHOcqxr_EtwDbW6rK0_JlSAhF74XIaWyGsHjDYsALeqaEv3jN2JRmS_S42Ia56l2UCOSmpBVtUKUft2Dypq5estHFYI-a9eY2k-huPMq)

  Por defecto, vendrá con http y el puerto 3000, del cual ambos pueden ser personalizados en el fichero **defaults.ini** de dentro del contenedor de Grafana.

  

  

  # 6) CAMBIAR CONTRASEÑA

  

  ![img](https://lh3.googleusercontent.com/BgVJPZK_fnV8V2PdYybszC19LQYvD6HWvB1gxuAWZvCDKR6ijcACt5t8Sv50gbPYruOMmq3Og3eIogwQ_oat5kU5B_bzvOfkh_z4UplyZC92RIVgY4QMNTXQYS0cgM8RgVpG76G5)

  

  

  # 7) ASSEGURAR COMUNICACIONES

  

  Primero, vamos a generar la llave privada de la CA para emitir el certificado para Grafana, teniendo una longitud de 4096 bits.

  ```bash
  openssl genrsa -out grafana.key 4096
  ```

  

  Antes de crear nuestra petición de certificado y posteriormente firmarlo, pondremos un nombre de DNS en **/etc/hosts** para el **CommonName**.

  


  ![img](https://lh5.googleusercontent.com/X4UqhHahg8ZU-FpMpAZxp9jm-hOImMnauT0eJCPdNwnIJw_y0IOceU6CIxjQVzQo6f8RbZSN689BmkPm6whYE148uVy4f1u7IdC3XpxNPWytI_nxL0_3xekre2IRGedBtNtJwqQ_)

  

  A continuación crearemos la petición del certificado con extensión .csr para Grafana indicándole cual será la clave privada que tendrá la misión de generar la petición.

  Esta petición de certificado tendrá el objetivo de mostrar al usuario final que Grafana es una entidad de confianza para poder conectarse a ella, añadiendo información que se asocian con dicha entidad.

  

  ![img](https://lh5.googleusercontent.com/0H-i8Rnr7EJo-hUQKHZB6mGfaZBL5KQcozsMvTdbRhYO907S6yDjDRcE9J1kVd5dWhcEIkAazK24hV7w_eZXvdHxzIBDCshWAR-3HFlBFX-OigyGxmELhUmCqdRZ0Sw8fOJ6T53J)

  

  **Importante** -> En el campo **Common Name** hemos de indicar el nombre de dominio para Grafana que hemos establecido anteriormente en **/etc/hosts**.

  

  Realizado la petición de certificado, lo deberemos de firmarlo para que se genere un certificado oficial de la entidad **(-out)**  con nuestra llave privada **(-signkey)** para que de ese modo sea utilizado por Grafana.

  Dicho certificado que se va a validar tendrá una duración de 1 año **(-days 365)**.

  

  ```bash
  sudo openssl x509 -req -days 365 -in grafana.csr -signkey grafana.key -out grafana.crt
  ```

  

  Una vez, tenemos listo tanto la llave privada y el certificado, debemos moverlos dentro del contenedor para añadirlos en el fichero de configuración de Grafana.

  Entonces, una manera de hacerlo es utilizar el comando **cp** de docker o bien mapear un punto de montaje de nuestro sistema local hacia el contenedor mediante docker-compose.

  

  En nuestro caso, lo haremos de la primera forma.

  Con lo siguiente le estamos diciendo que la llave privada que se encuentra en el directorio **/etc/ssl/private** y el certificado que esta en **/etc/ssl/certs** se copien al directorio **/usr/share/grafana** del contenedor.

  

  ```bash
  docker cp private/grafana.key grafana:/usr/share/grafana
  docker cp certs/grafana.crt grafana:/usr/share/grafana
  ```

  

  Entramos en el contenedor de Grafana:

  ```bash
  sudo docker exec -it grafana /bin/bash
  ```

  

  Seguidamente, cambiaremos el propietario de los dos archivos y los permisos

  ```bash
  chown grafana grafana.crt grafana.key
  chmod 400 grafana.crt grafana.key
  ```

  

  Dentro del contenedor nos ubicamos al siguiente fichero que será donde constara toda la información personalizable de Grafana, haciendo que sea de utilidad de que queremos permitir la conexión HTTPs y añadir tanto la llave privada como el certificado.

  ```bash
  /usr/share/grafana/conf/defaults.ini
  ````

  

  Lo abriremos con el editor nano, del cual si no esta instalado con nuestro contenedor la instalaremos con el siguiente comando.

  Utilizo apk debido a que el contenedor esta basado en una distribución de **Alpine**.

  **apk** seria el paquete de repositorio como **apt** en Linux y **add** seria como **install**.

  ```bash
  apk add nano
  ```

  Dentro del fichero, filtraremos por la directiva **[server]**

  

  ```bash
  [server]
  protocol = https  #Habilitamos protocolo https
  cert_file = /usr/share/grafana/grafana.crt  #Indicamos la ubicación del certificado de dentro del contenedor
  cert_key = /usr/share/grafana/grafana.key   #Indicamos la ubicación de la clave privada de dentro del contenedor
  ```

  


  Finalmente, para que se apliquen los cambios reiniciamos el contenedor

  ```bash
  docker restart grafana
  ```

  


  Como resultado, podemos ver si accedemos al navegador a Grafana ya admite el protocolo **https**.

  

  ![img](https://lh6.googleusercontent.com/SVpsvBBzJj7SrebZV0NUt0AFUw5twCMhvR2Ci3btqoj5i93h1xG73pZFfwGUO6zqrfHrpR8ia3q8Jas6dY0Iy8G9I5w5ta4tuAraIemgmk3rZfxxJRlyPaPludIZ5UCRC6rmS5Lx)

  

  Links

  ```href
  #Imagen de Grafana
  https://hub.docker.com/r/grafana/grafana/tags?page=1&ordering=last_updated
  
  #Copiar archivos locales a un contenedor de Docker
  https://linuxhandbook.com/docker-cp-example/
  
  #Configurar SSL en Grafana
  https://www.turbogeek.co.uk/grafana-how-to-configure-ssl-https-in-grafana/
  ```

  

  # 8) RECOGER DATOS DE MYSQL

  

  ## 1) CREACIÓN DE LA BASE DE DATOS Y TABLA

  Haremos que Grafana pueda monitorizar los datos de una tabla que disponemos.

  **MySQL** es un contenedor, accederemos a el usando el siguiente comando:

  

  ```bash
  docker exec --user root -it so-mysql /bin/bash
  ```

  

  Dentro, ejecutaremos el comando para conectarnos a la base de datos

  ```bash
  mysql -u root -p
  ```

  

  Creamos la base de datos.

  ```sql
  CREATE DATABASE SIEM;
  ```

  

  Creamos la tabla, que tendrá el objetivo de almacenar algunas de las amenazas que se encuentran en nuestra base de datos **SIEM**.

  


  ```sql
  CREATE TABLE amenaces ( 
       id int, 
       nom VARCHAR(30), 
       quantitat int, 
       data TIMESTAMP DEFAULT CURRENT_TIMESTAMP, 
       PRIMARY KEY(id)
     );
  ```

  

  El campo fecha irá recogiendo de forma automática, el día y hora actual que se va almacenando la amenaza. 

  

  Para insertar una determinada amenaza haremos servir la siguiente instrucción:

  

  ```sql
  INSERT INTO amenaces values (1, 'Phising', 2, now());
  ```

  La función **now()** escribirá el momento actual que hemos insertado la amenaza.

  

  ![img](https://lh6.googleusercontent.com/k7PFArihuv2NSkl2ByDHWVipHkvVhO4tATMwt2yO7uq6qg8CE0qyXHhSPHu7ilvqTvVJWK5ggu_Koq_F2NB56RjqY2DRkrL5ORf3couBR6WUNfaBzQruI3Q182z1bbhTOzFBloTxz4k)

  

  ## 2) CONNEXIÓN AL DATASOURCE

  

  Vamos a **Configuration** y añadir un **Data Sources **.

  Por defecto, podemos ver que disponemos de un **Data Sources** que es **InfluxDB**, esto es una base de datos que permite almacenar métricas.

  

  Para crear nuestro **Data Sources**, le añadimos a **"Add data source"** 

  ![img](https://lh6.googleusercontent.com/Wl1IKncF_51j5ufVlprXVWZXoEXCSIN54ocQT5S29t4JqdgjAFCHwPqUcQCuvRcugkTSKrnHjg6x65dsgFW7IMMJl1xFcYz4Q-Lu04GvAC4Jlyq72bKbcUzCDeoe2x6nTV4EqjdB)

  Seleccionamos MySQL

  ![img](https://lh3.googleusercontent.com/0pm0hm3F2142aaplIcXObhVrX1s19qNidHjiceUAr91ckLtuB3OrT04905cr9gIsN5lTIsJ4j_eNq5nm9pQbBGAfvvXFzO4SZJO_iMojSU7ZfPd3rrQZQAAuCMmGnemfAljSKpv2)

  Requerirá de un nombre para la conexión, y los datos del contenedor.

  ![img](https://lh4.googleusercontent.com/XffLDDdBGLjctzs3R57jZu2eNH-UmdStDWlc6eaNKcV6Zd7onD6S0JXVLDqAgJnSZEhJjak8iImSfavFEzPBq5HW8xiN7IqcVR6qkpsZ28LoKnRGOjIPq9b4-3brLhui_oI3CAKo)

  

  Finalmente, ya estaremos conectados a nuestra base de datos y solamente lo que tendremos que hacer es guardar la configuración de nuestra conexión.

  ![img](https://lh5.googleusercontent.com/ZPMdmmrsfg36jfnpp2afX4KMJs-3AXO1gVKsI1QtyDYL8RnFm32XugGULW5PAPOKq4IkqsKb4zjjVi7N5axTjWnp9x1XJJ8jtoxRR6DTWDuegOqqbPaaRcp4HMzvAuUH_QE4Of2f)

  

  ## 3) EXTRACCIÓN DE DATOS

  vamos a crear un **dashboard** para tener interacción con nuestros datos, y a continuación el **Panel** que contendrá cada uno de los datos de MySQL.

  

  ![img](https://lh6.googleusercontent.com/9fXh4ngLgM-BhGdjwNTACCL4GNgvKHvVlk5iqRPxuS-srIDRiopDC0xXoitNdFxEzMOCDMmyg2XFYZKZDh5iHmx8LVylyXzr1de2nmVPRqjHJnseOWm6p3k225Q12wu4twYP1V03)

  

  Escogemos nuestro **Data Sources** de MySQL.

  ![img](https://lh6.googleusercontent.com/FGniM8wmZtAPf1yMNYMU9Sjq6D2ty571VsZtTO8YFLmsORoTQ201igHOEqvi3_tfngOdEBsvhyCjJLSmGex2DzApFuwO_KN0PHkh5Ab4sxgRh064pfphquhC6LxqVfiKFdf2tY4c)

  

  Una vez nos conectamos a la base de datos, podremos hacer interacción con la tabla a partir de una consulta SQL.

  - **A** -> Es la letra que identifica cada consulta dentro de Grafana, si tuviéramos mas consultas serian identificadas por una letra superior, por ejemplo la consulta 2 se identificaría por la B, la 3 por la C, etc.

  - **FROM** -> Indicaremos la tabla que queremos extraer los datos. 
  - **Time_column** -> Indicaremos la columna que Grafana comprobará para mostrar los datos por su rango de tiempo.
  - **Metric column** -> Indicamos la columna que contendrá el nombre de los ataques.

  Debe ser de tipo **string**, por ejemplo VARCHAR, CHAR, TINYTEXT. 

  - **Column** -> Indicamos el valor que queremos visualizar en nuestro panel. 

    

  ![img](https://lh3.googleusercontent.com/UQW9M0bfuneeyUYDSFPtyRHzHAPa9cj9S5C03MbuGUgkF16H_uqGmNHWsnrJgt-V8k8ClVHWyg6JhjucjjFrj6lR5ZJrNajSKoDA3uVBPDC-w-G82Zs_iJENsVxAwRqJU6IQxxso)

  

  A partir de este momento, ya dispondremos de los primeros datos obtenidos a partir de la tabla.

  Podemos visualizar que se generan los nombres de las amenazas como **Metric column** y que hemos seleccionado por la cantidad de estas amenazas.

  Sin embargo, podemos cambiar el dashboard por otro más adecuado para nosotros. 


  ![img](https://lh3.googleusercontent.com/wwCOS9WmA5X1qCNU4nr_Xwp1O6StuAEhbF5EAmuFaX_G6hvHi9Kfh2wtZl8vcvPTjmI77eS8mrPgKGVY6cVy0qt1CaPs-iRPDbqxkY6RzH2j78nscXs6Xpo0xELVyIGTa2Ik9F-8)

  

  Entonces, accederemos al menú **Panel** ubicado a la derecha del dashboard y después a **Visualization**. 

  ![img](https://lh5.googleusercontent.com/w4RipwS1Ft33aSW-x4LeqARUiAkvN234SaRcn-51GgskuipkTR6xIzv9JZfJ6XVYw6g88SJsXYJYBfkltxh4qvEzjSFipYCDY2M6z5--_e7M_0mlUIpN-Pr2H8ZGVoYVuMgcaYc0)

  Si escogemos el dashboard **Dashboard Gauge** se verá de la siguiente forma

  ![img](https://lh4.googleusercontent.com/D-HMiAcIOlfupbdugJ6OiAtNYVglrP5GwO64WWi3nC9y3fY_4mzFmRe2a_iqdsXn9-0dOM_ZMavBCWaaP4HJFaaqZrDbo2CgEBzPYRXk_sPChvWw-Yr1vW8Ed6tvqqukPc7xMUeu)

  En el caso de que lo deseamos ver con barras, optaríamos por el dashboard **Bar Gauge** que nos mostrará de una forma más clara, cuál ha sido la amenaza más y menos detectada. 

  ![img](https://lh3.googleusercontent.com/3T_6jHh_AkZ9fS4iFLgbpt6hm-k6n5m6xkDZnp8hpzfI3fy4TignVNlQO6_byubxKgLBv4qvAwhuaG56XwekNdUzZx7L6n8JKRmx3iUMPI6amVxASkYTtNAC9OBJyxnbvll4H2cF)

  

  Por ejemplo, también podemos cambiar el modo de visualización, yendo a la pestaña de **Display**. Para que se vea más agradable, podemos aplicarlo con líneas, como tambien establecer una mida de las líneas.

  ![img](https://lh3.googleusercontent.com/MT94xOR91ZuqITQ_Zgih0TUyFGDkrIm3ep9WKDXh3sZxqqg_pGgkRjdOqH0FhX-CvGPOKwbKSq0t69nNFXdNGP41iIXqeo4iXqWKKQieGaWTsx25LPmvF2XB5d0aBUKeSe0Ev5nF)

  Además de esto, también podemos consultar la cantidad de una determinada amenaza.

  Esto se puede hacer en **WHERE** aplicando la expresión **Expr: campo = string**. 

  ![img](https://lh6.googleusercontent.com/Imv3uU5-dE9Nk6H9iWTifEp4Nw__5U8r7FuQZztWZCWGsyMXfEEsRdUgESPSrWkkzTig3G08Q6bnqzVyNp4Uylt6dxufDOlQMua5MW5zUZqARz8PXkt81OXvT9E0NGVUqFTR6Z3k)

  Ahora imaginemos, que aparte de extraer los datos del ataque de **Fuerza Bruta** también queremos hacer una segunda consulta para el ataque de **Botnet**.

  Entonces, esto se haría mediante el botón **+ Query**. 

  ![img](https://lh5.googleusercontent.com/fs_tJIzOY8gHqYgethqh8V8XalBzB7r5F9RMVmqbHzE_d_YmlaxnTpRqmnGAz7OYVIdUu6a8y8WTiz_ukxl7UCIAjWO1EWyoNx4cBS-GPSuc54dv98ICZ0iaT52QrmM_f9mGJQHk)


  ![img](https://lh5.googleusercontent.com/BcuYCYEaZMS3wfYUH-mj0WTvrN8DPALyplbCrXZ-hMvILkpgJV850Cs-xjMpKagYyhMYe3ZuBweCy51uWRNzMxoiEAkedU1fiTBCdKjLJswQaoHg4hAM7DEfWSNO4Nq6rfMqBHrj)

  Si volvemos al dashboard **Gauge**, podemos ver cómo únicamente se encuentran las dos amenazas **(Fuerza Bruta y Botnet)**.

  ![img](https://lh5.googleusercontent.com/hHfWbu9lT42UEceycfZDtwiB1IfN9SfveeNsXwazRPiqxtylcAHpxKSEJCoxknlQvTT4rGd39llJBY5P-6GuDDQyRiqOjTHPaMA5ZViqK-Kq_Db-cLOd6TDE4ORq57hm0JuDgCnX)

  

  Finalmente, para almacenar los paneles para que se encuentren en nuestro dashboard, le daremos a **Save** y despues a **Apply**.

  ![img](https://lh6.googleusercontent.com/B2jaZ7Wm0oY8klDFnK_g70nKY71M0IDdDHt6SSoAoF92FJGkrTJF8RDvaEhA3kuMOdCP5MSMw4yPJRhBkaJ0tqI-wjL1aVs3NNaL1-GNBZeoiq-b_uE3-mf8tVkvmk0HvvtyYfla)

  

  Como resultado final, tenemos los paneles que hemos ido creando.

  ![img](https://lh4.googleusercontent.com/BneyZdP9V0XZhE07UDI32ITOJqZ_TjSGgOY3_-DY_IqdsMAy6rHq6-O8MYngpTUr7XyAu8EuW4Ltx4PVzuv3CI-nAWGMPmcUpcfzZ3Gho4cpewHtQCfkLK_zNmMc_nmP6RCQeOTo)

  

  # 9) ALERTS

  

  Grafana nos permite controlar el comportamiento de los valores recogidos por los paneles a partir de alertas, haciendo que si un valor anómalo es anómalo nos avise.

  Esta característica solo se encuentra disponible en los paneles de tipos **Graphs** o gráficos.

  Como primer punto, hemos de saber a que cuenta se enviará la notificación, por eso vamos a **Alerting** > **Notification channels**.

  

  ![img](https://lh6.googleusercontent.com/qtUD0NBbTbE9SM8VS6aFNLtx7La3LpyUtbLD9O-_XO0QD5jFXLWE3j2ZL0hSewQsi-DLqXJDhtGTxSbfTbERP8AAuHdeIlsQjjfpI7mSFTr5g8lVFaXtL4B2aB_orgqjKQ2Jyw9O)

  

  Dentro nos ofrece varios tipos de canales, como **Telegram, Hangouts, Discord**,  entre los más conocidos.

  En este caso nosotros lo personalizaremos porque se envíe a una cuenta externa de Email concretamente al de **Gmail**.

  

  ![img](https://lh5.googleusercontent.com/6KEtiANUWrRUVVa5NGWKCIXI7L_9e-T6qSwlcFp9Ib3dFnK83uFGNahWGoj2Lwr0-B-5M57utrNymIqOHyBWI5NLGZTI_8ePdEyoXNP1BnIRnfC-Yzf4OewVPAOBtL7WHZI6hp6D)

  

  A continuación le daremos a **Save** para almacenar nuestra alerta y después a **Test** podremos ver que nos saldrá un error indicándonos que tenemos que hacer la configuración smtp de gmail dentro del fichero **grafana.ini**.

  ![img](https://lh4.googleusercontent.com/O0lvQ5rPMytWOMj8r5ORTqvT9-bxVp8kMALMiWD6bIR9AzahdpL_cN0pTS1aitZCWJtpu1VIuvAQwu5j3YDT2ikVrCVrMV_TBWPBnpl5FSGpHmn-z9mOWkSN6WRw-QfeHPZcjYLY)

  

  ```ini
  #Abrimos el siguiente archivo con nuestro editor nano
  /usr/share/grafana/conf/defaults.ini
  
  #Localizamos el protocolo [smtp] y modificamos las siguientes línias
  
  [smtp]
  #Permitimos el envio de mensajes
  enabled = true
  #Indicamos el nombre de host de SMTP de Gmail mas su puerto
  host = smtp.gmail.com:465 
  #Indicamos la cuenta que obtendra la notificación
  user= javi.ubeda.grail@gmail.com 
  #Indicamos la contraseña de la cuenta
  password="{PASSWORD}" 
  #Indicamos la cuenta que sera donde se enviara el mensaje
  from_address = admin@grafana.localhost
  #Indicamos el nombre de la cuenta de origen
  from_name = Grafana
  ```

  

  Reiniciamos el contenedor


  ```bash
  docker restart grafana
  ```

  Aceptamos el envió de mensajes de aplicaciones desconocidas

  ```href
  https://myaccount.google.com/lesssecureapps
  ```

  A continuación vamos a  **Dashboards** > **Manage** y clicamos sobre nuestro dashboard

  ![img](https://lh3.googleusercontent.com/E6HJwnUrZbFErA6_XwS23anwPho1ioiagMVCdY7tkiAGBO4fW4zFmRX66E-_LxbK-1SYrHFhsYsbhCk2zYxi-4xFZJiSYT6WgHEjLq4HEHSfXyX7YpVLdzMJRxdRQ7AKphzvGyvs)

  

  Vamos al grafico y le damos a **Editar** para crear nuestra alerta

  ![img](https://lh6.googleusercontent.com/urs5YqyZpUcAXup7YX-o3SmMG0F3_OTBfrfIkBZ4Pu2ZUydqM2odChOrhMaJdPraI-geevHjGgLuv8m_BJl0-y8G716R-9D_iUny09LQxeHbFvc-_gDFz9DD9VQyhsT--nO5fmKc)

  

  Después, nos ubicamos a la pestaña **Alert** > **Create Alert**.

  ![img](https://lh6.googleusercontent.com/yRIqaV4p7D6FI7EJJvnWvSiZRTbyiVN8ROGfLtvQw8RNvpz8Iw6cIUGqDxCpG1XzOQfGR154vt1VOypUaEP8VhU_Q6lL6ldhUZCrAsXS65Ye2x0bzmW6-DGizX0wgpXAepNpuHey)

  

  ![img](https://lh4.googleusercontent.com/HIteB4mkKldhQ5yOAj0FltsUGZNzKMCxqwDHXVUlYi22yCkTkbry18jd3E8AfPEWb6JdaDvOPKzSeLcLMw4SFPdOvN8j-0hPXXGfsb0d3e5gAKCAJEkIevuox75iNd4eWSReZmm7)

  

  ### 9.1) RULE

  - **Name:**  Nombre de alerta
  - **Evaluate every: **  Especificamos cada cuanto tiempo queremos que la alerta se evalue. 
  - **For**:  Especifica el tiempo que durante la alerta sera evaluada, una vez acabe ese periodo de tiempo, la notificación serà enviada a nuestro correo.

  

  ### 9.2) CONDITIONS

     En nuestro caso vamos a elegir la función **max () **:

  ​	Con esto le decimos a nuestra alerta que encuentre los valores mas altos de cada amenaza para poder  	ser evaluados y que se cumpla la condición.

     Otras funciones que tenemos disponibilidad:

  - **count()** -> Nos permite saber la cantidad de veces que aparecen las amenazas en la tabla.

  - **avg()** -> Nos permite obtener  la media de todas las cantidades de una amenaza.

  

  ![img](https://lh4.googleusercontent.com/pLLLyfpUuHuewP6USqUK_SOP3WhCtVClb5APnwsdvZ8jd9w_gkZ9a2dli6LxbAA3uTKFDZI9AktrkTzViqqt8gx3heirPuRfn13pypgYeIj2YVYKAvIFuj4XTlXOPkkQTkp2AfwP)

  

  - **query(A, 5m, now)**  -> La letra **A** define el tipo de consulta que se ejecutará, **5m y now** serán la franja de tiempo que se evaluaran los datos, es decir des de hace 5 minutos hasta en este momento.

  - **IS ABOVE** -> Indicamos que localice los valores que estén por encima de 10.

    

  **No Data & Error Handling**:  Indica a Grafana que tiene que hacer
  en caso de que la consulta anterior devuelve valores nulos.

  Tenemos diferentes estados:

    - **No Data** -> La alerta pasa a **NoData**

    - **Alerting** -> En caso de detectar valores nulos, enviara un estado **Alerting**. 

    - **Keep Last State** -> Se mantiene el estado de la alerta.

    - **Ok** -> Indica un Ok cuando no se cumple la condición.

      

  - **Execution errors or timeouts:** Indica a Grana como controlar los errores de ejecución o **timeout**

    - **Alerting** ->  Establece el estado de la alerta a **Alerting** 

    - **Keep Last** -> se mantiene el estado actual de la alerta, sea cual sea.

      

  - **Notifications**:  Indica a Grafana a que destinatario enviará la notificación y qué mensaje será escrito para hacer la alerta. 


  ​    

  ![img](https://lh4.googleusercontent.com/jAYjCdOhSxQoHRIrq0PnMI9m8HxTXVQTZh7WAy33JJMLTotXwyRJk2vJJPxYUoqPYquKfwxtfG2y5YR8RyKxyoJE3HjcScvvZ0KrOtJWuH1Sc1bIPJ9lHUAjz97oWAgOQ4qBuHTf)

  

  ### 9.3) TIPOS DE ESTADOS

  En Grafana disponemos de 4 tipos de estados principales,  según el resultado que haya verificado la alerta después de comprobar nuestra condición.

  

  ![img](https://lh5.googleusercontent.com/r1H3SFGPHol58XDlNuV-PRkG3yKZVcsJzd-CN7A3_JK-S6Zq4_VLqbEZKMCIs46aaIwAC-ZGHTxubj3h-1VBle2TZm-0jUAT4OYe3VVCBl7ciHGECZM89xAObG_pFTDAaw9D_xKw)

  

  Basándonos en la tabla amenazas:

  ```sql
  id    nom        quantitat
   1   Phising         2
   2   Troyano         4
   3   Botnet	         6
   4   Fuerza Bruta    20
   5   SQL Injection   14
   6   Ransomware      8
   7   DOS             14
   8   Spyware         1
   9   Whaling         1
   10  Speark Phising  5
   11  Rootkit         1
   12  Thread          7
  ```

  

  - **OK** -> Se mostrara cuando una consulta no se cumpla, por ejemplo si queremos enviar una notificación de las amenazas que estén por encima de 20 (Fuerza Bruta), no habrán resultados que coincidan.

  - **Pending** -> Es el estado que ha detectado que existen coincidencias con la consulta y la esta evaluando a partir del tiempo establecido en el **For**.

    Por ejemplo, cuando en nuestra consulta anterior, le hemos dicho la cantidad de amenazas que estén por encima de 10, si que se cumple, ya que estaría **Fuerza Bruta**, **SQL Injection** y **DOS**.

  - **Alerting** -> Es el encargado de enviar la notificación al administrador una vez finalizado el estado de **Pending**.


  - **NoData** -> Es cuando existen valores nulos y la condición no puede ser evaluada.

    

    

  Para ver que estado nos sale a partir de nuestra consulta, le damos a **Test Rule**

  - El campo **state** vemos que se ha cumplido la condición, ya que esta en **pending**.
  - El campo **matches**, vemos todas las coincidencias que han habido, en este caso existen **3**.

  

  ![img](https://lh3.googleusercontent.com/9l2nVXbTEu-UuWpndBtoAfYu_xZe6CrCJseD9hUwdBfnpN1Sqap4QHLl-H4PavTwoSzDszzKXB-23i7jzhZKTb3FnN9G2bgwkz-2_x5Nf8IfkY8pIcy9K6cix3UThpukADKu-tYt)

  

    Otra forma de ver el estado que se encuentra la alerta es partir del apartado **Alert Rules**.

  

     ![img](https://lh5.googleusercontent.com/eNsVsUn0HmaZZReR4U1_WrdMXdYYWpYFHhKzmDWUrhGMvdscP1MklTman6hm5UTzYo6NDesEJmNL6uin5r0wuR0y0sUISd9UfIpTDkD_f-v0mqQ9fUB_64i8CZnqNk0G_QI1cIaI)

  

  En estos momentos, el estado que ha alcanzado la alerta es de **PENDING**, deberemos esperar a que finalice la evaluación, para ver como se cambia a **ALERTING**.

   ![img](https://lh3.googleusercontent.com/_EvwW-Svqy8XMqYklQgUbd2vWGRmXzif2RN1gUmcqqR3jN7-00v6GyD0KCBYR7vgiASZXuorX4eneq9Vx80DIlK4YB322TolhvFfwh5x4stypW7lzL9ye9DDe5tPHVGtA0Hpth1j)

  

  Pasado el minuto de **For**, ya vemos el nuevo estado, lo cual significa que ya habremos obtenido nuestra notificación por email.

  ![img](https://lh5.googleusercontent.com/YOL-l6-rWYNZxoff-iuFcAaCLBplAlriYvDET92-fWjophuxkLXDnXgiPifqHQs1vQNMzroPEn2rErDHYnkyLJlZhsOVnKieaJtM_ey2wWm-Y9NQn2DRLq_QGfyfUoGzivGcn3BS)

  

  ### 9.4) ENVIO DE NOTIFICACIÓN

  ![img](https://lh4.googleusercontent.com/eTAXN0_ogmHXbZjWdIWq2giypHBmuc0z8q4mZw2N11AjUTuD697NQYAEKmuHs-eYYTgEOQBya99LWNtIWHUDvcnJcHBrT5jjcidT0WtqgVUw4ca9LkMUg-Bk3t4VzD3DyfbQ3uIY)

  

  Links

  ```href
  #Grafana
  https://grafana.com/docs/grafana/latest/alerting/create-alerts/#alert-rule-fields
  https://techexpert.tips/grafana/grafana-email-notification-setup/
  https://community.grafana.com/t/gmail-for-notifications/1895
  ```

  

  

  # 10) RECOGER DATOS DE ELASTICSEARCH

  

  ## 10.1) CONNEXIÓN AL DATASOURCE

  

  Vamos a **Configuration** y añadir un **Data Sources ** para escoger el punto de conexión de ElasticSearch.

  ![img](https://lh5.googleusercontent.com/CaA8-hiofEyn2Mfa8MfFICuga3FaiZ7LhFyxwLxN86erxIlw9d8ezeEY80hXUgG-CRT0LH8HqHTwA1sL12QcJT4QgZ029xgv3IW9obTOxub1ELIaQ8KACmJf6TevuJ18hhplLsAr)

  Seleccionamos ElasticSearch

  ![img](https://lh4.googleusercontent.com/TcoTIto5doTJ545I31vJD5bYsNYpSIlFUGMwjAg3EW4M7wD82mcf_FaYkkq1HsutZYVSctA88ZNCpqj5JHK6Y0fe7N_3EeuBhfEnUTgBiB0EVpOiHOMenHhFpGr3yo5EM35c9Emr)

  

  ![img](https://lh4.googleusercontent.com/py4C_zL1e3r4S6wV2PY09OIrKEmOBPvmMoi_djXm9tTJ5BTKIXYhEgL6YirvToTVk2hW0ZLiFCyqDmsd1eLnCzJXSE67ECqBIFUOtCXYdkL7nQXQR6udFFhbl17Z7DjcUea9z5hZ)

  

  Primero para conectarnos a su data sources ponemos los siguientes parámetros:

  


  - Name: Como se llamará el data sources [Elasticsearch]

   **HTTP**

  - Url:  Dirección que utilizamos para acceder a ElasticSearch  https://10.200.0.9:9201

  - En Access escogemos -> **Server (default)**.

    ​	 **Server (default)**: Las peticiones se harán a Grafana que serán reenviadas al data sources.

    ​    **Browser access**: Las peticiones se hacen directamente al data sources.

    


  **AUTH** 


  Con la primera opción nos permitirá introducir las credenciales del usuario de **elastic** y la segunda la hacemos para que no verifique el certificado debido a ser un certificado autofirmado.

   

  **ELASTICSEARCH DETAILS**

  Es donde indicaremos que índice queremos extraer los datos.

  

  - **Index name**:  

    [metrics-] -> El nombre del índice a monitorizar.
    YYYY.MM.DD -> Año/mes/día que se ha generado el índice

    

  - **Time field name**: Campo que Grafana gestionara para determinar cuando se han insertado los datos de ElasticSearch en sus respectivos documentos.

    Por defecto será **@timestamp**, debido que indica día/hora que se generó los datos del índice.

  

  - **Index name** -> Vamos a monitorizar todos los índices de Filebeat, a partir del patrón **filebeat-***.

    El patrón será de utilidad, ya que es la forma que podremos acceder a los índices de filebeat de **elastic**.

  - **Version** -> Debemos indicar la versión que contendrá nuestro **Elastic**, en este caso es la versión **7.11**, entonces escogeremos la versión **7.0**.

    Que es superior a **7.0 (incluido)** y menor a la versión **8.0**.

    

    Esto es importante, debido a que las sintaxis de las consultas pueden cambiar o no ser compatibles con la versión actual de elastic.

    Por lo tanto, tenemos que escoger la correcta.

    

  Una vez todo este completado, nos saldrá que se ha conectado al patrón especificado donde ya podremos interactuar con los datos.

  

  ![img](https://lh3.googleusercontent.com/hRbWTReCwbKPfMYV-CsHK4dN4YdiHZjXoRAzpmTT9wAeprOIQ7G-Ns3OOver-Q13TUspayP-wPafbKcXl9IV3uvhzpDrlo9kMZGK1lZtYjpqDCsIYrUVqteFV0eR2AZxh-8o1wL9)

  

  

  ## 10.2) METRIC QUERY EDITOR

  

  ![img](https://grafana.com/static/img/docs/elasticsearch/query-editor-7-4.png)

  

  Nos permitirá hacer consultas de los datos de Elastic basándose en la sintaxis **Lucene**.

  Sera necesario un conocimiento mínimo de Lucene.

  

  ```java
  #Sintaxi 
   key:value
  
  ### Ejemplo consulta Lucene
  
   #Muestra todas las detecciones que ha bloqueado Meraki
   
   company_name="Meraki" AND lock_threats:*     
  ```

  

  ## 10.3) CONSULTAS BASADAS EN PLANTILLAS

   

  #### 1) VARIABLES 

  Podemos crear consultas por medio de variables, que nos permitirá cambiar el tipo de visualización que muestre Grafana en su dashboard.

  

  ![img](https://grafana.com/static/img/docs/v50/variables_dashboard.png)

  

  ##### 1.1) CÓMO CREARLAS? 

  Entramos a uno de nuestros dashboards > Accedemos al siguiente icono > Apartado **Variables**

  

  ![img](https://lh6.googleusercontent.com/f-QgYUxmXel4TMx10gx9mMDAHiXYDgF3X1hO6VncJwcpqq9lMUXoMh9i0c7fjKGnJJJDgoHmCMFwaWPMVl1T_jNiehHF0DGuQIJWjnT-6LA2y8wA23LFWoQmohte_gPOBupj016I)

  

  ​	 ![img](https://lh6.googleusercontent.com/vTiJK-52R0TqK1SUX0pu4pdEWCoO35zSR_ynRNtE0gz4Am4XqAU4K7pqE-J94vul4-kkeePCIpIquI07R3nq8ROehsaPkTLb8RdQIh9OcZyS13d3dURDHt5fPQ-KTRUMtWNiKpLW)

  

  ![img](https://lh4.googleusercontent.com/ALyzhHf4cbRlku44LBuiEIr2MKzPLqgp4BGjh1Px0PhQ4Q4RPlHmscZ82YkspFEd6_SDYvN4NcvnG06UlZgz7joIL6_1hYXFXLOOXg-XOi7KUVX1Q-Fj2-oclEZBwiMVnYVTBHn4)

  **Name** -> Indicamos el nombre de la variable que almacenara los resultados.	

  **Data source** -> Donde se hará la consulta.

  **Query** -> Donde indicamos la consulta, en este caso buscara todos los orígenes del hostname del sistema.

  

  Ejemplos de consultas en variables de cadenas personalizadas de **JSON**.

  ```yaml
  #Busca todos los valores de los documentos de Elastic que pertenecen al campo hostname
  
  {"find": "terms", "field": "@hostname"}
  
  #En esta ocasion, solo buscamos 500 valores del campo hostname
  
  {"find": "terms", "field": "@hostname", "size": "500"}
  
  #Ordenamos los valores de hostname a partir del doc_count, que ordenara cada coincidencia de forma descendente.
  
  {"find": "terms", "field": "@hostname", "orderBy": "doc_count"}
  
  #O tambien podemos usar order:desc
  
  {"find": "terms", "field": "@hostname", "order": "desc"}
  
  #Los siguientes campos nos seran utiles, ya que podremos buscar algunos de los campos de tipo "string" de nuestro Elastic.
  
  {"find": "fields", "type": "keyword"}
  {"find": "fields", "type": "text"}
  ```

  

  Links

  ```href
  #Conexión ElasticSearch
  https://grafana.com/docs/grafana/latest/datasources/elasticsearch/
  
  #Como crear variables
  https://grafana.com/docs/grafana/latest/variables/
  ```

  

  ##### 1.2) TIPOS DE VARIABLE

  **Query** -> Nos permite almacenar un listado de valores que frecuentemente cambian su contenido al paso del tiempo.

  **Custom** -> Almacena un listado de valores que sean estáticos o de otra manera dicha que nunca cambien.

  Eje: servidores que siempre tendrán el mismo nombre.

  Para que la variable almacena este tipo de datos, deberemos de especificar manualmente, separados por una coma (en caso de querer múltiples).

  

  Si siempre quisiéramos almacenar el número 2 y 100 en la variable haríamos

  ```bash
  2,100
  ```

  O bien, si almacenáramos el valor de un campo

  ```bash
  myvalue
  ```

   Todo esto se pondría en el campo **Values separated by comma**.

  

  Ejemplo práctico

  ![img](https://lh3.googleusercontent.com/F7ndXBUnyij2W2HNRJOvl4aNKEAldSrk7RDsMrQp0wNhyx2dgQ402oUrQ9Tcdj11z-TTpnt8uArFB-qMOqKJhRNzHshvhZPWu2zpyq4eQwc4S8cJsqSEHe5fIkDZuxAyGtauNfOr)

  

  Como valor vamos a poner el siguiente mensaje que sabemos de antemano que nunca va a cambiar.

  

  Entonces, en nuestro panel podemos filtrar únicamente por el valor que hemos establecido en nuestra variable de tipo **Custom**.

  ![img](https://lh6.googleusercontent.com/ECSpuSWO4CD6N_ZYDdzbCMr_hizjbT222eS5S_KGmmfu81mePKnd4vvWsXrajyrouCfmc32oUMqw3uwQcJwsyDlwUWQ3KosqTn5eODAqNXwUF68YhzKG_dT6bt0sImSjozs77Zgu)

  

  **Text box** -> Es un campo de tipo **input** como en los formularios de **HTML** que nos permite introducir cualquier valor para asignarle a la variable.

  Nos puede ayudar en el hipotético caso de que queramos actualizar los datos de nuestros paneles al mismo tiempo a partir del valor establecido en la variable.

  Esto se escribe en el campo **Default value** de dicha variable.

  Si no escribimos nada en dicha variable, los usuarios podrán escoger el valor en el menú desplegable después de la creación de la variable.

  ![img](https://lh4.googleusercontent.com/E2SNooG_Y2yQD9-sn6N8oi3ABgViEKE3qlbravSnjzc-kZngKEz_pEmb-Zq0rWvrcRkZKm8LZ3_j8e9kAJ97HE-X5g4xL9qNZKo20CUeuGnsz1lR54N1QnB2xhycr5nOl_-pLZem)

  ​										*Creación de variable sin asignarle valor*

  

  ​       ![img](https://lh4.googleusercontent.com/jgCQlaNB5Gag9K7fY2s_wjUvwbrULm9IGlYECi1xVPCRDAuLBmJRZD61xdWOiaudNOsQ1fS0h-4HCUL9w0h1Bt6v4fH7Br1FxM3TO9dFmKBP8kO-kOk2akIYOX1PrafMACyHY0fF)  

  ​    									*Asignación de valor en el menú desplegable*

  

  **Constant** -> Pueden ser usadas cuando quieres incluir un valor complejo dentro de una consulta para no volver a escribirlo en cada consulta.

  Por ejemplo, si tuviéramos la cadena **uewiwasmadas** podríamos referenciar esa cadena con una variable llamada **$compleja**, para que de ese modo siempre tengamos acceso a la cadena.

  Pueden ser usadas cuando quieres incluir alguna cadena compleja.

  

  **Data sources ** -> Puedes usar este tipo de variable para cambiar el punto de conexión al que estas haciendo consultas dentro de tu panel.

  - **Instance name filter** -> Puedes extraer partes de la cadena que se quiera consultar a partir de **regex**.

  **Interval variable** -> Podemos cambiar el intervalo de tiempo que queremos que se muestre nuestros datos en Elastic.

  Por ejemplo:

  ![img](https://lh5.googleusercontent.com/ndXFPCiFqb39PS756mBAjSTyu18-9l4DHsYy4yhmY1ww1TMpLUQQFoig8IKwSvHDLYPdhYVuSfMWRvjoj65vkkgNvRpwmQUrW85GqjwqwO8fkHgVaDQN8Z-8M0eb1Cltjqm7QbzF)

  

  Tenemos la variable **$tiempo** que almacenará el listado de minutos, **1m, 10m y 20m**.

  Es también valido las siguientes unidades de tiempo:

  - s (segundos).
  - m (minutos).

  - h (horas).
  - d (días).
  - w (semanas).
  - M (meses).
  - y (años).

  ![img](https://lh4.googleusercontent.com/P2mxRvsboTpzLTZAPrj5-LYVtQL1xWOKosdP-VfSZxU0wrf09sPPe7tjw3fG3FH1vqg5c0LCvKN5XRFm8atePtWxzLuAn9Ns6ISEzOV8-Fj9vnaLg7ssE45T0UoKHtSLteQCahhz)

  

  Entonces, podemos indicar que la franja de tiempo que queremos extraer los datos de Elasticsearch a partir de su campo **@timestamp** sea de **20m**.

  

  **Ad hoc** 

  Te permite hacer una búsqueda basada en **clave:valor** que automáticamente Grafana te las añade al datasource seleccionado.

  Este tipo de variable solo esta disponible para los siguientes datasources:

  - **InfluxDB**
  - **Prometheus**
  - **Elasticsearch**

  

  Ejemplo practico:

  ![img](https://lh5.googleusercontent.com/ndL_tcJiCFXRCNPEEsbGEI4jk8YaU-1lf92mT-iQFcXhMQSt_m-FSjFyUQFCPgMaE2dWM5rQgOxd4FEuV9dd9DUKj5dj9AF2XkxRx26cR97WCKwRvHVXDHH46hKmWAIp_JGNOeeG)

  ​                         Variable reservada solo al datasource **ElasticSearch**

  

   

  ![img](https://lh4.googleusercontent.com/FsYKsUa_e9HNUKQMzeNY1dEEz3zTnZAcfl2jur7CAaMs_r7GlQbTeRMqQsbiFtC_cuW3sgz59CJ5wyKRSSwSf5ovtlWxNHkfKE4L8yqaN7wzg9xPsW9mW3_MWm_oxN4OqrRqfbNY)

    

  Requerirá que le indiquemos el campo de elastic **(event.sms)** y un valor en concreto **Nmap ping sweep**, para hacer que nos encuentre solamente dicho valor automáticamente.

  

  Link

  ```bash
  https://grafana.com/docs/grafana/latest/variables/variable-types/
  ```

  

  #### 2) Templates

  Son consultas de Lucene que para su creación requieren de una variable.

  Para la monitorización de nuestras empresas podemos disponer de un dashboard y usar paneles para gestionar la actividad de todas ellas con consultas basadas en plantillas.

  

  Funciones disponibles a utilizar:

  - **Average** -> Devuelve la media aritmética de la suma de **'X'** valores divididos por su cantidad.

  - **Min** y **Max** -> devuelven el valor mas grande y pequeño en la colección.

  - **Sum** -> devuelven la suma de todos los valores.

  - **Count** -> devuelve las veces que han aparecido esos valores en Elastic.

    

  #### 3) Creación de Dashboard

  Primero, vamos a crear un dashboard que tendrá todos nuestros paneles que van a mostrar todos nuestros datos.

  ![img](https://lh4.googleusercontent.com/MKGy7HpRvD1szn4GQCVBez5Fb8UO-tgfOhnvlovAfYq2KG_RbU1g45ot0dadtVKc4FVf4-9rA5m_h1nrGo7zNHCFGJDQo3xNvX1YvKzOVj3cUoSkyi_p45I-CCo1v9RW803UlQf6)

  

  Nuestro dashboard se va a guardar con el siguiente nombre y va a estar ubicado en el directorio **General**.

  ![img](https://lh3.googleusercontent.com/qmAxKFp-twNFrrrT5UX8y2nBtwJ32YCysXA5OdwvlFpZjIx7D2dQYdPPxGpu3wa2c2TSaGAQ_SOy6KLCTq6h0ulzpmlQCV_2QBkhHfj9y6X8I6nwHNWvK0eAP45NVIMPEesj5L4w)

  

  Creado nuestro dashboard, hemos de añadir los paneles que hemos estado comentando.

  ![img](https://lh6.googleusercontent.com/H16m-N23AkLT4_pX1fTMq54eiSJ3-QY-bvl3VaLWbajUBovCcWIW9lJS9T1G5KpzFoToGj9mgfkBtmVifcXD6M9PIOePUeZNA8RctVfA5cinfXTweMBNT_NYZlhpbnwFbr9aemGW)

  

  Dentro de nuestro panel, vamos a escoger el punto de conexión que nos vamos a conectar para extraer los datos, en este caso **Elasticsearch**.

  El campo de elasticsearch que tendrá el objetivo de almacenar el nombre de las alertas de Snort, como por ejemplo Ataque de Fuerza Bruta será llamado **dissect_alert**, por lo tanto para que nuestro Grafana muestre dichos nombres, tendremos que contactar con el campo.

  Nuestra consulta será la siguiente:

  - La función de **Metric** será **count()** ya que queremos contar todas las existencias de los valores que estén en el campo explicado anteriormente.
  - Dentro de **Group By** le indicamos que agrupe los 5 últimos resultados del campo **dissect.alert**, para ser mostrados en el panel.
  - Finalmente, con **Then By** vamos a decir a Grafana que para saber cuando fueron indexados en Elastic mire el campo @timestamp que constará el dia/hora de la indexación.

  ![img](https://lh3.googleusercontent.com/YVBQa1T57xJaIlLunBmsdFf5y9PiWoojrz1o-zfiOZ3520FdXZ0tjU_k0mZXFRD4Pj6J6VzSDZKrsbn6F2LPTRkK0zCqzix0DFOhEh7S1B3MQst5dVBmFuSKX3F6-msJcbquFL2Z)

  

  ## 10.4) Pie chart

  

  Entonces, a partir de la anterior **query**, ya podemos elegir algunas de las visualizaciones disponibles que nos ofrece **Grafana**, en mi caso he optado por el típico quesito que podemos ver también en Kibana, este tipo de visualización se llama  **Pie chart v2**.

  ![img](https://lh3.googleusercontent.com/IaYxAibtbMkr_QwWXRM4RMzfGKH6llfNjBS8ZP58Gj2u-GGYqhj1_ZNPTX7qcO4Ho9evAKYpAqMXGhJBT-sPSWOT751jd7qkJPJNUy2eoGwhVIS4MjLvEH11w6AEidr8ksAEFj52)

  

  A continuación, vamos al apartado **Display** y vamos a tocar algunas opciones:

  - **Calculation** -> Escogeremos la función **Max** ya que queremos obtener el número más alto que haya encontrado Grafana de cada alerta en ElasticSearch.
  - **Piechart type** -> Describe de que forma se vera el gráfico, si escogemos **Donut**, tendremos una redonda con un agujero grande en el medio, y si por el contrario queremos **Pie**, será el caso contrario.

  - **Labels** -> Serán los valores que se mostraran en el **Donut**, tenemos tres disponibles para escoger.
    - **Value** -> Mostrará el número máximo por cada alerta
    - **Percent** -> Mostrará el porcentaje de cada una
    - **Name** -> Mostrará el nombre de las alertas en cada sección del gráfico.

  - **Legend mode** -> Es la forma que se clasificaran los nombres de nuestras alertas, en este caso escogeremos que sea en formato **Tabla**, que saldrá divididos con una línea en blanco a la parta derecha de nuestro **Donut**, ya que lo especificamos en **Legend placement**.

  

  ![img](https://lh5.googleusercontent.com/F2lWHzYD3qg1C27fCNMgCjNAcRd3begl4dE-WALVoz4LNwJiLZ-HbKVKLQ11HdbOqMtfcJso5y6uToF78NwtTYp1EE76v25shUEe8sGrsoMYNefSNTiZo7SqevT1g1jt8IKCwref)

  

  Tipo **Pie**:

  ![img](https://lh3.googleusercontent.com/OliCgnjw315hmo5VL_1iSYgM724hJoTbT2L__mmFWuB-pEmSES9Q07e0tyNdOp5tIJgdzbPkiHyIEs22qHcBW3-OvDhQesrEcUmWmms1shAjaUeXRszpCaQ3kiJyEmLOb9MJQ0WS)

  

  Tipo **Donut**:

  ![img](https://lh4.googleusercontent.com/UGlWq77zEoHIXpOXvrMMbr9tbZBijIWTmeoh6wTkjwIe2skBogBHeIar5NqNHv98YIZAzViDwt5xPr3wc9nkA8mEKFtsCHr1P7UIXxSzJZNbkK4CcSMA3hZKODcNJ9Dtd-Srb4Lh)

  

  Para acabar, tendremos la siguiente apariencia

  ![img](https://lh4.googleusercontent.com/2feBb2r9ltQZWiA8BVFf37X8GpaH8zgBB2L3dPFmDG75JPi_VxbUFX-mq1Nqsf5kdT7sWa8KRvlpb7xjGj0P24l2JqVScJtz3og1B310zT1278B_G7nkJnYupH8zkCH-S55OU1B0)

  

  ## 10.5)  IPs origen

  En este apartado se verán cuales han sido las IPs de origen implicadas dentro de las alertas de Snort recogidas por Grafana.

  Lo que podemos hacer en este momento, es crear una variable, que tendrá la misión de guardar todos los nombres de las alertas para que cuando el analista quiera ver solamente las IPs de origen de **NMAP ping sweep Scan** y no las de **Ataque TCP DOS**, pueda verlas a partir de un simple clic de ratón.


  Primero, iremos al siguiente icono, para crear nuestra variable de tipo **Query**.

  ![img](https://lh4.googleusercontent.com/jnjS99uzWkmIfqLgVfqcvA81tA6aOrBrg4Mk1-T30bO1rKKc8w1toTVMClEyJLV4lcJAj7IEkaPjFTI0uEeapQNhVUaYsf7vsP1ATYosJEXe3_mU6ywJZZ3bd5KdFpOaQ5aySQIw)

  

  Dentro vamos al apartado **Variables**.

  ![img](https://lh4.googleusercontent.com/pesFUVACk7s4ZojSicjwdi7lurYJwDrThJht_U1eVHAH48GBSjIKpqgTcvcKrsjlffXyT26caj_zzSQTQxcLghT_6AnM_4gLo4n3X82zfXGyxejjiBZ4Dek0jDjhO-LCFio7V9vG)

  

  ![img](https://lh4.googleusercontent.com/bs-m0BBBOisFT0ObzQJqCLJ_cRfUyPeKdwhSKX68XwFh04YLgW3lVge8O01uTZDTpg71Xd6a_vkRArbVGpfTwB33cpP6YWnOh0m8xGCaUv1g4APyaU4zSTZzZ0bZ2oi1c1KIW2EP)

  

  - **Name** -> Indicamos el nombre de la variable.

  - **Type** -> La variable de tipo **Query** tendrá la misión de almacenar valores que se vayan actualizando al paso del tiempo.

  - **Label** -> Nos permite establecer un alias a nuestra variable para ser visualizada en el desplegable posterior.

    Si no ponemos nada, es decir lo dejamos por defecto, el desplegable cojera el nombre de la variable.

  - **Hide** -> Opciones para ocultar información en el menú desplegable.

    - En blanco (por defecto) -> Mostrará el nombre de la variable o alias **label** en el desplegable.
    - **Label** -> Ocultará el nombre de la variable dentro del desplegable mostrando solo el valor seleccionado.
    - **Variable** -> Ocultará todo el menú desplegable tanto el nombre de la variable como el listado de valores.

  - **Description** -> Podemos definir en pocas palabras el propósito de la declaración de la variable.

  - **Datasource** -> Escogeremos el punto de conexión que hemos creado para extraer datos de interés. 

  - **Refresh** -> 

    - **Never** ->  Esta orientada a almacenar datos que no serán actualizados con dentro de la variable.

      Los valores de la consulta se encuentran en la caché.

      En caso que nuestro datasources vaya a actualizarse diariamente no seria la mejor opción y deberíamos optar por una de las dos siguientes.

    - **On Dashboard Load** -> Se irá modificando el listado de valores de dentro de la variable cada vez que el dashboard de Elastic cargue nueva información.

     - **On Time Range** ->  Se utilizaría en caso que queramos extraer datos más recientes en nuestro panel de una franja concreta de tiempo.

  - **Query** -> Buscaremos el listado de valores que se encuentren en el campo  **dissect.alert** de los documentos de **ElasticSearch**.

    En caso, de que tengamos muchos valores y queramos ver los más recientes, podemos usar **"order": "desc"**, que lo que hará será ordenar del último al primer valor, para de ese modo obtener los últimos que se hayan indexado.

    

    Ejemplo con **"order": "desc"**

    ````yml
     {"find": "terms", "field": "dissect.alert", "order": "desc"}
    ````

  

  - **Regex** -> Podemos usarla para extraer parte de nuestros resultados.

    Es útil en caso que tengamos un string muy largo y solo queramos obtener una porción de ella para almacenarlo en la variable.

    

  - **Sort** -> Podemos usarla para ordenar nuestro listado de valores de diferentes formas para que sean almacenadas en nuestra variable personalizada.

    - Alfabéticamente de forma ascendente o descendente.
    - Numéricamente de forma ascendente o descendente.

  - **Multi-value** -> Con esta opción, podemos seleccionar más de una alerta a la vez o una única alerta para su previsualización.

  - **All** -> Con esta opción, podemos seleccionar todas las alertas a la vez.

  - **Preview of values** -> Podemos ver la lista de elementos que serán almacenadas en la variable antes de ser utilizada en el panel.

    

  Para acabar, le damos a **Update**.

  

  La variable **snort** que hemos creado ahora tendrá los nombres de las alertas y podemos empezar a filtrar por cada una de ellas, seleccionando en una de sus casillas.

  Este es el menú desplegable de la variable.

  ![img](https://lh4.googleusercontent.com/LFe56vrnmE5RHT0nJfU9hInF-Cd4aiWCm0JE0tIGJR1O7vzj1w4gAf4jr8GuIz5JpeaOadW75Jka0RHbJNK0YuwLZEeXIf3BOJghI6492CBzye_XzbnlLwEP2faA00YGuZU7vcin)

  ​	

  El panel de las IPs de origen, será de tipo **Stat** que nos permitirá ver de una manera muy simple cualas han sido las IPs que coinciden con la alerta seleccionada por la variable y cuantas veces aparecen en Elastic.

  También como el anterior panel, tendrá la función **Max**.

  

  ![img](https://lh4.googleusercontent.com/ELySWooKwff2AZ3g8KZ0uVTfv7lTz-cR4ppBLWsTAyZpQ5nuVkRffEOO6r_rGOWdX9FCiyV54QiFNtXlVzFW6EO9xsMQEni4HeJuFtNZQ5m82RLgZD_Xo6Z5xCHZrOYvoih3hebR)

  A diferencia de la primera consulta, en este caso especificaremos un valor en el campo **Query**, ya que en este caso solamente queremos que nos muestre las IPs de origen que coincidan con la alerta seleccionada de nuestra variable.

  En formato **Lucene**, como estamos acostumbrados a filtrar por ElasticSearch.

  ```bash
  dissect.alert:$snort AND dissect.ip_ori:*
  ```

  

  Si cambiamos el valor de la variable a **INDICATOR-SCAN SSH brute force** , podemos observar como solo aparece una determinada IP de origen, que en este caso es nuestro **Kali**.

  ![img](https://lh4.googleusercontent.com/eXGCHaCK7qw_eALqUV2myvYzqabO2fvoPnmR0WANZgea1BEGIo93pUwsaMeNFOtdW015yBD5kRPmWiC8aLh3gGUg3I1BY4u3snd-3spECF-0xNIT_QzIqntHj1h_IDc3sC87N9qS)

  

  Para cambiar el color de los números que aparecen de cada dirección IP de origen hemos ido a **Field > Thresholds** y a continuación a **Base**, este menú esta justo a la parte derecha de nuestro panel.

  ![img](https://lh4.googleusercontent.com/vo3IvwZ40tPUHJqin17n2idRjJtKfh2Ae0s58RLc8ahqTFxcjuNjOVHsDle8G9yQREsfEsScivszLWfxpYzC-3Dat_iugOzrSXPTHv58TnGayFuUm5bLpwy9VrTnmD9ZLtwcY_0C)

  

  También, para añadir la función **Max** para que muestro los valores mas altos de cada alerta, vamos a **Panel** > **Calculation**.

  ![img](https://lh6.googleusercontent.com/8BEIilzPrKDZh6DdAStWlc_e96DNcUk5GIPcqnsSbbUnq4SOOxjYowSCVHVR0gOBgA7UHS1Jo-QuF2x5ZWZQ-h1-KWhGGZc3Wz0neyZkUkeembNmZRPxsohlTjTVbjXr0uPfyLCI)

  

  Para que el nombre de la alerta dentro del panel vaya cambiando, según lo que escojamos de la variable hemos introducido el valor de la variable **$snort**.

  ![img](https://lh6.googleusercontent.com/LQvuk1WfWtA-PJSz4OuFGVqxFO46lmcdq8bvh4Ug3HilU3zP8XWGGgaHc-J5qS-FodH6B37fxdM1dpkg9fO495qGamUJk_dtXL8qpFjImuH5_f4LT8DiEWyHu9aNfPoe4C0JEtH9)

  

  ```href
  https://grafana.com/docs/grafana/latest/variables/variable-types/add-query-variable/
  ```

  

  ## 10.6)  IPs destino

  

  Ahora en este apartado vamos a extraer a que direcciones IP  han ido dirigidos todas las alertas.

  Para eso, vamos a cambiar la consulta anterior y en lugar de **dissect.ip_or** vamos a reemplazarla por **dissect.ip_dest** ya que es el campo donde estarán todas las IP de destino dentro de los documentos de Elastic.

  ![img](https://lh3.googleusercontent.com/e-BciJjeDE2QOqqHzxhE1fIys1_F1r2OYne8u6veVk-sNMwptkQD4Xy01KBRTJgjXBN_xdgRTEG1CN5wJS8hXT431pet25FW5gu4WSJz2djezZKMifqrjUOC_Sy3qgV8Zbnv2GRV)

  Como el caso contrario, escogeremos **Stat**  y a continuación nos ubicaremos a **Display** para cambiar algunos campos:

  - **Calculation** -> Indicamos función max para que nos devuelva el valor máximo de cada dirección IP de cada alerta.
  - **Text mode** -> Vamos a indicarle que nos muestro **Value** que seria la cantidad máxima de cada IP y **Name** que seria la dirección IP.
  - **Alignment mode** -> Escogeremos **Auto** para que tanto la IP como su cantidad tengan separación a la hora de mostrarse en el panel.

  ![img](https://lh4.googleusercontent.com/8UAITCYR_CSTnnRnr42adn8XeLdQeEQj8bkDMtOYhpZ1N9DZQjV_BubVJPfd_Yjm83tEiXtr-eSj2KtSoGufm8fcZbUA8LxQO_f0CLlXdZeJGY5G0Oh39KtIoRQ2Ytbqjp_Ut_sh)

  

  Más abajo del mismo apartado también modificaremos los valores numéricos de **Text size**, que se basará en pixeles.

  - **Title** -> Se referencia a la dirección IP que será mostrada en la parte izquierda del panel.
  - **Value** -> Se referencia a la cantidad máxima de esa IP que será mostrada en la parte derecha del panel.

  ![img](https://lh6.googleusercontent.com/nGmfyaa3bVPSM_G3NGB0a7-u5Es9BMU39sNZg_ZPOrECVqX-I9FqffrWH_RJLRHkOekqyzC7UPWyiLZISO8up_iOGFT6EGB_MT2gt7BVj2LYcwRqDFXQpnUb3ourfx-QOw5aOhfJ)

  Finalmente, habiendo hecho todo lo anterior nos saldrá estos resultados cuando la alerta sea **NMAP**.

  ![img](https://lh3.googleusercontent.com/3cDfeRwPxkW_WTmSc2xbvnyu_UqARidd875Wga5ODBsLodz222BZAbt3bNye00Dhyea7gnxmGGBdY-xYYTaeDGkZkJ72_YhrXX3Aehmf19Wy25XfV8X_uKH9WvIuVa2md-svSOOH)

  

  Si escogemos por otro lado la alerta de fuerza bruta, nos sale que se ha intentado 7 veces en nuestra màquina.

  ![img](https://lh6.googleusercontent.com/VDCw5QW1QG6PE_bzyG0SRs0SX95hflUa9h6flU3MdIx9SBgifzneq7uNPnQLKjrMNmYgdp78jnBGF_Ctgr55a5O7ENfrt_F5iD9cEon0kJOYxUqFSPJg2AZG8LasBQRrQERt1rY6)

  

  Links

  ```href
  ---- Grafana -----
  
  #Credenciales usuario de Grafana y Fichero editar correo electronico
  https://docs.securityonion.net/en/2.3/grafana.html
  
  #Información de como funcionan las alertas
  https://grafana.com/docs/grafana/latest/alerting/create-alerts/#alert-rule-fields
  
  #Envio de notificaciones desde Gmail
  https://community.grafana.com/t/gmail-for-notifications/1895
  
  ---- ElasticSearch ----
  
  #Conexión del DataSources de Elasticsearch en Grafana + Consultas Lucene
  https://grafana.com/docs/grafana/latest/datasources/elasticsearch/
  
  #Como crear variables
  https://grafana.com/docs/grafana/latest/variables/
  
  #Tipos de variables
  https://grafana.com/docs/grafana/latest/variables/variable-types/
  
  #Links de Datos
  https://grafana.com/docs/grafana/latest/linking/data-links/
  
  #Average Grafana
  https://community.grafana.com/t/average-count-per-time-interval/5928/3
  ```

  

  

  # 11) Alertas de Grafana a Telegram vía Elasticsearch

  

  Para enviar una notificación por **Telegram**, primero necesitaremos crear un Telegram Bot que es un robot que nos permitirá enviar notificaciones desde Grafana a nuestro grupo creado de analistas.

  

  ## 11.1) Creador de bots

  

  Es llamado **BotFather**

  **BotFather** no será el que realmente envié dichas notificaciones, sino más bien es el que nos permitirá crear nuestros bots para posteriormente poder usarlas.

  En pequeñas palabras es el **padre de los robots de Telegram**.

  Primero, le daremos a **START** para empezar las configuraciones de nuestro **bot**.

  

  ![img](https://lh6.googleusercontent.com/pvyK071WPSyLgWprQjGkipBj9SW8nKm-vmI04lv_dpBph4dI6g4YD-WJ4BThoRbdEwYA-ZBVMXlyKLSs1S0ONbDdxy7mhu2Q7BYllFOXPej8l50pdWn-0zQ4qtw6n1gfrcb4uQCz)

  

  ## 11.2) Creación de nuestro bot

  A continuación crearemos el bot escribiendo el comando

  ```bash
  /newbot
  ```

  Seguidamente, escogeremos el nombre personalizado para nuestro bot.

  ```
  DaniAlertaje
  ```

  A continuación, escogemos el nombre de usuario del **bot**, como estamos viendo es requerido que acabe con **_bot**, nuestra elección será de **GraGCyber_bot**.

  ```
  DaniAlertajebot
  ```

  Ahora para tener acceso a nuestro bot tendremos que clicar sobre el enlace.

  ```
  t.me/DaniAlertajebot
  ```

  

  ## 11.3) Creación de un grupo para la alerta

  

  Hecho esto nos hará falta añadir el bot al grupo que vamos a crear para Grafana que tendrá el objetivo de recibir las notificaciones.

  Primero, crearemos el grupo.

  

  ![img](https://lh6.googleusercontent.com/ZZSI_TBV7e6kLms48H6KZNKbc5pfM6xHhit5r27EexOE2-wcnnBBYkjPou36880XYsSEi7WsVlEUo8Q4rBH9qbFCziDcz_5iC7Qco8H27O0aIXXnZmyeNXPO5QrkT73ObGfanFlW)

  Nuestro grupo estará formado por los analistas del SOC i el bot.

  ![img](https://lh5.googleusercontent.com/xaanLPi6CuOWtyR3PQeLhQ3hToj3lZtYZq3RMiNPBTlj1kqzNQbOnhRbXlMi-UWSI-IsQDHbnVHybyFzL9SSKrN8sC0UY6eZRYmQ_fIxRXjJfB7LTHVCIvgVCjIfq8dVIq5Z8aBE)

  Copiamos nuestra BOT API Token del mensaje. 

  ![img](https://lh6.googleusercontent.com/S8ViMWcq8WlHuWSKzW2NUXHVRTXIioApWbrMYr0OGevAT1Hec4NASLfJCyb3EO0QZej1FQ9B_EzSS3gNvNu4zJueXFWMtLbPq_DvNtm1VpJFCGqhz1n-ZIJVCArUJb5uOG97LVCf)

  En concreto esto:

  ![img](https://lh4.googleusercontent.com/AWz3y5Vh7mu2CzPy5c8OGiUrxAT6tsroOuU7ghDcHCgK-qrS5XduPuEgX-7mVYTCkw--Z0llzTMwa7488SR-C45lKcX0wz47s9aqp9lvQT9pmiUZkeDae54BnbX_-paEkUZEpU8F)

  

  Y vamos a obtener el identificador del grupo que hemos creado anteriormente, añadiendo nuestra API Key en la dirección siguiente.

  ```href
  https://api.telegram.org/bot<API TOKEN>/getUpdates
  ```

  

  A mi no me mostraba nada cuando busque a partir de esa url además de añadirle la API.

  Y lo que fui fue administrar el Grupo cambiando el historial de chat para nuevos miembros de Oculto **Hidden** a Visible.

  

  Solucionado el problema anterior, vamos a copiar el identificador del grupo en cuestión.

  ![img](https://lh6.googleusercontent.com/0Ni2GDbqLK3zWfrrSsKMeoEIa7UFPpKOvvc2hNop-0NCy_SR0sXr0vJ6O_q7n080StlltpHiTNh3HfOZzK0oZF1On-_6GxGLte2oNqxf8ua0Uoi9Bad2g1FF6QVq3S2vKnH3BIiT)

  

  Dentro de Grafana deberemos de añadir un canal que será donde se van a enviar los mensajes de Grafana.

  Para eso, debemos de ir a la barra lateral izquierda de Grafana y a continuación al icono con forma de campanilla y finalmente a **Notification channels**.

  

  ![img](https://lh5.googleusercontent.com/ggzf24EJW2vINHV5Vb3rzBcfhQQiqwM-IaG_4JzrsejB6U_OGxIBUgJC2oeW2Gh0wupwdqyzopApiwAbEomB2dIMDVytT7wWuWvrx5T5nBZHoZI-f1i7OxCd4LxfpCTvQ5lrc8sx)

  ![img](https://lh5.googleusercontent.com/R4JxViMfupsVijf8yzYQJMA7QPpOlux-4PMMx_1oBphKAkRAWymbR53QfX2gspwt7ulk80bKUVcD1HKIHxPJcukAMU8ZZzq043yaxNTjnwi_ngmOUrXfIogY9ujZxtAHTWqBbWof)

  

  

  ## 11.4) Creación de alerta

  Crearemos el panel de tipo **Graph** que será el que nos permitirá crear nuestra alerta, ya que los otros gráficos no lo permiten.

  **Aviso** -> Los siguientes parámetros de **Alert** son vistos en el apartado 9) ALERTS que lo implemento con MySQL que es necesario revisárselo para entender su funcionamiento.

  ![img](https://lh6.googleusercontent.com/s2eCDqqDpzZ6A_dGmyP4z50PBzhgWSFry5kR9CN0cN19h9tPunJxSb6I9ZxuQczjCrapyQ5poY75D3TacLrfSe1B0btzXzHbR7koMScDC6BWJSYv7c0K0NvLE3arKg__tokkanMh)

  

  

  - max() -> Calculará el valor máximo de cada alerta proveniente de Snort.

  - query (A, 48h, now) -> Estudiará los datos des de hace 2 días hasta en estos instantes para obtener resultados.
  - IS ABOVE -> 1  -> Filtrará los valores que están por encima de 1.

  

  ## 11.5) Resultado final

  ![img](https://lh6.googleusercontent.com/HIEEQbafxuf-1nJh75fecZv8vgUsXkCuwwW0MxouerDsthfQny-ymeMbXxkPFA7EE_L0QyStYfDqRVEFG5amIeOUww5RrYbY65Pyy4v9-7IU-FC9dLFbu_HjIB5-AThmfNTuajyc)

  ## 11.6) Cambiar de localhost a ~IP

  

  También lo que podemos hacer esque cuando Telegram envié la alerta salga la dirección IP de donde se encuentra nuestro contenedor de Grafana, para que de ese modo desde Telegram los analistas puedan clicar el link para redireccionar donde se encuentra el panel.

  Lo comento, porque por defecto vendrá con **localhost**, haciendo imposible acceder a dicho panel desde otro endpoint de la red.

  Tal como vemos a partir del campo **URL** -> *https://**localhost***

  Para eso vamos a acceder al contenedor

  ````bash
  docker exec -it grafana /bin/bash
  ````

  

  Dentro vamos a editar el fichero de configuración de Grafana con extensión **.ini**

  ````bash
  nano conf/defaults.ini
  ````

  

  Ya dentro vamos a ubicar la variable **domain** que se encuentra debajo de **http_port** de la sección **Server** y añadimos la @IP de nuestra máquina

  ```ini
  domain = 10.200.0.35
  ```

  

  Finalmente, para que se apliquen los cambios, salimos del contenedor y lo reiniciamos.

  ````bash
  docker restart grafana
  ````

  

  
