Title: Realizar a instalação

# Realizar a instalação

Instalação do Servidor de Aplicação Wildfly
-------------------------------------------

1. Descompactar o pacote JAVA JDK no diretório /opt e criar um link
simbólico conforme mostrado no exemplo abaixo. *(Caso já tenha feito a
instalação do item Servidor de Indexação Apache Solr (sessão Configuração dos
pacotes) no mesmo servidor que ficará o Wildfly, não será necessário a execução
dos comandos de instalação do Java JDK abaixo)*.

    ```sh
    tar xzvf jdk-8u172-linux-x64.tar.gz -C /opt/
    ```
    
    ```sh
    ln -s /opt/jdk1.8.0_172 /opt/jdk
    ```
    
2. Executar os comandos abaixo para configuração dos pacotes para o CITSmart;
    
    ```sh
    tar xzvf wildfly-12.0.0.Final.tar.gz -C /opt/ 
    ```
    
    ```sh
    ln -s /opt/wildfly-12.0.0.Final /opt/wildfly 
    ```
    
    ```sh
    cp /etc/skel/.bash_profile /opt/wildfly/
    ```
    
    ```sh
    tar xzvf assets.tar.gz -C /opt/wildfly/
    ```
    
    ```sh
    mkdir /opt/wildfly/reports
    ```
    
3. Criar um usuário para administração do Wildfly;

    ```sh
    groupadd -r citsmart
    ```

    ```sh
    useradd -r -g citsmart -d /opt/wildfly -s /sbin/nologin citsmart
    ```

    ```sh
    chown citsmart:citsmart /opt/wildfly-12.0.0.Final/ -R
    ```

    ```sh
    chown citsmart:citsmart /opt/jdk1.8.0_172/ -R
    ```

4. Configurar o **PATH** do para o JAVA_HOME e o JBOSS_HOME. Para
isso fazer conforme exemplo abaixo.

    ```sh
    vim /opt/wildfly/.bash_profile
    ```
    ```sh
    export JAVA_HOME="/opt/jdk"
    ```
    ```sh
    export JBOSS_HOME="/opt/wildfly"
    ```
    ```sh
    export PATH="$JAVA_HOME/bin:$JBOSS_HOME/bin:$PATH"
    ```
    
5. Fazer um teste para validar se o Wildfly está iniciando corretamente até esse
ponto. Para isso executar os comandos abaixo.

    ```sh
    su - citsmart -s /bin/bash
    ```

    ```sh
    java -version
    ```
    ```html
    java version "1.8.0_172"
    Java(TM) SE Runtime Environment (build 1.8.0_172-b11)
    Java HotSpot(TM) 64-Bit Server VM (build 25.172-b11, mixed mode)
    ```
    ```sh
    bin/standalone.sh
    ```

6. Parar o Wildfly (Iniciado anteriormente) e configurar o standalone.conf no
diretório \$JBOSS_HOME/bin, conforme mostrado abaixo.

    ```sh
    mv standalone.conf standalone.dist
    ```

    ```sh
    vim standalone.conf
    ```
    ```java
    if [ "x$JBOSS_MODULES_SYSTEM_PKGS" = "x" ]; then
    JBOSS_MODULES_SYSTEM_PKGS="org.jboss.byteman"
    fi  
    if [ "x$JAVA_OPTS" = "x" ]; then
    JAVA_OPTS="$JAVA_OPTS -Xms5200m"
    JAVA_OPTS="$JAVA_OPTS -Xmx5200m"
    JAVA_OPTS="$JAVA_OPTS -XX:MinHeapFreeRatio=40"
    JAVA_OPTS="$JAVA_OPTS -XX:MaxHeapFreeRatio=80"
    JAVA_OPTS="$JAVA_OPTS -XX:NewRatio=8"
    JAVA_OPTS="$JAVA_OPTS -XX:SurvivorRatio=32"
    JAVA_OPTS="$JAVA_OPTS -XX:+UseG1GC"
    JAVA_OPTS="$JAVA_OPTS -XX:G1HeapRegionSize=4"
    JAVA_OPTS="$JAVA_OPTS -XX:InitiatingHeapOccupancyPercent=50"
    JAVA_OPTS="$JAVA_OPTS -Djava.net.preferIPv4Stack=true"
    JAVA_OPTS="$JAVA_OPTS -Dorg.jboss.resolver.warning=true"
    JAVA_OPTS="$JAVA_OPTS -Duser.timezone="America/Sao_Paulo""
    JAVA_OPTS="$JAVA_OPTS -Djboss.modules.system.pkgs=$JBOSS_MODULES_SYSTEM_PKGS"
    JAVA_OPTS="$JAVA_OPTS -Djava.awt.headless=true"
    JAVA_OPTS="$JAVA_OPTS -Djboss.server.default.config=standalone-full-ha.xml"
    JAVA_OPTS="$JAVA_OPTS -Djboss.bind.address=0.0.0.0"
    JAVA_OPTS="$JAVA_OPTS -Djboss.bind.address.management=0.0.0.0"
    else
    echo "JAVA_OPTS already set in environment; overriding default settings with values: $JAVA_OPTS"
    fi
    ```
    ```sh
    chown citsmart:citsmart /opt/wildfly/bin/standalone.conf
    ```
### Configuração do Servidor de Aplicação Wildfly

Todas as configurações feitas neste documento serão feitas através do jboss-cli. Para isso, inicie o Wildfly em standalone, conecte-se ao jboss-cli e execute os seguintes comandos.

```sh
su citsmart /opt/wildfly/bin/standalone.sh -s /bin/bash
```

```sh
/opt/wildfly/bin/jboss-cli.sh --connect
```

```sh
[standalone@localhost:9990 /]
```

### Configuração do System Properties

No bash do CLI executar os comandos abaixo para criação das propriedades do
CITSmart.

```java
/system-property=mongodb.host:add(value="mongodb.citsmart.com")
/system-property=mongodb.port:add(value="27017")
/system-property=mongodb.user:add(value="admin")
/system-property=mongodb.password:add(value="admin")
/system-property=citsmart.protocol:add(value="http")
/system-property=citsmart.host:add(value="itsm.citsmart.com")
/system-property=citsmart.port:add(value="8080")
/system-property=citsmart.context:add(value="citsmart")
/system-property=citsmart.login:add(value="citsmart.local\\\consultor")
/system-property=citsmart.password:add(value="senhaConsultor")
/system-property=citsmart.inventory.id:add(value="citsmartinventory")
/system-property=citsmart.evm.id:add(value="citsmartevm")
/system-property=citsmart.evm.enable:add(value=true)
/system-property=citsmart.inventory.enable:add(value=true)
/system-property=rhino.scripts.directory:add(value="")
/system-property=citsmart.port.updateparameters:add(value="9000")
/system-property name="citsmart.inventory.pagelength" (value="100")
```

### Configuração dos Datasources

Antes de criar os datasources, deve-se adicionar ao Wildfly o modulo JDBC do
PostgreSQL. Para isso, sair do modo jboss-cli e executar os comandos abaixo.

1. Adicionar o modulo do banco de dados conforme exemplo abaixo:

    ```sh
    mkdir -p /opt/wildfly/modules/system/layers/base/org/postgres/main
    ```

    ```sh
    tar xzvf postgresql-jdbc-driver.tar.gz -C /opt/wildfly/modules/system/layers/base/org/postgres/main
    ```

    ```sh
    chown citsmart:citsmart /opt/wildfly/modules/system/layers/base/org/postgres/ -R
    ```

2. Conectar no jboss-cli novamente e executar o comando abaixo para adicionar o
modulo ao standalone-full-ha.xml

   
    ```sh
    module add --name=org.postgres --resources=/opt/wildfly/modules/system/layers/base/org/postgres/main/postgresql-9.3-1103.jdbc41.jar --dependencies=javax.api,javax.transaction.api
    ```
    ```sh
    /subsystem=datasources/jdbc-driver=postgres:add(driver-name="postgres",driver-module-name="org.postgres",driver-xa-datasource-class-name=org.postgresql.xa.PGXADataSource
    ```

3. Existem **oito entradas** de datasource para o **citsmart_db**, sendo que quatro são para o Citsmart e quatro para o Citsmart Neuro. O usuário e senha é **citsmartdbuser e exemplo123**, respectivamente, criados no item *Servidor de Banco de Dados PostgreSQL*;

4. Para criar os datasources, execute os comandos CLI abaixo:

    Datasource citsmart:

    ```sh
    /subsystem=datasources/data-source="/jdbc/citsmart":add(jndi-name="java:/jdbc/citsmart",driver-name="postgres",connection-url="jdbc:postgresql://pgdata.citsmart.com:5432/citsmart_db",user-name="citsmartdbuser",password="exemplo123",driver-class="org.postgresql.Driver", enabled=true, use-java-context=true)
    /subsystem=datasources/data-source="/jdbc/citsmart":write-attribute(name=min-pool-size,value=10)
    /subsystem=datasources/data-source="/jdbc/citsmart":write-attribute(name=max-pool-size,value=300)
    /subsystem=datasources/data-source="/jdbc/citsmart":write-attribute(name=pool-prefill,value=true)
    /subsystem=datasources/data-source="/jdbc/citsmart":write-attribute(name=flush-strategy,value=FailingConnectionOnly)
    /subsystem=datasources/data-source="/jdbc/citsmart":write-attribute(name=blocking-timeout-wait-millis,value=60000)
    /subsystem=datasources/data-source="/jdbc/citsmart":write-attribute(name=idle-timeout-minutes,value=5)
    ```

    Datasource citsmartFlow:

    ```sh
    /subsystem=datasources/data-source="/jdbc/citsmartFluxo":add(jndi-name="java:/jdbc/citsmartFluxo",driver-name="postgres",connection-url="jdbc:postgresql://pgdata.citsmart.com:5432/citsmart_db",user-name="citsmartdbuser",password="exemplo123",driver-class="org.postgresql.Driver", enabled=true, use-java-context=true)
    /subsystem=datasources/data-source="/jdbc/citsmartFluxo":write-attribute(name=min-pool-size,value=10)
    /subsystem=datasources/data-source="/jdbc/citsmartFluxo":write-attribute(name=max-pool-size,value=300)
    /subsystem=datasources/data-source="/jdbc/citsmartFluxo":write-attribute(name=pool-prefill,value=true)
    /subsystem=datasources/data-source="/jdbc/citsmartFluxo":write-attribute(name=flush-strategy,value=FailingConnectionOnly)
    /subsystem=datasources/data-source="/jdbc/citsmartFluxo":write-attribute(name=blocking-timeout-wait-millis,value=60000)
    /subsystem=datasources/data-source="/jdbc/citsmartFluxo":write-attribute(name=idle-timeout-minutes,value=5)
    ```

    Datasourece citsmart_reports

    ```sh
    /subsystem=datasources/data-source="/jdbc/citsmart_reports":add(jndi-name="java:/jdbc/citsmart_reports",driver-name="postgres",connection-url="jdbc:postgresql://pgdata.citsmart.com:5432/citsmart_db",user-name="citsmartdbuser",password="exemplo123",driver-class="org.postgresql.Driver", enabled=true, use-java-context=true)
    /subsystem=datasources/data-source="/jdbc/citsmart_reports":write-attribute(name=min-pool-size,value=10)
    /subsystem=datasources/data-source="/jdbc/citsmart_reports":write-attribute(name=max-pool-size,value=300)
    /subsystem=datasources/data-source="/jdbc/citsmart_reports":write-attribute(name=pool-prefill,value=true)
    /subsystem=datasources/data-source="/jdbc/citsmart_reports":write-attribute(name=flush-strategy,value=FailingConnectionOnly)
    /subsystem=datasources/data-source="/jdbc/citsmart_reports":write-attribute(name=blocking-timeout-wait-millis,value=60000)
    /subsystem=datasources/data-source="/jdbc/citsmart_reports":write-attribute(name=idle-timeout-minutes,value=5)
    ```

    Datasource citsmartBpmEventos

    ```sh
    /subsystem=datasources/data-source="/jdbc/citsmartBpmEventos":add(jndi-name="java:/jdbc/citsmartBpmEventos",driver-name="postgres",connection-url="jdbc:postgresql://pgdata.citsmart.com:5432/citsmart_db",user-name="citsmartdbuser",password="exemplo123",driver-class="org.postgresql.Driver", enabled=true, use-java-context=true)
    /subsystem=datasources/data-source="/jdbc/citsmartBpmEventos":write-attribute(name=min-pool-size,value=10)
    /subsystem=datasources/data-source="/jdbc/citsmartBpmEventos":write-attribute(name=max-pool-size,value=300)
    /subsystem=datasources/data-source="/jdbc/citsmartBpmEventos":write-attribute(name=pool-prefill,value=true)
    /subsystem=datasources/data-source="/jdbc/citsmartBpmEventos":write-attribute(name=flush-strategy,value=FailingConnectionOnly)
    /subsystem=datasources/data-source="/jdbc/citsmartBpmEventos":write-attribute(name=blocking-timeout-wait-millis,value=60000)
    /subsystem=datasources/data-source="/jdbc/citsmartBpmEventos":write-attribute(name=idle-timeout-minutes,value=5
    ```

    Datasource citsmart-neuro

    ```sh
    /subsystem=datasources/data-source="/env/jdbc/citsmart-neuro":add(jndi-name="java:/env/jdbc/citsmart-neuro",driver-name="postgres",connection-url="jdbc:postgresql://pgdata.citsmart.com:5432/citsmart_db",user-name="citsmartdbuser",password="exemplo123",driver-class="org.postgresql.Driver", enabled=true, use-java-context=true)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=min-pool-size,value=10)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=max-pool-size,value=300)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=pool-prefill,value=true)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=flush-strategy,value=FailingConnectionOnly)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=blocking-timeout-wait-millis,value=60000)
    ```

    Datasource citsmart-neuro-app1

    ```sh
    /subsystem=datasources/data-source="/env/jdbc/citsmart-neuro-app1":add(jndi-name="java:/env/jdbc/citsmart-neuro-app1",driver-name="postgres",connection-url="jdbc:postgresql://pgdata.citsmart.com:5432/citsmart_db",user-name="citsmartdbuser",password="exemplo123",driver-class="org.postgresql.Driver", enabled=true, use-java-context=true)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=min-pool-size,value=10)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=max-pool-size,value=300)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=pool-prefill,value=true)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=flush-strategy,value=FailingConnectionOnly)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=blocking-timeout-wait-millis,value=60000)
    ```

    Datasource citsmart-neuro-app2

    ```sh
    /subsystem=datasources/data-source="/env/jdbc/citsmart-neuro-app2":add(jndi-name="java:/env/jdbc/citsmart-neuro-app2",driver-name="postgres",connection-url="jdbc:postgresql://pgdata.citsmart.com:5432/citsmart_db",user-name="citsmartdbuser",password="exemplo123",driver-class="org.postgresql.Driver", enabled=true, use-java-context=true)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=min-pool-size,value=10)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=max-pool-size,value=300)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=pool-prefill,value=true)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=flush-strategy,value=FailingConnectionOnly)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=blocking-timeout-wait-millis,value=60000)
    ```

    Datasource citsmart-neuro-app3

    ```sh
    /subsystem=datasources/data-source="/env/jdbc/citsmart-neuro-app3":add(jndi-name="java:/env/jdbc/citsmart-neuro-app3",driver-name="postgres",connection-url="jdbc:postgresql://pgdata.citsmart.com:5432/citsmart_db",user-name="citsmartdbuser",password="exemplo123",driver-class="org.postgresql.Driver", enabled=true, use-java-context=true)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=min-pool-size,value=10)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=max-pool-size,value=300)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=pool-prefill,value=true)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=flush-strategy,value=FailingConnectionOnly)
    /subsystem=datasources/data-source="/env\/jdbc\/citsmart-neuro":write-attribute(name=blocking-timeout-wait-millis,value=60000)
    ```



5. Antes de sair do jboss-cli executar o comando reload para aplicar as alterações e fazer um teste de conexão com a base de dados.
    
    ```sh
    [standalone\@localhost:9990 /] :reload
    ```
    ```sh
    [standalone\@localhost:9990 /] /subsystem=datasources/data-source="/jdbc/citsmart":test-connection-in-pool { "outcome" =\> "success", "result" =\> [true] }
    ```

### Configurando os Subsystems


```sh
/subsystem=logging/root-logger=ROOT:write-attribute(name=level,value=INFO)
/subsystem=logging/console-handler=CONSOLE:write-attribute(name=level,value=INFO)
/subsystem=undertow/server=default-server/http-listener=default:write-attribute(name=max-post-size,value="5000485760")
/subsystem=undertow/server=default-server/http-listener=default:write-attribute(name=max-parameters,value="3000")
/subsystem=undertow/server=default-server/http-listener=default:write-attribute(name=max-header-size,value="65535")
/subsystem=undertow/server=default-server/https-listener=https:write-attribute(name=max-post-size,value="5000485760")
/subsystem=undertow/server=default-server/https-listener=https:write-attribute(name=max-header-size,value="65535")
/subsystem=undertow/server=default-server/https-listener=https:write-attribute(name=max-parameters,value="3000")
/subsystem=undertow/configuration=filter/rewrite=citsmart:add(target="/citsmart")
/subsystem=undertow/server=default-server/host=default-host/filter-ref=citsmart:add(predicate="regex('\^/?\$') and equals(/citsmart)")
/subsystem=undertow/server=default-server/host=default-host/setting=access-log:add
/subsystem=undertow/server=default-server/host=default-host/setting=access-log:write-attribute(name=pattern, value="%h %l %u [%t] \\"%r\\" %s %b \\"%{i,Referer}\\" \\"%{i,User-Agent}\\"")
/subsystem=messaging-activemq/server=default/jms-queue=filaDocumentoQueue:add(entries=["queue/filaDocumento","java:jboss/exported/jms/queue/filaDocumento"])
/subsystem=messaging-activemq/server=default/jms-topic=filaDocumentoTopic:add(entries=["topic/filaDocumento","java:jboss/exported/jms/topic/filaDocumento"])
/subsystem=messaging-activemq/server=default/jms-queue=neuroInputQueue:add(entries=["queue/neuroInputQueue","java:jboss/exported/jms/queue/queue/neuroInputQueue"])
/subsystem=messaging-activemq/server=default/jms-queue=neuroOutputQueue:add(entries=["queue/neuroOutputQueue","java:jboss/exported/jms/queue/queue/neuroOutputQueue"])
/subsystem=deployment-scanner/scanner=default:write-attribute(name=deployment-timeout,value=6000000)
```

    1. Para possibilitar o upload acima de 10 Mb, incluir no arquivo subsystems a seguinte informação:

    ```java
    <subsystem xmlns="urn:jboss:domain:undertow:5.0">
            <buffer-cache name="default"/>
            <server name="default-server">
                <http-listener name="default" socket-binding="http" max-post-size="5000485760" max-header-size="65535" max-parameters="3000" redirect-socket="https" enable-http2="true"/>
                <https-listener name="https" socket-binding="https" max-post-size="5000485760" max-header-size="65535" max-parameters="3000" security-realm="ApplicationRealm" enable-http2="true"/>

            ...
            </server>
    ...
    </subsystem>
    ```

    2. Antes de sair do jboss-cli executar o comando reload para aplicar as alterações.

```sh
[standalone\@localhost:9990 /] :reload
```

## Criação do arquivo citsmart.cfg

1. No arquivo citsmart.cfg, o valor padrão é TRUE, ou seja, se essa opção não existir no arquivo, o sistema utilizará o valor TRUE para essa propriedade. Definido como TRUE, ativa o Thread que atualiza a tabela de fatos de solicitações de serviço na inicialização do sistema. Definido como FALSE, a atualização ocorrerá somente após a inclusão ou alteração da solicitação de serviço;

2. Deve-se criar um arquivo citsmart.cfg in /opt/wildfly/standalone/configuration/ com as informações abaixo:


    ```java
    START_MONITORA_INCIDENTES=FALSE
    JDBC_ALIAS_REPORTS=
    JDBC_ALIAS_BPM=
    JDBC_ALIAS_BPM_EVENTOS=
    START_VERIFICA_EVENTOS=FALSE
    QUANTIDADE_BACKUPLOGDADOS=1000
    START_MODE_RULES=FALSE
    START_MODE_RULES=FALSE
    LOAD_FACTSERVICEREQUESTRULES = TRUE
    ```

    !!! Abstract "ATENÇÃO"
    
        Não esquecer de alterar o dono dos arquivos e diretórios para o usuário CITSmart.


## Criação de diretórios para instalação


!!! Abstract "ATENÇÃO"

    Não esquecer de alterar o dono do diretório /opt/citsmart .
    

1. Criar os diretórios abaixo para serem configurados nos 3 passos de instalação web.

    Para GED: 

    ```sh
    mkdir -p /opt/citsmart/ged
    ```
    Para Base de Conhecimento:
	
    ```sh
    mkdir /opt/citsmart/kb
    ```
    Para Palavras Sinônimas:
	
	```sh
    mkdir /opt/citsmart/twinwords
    ```
    Para Anexos de Base de Conhecimento:
	
    ```sh
    mkdir /opt/citsmart/attachkb
    ```
    Para Upload: 
	
    ```
	mkdir /opt/citsmart/upload
    ```


## Geração de certificado auto assinado SSL

Para o Wildfly será gerado um certificado auto assinado.
Caso possua um certificado é importante utilizá-lo.

1. Conectar no servidor do Wildfly.
    
    Criando aliás novo com DNS (exemplo itsm.citsmart.com): 
    
    
    ```sh
    /opt/jdk/bin/keytool -genkey -alias GRPv1 -keyalg RSA -keystore /opt/wildfly/standalone/configuration/GRPv1.keystore -ext san=dns:itsm.citsmart.com -validity 3650 -storepass 123456 
    ```
    
    Criando alias com IP do servidor do Jboss (exemplo 192.168.0.40): 
    
    ```
    /opt/jdk/bin/keytool -genkey -alias GRPv1 -keyalg RSA -keystore /opt/wildfly/standalone/configuration/GRPv1.keystore -ext san=ip:192.168.0.40 -validity 3650 -storepass 123456 
    ```
    
    Exportando certificado para extensão .cer:
    
    ```
    /opt/jdk/bin/keytool -export -alias GRPv1 -keystore /opt/wildfly/standalone/configuration/GRPv1.keystore -validity 3650 -file /opt/wildfly/standalone/configuration/GRPv1.cer 
    ```
    
    Adicionando certificado no cacerts do Java:
    
    ```
    /opt/jdk/bin/keytool -keystore /opt/jdk/jre/lib/security/cacerts -importcert -alias GRPv1 -file /opt/wildfly/standalone/configuration/GRPv1.cer
    ```
    
    **Lembrar de aplicar as permissões para o dono do wildfly e java jdk**
    
    ```sh
    chown citsmart:citsmart /opt/jdk1.8.0_172/ -R chown citsmart:citsmart /opt/wildfly-12.0.0.Final/ -R
    ```

2. Após a geração do certificado, conectar novamente no jboss-cli e executar os comandos abaixo:
    
    ```sh
    /subsystem=undertow/server=default-server/https-listener=https:read-attribute(name=security-realm)
    /subsystem=elytron/key-store=citsmartKeyStore:add(path="GRPv1.keystore",relative-to=jboss.server.config.dir,credential-reference={clear-text="123456"},type=JKS)
    /subsystem=elytron/key-manager=citsmartKeyManager:add(key-store=citsmartKeyStore,credential-reference={clear-text="123456"})
    /subsystem=elytron/server-ssl-context=citsmartSSLContext:add(key-manager=citsmartKeyManager,protocols=["TLSv1.2"])
    /core-service=management/security-realm=ApplicationRealm/server-identity=ssl:remove
    /core-service=management/security-realm=ApplicationRealm/server-identity=ssl:add(keystore-path="GRPv1.keystore", keystore-password-credential-reference={clear-text="123456"}, keystore-relative-to="jboss.server.config.dir",alias="GRPv1")
    ```
	
3. Antes de sair do jboss-cli executar o comando reload para aplicar as alterações.

    ```sh
    [standalone\@localhost:9990 /] :reload
    ```

## Iniciando as soluções seguindo dependências

1. Antes de sair do jboss-cli execute o comando reload para aplicar as alterações.

    **Servidor de Banco de Dados PostgreSQL**:

    ```sh
    systemctl postgresql start
    ```

    **Servidor de Banco de Dados MongoDB**

    ```sh
    /opt/mongodb-linux-x86_64-rhel70-3.4.15/bin/mongod --auth --port 27017
    ```

    **Servidor de Indexação Apache Solr**

    ```sh
    su solr /opt/solr/bin/solr start -s /bin/bash
    ```

    **Servidor de Aplicação Wildfly**

    ```sh
    su citsmart /opt/wildfly/bin/standalone.sh -s /bin/bash
    ```
    

## Deploy do CITSmart Enterprise


1. Enviar os arquivos de deploy fornecidos para o servidor e mover para o diretório “deployments”.

    ```sh
    cp CitsmartITSM-Enterprise.war /opt/wildfly/standalone/deployments/
    ```

2. Fazer o deploy do Citsmart Neuro após finalizar os passos da próxima sessão (Acesso ao CITSmart Enterprise).


### Acesso ao CITSmart Enterprise


1. Para acessar o CITSmart Enterprise, devemos acessar o IP ou endereço (registrado no DNS) seguido da porta e contexto.

    ```sh
    https://itsm.citsmart.com:8443/citsmart
    ```
	
2. O contexto "citsmart" é o padrão do CITSmart Enterprise.

    Primeiro acesso: Entre com a URL > https://itsm.citsmart.com:8443/citsmart.

3. Agora, siga os 3 passos de configuração e comece a usar a solução CITSmart.

## Deploy do CITSmart Neuro

1. Enviar os arquivos de deploy fornecidos para o servidor e mover para o diretório “deployments”.

    ```sh
    cp citsmart-neuro-web.war /opt/wildfly/standalone/deployments/
    ```


!!! tip "About"

    <b>Product/Version:</b> CITSmart Platform | 8.00 &nbsp;&nbsp;
    <b>Updated:</b>01/17/2019 – Anna Martins
