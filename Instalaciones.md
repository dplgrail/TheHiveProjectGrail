[TOC]

# Instalaciones

## Prerrequisitos

Instale todos los paquetes necesarios para la instalación:

```
apt install curl apt-transport-https unzip wget libcap2-bin software-properties-common lsb-release gnupg2
```

Agregue el repositorio para Java Development Kit (JDK):

```
add-apt-repository ppa:openjdk-r/ppa
```

Actualice los datos del repositorio:

```
apt update
```

Instale todas las utilidades necesarias:

```
export JAVA_HOME=/usr/ && apt install openjdk-11-jdk
```

## Wazuh

El servidor de Wazuh recopila y analiza datos de los agentes de Wazuh desplegados. Ejecuta el administrador de Wazuh, la API de Wazuh y Filebeat.

El primer paso para configurar Wazuh es agregar el repositorio de Wazuh al servidor.

1. Instale la clave GPG:

```
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | apt-key add -
```

2. Agrega el repositorio:

```
echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list
```

3. Actualice la información del paquete:

```
apt-get update
```



### Instalación del administrador de Wazuh[¶](https://documentation.wazuh.com/4.0/installation-guide/open-distro/all-in-one-deployment/all_in_one.html#installing-the-wazuh-manager)

1. Instale el paquete del administrador de Wazuh:

```
apt-get install wazuh-manager=4.0.4-1
```

2. Habilite e inicie el servicio de administrador de Wazuh:

   ```
   systemctl daemon-reload
   systemctl enable wazuh-manager
   systemctl start wazuh-manager
   ```

3. Ejecute el siguiente comando para verificar si el administrador de Wazuh está activo:

```
systemctl status wazuh-manager
```

## Instalación de Elasticsearch[¶](https://documentation.wazuh.com/4.0/installation-guide/open-distro/all-in-one-deployment/all_in_one.html#installing-elasticsearch)

Open Distro para Elasticsearch es una distribución de código abierto de Elasticsearch, un motor de búsqueda de texto completo altamente escalable. Ofrece seguridad avanzada, alertas, administración de índices, análisis profundo del rendimiento y varias otras características adicionales.

Instale Elasticsearch OSS y Open Distro para Elasticsearch:

```
apt install elasticsearch-oss opendistroforelasticsearch=1.11.0-1
```

### Configurar Elasticsearch[¶](https://documentation.wazuh.com/4.0/installation-guide/open-distro/all-in-one-deployment/all_in_one.html#configuring-elasticsearch)

Descargue el archivo de configuración de la `/etc/elasticsearch/elasticsearch.yml`siguiente manera:

```
# curl -so /etc/elasticsearch/elasticsearch.yml https://raw.githubusercontent.com/wazuh/wazuh-documentation/4.0/resources/open-distro/elasticsearch/7.x/elasticsearch_all_in_one.yml
```

### Roles y usuarios de Elasticsearch[¶](https://documentation.wazuh.com/4.0/installation-guide/open-distro/all-in-one-deployment/all_in_one.html#elasticsearch-roles-and-users)

Para usar el complemento Wazuh Kibana correctamente, es necesario agregar roles y usuarios adicionales:

```
curl -so /usr/share/elasticsearch/plugins/opendistro_security/securityconfig/roles.yml https://raw.githubusercontent.com/wazuh/wazuh-documentation/4.0/resources/open-distro/elasticsearch/roles/roles.yml
curl -so /usr/share/elasticsearch/plugins/opendistro_security/securityconfig/roles_mapping.yml https://raw.githubusercontent.com/wazuh/wazuh-documentation/4.0/resources/open-distro/elasticsearch/roles/roles_mapping.yml
curl -so /usr/share/elasticsearch/plugins/opendistro_security/securityconfig/internal_users.yml https://raw.githubusercontent.com/wazuh/wazuh-documentation/4.0/resources/open-distro/elasticsearch/roles/internal_users.yml
```

Los comandos anteriores agregan los siguientes usuarios de Wazuh en Kibana:

| Usuarios    | Roles                                                        |
| :---------- | :----------------------------------------------------------- |
| wazuh_user  | Creado para usuarios que necesitan acceso de solo lectura al complemento Wazuh Kibana. Complemento de Kibana. |
| wazuh_admin | Usuario recomendado para usuarios que necesitan privilegios administrativos. privilegios. |

Se agregan dos roles adicionales, cuya función es otorgar los permisos adecuados a los usuarios:

| Usuarios       | Roles                                                        |
| -------------- | ------------------------------------------------------------ |
| wazuh_ui_user  | Este rol proporciona `wazuh_user`permisos para leer los índices de Wazuh. |
| wazuh_ui_admin | Este rol permite `wazuh_admin`realizar tareas de lectura, escritura, gestión e indexación en los índices de Wazuh. |

Estos usuarios y roles están diseñados para operar junto con el complemento Wazuh Kibana y están protegidos para que no se puedan modificar desde la interfaz de Kibana. Para modificarlos o agregar nuevos usuarios o roles, `securityadmin`se debe ejecutar el script.

### Creación de certificados[¶](https://documentation.wazuh.com/4.0/installation-guide/open-distro/all-in-one-deployment/all_in_one.html#certificates-creation)

1. Elimine los certificados de demostración:


```
# rm /etc/elasticsearch/esnode-key.pem /etc/elasticsearch/esnode.pem /etc/elasticsearch/kirk-key.pem /etc/elasticsearch/kirk.pem /etc/elasticsearch/root-ca.pem -f
```

2. Genere e implemente los certificados:

   - Vaya a la ubicación de instalación y cree el directorio de certificados:

   ```
   # mkdir /etc/elasticsearch/certs
   # cd /etc/elasticsearch/certs
   ```

   - Descargue la herramienta TLS sin conexión de Search Guard para crear los certificados:

   ```
   # curl -so ~/search-guard-tlstool-1.8.zip https://maven.search-guard.com/search-guard-tlstool/1.8/search-guard-tlstool-1.8.zip
   ```

   - ​	Extrae el archivo descargado. Se asume que se ha descargado en `~/`(directorio de inicio):

   ```
   # unzip ~/search-guard-tlstool-1.8.zip -d ~/searchguard
   ```

   - Descarga el `search-guard.yml`archivo de configuración. Este archivo está preconfigurado para generar todos los certificados necesarios:

   ```
   # curl -so ~/searchguard/search-guard.yml https://raw.githubusercontent.com/wazuh/wazuh-documentation/4.0/resources/open-distro/searchguard/search-guard-aio.yml
   ```

   - Ejecute el script de Search Guard para crear los certificados:

   ```
   #  ~/searchguard/tools/sgtlstool.sh -c ~/searchguard/search-guard.yml -ca -crt -t /etc/elasticsearch/certs/
   ```

   - Una vez creados los certificados, elimine los archivos innecesarios:

   ```
   # rm /etc/elasticsearch/certs/client-certificates.readme /etc/elasticsearch/certs/elasticsearch_elasticsearch_config_snippet.yml ~/search-guard-tlstool-1.8.zip ~/searchguard -rf
   ```

3. Habilite e inicie el servicio Elasticsearch:

   ```
   # systemctl daemon-reload
   # systemctl enable elasticsearch
   # systemctl start elasticsearch
   ```

4. Ejecute el `securityadmin` script de Elasticsearch para cargar la información de los nuevos certificados e iniciar el clúster:

```
# /usr/share/elasticsearch/plugins/opendistro_security/tools/securityadmin.sh -cd /usr/share/elasticsearch/plugins/opendistro_security/securityconfig/ -nhnv -cacert /etc/elasticsearch/certs/root-ca.pem -cert /etc/elasticsearch/certs/admin.pem -key /etc/elasticsearch/certs/admin.key
```

Ejecute el siguiente comando para asegurarse de que la instalación se haya realizado correctamente:

```
# curl -XGET https://localhost:9200 -u admin:admin -k
```

Un ejemplo de respuesta debería tener el siguiente aspecto:

```
 {
   "name" : "node-1",
   "cluster_name" : "elasticsearch",
   "cluster_uuid" : "2gIeOOeUQh25c2yU0Pd-RQ",
   "version" : {
     "number" : "7.9.1",
     "build_flavor" : "oss",
     "build_type" : "rpm",
     "build_hash" : "083627f112ba94dffc1232e8b42b73492789ef91",
     "build_date" : "2020-09-01T21:22:21.964974Z",
     "build_snapshot" : false,
     "lucene_version" : "8.6.2",
     "minimum_wire_compatibility_version" : "6.8.0",
     "minimum_index_compatibility_version" : "6.0.0-beta1"
   },
   "tagline" : "You Know, for Search"
 }
```

[^Nota]: El complemento de analizador de rendimiento Open Distro for Elasticsearch se instala de forma predeterminada y puede tener un impacto negativo en los recursos del sistema. Recomendamos eliminarlo con el siguiente comando . Asegúrese de reiniciar el servicio Elasticsearch después.`/usr/share/elasticsearch/bin/elasticsearch-plugin remove opendistro_performance_analyzer`

## Instalación de Filebeat[¶](https://documentation.wazuh.com/4.0/installation-guide/open-distro/all-in-one-deployment/all_in_one.html#installing-filebeat)

Filebeat es la herramienta en el servidor de Wazuh que reenvía de forma segura alertas y eventos archivados a Elasticsearch.

1. Instale el paquete Filebeat:

```
apt-get install filebeat=7.9.1
```

2. Descargue el archivo de configuración de Filebeat preconfigurado que se usa para reenviar las alertas de Wazuh a Elasticsearch:

```
curl -so /etc/filebeat/filebeat.yml https://raw.githubusercontent.com/wazuh/wazuh-documentation/4.0/resources/open-distro/filebeat/7.x/filebeat_all_in_one.yml
```

3. Descargue la plantilla de alertas para Elasticsearch:


```
curl -so /etc/filebeat/wazuh-template.json https://raw.githubusercontent.com/wazuh/wazuh/4.0/extensions/elasticsearch/7.x/wazuh-template.json
chmod go+r /etc/filebeat/wazuh-template.json
```

4. Descargue el módulo Wazuh para Filebeat:


```
curl -s https://packages.wazuh.com/4.x/filebeat/wazuh-filebeat-0.1.tar.gz | tar -xvz -C /usr/share/filebeat/module
```

5. Copie los certificados de Elasticsearch en `/etc/filebeat/certs`:


```
mkdir /etc/filebeat/certs
cp /etc/elasticsearch/certs/root-ca.pem /etc/filebeat/certs/
mv /etc/elasticsearch/certs/filebeat* /etc/filebeat/certs/
```

6. Habilite e inicie el servicio Filebeat:

```
systemctl daemon-reload
systemctl enable filebeat
systemctl start filebeat
```

Para asegurarse de que Filebeat se haya instalado correctamente, ejecute el siguiente comando:

```
filebeat test output
```

Un ejemplo de respuesta debería tener el siguiente aspecto:

```
 elasticsearch: https://127.0.0.1:9200...
   parse url... OK
   connection...
     parse host... OK
     dns lookup... OK
     addresses: 127.0.0.1
     dial up... OK
   TLS...
     security: server's certificate chain verification is enabled
     handshake... OK
     TLS version: TLSv1.3
     dial up... OK
   talk to server... OK
   version: 7.9.1
```

## Instalación de Kibana[¶](https://documentation.wazuh.com/4.0/installation-guide/open-distro/all-in-one-deployment/all_in_one.html#installing-kibana)

Kibana es una interfaz web flexible e intuitiva para minar y visualizar los eventos y archivos almacenados en Elasticsearch.

1. Instale el paquete de Kibana:

```
apt-get install opendistroforelasticsearch-kibana=1.11.0-1
```

2. Descargue el archivo de configuración de Kibana:


```
curl -so /etc/kibana/kibana.yml https://raw.githubusercontent.com/wazuh/wazuh-documentation/4.0/resources/open-distro/kibana/7.x/kibana_all_in_one.yml
```

En el `/etc/kibana/kibana.yml`archivo, la configuración `server.host`tiene el valor `0.0.0.0`. Significa que se puede acceder a Kibana desde el exterior y aceptará todas las direcciones IP disponibles del host. Este valor se puede cambiar para una IP específica si es necesario.

3. Actualice los permisos de los directorios `optimize`y `plugins`:


```
chown -R kibana:kibana /usr/share/kibana/optimize
chown -R kibana:kibana /usr/share/kibana/plugins
```

4. Instale el complemento Wazuh Kibana. La instalación del complemento debe realizarse desde el directorio de inicio de Kibana de la siguiente manera:

```
cd /usr/share/kibana
sudo -u kibana /usr/share/kibana/bin/kibana-plugin install https://packages.wazuh.com/4.x/ui/kibana/wazuh_kibana-4.0.4_7.9.1-1.zip
```

5. Copie los certificados de Elasticsearch en `/etc/kibana/certs`:


```
mkdir /etc/kibana/certs
cp /etc/elasticsearch/certs/root-ca.pem /etc/kibana/certs/
mv /etc/elasticsearch/certs/kibana_http.key /etc/kibana/certs/kibana.key
mv /etc/elasticsearch/certs/kibana_http.pem /etc/kibana/certs/kibana.pem
```

6. Vincula el socket de Kibana al puerto privilegiado 443:


```
setcap 'cap_net_bind_service=+ep' /usr/share/kibana/node/bin/node
```

7. Habilite e inicie el servicio Kibana:

```
systemctl daemon-reload
systemctl enable kibana
systemctl start kibana
```

8. Acceda a la interfaz web:

```
URL: https://<wazuh_server_ip>
user: admin
password: admin
```

Tras el primer acceso a Kibana, el navegador muestra un mensaje de advertencia que indica que el certificado no fue emitido por una autoridad confiable. Se puede agregar una excepción en las opciones avanzadas del navegador web o, para mayor seguridad, el `root-ca.pem`archivo generado previamente se puede importar al administrador de certificados del navegador. Alternativamente, se puede configurar un certificado de una autoridad confiable.

Se recomienda encarecidamente cambiar las contraseñas predeterminadas de Elasticsearch para los usuarios que se encuentran en el `/usr/share/elasticsearch/plugins/opendistro_security/securityconfig/internal_users.yml`archivo. Puede encontrar más información sobre este proceso en nuestro [manual de usuario](https://documentation.wazuh.com/4.0/user-manual/elasticsearch/elastic_tuning.html#change-elastic-pass) . También se recomienda personalizar el archivo `/etc/elasticsearch/jvm.options`para mejorar el rendimiento de Elasticsearch. Obtenga más información sobre este proceso en la sección de [ajuste de Elasticsearch](https://documentation.wazuh.com/4.0/user-manual/elasticsearch/elastic_tuning.html#elastic-tuning) .

Una vez que Kibana se está ejecutando, es necesario asignar a cada usuario su rol correspondiente. Para obtener más información, visite [la sección de configuración del complemento Wazuh Kibana](https://documentation.wazuh.com/4.0/user-manual/kibana-app/connect-kibana-app.html#connect-kibana-app) .

###### Próximos pasos

Una vez que el entorno de Wazuh está listo, se puede instalar un agente de Wazuh en cada punto final que se supervisará. La guía de instalación del agente de Wazuh está disponible para la mayoría de los sistemas operativos y se puede encontrar [en nuestra guía de instalación](https://documentation.wazuh.com/4.0/installation-guide/wazuh-agent/index.html#installation-agents) .

## TheHive

## Cortex

## MISP

Para la instalación de **MISP** recomendamos usar un contenedor ya que es más fácil que instalarlo desde la fuente. Hemos dejado un *docker-compose.yml* correspondiente.

Abra un navegador web en [https : // localhost](https://localhost/)

Úselo `admin@admin.test`como nombre de usuario y `admin`como contraseña.

Se le pedirá que cambie su contraseña. La nueva contraseña debe tener al menos 12 caracteres con una mayúscula y un carácter especial.

### Configurar MISP

Administración> Configuración y mantenimiento del servidor> Configuración de MISP
MISP.live to TRUE
MISP.disable_emailing to TRUE
MISP.baseurl to the IP of MISP

Administración> Tareas programadas
Establezca fetch_feeds en 24 y haga clic en "Actualizar todo"

Acciones de sincronización> Fuentes de lista
Elija una fuente de lista para suscribirse. Elegí malwaredomainlist. Marque la casilla y haga clic en "Habilitar fuente" en la parte superior.
Ahora busque esa fuente en la lista nuevamente, mire a la derecha en los íconos para una lupa y un bote de basura. Haga clic en el círculo con la flecha hacia abajo para "Obtener todos los eventos". Verá una tarea ejecutándose en Administración> Trabajos

En el mismo grupo de iconos, haga clic en la lupa. Esto le mostrará la lista de direcciones IP incluidas en esta lista de bloqueo. Copie uno de ellos, lo usaremos más tarde para probarlo.