# Duración de Subasta (_Flop_)

>**Alias:** N/A  
>**Nombre del Parámetro :** `tau`  
>**Contenido del Contrato:** `_Flop_`  
>**Alcance:** Sistema
>**Documentos Técnicos:** [Enlace](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flop-detailed-documentation)  

## Descripción

El parámetro de Duración de Subasta (_Flop_) permite a la Gobernanza controlar el tiempo de vida máximo de una Subasta de Deuda. Una Subasta de Deuda puede terminar antes de este plazo máximo si el temporizador de la Duración de Oferta expira sin ninguna oferta adicional.

Las Subastas de Deuda se usan para recapitalizar al Protocolo de Maker, acuñando y subastando MKR por un monto fijo de DAI. En este proceso, los _keepers_ ofertan la cantidad de MKR que están dispuestos a aceptar a cambio de un monto fijo de DAI que van a proveer.

### Ejemplo

`Duración de Oferta (Flop)` = 300 segundos  
`Duración de Subasta (Flop)` = 24 horas  

1. Una Subasta de Deuda ha sido activada y pasaron 3 horas sin una sola oferta.
2. _Keeper A_ ofrece tomar 20 MKR a cambio de 100 DAI a las 3 horas.  
3. _Keeper B_ tiene 300 segundos para proponer una oferta más atractiva o, si no, _Keeper A_ ganará la subasta.  
4. _Keeper B_ ofrece tomar 19 MKR a cambio de 100 DAI a las 23 horas y 59 minutos de haber iniciado la subasta.
5. _Keeper A_ tiene 60 segundos para proponer una oferta más atractiva o, si no, _Keeper B_ ganará la subasta.


## Propósito

La Duración de Subasta (_Flop_) permite a la Gobernanza de Maker ajustar el plazo máximo para las Subastas de Deuda, para asegurar que los _keepers_ tenga una sólida participación. También ayuda a asegurar un plazo de tiempo predictivo para que el protocolo se recupere de un estado de sub-colateralización.

## Contraparte

La Duración de Subasta (_Flop_) mantiene un balance entre asegurar suficiente tiempo para que los _keepers_ puedan desplegar su capital y limitar su riesgo de mercado. Una Duración de Subasta (_Flop_) más larga, le da más tiempo a los _keepers_ de participar en las subastas. Una Duración de Subasta (_Flop_) más corta, significa que los _keepers_ tienen menos posibilidades de verse afectados por movimientos de precio negativos del Token MKR durante el proceso de subasta. El maximizar el número de participantes ofertando, hace que las subastas sean más eficientes y que menos MKR sea acuñado.

Sin embargo, una Duración de Subasta (_Flop_) que sea muy larga, podría resultar en una situación en la cual muchas subastas sucedan simultáneamente. Si la Duración de Subasta (_Flop_) es muy pequeña, entonces los _keepers_ quizá no tengan suficiente tiempo para organizar sus recursos y hacer las ofertas. Cualquiera de estas situaciones podría terminar en subastas ineficientes que aumenten la cantidad de MKR acuñado.

El parámetro también afectará en la cantidad de tiempo que tomará recapitalizar al Protocolo de Maker en un evento en el que el protocolo termina con deuda incobrable, lo que puede ser importante dependiendo de la severidad de la situación.  

## Cambios
Ajustar el parámetro de Duración de Subasta (_Flop_) es un proceso manual que requiere de un Voto Ejecutivo. Los cambios en la Duración de Subasta (_Flop_) están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza..

**¿Por qué aumentar este parámetro?**
La Gobernanza deMaker podría considerar aumentar la duración de Subasta (_Flop_) si muy pocos _keepers_ están participando en subastas de deuda, fomentando así una mayor participación.

**¿Por qué reducir este parámetro?**
La Gobernanza de Maker podría considerar necesario disminuir la duración de Subasta (_Flop_) si las subastas son tan largas que los _keepers_ casi siempre generan pérdidas. Si hay muchas subastas superpuestas, podrían desear disminuir este parámetro.

## Consideraciones
La Duración de Subasta (_Flop_) siempre está limitada por la Duración de Oferta (_Flop_), es decir, el período de tiempo antes de que termine una oferta. Si es fijada por debajo de la Duración de Oferta (_Flop_), hará que el parámetro sea innecesario, ya que la subasta terminará antes de que expire la oferta.

### Ejemplo

`Duración de Oferta (_Flop_)` = 1 hora  
`Duración de Subasta (_Flop_)` = 30 minutos

Esta subasta solo durará 30 minutos, haciendo que la Duración de Oferta (_Flop_) sea irrelevante.

El parámetro de duración de Subasta (_Flop_) cumple la misma función que este parámetro en la Subasta de Excedente.
