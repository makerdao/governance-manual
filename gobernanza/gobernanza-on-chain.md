# Gobernanza _On-chain_ 
Hay dos tipos de actividades principales de Gobernanza _on-chain_: Encuestas de Gobernanza y Votaciones Ejecutivas.

### Encuestas de Gobernanza
Las Encuestas de Gobernanza ocurren _on-chain_ (_en la cadena_) y se utilizan para medir el sentimiento de los poseedores de MKR. A menudo, las encuestas corren simultáneamente, habilitando a los votantes a participar, al mismo tiempo, en la cantidad de encuestas que deseen y algunos utilizan la [segunda vuelta instantánea](https://es.wikipedia.org/wiki/Segunda_vuelta_instant%C3%A1nea). El cronograma actual exige que las encuestas se activen semanalmente todos los lunes a las 16:00 UTC.

Se les pedirá a los poseedores de MKR que:

- Determinen los procesos de la gobernanza y la DAO fuera de la capa técnica del Protocolo de Maker.
- Formen un consenso sobre metas y objetivos comunitarios importantes.
- Midan el sentimiento sobre posibles propuestas de Voto Ejecutivo.
- Ratifiquen las propuestas de la gobernanza que se originen en los hilos de señales del foro de MakerDAO.
- Determinen en qué valores se deben establecer ciertos parámetros del sistema antes de que esos valores se confirmen en una votación ejecutiva.
- Ratifiquen los parámetros de riesgo para los nuevos tipos de colaterales presentados por los equipos de Riesgo.

[Aquí](https://vote.makerdao.com/polling/Qmeac95W?network=mainnet#poll-detail) se encuentra un ejemplo de una encuesta de gobernanza en el Portal de Gobernanza.

#### ¿Qué tan largo es el Período de Votación para una Encuesta de Gobernanza?
El período de votación de una Encuesta de Gobernanza determinada varía. Las encuestas recurrentes del mismo tipo suelen estar estandarizadas y tienen la misma duración. Los más comunes son los períodos de tres y siete días. Las encuestas que se ejecutan simultáneamente no necesariamente tienen los mismos períodos de votación.

#### ¿Dónde puedo encontrar las Encuestas de Gobernanza _On-Chain_?
La encuestas que se encuentran vigentes y el historial de las ya cerradas, se pueden encontrar en la [página de encuestas](https://vote.makerdao.com/polling) del Portal de Gobernanza.

#### ¿Cómo se crea una Encuesta de Gobernanza _On-Chain_?
Cualquiera puede crear una encuesta de gobernanza _on-chain_ utilizando el _smart contract_ de encuestas; sin embargo, no hay una interfaz de usuario.

Actualmente, solo los Facilitadores de Gobernanza electos pueden colocar encuestas que se muestran en el [Portal de Gobernanza](https://vote.makerdao.com). Las encuestas creadas por addresses arbitrarias de Ethereum **no** son mostradas. En el futuro, los poseedores de tokens MKR o terceros podrán desarrollar nuevas interfaces de usuario u otras interfaces de votación que permitan esto.

### Votaciones Ejecutivas
Las Votaciones Ejecutivas ocurren _on-chain_ y se puede acceder a ellas por medio de la [página ejecutiva](https://vote.makerdao.com/executive) en el Portal de Gobernanza.

Las Votaciones Ejecutivas ejecutan cambios técnicos en el Protocolo de Maker. Cuando está activa, cada votación ejecutiva tiene un conjunto de cambios propuesto que se realizarán en los _smart contracts_ del Protocolo de Maker. Las Votaciones Ejecutivas utilizan un modelo de Votación de Aprobación Continua.

Las Votaciones Ejecutivas pueden ocurrir en cualquier momento, sin embargo, el cronograma actual exige que las Votaciones Ejecutivas corran los viernes. La hora exacta varía, pero casi siempre es después de las 12pm EST, 9am PST, 14:00 UTC.

La Votaciones Ejecutivas pueden ser utilizadas para:

- Agregar o remover tipos de colaterales.
- Agregar o remover tipos de vaults.
- Ajustar los parámetros del sistema global.
- Ajustar los parámetros específicos de vaults.
- Reemplazar los _smart contracts_ modulares.

Cualquiera puede crear una Votación Ejecutiva _on-chain_ usando los contratos de Gobernanza de MakerDAO, sin embargo, no se encuentra disponible ninguna interfaz de usuario para hacer esto. Los usuarios pueden crear propuestas, también conocidas como [_slates_](https://docs.makerdao.com/smart-contract-modules/governance-module/chief-detailed-documentation) (_pizarras_), a través de este [portal experimental](https://chief.makerdao.com/) o interactuando directamente con los _smart contracts_.

[Aquí](https://vote.makerdao.com/executive/template-executive-vote-parameter-changes-wsteth-a-onboarding-october-22-2021?network=mainnet#proposal-detail) se encuentra un ejemplo de una votación ejecutiva en el Portal de Gobernanza.

#### ¿Cómo se calculan los votos?

Los votos ejecutivos se calculan a través de la Votación de Aprobación Continua. En tal sistema, se pueden presentar propuestas de competencia en cualquier momento. Las propuestas permanecen activas durante un período de 30 días o hasta que se ejecutan, lo que ocurra primero. Después de esto, se vuelven propuestas inactivas pero siguen siendo elegibles para votos.

Una propuesta activa es ejecutada si tiene más votos a favor que cualquier otra propuesta. Si los poseedores de tokens MKR no están de acuerdo con una propuesta nueva pueden enviar sus votos a una propuesta inactiva, dando a entender que apoyan el estado actual del sistema. Para revertir un cambio en el sistema se debe presentar una propuesta enteramente nueva. Es imposible reactivar una propuesta una vez se torna inactiva.

Hay tres aspectos a considerar con respecto a la Votación de Aprobación Continua:

- Un voto por cualquier propuesta inactiva crea una barrera para las nuevas propuestas, ya que las nuevas propuestas deben superar el peso de votación de la propuesta inactiva con la mayor cantidad de MKR votando a su favor.
- Los votos deben permanecer en el sistema continuamente para evitar que las malas propuestas se aprueben fácilmente.
- Cuantos más votos haya en el estado actual del sistema, más seguro estará el sistema en general frente a cualquier propuesta "falsa".

Con la Votación de Aprobación Continua, la continuidad de los votos en juego desafía y refuerza el status quo del sistema a través de los movimientos de la mayoría de votos entre el estado actual (la propuesta exitosa más reciente) y las nuevas propuestas.

### Auditabilidad

#### Con respecto a los nuevas votaciones
Se alienta al público a autoauditar el código de cada voto. Hay una guía accesible sobre cómo hacerlo [aquí](governance/executive-audit.md).

#### Con respecto al registro de las votaciones de los usuarios
El voto actual del usuario se muestra en una página de propuesta dada en el [Portal de Gobernanza](https://vote.makerdao.com/). Los registros históricos de votación también están disponibles en el portal de gobernanza.
