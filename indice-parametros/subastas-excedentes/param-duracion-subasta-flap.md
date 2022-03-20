# Duración de Subasta (Flap)

>**Alias:** N/A  
>**Parameter Name:** `tau`  
>**Containing Contract:** `Flap`  
>**Scope:** System  
>**Technical Docs:** [link](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flap-detailed-documentation)  


## Descripción

El parámetro de Duración de Subasta (Flap) permite a la Gobernanza controlar el tiempo de vida máximo de una Subasta de Excedentes. Una Subasta de Excedentes puede terminar antes de esta duración máxima si el temporizador de la Duración de Oferta caduca sin ninguna oferta adicional.

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

El parámetro de Duración de Subasta (Flap) permite a la Gobernanza de Maker ajustar la duración máxima de una subasta de excedentes para asegurar una robusta participación por parte de los _keepers_.

## Contraparte

La Duración de Subasta (Flap) hace un compromiso entre garantizar suficiente tiempo para que los _keepers_ desplieguen su capital y limitar su riesgo de mercado. Una mayor Duración de Subasta (Flap) le da a los _keepers_ más tiempo para participar en las subastas. Una Duración de Subasta (Flap) más pequeña significa que es menos probable que los _keepers_ se vean afectados por los movimientos negativos de los precios del token MKR durante el proceso de la subasta. El maximizar la cantidad de postores que participen da como resultado subastas más eficientes y más MKR quemados.

Sin embargo, una Duración de Subasta (Flap) mayor podría resultar en una situación en la que se realizan muchas subastas simultáneamente. Si la Duración de Subasta (Flap) es demasiado pequeña, es posible que los _keepers_ no tengan suficiente tiempo para organizar sus recursos y hacer ofertas. Cualquiera de estas situaciones podría resultar en subastas ineficientes que reduzcan la cantidad de MKR que se pueda quemar.


## Cambios

El ajuste del parámetro de Duración de Subasta (Flap) es un proceso manual que requiere un Voto Ejecutivo. Los cambios al Duración de Subasta (Flap) están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar este parámetro?**
La Gobernanza de Maker puede desear incrementar la Duración de Subasta (Flap) si pocos _keepers_ están participando en las subastas de excedentes para incentivarlos para una mayor participación.

**¿Por qué reducir este parámetro?**
La Gobernanza de Maker puede desear reducir la Duración de Subasta (Flap) si las subastas son tan largas que los _keepers_ casi siempre tienen pérdidas. Además, si hay demasiadas subastas superpuestas, puede ser conveniente disminuir este parámetro.

## Consideraciones

La Duración de Subasta (Flap) siempre está limitada por la Duración de Oferta (Flap), es decir, el período de tiempo antes del cual vence una oferta. Si se establece en un valor inferior a la Duración de Oferta (Flap), hará que este parámetro sea innecesario ya que la subasta terminará antes de que expire la oferta.

Por ejemplo, si la Duración de la Oferta (Flap) es de 1 hora y la Duración de Subasta (Flap) es de 30 minutos, entonces la subasta solo durará 30 minutos, haciendo que la Duración de Oferta (Flap) sea irrelevante.

---

[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/surplus-auction/param-auction-duration-flap.md)
