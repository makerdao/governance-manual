# Depósito Directo de Dai

>**Alias:** D3M, DDM, Direct DAI Deposit  
>**Nombre del Contrato:** `DssDirectDeposit`  
>**Alcance:** Un contrato DssDirectDeposit por objetivo de depósito.  
>**Documentos Técnicos:** TBD  

## Descripción

El Módulo de Depósito Directo de Dai (D3M) permite que el DAI sea acuñado y depositado en otros protocolos cripto de préstamos en la _blockchain_ (cadena de bloques) de Ethereum a cambio de un token depositado/colateralizado proveniente de ese protocolo de préstamos.  

En esencia, esto permite a Maker distribuir de forma indirecta DAI recién acuñado mediante otros protocolos de préstamo, asegurando que el DAI se mantenga totalmente respaldado.

Por ejemplo, el D3M de Aave deposita DAI dentro del Protocolo Aave a cambio de tokens aDAI que representan depósitos en Aave. Los Tokens aDAI luego son usados como colateral en contra del DAI acuñado.

Efectivamente, esto significa que el colateral depositado por los usuarios de Aave para pedir prestado DAI, es indirectamente usado para mantener el respaldo del DAI en el Protocolo Maker.

## Propósito

El propósito principal del D3M es ampliar el alcance del DAI como _stablecoin_, proveyendo DAI directamente a otros protocolos de préstamos. Adicionalmente, permite al Protocolo de Maker obtener un rendimiento sobre el DAI depositado en estos protocolos, proporcionando una fuente ingresos.

Además, permite a Maker subcotizar stablecoins centralizadas en estos Protocolos de Préstamos.  Al proveer DAI directamente en otros Protocolos de Préstamos, Maker puede asegurar que la Tasa de Préstamo de DAI en estos protocolos esté casi siempre por debajo de la Tasa de Préstamo de las _stablecoins_ centralizadas.

Finalmente, es probable que el módulo D3M se active durante mercados volátiles, ya que las tasas de préstamos en estos protocolos también tienden a fluctuar fuértemente durante esos períodos. El Módulo les garantiza a los usuarios de DAI que están el protocolo de préstamo que las tasas para prestar/pedir prestado se mantengan predecibles, haciendo que el DAI sea una mejor opción que otras _stablecoins_.


## Parámetros Clave

### Techo de Deuda (line)

El parámetro de Techo de Deuda para el Módulo de Depósito Directo de Dai es sustancialmente idéntico al parámetro de Techo de Deuda para los tipos de _vaults_. Controla la máxima cantidad de DAI que puede ser acuñada mediante el D3M. Un Techo de Deuda D3M también puede ser controlado por el Módulo de Acceso Instantáneo al Techo de Deuda.

### Tasa de Préstamo Objetivo (bar)

La Tasa de Préstamo Objetivo permite a la Gobernanza de Maker fijar la tasa 'ideal' para pedir prestado DAI en el protocolo de préstamo objetivo. Esto se logra añadiendo o removiendo una cantidad de DAI del protocolo de préstamos de manera que la Tasa de Préstamo en el protocolo objetivo se vuelva igual a la Tasa de Préstamo Objetivo (siempre que la restricción del Techo de Deuda lo permita).

Si la tasa de interés del préstamo en el protocolo objetivo de préstamos es más alta que la Tasa de Préstamo objetivo y el techo de deuda aún no ha sido alcanzado, entonces el módulo acuña y deposita DAI adicional dentro del protocolo de préstamos a cambio de tokens depositados.    

Por el contrario, si la tasa de interés del préstamo en el protocolo objetivo de préstamos es más baja que la Tasa de Préstamo y el módulo tiene una cantidad no nula de tokens depositados, entonces el contrato devuelve los tokens depositados al protocolo de préstamos a cambio de DAI, que posteriormente es quemado.

La función para activar este mecanismo no necesita permisos y es llamada por _bots_  que maneja MakerDAO a intervalos regulares.

## Meta-Parámetros

Los meta-parámetros son parámetros que no existen directamente en un _smart contract_ (en este caso el contrato DssDirectDeposit) pero son parámetros que la Gobernanza de Maker utiliza para determinar reglas generales acerca de cómo establecer parámetros actuales.   

### Participación Máxima


El meta-parámetro de Participación Máxima se refiere a la cuota máxima proporcional de tokens depositados que MakerDAO espera _holdear_ para un protocolo objetivo de préstamos. Este parámetro es expresado en términos de porcentaje y es utilizado para calcular el parámetro de Techo de Deuda.

Una participación máxima del 100% podría indicar que MakerDAO está dispuesto a ser el único que proporcione DAI al protocolo objetivo de préstamos.

Una participación máxima de 30% indicaría que MakerDAO esta dispuesto a proveer el 30% del total de DAI al protocolo objetivo de préstamos, mientras que el 70% seria proporcionado por otros usuarios o protocolos.

###  _Spread_

El meta-parámetro de _Spread_ se refiere a la diferencia entre la Tasa de Préstamo _efectivo_ para DAI en el protocolo objetivo de préstamos y la tarifa de estabilidad del Protocolo Maker en ETH-A. Esto es usado para calcular el parámetro de la Tasa de Préstamo objetivo. El propósito de este parámetro es que la Gobernanza Maker sea capaz de decidir si debería ser más económico o más costoso prestar DAI en el protocolo objetivo de préstamos en comparación con el Protocolo Maker.   

La Tarifa de Estabilidad del ETH-A es utilizada como un _proxy_ para el costo de prestar DAI usando el Protocolo de Maker, ya que tradicionalmente ha sido el tipo de _vault_ no-PSM más grande en Maker.

El _Spread_ es descrito como una tasa de porcentaje anual. Una distribución del 0% indica que el costo de prestar DAI en el protocolo objetivo de préstamos debería ser igual al costo de prestar DAI en un tipo de _vault_ de ETH-A a lo largo de un año.

Una _Spread_ de -0.5% indica que el costo de pedir prestado DAI en el protocolo objetivo de préstamos debería ser 0.5% más barato que en el Protocolo de Maker a lo largo de un año.

Un _Spread_ de 0.5% indica que el costo de pedir prestado DAI en el protocolo objetivo de préstamos debería ser 0.5% más caro que en el Protocolo de Maker a lo largo de un año.

La Tasa de Préstamo _efectiva_ para DAI en el protocolo objetivo de préstamos se ve afectada en ocasiones por las recompensas que ofrece el protocolo de préstamos en cuestión. Por ejemplo, los usuarios reciben recompensas de préstamo (por tomar prestado DAI) y recompensas de suministro (por suministrar colateral) en varios protocolos de préstamos.

### Fórmulas

La Tasa de Préstamo Objetivo está fijada de la siguiente manera:

`` Tasa de Préstamo Objetivo = Tasa ETH-A (Maker) + Recompensas de Préstamo en DAI (Protocolo Objetivo ) + 2 x Recompensas de Suministro de ETH (Protocolo Objetivo) + _Spread_``

Las recompensas de suministro están doblemente basadas en la presunción de que los prestatarios de DAI mantienen un 200% de ratio de colateralización en el protocolo objetivo.

El Techo de Deuda esta fijado de la siguiente manera:

``Techo de Deuda = Participación Máxima * Suministro de DAI Total (Plataforma)``

## Contrapartida

Un valor de distribución más positivo y, en consecuencia, una meta más alta resultaría en menos préstamos o endeudamiento (_borrowing_) en el protocolo de prestamos mediante el D3M y por lo tanto se reducirían las ganancias de Maker por parte del D3M. Sin embargo, esto podría resultar en un incremento potencial del uso de la propia _vault_ de Maker y así obtener mayores ingresos de dichas _vaults_. Un valor de _Spread_ más negativo resulta en mayores ingresos por parte del módulo D3M y potencialmente menores ingresos de las _vaults_.

Un Techo de Deuda D3M más alto resulta en ingresos potencialmente más altos por parte del módulo D3M y la capacidad de atender los picos de demanda de DAI, pero también puede resultar en mayor riesgo de crédito para Maker en caso de que el protocolo objetivo de préstamos sufra perdidas. Por el contrario, un techo de deuda D3M bajo disminuye el riesgo de crédito para Maker, pero también disminuye los potenciales ingresos por parte del módulo D3M y reduce la capacidad de atender los picos de demanda por DAI.

## Consideraciones

Debido a que los protocolos de préstamos ofrecen recompensas por _farmear_ tokens nativos (como por ejemplo stkAAVE en Aave), el módulo D3M genera ganancias adicionales en ese token nativo. Queda de parte de la Gobernanza si se decide _holdear_ los ingresos provenientes de las recompensas en tokens nativos que se obtuvieron _farmeando_ o si se decide convertirlos en DAI y agregarlos al Buffer de Excedentes. Por defecto, las recompensas se mantienen en el token nativo.  

El suministro de DAI en el protocolo de préstamos puede que no siempre refleje los parámetros establecidos. Por ejemplo, una gran disminución en el parámetro `line` puede requerir tiempo para que surta efecto debido a los problemas de liquidez al cambiar el token por DAI. De forma similar, el DAI suministrado por el modulo puede exceder temporalmente la participación máxima si el DAI suministrado por otros usuarios en el protocolo disminuye rápidamente.

Mientras el módulo D3M pueda ser llamado por cualquier persona, la _Core Unit_ de Tech-Ops de MakerDAO maneja un _bot_ que llama al modulo si la Tasa de Préstamo objetivo y la tasa actual en el protocolo de préstamos divergen en algún umbral. Este umbral es manejado por la _Core Unit_ de Tech-Ops con asesoramiento de la _Core Unit_ de Ingeniería de Protocolos. El umbral es escogido de tal manera que las tasas se mantienen cerca de la tasa objetivo, pero el número de llamadas al módulo no es muy alto, ya que cada llamada implicas costos de gas.

Los préstamos recursivos son comunes en protocolos de préstamos debido al _yield farming_ (agricultura de rendimiento). Aquí es donde un usuario deposita DAI como colateral, pide prestado DAI del protocolo y deposita el DAI prestado de nuevo en el protocolo. El bucle recursivo puede repetirse varias veces e inflar el suministro total de DAI. El cálculo de la participación máxima para el techo de deuda D3M solo toma en cuenta el suministro real de DAI sin el préstamo recursivo.
