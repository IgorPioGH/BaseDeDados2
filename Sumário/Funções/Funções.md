- Antes de rodar uma função é necessário instalar o _PL/pgSQL_ no banco de dados
	- createlang plpgsql -U _usuário_ -h _servidor_ _banco_
## Definição de uma função
- É possível sobrecarregar funções, para elas lidarem com diferentes tipos e quantidades de parâmetros
- Definição de uma função simples:
```
CREATE OR REPLACE FUNCTION nom_funcao (nome_param tipo_param, nome_param2 tipo_param2)
RETURNS tipo_retorno AS
$$
	DECLARE 
		nome_var tipo_var;
		nome_var tabela.coluna%TYPE;
		var_registro tabela%ROWTYPE
	BEGIN
		instrução;
		RETURN valor_retorno;
	END;
$$
LANGUAGE 'plpgsql';
```
### Exemplo 1:
```
CREATE OR REPLACE FUNCTION media (NUMERIC, NUMERIC)
RETURNS NUMERIC AS
$$
	DECLARE
		result NUMERIC;
	BEGIN
		result = ($1+$2)/2;
		RETURNS result;
	END;
$$
LANGUAGE 'plpgsql';
```
### Exemplo 2:
```
CREATE OR REPLACE FUNCTION altera_salario(p_codigo Func.codigo%TYPE, p_aumento Func.salario%TYPE)
RETURNS boolean AS
$$
	DECLARE
		v_nome Func.nome%TYPE
		v_salario Func.salario%TYPE
	BEGIN
		SELECT INTO v_nome, v_salario nome, salrio FROM Func WHERE codigo = p_codigo;
		RAISE NOTICE 'nome: %, v_nome;
		RAISE NOTICE 'salario atual: %', v_salario;
		v_salario = v_salario + p_aumento;
		RAISE NOTICE 'novo salario: %', v_salario;
		UPDATE Func SET salario = v_salario WHERE codigo = p_codigo;
		RETURN 't';
	END;
$$
LANGUAGE 'plpgsql';
```
## Executando uma função
- SELECT nome_funcao(param);
## Excluindo uma função
- DROP FUNCTION nome_funcao(param);
## Condicionais
### IF THEN ELSE
```
...
BEGIN
	IF (condicao) THEN
		....
	ELSE
		....
	END IF;
...
```

### LOOP
```
...
BEGIN 
	LOOP 
		...
		EXIT WHEN (condição);
	END LOOP;
...
```
### LOOP + IF
```
...
BEGIN 
	LOOP
		...
		IF (condição) THEN EXIT;
		END IF;
	END LOOP;
...
```

### WHILE
```
...
BEGIN
	WHILE (condição) LOOP
		...
	END LOOP;
...
```

### Estruturas de Repetição
#### FOR IN
```
FOR v_controle IN valor_inicio valor_final LOOP
	...
END LOOP;
```

#### FOR IN SELECT 
```
FOR v_controle IN SELECT ... LOOP
	...
END LOOP;
```

#### Exemplo FOR IN
```
CREATE OR REPLACE FUNCTION contador_cli()
RETURNS BOOLEAN
AS $$
	DECLARE 
		registro RECORD;
		qtde INTEGER;
	BEGIN
		qtde =0;
		FOR registro IN SELECT * FROM Cliente LOOP
			qtde = qtde +1;
			RAISE NOTICE 'nome: %, cidade: %', registro.nome, registro.cidade;
		END LOOP;
		RETURN 't';
	END;
$$
LANGUAGE 'plpgsql';
```