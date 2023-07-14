#Notas

Ao obtermos os arquivos do desafio nos é dado um arquivo “docrypt”,nos é dito que ele é utilizado para decriptar os arquivos sample.cry e test.cry o qual nos foi dado as credenciais.

Ao explorarmos o binário do arquivo docrypt nos é percebido que ele chama uma função chamada de “authorize”, essa função é carregada dinamicamente.

Investigando a biblioteca dinâmica libauth.so, podemos encontrar a função “authorize”, para burlar a autenticação do docrypt, precisamos carregar o símbolo não resolvido do docrypt para uma função nossa, assim alterando a função do script, fazendo então uma função que sempre vai retornar que a autenticação foi um sucesso.

Para fazer essa função podemos simplesmente programá-la em C e depois compilar para gerar um .so.
podemos carregá la com o executável usando o seguinte comando: 

`LD_PRELOAD=$diretório/preload.so $diretorio/docrypt $diretorio/sample.cry`

Recomendamos entrar no diretório `resolution` e rodar o comando `make`

O comando irá automaticamente compilar o arquivo preload.c e carregar o simbolo no arquivo docrypt antes de sua execução


Depois de rodado, podemos colocar qualquer credencial, não seremos barrados pela autenticação. Falta então descobrir qual é a chave de encriptação.

Abrindo o binario do arquivo encrypt, podemos perceber uma variável chamada `encrypt_key` na seção .rodata, se jogarmos o código em ferramentas como o IDA, ele irá nos mostrar que o valor estático dessa variável é “easy”

Tambem podemos simplesmente olhar no código hexadecimal e ver qual é o valor da variavel

