# EVM Bridge (ERC-20)
Para ter acesso a versão em inglês [clique aqui](link)

## Descrição
EVM Bridge é um projeto que oferece uma ponte entre redes baseadas em blockchain usando a Máquina Virtual Ethereum (EVM). Sua finalidade é facilitar o desenvolvimento e teste de tokens interoperáveis, permitindo a transferência de valor entre diferentes blockchains compatíveis com a EVM. Além disso, o projeto fornece uma documentação abrangente para auxiliar os desenvolvedores na utilização da ponte e no entendimento do seu funcionamento.

## Recursos
 - Tranferência de token ERC-20 entre redes compatíveis.
 - Processo seguro para a quima de tokens.
 - Infraestrutura escalável para transferências de tokens entre blockchains.

## Visão Geral do Projeto

## EVM


## Server

### [contract-methods.js](https://github.com/brunowanderson7/bridge-evm/blob/main/server/contract-methods.js)

<details>
<summary> mintTokens </summary>

### `mintTokens(provider, contract, amount, address)`
Minta tokens no contrato fornecido. Esta função é responsável por criar novos tokens e atribuí-los a um endereço específico.

 - `provider`: O provedor Ethereum usado para interagir com a blockchain. 
 - `contract`: O contrato Ethereum usado para interagir com a blockchain.
 - `amount`: A quantidade de tokens a serem criados. 
 - `address`: O endereço para o qual os tokens serão criados. 

<br/></details>


<details>
<summary> transferToEthWallet </summary>

### `transferToEthWallet(provider, contract, amount, address)`
Transfere tokens para a carteira ETH. Esta função permite a transferência de tokens de um endereço para outro dentro da mesma blockchain.

 - `provider`: O provedor Ethereum usado para interagir com a blockchain. 
 - `contract`: O contrato Ethereum usado para interagir com a blockchain. 
 - `amount`: A quantidade de tokens a serem tranferidos. 
 - `address`: O endereço para o qual os tokens serão tranferidos.

<br/></details>


<details>
<summary> approveForBurn </summary>

### `approveForBurn(provider, contract, amount)`
Aprova a operação de queima de tokens. Esta função dá permissão para que uma quantidade específica de tokens seja queimada.

 - `provider`: O provedor Ethereum usado para interagir com a blockchain. 
 - `contract`: O contrato Ethereum usado para interagir com a blockchain. 
 - `amount`: A quantidade de tokens a serem tranferidos. 

<br/></details>


<details>
<summary> burnTokens </summary>

### `burnTokens(provider, contract, amount)`
Queima tokens da carteira. Esta função destrói uma quantidade especificada de tokens, removendo-os permanentemente de circulação.

 - `provider`: O provedor Ethereum usado para interagir com a blockchain. 
 - `contract`: O contrato Ethereum usado para interagir com a blockchain. 
 - `amount`: A quantidade de tokens a serem tranferidos. 

</details>  <br/>

### [event-watcher.js](https://github.com/brunowanderson7/bridge-evm/blob/main/server/event-watcher.js)

<details>
<summary>handleEthEvent</summary>

### `handleEthEvent(event, provider, contract)`
Lida com eventos relacionados à blockchain Ethereum. Verifica transferências de tokens em um contrato e realiza a mintagem dos tokens recebidos.

- `event`: O evento relacionado à transferência de tokens.
- `provider`: O provedor Ethereum usado para interagir com a blockchain.
- `contract`: O contrato Ethereum usado para interagir com a blockchain. 

A função handleEthEvent é chamada quando um evento relacionado à blockchain de origem é disparado.

<br/></details>

<details>
<summary>handleDestinationEvent</summary>

### `handleDestinationEvent(event, provider, contract, providerDest, contractDest)`
Lida com eventos relacionados à blockchain de destino. Verifica transferências de tokens em um contrato de destino e executa as operações de queima e transferência de tokens de volta para a cadeia de origem.

- `event`: O evento relacionado à transferência de tokens.
- `provider`: O provedor Ethereum usado para interagir com a blockchain Ethereum.
- `contract`: O contrato Ethereum usado para interagir com a blockchain Ethereum.
- `providerDest`: O provedor Ethereum usado para interagir com a blockchain de destino.
- `contractDest`: O contrato Ethereum usado para interagir com a blockchain de destino.

A função handleDestinationEvent é chamada quando um evento relacionado à blockchain de destino é disparado.

</details> <br/>

### `main ( )` [Incluso no arquivo event-watcher.js](https://github.com/brunowanderson7/bridge-evm/blob/main/server/event-watcher.js)

    const  originWebSockerProvider  =  new  Web3(process.env.ORIGIN_WSS_ENDPOINT)

    const  destinationWebSockerProvider  =  new  Web3(process.env.DESTINATION_WSS_ENDPOINT)

Cria duas instâncias `Web3`, uma do provedor origem e outra do provedor destino.

    originWebSockerProvider.eth.accounts.wallet.add(BRIDGE_WALLET_KEY)

    destinationWebSockerProvider.eth.accounts.wallet.add(BRIDGE_WALLET_KEY)

Adiciona a `Bridge Wallet` para assinar as transações.

    const  oriNetworkId  =  await originWebSockerProvider.eth.net.getId()

    const  destNetworkId  =  await destinationWebSockerProvider.eth.net.getId()

Faz chamadas assícrona para descobrir o `Id Chain` da rede em questão.

 

    const  originTokenContract  =  new  originWebSockerProvider.eth.Contract(
	  CHSD_ABIJSON.abi,
	  ORIGIN_TOKEN_CONTRACT_ADDRESS
    )
    const  destinationTokenContract  =  new destinationWebSockerProvider.eth.Contract(
	  QCHSD_ABIJSON.abi,
	  DESTINATION_TOKEN_CONTRACT_ADDRESS
	)

Cria a instância do contrato do token na rede origem `CHSD` e do token encapsulado na rede destino `D-CHSD` usando os endereçoes e a ABI dos mesmos.

    originTokenContract.events.Transfer().on('data',  async  (event)  =>  {
	  await  handleEthEvent(
		event,
		destinationWebSockerProvider,
		destinationTokenContract
	  )})

Esse trecho do código fica ouvindo o evento `Transfer` na blockchain de origem, quando esse evento acontece `.on('data'...)` é executado, nesse caso, aplicando a função de callback que invoca a `handleEthEvent( )` passando os parâmetros necessários.

    enter code heredestinationTokenContract.events.Transfer().on('data', async (event) => {
      await handleDestinationEvent(
        event,
        originWebSockerProvider,
        originTokenContract,
        destinationWebSockerProvider,
        destinationTokenContract
      )})
Similar ao trecho anterior, entretanto, esse fica ouvindo o evento na rede destino para realizar o processo inverso.







## Web