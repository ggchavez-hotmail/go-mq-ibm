# Uso de MQ Mensaje basico

## Instalar Cliente MQ

Descargar conector e instalar.

```
mkdir mq-cliente
cd mq-cliente
wget https://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/messaging/mqdev/redist/9.3.2.0-IBM-MQC-Redist-LinuxX64.tar.gz
tar -xvf 9.3.1.0-IBM-MQC-Redist-LinuxX64.tar.gz
rm -f 9.3.1.0-IBM-MQC-Redist-LinuxX64.tar.gz
cd ..
sudo mv mq-cliente/ /opt/mqm
```

## Configurar variables de ambientes

Agregar al `/etc/profile` o en `~/.bashrc` o solo ejecutar los siguientes `export`.

```
#Configuracion SDK IBM MQ
export MQ_INSTALLATION_PATH=/opt/mqm
export CGO_CFLAGS="-I$MQ_INSTALLATION_PATH/inc"
export CGO_LDFLAGS="-L$MQ_INSTALLATION_PATH/lib64 -Wl,-rpath,$MQ_INSTALLATION_PATH/lib64"
```

Nota: dependiendo del linux elegido puede ser necesario instalar el compilador C, para eso ejecutar.

```
sudo apt install gcc
```

### Documentacion oficial : https://developer.ibm.com/articles/mq-downloads/

## Levantar Servidor IBM MQ en Docker

Se debe contar con Docker instalado y ejecutar siguiente comando

```
docker run --env LICENSE=accept --env MQ_QMGR_NAME=QM1 --volume /home/<<users>>/dockermq/:/mnt/mqm --publish 1414:1414 --publish 9443:9443 --detach --env MQ_APP_PASSWORD=passw0d icr.io/ibm-messaging/mq:9.3.0.0-r2
```

### Documentacion oficial : https://hub.docker.com/r/ibmcom/mq/

## Ingresar al servidor web local IBM MQ

Ingresar: `https://localhost:9443/ibmmq/console/`
Usuario: `admin`
Password: `passw0rd`

## Instalar golang

```
wget https://go.dev/dl/go1.17.10.linux-amd64.tar.gz
sudo tar -xvf go1.17.10.linux-amd64.tar.gz
sudo mv go /usr/local
```

## Configurar variables ambiente para Golang

Agregar al `/etc/profile` o en `~/.bashrc` o solo ejecutar los siguientes `export`.

```
#Configuracion Golang
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

Adicionalmente preparar espacio de trabajo golang

```
mkdir go
cd go
mkdir src
mkdir pkg
mkdir bin
```

## Configuración para utilizar el repo

Ir al espacio de trabajo golang

```
cd ~/go/src
```

Descargar repositorio

```
git clone <<repo>>
```

Entrar al repo y ejecutar comando para recuperar las librerias go utilizadas.

```
go mod tidy
```

## Funcionalidades

Se puede utilizar la shell `putget.sh` para ejecutar ambas funcionalidades o se puede ejecutar por separado `amqsget.go` | `amqsput.go`

Ejecución shell

```
sh putget.sh "mensaje de prueba"
```
