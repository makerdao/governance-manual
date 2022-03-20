# Duración de Oferta (Flap)

>**Alias:** N/A  
>**Parameter Name:** `ttl`  
>**Containing Contract:** `Flap`  
>**Scope:** System  
>**Technical Docs:** [link](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flap-detailed-documentation)  

## Descripción
El parámetro de Duración de Oferta (Flap) permite a la Gobernanza controlar que tan pronto puede termninar una Subasta de Excedentes luego de una oferta exitosa. Las próximas oferta reiniciarán este temporizador, extendiendo la subasta. Una Subasta de Excedentes puede extenderse hasta un tiempo máximo determinado por el parámetro de Duración de Subasta (Flap), momento en el cual la subasta finalizará independientemente del temporizador de Duración de Oferta.

Las Subastas de Excedentes se utilizan para subastar el excedente de DAI en lotes fijos por una oferta variable de MKR que, luego, es quemado. En este proceso, los _keepers_ ofertan por cuánto MKR están dispuestos a pagar por una cantidad fija de DAI.

### Ejemplo

`Bid Duration (Flap)` (_Duración de Oferta_) = 300 segundos  
`Auction Duration (Flap)` (_Duración de Subasta_) = 24 horas  

1. Una Subasta de Excedentes ha sido activada y han pasado 3 horas sin ninguna oferta.
2. El _keeper_ A ofrece dar 10 MKR a cambio de 100 DAI a las 3 horas.
3. El _keeper_ B tiene 300 segundos en el cual debe ofrecer una oferta más atractiva, sino, el _keeper_ A ganará la subasta.
4. El _keeper_ B ofrece dar 11 MKR a cambio de 100 DAI a las 23 horas y 59 minutos de transcurrida la subasta.
5. El _keeper_ A tiene 60 segundos en el cual debe ofrecer una oferta más atractiva, sino, el _keeper_ B ganará la subasta.

## Propósito

El ajustar el parámetro de Duración de Oferta (Flap), permite a la Gobernanza de Maker maximizar el total de MKR quemado al asegurar la competencia suficiente entre _Keepers_.

## Contraparte

Al ofertar, los _Keepers_ toman el riesgo de que el precio de MKR-DAI cambie negativamente (para ellos) durante la duración de la subasta; si esto pasa, ellos pueden perder dinero.

Una Duración de Oferta (Flap) pequeña significa que los _keepers_ tienen menos riesgo de que el mercado se mueva mientras la subasta se encuentre en progreso. Ya que el riesgo es bajo, los _keepers_ pueden realizar ofertas más agresivas lo cual puede resultar en más quema de MKR. Sin embargo, si la Duración de Oferta (Flap) es muy baja, tal vez no haya tiempo para que los _keepers_ organicen sus fondos y participen en tales subastas. En un caso extremo, una subasta con un solo postor resultará en ofertas arbitrarias de MKR y una pérdida de valor del Protocolo de Maker.

Una Duración de Oferta (Flap) pequeña también aumenta el riesgo de una pérdida de valor más severa en el caso de una congestión de _blockchain_. El elevar los precios del _gas_ puede bloquear a los _keepers_ debido a problemas técnicos o al costo fijo adicional del _gas_.

Una Duración de Oferta (Flap) más grande le da a los _keepers_ más tiempo para poder participar en las subasta, esperando que eso anime a un mayor número de postores a participar. Si la Duración de Oferta (Flap) es muy grande, puede haber ofertas por cantidades mínimas de MKR para protegerse contra la volatilidad de los precios durante el período de Duración de Oferta (Flap). Las ofertas con precios realistas solo aparecerán cuando el final de la subasta (determinado por la Duración de Subasta) esté más cerca que el período de Duración de Oferta (Flap). En situaciones en las que el precio de MKR esté cayendo, esto conduciría a que se queme menos MKR que con una Duración de Oferta (Flap) más pequeña.

## Cambios

El ajuste del parámetro de Duración de Oferta (Flap) es un proceso manual que requiere un Voto Ejecutivo. Los cambios al Duración de Oferta (Flap) están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar este parámetro?**
La Gobernanza de Maker puede desear incrementar la Duración de Oferta (Flap) si pocos _keepers_ están participando en las subastas de excedentes para incentivarlos para una mayor participación o si les preocupa una congestión de la _blockchain_.

**¿Por qué reducir este parámetro?**
La Gobernanza de Maker puede desear reducir la Duración de Oferta (Flap) si los _keepers_ están ofreciendo ofertas bajas dado a la volatilidad en el precio del MKR durante el período de Duración de Oferta (Flap).

## Consideraciones

La Duración de Oferta (Flap) siempre está limitada por la duración total de la subasta. Si se establece por encima de la duración total de la subasta, no tendrá efecto.

El parámetro de Duración de Oferta (Flop) cumple el mismo rol que este parámetro en las Subastas de Deuda.

Inicialmente, un sistema similar de subastas fue utilizado también para Subasta de Colaterales; este fue reemplazado por un sistema de subasta holandés.

---

[Texto Original](https://github.com/makerdao/governance-manual/edit/main/parameter-index/surplus-auction/param-bid-duration-flap.md)
