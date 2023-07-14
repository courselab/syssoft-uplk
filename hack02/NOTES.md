# Notas

# 2. Resolução

## 2.b) Explicação do exploit

O exploit funciona da seguinte maneira: 

Ao declarar variáveis o SO aloca a memória necessária para aquela variável. Então ao declarar um array de caracteres de 4 bytes, o SO irá reservar 4 bytes na pilha para aquela variável. 

Ao inserirmos valores nessa variável ela é armazenada de maneira que seu conteúdo desça na pilha (aumente o endereço da memória)

Porém se tentarmos colocar 5 valores, sobrescrevemos 1 byte que não deveríamos ter acesso

O exploit consiste então em sobrescrever todo o conteúdo da pilha até chegar no endereço de retorno e sobrescrever aquele endereço por alguma coisa que nós queiramos. 

Como por exemplo um endereço de retorno de algum arquivo ou função a


## 2.c) Explicação dos mecanismos de proteção

### O Address-Space Layout Randomization: 

Tem por objetivo tornar imprevisível onde cada parte do programa será carregado na memória. 

Ao iniciar um processo o sistema operacional gera aleatoriamente valores de deslocamento (offsets) que são aplicados a cada parte do programa. 

Esses deslocamentos aleatórios são adicionados aos endereços base predefinidos de cada parte do programa para determinar sua posição final na memória. 

Como os deslocamentos são gerados aleatoriamente a cada execução, o layout do espaço de endereçamento será diferente a cada vez que o programa é executado.

### O Canario:

O intuito do canário é proteger o programa de ataques de stack overflow. 

O canário é colocado logo depois do endereço de retorno armazenado na pilha. 

O valor do canário é decidido de maneira aleatória pelo Kernel.

Quando o programa termina uma função de está prestes a fazer o retorno, o programa então checa o valor do canário para saber se o valor foi sobrescrito para então terminar a execução do programa.

