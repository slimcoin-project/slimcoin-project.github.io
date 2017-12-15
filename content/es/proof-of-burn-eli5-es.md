---
title: ¿Qué es el Proof of Burn (ELI5)?
lang: es
menuitem: Proof of Burn ELI5
category: technology
ref: eli5
layout: page
permalink: /proof-of-burn-eli5-es/
priority: 4
---

En este artículo te explicamos el mecanismo de consenso revolucionario usado en Slimcoin: **Proof of burn**.

*Para una explicación súper-corta puedes ir al **[resumen](#resumen)** al final del artículo. Los lectores que ya conocen el mecanismo de las pruebas de trabajo de Bitcoin y saben **por qué** funciona pueden saltar las primeras dos secciones.*

### ¿Para qué necesitamos un "mecanismo de consenso"?

Para comprender bien el Proof of Burn, primero tenemos que saber por qué las criptomonedas necesitan un mecanismo de consenso.

Primero, lo básico: La **cadena de bloques** o **blockchain** es la base de datos de toda criptomoneda. Contiene todas las transacciones válidas. Todos los nodos - los participantes que corren un software de cliente - graban la cadena de bloques en sus discos. Es llamada "cadena de bloques" porque las transacciones se agrupan en **bloques**. Un bloque es concebido cuando los nodos se ponen de acuerdo que un grupo de transacciones es "válido".

Ahora, **¿cómo hacen los nodos para ponerse de acuerdo** cuales son las transacciones válidas? No hay una autoridad central que valida las transacciones, por eso éste trabajo debe ser realizado por los nodos en conjunto.

La arquitectura de la cadena de bloques ya evita que algún nodo pueda crear dinero a partir de la nada. Lo que sí podrían probar los nodos es tratar de usar o transferir una cantidad de dinero dos veces - esto es llamado **gasto doble** (en inglés, *double spend*). Por ejemplo, podrían comprar un producto en una tienda en línea e inmediatamente después intentar de enviar el mismo dinero a una bolsa y cambiarlo por una moneda fiat como el euro o el dólar. Sí el truco funciona, podrían engañar al dueño de la tienda y a la bolsa y apropiarse de las dos cosas - el producto comprado y el dinero fiat.

Para evitar los gastos dobles, los nodos tienen que **ponerse de acuerdo** cuales son las transacciones válidas, y cuales no.

Podríamos pensar que sea posible que los nodos **voten** cuales son las transacciones que se incluirán en el próximo bloque, cada nodo contando con un voto. Pero hay un problema: **Un participante con intenciones maliciosas podría crear miles de nodos** y manipular el voto.

### Pruebas de trabajo: El mecanismo de consenso de Bitcoin

Por eso, necesitamos otro mecanismo - uno que no se pueda manipular fácilmente. En 2009, el Bitcoin revolucionó el mundo del dinero electrónico con un mecanismo llamado **Prueba de trabajo**.

Podríamos describir el proceso de la siguiente manera: Los nodos (*mineros*) compiten para escribir un bloque y añadirlo a la cadena de bloques. Para esto, los nodos primero deben probar que realizaron un *trabajo*: tienen que resolver una especie de **rompecabezas criptográfico**. El nodo que primero lo resuelve se gana el derecho de escribir el bloque. Este proceso coloquialmente es llamado **minería**.

Si un atacante quiere ejecutar un **gasto doble**, debe contar con la potencia de cómputo para **escribir varios bloques** uno atrás de otro. Sólo de esta manera, puede asegurar que las dos transacciones del gasto doble se incluyan en la cadena. (En realidad, lo que hace es bifurcar la cadena un bloque antes de la primera de las dos transacciones y luego de que la tienda haya aceptado el pago, "colarse" con una cadena alternativa que contenga la segunda transacción - en nuestro ejemplo, la que va a una bolsa.)

Para este ataque se necesita **mucha potencia** - solamente si el atacante cuenta con más de la mitad de la potencia de toda la red (esto es el llamado **ataque del 51 por ciento**). El mecanismo de las pruebas de trabajo, de esta manera, previene los gastos dobles porque es extremamente **caro** comprar la potencia de minería necesaria para este ataque.

### Proof of Burn: Prueba de trabajo sin trabajo

Lo importante que hay que entender es que la potencia computacional en si misma no es importante para prevenir un ataque. Lo importante es **el costo** de la potencia (electricidad, equipos, etc). **Debe ser costoso** para un atacante de adquirir la potencia para *minar* varios bloques en cadena.

De esta manera, el derecho de minar bloques en el mecanismo Proof of Work está relacionado con un costo para el minero. **Cuánto más paga** para los equipos (*mineros*) y la electricidad que son necesarios para resolver los rompecabezas criptográficos, **más chances tiene** de añadir bloques a la cadena.

Ahora ¿este efecto, no se puede conseguir de una manera más "directa", sin necesitar el complejo proceso de minería?

Podemos imitar el costo de los mineros si los nodos simplemente tienen que "destruir" o "quemar" dinero, si quieren ganarse el derecho de minar bloques. **Este es el principio básico detrás del Proof of Burn**.

Esto quizá suene loco: Destruimos dinero para luego ganárnoslo a través de las recompensas de los bloques. Pero el brillante inventor del Proof of Burn, Iain Stewart, nos ha provisto de una analogía interesante: **¡Las monedas quemadas son equipos de minería!** ([Fuente](https://en.bitcoin.it/wiki/Proof_of_burn#Technical_sketch_of_proof_of_burn:_.22Burnt_coins_are_mining_rigs.21.22)).

Esto quiere decir: El acto de *quemar monedas* se puede comparar con el acto de *comprar un equipo de minería*. Es decir: Siempre cuando quemamos monedas, **compramos un equipo de minería virtual** que nos da el poder de escribir bloques. Cuanto más monedas quememos, más potencia tendrá nuestro equipo virtual.

En el Proof of Burn, hablamos de **acuñar** (*mint*), no de **minar**, porque no se requiere (mucho) trabajo computacional. Hay que acordarse siempre que lo importante es el costo requerido para engañar al sistema.

El mecanismo de Proof of Burn de Slimcoin sigue casi exactamente la analogía de la minería virtual:

Si quemamos monedas, **no solamente** ganamos el derecho de competir para el próximo bloque. Un equipo de minería es algo más duradero, y **esto mismo pasa con los mineros virtuales** de Slimcoin. Cada vez que quemamos monedas, tendremos la posibilidad de participar de la minería por un largo tiempo - **al menos por un año**.

Para prevenir que **los primeros usuarios de Slimcoin se beneficien demasiado** del mecanismo o lo puedan atacar, la **potencia** de las monedas quemadas **decrece** cada vez un bloque es añadido a la cadena. Decrece **muy de a poco**, así que no tienes preocuparte si no ganas bloques directamente después de quemar monedas - tienes mucho tiempo.

Esto también se puede comparar con la minería Proof of Work: Los equipos de minería en algún momento **se vuelven obsoletos** cuando emergen nuevas tecnologías más eficientes. Para seguir siendo competitivos, los mineros deben renovar sus equipos cada vez en cuando. Lo mismo pasa con el Proof of Burn: **Si quieres mantener tu poder para acuñar dinero, de vez en cuando tienes que quemar más monedas**. 

Como en Proof of Work, las **recompensas por los bloques** son suficientes para que los participantes del sistema puedan adquirir ganancias. No es que te ganarás todo el dinero que quemaste en una hora o en un día, pero en la mayoría de las situaciones después de semanas o meses **ganarás bastante más monedas que las que quemaste**.

El Proof of Burn, comparado con el Proof of Work, tiene la gran ventaja de que **consume mucho menos energía**. Slimcoin es la moneda para ti si estás preocupado por el daño ambiental que pueda producir la minería de Bitcoin. Pero Proof of Burn también tiene algunas ventajas respecto al Proof of Stake (prueba de participación).

### Resumen

**El Proof of Burn funciona como un proceso de "minería virtual": Cuando quemas monedas compras un equipo de minería virtual. Cuánto más dinero quemas, más potente es tu equipo. Cada equipo virtual de da el derecho de minar por un largo período, como los mineros de verdad. Pero gradualmente pierden competitividad - tal como los equipos de minería que quedan obsoletas por el avance tecnológico.**

