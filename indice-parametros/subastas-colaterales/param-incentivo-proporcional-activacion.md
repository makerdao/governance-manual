# Incentivo Proporcional de Activación

>**Alias:** Proportional Kick Incentive  
>**Parameter Name:** `chip`  
>**Containing Contract:** `Clipper`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:**  

## Descripción

El parámetro del Incentivo Proporcional de Activación representa la recompensa en DAI que se le paga a los _Keepers_ que activan las subastas de liquidación de colaterales en el Protocolo de Maker.

El Incentivo Proporcional de Activación está establecido como un porcentaje y representa una fracción de DAI basada en la deuda de la vault que está siendo liquidada. El DAI es recompensado en cada subasta de liquidación al momento en que se activa dicha subasta.

Cada tipo de vault tiene su propio Incentivo Proporcional de Activación que la Gobernanza de Maker puede ajustar por separado.

## Propósito

El Incentivo Proporcional de Activación existe para asegurar que las subasta sean activadas de manera rápida y confiable, incluso en tiempos de tarifas de _gas_ altas en la _blockchain_ de Ethereum.

## Contrapartida

El tener un gran parámetro de Incentivo Proporcional de Activación debería hacer que las subastas de liquidación de _vaults_ grandes se activen de manera rápida y confiable. Sin embargo, este incentivo reduce directamente los ingresos del Protocolo de Maker.

Establecer el parámetro demasiado bajo puede provocar que las subastas de liquidación no se activen lo suficientemente rápido como para evitar una pérdida neta para el Protocolo de Maker.

Si este parámetro se establece más alto que la Penalización de Liquidación para las _vaults_, este brinda una oportunidad para que los atacantes exploten el sistema liquidando sus propias _vaults_ para obtener el incentivo en DAI.

## Cambios

El ajuste del parámetro de Incentivo Proporcional de Activación es un proceso manual que requiere una votación ejecutiva. Los cambios al Incentivo Proporcional de Activación están sujetos al Bloqueo de Tiempo del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar este parámetro?**

Incrementar el Incentivo Proporcional de Activación puede ser deseable cuando los precios del _gas_ son lo suficientemente altos como para disuadir a los _Keepers_ de iniciar subastas de manera rápida y confiable.

Tener liquidaciones rápidas y confiables disminuye las posibilidades de acumular deudas incobrables cuando el precio de un activo colateral está cayendo.

**¿Por qué reducir este parámetro?**

Es importante que este parámetro sea razonablemente más bajo que la Penalización de Liquidación para que los ataques relacionados con subastas sean menos atractivos para los actores malintencionados.

La Gobernanza puede querer reducir este parámetro si determina que 'el pago en exceso' a los _Keepers_ es lo que desencadena las liquidaciones.

## Consideraciones

El parámetro del Incentivo Proporcional de Activación debe establecerse de manera que:
`Incentivo Proporcional de Activación < Penalización de Liquidación`

La combinación de incentivos de liquidaciones debe establecerse de manera que lo siguiente sea cierto:
`Incentivo Plano de Activación + Incentivo Proporcional de Activación < Penalización de Liquidación + Costos de _Gas_ de Liquidación + Costos de _Gas_ de Creación de Vaults`.

Si tanto el Incentivo Proporcional de Activación y como el Incentivo Plano de Activación no son _0_, ambos serán dados a un _Keeper_ que active un liquidación válida.

El restablecer una subasta fallida también otorgará al _Keeper_ que la activó el Incentivo Proporcional de Activación.

Los fondos para el Incentivo Proporcional de Activación se sacan del buffer de excedentes y pueden desencadenar en la acuñación de MKR si no hay DAI disponible dentro del buffer de excedentes.

___

[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/collateral-auction/param-proportional-kick-incentive.md)
