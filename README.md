# Architecture Challenge

## 1-	O problema

É necessário elaborar uma solução que ofereça armazenamento, processamento e disponibilização de dados, sempre considerando que tudo deve estar conforme as boas práticas de segurança em TI. Afinal, nosso principal ativo são dados sensíveis dos consumidores brasileiros.

## 2-	Armazenamento
Vamos supor que existam três grandes bases de dados externas que organizam nossas informações. A primeira delas, que chamamos de Base A, é extremamente sensível e deve ser protegida com os maiores níveis de segurança, mas o acesso a esses dados não precisa ser tão performática. A segunda, é a Base B que também possui dados críticos, mas ao contrário da Base A, o acesso precisa ser um pouco mais rápido. Uma outra característica da Base B é que além de consultas ela é utilizada para extração de dados por meio de algoritmos de aprendizado de máquina. A última base, é a Base C, que não possui nenhum tipo de dado crítico, mas precisa de um acesso extremamente rápido.

##

# Solução:
### Base A: Oracle Database 


Oracle Database fornece uma camada de segurança muito maior por estar a tanto tempo no mercado.
Já se estabeleceu e é utilizada por grandes empresas a muitos anos, tendo muitas 
melhorias de segurança e performance já implantados, favorecendo o uso deste DB 
quando o quesito é segurança e transações por segundo.


### Base B: Postgres
 

Como acesso e performance é importante, Postgres oferece múltiplas interfaces de consumo de 
dados menos engessado como o Oracle Database, se tornando ideal tanto para consumo de 
aprendizado de máquina como para Big Data.


### Base C: MongoDB

```bash
NoSQL supera Oracle DB e Postgres em velocidade mas não oferece um sistema de segurança tão 
forte quanto os banco de dados relacionais e por isso mesmo é possível fazer um acesso muito 
mais rápido a estes dados. Por não conter dados críticos, é uma opção viável.
```

# 3-	Tráfego

### Base A: Python


Python através da lib cx_oracle acessa o Banco A para consumo dos dados. 
Geralmente utilizando um campo chave que pode ser neste caso o CPF, recupera 
e retorna em JSON ou qualquer outro formato necessário os dados recuperados.

Exemplo:

```bash
{
	“id”: 87623,
	“cpf”:00000000000,
	“name”: “John Doe”,
	“address”: “Rua das Araucárias 620”,
	“debts”: [
			{
				“id”: 1,
				“status”: “Ativa”,
				“value”: 1000.67,
				“company”: “SUBMARINO VIAGENS LTDA”,
				“cnpj”: 06179342000105}

				{“id”: 2,
				“status”: “Ativa”,
				“value”: 367.56,
				“company”: “C&A MODAS S.A”,
				“cnpj”: 45242914017253
			}
		]
}	

```


### Base B: Python

Python continua sendo uma ótima opção por ser de rápida interpretação, utilizada para trabalhar 
grandes volumes de dados e também facilitar a leitura do código.
Conectando ao banco Postgres via psycopg2 é possível trabalhar com os dados necessários 
e também os exportar em JSON ou da forma como for mais dinâmico para seu consumo.
No caso, passando a chave CPF, podemos retornar um JSON das informações, como no exemplo da Base A.

Exemplo:

```bash
{
	“cpf”: 00000000000,
	“age”: 26,
	“assets_properties”: [
				{
					“type”: “car”,
					“market_value”: 30000,
					“acquisition_year”: 2017
				},
	“address”: “Rua das Araucárias 620”,
	“income_value”: 4300,
	“source_income”: “salary”
}
```

### Base C: Python


Para trabalhar este DB basta utilizarmos a lib MongoEngine. 
Em poucas linhas de códigos podemos conectar ao banco e realizar uma 
query semelhante ao SQL, deixando o seu uso e manutenção simplificado para o time de engenharia.
Por Python ser tão dinâmico, é possível para os 3 tipos diferentes
 de banco, corresponder a resultados da forma que for mais eficiente para seu consumo.

# 4-	Disponibilização dos Dados

Podemos disponibilizar cada informação agregada com um microserviço em Flask que recupera estas informações. Sua disponibilização pode ser feita de diversas maneiras como retornar um JSON das informações compiladas seja de 3, 2 ou 1 banco apenas.
Dependendo do uso final, é possível trabalhar diferentes endpoints para disponibilização dos dados como:

```bash
SOAP (xml)
REST (json)
```
Estes dois meios são os comuns entre serviços e brandamente aceitos para consumo em diferentes sistemas.

##
\
[README.md](http://www.giuthub.com/fredbrowne/arquitecture_challenge)



