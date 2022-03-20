# Tamaño del Lote de Excedentes

>**Alias:** Surplus Auction Lot Size  
>**Parameter Name:** `bump`  
>**Containing contract:** `Vow`  
>**Scope:** System  
>**Technical Docs:** [link](https://docs.makerdao.com/smart-contract-modules/system-stabilizer-module/vow-detailed-documentation)  

## Descripción
El Tamaño del Lote de Excedentes o el parámetro `bump` controla el monto de DAI que es subastado en cada subasta de excedentes.

Las Subastas de Excedentes se pueden activar cuando `Surplus DAI > System Surplus Buffer (hump) + Surplus Lot Size (bump)`.


### Ejemplo

`System Surplus Buffer` (_Buffer de Excedentes del Sistema_) = 50 millones de DAI  
`Surplus Lot Size` (_Tamaño del Lote de Excedentes_) = 10.000 DAI

El excedente del sistema debe superar los 50.010.000 DAIs antes de que una subasta de excedentes se active. Cuando ocurra esta subasta de excedentes, 10.000 DAIs serán subastados a los _keepers_ a cambio de MKR.

## Propósito
El Tamaño del Lote de Excedentes asegura que las subastas de excedentes tengan un tamaño constante haciendo que el sistema sea más predecible. También permite que la Gobernanza de Maker sintonice la frecuencia y accesibilidad de las subastas de excedentes con el fin de conseguir mejores precios.

## Contraparte

El incrementar el Tamaño del Lote de Excedentes acabará en que haya menos subastas, lo cual resultaría en una competencia entre los _keepers_ en cada subasta y la eficiencia aumentada del _gas_. Sin embargo, un Tamaño del Lote de Excedentes más grande puede hacer que el requisito de capital sea prohibido para algunos _keepers_, lo que reduce la cantidad de personas que pueden ofertar.

El reducir el Tamaño del Lote de Excedentes significa que ocurrirán un gran número de subastas. Estas subastas requerirán montos menores para poder participar en ellas, permitiendo que más _keepers_ participen. Sin embargo, el que hayan más subastas conduce a un costo fijo más alto para ofertar en relación con la ganancia potencial, lo que podría disminuir la participación. Si las subastas no son competitivas entonces el precio obtenido por el DAI subastado puede quedar por debajo de las tasas del mercado.

## Cambios
Ajustar el Tamaño del Lote de Excedentes es un proceso manual que requiere de un Voto Ejecutivo. Los cambios al Tamaño del Lote de Excedentes están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

Por lo general, el objetivo del ajuste de este parámetro es incrementar la participación de _keepers_ en las subastas de excedentes.

**¿Por qué incrementar el Tamaño del Lote de Excedentes?**
La razón principal por la cual la Gobernanza de Maker incrementaría el Tamaño del Lote de Excedentes es para reducir el número total de subastas de excedentes. Al tener menos subastas, se reduce el costo del _gas_ de los _keepers_ en relación con su ganancia potencial, lo que hace que la participación sea más atractiva para ellos.

**¿Por qué disminuir el Tamaño del Lote de Excedentes?**
La razón principal por la cual la Gobernanza de Maker disminuiría el Tamaño del Lote de Excedentes es para reducir el requisito de capital para la participación en las subastas; lo cual resultaría en un potencial incremento en el número de _keepers_ que puedan participar.

## Consideraciones

El Tamaño del Lote de Excedentes no puede ser menor o igual a 0 DAI.

El costo del _gas_ para activar (`kick`) una subasta de excedentes no es trivial. Si el Tamaño del Lote de Excedentes es muy bajo, puede que las subastas de excedentes no sean activadas por ningún _keeper_ porque ellos se encuentran obligados a aceptar un costo fijo por un desenlace incierto.

---

[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/surplus-auction/param-surplus-lot-size.md)
