# SmartContract - teste

Este projeto conta com três arquivos .zip.

**SmartContract.zip**: Implementação da classe “Blockchain” utilizando a classe de contrato gerada pelo Web3j.

**Exemplo.zip**: Exemplo de como utilizar a classe “Blockchain”.

**libs.zip**: Libs necessárias para o funcionamento dos projetos.

Para conseguirmos firmar um contrato e enviá-lo para uma Blockchain necessariamente precisamos de três itens, sendo eles: um endereço de uma rede que implemente uma Blockchain, uma carteira Ethereum, e um modelo de contrato.

Abaixo veremos exemplos e formas de criar cada um dos itens necessários. É importante termos em mente que as formas descritas abaixo não são os únicos meios de se conseguir cada um dos três itens, contudo são os mais comuns e com o melhor custo benefício.

![](https://i.ibb.co/bBLSQ5d/sample.jpg)

**Importante!** Os arquivos SmartContract.zip e Exemplos.zip, já possuem um modelo de contrato implementado, sendo assim, caso opte por usar um destes projetos como base, apenas a carteira e o endereço da rede são necessários, desta forma a geração do modelo de contrato só é necessária caso opte por outra linguagem de programação, ou um modelo de contrato diferente do proposto.

## Rede Blockchain
Para que possamos enviar nosso SmartContract para a Blockchain, precisamos de um endereço de uma Blockchain, para isso existem várias, públicas e privadas, pagas e gratuitas, inclusive podemos criar um servidor local para tal função. Em nosso exemplo vamos utilizar um site chamado Infura, que disponibiliza algumas redes e até alguns gráficos para análise de tráfego. Então, vamos ao passo a passo.
1. Acesse o site [infura.io](https://infura.io/) e crie um conta utilizando seu e-mail;
2. Acesso o [dashboard](https://infura.io/dashboard) da plataforma onde haverá uma opção para criar um projeto;
3. Ao criar um projeto, haverá a possibilidade de selecionar o “ENDPOINT”, nesse caso utilizaremos a opção “ROPSTEN”;
4. Feito isso já é possível copiar o endereço da nossa Blockchain, que servirá futuramente para envio dos nossos contratos.

![](https://i.ibb.co/ZxQnZv6/infura.png)

## Carteira Ethereum
É o endereço da carteira que servirá de remetente do contrato, também é dela que será debitado o valor das taxas de mineração provenientes do envio do contrato.

Da mesma forma que a rede Blockchain, existem várias formas para adquirir uma carteira, porém é necessário que ela seja criada na mesma rede do Blockchain, nesse caso “ROPSTEN”, caso contrário a carteira não existirá dentro da rede.
Outro detalhe muito importante é que iremos precisar da chave privada da carteira, e nem todos os sites disponibilizam essa informação, então antes de creditar valores na carteira criada, certifique-se que será possível obter a chave privada da carteira, pois sem ela não conseguiremos enviar nosso contrato para a Blockchain.

Para tal utilizaremos o MetaMask para criação da carteira e o Faucet para conseguir alguns créditos de Ether. Então vamos ao passo a passo.
1. Utilizando o Google Chrome, acesse o [Chrome Web Store](https://chrome.google.com/webstore/category/extensions) e instale a extensão [MetaMask](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn); 

![](https://i.ibb.co/Th2hcHb/metamask-chrome.png)

2. Acesse a extensão instalada e siga os passos para criação da carteira;

**Importante!** Na etapa de frase de backup, copie e salve a frase em algum outro lugar, pois ela será necessária no futuro.

3. Após a criação da carteira, **selecione a mesma rede selecionada no Infura**, neste caso “ROPSTEN”;

![](https://i.ibb.co/4F04b9M/metamask.png)

4. Ainda com o MetaMask aberto, acesse o [Faucet](https://faucet.metamask.io/) para obter alguns créditos;
5. No Faucet, clique em “request 1 ether from faucet”, e confirme as solicitações que surgirão (esta etapa pode demorar alguns minutos, até que a transação seja minerada);
6. Tendo os créditos na carteira, clique em “Detalhes”, como mostrado na imagem acima e utilize a opção “Exportar Chave Privada”, informe a senha criada nos primeiros passos e copie a chave exibida, é esta chave que precisaremos futuramente.


## Modelo de Contrato
Para criar o modelo do contrato, precisaremos criar um script na linguagem “sol”. É possível personalizar o modelo de contrato de infinitas formas, porém utilizaremos um modelo bem simples que será disponibilizado abaixo.

Utilizaremos a biblioteca Web3j para envio do contrato, esta biblioteca funciona em java, porém existe para várias outras linguagens, porém caso opte por outra linguagem, a geração da classe deve ser adaptada para a linguagem selecionada. 
Então, vamos ao passo a passo.

1. Acesse o site do [Remix](https://remix.ethereum.org/) e no editor que abrirá, cole o script abaixo;

> pragma solidity ^0.4.0;
>
> contract Hello
> {
>     string private valor = "hello world";
>     
>     function getValor() public returns(string)
>     {
>         return valor;
>     }
>     function setValor(string a) public returns(bool)
>     {
>         valor = a;
>         return true;
>     }
> }

2. Observe que o script exige a versão do compilador 0.4.0, então selecione esta opção no menu à direita;

![](https://i.ibb.co/W3pwx72/remix-1.png)

3. Após compilar utilize a opção “ABI” para copiar o código, e crie um arquivo com o nome “SmartContract.abi”, com o conteúdo copiado, em uma pasta de sua preferência;
4. Utilize a opção “Bytecode” para copiar o código, e crie um arquivo com o nome “SmartContract.bin”, como conteúdo copiado, juntamente com o arquivo criado na etapa anterior;

![](https://i.ibb.co/QKfyQVf/remix-2.png)

5. Faça download do [Web3j](https://github-production-release-asset-2e65be.s3.amazonaws.com/67328052/363b3e80-723b-11e9-97de-2c808160e444?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20190609%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20190609T210215Z&X-Amz-Expires=300&X-Amz-Signature=1f9bbf418f40da9002fa2fe3f03f81f64f517bd84ae7e3ff43b5ec81212825d7&X-Amz-SignedHeaders=host&actor_id=0&response-content-disposition=attachment%3B%20filename%3Dweb3j-4.3.0.zip&response-content-type=application%2Foctet-stream) que servirá para gerar a nossa classe java do contrato (a partir desta etapa, adaptações devem ser feitas de acordo com a linguagem);
6. Descompacte o conteúdo do zip em um diretório de sua preferência, e através do cmd acesse a pasta “\web3j-4.3.0\bin”
7. Ainda no cmd, execute o comando:

`web3j.bat solidity generate --binFile=[diretorio_completo]\SmartContract.bin --abiFile=[diretorio_completo]\SmartContract.abi -o [diretorio_completo] -p SmartContract`

Substituindo `[diretorio_completo]` pelo diretório onde os arquivos .bin e .abi foram criados.

**Importante!** O parâmetro `-o [diretorio_completo]` determina onde a classe será gerada.

8. Acesse a classe SmarContract.java gerada e altere o conteúdo da variável BINARY, deixando apenas o conteúdo do “object”, como no exemplo abaixo;

Alterar isto:
 
![](https://i.ibb.co/tQXrBRt/java-1.png)

Para isto:

![](https://i.ibb.co/RhPpFm8/java-2.png)
 

Pronto, agora já temos todo o necessário para implementação dos contratos inteligentes.

As lib’s necessárias para utilização da classe se encontram no arquivo libs.zip, juntamente com exemplos de códigos para implementação.

Este tutorial foi baseado [neste](https://github.com/HenryNunes/EthereumTutorial) projeto.
