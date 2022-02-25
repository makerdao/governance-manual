# Techo de Deuda Global

>**Alias:** Techo de Deuda Global  
>**Nombre del Parámetro:** `line`  
>**Contrato:** `Vat`  
>**Alcance:** System  
>**Documentos Técnicos:** [Enlace](https://docs.makerdao.com/smart-contract-modules/core-module/vat-detailed-documentation)  

## Descripción

El `Techo de Deuda Global` o `line`, es un parámetro que permite a la Gobernanza de Maker fijar una cantidad máxima de DAI que pueda ser acuñada por los usuarios del Protocolo de Maker. Si un usuario intenta acuñar DAI y el monto del nuevo DAI acuñado pondría la cantidad total de DAI por encima del `Techo Global de Deuda`, la transacción fallará y el DAI no será acuñado.

Adicionalmente, los tipos de _vault_ tienen un parámetro de Techo de Deuda que no será tratado en este artículo. Para que un usuario pueda acuñar DAI desde su vault, debe haber espacio disponible tanto en el Techo de Deuda de su vault, como también en el ´Techo de Deuda Global´.

## Propósito

El propósito del `Techo Global de Deuda` es el de actuar como un límite superior sobre la cantidad de DAI en circulación. En el caso de que una falla en otra parte del Protocolo de Maker diera como resultado la acuñación de DAI sin respaldo, el `Techo Global de Deuda` limitará la pérdida total.

## Contraparte

Si el `Techo Global de Deuda` es fijado muy bajo, impedirá que se acuñen DAI. Esto es una mala experiencia en todo sentido, puede afectar a los dueños de _vaults_ y también puede causar que el _peg_ del DAI rompa al alza si la demanda de DAI aumenta pero la oferta de DAI no puede incrementar.

Si el `Techo de la Deuda Global` es fijado demasiado alto, el Protocolo de Maker tendrá un incremento en sus pérdidas en caso de que un error o falla empiece a acuñar DAI sin respaldo.

## Cambios

Ajustar el parámetro de `Techo de Deuda Global` puede hacerse a través de un proceso manual que requiere de un Voto Ejecutivo. Los cambios en el `Techo de Deuda Global` están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

Por lo general, el `Techo de Deuda Global` no necesita ser manejado manualmente por la Gobernanza de Maker. La Core Unit de Ingeniería de Protocolos incluye modificaciones a los parámetros en las propuestas ejecutivas, de manera que sea igual a la suma aproximada de los techos de deuda de las _vaults_ individuales.

El `Techo Global de Deuda` también está ajustado automáticamente para tener en cuenta los cambios en el techo de deuda que ocurren a través del Módulo de Acceso Instantáneo al Techo de Deuda. Este Módulo de Acceso Instantáneo al Techo de Deuda permite que el techo de deuda de una _vault_ determinada se ajuste instantáneamente de acuerdo a ciertas reglas y parámetros codificados. Cuando esto ocurre, el `Techo de Deuda Global` cambiará por la misma cantidad.

## Consideraciones

En un Apagado de Emergencia, el DAI no puede ser acuñado independientemente del `Techo Global de Deuda`.

El `Techo Global de Deuda` no impedirá que el DAI se acumule en el Buffer de Excedente del Sistema por las tarifas de estabilidad. Por lo tanto, la oferta global de DAI puede seguir aumentando a pesar de que se haya alcanzado el `Techo Global de Deuda`.

La Gobernanza de Maker debe tener cuidado al reducir el techo de deuda de los tipos de colateral; ya que sin quererlo esto puede llevar a una situación donde el `Techo Global de Deuda` esté por debajo de la oferta total de DAI, impidiendo así que se acuñe más DAI.
