# Límite de Liquidación Local

>**Alias:** Local Liquidation Limit  
>**Parameter Name:** `hole`  
>**Containing Contract:** `Dog`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:**  

## Descripción

El Límite de Liquidación Local establece la cantidad máxima de deuda en DAI para la cual las subastas de colaterales pueden estar activas en cualquier momento dentro de un tipo de _vault_ en particular (`ilk`). Cuando el valor total de DAI de las subastas supera este máximo para un tipo de _vault_ en particular, no se pueden subastar más colaterales utilizando ese tipo de _vault_ hasta que otras se completen.

Cada tipo de _vault_ tiene un Límite de Liquidación Local por separado. Si las subastas de las liquidaciones de ETH-A llenan el límite de liquidación local de ETH-A, no se pueden activar más subastas en la _vault_ de ETH-A, pero las liquidaciones en la _vault_ de WBTC-A aún podrían ir a subasta.

## Propósito

Al igual que el Límite de Liquidación Global, el parámetro de Límite de Liquidación Local existe para evitar que un exceso en un tipo de colateral particular abrume a los _Keepers_ de Maker o al mercado en general. Mientras que la implementación de _Liquidations 2.0_ resuelve muchas inquietudes sobre la liquidación _Keeper_, la colateral adquirida en una subasta aún debe venderse en el mercado.

En el caso de que una colateral tenga múltiples tipos de _vaults_, el Límite de Liquidación Local ayuda a evitar que los tipos de _vaults_ riesgosas aceleren una liquidación del mercado que podría desencadenar liquidaciones en otros tipos de _vaults_ en cascada que comparten el mismo activo de colateral.

## Contrapartida

Si bien el Límite de Liquidación Local proporciona una medida adicional de seguridad para los tipos de _vaults_ individuales, establecer un límite apropiado es bastante difícil. Si este parámetro se establece en un valor demasiado alto, una gran disminución o explotación de la colateral dentro de una _vault_ en particular podría generar rápidamente un nivel inaceptable de deuda incobrable dentro del sistema.

El principal riesgo de establecer el parámetro de Límite de Liquidación Global demasiado bajo es que se podrían crear una acumulación de posiciones infracolateralizadas, lo que daría lugar a la acumulación de deuda incobrable por encima de las tasas de mercado en el momento de la subasta. Cuanto más tiempo transcurre, este escenario se vuelve cada vez más peligroso para el protocolo (como en una disminución prolongada de múltiples activos colaterales).

## Cambios

El ajuste del parámetro de Límite de Liquidación Local es un proceso manual que requiere una votación ejecutiva. Los cambios al Incentivo de Activación Proporcional están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar este parámetro?**

La razón principal para incrementar el Límite de Liquidación Local sería la confianza en la configuración de riesgo de un tipo de _vault_ combinada con abundante liquidez de mercado para el activo de la colateral subyacente. Siempre que haya suficiente liquidez, es posible que la comunidad desee aumentar el Límite de Liquidación Local para evitar una situación en la que el protocolo no pueda subastar posiciones inseguras con la suficiente rapidez.

**¿Por qué reducir este parámetro?**

Por el contrario, la razón principal para reducir el Límite de Liquidación Local es la preocupación por la liquidez de un tipo de colateral subyacente o los otros parámetros de riesgo de un tipo de _vault_. Si existen dudas sobre la liquidez de los Keepers de Maker o el mercado más amplio para absorber las grandes órdenes de venta provocadas por las liquidaciones, una respuesta puede ser reducir el Límite de Liquidación Local para los tipos de _vault_ respaldadas por activos colaterales que tienen menos liquidez de mercado.

## Consideraciones

El sistema _Liquidations 2.0_ permite que el Límite de Liquidación Local se establezca en un nivel más alto que el `box` (_caja_) en _Liquidations 1.2_ porque el formato de Subasta Holandesa permite la liquidación instantánea, lo que permite el uso de _Flash Loans_ (_préstamos rápidos_) por parte de los _Keepers_ de Maker. Sin embargo, dado que las subastas pueden tener una liquidación casi instantánea, el Límite de Liquidación Local siempre actúa como un límite de tasa en las subastas de colaterales.

Durante el Apagado de Emergencia, no se pueden realizar nuevas subastas de colaterales. Todas las subastas en curso durante un apagado de emergencia, habrían de estar sujetas a los parámetros del Límite de Liquidación Local sin consideraciones especiales.

---

[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/collateral-auction/param-local-liquidation-limit.md)
