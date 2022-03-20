# Buffer de Excedentes del Sistema

>**Alias:** Buffer de Excedentes de Subasta  
>**Nombre del Parámetro:** `hump`  
>**Contrato:** `Vow`  
>**Alcance:** System  
>**Documentos Técnicos:** [link](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/vow-detailed-documentation)  

## Descripción

El Buffer de Excedentes del Sistema controla la cantidad máxima de DAI que el protocolo puede acumular de los ingresos de las _Stability Fees_ (Tarifas de Estabilidad) antes de que se activen las subastas FLAP. A medida que ingresan las _Stability Fees_, la cantidad total de DAI dentro del Buffer de Excedentes del Sistema se incrementará hasta alcanzar el `Buffer de Excedentes del Sistema (hump) + Tamaño del Lote de Excedentes (bump)`; en este punto una subasta FLAP puede ser activada y el DAI es subastado por MKR. Entonces este MKR comprado es quemado.

El Protocolo Maker sólo tiene un Buffer de Excedentes del Sistema y las _Stability Fees_ de todos los vaults se acumulan en él.

El Buffer de Excedentes del Sistema está expresado en términos absolutos, en vez de relativos, siendo 1,000,000 de DAI en vez del 1% del Total de Deuda de DAI.

## Propósito

En términos generales, cuando el Protocolo Maker hace dinero en DAI, se compra y quema MKR. Del mismo modo, cada vez que el sistema pierde dinero (_deuda incobrable_), acuña MKR, lo vende y compra DAI. El propósito principal del Buffer de Excedentes del Sistema es reducir la frecuencia con la que esto ocurre. Esto es beneficioso para el protocolo porque cada vez que una subasta se lleva a cabo (sea FLAP o FLOP), la subasta no es perfectamente eficiente y el protocolo pierde algún porcentaje del valor subastado.

Además de esto, el buffer provee una reserva de DAI que puede ser utilizada por la gobernanza para financiar las operaciones de los equipos de dominio y para pagar las tarifas de Oráculos sin necesidad de acuñar MKR.

## Contrapartida

Incrementar el Buffer de Excedentes del Sistema le permite al Protocolo Maker acumular mayores reservas de DAI antes de quemar MKR. Estas reservas más grandes proveen mayor seguridad al protocolo en caso de que suceda una _deuda incobrable_.

Sin embargo, mientras el buffer no esté lleno, no se llevan a cabo subastas FLAP y no se quema MKR. Esto significa que la Gobernanza Maker no es recompensada por sus esfuerzos durante este tiempo.

Adicionalmente, el DAI en el Buffer de Excedentes del Sistema no circula en el mercado. Esto significa que acumular grandes cantidades de DAI en el Buffer de Excedentes del Sistema pueden incrementar la presión en el _peg_ del DAI.

Por otro lado, mantener el Buffer de Excedentes del Sistema muy bajo significa que es más probable que se realicen subastas FLOP en caso de _deudas incobrables_. Esto hace que sea más probable que la oferta de MKR aumente y diluya el valor de los Poseedores de MKR actuales.

## Cambios

Ajustar los parámetros del Buffer de Excedentes del Sistema es un proceso manual y requiere un Voto Ejecutivo. Los cambios al Buffer de Excedentes del Sistema están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.


**¿Por qué incrementar este parámetro?**

La razón principal para que incremente el Buffer de Excedentes del Sistema es; si se considera que necesario más excedentes para minimizar el riesgo de acuñar MKR, en caso de que algún evento del mercado lleve a una _deuda incobrable_. En general, mientras mayor sea la deuda total en DAI, mayor debe ser el Buffer de Excedentes del Sistema para balancear el riesgo de colaterales volátiles.

Otra razón para incrementar el Buffer de Excedentes del Sistema es si, por el motivo que fuere, sea beneficioso para prevenir la quema de MKR por un período de tiempo.

**¿Por qué disminuir este parámetro?**

La razón principal para la disminución del Buffer de Excedentes del Sistema, cuando está lleno sería en caso de que la Gobernanza desee utilizar el DAI actualmente en el buffer para comprar o quemar MKR. Alternativamente, si el buffer no estuviese lleno, la Gobernanza puede elegir disminuir el buffer, para reiniciar la quema continua de MKR que surge del desbordamiento.

Otra razón para disminuir el buffer puede ser que el riesgo del _portfolio_ de colaterales disminuya, ya sea debido a una reducción de deuda en DAI en todos los _vaults_ o que el _portfolio_ de colaterales que respalda el DAI se vuelva más estable y menos riesgoso que el promedio.

## Consideraciones

Se debe tener cuidado al momento de disminuir los parámetros, cuando el Buffer de Excedentes del Sistema esté lleno. Disminuir el tamaño del buffer activará las subastas FLAP por la cantidad de DAI pendiente que ya no entrará dentro del nuevo buffer. Mucha cantidad de subastas FLAP al mismo tiempo pueden abrumar a los _keepers_ de las subastas y resultar en la compra de MKR a precios más altos en la subasta.

Si el Cierre de Emergencia es activado, el DAI dentro del Buffer de Excedentes del Sistema es destruido y el colateral que lo respalda se reembolsa proporcionalmente a otros Poseedores de DAI. Esto significa que el DAI en el Buffer de Excedentes del Sistema puede ser descontado, en términos de la cantidad total de DAI que necesita ser respaldado por un colateral.

El DAI puede ser retirado del Protocolo Maker, a través de la Gobernanza Maker, utilizando el método `suck` como parte de un Voto Ejecutivo. El DAI 'succionado' del protocolo de esta forma será deducido del Buffer de Excedentes del Sistema y activará el acuñamiento de MKR si el DAI 'succionado' excede al DAI en el Buffer de Excedentes del Sistema.
