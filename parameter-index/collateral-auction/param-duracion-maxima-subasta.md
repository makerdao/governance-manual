# Duración Máxima de Subasta

>**Alias:** Max Auction Duration  
>**Parameter Name:** `tail`  
>**Containing Contract:** `Clipper`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:**  

## Descripción

El parámetro de Duración Máxima de Subasta establece el tiempo máximo que puede transcurrir antes de que una subasta deba reiniciarse para un tipo de _vault_ en particular. Expresado en segundos, este parámetro determina cuándo ya no puede liquidarse una subasta y ésta debe reiniciarse.

Si la Duración Máxima de Subasta se establece en 9.000 segundos para un tipo de _vault_ determinada, entonces cualquier subasta en el sistema de liquidaciones para ese tipo de _vault_, que haya estado funcionando durante más de 2.5 horas, no podrá liquidarse y esta deberá reiniciarse.

El parámetro de Duración Máxima de Subasta se superpone con el parámetro de Reducción Máxima de Subastas en el sentido de que será necesario reiniciar una subasta una vez que se exceda el máximo.

## Propósito

El parámetro de Duración Máxima de Subasta existe para evitar que las subastas continúen por más tiempo del que la Gobernanza de Maker desea. Es redundante con el parámetro de Reducción Máxima de Subastas y permite que la Gobernanza de Maker decida si establecer la duración máxima de forma directa o implícitamente a través de los parámetros Curva de Precio de Subastas y Reducción Máxima de Subastas.

La Duración Máxima de Subasta debería usarse si la Función de Precio de Subastas para un tipo de _vault_ fuera completamente plana (ofreciendo una redención de precio fijo), lo que puede ser cierto cuando se liquidan colaterales de _stablecoins_.


## Contraparte

Una Duración Máxima de Subasta grande aumenta la cantidad de tiempo que los _Keepers_ tienen para ofertar en la subasta antes de que sea necesario reiniciarla. Por otro lado, el que se tenga una duración acotada significa que se debe confiar en la rápida participación de los _Keepers_ en las subastas de colaterales.

Si las subastas son demasiado cortas, existe el riesgo de que las liquidaciones no finalicen de manera rentable antes de que se requiera un reinicio. Esto puede ser negativo dependiendo de la configuración del Incentivo Plano de Activación y el Incentivo Proporcional de Activación porque en cada reinicio estos incentivos se pagan a los _Keepers_.

Las contrapartes de este parámetro están fuertemente ligadas al parámetro de Función de Precio de Subastas, ya que la forma de la curva puede afectar en gran medida la duración deseada de la subasta.

## Cambios

El ajuste del parámetro de Duración Máxima de Subasta para un tipo específico de _vaults_ es un proceso manual que requiere un Voto Ejecutivo. Los cambios al parámetro de Duración Máxima de Subasta están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

## Consideraciones

Solo se pueden reiniciar las subastas si se supera tanto el parámetro de Duración Máxima de Subasta como el parámetro de Reducción Máxima de Subastas.

Durante un Apagado de Emergencia, las nuevas subastas se detendrán, pero el Disyuntor de Liquidaciones de Tres Etapas determinará si las subastas en curso se pueden restablecer o no. Si solo se activa un nivel adicional del disyuntor, aún se utilizará la Duración Máxima de Subasta para verificar la elegibilidad para el restablecimiento de las subastas, pero no se pueden realizar restablecimientos en el nivel más severo del Disyuntor de Liquidaciones, lo que limita la efectividad del parámetro.

---

[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/collateral-auction/param-max-auction-duration.md)
