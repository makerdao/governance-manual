# Piso de Deuda

>**Alias:** Dust, Minimum Debt  
>**Parameter Name:** `dust`  
>**Containing Contract:** `Vat`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:** [link](https://docs.makerdao.com/smart-contract-modules/core-module/vat-detailed-documentation)  

## Descripción

El parámetro de Piso de Deuda controla el monto mínimo de DAI que puede ser acuñado usando un tipo de _vault_ específica para una _vault_ individual. Si un usuario intenta acuñar DAI y el monto de DAI que se acuña no logra hacer que el monto de DAI ya acuñado en la _vault_ supere su Piso de Deuda, la transacción fallará y no se acuñará DAI. Del mismo modo, si un usuario intenta pagar una deuda de tal manera que su deuda sea inferior al Piso de Deuda y mayor que cero, la transacción fallará y no se devolverá ningún DAI.

Cada tipo de _vault_ tiene su propio Piso de Deuda que puede ser ajustado por la Gobernanza de Maker. Nótese que el Piso de Deuda aplica a cada _vault_ individual, en lugar de al conjunto de _vaults_. Esto último es lo que difiere del Techo de Deuda.

El Piso de Deuda para cada _vault_ se expresa en términos absolutos.

## Propósito

El objetivo principal del Piso de Deuda es evitar que los usuarios creen múltiples _vaults_ con un colateral y un monto de deuda muy bajos. Los _Keepers_ de las mismas pueden verse reacios a liquidar pequeñas _vaults_ porque su recompensa es baja con respecto a los costos de _gas_ de liquidación y licitación para las siguientes subastas. Esto es un problema ya que el Protocolo de Maker se basa en liquidaciones rápidas para evitar la acumulación de deudas incobrables.

## Contrapartida

Incrementar el Piso de Deuda limita el tamaño mínimo de las _vaults_ haciendo que los _Keepers_ puedan liquidar _vaults_ de manera rentable donde el ratio de colateralización ha caído por debajo del ratio de liquidación.

Sin embargo, incrementar el Piso de Deuda perjudica el uso de las _vaults_. Establecer el Piso de Deuda demasiado alto puede excluir a los usuarios con menos capital de usar por completo las _vaults_ de Maker.

Además, cuanto más alto se establece el Piso de Deuda, más difícil se vuelve probar la funcionalidad de la _vault_ del Protocolo de Maker sin arriesgar un capital significativo.

## Cambios

Ajustar el parámetro de Piso de Deuda para un tipo de _vault_ específica es un proceso manual que requiere un Voto Ejecutivo. Los cambios en los parámetros del Piso de Deuda están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

En el pasado, la Gobernanza de Maker modificó el Piso de Deuda de todos los tipos de _vault_ al unísono, en lugar de establecer diferentes valores para cada tipo de _vault_.

**¿Por qué incrementar este parámetro?**
Es posible que la Gobernanza de Maker desée aumentar este parámetro si los precios del _gas_ en la red Ethereum se han mantenido con tasas altas. Esto indica que los _Keepers_ pueden llegar a tener problemas para liquidar _vaults_ pequeñas ya que el costo del _gas_ excederá la recompensa relativa de puja en colaterales para las mismas.

**¿Por qué disminuir este parámetro?**
Es posible que la Gobernanza de Maker desée reducir este parámetro si desean hacer a las _vaults_ de Maker más atractivas al uso para aquellos que posean un capital pequeño.

Alternativamente, si los precios del _gas_ en la red de Ethereum bajan a tasas consistentemente más bajas, es posible reducir el parámetro de Piso de Deuda para un tipo de _vault_ sin impactar negativamente en las liquidaciones.

## Consideraciones

Las _vaults_ que tengan una deuda menor a su Piso de Deuda actual no podrán retirar o pagar DAI adicional a menos que su deuda total se coloque por encima del Piso de Deuda o se reduzca a cero. Sin embargo, no serán liquidadas a la fuerza ni sufrirán ninguna consecuencia negativa inmediata.

___

[Texto original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/vault-risk/param-debt-floor.md)
