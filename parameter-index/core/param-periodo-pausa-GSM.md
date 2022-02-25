# Período de Pausa del Módulo de Seguridad de la Gobernanza

>**Alias:** GSM, Pause, Governance Security Delay  
>**Nombre del Parámetro:** `Pause_delay`  
>**Contrato:** `Pause`  
>**Alcance:** System  
>**Documentos Técnicos:** [enlace](https://docs.makerdao.com/smart-contract-modules/governance-module/pause-detailed-documentation)

## Descripción

El Período de Pausa del Módulo de Seguridad de la Gobernanza establece la cantidad mínima de tiempo en la que los cambios entrarán en vigencia en el Protocolo Maker luego de que un Voto Ejecutivo haya sido aprobado. Una vez que un _spell_ ejecutivo es aprobado, el módulo del Período de Pausa debe ser aprobado antes de que los cambios dentro del _spell_ ejecutivo puedan afectar al Protocolo Maker. El Protocolo sólo tiene un módulo de Período de Pausa y todos los cambios de parámetros están sujetos al mismo.

Es posible mover la funcionalidad fuera del módulo de Período de Pausa, sin embargo, esto requiere trabajo de ingeniería adicional. Esto ha ocurrido en el pasado, se ha habilitado la funcionalidad que le permitió a la Gobernanza de Maker congelar o descongelar los precios de los oráculos, así como congelar o descongelar las liquidaciones sin esperar el lapso de la demora.

El Período de Pausa del Módulo de Seguridad de la Gobernanza usualmente es expresado en forma de horas.

## Propósito

Este parámetro existe, principalmente, para proteger a los usuarios del Protocolo Maker de un ataque a la Gobernanza por parte de Poseedores de MKR maliciosos. En el caso de que una propuesta maliciosa sea aprobada a través de la Gobernanza, los Poseedores de DAI y usuarios de _vaults_ tendrán la oportunidad de vender sus DAI o cerrar sus _vaults_ antes de que los cambios sean activados en el Protocolo Maker. Adicionalmente, esto le da a una minoría de Poseedores de  MKR la oportunidad de cancelar los cambios maliciosos o apagar el Protocolo Maker haciendo uso del Módulo de Apagado de Emergencia.

También les da a los usuarios la oportunidad de salirse del protocolo en el caso de que haya cambios que no sean maliciosos, pero con los que no se estén de acuerdo.

## Contrapartida

El Período de Pausa del Módulo de Seguridad de la Gobernanza le da más tiempo a los Poseedores de MKR no maliciosos y a los usuarios del protocolo para notar y reaccionar ante ataques al Protocolo. También les proporciona tiempo adicional a los usuarios para salirse en caso de que suceda algo no malicioso, pero con lo que no estén de acuerdo, como un incremento en los Ratios de Liquidez que pueda causar la liquidación del _Vault_ del usuario.

Sin embargo, tener un Período de Pausa más largo también impone un tiempo de reacción más lento en toda la Gobernanza Maker, lo que genera riesgo en el caso de una emergencia en la que el tiempo sea de vital importancia:

* Volatilidad extrema del mercado.
* Problemas técnicos en el Protocolo Maker.
* Ataque a los Oráculos.
* Congestión extrema en la red.

Cualquiera de las situaciones expresadas arriba puede requerir una acción rápida por parte de la Gobernanza, sin embargo, aún la respuesta más rápida requiere que el Período de Pausa del Módulo de Seguridad de la Gobernanza sea aprobado antes de que los cambios sean activados en el Protocolo Maker.

## Cambios

Ajustar El Período de Pausa del Módulo de Seguridad de la Gobernanza es un proceso manual que requiere un Voto Ejecutivo. Los cambios al Período de Pausa del Módulo de Seguridad de la Gobernanza están sujetos al pre-cambio del Período de Pausa del Módulo de Seguridad de la Gobernanza.

**¿Por qué incrementar este parámetro?**

Se debe tener en cuenta un incremento en el Período de Pausa del Módulo de Seguridad de la Gobernanza si se considera que hay un alto riesgo de ataque a la Gobernanza, por el motivo que fuere. En el pasado, el Período de Pausa ha sido incrementada debido al riesgo de los préstamos rápidos, combinado con el aumento de la liquidez del token MKR en el mercado abierto.

**¿Por qué disminuir este parámetro?**

Si en un futuro cercano, se considera pertinente tomar acciones de Gobernanza urgentes, se debe tener en cuenta disminuir este parámetro. Por ejemplo, si se espera un comportamiento extremadamente volátil por parte del mercado, puede ser beneficioso reducir el Período de Pausa del Módulo de Seguridad de la Gobernanza temporalmente para permitir que la Gobernanza tenga una mejor reacción antes las condiciones cambiantes.

Una disminución también puede ser considerada si el riesgo de ataque a la Gobernanza ha demostrado ser mínimo.

Probablemente no sea recomendable reducir el Período de Pausa a cero permanentemente, porque dejaría al Protocolo Maker expuesto a ataques en contra de la Gobernanza.

## Consideraciones

La mayor consideración a tener en cuenta cuando se configura este parámetro es: cuánto tiempo es requerido para juntar una cantidad suficiente de MKR y poder así cancelar una propuesta de Gobernanza maliciosa en caso de un ataque a la Gobernanza.

En caso de que una vulnerabilidad técnica sea descubierta y divulgada responsablemente al Equipo de Dominio de Contratos Inteligentes de MakerDAO, puede ser utilizado el mecanismo _dark-spell_ para arreglar el _exploit_. El mecanismo _dark-spell_ fue presentado para ayudar a mitigar el riesgo de que se realicen arreglos técnicos en el protocolo, mientras está sujeto al Período de Pausa del Módulo de Seguridad de la Gobernanza. Si un arreglo técnico a una vulnerabilidad crítica no es activado inmediatamente, la vulnerabilidad puede explotar antes de que el arreglo sea efectivo.

El Período de Pausa del Módulo de Seguridad de la Gobernanza no aplica al Módulo de Apagado de Emergencia, el cual puede ser activado en cualquier momento por una minoría actualmente fijada en 50,000 MKR.

El Período de Pausa del Módulo de Seguridad de la Gobernanza no aplica a los _'cancel' spells_ (_spells_ ejecutivos que cancelan un Voto Ejecutivo existente que haya sido aprobado, pero esté esperando que expire el Período de Pausa del Módulo de Seguridad de la Gobernanza antes de ser activado).
