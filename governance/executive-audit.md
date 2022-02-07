# Auditoría de los _Spells_ Ejecutivos

Esta es una guía para ayudar a los poseedores de MKR a verificar los _spells_ ejecutivos en el Protocolo de Maker antes de votar por ellos.

Este documento contiene 4 secciones principales:

1. **Encontrar el Código del Contrato** - se ocupa de localizar el código del ejecutivo en cuestión.

2. **Validar el Código y Copia del Ejecutivo** - se ocupa de asegurar que el _spell_ y su copia asociada se encuentren según lo esperado.

3. **Anatomía del Contrato de un _Spell_** - muestra ejemplos de las secciones principales que se esperan encontrar en un _spell_ ejecutivo.

4. **Lista de Verificación No Exhaustiva**: incluye una lista de las cosas más importantes para chequear dos veces y cómo hacerlo.

El enfoque clave al revisar un _spell_ ejecutivo es que si alguna parte de un _spell_ ejecutivo parece sospechosa o confusa de alguna manera, siempre es mejor verificar dos veces antes de votar. Aunque te encuentres equivocado con respecto a tus inquietudes, esto nos informa que debemos agregar más detalles a este documento para evitar que alguien se confunda de la misma forma en el futuro.

## Encontrar el Código del Contrato

El link al _spell_ en Etherscan se puede encontrar en el Portal de Votación en el panel de "Detalles de Propuestas". Busca por la propiedad `Spell Address`:

![](https://i.imgur.com/qdAfqZM.png)

Dándole clic a `Spell Address` abrirá el _spell_ en Etherscan, donde el espectador puede hacer clic en la pestaña del Contrato para ver el código:

![](https://i.imgur.com/vrIClir.png)

El código del contrato debería ser visible. Si solo es posible ver el código de bytes (lo que significa que el contrato no está verificado), entonces el ejecutivo debe verse como potencialmente malicioso. En este caso, pega un grito en el chat y anima a las personas a NO votar por él hasta que el código del contrato verificado esté disponible.

Más allá de buscar en el [Portal de Gobernanza](www.vote.makerdao.com), también puedes encontrar en [Github](https://github.com/makerdao/community/tree/master/governance/votes) la copia de los _spell_ ejecutivo actuales y pasados.

## Validar el Código del _Spell_

Valida que el código Etherscan _on-chain_ coincida con el [código archivado](https://github.com/makerdao/spells-mainnet/tree/master/archive) correspondiente o con el [ejecutivo más reciente](https://github.com/makerdao/spells-mainnet/tree/master/src) en Github. Si no es posible ubicar el _spell_ más reciente, puede deberse a que aún no se ha fusionado con la rama maestra antes de que se active, si ese es el caso, los cambios se pueden encontrar en las [solicitudes de _pulls_](https://github.com/makerdao/spells-mainnet/pulls) pendientes.

Para hacer esta comparación de códigos, usa el programa llamado [Diff Checker](https://www.diffchecker.com/) para comparar el _spell_ en Etherscan contra el código correspondiente en Github. Cliqueando en `find difference` (_encontrar diferencias_) podrás ver cualquier diferencia encontrada entre ambos códigos.

Ten en cuenta que el código de Etherscan también mostrará las interfaces de DssExecLib, representadas por la sección verde adicional en la parte superior del archivo, que incluye lo siguiente para tu conocimiento:

```
The following library code acts as an interface to the actual DssExecLib
library, which can be found in its own deployed contract. Only trust the actual
library's implementation.
```
###### _'El siguiente código de biblioteca actúa como una interfaz para la biblioteca real de DssExecLib, que se puede encontrar en su propio contrato implementado. Solo confía en la implementación de la biblioteca actual.'_

Esto significa, que esta es la [biblioteca](https://github.com/makerdao/spells-mainnet/tree/master/lib) de DssExecLib que debería revisarse y que será cubierto en la próxima sección de anatomía de un _spell_. De lo contrario, todo lo que se encuentra debajo de este texto verde debe ser idéntico al contenido del _spell_ tal como se presenta en Github.

![](https://i.imgur.com/AaG6YDc.png)

En el ejemplo anterior, la comparación se realiza entre el [archivo en Github](https://github.com/makerdao/spells-mainnet/blob/master/archive/2021-09-24-DssSpell.sol) contra el [código de contrato de Etherscan](https://etherscan.io/address/0x0ed5a04DdE29f90bB00529608D3f17C1ffF778A0#code) correspondiente.

### Validar la Copia de la Gobernanza

Para garantizar que los diversos actores (incluidos los Facilitadores de la Gobernanza y los desarrolladores de _smart contracts_) estén alineados, el cuerpo del _spell_ incluye un hash de la copia de github que aparece en el portal de la Gobernanza. Este hash se incluye en el _spell_ para confirmar que los desarrolladores de _smart contracts_ que crean el _spell_ han hecho referencia a la copia correcta que se está votando. El hash aparece en el hechizo de esta manera:

```
"2021-09-24 MakerDAO Executive Spell | Hash: 0x655e71cb00b63a11c14db615d43d3e59202ff9d2b2bc6a6a03de42e258bd1be8";
````

Para validar que la copia en el [Portal de la Gobernanza](vote.makerdao.com), que se encuentra reflejada en [Github](https://github.com/makerdao/community/tree/master/governance/votes), tenga el mismo hash que la que se encuentra en el _spell_ ejecutivo, el usuario puede copiar y pegar el cuerpo del texto en Github en esta [herramienta online](https://emn178.github.io/online-tools/keccak_256.html) de Github para generar el hash y ver si coinciden.

Alternativamente, el usuario puede generar este hash ejecutando el siguiente comando seth:

```
seth keccak -- "$(wget https://raw.githubusercontent.com/makerdao/community/f33870a7938c1842e8467226f8007a2d47f9ddeb/governance/votes/Executive%20vote%20-%20October%208%2C%202021.md -q -O - 2>/dev/null)"
```
Si el hash no coincide, sería prudente cuestionar los contenidos del _spell_ y la copia a la que hace referencia o fue modificada.

## Anatomía de un Ejecutivo
Un _spell_ ejecutivo se divide en varias partes, incluyendo: biblioteca de _spells_, acciones de _spells_ y constructores, las cuales se revisarán a continuación.

### Biblioteca de _Spells_

Los _spells_ ejecutivos de MakerDAO han evolucionado con el tiempo hacia el uso de bibliotecas en un esfuerzo por automatizar el proceso de realizar actualizaciones y cambios repetitivos en los parámetros del Protocolo. Las bibliotecas reducen la posibilidad de errores mediante la reutilización o la creación de código previamente probado y verificado.

Al auditar el ejecutivo, es necesario verificar primero que el hechizo use la biblioteca `dss-exec-lib` y, en segundo lugar, que la biblioteca sea la biblioteca legítima y oficial. Esto se puede verificar mirando la copia del _spell_ en Etherscan.

El usuario puede confirmar que el ejecutivo esté usando la biblioteca `dss-exec-lib` identificando que el punto de entrada para DssSpell es DssExec en la parte inferior del código del contrato:

```
contract DssSpell is DssExec
```
###### '_El Contracto DssSpell es DssExec._'

Entonces es necesario validar que la biblioteca correcta esté vinculada y, por lo tanto, importar el código correcto. Al permanecer en la pestaña de contrato de etherscan, uno puede desplazarse hasta la parte inferior de la página y ver la _address_ de DssExecLib:

![](https://i.imgur.com/OJfhqkr.png)

Para verificar que DssExecLib no es maliciosa, el usuario puede tomar el bloque del código y compararlo contra un repositorio conocido, como [makerdao/dss-exec-lib](https://github.com/makerdao/dss-exec-lib/tree/47bf15efe4cc9c737608c6acefb9de37fb3b3c7f), para validar cualquier cambio que pueda estar presente. El uso de Diff Checker puede ser útil para este propósito.

También es importante comparar la _address_ de la ExecLib de Etherscan contra el [Makefile](https://github.com/makerdao/spells-mainnet/blob/master/Makefile) de MakerDAO y asegurarse que este coincide con la _address_ de DssExecLib:

![](https://i.imgur.com/NpVIocV.png)

Si lo dicho anteriormente coincide, el usuario puede estar seguro de que la biblioteca a la que se hace referencia es realmente válida.

### Constructos de _spells_

Ahora que el usuario se encuentra seguro de que la biblioteca es válida, es posible volver al _spell_ y revisar la última línea que revela el constructor de DssExec que determina la programación y las restricciones de la emisión:

```
{
    constructor() DssExec(block.timestamp + 30 days, address(new DssSpellAction())) public {}
}
```
Esta línea llama al código del constructor dentro de la biblioteca DssExec y le pasa una fecha de caducidad, por lo que cada vez que se crea este _spell_, toma la fecha del bloque actual y agrega una cantidad de días, en este caso 30 días. Esto debe alinearse con el proceso de la Gobernanza. También es necesario asegurarse de que esto pase por el bloque de código del DssSpellAction anterior, que es la instancia del _spell_.

Vale la pena señalar que, aunque el constructor determina la programación y las restricciones de la emisión, estas variables se abstrajeron en [ExecLib](https://github.com/makerdao/dss-exec-lib/blob/master/src/DssExec. sol), y ya no aparecen en el _spell_.

Luego de llamar a `schedule` ("programar") y después de que finalice el retraso, cualquiera puede llamar a `cast` ("emisión"), que ejecutará el código en la función `DssSpellActions` de SpellAction, que se encuentra a continuación.

### Acciones de los _Spells_

Ahora que hay confianza en el _framework_ en torno al _spell_ y la biblioteca externa, es posible concentrarse en las Acciones de los _Spells_, que es la mayor parte de lo que se programa y lanza para su ejecución.

Los usuarios que han revisado _spells_ anteriores, pueden recordar el uso de la función `execute` ("ejecutar"). Esto ya no se usa debido a que las acciones de _spells_ se emplean para apuntar a ExecLib y realizar cambios en el Protocolo. Una vez más, esto destaca la importancia de la biblioteca y un enfoque útil para reducir el tamaño de los _spells_.

Como regla general, es importante verificar que todo en la sección anterior o posterior a las Acciones de los _Spells_ sea una **constante**, por ejemplo, como se muestra aquí:

```
contract DssSpellAction is DssAction {

    // Provides a descriptive tag for bot consumption
    // This should be modified weekly to provide a summary of the actions
    // Hash: seth keccak -- "$(wget https://raw.githubusercontent.com/makerdao/community/3d3670a98ca02e74c001bdf083765ab4eb4bc2cd/governance/votes/Executive%20vote%20-%20September%2024%2C%202021.md -q -O - 2>/dev/null)"
    string public constant override description =
        "2021-09-24 MakerDAO Executive Spell | Hash: 0x655e71cb00b63a11c14db615d43d3e59202ff9d2b2bc6a6a03de42e258bd1be8";

    // L2 Test Spells
    address constant OPTIMISM_L1_GOVERNANCE_RELAY         = 0x09B354CDA89203BB7B3131CC728dFa06ab09Ae2F;
    address constant OPTIMISM_L2_SPELL                    = 0x71d75C3D100D14d4db0cE7a83d0De48ecEC32D19;
    address constant ARBITRUM_L1_GOVERNANCE_RELAY         = 0x9ba25c289e351779E0D481Ba37489317c34A899d;
    address constant ARBITRUM_L2_SPELL                    = 0xAeFc25750d8C2bd331293076E2DC5d5ad414b4a2;

    // Math
    uint256 constant MILLION  = 10 ** 6;

    function actions() public override {
```

Si alguno de estos valores no es constante, esto podría presentar un código malicioso en forma de mutaciones de memoria que afecten la función del proxy de pausa y se debe alertar a la comunidad. Este riesgo se cubre más adelante en la sección de Variables Constantes.


Como se mencionó en la sección de la biblioteca, las acciones estándar generalmente usarán DssExecLib para realizar una acción de manera segura. Para las acciones no estándar, estas recurrirán a las llamadas directas al sistema. Algunos ejemplos incluyen:

```
function actions() public override {

  // Set ilk/global DC
  DssExecLib.increaseIlkDebtCeiling(collateral.ilk, collateral.CEIL, true);

  // Set stability fee
  DssExecLib.setIlkStabilityFee(collateral.ilk, collateral.RATE, false);

  // Set values directly
  Fileable(col.dog).file(col.ilk, "hole", col.hole);
  Fileable(col.dog).file(col.ilk, "chop", col.chop);
  Fileable(col.clipper).file("buf", col.buf);

}
```



### Horario de Oficina

La función de horario de oficina determina si el _spell_, una vez votado, se limita o no a programarse entre las 10:00 y las 16:00 EST de lunes a viernes. Para saber si debe aplicarse o no, se establece el valor booleano _true_/_false_ ("verdadero/falso").

Si falta esta función en la Acción de los _Spells_, el código volverá al estado de horario de oficina que se encuentre predeterminado, el cual es _true_ (horario de oficina _on_)

```
function officeHours() public virtual returns (bool) {
    return true;
```

Tal valor es `true` cuando los nuevos cambios pueden afectar a los integradores o a los encargados de las subastas, y es `false` cuando no se aplica el horario de oficina, lo que significa que el _spell_ se puede lanzar en cualquier momento una vez que se haya votado con éxito. El código que determina estas reglas también ha sido [abstraído](https://etherscan.io/address/0xfD88CeE74f7D78697775aBDAE53f9Da1559728E4#code#L335) en ExecLib.

## Lista de Verificación No Exhaustiva

### Verificar que el código del contrato sea visible
Usando las instrucciones detalladas anteriormente, encuentra el código del contrato en Etherscan y asegúrate de que este sea visible y esté verificado. Del mismo modo, asegúrate de que se haga referencia a ExecLib correctamente. Verifica que estos coincidan con lo que los desarrolladores de _smart contracts_ han publicado/implementado.

### Verifica que la copia de la interfaz coincida con la copia utilizada para construir el _spell_
Crea un hash de la copia de github/_frontend_ ("interfaz") y compáralo contra el hash en el _spell_ para confirmar que los dos estén alineados.

### Verifica que el constructor sea el esperado
Asegúrate que la caducidad del _spell_ coincida con los _spells_ anteriores, esto incluye al bloque de código DssActions y que las funciones de programación y emisión existan en DssExecLib. Si el Constructor no coincide con las funciones anteriores, debe haber una explicación del por qué.

### Revisa el _Changelog_

Asegúrate de que DssExecLib llame al _changelog_ ("registro de cambios") con los descriptores de nombre correctos (estas solían ser _addresses_ ortográficas, pero desde entonces han sido reemplazadas por descriptores de nombres para su simplicidad y reducción de errores). Por lo tanto, es una buena práctica revisar el _changelog_ para asegurarte que hayas hecho referencia al descriptor de nombre correcto como parte de la acción _on-chain_.

### Revisa las _addresses_ de Oráculos

Ocasionalmente, hay _spells_ que involucran a Oráculos, generalmente agregando _addresses_ a la lista y ocasionalmente, agregando un nuevo oráculo. Estas _addresses_ también deben verificarse cuidadosamente. Para hacerlo, es necesario ir al [_Changelog_](https://changelog.makerdao.com/) y buscar, como por e.j: `PIP_ETH`. Llevar el contrato a Etherscan y abrir la pestaña `read` ("leer") del contrato, que mostrará el `src` ("fuente"; aparece como número 7 actualmente). La _address_ del contrato que aparece allí se puede verificar para que coincida con el `MedianETHUSDcontract` ("Contrato medio de ETHUSD") que se encuentra en el _spell_.

### Revisa los cambios de tasa

Las tasas se definen como valores de acumulación por segundo. Estos valores se pueden validar con la tasa comentada usando el comando bc en una shell bash. En el ejemplo, usando la variable `NEW_FEE` en el contrato, se ve lo siguiente:

`bc -l <<< 'scale=27; e( l(1.095)/(60 * 60 * 24 * 365) )`

Esto produce 1.000000002877801985002875644. Sacando los decimales, se puede comprobar que esto coincide con la definición de `NEW_FEE`.

La validación de todos los ajustes de tasas se puede hacer de la misma manera. Para más información acerca del módulo de tasas, visita las [guías para desarrolladores de github](https://github.com/makerdao/developerguides/blob/master/mcd/intro-rate-mechanism/intro-rate-mechanism.md). Para una fácil referencia, las tasas comunes precalculadas también se pueden ver en el siguiente [enlace de ipfs](https://ipfs.io/ipfs/QmefQMseb3AiTapiAKKexdKHig8wroKuZbmLtPLv4u2YwW).

### Revisa DssExecLib para asegurarte de que 'Drip' sea llamado antes de que se cambien las tasas
Al hacer cambios en las tasas, se debe llamado la función `drip` en los respectivos contratos. Como por ejemplo, si se está haciendo el cambio de una tasa DSR, `drip` será llamado en al función `pot` o, si la tarifa de estabilidad está siendo modificada en un tipo de colateral, es necesario llamar a `drip("ILK")` en la función `jug`. A pesar de que `drip` se abstrae a DssExecLib, todavía se puede confirmar en la biblioteca como parte de las anteriores verificaciones de biblioteca.

Para confirmar que esto es posible, hay un parámetro booleano en la función execlib, `doDrip`. El usuario debe asegurarse de que sea `true` para relaizar un `drip`, el cual se puede encontrar [aquí](https://github.com/makerdao/dss-exec-lib/blob/master/src/DssExecLib.sol#L777);

```
function setIlkStabilityFee(bytes32 _ilk, uint256 _rate, bool _doDrip) public {
```

### Toda variable de contrato _SpellActions_ ("Acciones de los _Spells_") debe declararse como "constante"

_SpellActions_ nunca debe tener nada en la memoria del contrato. Por lo tanto, todas las variables del contrato deben declararse como constantes. Esto se debe a que, en el momento de la ejecución, las variables del contrato serán las del DSPauseProxy. Si hay variables en esta sección que no sean constantes, entonces es un error significativo y no debe votarse.

---

[Artículo Original](https://github.com/makerdao/governance-manual/edit/main/governance/executive-audit.md)
