- Dados: Conteúdo real armazenado nos bancos
- Metadados: Informações sobre a estrutura dos bancos de dados (dados sobre os dados)
- Índices: Estruturas que permitem rápido acesso aos dados
- Bloco: Determina a transferência de dados entre o disco e a memória principal
- Buffer: Região da memória principal na qual os blocos podem ser transferidos
## Processador de consultas
- Responsável por compilar e executar consultas
### Compilador 
- Analisador de consultas: Constrói estrutura em árvore da consulta
- Pré-Processador: Verificações semânticas $\to$ Operadores algébricos
- Otimizador: Define qual a melhor sequência de operações (baseada no tempo)

### Mecanismo de Execução
- Coloca os dados necessários à execução da consulta no buffer
- Interage com o scheduller (controle de concorrência) para evitar acesso a dados bloqueados
- Registro das operações no log
### Propriedades ACID
- Garantem a estabilidade e confiabilidade nas consultas
	- *Atomicidade* $\to$ Tudo ou nada
	- *Consistência* $\to$ Mantém a integridade dos dados
	- *Isolamento* $\to$ Transações devem ser idependentes
	- *Durabilidade* $\to$ As transações persistem no banco após falhas
### Armazenamento de dados
- Primário $\to$ Na memória RAM
- Secundário $\to$ No disco magnético (maioria)
- Blocos de Armazenamento $\to$ Registros são armazenados em blocos no disco e operações envolvem mover esses blocos entre Memória RAM e Disco
### Operações de acesso a Arquivos
- Abertura, leitura, escrita, modificação e  fechamento de arquivos envolvem diversos passos, como localizar o bloca correto, carregar para o buffer, modificar e gravar novamente em disco
### Organização de arquivos
- Os arquivos podem ser organizados de várias maneiras:
	- Heap (não ordenado)
	- Sequencial (ordenado)
	- Hashed (utilizando funções hash)
	- Árvores B.
### Estrutura de Registros
- Registros podem possuir comprimento fixo ou variável, podem incluir também campos compostos e multivalorados
### Movimento entre Disco e Buffer
- Ao mover um bloco da memória principal, os ponteiros para o endereços precisam ser ajustados para garantir que apontem corretamente tanto na memória quanto no disco
