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

## Comandos básicos para directorios

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

## Comandos básicos para archivos

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