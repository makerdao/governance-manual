# Acceso Instantáneo al Techo de Deuda

>**Alias:** DC-IAM  
>**Nombre del Contrato:** `DssAutoLine`  
>**Alcance:** Un solo contrato DssAutoLine puede contener un conjunto de parámetros para cada tipo de vault.

## Descripción

El Módulo de Acceso Instantáneo al Techo de Deuda permite a cualquier usuario ajustar el Techo de Deuda de un tipo de _vault_ respaldado de acuerdo a las reglas definidas en la lógica del _smart contract_ (contrato inteligente) de DC-IAM y los parámetros fijados por la Gobernanza de Maker.  

Las reglas definidas en el _smart contract_ de DC-IAM fomentan una cantidad de 'espacio libre' entre el uso actual de la deuda y el Techo de Deuda de un tipo de _vault_. El DC-IAM contiene tres parámetros que pueden ser fijados por la gobernanza para cada tipo de _vault_ \(como ETH-A.\) Estos parámetros son `line`, `gap`, y `ttl`. El efecto de estos parámetros es descrito en detalle en la sección de Parámetros Clave.

Por ejemplo, si actualmente el Techo de Deuda del ETH-A es de 100 DAI y se extraen 90 DAI como deuda, el DC-IAM podría ser utilizado para incrementar el Techo de Deuda del ETH-A a 110 DAI, imponiendo una diferencia de 20 DAI entre el uso y el techo. Si el Techo de Deuda del ETH-A cae a 50 DAI, un usuario podría activar el DC-IAM y reducir el techo de deuda a 70 DAI, manteniendo una diferencia de 20 DAI entre el uso y el techo.

## Propósito
El modulo fue diseñado con dos propósitos en mente:

1.	Para minimizar la cantidad de gastos de gobernanza provenientes de actualizar techos de deuda para un tipo de _vault_.

2.	Para reducir riesgos en caso de que ocurra una caída significativa en los precios del colateral en menos tiempo del que a un oráculo le tomaría actualizar los precios.

## Contrapartida

El DC-IAM provee una variedad de beneficios y solo una desventaja conocida. Los principales beneficios son reducir los gastos de gobernanza, configurando los techos de deuda y mitigando los riesgos en caso de una gran caída en el precio de un colateral. Estos beneficios son significativos.

La única desventaja es que el DC-IAM permite un ataque _griefing_ en el Techo de Deuda de los tipos de colateral que lo están usando. El resultado de este ataque es el de prevenir que DAI sea acuñado usando un tipo de colateral especifico. Se ha determinado que la probabilidad y severidad de este ataque son mínimas y la estrategia de mitigación es sencilla, consiste en desactivar el DC-IAM para el tipo de colateral atacado.     

## Parámetros Clave

A continuación, se analizarán tres parámetros clave para el DC-IAM. Cada uno de estos parámetros puede ser fijado para un tipo de _vault_.

### Techo de Deuda Máximo \(`line`\)
El Techo de Deuda Máximo se refiere al máximo valor para el Techo de Deuda que el DC-IAM permitirá dado un tipo de _vault_ especifico. Este parámetro también es llamado `line` dentro del contrato inteligente. Cuando se usa el DC-IAM para manejar el Techo de Deuda de un tipo de _vault_, este parámetro esencialmente remplaza al Techo de Deuda de ese tipo de _vault_. En lugar de que la Gobernanza fije el Techo de Deuda directamente, se necesita fijar el Techo de Deuda Máximo en el DC-IAM.

### Objetivo Disponible de Deuda \(`gap`\)
El parámetro Objetivo Disponible de Deuda controla de cuánto es la diferencia que el DC-IAM pretende mantener entre el uso actual de la deuda y el Techo de Deuda de un tipo de _vault_.

Cuanto más alto sea este valor, hay mayor riesgo de que ocurran grandes caídas de colaterales en un periodo muy corto de tiempo.  

Cuanto más bajo sea este valor, más afecta negativamente al uso de la _vault_. Un Objetivo Disponible de Deuda relativamente bajo, por ejemplo de 100,000 DAI, seria malo para cualquiera que quisiera acuñar más de 100,000 DAI de una sola vez \(y para otros usuarios también\). La razón de esto se vincula con el parámetro de Enfriamiento de Aumento de Techo de Deuda.

### Enfriamiento de Aumento del Techo \(`ttl`\)

El parámetro de Enfriamiento de Aumento de Techo controla que tan frecuentemente el Techo de Deuda puede _incrementado_ por el DC-IAM. Si un usuario intenta usar el DC-IAM para incrementar el Techo de Deuda de un tipo de _vault_ antes de que este expire, la transacción fallará en ejecutarse y el Techo de Deuda se mantendrá sin cambios.

Por el otro lado, la _disminución_ del Techo de Deuda siempre es posible, independientemente del Enfriamiento de Aumento de Techo.

En conjunto, el Objetivo Disponible de Deuda y el Enfriamiento de Aumento de Techo aplican una tasa máxima que el uso de la deuda puede incrementar a través del tiempo usando un tipo de _vault_ específica. Estos parámetros deben establecerse de forma que el máximo aumento en el tiempo pueda acomodar todo uso razonable del tipo de _vault_ en cuestión.

## Interacción con el Usuario

El _smart contract_ DC-IAM contiene un solo método de activar una potencial actualización del Techo de Deuda para un cierto tipo de _vault_. Este método se llama `exec`.

Cuando se utiliza `exec`, la lógica siguiente es ejecutada por el _smart contract_:

1. ¿La diferencia entre el uso de deuda actual y el Techo de Deuda es más grande que el Objetivo Disponible de Deuda?

    a\) Si la respuesta es afirmativa, pase al punto 3.


    b\) Si la respuesta es negativa, no haga nada.

2. ¿La diferencia entre el uso de deuda actual y el Techo de Deuda es menor que el Objetivo Disponible de Deuda y el Enfriamiento del Techo de Deuda ha expirado?

    a\) Si la respuesta es afirmativa, pase al punto 3.  

    b\) Si la respuesta es negativa, no haga nada.

3. Fijar el Techo de Deuda igual al uso de deuda actual + Objetivo Disponible de Deuda, en el valor de Máximo Techo de Deuda.


En la práctica, el método `exec` siempre fijará el Techo de Deuda igual al uso de deuda actual + Objetivo Disponible de Deuda. Si esta operación _aumentara_ el Techo de Deuda, posteriormente solo se ejecutará si el Enfriamiento del Techo de Deuda ha expirado.

## Tutorial

Para cualquier tipo de _vault_, estos son los pasos que se deben tomar para modificar su Techo de Deuda a través del DC-IAM:

### 1. Determinar el Código Hexadecimal para el Tipo de _Vault_

1. Convertir el nombre de la _vault_ a Hexadecimal
2. Poner el prefijo `0x`
3. Agregar ceros como sufijo, para que la cadena tenga una longitud total de 66 caracteres.  

   > Ejemplo:
   >
   > 1. ETH-A se convierte en `4554482d41`
   > 2. `4554482d41` se convierte en `0x4554482d41`
   > 3. `0x4554482d41` se convierte en `0x4554482d41000000000000000000000000000000000000000000000000000000`

### 2. Introduce el Código en el Contrato DC-IAM y Escribe
Ejecuta el método `exec` del contrato con el código hexadecimal para los tipos de _vaults_ en función al argumento. Esto se puede hacer [aquí](https://etherscan.io/address/0xc7bdd1f2b16447dcf3de045c4a039a60ec2f0ba3#writeContract).

![DC-IAM exec](https://i.imgur.com/pglxvKG.png)

Ejecutar este método modificará efectivamente el Techo de Deuda para el tipo de _vault_ en cuestión, a menos que se espere un aumento que esté en orden y que el Enfriamiento del Crecimiento de Techo de Deuda no haya sido aprobado aún.

>Para revisar la última vez que el DC-IAM fue ejecutado en una _vault_ determinada, dirígete los [Eventos del Contrato](https://etherscan.io/address/0xc7bdd1f2b16447dcf3de045c4a039a60ec2f0ba3#events) y busca el código hexadecimal de la _vault_ correspondiente \(al lado de `[topic1]`\), así como la fecha de ejecución. Actualmente `tty` está fijado en 12 horas.
>
> ![Ultima Ejecución](https://i.imgur.com/FEd7gBX.png)

## Consideraciones

* Las _Reducciones_ del Techo de Deuda no pueden tomar lugar en el mismo bloque que los aumentos del Techo de Deuda. Esto es para prevenir _griefing_ a través del uso de `flash loans` (préstamos rápidos).  

## Información Adicional  

* [MIP27: Modulo de Acceso Instantáneo al Techo de Deuda](https://forum.makerdao.com/t/mip27-debt-ceiling-instant-access-module/4625)
* [DC-IAM Dirección del Contrato en Etherscan](https://etherscan.io/address/0xc7bdd1f2b16447dcf3de045c4a039a60ec2f0ba3)
* [DssAutoLine Griefing Attack](https://forum.makerdao.com/t/mip27-debt-ceiling-instant-access-module/4625/22)
* [Tag DC-IAM en el Foro de Maker](https://forum.makerdao.com/tag/dc-iam)

## Apéndice

* Contrato de un solo método para la ejecución de DC-IAM para todos los tipos de _vaults_ al mismo tiempo: [https://etherscan.io/address/0xd5a63a56c790c67e3f92bce5076dc464f98c6df1\#writeContract](https://etherscan.io/address/0xd5a63a56c790c67e3f92bce5076dc464f98c6df1#writeContract)

* Lista de códigos hexadecimales para todos los tipos de _vaults_ que se pueden introducir en el DC-IAM:
  * **AAVE-A**
    * 0x414156452d410000000000000000000000000000000000000000000000000000
  * **BAL-A**
    * 0x42414c2d41000000000000000000000000000000000000000000000000000000
  * **BAT-A**
    * 0x4241542d41000000000000000000000000000000000000000000000000000000
  * **COMP-A**
    * 0x434f4d502d410000000000000000000000000000000000000000000000000000
  * **ETH-A**
    * 0x4554482d41000000000000000000000000000000000000000000000000000000
  * **ETH-B**
    * 0x4554482d42000000000000000000000000000000000000000000000000000000
  * **KNC-A**
    * 0x4b4e432d41000000000000000000000000000000000000000000000000000000
  * **LINK-A**
    * 0x4c494e4b2d410000000000000000000000000000000000000000000000000000
  * **LRC-A**
    * 0x4c52432d41000000000000000000000000000000000000000000000000000000
  * **MANA-A**
    * 0x4d414e412d410000000000000000000000000000000000000000000000000000
  * **RENBTC-A**
    * 0x52454e4254432d41000000000000000000000000000000000000000000000000
  * **UNI-A**
    * 0x554e492d41000000000000000000000000000000000000000000000000000000
  * **WBTC-A**
    * 0x574254432d410000000000000000000000000000000000000000000000000000
  * **YFI-A**
    * 0x5946492d41000000000000000000000000000000000000000000000000000000
