# Estabilidad de Paridad

>**Alias:** PSM  
>**Nombre del Contrato:** `DssPsm`  
>**Alcance:** cada PSM interactúa con un solo tipo de vault subyacente.  

## Descripción  

El Módulo de Estabilidad de Paridad le permite a los usuarios intercambiar un tipo de colateral determinado por DAI a una tasa fija, en vez de pedir prestado DAI. El contrato PSM fue diseñado pensando en un colateral de stablecoin, permitiendo a los usuarios intercambiar otras stablecoins por DAI a una tasa fija para ayudar a mantener el la paridad (`peg`) del DAI a 1 dólar.

El PSM opera de forma similar a un tipo de _vault_ regular con cero tarifas de estabilidad y un ratio de liquidación del 100% al que solo se puede acceder a través de un _smart contract_ por el usuario, que contiene las funciones de intercambio correspondientes. A diferencia de lo que ocurre con _vaults_ regulares, los usuarios de PSM no conservan la propiedad del activo y toman prestado DAI, sino que intercambian el activo directamente por DAI.

Por ejemplo, con un PSM respaldado por USDC, un usuario podría ser capaz de intercambiar 100 USDC por 100 DAI \(menos tarifas\) usando el PSM respaldado por USDC sin tomar ninguna deuda ni usar una _vault_ de Maker.

## Propósito

El contrato PSM fue creado principalmente para ayudar a mantener la paridad del DAI cerca de $1 durante el tiempo en que la demanda de DAI superaba la oferta de DAI.

Inicialmente, _vaults_ de stablecoins con un ratio de liquidación bajo fueron usados para este propósito, pero esta solución demostró ser muy difícil de administrar para la Gobernanza debido al riesgo de que las tarifas de estabilidad presionen a la _vaults_ por debajo del 100% del ratio de colateralización.

El contrato PSM permite a la Gobernanza cobrar las tarifas en stablecoins en el momento del intercambio, en lugar de hacerlo a lo largo del tiempo.

## Contrapartida

Un PSM genera el mismo peligro que las _vaults_ de stablecoins con bajos ratios de liquidación: el Protocolo de Maker asumirá una gran cantidad de colateral de stablecoin en los momentos en los que la demanda de DAI supere la oferta de DAI. Generalmente, esto se considera como un riesgo debido a la centralización de otras stablecoins y a la posibilidad de una acción regulatoria dirigida específicamente a Maker. El riesgo de una acción regulatoria podría ser ligeramente mayor con un PSM, debido a que el colateral stablecoin creado a través de un PSM es efectivamente propiedad del Protocolo de Maker, en lugar de ser propiedad del usuario que lo utilizó como colateral para el préstamo de DAI.

Adicionalmente, el Protocolo de Maker asume el riesgo de que la stablecoin colateral pierda su paridad \(aunque esto no es diferente de un tipo de _vault_ regular con colateral de stablecoin.\)

Por otro lado, un PSM ofrece diversas ventajas:

* Aumentar la estabilidad del DAI debido a la oportunidad de arbitraje instantánea cuando el precio del DAI difiere del precio del tipo de colateral subyacente al PSM.
* Las tarifas se cobran por adelantado en cada intercambio, ya sea hacia DAI o desde DAI. Dado que los PSM no tienen deslizamiento, es capaz de atraer un volumen de _trading_ respetable.
* No es necesario micro gestionar los parámetros \(a través de acciones de Gobernanza\) para asegurar que continúe funcionando, en contraste con _vaults_ de stablecoins con ratios bajos de liquidación.

## Parámetros Clave

En realidad, un PSM es solo un contrato _wrapper_ alrededor de un tipo de _vault_ privilegiado en el Protocolo de Maker. Todos los parámetros que se aplican a los tipos de _vault_ también aplican a los PSM. Sin embargo, un PSM de _stablecoin_ siempre debería tener una Tarifa de Estabilidad de 0% y un Ratio de Liquidación de 100%.

### Techo de Deuda \(line\)

El Techo de Deuda se refiere al monto máximo de deuda que el PSM puede acumular.

Ten en cuenta que a pesar de que los usuarios no tengan una deuda cuando usan el PSM para comerciar entre DAI y el activo de colateral, el Protocolo de Maker _sí_ acumula una deuda en DAI que está respaldada por los activos que los usuarios comercian en el PSM a cambio de DAI.  

### Tarifa de Entrada \(tin\)
El porcentaje de la tarifa que se aplica cuando se comercia el activo de colateral a cambio de DAI.

### Tarifa de salida \(tout\)

El porcentaje de la tarifa que se aplica cuando se comercia DAI en el PSM a cambio del activo de colateral.

## Interacción con el Usuario

Los usuarios pueden llamar a las funciones de intercambio directamente en un contrato PSM, pero se espera que los PSM se integren a los agregadores DEX de manera que se lleven a cabo los intercambios cuando un PSM pueda ofrecer el mejor precio del mercado.

## Consideraciones

Es importante tener en cuenta que la cantidad de operaciones que un PSM puede ofrecer está limitada por su Techo de Deuda y la cantidad de tokens de colateral depositados al momento. Un PSM no puede ofrecer comerciar DAI si su Techo de Deuda ha sido alcanzado. De la misma forma, un PSM no puede ofrecer comerciar ul activo de colateral si no hay tokens de colateral en el PSM.

Un PSM es un tipo de _vault_ regular con la excepción de que solo se puede acceder a él mediante un contrato _wrapper_ específico. El contrato _wrapper_ define las funciones de comercio para los usuarios y cobra las tarifas de comercio fijadas por la Gobernanza.

Un PSM solo es posible con un activo que tenga una estabilidad anclada al mismo activo que el DAI. Ofrecer intercambios 1 – 1 requiere un ratio de liquidación del 100%. Si se intenta un PSM con un activo no estable, se correrá el riesgo de que de que se vuelva sub-colateralizado tan pronto como el precio de mercado del activo de colateral disminuya.
