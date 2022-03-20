# Incremento Mínimo de Oferta (Flap)

>**Alias:** N/A  
>**Parameter Name:** `beg`  
>**Containing Contract:** `Flap`  
>**Scope:** System  
>**Technical Docs:** [link](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flap-detailed-documentation)  

## Descripción
Durante las subastas de excedentes, el excedente de DAI en el sistema será subastado por MKR en lotes fijos. En este proceso, los _keepers_ ofertan cantidades crecientes de MKR por una cantidad fija de DAI. El MKR recibido de esta manera es quemado por el Protocolo de Maker.

Las nuevas ofertas de MKR deben superar la oferta actual de MKR por, al menos, un monto determinado por el Incremento Mínimo de Oferta (Flap) o `beg`. El Incremento Mínimo de Oferta (Flap) se expresa en términos de un porcentaje mínimo de aumento de la oferta actual.

En la práctica, el Incremento Mínimo de Oferta (Flap) representa:
* La ganancia máxima que los _keepers_ pueden generar al ofertar en Subastas de Excedentes.
* El desliz máximo durante una subasta que MakerDAO está dispuesto a aceptar para asegurar una participación suficiente de _keepers_.

### Ejemplo

`Min Bid Increase (Flap)` (_Incremento Mínimo de Oferta_) = 5%

Si la oferta ganadora actual es 10 MKR por 1000 DAI, la próxima oferta debe de ser de al menos 10,5 MKR por 1000 DAI, un incremento del 5%.

## Propósito
El parámetro de Incremento Mínimo de Oferta (Flap) permite a la Gobernanza de Maker asegurar que los _keepers_ se encuentren lo suficientemente motivados para ofertar en las subastas de excedentes.

## Contraparte
Un Incremento Mínimo de Oferta (Flap) bajo ayuda a incrementar el monto quemado de MKR ya que las ofertas estarán más cerca del valor del mercado de MKR. Sin embargo, si es demasiado bajo, puede resultar en una baja participación de los _keepers_ debido a la falta de ganancias percibidas. Si solo un _keeper_ participa en una subasta, esto puede generar pérdidas significativas para el Protocolo de Maker.

Un Incremento Mínimo de Oferta (Flap) alto asegura una participación alta de los _keepers_ ya que hay una gran oportunidad de percibir una ganancia mucho más grande. También ayuda a los _keepers_ a balancear otros costos cuando ofertan, tales como el efecto de la volatilidad del precio de MKR durante la duración de la subasta y el costo del _gas_ al hacer una oferta.

## Cambios
El ajuste del parámetro de Incremento Mínimo de Oferta (Flap) es un proceso manual que requiere un Voto Ejecutivo. Los cambios al Incremento Mínimo de Oferta (Flap) están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar este parámetro?**

Este párametro debería incrementarse para aumentar la participación de _keepers_ en las subastas de excedentes.

**¿Por qué reducir este parámetro?**

Este parámetro debería reducirse para incrementar la eficiencia de las subastas. Por ejemplo: precio de la oferta ganadora vs. precio de mercado del MKR.

## Consideraciones
El costo de _gas_ para activar (`kick`) una subasta de excedentes no es trivial. Si el Incremento Mínimo de Oferta (Flap) es muy bajo, puede que las subastas de excedentes no sean activadas por ningún _keeper_ porque ellos se encuentran obligados a aceptar un costo fijo por un desenlace incierto.

Las "ejecuciones anticipadas" pueden ser un problema en las subastas de excedentes.

---

[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/surplus-auction/param-min-bid-increase-flap.md)
