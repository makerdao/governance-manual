# Techo de Deuda

>**Alias:** N/A  
>**Nombre del Parámetro:** `line`  
>**Contrato:** `Vat`  
>**Alcance:** Vault Type (Ilk)  
>**Documentos Técnicos:** [Enlace](https://docs.makerdao.com/smart-contract-modules/core-module/vat-detailed-documentation)  

## Descripción

El parámetro de Techo de Deuda controla la cantidad máxima de DAI que puede ser acuñado usando un tipo específico de _vault_, a través de todos los usuarios de _vaults_. Si un usuario trata de acuñar DAI y si la cantidad de DAI que quiere acuñar pondría el monto en DAI acuñado de ese tipo de _vault_ por encima del Techo de Deuda, la transacción fallará y el DAI no será acuñado.

Cada tipo de _vault_ tiene su propio Techo de Deuda, que puede ser ajustado por la Gobernanza de Maker. Nótese que el Techo de Deuda se aplica colectivamente a todas las _vaults_ creadas usando un tipo específico de _vault_, en vez de _vaults_ individuales.

Adicionalmente, existe otro parámetro, que es el Techo de Deuda Global, que no será tratado en este artículo. Para que un usuario pueda acuñar DAI desde su _vault_, debe haber espacio disponible en ambos, tanto en el Techo de Deuda como en el Techo de Deuda Global.

El Techo de Deuda para cada tipo de _vault_ es expresado en términos absolutos en vez de términos relativos, por lo que serían 1.000.000 DAI en vez de 10% de Techo de Deuda Global.  

## Propósito

El propósito principal del parámetro de Techo de Deuda es el de permitir que la Gobernanza controle la cantidad de DAI que puede ser creado usando ciertos tipos de _vaults_. Controlar la cantidad de DAI que es acuñado por ciertos tipos de _vault_ limita la exposición al riesgo del colateral usado dentro de dicho tipo de _vault_. También disminuye el riesgo de combinar sistemas de parámetros que son usados dentro de un tipo de _vault_, por ejemplo, un Ratio de Liquidación muy bajo, combinado con una Tarifa de Estabilidad alta.

## Contrapartida

Aumentar el Techo de Deuda de un tipo de _vault_ permite que más DAIs sean acuñados usando ese mismo tipo de _vault_. En la mayoría de los casos, esto es positivo debido a que la Gobernanza de Maker casi siempre querrá crear más DAI, ya que se puede mantener al _peg_ del precio a $1.

Sin embargo, aumentar el Techo de Deuda y permitir que el DAI este fuertemente colateralizado por un solo activo aumenta el riesgo de que ocurra un evento de  cisne negro que se localiza en ese activo.  

Tener una gran cantidad de ´espacio libre´ entre el Techo de Deuda para un tipo de _vault_ y la cantidad actual de DAI acuñado que utiliza dicho tipo de _vault_ representa un gran riesgo. En el caso de una caída significativa en los precios de la colateral usada dentro de este tipo de _vault_, los poseedores de esta colateral pueden cambiar su pérdida en el Protocolo de Maker, acuñando DAI y dejando que Maker se encargue de la colateral mala. Este riesgo es conocido como el ´Tiempo de Ataque de OSM´ (_Oracle Security Module_ o _Módulo de Seguridad de Oráculos_ en español) porque solo es posible gracias al retraso de una hora en las actualizaciones de precios del OSM.

Dejar una gran cantidad de ´espacio libre´ en el Techo de Deuda de un tipo de _vault_, también significa que el suministro de DAI puede cambiar rápidamente, de forma que pueda afectar al _peg_ del precio del DAI.

## Cambios

Ajustar el Techo de Deuda para un tipo específico de _vault_ es un proceso manual que requiere de un Voto Ejecutivo. Los cambios en los parámetros del Techo de Deuda están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar un parámetro de Techo de Deuda?**

La razón principal por la cual aumentar el Techo de Deuda de un tipo de _vault_ es para permitir que más DAI sea acuñado usando ese tipo de _vault_. Generalmente, esto es positivo, ya que implica que tarifas adicionales sean recolectadas por el Protocolo y aumente el suministro de DAI.

Usualmente, esta razón solo es válida si se predice que el Techo de Deuda actual será alcanzado y se evitarán futuras acuñaciones.

**¿Por qué disminuir un parámetro de Techo de Deuda?**

La razón principal para disminuir el Techo de Deuda de un tipo de _vault_, es para diminuir el riesgo e impacto del ´Tiempo de Ataque OSM´ que se describe más arriba.

Un Techo de Deuda puede ser reducido por debajo de la cantidad actual de deuda utilizada para un tipo de _vault_, para dasaprobar o evitar temporalmente que se acuñe DAI utilizando ese tipo de _vault_.  

El parámetro también se puede usar para promover la diversificación entre los tipos de _vault_ que están basados en activos similares. Por ejemplo, la disminución del Techo de Deuda del USDC-A podría utilizarse para desplazar el uso de las _stablecoins_ hacia TUSD-A o PAX-A.

También, el Techo de Deuda puede ser reducido como un intento de afectar a la política monetaria aunque, en el pasado, la Gobernanza de Maker ha preferido usar la estabilidad para este propósito.

## Consideraciones

El Techo de Deuda para un tipo de _vault_ puede ser excedido a medida que las tarifas de estabilidad se acumulan en las _vaults_ dentro de ese tipo de _vault_.

Si el parámetro de Techo de Deuda para un tipo de _vault_ cae por debajo del monto actual del DAI acuñado usando ese tipo de _vault_, este no tendrá ningún efecto negativo, más allá de evitar futuras acuñaciones que usen ese tipo de _vault_.
