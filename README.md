# Desafio-DIO-Blockchain

Para este desafio, vamos construir um gerador de carteira de Bitcoin usando Node.js, importar a carteira gerada para o Electrum, e realizar transações de envio e recebimento de Bitcoin. Aqui estão os tópicos e os passos detalhados para realizar cada um deles:

1. Construir o nosso gerador de carteira de Bitcoin
Vamos utilizar a biblioteca bitcoinjs-lib para criar a carteira de Bitcoin. Primeiro, precisamos instalar as dependências necessárias:

npm init -y
npm install bitcoinjs-lib bip39 bip32


Depois, vamos criar um arquivo chamado wallet.js e adicionar o seguinte código:

const bitcoin = require('bitcoinjs-lib');
const bip39 = require('bip39');
const bip32 = require('bip32');

function generateWallet() {
    // Gerar uma frase mnemônica
    const mnemonic = bip39.generateMnemonic();
    console.log('Frase Mnemônica:', mnemonic);

    // Gerar a semente a partir da frase mnemônica
    const seed = bip39.mnemonicToSeedSync(mnemonic);

    // Gerar a chave mestre a partir da semente
    const root = bip32.fromSeed(seed);

    // Gerar o primeiro endereço de Bitcoin
    const { address } = bitcoin.payments.p2pkh({ pubkey: root.derivePath("m/44'/0'/0'/0/0").publicKey });
    console.log('Endereço Bitcoin:', address);

    // Retornar a chave privada em formato WIF (Wallet Import Format)
    const privateKey = root.derivePath("m/44'/0'/0'/0/0").toWIF();
    console.log('Chave Privada (WIF):', privateKey);
}

generateWallet();


2. Importar para um software gerenciador de carteiras (Electrum)
Com a carteira gerada, vamos importar os dados para o Electrum. Para isso, siga os passos abaixo:

Abrir o Electrum: Inicie o Electrum no seu computador.

Criar uma nova carteira:

Selecione "File" > "New/Restore".
Digite um nome para a nova carteira.
Selecione "Standard wallet".
Importar chave privada:

Selecione "Use a master key".
Cole a chave privada (WIF) gerada anteriormente e clique em "Next".
Siga as instruções para concluir a criação da carteira.
3. Realizar transações de envio e recebimento de Bitcoin
3.1. Enviar Bitcoin
Para enviar Bitcoin, você precisará de uma transação. No Electrum, siga os passos abaixo:

Acessar a aba "Send":

No Electrum, vá para a aba "Send".
Preencher os detalhes da transação:

No campo "Pay to", insira o endereço do destinatário.
No campo "Amount", insira a quantidade de Bitcoin a ser enviada.
Opcionalmente, ajuste a taxa de transação.
Assinar e enviar a transação:

Clique em "Send".
Confirme os detalhes e assine a transação com sua senha.
A transação será transmitida para a rede Bitcoin.
3.2. Receber Bitcoin
Para receber Bitcoin, você precisará fornecer um endereço de recebimento:

Acessar a aba "Receive":

No Electrum, vá para a aba "Receive".
Gerar um novo endereço:

Clique em "New Address" para gerar um novo endereço de recebimento.
Forneça este endereço ao remetente para que ele envie os Bitcoins para você.
4. Explorar transações com um explorador de blocos
Para verificar o status das suas transações, você pode usar um explorador de blocos, como o Blockchair. Siga os passos abaixo:

Obter o ID da transação:

No Electrum, vá para a aba "History" e encontre a transação que você deseja verificar.
Clique com o botão direito na transação e selecione "Details" para obter o ID da transação.
Verificar no explorador de blocos:

Acesse o site do Blockchair ou outro explorador de blocos de sua preferência.
Cole o ID da transação na barra de pesquisa e visualize os detalhes da transação.
Seguindo esses passos, concluímos o desafio de criar e utilizar uma carteira de criptomoedas.
