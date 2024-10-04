### Exercício 1
![[Pasted image 20241003194146.png]]
#### Resolução 1
- Ordem de "índices do bloco":
	- Cabeçalho $\to$ Ponteiros (p/ Variaveis ou composto) $\to$ Atributos compri. fixo $\to$ Atributos compri. var. $\to$ Atri. multivalorados
![[Pasted image 20241003201656.png]]
![[Pasted image 20241003201709.png]]
![[Pasted image 20241003201721.png]]
- Cada bloco livre "perde" o número de bytes do cabeçalho
- E cada registro tem + 1 byte do ponteiro para ele
- O número de registros por blocos é truncado, pois não se cabem 14.7 registros por bloco não há espaço o suficiente para 15 registros
- E o número de blocos necessários independentemente do valor da casa decimal é adicionado mais um, já que se são necessários 14.3 blocos, vamos precisar utilizar 15 blocos, pois blocos são inteiros.