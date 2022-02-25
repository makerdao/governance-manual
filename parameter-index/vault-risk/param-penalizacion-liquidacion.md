# Penalización de Liquidación

>**Alias:** Liquidation Penalty  
>**Parameter Name:** `chop`  
>**Containing Contract:** `Dog`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:**  

## Descripción

El parámetro de Penalización de Liquidación controla la tarifa que los poseedores de las _vaults_ deben pagar cuando su posición se liquida debido a colaterales insuficientes. Para que el poseedor de una _vault_ reciba de regreso cualquier colateral del proceso de liquidación, la deuda y la Penalización de Liquidación deben estar cubiertas por la subasta de colaterales.

Cada tipo de _vault_ tiene su propia Penalización de Liquidación que puede ser ajustada por la Gobernanza de Maker. Ten en cuenta que la Penalización de Liquidación se aplica colectivamente a todas las _vaults_ creadas con un tipo de _vault_ específico, en lugar de a las _vaults_ individuales.

La Penalización de Liquidación se expresa como un porcentaje de la colateral en lugar de una monto fijo. Por ejemplo, si una deuda de 100 DAI se liquida en un tipo de _vault_ con una Penalización por Liquidación del 13%, se activará una subasta con el objetivo de recuperar al menos 113 DAI utilizando la colateral en la vault liquidada.

## Propósito

En general, la Penalización de Liquidación puede considerarse como una tarifa para incentivar la colateralización adecuada para los poseedores de _vaults_. Como parámetro de riesgo, su función principal es asegurar que el sistema no acumule DAI sin respaldo. La Penalización de Liquidación brinda a los usuarios de vaults un incentivo adicional para mantener sus posiciones sobrecolateralizadas al mismo tiempo que brinda al sistema ingresos adicionales para mitigar pérdidas potenciales debido a liquidaciones. La Penalización de Liquidación también juega un papel importante al actuar como elemento disuasorio contra los ataques relacionados con la liquidación al agregar cierta fricción al proceso de liquidación.

## Contraparte

Cuanto mayor sea la Penalización de Liquidación, más usuarios de las _vaults_ tendrán incentivos para mantener su posición financiada de forma segura. Tener posiciones más fuértemente colateralizadas, hace que el ecosistema del DAI sea más seguro.

Sin embargo, cuanto más grande sea la Penalización de Liquidación, más grande será el riesgo para los usuarios de _vaults_. Como resultado, el costo de pedir prestado a través de MakerDAO puede ser demasiado alto o los usuarios pueden optar por dejar sus _vaults_ más fuértemente colateralizadas. Esto reduciría el atractivo del Protocolo de Maker en comparación con los competidores y podría reducir la generación de DAI.

Cuanto mayor sea la Penalización de Liquidación, es menos probable que a un usuario de una _vault_ le quede colateral después de un evento de liquidación. Si bien es apropiado para incentivar el mantenimiento adecuado de una _vault_, la Penalización de Liquidación puede causar un riesgo para el sistema cuando se establece en un valor demasiado bajo y desalentar la generación de DAI si se establece en un valor demasiado alto.

## Cambios

El ajuste del parámetro de Penalización de Liquidación es un proceso manual que requiere una votación ejecutiva. Los cambios a la Penalización de Liquidación están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar el parámetro de Penalización de Liquidación?**

El incrementar de la Penalización de Liquidación debería generar más ingresos para el sistema durante los eventos de liquidación. Si bien existen consideraciones fiscales vinculadas a este parámetro, la principal razón para incrementar la Penalización de Liquidación se debe al riesgo o al riesgo percibido de un tipo de colateral durante la liquidación. Las colaterales que son menos deseadas o más riesgosas de mantener, debido a la fluctuación de precios, pueden dar lugar a un aumento de la Penalización de Liquidación para tener en cuenta las pérdidas potenciales debidas a subastas ineficientes.

Al aumentar este parámetro, se debe prestar atención a las relaciones públicas y la comunicación. Los usuarios de _vaults_ que no estén al tanto de un aumento pueden sentirse víctimas si luego son liquidados y pierden más colaterales de los que esperaban.

**¿Por qué disminuir el parámetro de Penalización de Liquidación?**

La reducción de la Penalización de Liquidación debería dar como resultado menos ingresos al sistema durante los eventos de liquidación y, al mismo tiempo, aumentar las posibilidades de que los poseedores de las _vaults_ reciban el colateral de regreso luego de la liquidación. Si bien puede haber razones comerciales para reducir este parámetro, la principal razón para reducir la Penalización de Liquidación sería la confianza en el sistema de subastas. La reducción de la Penalización de Liquidación resulta en la reducción del costo esperado de manutención de la posición de una _vault_, lo que genera mayor incentivos para la creación de DAI.

## Consideraciones

Dado que este parámetro afecta directamente el riesgo de los poseedores de las _vaults_ y el sistema, los cambios en el parámetro de Penalización de Liquidación siempre deben realizarse con sumo cuidado.

La Penalización de Liquidación siempre debe ser más alta que la suma de las recompensas de liquidación (`tip` y `chip`) para evitar el farmeo de incentivos, una práctica mediante la cual un atacante liquida deliberadamente sus propias _vaults_ para obtener las recompensas de liquidación.

Particularmente importante para los poseedores de _vaults_ es la noción de que la Penalización de Liquidación representa la pérdida mínima durante un evento de liquidación, no la máxima. Dado que los poseedores de _vaults_ solo recibirán colaterales en exceso de la deuda liquidada y la Penalización de Liquidación, no hay garantía de que la subasta de colaterales sea suficiente para cubrir ambas.

Durante un Apagado de Emergencia, no se pueden iniciar nuevas subastas de colaterales. Todas las subastas en curso durante un apagado de emergencia estarán sujetas al parámetro de Penalización de Liquidación sin consideraciones especiales.
---
[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/vault-risk/param-liquidation-penalty.md)
