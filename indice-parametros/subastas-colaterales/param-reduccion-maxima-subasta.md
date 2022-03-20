# Reducción Máxima de la Subasta

>**Alias:**  
>**Parameter Name:** `cusp`  
>**Containing Contract:** `Clipper`  
>**Scope:** Vault Type (Ilk)  
>**Technical Docs:**  

## Descripción

La Reducción Máxima de la Subasta es el porcentaje máximo que puede caer el precio de un colateral durante una subasta de colaterales antes de que la misma se reinicie. Cuando decimos 'precio de un colateral' en este contexto nos referimos al _precio de subasta_ del colateral más que al _precio del mercado_ del colateral. Las subastas de colaterales utilizan una subasta de caída de precio, donde el precio comienza alto y va disminuyendo de acuerdo a la Función de Precio de Subasta hasta que haya sido disminuido por el parámetro de Reducción Máxima de la Subasta.

Si una subasta de colaterales comienza con un precio de $100, y luego la Reducción Máxima de la Subasta es fijada en 70%, la subasta se reiniciará si el precio de la subasta de colaterales llega a $30.

El parámetro de Reducción Máxima de la Subasta se superpone con el parámetro Duración Máxima de la Subasta, en el cual una subasta necesita reiniciarse una vez que cualquiera de los máximos es excedido.

## Propósito

Este parámetro existe, principalmente, para prevenir que las subastas de colaterales que continúen más allá del punto de la cordura, y subastar colaterales a un precio muy por debajo del precio de mercado en caso de un problema imprevisto que impida las ofertas. Es redundante con el parámetro de Duración Máxima de la Subasta y le permite a la Gobernanza de Maker decidir si fijar el precio más bajo directamente o implícitamente a través de los parámetros de Curva de Precio de la Subasta y Duración Máxima de la Subasta.

## Contrapartida

Fijar este parámetro muy bajo puede resultar en subasta de colaterales vendiendo colaterales por debajo del precio del mercado en caso de que interrupciones imprevistas impidan las ofertas.

Por otro lado, fijar este parámetro muy alto puede retrasar la resolución exitosa de la subasta debido a los muy frecuentes reinicios en la subasta. Reinicios freceuntes también dan como resultado que el protocolo pague Incentivos de Activación adicionales (tanto proporcionales como planos).

## Cambios
Ajustar el parámetro de Reducción Máxima de la Subasta para un tipo de _vault_ específico es un proceso manual que requiere de un Voto Ejecutivo. Los cambios a los parámetros de Reducción Máxima de la Subasta están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

## Consideraciones

La Reducción Máxima de la Subasta está basada en el precio inicial de la subasta (`top`), el cual es igual al precio _OSM_ multiplicado por el Multiplicador de Precio de la Subasta (`buf`).

El parámetro Reducción Máxima de la Subasta fija una de las dos condiciones que pueden solicitar de forma independiente el reinicio en una subasta, el otro es el parámetro Duración Máxima de la Subasta.
