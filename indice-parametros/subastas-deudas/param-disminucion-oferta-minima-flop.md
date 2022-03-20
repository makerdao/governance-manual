# Disminución de la Oferta Mínima (_Flop_)

>**Alias:** Minimum Bid Decrease  
>**Nombre del Parámetro:** `beg`  
>**Contenido del Contrato:** `_Flop_`  
>**Alcance:** System  
>**Documentos Técnicos:** [Enlace](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flop-detailed-documentation)  

## Descripción
Las Subastas de Deuda se usan para recapitalizar el sistema, acuñando y subastando MKR por una cantidad fija de DAI. En este proceso los _keepers_ ofertan una pequeña cantidad de MKR que están dispuestos a aceptar por el monto fijo de DAI que tienen que pagar en la subasta de liquidación.

Durante las Subastas de Deuda, las nuevas ofertas de MKR deben estar por debajo de las actuales ofertas de MKR, por lo menos en un monto determinado por la Disminución de la Oferta Mínima (_Flop_) o `beg`. La Disminución de la Oferta Mínima (_Flop_) se da en términos de un porcentaje mínimo de disminución de la oferta actual.    

En la práctica, la Disminución de la Oferta Mínima (_Flop_) representa a ambos:
* La ganancia máxima que los _keepers_ pueden generar cuando ofertan en las subastas de deuda.    
*  EL deslizamiento máximo que MakerDAO está dispuesto a aceptar durante las subastas, para asegurar que haya suficiente participación de los _keepers_

### Ejemplo

`Disminución de la Oferta Mínima (Flop)` = 5%


Si la oferta actual es de 10 MKR por 1000 DAI, la oferta siguiente debe ser de 9,5 MKR por 1000 DAI como máximo, o sea, una disminución del 5%.  

## Propósito

El parámetro de Disminución de la Oferta Mínima (_Flop_) permite a la Gobernanza de Maker asegurarse que los _keepers_ esten lo suficientemente incentivados como para ofertar en subastas de deuda.

## Contraparte

Una pequeña Disminución de la Oferta Mínima (_Flop_) ayuda a reducir el MKR acuñado en las subastas de deuda, ya que las ofertas estarán mas cerca del valor de mercado del MKR. Sin embargo, si la DOM (_Flop_) es muy baja, puede terminar disminuyendo la participación de los _keepers_ debido a que no habrán beneficios. Si en una subasta solo participa un _keeper_, puede implicar una pérdida significativa para el Protocolo de Maker y, potencialmente, para los poseedores de DAI.    

Una gran Disminución de la Oferta Mínima (_Flop_) asegura mayor participación de los _keepers_, ya que hay una oportunidad de obtener mayores ganancias. También ayuda a balancear otros costos para el _keeper_ cuando hace una oferta, como el efecto de la volatilidad del precio del MKR durante la subasta, así como el costo del _gas_ cuando se hace la oferta.  

## Cambios

Ajustar el parámetro de Disminución de la Oferta Mínima (_Flop_) es un proceso manual que requiere de un Voto Ejecutivo. Los cambios en la Disminución de la Oferta Mínima (_Flop_) están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué aumentar este parámetro?**

Este parámetro se debería aumentar para que incremente la participación de los _keepers_ en las subastas de deuda.

**¿Por qué reducir este parámetro?**

Este parámetro se debería reducir para que incremente la eficiencia de la subasta, es decir, el precio de oferta ganadora vs. el precio de mercado del MKR.

## Consideraciones

Que el costo del _gas_ active (`kick`) una Subasta de Deuda no es algo trivial. Si la Disminución de la Oferta Mínima (_Flop_) es muy baja, puede que, las Subastas de Deuda, no se activen por ningún _keeper_ ya que se les exige aceptar un costo fijo a cambio de un desenlace incierto.

El "_Front-running_" puede ser un problema para las Subastas de Deuda.
