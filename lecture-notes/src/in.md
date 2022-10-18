# Introducción

## Información del curso

Se trata de un curso de introducción al mundo y herramientas Cloud/Devops.

[Link al curso](https://www.youtube.com/watch?v=Wvf0mBNGjXY)

# Comandos básicos de linux

## Desplegar un entorno linux

Necesitamos un entorno linux para practicar con los comando linux, por lo que necesitamos aprender como desplegar un SO Linux en nuestro ordenador.

## Tipos de Shell

Algunos tipos de shell son:

- Bourne Shell `Sh Shell`
- C Shell `csh` or `tcsh`
- Z Shell `zsh`)
- Bourne again Shell `bash`

Se puede utilizar el comando

```bash
$ echo $SHELL
/bin/bash
```

para saber que la shell que se está utilizando.

## Comandos básicos de navegación

Repaso de algunos comandos básicos:

```bash
$ echo Hello
Hello
$ ls
File.txt my_dir1 file2.conf
$ cd my_dir1
$ pwd
/home/my_dir1
$ mkdir new_directory
$ cd new_directory; mkdir www; pwd
/home/my_dir1/new_directory
```

## Comandos básicos de directorios

Creación de un directorios anidados:

```bash
$ mkdir /tmp/asia
$ mkdir /tmp/asia/india
$ mkdir /tmp/asia/india/bangalore
```

o alternativamente

```bash
$ mkdir -p /tmp/asia/india/bangalore
```

Para borrar un directorio y su contenido:

```bash
$ rm -r /tmp/my_dir1
```

Para copiar un directorio y su contenido a otra localización:

```bash
$ cp -r my_dir1 /tmp/my_dir1
```

## Comandos básicos de archivos

Para crear un nuevo archivo sin contenido

```bash
$ touch new_file.txt
```

Para añadir contenido, una vez que se escribe el texto deseado, se sale y se guarda con `Ctrl + D`

```bash
$ cat > new_file.txt
[CTRL + D]
```

¡Cuidado! Si se vuelve a utilizar la orden anterior, se borra el contenido anterior del archivo.

Para ver el contenido del archivo

```bash
$ cat new_file.txt
```

Para copiar un archivo

```bash
$ mkdir folder
$ cp new_file.txt ./folder/copy_file.txt
```

Para mover (renombrar) un archivo

```bash
$ mv new_file.txt sample_file.txt
$ mv sample_file.txt ./folder/sample_file.txt
$ mv ./folder/sample_file.txt new_file.txt
```

Para borrar un archivo

```bash
rm new_file.txt
```

## Laboratorio para practicar

[https://kodekloud.com/topic/labs-working-your-way-through-the-cli-2/](https://kodekloud.com/topic/labs-working-your-way-through-the-cli-2/)

## Comandos de usuario

```bash
$ whoami
pepe
$ id
uid=xxxx (pepe) gid=xxxx groups=xxxx
$ su carlos
Password:
$ ssh carlos@192.168.1.2
```

Como buena prática, nos logueamos en el sistema con nuestro usuario regular `pepe` y no con el usuario `root`. Si necesitamos elevar privilegios para ejecutar alguna orden, utilizaremos el prefijo `sudo` delante del comando a ejecutar, por ejemplo

```bash
$ sudo ls /root
```

## Comandos de descarga de archivos

Para descargar un archivo se utiliza

```bash
$  curl -O http://ipv4.download.thinkbroadband.com/10MB.zip
10MB.zip
$  curl -o  demofile.zip http://ipv4.download.thinkbroadband.com/10MB.zip
demofile.zip
```

Flags:

- `-O` descargar y guardar el archivo en el directorio actual
- `-o  demofile.zip` descargar y guardar el archivo en el directorio actual con el nombre especificado

También se pude utilizar

```bash
$  wget -O demofile.zip http://ipv4.download.thinkbroadband.com/10MB.zip
demofile.zip
```

## Comandos de SO

Comprobar la versión del sistemas operativo

```bash
$ ls /etc/*release*
$ cat /etc/*release*
```

# Gestores de paquetes en Linux

Nos vamos a centrar en el SO Centos.

**RPM (Red Hat Package Manager)**

Instalar/Desinstalar/Query-de un paquete

```bash
$ rpm -i telnet.rpm´
$ rpm -e telnet.rpm´
$ rpm -q telnet.rpm´
```

Para resolver el infierno de las dependencias se utilizan gestores de paquetes de más alto nivel como yum.

**YUM (Red Hat Package Manager)**

Gestor de paquetes que utiliza RPM por debajo.

Instalar un paquete y todas sus dependencias

```bash
$ yum install ansible
```

Algunas notas sobre el proceso de búsqueda de paquetes:

- `yum` busca los paquetes en un archivo local llamado `/etc/yum.repos.d`
- En ocasiones, esta lista no contiene un determinado paquete o una versión deseada del mismo.

Para ver la lista de paquetes de Centos disponible en nuestro sistema se ordena

```bash
$ yum repolist
```

El siguiente comando muestra los archivos en los que se indica el repositorio donde se busca cada paquete. Se puede ver la url del repositorio:

```bash
$ ls /etc/yum.repos.d
CentOS-Base.repo   CentOS-Media.repo   mysql-comunity.repo 
$ cat /etc/yum.repos.d/CentOS-Base.repo
name=xxx
baseurl=xxx
```

Al navegar a esa url, podríamos darnos cuenta de que el repo no contiene la última versión de Ansible (contiene por ejemplo la 2.4 y la última es 2.9) 

Si navegamos a la página de Ansible, podemos obtener información de como obtener esta última versión. En ocasiones habrá que ejecutar un comando como el siguiente

```bash
yum install https://some-web/some-file.rpm
```

El comando anterior añade un nuevo repositorio al sistema que apunta a la versión de Ansible deseada.

Para listar la ultima versión de ansible instalada o disponible en el sistema, se ordena

```bash
$ yum list ansible
Installed Packages
ansible.noarch   2.9.6-1.el7     epel
```

Para eliminar un paquete

```bash
yum remove ansible
```

Para listar las versiones disponibles de Ansible, incluyendo duplicado, se ordena

```bash
$ yum --showduplicates list ansible
Available Packages
ansible.noarch   2.4.2.0-2.el7   extras
ansible.noarch   2.9.6-1.el7     epel
```

Se observa que un paquete procede del repositorio extras y otro paquete procede del repositorio epel.

Para instalar una versión específica de Ansible utilizaríamos el siguiente comando

```bash
yum install ansible-2.4.2.0
```

# Configuración de servicios en Linux

## Introducción a lo servicios en linux

Una vez que se instala software en un servidor, especialmente los que se ejecutan en el background, como los servidores web o los servidores de base de datos, hay que asegurarse que estos servidores o servicios están ejecutándose y que lo siguen haciendo incluso tras reiniciar los servidores.

Los servicios de linux nos ayudan a configurar el software para que se ejecuta en el background.

Cuando un software que se ejecuta como servicio en el background es instalado (web server, database server, docker), automaticamente se configura como servicio en el sistema. 

Veamos que herramientas existen para el manejo de los servicios del sistema.

## Manejo de los servicios de linux

Para iniciar un servicio en linux, por ejemplo httpd, se puede utilizar cualquiera el comando

```bash
service httpd start
```

o el comando

```bash
systemctl start httpd
```

Ambos cubren el mismo propóstito. El comando `service` utiliza la utilidad `systemctl` por debajo. Nos centraremos en esta última herramienta.

Para parar un servicio se utiliza

```bash
systemctl stop httpd
```

Para comprobar el estado del servicio se utiliza

```bash
systemctl status httpd
```



