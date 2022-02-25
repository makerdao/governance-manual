# Tasa de Ahorro de DAI

>**Alias:** DSR  
>**Nombre del Parámetro:** `Pot_dsr`  
>**Contrato:** `Pot`  
>**Alcance:** Sistema
>**Documentos Técnicos:** [Enlace](https://docs.makerdao.com/mcd-developer-guides/developer-guides-and-tutorials#dai-savings-rate-dsr)  

## Descripción

El parámetro de la Tasa de Ahorro de DAI permite a la Gobernanza ajustar la tasa de interés pagada a los poseedores de DAI, que los han depositado en estos contratos de TAD (`Pot`). Todos los poseedores de DAI pueden depositarlos en el contrato para recibir la Tasa de Ahorro de DAI.

La Tasa de Ahorro es comúnmente expresada como un APY (Porcentaje de Rendimiento Anual) y los balances aumentan cuando se ajusta a cualquier valor positivo.

Por ejemplo, si la Tasa de Ahorro de DAI esta fijada al 1%, un depósito de 100 DAI, después de un año, tendrá un valor de 101 DAI.

## Propósito

La Tasa de Ahorro de DAI permite que la Gobernanza Maker motive a los poseedores de DAI a depositarlos en el contrato. Grandes cantidades de DAI dentro del contrato de la Tasa de Ahorro de DAI deberían reducir su oferta de mercado y actuar como una presión alcista en la paridad con el dólar.

## Contrapartida

Aumentar la Tasa de Ahorro de DAI también aumenta su demanda, pero a costa de disminuir su liquidez y aumentar los gastos del Protocolo de Maker.

Disminuir la Tasa de Ahorro de DAI también disminuirá los gastos para el Protocolo de Maker, pero simultáneamente puede reducir la demanda de DAI y hacer que los poseedores decidan sacarlos del contrato, generando así un aumento en la oferta de mercado.

## Cambios

Ajustar la Tasa de Ahorro de DAI es un proceso manual que requiere de un Voto Ejecutivo. Los cambios al contrato están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

En esencia, un aumento en la Tasa de Ahorro de DAI produce una presión alcista sobre el precio del DAI, por otro lado, una menor Tasa de Ahorro de DAI reduciría esta presión.

**¿Por qué incrementar este parámetro?**

La principal razón para el incremento de la Tasa de Ahorro de DAI, es el aumento en la demanda de DAI. Este aumento en la demanda se logra motivando a los poseedores de DAI a que los depositen en el contrato de la Tasa de Ahorro de DAI, removiéndolo así del mercado, lo que crearía presiones alcistas en la paridad con el dólar. De esta forma, elevar la Tasa de Ahorro de DAI debería tenerse en cuenta si el DAI se está cotizando por debajo de la paridad con el dólar.

Aumentar la Tasa de Ahorro de DAI debería hacer que el DAI sea un activo más atractivo para los poseedores que otros activos stablecoins e incentivar su integración al Protocolo Maker, por ejemplo, logrando que otras DAPPs que posean stablecoins, las depositen en el contrato de Tasa de Ahorro de DAI para ganar interés.

**¿Por qué disminuir este parámetro?**

La razón principal para disminuir la Tasa de Ahorro de DAI, es para reducir la demanda de DAI. Disminuir la Tasa de Ahorro de DAI resultaría en menos DAI depositado en el contrato de Tasa de Ahorro, haciendo que el DAI vuelva a entrar en el mercado. Adicionalmente, podría ser recomendable disminuir la Tasa de Ahorro de DAI si el DAI se cotiza por encima de su paridad con el dólar, para reducir la presión alcista del precio.

La Gobernanza de Maker podría disminuir la Tasa de Ahorro de DAI si el Protocolo de Maker experimenta una caída en sus ingresos. Si la Gobernanza no reduce la Tasa de Ahorro cuando los ingresos caigan, el Protocolo podría encontrar flujos de caja negativos. Estos flujos de caja negativos reducirán el Buffer de Excedente del Sistema a lo largo del tiempo, y si el buffer se agota, el Protocolo acuñará y venderá MKR para cubrir el déficit.

## Consideraciones
Cuando los poseedores de DAI depositan DAI en el contrato de Tasa de Ahorro de DAI, el interés es pagado de las tarifas de estabilidad acumuladas. Por lo tanto, aumentar la Tasa de Ahorro de DAI causará que el Buffer de Excedente del Sistemas se llene más lentamente y reduzca la cantidad de DAI disponible para Subastas de Excedentes. Si la Tasa de Ahorro de DAI se ajusta muy arriba, el Protocolo de Maker podría tener flujos de caja negativos y eventualmente la necesitaría imprimir MKR.

La Gobernanza de Maker deberá reconocer que una Tasa de Ahorro de DAI negativa no funcionará como estaba previsto, ya que los balances dentro del contrato de la Tasa de Ahorro de DAI no pueden disminuir. Esto es porque la función `drip` (_goteo_) se revertirá si es negativa.

Cualquier posibilidad de cambio en la Tasa de Ahorro de DAI puede afectar el comportamiento de uso del PSM. Por ejemplo, aumentar la presión alcista en la paridad con el dólar, causado por la Tasa de Ahorro de DAI podría requerir un incremento en el uso de PSM para estabilizar. Esto puede contribuir al flujo de caja negativo, ya que no abra ingresos continuos del PSM.

En caso de que se active el Apagado de Emergencia, la Tasa de Ahorro de DAI estará fijada al 0% para prevenir que la deuda total del Protocolo Maker aumente.
