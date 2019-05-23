# Script
Los scripts deben controlar todos los posibles errores, si el número de parámetros no es el correcto, se mostrará al usuario cuáles son las posibles opciones para su ejecución.

Escriba un script que elimine un archivo o directorio pasado como parámetro, y le pregunte si está seguro de llevar a cabo la acción.
``` 
 #/!bin/bash
 if [ -e $1 ]
 then
 	if [ -d $1 ]
	then
  		read -p "Seguro que desea eliminarlo(S/N) " opcion
    	if [ $opcion = "S" -o $opcion = "s" ]
    	then
      		rm -r $1
      		exit 0
    	fi
     	exit 1
  	else 
		read -p "Seguro que desea eliminarlo(S/N) " opcion
		if [ $opcion = "S" -o $opcion = "s" ]
    	then
      		rm -r $1
      		exit 0
    	fi
		exit 1
	fi
else
	echo "No existe el fichero/directorio introducido."
fi
exit -1
```
Escribir un script que pueda mostrar información de un comando al ejecutar dicho script y pasar como parámetro el comando.
``` 
 #/!bin/bash
 $1 --help
```
Realiza un script que compruebe si el usuario actual del sistema es blas, si es así visualiza su nombre 5 veces, sino te despides de él amigablemente.

``` 
#/!bin/bash
usuario='manufercar'
if [ $usuario = 'blas' ]
	then
		echo 'blas'
		echo 'blas'
		echo 'blas'
		echo 'blas'
		echo 'blas'
else
	echo 'Hasta pronto '$usuario
fi
```

En un fichero tengo una palabra clave. Haz un script que muestre si dicha palabra es el parámetro pasado o no.

```
#/!bin/bash
clave= `cat ./candado.txt`
if [ $palabra = 'llave' ]; then
	echo "Has acertado"
else
	echo "Palabra incorrecta"
fi
```
Tenemos un menu principal:

(1) Suma

Lee dos números y los suma.
(2) Resta

Lee dos números y los resta.
(3) Multiplicación

Lee dos números y los multiplica.
(4) Salir

Termina el script. 
```
#/!bin/bash
clear
while [ true ]
do
	read -p "Introduce (1 para suma) (2 para resta) (3 para multiplicacion) (4 para salir) " opcion
	case $opcion in
		1)
			read -p "Primer numero " n1
			read -p "Segundo numero " n2
			resultado=$(expr $n1 + $n2)
			echo $n1 " + " $n2" = "$resultado
			;;
		2)
			read -p "Primer numero " n1
			read -p "Segundo numero " n2
			resultado=$(expr $n1 - $n2)
			echo $n1 " - " $n2" = "$resultado
			;;
		3)
			read -p "Primer numero " n1
			read -p "Segundo numero " n2
			resultado=$(expr $n1 \* $n2)
			echo $n1 " * " $n2" = "$resultado
			;;
		*)
			exit 0
		;;
	esac
done
```
Nos pide la edad y nos dice si es mayor de edad o menor.
```
#/!bin/bash
echo "Ponga su edad: "
read edad
if test $edad -lt 18
then
	echo "Eres menor de edad"
	else
		if test $edad -gt 18
		then
			echo "Si, eres mayor de edad"
			else
			echo "Si, eres mayor de edad"
		fi
fi
```
Script que reciba un nombre de fichero, verifique que existe y que es un fichero de lectura-escritura, lo convierta en ejecutable para el usuario y el grupo y muestre el estado final de los permisos.
```
#/!bin/bash
if [ -f $1 ]
then
	if [ -r $1 ]
	then
		echo "Tienes permisos para leer"
		if [ -w $1 ]
		then
			echo "Tienes permisos para editar"
			chmod ug+x $1
			ls -l $1
		else
			echo "El fichero no tiene permisos para ser leido ni editado"
		fi
	else
		echo "El fichero no tiene permisos para ser leido ni editado"
	fi
else
	echo "No existe el fichero"
fi
```
Script que nos diga al pulsar una tecla, si es letra, numero o caracter especial.

``` 
#/!bin/bash
read -p "Introduce un caracter " caracter
case $caracter in
	[a-z,A-Z])
		echo "Ha introducido un caracter de tipo letra"
		;;
	[0-9])
		echo "Ha introducido un caracter de tipo numero"
		;;
	*)
		echo "Ha introducido un caracter especial"
		;;
esac
```

Realizar un script que reciba varios parametros y nos diga cuantos de esos parametros son de directorios y cuantos son archivos. $# contador que indica cuantos parametros se pasan.

```
#/!bin/bash
cont1=0
cont2=0
for indice in $@
do
	if [ -d $indice ]
	then
		cont1=`expr $cont1 + 1`
	else [ -f $indice ]
	then
		cont2=`expr $cont2 + 1`
	fi
done
echo "Directorios: " $cont1
echo "Ficheros: " $cont2
```

Mostramos menu, con productos para vender, luego nos pide que introduzcamos la opcion. luego mensaje que indica que introduzca moneda. Si ponemos precio exacto nos da mensaje, "Gracias buen provecho", si ponemos menos, nos diga falta. Si poner mas valor, nos indique el cambio con mensaje.

![](https://github.com/mafercar/Script/blob/master/scriptmenu.png)

Realizar un script que pida introducir la ruta de un directorio por teclado (Hay que validar que la variable introducida sea un directorio) nos diga cuantos archivos y cuantos directorios hay dentro de ese directorio.

```
#/!bin/bash
read -p "Introduzca la ruta del directorio: " dir
until [-d $dir ]; do
read -p "Introduzca la ruta del directorio: " dir
done
cont=0
cont2=0
	for var in `ls $dir`; do
		if[ -d $var ]; then
		cont=`expr $cont + 1`
		else [-f $var ]; then
		cont2= `expr$cont2+1
		fi
	done
echo "Introdujiste "$cont" directorios y "$cont2" ficheros"
echo "Se introjueron "$#" parametros"
	
```

Realiza un script que introduzca número por parámetro y muestre tabla de multiplicar.

``` 
#/!bin/bash
clear
echo "La tabla de multiplicar de "$1" es: "
for (( i=0;i<11;i++))
	do
		resultado=$(expr $1 \* $i)
		echo $1 " * " $i " = "$resultado
	done
```

Script que limpie todas las reglas, y de permiso a todas las conexiones.

``` #/!bin/bash
`iptables -F`
`iptables -A INPUT -j ACCEPT`
`iptables -A OUTPUT -j ACCEPT`
`iptables -A FROMWARD -j ACCEPT`
```
Script que limpie todas las reglas, y prohíba cualquier conexión.

``` #/!bin/bash
`iptables -F`
`iptables -A INPUT -j REJECT`
`iptables -A OUTPUT -j REJECT`
`iptables -A FROMWARD -j REJECT`
```
Tendrá 3 parámetros: red(ip), entrada-salida, aceptar-denegar. Dará estos permisos a iptables.
![](https://github.com/mafercar/Script/blob/master/scriptpermisos.png)
