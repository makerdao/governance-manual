# Duración de Oferta (_Flop_)

>**Alias:** N/A  
>**Nombre del Parámetro:** `ttl`  
>**Contenido del Contrato:** `_Flop_`  
>**Alcance:** System  
>**Documentos Técnicos:** [Enlace](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/flop-detailed-documentation)  

## Descripción

El parámetro de Duración de Oferta (_Flop_) o `ttl` permite a la Gobernanza controlar la cantidad de tiempo que durará una Subasta de Deuda después de una oferta exitosa. Nuevas ofertas reinician el temporizador, extendiendo la subasta. Una Subasta de Deuda puede extenderse hasta un tiempo máximo establecido por el parámetro de Duración de Subasta (_Flop_), en el cual, la subasta terminará sin importar el Temporizador de Duración de Oferta.

Las Subastas de Deuda son usadas para recapitalizar el sistema, acuñando y subastando MKR por una cantidad fija de DAI. En este proceso, los _Keepers_ ofertan por la cantidad de MKR que están dispuestos a aceptar, a cambio de una cantidad fija de DAI que van a proporcionar.

### Ejemplo

`Duración de Oferta (Flop)` = 300 segundos  

`Duración de Subasta (Flop)` = 24 horas

1. Una Subasta de Deuda ha sido activada y pasaron 3 horas sin una sola oferta.
2. _Keeper A_ ofrece tomar 20 MKR a cambio de 100 DAI a las 3 horas.  
3. _Keeper B_ tiene 300 segundos para proponer una oferta más atractiva o, si no, _Keeper A_ ganará la subasta.  
4. _Keeper B_ ofrece tomar 19 MKR a cambio de 100 DAI, a las 23 horas y 59 minutos de haber iniciado la subasta.
5. _Keeper A_ tiene 60 segundos para proponer una oferta más atractiva o, si no, _Keeper B_ ganará la subasta.


## Propósito
Ajustar el parámetro de Duración de Oferta (_Flop_) permite a la Gobernanza de Maker minimizar el total de MKR acuñado, asegurando que haya suficiente competencia entre los _Keepers_.

## Contraparte

Cuando se oferta, los _Keepers_ toman el riesgo de que el precio del MKR-DAI cambie negativamente (para ellos) durante el transcurso de la subasta; si esto sucede, pueden perder dinero.

Una Duración de Oferta (_Flop_) corta significa que los _Keepers_ tienen menos riesgos de que el mercado se mueva durante el progreso de la subasta. Ya que el riesgo es menor, los _keepers_ pueden proponer ofertas más agresivas, que pueden terminar en menos MKR acuñado. Sin embargo, si la Duración de Oferta (_Flop_) es muy corta, puede que no haya suficiente tiempo para que los _keepers_ organicen los fondos y puedan participar en dichas subastas. En un caso extremo, una subasta con un solo participante, resultará en ofertas de MKR arbitrariamente altas y una pérdida de valor para el Protocolo de Maker.

Una Duración de Oferta (_Flop_) corta también aumenta el riesgo de una severa pérdida de valor en caso de congestión en la _blockchain_. El aumento en los precios del _gas_ puede bloquear a los _keepers_, ya sea por problemas técnicos o por el costo adicional del _gas_.  

Una Duración de Oferta (_Flop_) más larga, le da a los _keepers_ más tiempo de participar en la subasta, con lo que se espera alentar a un mayor número de participantes. Si la Duración de Oferta (_Flop_) es muy larga, puede haber ofertas por cantidades muy elevadas de MKR, para protegerse ante la volatilidad de precios durante el período de Duración de Oferta (_Flop_). Los precios de oferta realistas solo aparecerán cuando el final de la subasta (determinado por la Duración de Subasta) esté más cerca que el Período de Duración de Oferta (_Flop_). En situaciones donde el precio del MKR está cayendo, podría acuñarse más MKR que con una Oferta de Duración (_Flop_) más corta.

## Cambios

Ajustar el parámetro de Duración de Oferta (_Flop_) es un proceso manual que requiere de un Voto Ejecutivo. Los cambios en la Duración de Oferta (_Flop_) están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué aumentar este parámetro?**

La Gobernanza de Maker podría desear aumentar la Duración de Oferta (_Flop_) si muy pocos _keepers_ están participando en las Subastas de Deuda, para poder así fomentar una mayor participación. Esto también puede ocurrir si están preocupados por la congestión de la _blockchain_.

**¿Por qué reducir este parámetro?**

La Gobernanza de Maker podría considerar necesario que disminuya la Duración de Oferta (_Flop_), si los _keepers_ están proponiendo grandes ofertas debido a la volatilidad en los precios del MKR durante el período de la Duración de Oferta (_Flop_).

## Consideraciones

La Duración de Oferta (_Flop_) siempre está limitada por la duración total de la subasta. Si esta se fija por encima de la duración total de la subasta, entonces no tendrá ningún efecto.

### Ejemplo

`Duración de Oferta (_Flop_)` = 1 hora  

`Duración de Subasta (_Flop_)` = 30 minutos

La subasta solo durará 30 minutos, haciendo que la Duración de Oferta (_Flop_) sea irrelevante.

El parámetro de Duración de Oferta (_Flop_) cumple la misma función que este parámetro en las subastas de Excedentes.  

Inicialmente, se usaba un sistema similar para las subastas de colateral, que después fue reemplazado por el sistema de subasta holandesa.
