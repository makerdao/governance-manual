# Demora de Subasta de Deuda

>**Alias:** Flop Delay  
>**Nombre del Parámetro:** wait  
>**Contenido del Contrato:** Vow  
>**Alcance:** System  
>**Documentos Técnicos:** [Enlace](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/vow-detailed-documentation)  

## Descripción

La Demora de Subasta de Deuda o parámetro `wait`, define el tiempo que debe transcurrir tras la liquidación de una _vault_, antes de que la deuda correspondiente se marque como deuda incobrable.

Si una Subasta de Colateral correspondiente no salda la deuda y cualquier tarifa de penalización es asociada con la Demora de Subasta de Deuda, la deuda restante será considerada como deuda incobrable. Esto podría ocurrir, si la subasta de colateral no recauda suficiente Dai para cubrir la deuda total, a pesar de que todo el colateral haya sido vendido o si la subasta no finaliza dentro del plazo de la Demora de Subasta de Deuda.  

Inicialmente, el _buffer_ de excedentes cubrirá la deuda incobrable, pero si el sistema acumula suficiente deuda incobrable como para agotar al _buffer_ de excedentes, el sistema activará una Subasta de Deuda donde el MKR sera acuñado y vendido para cubrir el balance.

### Ejemplo

`Demora de Subasta de Deuda` = 2 horas

Una vez que una _vault_ es liquidada, si la deuda de la _vault_ no ha sido cubierta en un plazo de dos horas, será considerada como deuda incobrable, si el _buffer_ de excedentes no puede cubrir la deuda, comenzará una subasta de deuda.

## Propósito

La Demora de Subasta de Deuda existe para brindar tiempo a los _keepers_ y que estos puedan ofertar por las _vault_s liquidadas a través de las Subastas de Colaterales. Si la Demora de Subasta de Deuda está fijada a cero, todas las liquidaciones procederán instantáneamente a Subastas de Deuda, así como también se activarán Subastas de Colateral, las cuales acuñarán y posteriormente quemarán cantidades innecesarias de MKR.

## Contraparte

Si la Demora de Subasta de Deuda es muy corta, el sistema puede iniciar de forma prematura una Subasta de Deuda antes de que la Subasta de Colateral Correspondiente haya sido completada. Por ejemplo, esto puede ocurrir si la Demora de Subasta de Deuda es fijada a un valor menor que la Máxima Duración de Subasta de Colateral. En esta situación, es posible que los _keepers_ puedan cubrir la deuda pendiente con el tiempo restante, haciendo innecesaria la Subasta de Deuda. Este escenario puede hacer que se genere MKR excesivamente o que se agote el _buffer_ de Excedentes.   

Si la Demora de Subasta de Deuda es muy larga, se evitará que ocurran las Subastas de Deuda. Esto evitará que el Dai que esté sub-colateralizado sea removido del sistema. Permitir que el Dai se mantenga sub-colateralizado, podría dañar la confianza del Dai.

## Cambios

Ajustar la Demora de Subasta de Deuda es un proceso manual que requiere de un Voto Ejecutivo. Los cambios en la Demora de Subasta de Deuda están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué aumentar este parámetro?**
La Demora de Subasta de Deuda se debería incrementar si aumenta la Máxima Duración de Subasta de Colateral para evitar Subastas de Deuda innecesarias. Esta también se puede aumentar si se espera que haya un mayor número de Subastas de Deuda, para asegurar que los _keepers_ tengan suficiente capital en Dai para ofertar por el MKR que está siendo subastado.

**¿Por qué reducir este parámetro?**
La Demora de Subasta de Deuda se puede disminuir si se está tomando mucho tiempo para comenzar una Subasta de Deuda, dejando al sistema sub-colateralizado por un período de tiempo más largo de lo aceptable. Esto podría impactar negativamente sobre los usuarios del Dai y dañar la confianza del Dai en general.

## Consideraciones

Ya que las Subastas de Deuda pueden ocurrir antes de que la correspondiente Subasta de Colaterales haya terminado, es prudente asegurarse que la `Demora de Subasta de Deuda > Máxima Duración de Subasta` para permitir que el plazo de las Subastas de Colaterales culmine.

En teoría, la Gobernanza de Maker puede arbitrariamente extender la Demora de Subasta de Deuda, evitando así que las Subastas de Colateral ocurran indefinidamente.  

En caso de un Apagado de Emergencia, todas las subastas de Deuda son canceladas y la Demora de Subasta de Deuda queda anulada.
