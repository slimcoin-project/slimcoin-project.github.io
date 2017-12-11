---
title: Bajar e instalar Slimcoin
lang: es
menuitem: Instalar Slimcoin
ref: installation
category: help
layout: page
permalink: /instalar/
priority: 1
---

Hay varios métodos para instalar Slimcoin. El programa corre con Windows, Linux and Mac OS X.

## Bajar el cliente
### Ejecutables (Windows y Mac OS)

Puedes bajar los ejecutables de Slimcoin en la página [Releases](https://github.com/slimcoin-project/Slimcoin/releases) de nuestro proyecto en Github.

Descomprime al archivo y pónlo en cualquier carpeta a la que tienes acceso. Sigue con la sección *Configuración básica* más abajo.

### Código fuente (releases)

Bajá el código fuente en la [página Releases de Github](https://github.com/slimcoin-project/Slimcoin/releases).

Descomprime el archivo y pónlo en una carpeta (te recomendamos llamarla *Slimcoin*), abrí un terminal y cambiá a ésta carpeta.

#### Compilar

El proceso de compilado es simple si tienes todas las dependencias instaladas. En el archivo README encontrarás las dependencias que necesitas. Tienes que instalar también los paquetes de desarrollo (-dev o -devel en sistemas Linux).

Para compilar al cliente gráfico, tipeá:

```qmake
make
```

Si solamente quieres compilar el *daemon* (programa para la líea de comandos): En la subcarpeta *src* encontrarás *makefiles* preparados para tu sistema operativo (por ejemplo, *makefile.unix*). Fíjate cual es el que necesitas y después tipeá:

```cd src
make -f TU_MAKEFILE```

Después de una compilación exitosa, el programa ejecutable (*slimcoin-qt*) del cliente gráfico se encontrará en la carpeta básica, mientras que el daemon *slimcoind* "vivirá" en la subcarpeta *src*. Puedes mover a ambos programas a dónde quieras (por ejemplo, a una carpeta *bin* dónde tengas acceso directo a ella).

### Código fuente (git, experimental)

Para este método necesitarás el programa *git*, un sistema de control de versiones.

Cloná el repositorio de Slimcoin (ésto creará una subcarpeta, "Slimcoin") y cambiá a la subcarpeta:

```git clone https://github.com/slimcoin-project/Slimcoin.git
cd Slimcoin```

Por defecto encontrarás al code en la rama *slimcoin*, que se supone que es estable pero no es el código más reciente. Si quieres probar la versión más nueva y experimental cambiá a la rama *master*:

```git checkout master```

Ahora, compilá a Slimcoin tal como se indicó arriba.

## Configuración básica

Para configurar Slimcoin y usar opciones avanzadas, necesitás saber que Slimcoin graba todos los datos (la cadena de bloques, el archivo con la cartera, los logs y el archivo de configuración) en una carpeta llamada la **datadir**.

Por defecto, ésta se encuentra en (reemplazá USUARIO por tu propio nombre de usuario):

* **Windows:** `C:\Users\USUARIO\Appdata\Roaming\Slimcoin` (Windows Vista/7 y superior)
* **Linux/Unix:** `/home/USUARIO/.slimcoin` o simplemente `~/.slimcoin`
* **Mac OS:** `~/Library/Application Support/Slimcoin/`

**Note:** En Windows, para acceder rápidamente a esta carpeta puedes ir a *Ejecutar* e ingresar: `%APPDATA%/Slimcoin`

Es recomentable crear un archivo de configuración **slimcoin.conf** en esta carpeta, sobre todo si tu intención es usar opciones avanzadas de Slimcoin. En este archivo puedes ingresar la gran mayoría de las opciones de la línea de comandos disponibles para Slimcoin. Puedes crear el archivo en tu editor de texto favorito.

Sí quieres usar el daemon *slimcoind* son obligatorias las dos siguientes líneas (cambiá USUARIO y CONTRASEÑA según tus preferencias):

```
rpcuser=USUARIO
rpcpassword=CONTRASEÑA
```

'''Nota:''' ¡Esto no es la contraseña de acceso a la cartera! Es mejor usar contraseñas sin caracteres especiales como la ñ o letras con tildes o acentos. Sino, son posibles errores inesperados en algunos programas que usan Slimcoin. Puedes cambiar la constraseña en cualquier momento sin que esto perjudique tu acceso a tu cartera.

Para que el daemon corra en el fondo ingresá lo siguiente:

```
daemon=1
```

## Ejecutar Slimcoin

Ahora estamos listos para correr Slimcoin.

* Para el cliente gráfico simplemente abre la carpeta dónde instalaste el archivo ejecutable y hacé doble clic en **slimcoin-qt**, o abrilo en una consola.
* Para el daemon, tipeá **slimcoind** en la carpeta dónde se encuentra (acordate que si no la cambiaste después de compilar, está en la subcarpeta *src*).

Para las opciones en la línea de comandos simplemente ingresá **slimcoind --help** o **slimcoin-qt --help**. Las opciones son similares a las que ofrece Bitcoin. Una referencia se encuentra en la [Wiki de Bitcoin](https://es.bitcoin.it/wiki/Ejecuci%C3%B3n_de_Bitcoin). No todos los comandos de Bitcoin se encuentran disponibles para Slimcoin, pero los que sí existen funcionarán muy probablemente de la misma manera.
