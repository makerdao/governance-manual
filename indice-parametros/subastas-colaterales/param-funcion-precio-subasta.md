# Función de Precio

>**Alias:** Curva de Precio  
>**Nombre del Parámetro: ** `calc`  
>**Contrato:** `Clipper`  
>**Alcance:** Tipo de Vault (Ilk)  
>**Documentos Técnicos:**  

## Descripción
La Función del Precio de Subasta es una función matemática que determina cómo el precio del colateral cambia durante el tiempo que transcurre una subasta de colateral. Las subastas de colateral usan un precio de subasta que va en bajada, donde el precio comienza alto y disminuye de acuerdo con la función definida en este parámetro.     

Las Funciones del Precio de Subasta son implementadas como _smart-contracts_ (contratos inteligentes), exponiendo Funciones Específicas. Un contrato de Función de Precio de Subasta puede tener parámetros adicionales que permitan que la Gobernanza de Maker ajuste ciertos aspectos de la función.

Cada tipo de _vault_ puede tener su propia Función de Precio de Subasta, aunque en la práctica, pueden compartir el mismo Contrato de Función de Precio.  

## Propósito

Este parámetro existe para controlar la forma de la curva de precio cuando se está subastando el colateral de una _vault_ liquidado.

## Curvas de Precio

### 'Stair Step' Exponencial

**Cut**  
Controla la 'profundidad' de cada paso en la función. Un pequeño corte significa una línea más suave, en cambio un `cut` más grande significa pasos más pronunciados.
Esto es un factor multiplicativo. Por ejemplo, 0.99 equivale a una caída del precio en 1%.

**Step**  
Controla la duración del tiempo entre las caídas de los precios. Un `step` pequeño significa una línea más suave, mientras que uno grande significa pasos mas pronunciados. Es definido en segundos.

![](https://github.com/blimpa/maker-operational-manual/tree/74d4a3e2c96e851b7fafa610ba57d628eab7c817/images/cut-and-step.png)

## Contrapartidas

Tener control sobre los parámetros de la Subasta de Función de Precio le permite a la Gobernanza ajustar el rendimiento de las subastas para que se adapten mejor a las cambiantes condiciones del mercado. Una configuración no optima podría hacer que las subastas se resolvieran más lentamente o que el colateral se subaste en un precio inferior.

Que un precio de subasta caiga muy rápidamente puede llevar a una situación donde los _Keepers_ no sean capaces de proponer su oferta antes de que la subasta termine.

Que un precio de subasta caiga muy lentamente puede aumentar el deslizamiento de la subasta y potencialmente causar una deuda mala.

## Cambios

Ajustar el Parámetro de una Función de Precio es un proceso manual que requiere un voto ejecutivo. Cambios en la Función de Precio están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza
