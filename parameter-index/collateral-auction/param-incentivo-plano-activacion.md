# Incentivo Plano de Activación

>**Alias:** Flat Kick Incentive  
>**Parameter Name:** `tip`  
>**Containing Contract:** `Clipper`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:**  

## Descripción

El parámetro de Incentivo Plano de Activación representa una recompensa en DAI que se paga a los _Keepers_ que desencadenan subastas de liquidación de colaterales en el Protocolo de Maker.

El Incentivo Plano de Activación es un monto fijo de DAI que se recompensa por cada subasta de liquidación al momento en que la subasta se activa.

Cada tipo de _vault_ tiene su propio Incentivo Plano de Activación que la Gobernanza de Maker puede ajustar por separado.

## Propósito

El propósito de este parámetro es compensar el costo del _gas_ por activar las liquidaciones de la _vault_ si los costos del _gas_ en la _blockchain_ de Ethereum aumentan hasta el punto en el que las liquidaciones no se activan con prontitud.

## Contrapartida

Incrementar el parámetro de Incentivo Plano de Activación debería causar que las subastas se activen de manera más confiable incluso para las _vaults_ más pequeñas en donde la cantidad de colaterales en subasta pueden no ser atractiva para los _Keepers_. A su vez, hacer que las subastas se activen de manera confiable para las _vaults_ más pequeñas puede permitir que la Gobernanza mantenga un Piso de Deuda más bajo.

Sin embargo, si este parámetro se establece más alto que el costo del _gas_ para crear y liquidar _vaults_, este crea una oportunidad para que los atacantes exploten el sistema liquidando sus propias vaults para obtener el incentivo en DAI.

Otra contrapartida es que los fondos para este parámetro se sacan del buffer de excedentes, lo que significa que las liquidaciones de vaults muy pequeñas pueden costarle a la Gobernanza más de lo que gana a través de la Penalización de Liquidación.

## Cambios

El ajuste del parámetro de Incentivo Plano de Activación es un proceso manual que requiere un Voto Ejecutivo. Los cambios al Incentivo Plano de Activación están sujetos al Bloqueo de Tiempo del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar este parámetro?**

La Gobernanza puede considerar incrementar el Incentivo Plano de Activación para un tipo de _vault_ si los altos precios del _gas_ impiden la liquidación de _vaults_ más pequeñas dentro de ese tipo de _vault_.

**¿Por qué reducir este parámetro?**

La Gobernanza puede considerar disminuir el Incentivo Plano de Activación para un tipo de _vault_ si las _vaults_ más pequeñas se liquidan de manera confiable.

Debe considerarse **enormemente** una disminución de este parámetro cuando, en combinación con el Incentivo Proporcional de Activación y la Penalización de Liquidación, el farmeo de incentivos de liquidación es una opción viable para los atacantes.

## Consideraciones

El parámetro del Incentivo Plano de Activación debe establecerse de manera que:
`Incentivo Plano de Activación < Costos de _Gas_ de Liquidación + Costos de _Gas_ de Creación de Vaults`

La combinación de incentivos de liquidaciones debe establecerse de manera que lo siguiente sea cierto:
`Incentivo Plano de Activación + Incentivo Proporcional de Activación < Penalización de Liquidación + Costos de _Gas_ de Liquidación + Costos de _Gas_ de Creación de Vaults`.

Si tanto el Incentivo Plano de Activación y como el Incentivo Proporcional de Activación no son _0_, ambos serán dados un _Keeper_ que active un liquidación válida.

El restablecer una subasta fallida también otorgará al _Keeper_ que la activó el Incentivo Plano de Activación.

Los fondos para el Incentivo Plano de Activación se sacan del buffer de excedentes y pueden desencadenar en la acuñación de MKR si no hay DAI disponible dentro del buffer de excedentes.

---

[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/collateral-auction/param-flat-kick-incentive.md)
