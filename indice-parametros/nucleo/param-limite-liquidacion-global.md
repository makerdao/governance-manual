# Límite de Liquidación Global

>**Alias:** Global Liquidation Limit  
>**Nombre del Parámetro:** `Hole`  
>**Contrato:** `Dog`  
>**Alcance:** System  
>**Documentos Técnicos:**  

## Descripción

El Límite de Liquidación Global marca la cantidad máxima de deuda en DAI para la que las subastas de colaterales pueden estar activas en cualquier momento. Cuando el valor total de DAI de las subastas excede este máximo, no podrán comenzar nuevas subastas hasta que las otras sean completadas.

El Límite de Liquidación Global comprende todos los tipos de _vaults_. Si las subastas de liquidaciones ETH-A llenan el Límite de Liquidación Global, no pueden ser activadas nuevas subastas de _vaults_ ETH-A ni tampoco de _vaults_ WBTC-A.

## Propósito

El propósito del Límite de Liquidación Global es prevenir que la cantidad de colateral disponible para subastas no exceda lo que el mercado puede manejar, evitando así que incurra en un deslizamiento inaceptable. Mientras la implementación de Liquidaciones 2.0 resuelve muchas preocupaciones sobre la liquidez de los _Keepers_, el colateral comprado en subasta aún tiene que venderse en el mercado general.

El Límite de Liquidación Global también tiene un rol importante durante casos de ataques maliciosos al protocolo, previniendo que un gran porcentaje de colaterales sean movidos a subastas al mismo tiempo.

## Contrapartida

Si bien el Límite de Liquidación Global provee algo de seguridad para el sistema, establecer un límite puede ser difícil. Si este parámetro es establecido demasiado alto, el mercado general puede verse abrumado y las subastas de colateral pueden incurrir en más deslizamientos no deseados.

Sumado a las preocupaciones ya mencionadas, tener un Límite de Liquidación Global muy alto durante un momento de enorme volatilidad podría crear una demanda de DAI que rompa la altura del _peg_, causando así más inconvenientes para los usuarios que estén intentando evitar una liquidación.

El mayor riesgo a la hora de establecer un parámetro Límite de Liquidación Global demasiado bajo, es que se podría generar un _backlog_ de posiciones sub-colateralizadas, lo que llevaría a una acumulación de _deuda incobrable_, que esté por encima de las tasas del mercado para cuando esta salga a subasta. Este escenario se vuelve más y más peligroso para el protocolo a medida que siga sucediendo (como ocurre con una caída prolongada en múltiples activos de colaterales).

## Cambios

Ajustar el parámetro Límite de Liquidación Global es un proceso manual que requiere un Voto Ejecutivo. Los cambios al Límite de Liquidación Global están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar este parámetro?**

La razón principal para incrementar el Límite de Liquidación Global, sería la confianza en el sistema de subastas de colaterales subyacente y la liquidez de DAI disponible en el mercado. Si el mercado más amplio tiene una fuerte liquidez en colaterales cruzados y liquidez de DAI, un incremento en el Límite de Liquidación Global podría permitir que posiciones poco seguras sean liquidadas más rápido, para ayudar a proteger al protocolo durante las caídas fuertes del mercado.

**¿Por qué disminuir este parámetro?**

En cambio, la razón principal para disminuir el Límite de Liquidación Global es que haya alguna preocupación por el sistema de subastas de colaterales subyacente. Si hay preocupación sobre la liquidez accesible para los _Keepers_ o sobre la habilidad del mercado más amplio de absorber grandes órdenes de venta sin deslizamientos significativos, entonces bajar el Límite de Liquidación Global puede ser aconsejable.

## Consideraciones

El sistema de Liquidaciones 2.0 permite configurar el Límite de Liquidación Global a un nivel más alto que Liquidaciones 1.2, dado que el formato de Subasta Holandesa permite un acuerdo inmediato, permitiendo el uso de _Préstamos Rápidos_ por parte de los _Keepers_ de Maker. Sin embargo, ya que las subastas pueden tener arreglos casi instantáneos, el Límite de Liquidación Global no actúa como un límite de tasas para las subastas, como lo hizo en las Liquidaciones 1.2.

Durante un Apagado de Emergencia, ninguna subasta de colaterales nueva puede ser iniciada. Todas las subastas en curso durante un Apagón de Emergencia estarían sujetas al Límite de Liquidación Global sin consideraciones especiales.
