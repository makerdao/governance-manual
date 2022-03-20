# Acuñación Rápida

>**Alias:** Flash  
>**Nombre del Contrato:** DSSFlash  
>**Alcance:** System  
>**Documentos Técnicos:** https://docs.makerdao.com/smart-contract-modules/flash-mint-module  

## Descripción

El Modulo de Acuñación Rápida permite a cualquier usuario acuñar DAI sin restricción alguna, siempre y cuando sea pagado de vuelta en la misma transacción. Esto es comúnmente conocido como Préstamo Rápido (_Flash Loan_).

Los usuarios pueden combinar Préstamos Rápidos con las funciones de otros _smart contracts_ para llevar a cabo transacciones de múltiples pasos a través de _exchanges_ descentralizados (DEX). Este tipo de transacciones de múltiples pasos tienen usos variados, como lo es el arbitraje e incluso mejorar la experiencia del usuario creando posiciones apalancadas.

### Ejemplo

Para demostrar como funciona esto en la práctica, imaginemos operaciones de DAI a 1.02 DAI/USDC en DEX-1 y 0.98 DAI/USDC en DEX-2. Usando el Módulo de Acuñación Rápida, un usuario podría arbitrar sobre esta diferencia de precios de la siguiente forma:

* Acuñar 1000 DAI usando el Modulo de Acuñación Rápida  
* Intercambiar 1000 DAI por 1020 USDC en DEX-1
* Intercambiar 1020 USDC por ~1040 DAI en DEX-2
* Pagar devuelta 1000 DAI al Módulo de Acuñación Rápida, dando como resultado una ganancia de ~40 DAI
Para explicarlo de manera sencilla, el ejemplo de arriba no incluye las tarifas del gas. En realidad, el arbitraje de Préstamo Rápido debe tener en cuenta las tarifas del gas para poder ser rentable.

## Propósito

El Módulo de Acuñación Rápida incorpora Préstamos Rápidos en DAI al Protocolo de Maker bajo el control de la Gobernanza de Maker. A continuación se analizarán las variadas ventajas que esto implica.  

## Beneficios

El Módulo de Acuñación Rápida ofrece diversos beneficios al Protocolo de Maker y al ecosistema del DAI en general:

* Mejora la Liquidez del Préstamo Rápido - otros proveedores de Préstamos Rápidos dependen de la oferta de mercado de DAI para proveer de capacidad al mismo. Ya que el Protocolo de Maker es capaz de acuñar DAI, en teoría los Préstamos Rápidos pueden ser de un tamaño infinito. Debido a que el DAI es quemado al finalizar la transacción, esto no afecta la colateralización del DAI.

* El arbitraje de los Préstamos Rápidos mejora la eficiencia de mercado de DAI – un efecto secundario de esto podría ser el incremento de la Liquidez en los mercados de DAI y la Estabilidad de la Paridad, ya que las desviaciones del paridad serán más susceptibles al arbitraje.    

* La habilidad de pedir prestado grandes sumas incrementa la utilidad de los Préstamos Rápidos para identificar _exploits_ en protocolos DeFi – exponiendo _exploits_ y vectores de ataque, el ecosistema DeFi puede ser más robusto.
* El Módulo de Acuñación Rápida alienta futuras integraciones entre el Protocolo Maker y otras Aplicaciones Descentralizadas – Agregadores DEX pueden usarlo para asegurar que sus usuarios obtengan los mejores precios disponibles del mercado, así como los Sistemas de Automatización de _Vaults_ pueden utilizar Préstamos Rápidos para apalancar y desapalancar _Vaults_.  
* Ingresos del Protocolo de Maker - El Protocolo de Maker puede cobrar Tarifas de Acuñación a los Préstamos Rápidos que usen el Módulo de Acuñación Rápida. Las Tarifas de Acuñación tienen el potencial de ser una fuente alternativa de ingresos para el Protocolo de Maker. Normalmente, las tarifas cobradas en los Préstamos Rápidos son en orden del 0-0.1%.  
* El Módulo de Acuñación Rápida no requiere permisos, eso significa que cualquiera puede usarlo. Normalmente, hace posible que más usuarios accedan a oportunidades de arbitraje debido a que ya que no se depende del capital.

## Desventajas

Los Préstamos Rápidos son potentes herramientas, pero también implican cierto riesgo. Por ejemplo, pueden ser usados como un vector de ataque contra Protocolos DeFi. Sumado a ello, es teóricamente posible acuñar cantidades extremadamente grandes de DAI si no hay restricciones, lo que podría desestabilizar algunos Protocolos DeFi.

## Parámetros Clave  

En el Módulo de Acuñación Rápida hay dos parámetros clave que son controlados por la Gobernanza de Maker. Los cambios a estos parámetros se hacen mediante un proceso manual que requiere de un Voto Ejecutivo. Los cambios de estos parámetros están sujetos al Periodo de Pausa GSM.  

### Techo de Deuda (`line`)

El Techo de Deuda se refiere a la máxima cantidad de DAI que un usuario puede acuñar mediante un Préstamo Rápido en una sola transacción.

Entre más alto sea este valor, más grande es el potencial de ganancia de las oportunidades de arbitraje y también la posibilidad de que _exploits_ causen pérdidas para Protocolos DeFi.

Si el Techo de Deuda es muy bajo, las potenciales aplicaciones para el Módulo de Acuñación Rápida serán menos en número. Como resultado, los usuarios pueden buscar fuentes alternativas de Préstamos Rápidos en DAI que proporcionen Techos de Deuda mas generosos.   

### Tarifa de Acuñación (`toll`)

La Tarifa de Acuñación es una tarifa opcional que el Protocolo de Maker puede cobrar a los usuarios de los Préstamos Rápidos. Los usuarios deben devolver la tarifa de acuñación al mismo tiempo que devuelven el principio del Préstamo Rápido. Por ejemplo, un Préstamo Rápido de 1000 DAI con una Tarifa de Acuñación del 0.1% requerirá que 1001 DAI sean pagados devuelta al final de la transacción.

Las Tarifas de Acuñación pueden ser una fuente de ingresos para el Protocolo de Maker, pero disminuirán las ganancias de los usuarios de los Préstamos Rápidos.

Si las fuentes alternativas a los Préstamos Rápidos en DAI cobran tarifas mas bajas o no cobran tarifas, puede que los usuarios decidan usar esas alternativas en vez de usar el Modulo de Acuñación Rápida.

## Interacción del Usuario

El Módulo de Acuñación Rápida se ajusta al ERC1356. Por lo tanto, los usuarios pueden usar la implementación del prestatario de referencia de la especificación ERC1356. Esto requiere que el usuario tenga la habilidad técnica de trabajar con Solidity o tenga acceso a una interfaz de usuario que sea capaz de construir y ejecutar la transacción deseada.

## Consideraciones

Las Tarifas acumuladas a través del Módulo de Acuñación Rápida son transferidas al Buffer de Excedentes una vez que se haya completado la transacción.  
