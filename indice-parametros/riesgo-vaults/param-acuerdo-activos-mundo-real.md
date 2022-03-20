# Acuerdo de Activos del Mundo Real (_RWA, Real World Assets_)

>**Alias:**  
>**Parameter Name:** `doc`  
>**Containing Contract:** `RwaLiquidationOracle`  
>**Scope:** MIP21 / Ilk (RWA)  
>**Technical Docs:** [link](https://mips.makerdao.com/mips/details/MIP21)  

## Description

Las _vaults_ de _RWA_ son dependientes de un acuerdo contractual, el Acuerdo de Activos del Mundo Real (_RWA, Real World Assets_).
El parámetro del Acuerdo de Activos del Mundo Real permite al Protocolo de Maker registre un hash de IPFS que se vincula con la documentación del contrato real. Cada acuerdo tendrá una documentación de contrato individual y el formato de la documentación puede cambiar de un acuerdo a otro.

## Propósito

Al registar los contenidos del Acuerdo de Activos del Mundo Real en la _blockchain_, se consigue un registro limpio y transparente de los acuerdo legales realizados por la _Core Unit_ de Activos del Mundo Real. Esta transparencia beneficia a la Gobernanza y será útil en el caso de disputas con prestatarios.

Este parámetro es usado solo por Activos del Mundo Real usando la MIP21 - Definición de la Estructura de una _Vault_.

## Cambios

El ajuste del Acuerdo de Activos del Mundo Real se puede realizar mediante un proceso manual que requiere un Voto Ejecutivo. Los cambios al Acuerdo de Activos del Mundo Real están sujetos al Período de Pausa del Módulo de Seguridad de la Gobernanza.

La Gobernanza de Maker debe realizar cambios en el parámetro para reflejar los cambios en la documentación contractual subyacente.

La Gobernanza de Maker no debe cambiar el parámetro a menos que haya habido un cambio en la documentación contractual subyacente.

## Consideraciones

Dado que MakerDAO no es una entidad legal, el uso real de la documentación contractual puede estar limitado.

---

[Texto Original](https://github.com/makerdao/governance-manual/blob/main/parameter-index/vault-risk/param-rwa-agreement.md)
