# Multiplicador de Precio de Subasta

>**Alias:**  
>**Parameter Name:** `buf`  
>**Containing Contract:** `Clipper`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:**  

## Descripción

El parámetro de Multiplicador de Precio de Subasta es un multiplicador que se aplica al precio inicial de la subasta de una colateral.

Cada tipo de _vault_ tiene su propio Multiplicador de Precio de Subasta que la Gobernanza puede ajustar por separado. Este multiplicador tiene la intención de ser mayor a 1.0x ya que el sistema _Liquidations 2.0_ utiliza las subastas de precios en caida. Esto significa que es generalmente preferible que el precio de la subasta comience por encima del precio del mercado y, luego de cierto tiempo, caiga al valor correcto.

Si un usuario es liquidado, el precio del _OSM_ (_Oracle Security Module_, _ Módulo de Seguridad de Oráculos_ en español) está en $100 y el Multiplicador de Precio de Subasta está establecido a 1.6x, el precio inicial de la subasta será de $160.

## Propósito

El objetivo principal del Multiplicador de Precio de Subasta es que, cuando comiencen las subastas de colaterales con caida en los precios, en el caso general, el Protocolo de Maker no comience la subasta por debajo del precio de mercado actual. Un resultado ideal para el Protocolo de Maker es que las subastas de colaterales comiencen ligeramente por encima del precio del mercado y luego caigan al precio del mercado lo más rápido posible.

## Contrapartida

En una situación en la que una caída en los precios de las colaterales desencadene liquidaciones pero sea seguida rápidamente por un aumento en los precios de las colaterales, el Protocolo corre el riesgo de iniciar una subasta a un precio más bajo que el precio del mercado. Esto es malo para el dueño de la _vault_ porque la colateral se venderá con descuento. Si este descuento supera la Penalización de Liquidación, esto también puede ser malo para el Protocolo de Maker. Un Multiplicador de Precio de Subasta superior a 1.0x reduce la probabilidad de que esta situación se de, ya que el precio de subasta inicial se aumenta artificialmente.

La ventaja del Multiplicador de Precio de Subasta mayor a 1.0x se ilustra mejor con un ejemplo:

Imagina que ETH cae de $1000 a $800 y las liquidaciones son activadas para múltiples _vaults_. Debido al _OSM_, estas liquidaciones se retrasan por una hora. en esa hora, el precio del ETH se incrementa a $900.

* Con un Multiplicador de Precio de Subasta de 1.0x, la colateral se vendería instantáneamente a $800; $100 por debajo del precio del mercado.
* Con un Multiplicador de Precio de Subasta de 1.2x, la subasta comenzaría en $960 y, al poco tiempo, bajaría a $900 y cerraría justo por debajo del precio del mercado.

Sin embargo, la desventaja de un Multiplicador de Precio de Subasta más alto es que, en una situación en la que el precio del mercado de un tipo de colateral _sigue_ cayendo, es posible que la subasta de precios en caida nunca alcance el precio del mercado antes de que expire. En esta situación, la venta de la colateral se retrasa y el resultado es un precio general peor que si el Multiplicador del Precio de Subasta hubiera sido más bajo.

Este efecto negativo del Multiplicador de Precio de Subasta se puede mitigar estableciendo una Función de Precio de Subasta que complemente al multiplicador. Por ejemplo, al establecer un Multiplicador de Precio de Subasta más alto en combinación con una Función de Precio de Subasta que disminuye exponencialmente. Para obtener más detalles acerca de la Función de Precio de Subasta, consulta la documentación correspondiente.

## Cambios

El ajuste del parámetro de Multiplicador de Precio de Subasta para un tipo específico de vaults es un proceso manual que requiere una votación ejecutiva. Los cambios al parámetro de Duración Máxima de Subasta están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar este parámetro?**

Un parámetro de Multiplicador de Precio de Subasta debería ser incrementando para un tipo específico de _vault_ si, en el caso general, las subastas comenzaran con precios por debajo de los del mercado.

**¿Por qué reducir este parámetro?**

Un parámetro de Multiplicador de Precio de Subasta debería ser reducido para un tipo específico de _vault_ si, en el caso general, las subastas fueran regularmente reiniciadas debido a que los precios llegan al precio de la Reducción Máxima de Subasta.

## Consideraciones

El precio inicial para una subasta es calculado usando la publicación de precios del _OSM_ multiplicado por el Multiplicador de Precio de Subasta.

---
[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/collateral-auction/param-auction-price-multiplier.md)
