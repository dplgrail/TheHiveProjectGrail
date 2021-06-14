# SIEMONSTER

## INTRODUCTION

- SIEMonster como su nombre indica es un SIEM (Gestión de Información y Eventos de Seguridad) con las mejores herramientas de código abierto que se han lanzado, por eso lo de Monster porque tiene una gran cantidad de herramientas y funcionalidades que nos ofrece una gran cantidad de posibilidades con las que trabajar.

<img src="https://siemonster.com/wp-content/uploads/2019/09/SIEMonster-Latest-Logo.png" style="width: 600px;"/>

## FUNCIONALIDAD

- Este SIEM nos da informes de incidentes, correlación avanzada con inteligencia frente amenazas y de respuesta activa y todo esto gracias a la integración de diferentes herramientas que por separado rinden bien pero juntas rinden mucho mejor y nos da la posibilidad de tenerlo todo junto en una misma red de servidores con los que integrarlos entre si y hacer un sistema de analizadores muy potente.

## HERRAMIENTAS

- En SIEMonster podemos encontrar las siguientes herramientas: 

### THEHIVE

- Es una muy buena herramienta para poder tener una respuesta frente a las amenazas que detecten los analizadores que tengamos con TheHive. (Cortex i MISP) En el SIEMonster podremos encontrarnos que se integra con Cortex, MISP, OpenCTI y PatrOwl.

### CORTEX

- La función de Cortex es analizar y hacer la función de análisis forense de los datos que le lleguen de TheHive pero de forma digital. Puede responder activamente frente amenazas e interactuar con los "Responders" que tiene implementado Cortex. 

### MISP

- MISP es una plataforma de amenazas para que empresas y entidades puedan almacenar y correlacionar indicadores de ataques dirigidos para que posteriormente MISP pueda usar ese almacenamiento y compararlos con los datos recibidos por ejemplo de TheHive y analizarlos.  Puede utilizar los IoC y la información para detectar y prevenir ataques, como fraudes o amenazas contra organizaciones. 

### ELASTIC STACK

#### Elasticsearch

- Es un potente proveedor que nos permite monitorizar y crear alertas para el sistema que permite poder monitorizar los datos y enviar notificaciones automáticamente a los que se encargan de administrar el sistema para informar sobre esa dicha alerta. Su uso es muy sencillo y entendible de usar.

#### Kibana

- Con Kibana podemos añadirle una interfaz gráfica muy intuitiva, donde podremos configurar las alertas que nos será útil para poder reducir el tiempo de respuesta frente a una amenaza.

#### Filebeat

- Con Filebeat podremos recolectar toda la información que nos proporcione el IDS y que lo indexará para su fácil búsqueda. Una vez indexados, pasarlos a TheHive y que con los dos analizadores (Cortex y MISP) analicen si realmente es una amenaza o una falsa alarma.

### PATROWL

- Es una plataforma para organizar operaciones de seguridad como vulnerabilidades, revisión de código, verificaciones de cumplimientos, amenazas u operaciones de caza o inteligencia.
- PatrOwl lo usaremos para que esté integrado con Cortex y TheHive. 

### SNORT
- Snort no esta dentro de SIEMonster dado que se han decantado más por Suricata.
- En nuestro caso ese será nuestro objetivo, hacer que Snort sea nuestro IDS (sistema de detección de intrusos) con el que vamos a recoger las alertas de que han intentado entrar en nuestra network por algunas de las vias que tenemos bloqueadas o no queremos que estén activas. 

![img](https://manuelfrancoblog.files.wordpress.com/2017/10/snorttm.png?w=640)

- Estos datos obtenidos los integraremos a Kibana para verlos de forma grafica y más sencillo para analizar y pasarlos a TheHive para que con los dos analizadores (Cortex y MISP) puedan analizar si realmente es una amenaza o una falsa alarma.

<img src="https://ciberseguridad.blog/content/images/2018/09/TheHive_Cortex_MISP.jpg" style="width: 700px;"/>

## INSTALACIÓN Y CONFIGURACIÓN
- Para instalar todas las herramientas que vamos a usar he decidido decantarme por usar Docker y los contenedores de cada herramienta, dado que es un método muy simple y además muy ágil para poder poner todo en marcha. También usaré Scrips para Snort 3.0 y ElastAlert.

### SNORT 3.0

- Para instalar SNORT 3.0 he utilizado el siguiente script: 
```bash
#!/bin/bash
#Variables declarations
snort_interface="ens18"
#home_net=`hostname -I | awk '{print $1}'`
home_net="10.200.0.29/32"

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

- Para crear una regla necesitaremos entrar en la ruta siguiente y acceder al fichero con ese nombre "/usr/local/etc/rules/local.rules" y allí podremos crear las reglas que veamos necesarias para nuestra necesidad. Principalmente tenemos estas reglas

```txt
  alert icmp any any -> $HOME_NET any (msg:"ICMP connection test"; sid:1000001; rev:001;)
  alert tcp any any -> $HOME_NET 22 (msg:"SSH detected"; sid:10000004; rev:001;)
  alert tcp any any -> 10.200.0.29 443 (flags:S; msg:"Ataque TCP DOS"; flow:stateless; sid:10001; rev:1;)
  alert tcp $EXTERNAL_NET any -> $HOME_NET 22 (msg:"INDICATOR-SCAN SSH brute force login attempt"; flow:to_server,established,no_stream; content:"SSH-",depth 4; detection_filter:track by_src, count 5, seconds 60; metadata:policy max-detect-ips drop; service:ssh; classtype:misc-activity; sid:19559; rev:13;)
```

- Para crear una regla debemos tener clara de que queremos que se nos informe y de cuales son nuestras necesidades principales. También tenemos que tener claro como se crea una regla y su estructura, para ello podemos utilizar como referencia la siguiente imagen: 

![img](https://lh3.googleusercontent.com/iRMafaPFZBw42toysppR6G48UrkiYNQ7TpHnTKAd6_gq_JWWr8xf5oVbqDhnd-tzOxV22p-E405ViPy-H48oOP8yo38PF3TbkO2195otA1XshYkk-8tCaWGLJpTpMnLhbXGo0KnW)

- Vemos que la acción en este caso es *alert* pero tiene más opciones como pueden ser, el mismo alert (genera una alerta utilizando el método de alerta seleccionado y luego registra el paquete), log (registra el paquete), pass (ignorar el paquete), drop (bloquea y registra el paquete), reject (bloquear el paquete, lo registra y envía un restablecimiento de TCP si el protocolo es TCP o un mensaje de puerto ICMP inaccesible si el protocolo es UDP) y sdrop (bloquea el paquete pero no lo registra).
- Sobre los protocolos, actualmente Snort detecta 4 protocolos con comportamientos sospechosos que son TCP, UDP, ICMP e IP. Podemos ve que en este caso es *TCP*.
- El siguiente paso es indicarle una IP de origen y un puerto externos, que en este caso son el 192.168.43.200 y any (cualquier puerto, pero puede ser entre el 1 y el 65535); la flecha indica la dirección del tráfico, que en este caso es hacia la variable *$HOME_NET* (variable que se crea en el fichero de configuración de Snort, normalmente se indica la IP propia) por el puerto 80. Otro símbolo que nos permite Snort es el bidireccional, <>, que permite la dirección del tráfico en ambos lados.
- Y finalmente tenemos las opciones de la regla donde indicamos el mensaje, el identificador de la regla, el identificador de Snort (puede ser 1, 2 o 3), intentos, contador, flags, etc. pero para una regla sencilla hemos de tener los 3 primeros parámetros obligatorios ya que si no nos dará errores.

#### Puesta en Marcha

- Una vez tengamos el Snort configurado y con las reglas creadas simplemente vamos a iniciarlo con la siguiente comanda:

```bash
sudo snort -c /usr/local/etc/snort/snort.lua -R /usr/local/etc/rules/local.rules -i ens18 -s 65535 -k none -l /var/log/snort/
```
```txt
-c -->  esta opción nos permite indicarle el fichero de configuración que vamos a usar
-R --> esta opción nos permite indicarle por que ficheros de reglas debe regularse
-i --> esta opción nos permite indicarle la interfaz que va a usar para la detección
-s --> esta opción nos permite indicarle la longitud que tendrá el fichero con los logs, el mínimo es 1518 y el máximo es 65535
-k --> esta opción es el checksum mode y por defecto viene con all pero nosotros no lo requerimos y usaremos la opción none
-l --> esta opción nos permite indicarle la ruta de donde se va a crear el fichero que contendrá los logs
```


- Una vez iniciemos Snort 3.0 visualizaremos lo siguiente por terminal:

  ![img](https://lh4.googleusercontent.com/84efF3TnWuw1BGS30RnkaSc5EYhY_QJjMYvAZ3MoNphsW-9ZYa8WVfA6gAwtS_LMhS-zMBvTYhOzAGsI9-BTtMpV3C7n1JN2sBGB3BS7XonL_xn4vVAyw_aXDHHd7xDmF03Jsnuc)

- Una vez tengamos ya Snort 3.0 iniciado podremos visualizar como en la ruta "/var/log/snort/" se nos ha creado el fichero llamado "alert_fast.txt", en su interior contendrá las alertas que Snort a creado por la detección que ha tenido. 

- Con la siguiente comanda podremos visualizar las últimas 10 alertas:

```bash
sudo tail alert_fast.txt
```

**![img](https://lh5.googleusercontent.com/Kkl1Ky9v6mOwdLakcGrEH4xcigCfYYe4-dj1A6RZCe-mAjKa8x4soplBDrqURsOkW2Z5GVTHyw0HMMLPlNafKR27wFN6hw_T_9RLFrX8uW8L47yAOg-A2uCJIQ35J6SdjPWyVqQW)**

## CONTENEDORES

- Para la creación de contenedores primeramente vamos a crear el entorno para Docker y el Docker-Compose que serán los que nos ayudarán y se encargarán a subir los contenedores e iniciar los servicios.

### DOCKER
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

### DOCKER-COMPOSE
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

### FILEBEAT

- Para que Filebeat funcione correctamente deberemos realizar unos cuantos pasos.
- Principalmente empezaremos con crear el fichero llamado filebeat.yml. Podremos crear este fichero en la misma carpeta donde el docker-compose con "nano filebeat.yml":

```yaml
      ###################### Filebeat Configuration Example #########################

# This file is an example configuration file highlighting only the most common
# options. The filebeat.reference.yml file from the same directory contains all the
# supported options with more comments. You can use it as a reference.
#
# You can find the full configuration reference here:
# https://www.elastic.co/guide/en/beats/filebeat/index.html

# For more available modules and options, please see the filebeat.reference.yml sample
# configuration file.

# ============================== Filebeat inputs ===============================

filebeat.inputs:

# Each - is an input. Most options can be set at the input level, so
# you can use different inputs for various configurations.
# Below are the input specific configurations.

- type: log

  # Change to true to enable this input configuration.
  enabled: true

  # Paths that should be crawled and fetched. Glob based paths.
  paths:
    #- /var/log/*.log
    #- c:\programdata\elasticsearch\logs\*

  processors:

  # Exclude lines. A list of regular expressions to match. It drops the lines that are
  # matching any regular expression from the list.
  #exclude_lines: ['^DBG']

  # Include lines. A list of regular expressions to match. It exports the lines that are
  # matching any regular expression from the list.
  #include_lines: ['^ERR', '^WARN']

  # Exclude files. A list of regular expressions to match. Filebeat drops the files that
  # are matching any regular expression from the list. By default, no files are dropped.
  #exclude_files: ['.gz$']

  # Optional additional fields. These fields can be freely picked
  # to add additional information to the crawled log files for filtering
  #fields:
  #  level: debug
  #  review: 1

  ### Multiline options

  # Multiline can be used for log messages spanning multiple lines. This is common
  # for Java Stack Traces or C-Line Continuation

  # The regexp Pattern that has to be matched. The example pattern matches all lines starting with [
  #multiline.pattern: ^\[

  # Defines if the pattern set under pattern should be negated or not. Default is false.
  #multiline.negate: false

  # Match can be set to "after" or "before". It is used to define if lines should be append to a pattern
  # that was (not) matched before or after or as long as a pattern is not matched based on negate.
  # Note: After is the equivalent to previous and before is the equivalent to to next in Logstash
  #multiline.match: after

# filestream is an experimental input. It is going to replace log input in the future.
- type: filestream

  # Change to true to enable this input configuration.
  enabled: false

  # Paths that should be crawled and fetched. Glob based paths.
  paths:
    - /var/log/*.log
    #- c:\programdata\elasticsearch\logs\*

  # Exclude lines. A list of regular expressions to match. It drops the lines that are
  # matching any regular expression from the list.
  #exclude_lines: ['^DBG']

  # Include lines. A list of regular expressions to match. It exports the lines that are
  # matching any regular expression from the list.
  #include_lines: ['^ERR', '^WARN']

  # Exclude files. A list of regular expressions to match. Filebeat drops the files that
  # are matching any regular expression from the list. By default, no files are dropped.
  #prospector.scanner.exclude_files: ['.gz$']

  # Optional additional fields. These fields can be freely picked
  # to add additional information to the crawled log files for filtering
  #fields:
  #  level: debug
  #  review: 1

# ============================== Filebeat modules ==============================

filebeat.config.modules:
  # Glob pattern for configuration loading
  path: ${path.config}/modules.d/*.yml

  # Set to true to enable config reloading
  reload.enabled: false

  # Period on which files under path should be checked for changes
  #reload.period: 10s

# ======================= Elasticsearch template setting =======================

setup.template.settings:
  index.number_of_shards: 1
  #index.codec: best_compression
  #_source.enabled: false


# ================================== General ===================================

# The name of the shipper that publishes the network data. It can be used to group
# all the transactions sent by a single shipper in the web interface.
#name:

# The tags of the shipper are included in their own field with each
# transaction published.
#tags: ["service-X", "web-tier"]

# Optional fields that you can specify to add additional information to the
# output.
#fields:
#  env: staging

# ================================= Dashboards =================================
# These settings control loading the sample dashboards to the Kibana index. Loading
# the dashboards is disabled by default and can be enabled either by setting the
# options here or by using the `setup` command.
#setup.dashboards.enabled: false

# The URL from where to download the dashboards archive. By default this URL
# has a value which is computed based on the Beat name and version. For released
# versions, this URL points to the dashboard archive on the artifacts.elastic.co
# website.
#setup.dashboards.url:

# =================================== Kibana ===================================

# Starting with Beats version 6.0.0, the dashboards are loaded via the Kibana API.
# This requires a Kibana endpoint configuration.
setup.kibana:

  # Kibana Host
  # Scheme and port can be left out and will be set to the default (http and 5601)
  # In case you specify and additional path, the scheme is required: http://localhost:5601/path
  # IPv6 addresses should always be defined as: https://[2001:db8::1]:5601
  host: "10.200.0.29:5601"

  # Kibana Space ID
  # ID of the Kibana Space into which the dashboards should be loaded. By default,
  # the Default Space will be used.
  #space.id:

# =============================== Elastic Cloud ================================

# These settings simplify using Filebeat with the Elastic Cloud (https://cloud.elastic.co/).

# The cloud.id setting overwrites the `output.elasticsearch.hosts` and
# `setup.kibana.host` options.
# You can find the `cloud.id` in the Elastic Cloud web UI.
#cloud.id:

# The cloud.auth setting overwrites the `output.elasticsearch.username` and
# `output.elasticsearch.password` settings. The format is `<user>:<pass>`.
#cloud.auth:

# ================================== Outputs ===================================

# Configure what output to use when sending the data collected by the beat.

# ---------------------------- Elasticsearch Output ----------------------------
output.elasticsearch:
  # Array of hosts to connect to.
  hosts: ["10.200.0.29:9200"]

  # Protocol - either `http` (default) or `https`.
  #protocol: "https"

  # Authentication credentials - either API key or username/password.
  #api_key: "id:api_key"
  #username: "elastic"
  #password: "changeme"

# ------------------------------ Logstash Output -------------------------------
#output.logstash:
  # The Logstash hosts
  #hosts: ["localhost:5044"]

  # Optional SSL. By default is off.
  # List of root certificates for HTTPS server verifications
  #ssl.certificate_authorities: ["/etc/pki/root/ca.pem"]

  # Certificate for SSL client authentication
  #ssl.certificate: "/etc/pki/client/cert.pem"

  # Client Certificate Key
  #ssl.key: "/etc/pki/client/cert.key"

# ================================= Processors =================================
processors:
  - add_host_metadata:
      when.not.contains.tags: forwarded
  - add_cloud_metadata: ~
  - add_docker_metadata: ~
  - add_kubernetes_metadata: ~

# ================================== Logging ===================================

# Sets log level. The default log level is info.
# Available log levels are: error, warning, info, debug
#logging.level: debug

# At debug level, you can selectively enable logging only for some components.
# To enable all selectors use ["*"]. Examples of other selectors are "beat",
# "publisher", "service".
#logging.selectors: ["*"]

# ============================= X-Pack Monitoring ==============================
# Filebeat can export internal metrics to a central Elasticsearch monitoring
# cluster.  This requires xpack monitoring to be enabled in Elasticsearch.  The
# reporting is disabled by default.

# Set to true to enable the monitoring reporter.
#monitoring.enabled: false

# Sets the UUID of the Elasticsearch cluster under which monitoring data for this
# Filebeat instance will appear in the Stack Monitoring UI. If output.elasticsearch
# is enabled, the UUID is derived from the Elasticsearch cluster referenced by output.elasticsearch.
#monitoring.cluster_uuid:

# Uncomment to send the metrics to Elasticsearch. Most settings from the
# Elasticsearch output are accepted here as well.
# Note that the settings should point to your Elasticsearch *monitoring* cluster.
# Any setting that is not set is automatically inherited from the Elasticsearch
# output configuration, so if you have the Elasticsearch output configured such
# that it is pointing to your Elasticsearch monitoring cluster, you can simply
# uncomment the following line.
#monitoring.elasticsearch:

# ============================== Instrumentation ===============================

# Instrumentation support for the filebeat.
#instrumentation:
    # Set to true to enable instrumentation of filebeat.
    #enabled: false

    # Environment in which filebeat is running on (eg: staging, production, etc.)
    #environment: ""

    # APM Server hosts to report instrumentation results to.
    #hosts:
    #  - http://localhost:8200

    # API Key for the APM Server(s).
    # If api_key is set then secret_token will be ignored.
    #api_key:

    # Secret token for the APM Server(s).
    #secret_token:


# ================================= Migration ==================================

# This allows to enable 6.7 migration aliases
#migration.6_to_7.enabled: true
```

- Una vez tengamos el fichero ya creado vamos a reiniciar el contenedor Filebeat para que la configuración se recargue y funcione correctamente.

```bash
sudo docker-compose up -d filebeat
```

- Con el contenedor ya funcionando podremos acceder a su interior para activar 2 módulos, para acceder al contenedor: 

```bash
sudo docker exec -it filebeat bash
```

- Y para activar los módulos de filebeat utilizaremos:
```bash
filebeat modules enable system
filebeat modules enable snort
```
- Una vez ya tengamos los módulos habilitados podremos crear índex de Kibana y sus dashboard con la siguiente comanda:
```bash
sudo filebeat setup --index-management -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=["10.200.0.29:9200"]'

sudo filebeat setup -E output.logstash.enabled=false -E output.elasticsearch.hosts=['10.200.0.29:9200'] -E setup.kibana.host=10.200.0.29:5601
```

#### Kibana


- Y con Filebeat ya configurado, en Kibana en el apartado de Management > Stack Management > Index patterns, ya podríamos visualizar el índex de Filebeat llamado "filebeat-*:

![img](https://lh3.googleusercontent.com/6DzaLLnBVrKgqUenE6VIvdXdaILYVhjpDhZLv7_ySauTGP3m_AEC_t1MkNrfgdbtN6oaooE-R9o-G90knIoynJyTO66kZD1dw8FQbMWOfSKg6wSKSBLpHG87IvEObV-WwwzXt8lO)


- Y en el mismo Kibana en Analytics > Discover, seleccionaremos los campos creados con el "dissect" llamados dissect. y podremos ver que la información que nos aparece en el Discover se filtra según los campos que hemos ido seleccionando. En la imagen podemos visualizar como aparecen los datos desaedos: 

![img](https://lh4.googleusercontent.com/_wrTLKG45snk0kQAHn9XxQKPJ-R7dMvk8O0wp34GD61c2QzyL9i1ZMW_AmagXAUYz3U2DU00Xshq0eNzTQMqRPMFTZzg_nKHfMALZFwwozpZ24ulapBmJ6TEHsqoQ1v2_Sz-TNs6)


-  Una vez tengamos el Discover listo podremos ir a la creación de Dashboards donde visualizaremos los que tenemos disponibles (Snort es una creación ya hecha como prueba). Para crear un nuevo Dashboard seleccionaremos "+ Create dashboard".

![img](https://lh3.googleusercontent.com/krcfehdeMQHt8VwDvcZNypVb5HVX2tAkQ5wbDObo7SOGpowVh4StJFZwI_v83nulVab0d7a1w4lOzifO67-y4WuKlByk4yLIATY50bTF4dQxGH3-bbqPqJiTqr07cSzH8jFTIHzo)


-  Cuando seleccionemos la opción de crear un nuevo dashboard vamos a ver como estará todo vacío dado que tendremos uqe crear nosotros mismos nuestros paneles con la opción "+ Create Panel".

![img](https://lh6.googleusercontent.com/4hE3gq2SveKomWA6e3dW9HmgSiag4sVfkmCtQkzrB3Mz4OeRz2iKwh7sLeyMYgNRtEe3kWAw1EVCT1ONDiCR45gNN5bC7PmiOqK4oWCUYRYvPF26F7K58EVRoKy6T5r3WcZ6RhIN)


- Nos aparecerá una nueva ventana donde elegir entre diferentes opciones, principalmente vamos a utilizar la llamada "Lens" que es la más fácil desde mi punto de vista para empezar. 

  ![img](https://lh6.googleusercontent.com/RQCxfMRirLY0sDhqWDscNoYtQhcaU91-6SVnJNHcinGO8pilBZtYLMYSqB0Aa4BjJ9FnESWeSkp62j4go0FZaLPxn4CtJCoF3WxELGcqKKHL8c1Uh-Gg8zQUt60LKb4xQ8JTV1uR)

- Una vez seleccionemos "Lens" veremos que se nos mostrará la ventana donde podremos configurarlo. 

![img](https://lh6.googleusercontent.com/HLmsn5IrMfPJMU761cHFTVedWvZInNHDgbf4RlxY-7KQ1-YxLBmnh-A935OBLBm0e8vzmLS2e3Qt6Qfas-Qivj32WZhxKdJPDzctzmnTWPdihaqmsPPERP-wjYP4w2W9U4fR72hd)


- Para empezar a visualizar datos deberemos arrastrar los campos que queramos a la zona de visualización y así se empezaran a crear las diferentes gráficas. Usaremos el campo "dissect.alert" para crear las gráficas, así pues desde un principio podremos visualizar ya las primeras graficas creadas por defecto.

  ![img](https://lh6.googleusercontent.com/n_Wa4Yjd0NfcBdmX9Q47dKHQG5ff_Nksjre5_Spfj33KGrNr1WvCYPZF4h12M2suCFC4vpjUbarOiFkc3Ae5mmGk4X3QO0Z_GcOa39tp_rALdHa_5Ax5EaRlBys6c4usrQOqJM50)

- Para poder conservar este panel seleccionaremos la opción "Save" y nos solicitará que le indiquemos un Titulo, una Descripción y algunas Etiquetas, para este último necesitaremos crear esa etiqueta y así poder seleccionarla. 

- Para ello seleccionaremos la opción que se nos da "Create tag" y se nos abrirá una ventana con los datos del nombre que hemos elegido. Una vez creada la nueva etiqueta ya podremos seleccionarla.

  ![img](https://lh3.googleusercontent.com/8bb7j3A1TFuLezfmb4FmnACAJboQH6lcgBmKpMIumprTp7hxdEPsKC3v5whcUnM4AUueUMSATFMwWHZrFT5LndoCGPoJmWi_Z-_EioCA2ArHv2lEbnuPEPHKw2r6f45fu3nh8SG4)![img](https://lh4.googleusercontent.com/MiJrXtnrf2Nl6yJS-H5cspHX_DoC9g-h4JU5CQEEVuj0iLajHYgOo4k1wxDkMTIi-5Esuo0v2E78BWO2zyqRKF2tryhoaX2jERK5b7cVFjP0rewLMiDupqByJANWvoVxvQGfgni3)

- Una vez ya hemos guardado nuestros gráfico podremos visualizar algo similar a esto:

  ![img](https://lh4.googleusercontent.com/ainOr99KHawBh5StnL5cmQ9tFn91z12lI3xmM8TFrsCFYESHDpLS4yqqbbsPFSEU9Ca86xnH1I-iFWxZKTc-pSXY-oM-Uuj0nT4J7UCuMTkJesxYrXahP35DmqEb8vhljy-UCKIj)

- En este dashboard se puede visualizar una gráfica en forma de donut con las diferentes alertas que Snort nos ha enviado y el porcentaje de cada una de ellas y la otra, es una gráfica plana donde podremos visualizar cuantas veces ha aparecido cada una de las alertas en un periodo de tiempo. 

#### Extras


-  Para poder regular el tiempo iremos a la parte superior derecha y seleccionaremos el tiempo que nosotros queramos, en mi caso he utilizado una franja de tiempo donde se que podemos ver 4 tipos de alertas distintas.
-  Como podemos ver podemos hacer una selección rápida donde le diremos por teclado lo que queramos, también podemos utilizar los que nos da Kibana por defecto y rangos de tiempo que hemos utilizado recientemente. También podemos crear un bucle donde cada x segundos podamos recargar los datos como podemos ver al final de la imagen. 

![img](https://lh5.googleusercontent.com/7vgreGrnF3i4o_rMj132m4o6NTqg-JbjBvUlYaZ-n1UMiozTjDYYD0DyBayJClmSUsD_Z6kr08No6yL6a--GQPmhLF0Z9Vo5aCiYcyxUpEwQTFCQwL-oS3Pt4FMRM_wkK1wNXSwj)

### THEHIVE, CORTEX Y MISP 

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

### INTEGRACIONES
- Una vez tengamos nuestros servicios instalados y configurados deberemos proceder a integrarlos entre sí para que reciban información y realicen la función que les pertoca.
- Principalmente debemos saber que principalmente los servicios irán enfocados a TheHive que es quien recibirá la información y este las enviará a los diferentes analizadores. 
- Para ello deberemos crear un usuario para TheHive, Cortex y MISP si queremos realizar la integración correctamente. Lo podemos hacer de la siguiente manera.

#### Cortex

- Empezaremos con Cortex donde crearemos una nueva organización con el nombre de nuestra empresa para poder organizarlo todo mucho mejor y entenderlo más fácilmente.
- Deberemos ir a la URL de Cortex y seleccionar “+Add organization” y procederá a abrir una ventana donde configurar la nueva organización.

![img](https://lh6.googleusercontent.com/mXi2k12wbUJB4bgWkD_8NYX8pqNihuKIVxRU6x1q3zEAR2P-LV1iSzv4573GNp2CJy1PksMwb75WlWABOKDGDVTEBJNon8UYzu5aULxV30cYtONI7aZk0q4kYQS82keCjYjr1lrF)

- Una vez creada, entraremos y deberemos crear un usuario que será el que se encargará de la integración. Para ello seleccionamos a “+Add user” y configuraremos el nuevo usuario que debe tener los credenciales "read, analyze, orgadmin".

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

![img](https://lh6.googleusercontent.com/CVjqW9mKV17OEJjYfXjOtottoQytD4uvLlgv0UpGRmINq0glm3DptBkluZFuEZOi-QhB5rWKXpp18XJnnB-ritp60OB2scuyurQHm76pynHkjhUJN0GC2FcNM4iZW_Wu3htnBoaa)

![img](https://lh4.googleusercontent.com/tB9cTCFfBZATE96ZQH7XXenmX2zk_k6M0PtdcPJgePScwy5qKzdPVqJKU-sa6E6JVnD57de3QCYdzfR25pa8vrlYgXglzVY0n286mEATFwoM-WDcBulANl_LK5DAkYtAO0XNt4iQ)

- Una vez integrado MISP veremos que en la interfaz gráfica de TheHive ahora podemos ver un icono más en verde que será el de MISP indicándonos que ya está integrado. 

![img](https://lh6.googleusercontent.com/TsjiU-NDCgWHuiHNgraS6qD5bv5h8P3D5ilaNr00bIoL7ADLGkb1fKwElzTQ7Pz8oi8tcikSbHGuNPC8lMEe3wNyXnYCxQYYP1ydf7rVnCzHTiOWyVt48WAWHr_AnhvU52bKTbvB)

![img](https://lh6.googleusercontent.com/4ArxQBNQg5O987K35jaU_tYk0IsdZPYER6jy5OOCJozAFf82mJrPQIst_skIV7AGnS3yFVQk5neroGB_L0BbhWwwZxaUsqWx2HVq3152uNDe18cmwQRDi2iCuxaIpwXxG73bTsWF)

#### Pruebas
- Para hacer las pruebas iremos a TheHive y crearemos una nueva organización con el botón "+ New Organisation" y un nuevo usuario para esa misma organización.  

![img](https://lh5.googleusercontent.com/FYdOtN5NDDMhErV1VgKuFPhjzlu9x383FzathPnYtW9bqNDh2QWobZKVprUQ6WRaE62otiZUR2EPdsDBKxh-nK2hrgBUQ5DAk0gQO-BDgTa-UCEMmlcHniX-BSeVlE09ueowYPkm)

- Dentro de la nueva organización creada creamos el usuario con el botón "+ Create new user", debe tener los credenciales de "org-admin".

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

### ELASTALERT2

- Nuestro objetivo es automatizar todo el análisis de Cortex con TheHive y por ello queremos enviar los datos recogidos por Snort y enviarlos a TheHive con la siguiente ruta "Snort > Filebeat > Elasticsearch > ElastAlert2 > TheHive".

#### Instalación

- Para ello vamos a necesitar configurar ElastAlert2 siguiendo los siguientes pasos:
- Primeramente vamos a necesitar realizar la instalación de los paquetes para ElastAlert2 que con esta comanda ya podríamos instalarlos todos:

```bash
#Install all the packages for Ubuntu
sudo apt-get install -y python3-pip python36 python3-devel python3-setuptools python3-libs libffi-devel openssl-devel
```

- Una vez tengamos los paquetes ya instalados vamos a proceder a instalar y configurar ElastAlert2.
- Puedes seguir el siguiente Script para realizar la instalación:

```bash
#Install the lastest relesed version of ElastAlert2 with pip
pip install elastalert2

#Clone the ElastAlert2 repository
git clone https://github.com/jertel/elastalert2.git

#Install setuptools module
pip install "setuptools>=11.3"

#Install elasticsearch module
pip install "elasticsearch>=5.0.0"
```

#### Configuración

- Para la configuración vamos a realizar el siguiente script: 

```bash
#Create the new config file for ElastAlert2
sudo bash -c 'cat <<END> /elastalert2/config.yaml
# This is the folder that contains the rule yaml files
# Any .yaml file will be loaded as a rule
rules_folder: example_rules

# How often ElastAlert will query Elasticsearch
# The unit can be anything from weeks to seconds
run_every:
  minutes: 1

# ElastAlert will buffer results from the most recent
# period of time, in case some log sources are not in real time
buffer_time:
  minutes: 15

# The Elasticsearch hostname for metadata writeback
# Note that every rule can have its own Elasticsearch host
es_host: 10.200.0.29

# The Elasticsearch port
es_port: 9200

# The AWS region to use. Set this when using AWS-managed elasticsearch
#aws_region: us-east-1

# The AWS profile to use. Use this if you are using an aws-cli profile.
# See http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html
# for details
#profile: test

# Optional URL prefix for Elasticsearch
#es_url_prefix: elasticsearch

# Connect with TLS to Elasticsearch
#use_ssl: True

# Verify TLS certificates
#verify_certs: True

# GET request with body is the default option for Elasticsearch.
# If it fails for some reason, you can pass 'GET', 'POST' or 'source'.
# See http://elasticsearch-py.readthedocs.io/en/master/connection.html?highlight=send_get_body_as#transport
# for details
#es_send_get_body_as: GET

# Option basic-auth username and password for Elasticsearch
#es_username: someusername
#es_password: somepassword

# Use SSL authentication with client certificates client_cert must be
# a pem file containing both cert and key for client
#verify_certs: True
#ca_certs: /path/to/cacert.pem
#client_cert: /path/to/client_cert.pem
#client_key: /path/to/client_key.key

# The index on es_host which is used for metadata storage
# This can be a unmapped index, but it is recommended that you run
# elastalert-create-index to set a mapping
writeback_index: elastalert_status

# If an alert fails for some reason, ElastAlert will retry
# sending the alert until this time period has elapsed
alert_time_limit:
  days: 2

# Custom logging configuration
# If you want to setup your own logging configuration to log into
# files as well or to Logstash and/or modify log levels, use
# the configuration below and adjust to your needs.
# Note: if you run ElastAlert with --verbose/--debug, the log level of
# the "elastalert" logger is changed to INFO, if not already INFO/DEBUG.
#logging:
#  version: 1
#  incremental: false
#  disable_existing_loggers: false
#  formatters:
#    logline:
#      format: '%(asctime)s %(levelname)+8s %(name)+20s %(message)s'
#
#    handlers:
#      console:
#        class: logging.StreamHandler
#        formatter: logline
#        level: DEBUG
#        stream: ext://sys.stderr
#
#      file:
#        class : logging.FileHandler
#        formatter: logline
#        level: DEBUG
#        filename: elastalert.log
#
#    loggers:
#      elastalert:
#        level: WARN
#        handlers: []
#        propagate: true
#
#      elasticsearch:
#        level: WARN
#        handlers: []
#        propagate: true
#
#      elasticsearch.trace:
#        level: WARN
#        handlers: []
#        propagate: true
#
#      '':  # root logger
#        level: WARN
#          handlers:
#            - console
#            - file
#        propagate: false
END'

#Create index for ElastAlert2
elastalert-create-index

#Create elastalert rule for TheHive
sudo bash -c 'cat <<END> /elastalert2/example_rules/thehive.yaml
name: grail-demo

type: frequency

index: filebeat-*

num_events: 3

timeframe:
  hours: 1

realalert:
  minutes: 0

filter: []
#- term:
#    dissect.alert: "NMAP ping sweep Scan"

alert: hivealerter

hive_connection:
  hive_host: http://localhost
  hive_port: 9000
  hive_apikey: dgOZ/Rk54iWFFcZ20kXG0xUMmtv+R+IM
  hive_proxies:
    http: ''
    https: ''

hive_alert_config:
  title: 'Alert Snort'
  type: 'external'
  source: 'elastalert'
  severity: 2
  tags: ['elastalert', 'name']
  tlp: 3
  status: 'New'
  follow: True

hive_observable_data_mapping:
  - ip: dissect.ip
END'
```

- Para la creación del fichero de configuración hemos tenido que indicarle donde se encuentra nuestro Elasticsearch, indicándole la URL del mismo (en nuestro caso la ip o el localhost) y después el puerto pode donde se puede acceder. Con esto, ElastAlert2 ya podrá acceder a los datos que nuestro Elasticsearch guarda y con ellos poder crear las alertas para TheHive.
- En el fichero de creación de la regla vamos a tener que indicarle el host de nuestro TheHive más el puerto que usa y también se nos va a solicitar una API key de un usuario para integrarlo a el y que sea el indicado para recibir esas alertas.
- Para obtener la API key de un usuario de TheHive simplemente accederemos como admin iremos a organizaciones, entraremos y crearemos una API key en "Create API Key" y en "Reveal" podremos verla

![img](https://lh4.googleusercontent.com/700zsaXT4uMzXk7pEPWzgrvD3PAhA41InLTxnmmW6ai5i4VstIL8dwxcrcVeychyjuXUSJYNYLoFolqzwssvjzjZehOyZHNy3uty5_ievucNDdZoMsDhX_ApJbZ3VM7CRVHeQGpB)

![img](https://lh5.googleusercontent.com/T_Sfe7BQATw7bfrPOzgM-VnkQMP8AofUhaQVxzNNAAtCCr-2tZB6jhILNz0XHdslrut_DhDcdLDLyuWRzlbtf0G_lHnsXiKgkPKDj8DB8UYvxLXFvmbfeS3VmhglcMPHq8x0Uslk)

- Y esta API deberemos añadirla en el fichero de la Rule. 

#### Test de la Regla

- Ahora cuando ya tengamos la configuración mínima hecha y al rule ya creada podemos proceder a realizar un test para comprobar que todo funciona correctamente con la siguiente comanda: 

```bash
elastalert-test-rule example_rules/example_frequency.yaml
```

- Podemos especificar el fichero de configuración que queremos que use al testear la rule, para ello usaremos la función --config <path-to-config-file> y quedaría así:

```bash
elastalert-test-rule --config config.yaml example_rules/thehive.yaml
```
#### Puesta en Marcha
- Para la puesta en marcha usaremos la siguiente comanda:

```bash
python3 -m elastalert.elastalert --verbose --rule thehive.yaml
```

- Con esto iniciará el proceso de creación de la alerta.
- Para poder visualizar que es lo que esta haciendo, deberemos dirigirnos a nuestro usuario de TheHive e iremos al apartado "Alerts" y podemos visualizar que se ha creado una alerta con un observable que es el que le hemos indicado en el apartado llamado "hive_observable_data_mapping".

![img](https://lh6.googleusercontent.com/AOW4UotXM-pOD6a0EJW-XmLiX54JFr40JoMvuW3rTvo1Bht5d4hzgUUFfSYexT64bUSHZMoMhl_BzO3jWxX1gXI2EK54MI8OpKsj3d3ER6liju1nIVbiW5Q8yiDOqEmovC2oYaqf)

![img](https://lh4.googleusercontent.com/lx5EVWnLreHkKBdDOxH7cHefHvsB0ieKQmA7EtX3nSdUGqWmBu9HIbWtdOjI3iD6iweeqybZW9KtzQuFgppSWUiLyszc8gzcTc795gOsKmVZozAvs6Su8RsU2zuIpTeaLRqYUF7m)

- Con esta alerta podemos crear un caso directamente para poder realizar el análisis con los analizadores que tengamos activados con Cortex, para ello vamos a seleccionar la primera opción llamada "Preview and Import" (Con forma de hoja de papel) y no aparecerá la siguiente ventana:

![img](https://lh3.googleusercontent.com/x1iRlWahW-McP94VEmuyOBaQOqcsnf6mBHjLiXNXg-yks4MbmftLxoFvF-5e88qfy61r1bYpUXZ63fw5i9KgXZKhBUdmt-roaYjLsUPi3nZTauCGMP0mKwPUZDP9TQl3YO4nN0M-)

- Para crear el caso seleccionaremos "Yes, Import" y automáticamente se creará el caso con los observables que contenga en su interior  en nuestro caso 1 como vemos en la siguiente imagen: 

![img](https://lh3.googleusercontent.com/NjAspFYBzrMhOOVFk6WiX21REaP1xPxi-EEBkKebOh6pikpx-fHfIXR9vpoK1f5SWl73Ahbm2Df923nIf_TOzGWRGehSDtb-6CnCxq1nPICQ4Wowp8_rec-A2eC3S18hKUG48TK_)

- Podremos ir a observables y podremos utilizar los analistas de Cortex que tengamos instalados. 

![img](https://lh3.googleusercontent.com/7ct7_yyVKP_A1ADAVTJgnvPpv4U9_sQqT2kuVuUsq0BoMO8n7OkRgOBsTXxFgJOt-Dva1x7OXU9e33LDXwUDmCFACCq2Bsy0fAHmjKUbUSvt9dsmvcCTrYtQVYebUarCHS9yyyi3)

- Automáticamente Cortex creará el nuevo análisis y nos dará un reporte cuando finalice. 

![img](https://lh6.googleusercontent.com/vP16Z64oifiJmE-7cGY3R_HgRdt-E8mS13Hub4nL3hmfUShI_rEAlIt1Xf6pkjklZXQpPyXb8rY0BfxJM0ueEdPzP5irIs6Et4Pjd0KyhzW_HJARXlqRFU34IELOyncMD9qhTP0p)

![img](https://lh6.googleusercontent.com/ZRmPByGHK_fSRICYz7GjbqtynBgnuCgu5--ivQtjzelIRnN95ks7D3tawpevu4OcgoFS8NrecvdV0jNY1gW-zGYSWwnFLyQos4kJoqGznsEGg0Z-cnrGw5EFtZTRMr9Yhgm56Xgp)

- En este no ha encontrado ninguna amenaza.