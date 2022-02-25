# Tarifa de Estabilidad  

>**Alias:** N/A  
>**Nombre del Parámetro:** `duty`  
>**Contenido del Contrato:** `Contrato`  
>**Alcance:** Tipo de Vault (Ilk)  
>**Documentos Técnicos:** [Enlace](https://docs.makerdao.com/smart-contract-modules/rates-module/jug-detailed-documentation)  

## Descripción

El parámetro de la Tarifa de Estabilidad es una tarifa porcentual anual que se cobra sobre el DAI generado en los vaults. Se expresa como un rendimiento porcentual anual, pero se cobra por bloque en DAI. A su vez, el DAI proveniente de esta tarifa es minteado, agregado a la deuda en DAI de la vault y luego transferido al buffer de excedentes que esta bajo el control de la Gobernanza de Maker.

Cada tipo de vault tiene su propia Tarifa de Estabilidad que puede ser ajustada por la Gobernanza de Maker. Nótese que la tarifa de estabilidad se aplica colectivamente a todas las vaults creadas, usando un tipo específico de vault.

Por ejemplo, una vault con una deuda de 100 DAI usando un tipo de vault con una Tarifa de Estabilidad del 4% debería pagar 104 DAI después de un año (asumiendo que la Tarifa de Estabilidad se mantenga a un 4% durante el año).

## Propósito

El propósito principal de la Tarifa de Estabilidad es compensar al Protocolo de Maker por los riesgos asumidos al exponerse a los cambios de precio de la colateral usada para respaldar el DAI generado.

La Tasa de Estabilidad es también la mayor fuente de ingresos del Protocolo de Maker y se espera que sea usada para:

* Pagar por los gastos operativos de funcionamiento y crecimiento del Protocolo de Maker.
* Pagar por el funcionamiento de los mecanismos de alimentación de Oráculos.
* Comprar y quemar MKR para removerlo del suministro total, compensando así de forma indirecta a la Gobernanza por el funcionamiento del Protocolo de Maker y actuar como un prestamista de último recurso.

## Contrapartida

En teoría, modificar la Tarifa de Estabilidad de un tipo de vault impactar en el número de usuarios que estén dispuestos a usar dicho tipo de vault, con aumentos que den como resultado una reducción en la cantidad de DAI generado y a su vez, disminuciones que terminen aumentando la cantidad de DAI.

Sin embargo, está abierto a debate que tanto efecto tiene la modificación de una Tarifa de Estabilidad sobre el comportamiento del usuario. Otros factores más importantes influyen en la decisión de los usuarios de mantener una vault, incluyendo las condiciones del mercado y el panorama competitivo.

En la práctica, grandes cambios en la Tasa de Estabilidad han tenido efectos mensurables en el comportamiento de los usuarios, mientras que el impacto de pequeños cambios es menos claro.

Las Tarifas de Estabilidad altas pueden aumentar los ingresos de forma temporal o permanente para un tipo particular de vault, dependiendo de cómo sea la respuesta del usuario ante el cambio en la Tarifa de Estabilidad.

Del mismo modo, una Tasa de Estabilidad baja puede disminuir los ingresos de un tipo particular de vault de forma temporal o permanente, dependiendo también de como sea la respuesta del usuario ante el cambio de la Tasa de Estabilidad.

## Cambios

Ajustar la Tarifa de Estabilidad es un proceso manual que requiere de un Voto Ejecutivo. Los cambios en los parámetros de Tarifa de Estabilidad están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza

La Gobernanza de Maker le ha otorgado al Grupo de Trabajo de Tasas la facultad de proponer cambios en las tasas basándose en la política monetaria, el riesgo y los panoramas competitivos. En el foro de la Gobernanza de Maker se pueden encontrar las operaciones, membresías y propuestas históricas de este grupo.

**¿Por qué aumentar un parámetro de Tarifa de Estabilidad?**

La razón principal de aumentar la Tarifa de Estabilidad es por una de las políticas monetarias. Si el precio del DAI es menor que $1, esto indica que el suministro del DAI debe reducirse. La Tarifa de Estabilidad es usualmente el primer parámetro que la Gobernanza toma en consideración si el suministro del DAI necesita ser reducido.

Por otro lado, se puede incrementar una Tarifa de Estabilidad para un tipo de vault si la Gobernanza de Maker no considera que el protocolo está siendo compensado adecuadamente por el riesgo de ese tipo de vault en particular.

También, puede aumentarse una Tarifa de Estabilidad si la Gobernanza de Maker determina que necesita capital adicional para operar o crecer de manera efectiva y no considere que un aumento en la Tarifa de Estabilidad afecte negativamente al peg del DAI.

Por último, se puede incrementar una Tarifa de Estabilidad si no hay competidores viables que ofrezcan tasas más bajas que las del Protocolo de Maker y que la Gobernanza considere que se pueden cobrar comisiones más altas sin que esto impacte negativamente al peg del DAI.

**¿Por qué disminuir un parámetro de Tarifa de Estabilidad?**

La razón principal para disminuir una Tarifa de Estabilidad también es por una de las políticas monetarias. Si el precio del DAI es mayor a $1, esto indica que el suminitro del DAI debería ser aumentado. La Tarifa de Estabilidad es usualmente el primer parámetro que la Gobernanza toma en consideración si el suministro del DAI necesita ser aumentado.

Por otro lado, una Tarifa de Estabilidad para un tipo de vault puede ser disminuida si la Gobernanza de Maker considera que el nivel de riesgo proveniente de ese tipo de vault ha disminuido.

Por último, la Tarifa de Estabilidad puede ser disminuida si los competidores ofrecen tasas más bajas que el Protocolo de Maker y la Gobernanza desea conservar o aumentar su cuota de mercado.

## Consideraciones

El parámetro de la Tarifa de Estabilidad tiene un límite del 0%, este no puede ser negativo.

En ausencia de una gestión activa por parte del dueño de una vault, la acumulación de Tarifas de Estabilidad puede empujar la colateralización de una vault por debajo del ratio de liquidación, lo que generará que sea liquidada.

También existe un parámetro de Tarifa de Estabilidad Global dentro del Protocolo de Maker. En la práctica, esta no ha sido utilizada porque aumenta de forma innecesaria la complejidad del proceso de la Gobernanza y el cálculo de la Tarifa de Estabilidad.

Antes de la introducción del Grupo de Trabajo de Tasas, las Tarifas de Estabilidad se componían de Primas de Riesgo y de una Tasa Base votada por la Gobernanza.
