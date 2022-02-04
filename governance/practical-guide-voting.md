# Guía Práctica para la Votación _On-Chain_
Esta sección explica a los usuarios cómo utilizar sus MKR para emitir su voto.

### Voto de _wallet_ única
El voto de _wallet_ única es el método de votación más simple. La configuración inicial es más conveniente y los usuarios que almacenen MKR en MetaMask u otras _wallets_ web pueden encontrar a esta como la forma más fácil de comenzar a votar. Los usuarios deben depositar los tokens directamente en el contrato de votación conectando su _wallet_ con el Portal de Gobernanza.

El voto de _wallet_ única puede derivar en problemas de seguridad si no se utiliza una _hardware wallet_ (dispositivos físicos que operan como monederos sin conexión a Internet) dado que cada voto requiere una interacción con la _wallet_.

### Voto de _wallet_ linkeada
Las desventajas de utilizar un voto de _wallet_ única pueden ser eludidas por el contrato de Votación Proxy. El mismo provee seguridad durante el proceso de votación al permitir a los poseedores de MKR participar en la Gobernanza de Maker sin necesidad de utilizar su _wallet_ más segura (llamada _"cold wallet"_) para la votación. El dueño del MKR designa una llamada _"hot wallet"_ que sólo puede ser utilizada para votar, y transfiere su MKR al contrato de Votación Proxy. La _hot wallet_ designada puede entonces ser utilizada para bloquear MKR en el sistema de votación y retirar posteriormente el MKR de vuelta a la _cold wallet_. Estas son las únicas acciones que puede realizar una _hot wallet_. No puede enviar MKR a ningún otro lado, ni tampoco puede retirar MKR a su propia _wallet_. Por esto, si la _hot wallet_ resulta comprometida, los MKR del votante no corren peligro.

### Costos del Voto
Votar requiere una única transaccióon y el costo varía dependiendo de la congestión de la blockchain de Ethereum.

Configurar una _wallet_ linkeada a los Contratos de Votación requiere de cuatro transacciones por un total de aproximadamente 1 millón de _gas_. El costo de la configuración de una _wallet_ linkeada a los Contratos de Votación se divide entre ambas _hot_ y _cold wallets_ de manera que los usuarios deben asegurarse de que ambas _wallets_ poseen suficiente Ether (ETH) para pagar los costos de _gas_.

### Delegación
Los poseedores de MKR pueden también delegar sus MKR y permitir a un delegado votar en su nombre. Para más información sobre la delegación, puedes consultar [aquí](https://manual.makerdao.com/governance/what-is-delegation).
