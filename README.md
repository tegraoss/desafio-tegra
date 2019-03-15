# Desafio Tegra
Bem vindo ao Desafio Tegra. Você pode fazer este teste da seguinte maneira:

- Frontend: Realizar somente a parte que consome a API
- Backend: Realizar somente a parte que cria a API
- Fullstack: Realizar ambas as partes.

Cada parte tem requisitos diferentes, porém ambas funcionam em conjunto. Abaixo você irá encontrar mais informações sobre ambas.

Estimamos que para cada um dos itens (Frontend ou Backend) seja necessário alocar cerca de 4 horas de trabalho para realizar a tarefa.

---

## Teste de Backend: Criar a API 

**Objetivo:**
Criar uma API para Busca de Voos.

**Premissas:**

- A API deve ser em Java 8 / Kotlin com SpringBoot ou  C# com .NET Core.
- Não é necessário utilizar banco de dados.
- Temos um [CSV da UberAir](uberair.csv) e um [JSON da 99Planes](99planes.json), ambos com uma lista de voos de cada operadora. Estes dois arquivos que serão a origem inicial dos dados.
- Um arquivo [JSON dos aeroportos](aeroportos.json) disponíveis.
- Os arquivos contém voos entre as data 10/02/2019 e 18/02/2019
- Eles estão na seguinte estrutura:

**UberAir**

| Campo | Formato
|--|--|
| numero_voo | Identificador do voo
| aeroporto_origem | Sigla 3 Dígitos
| aeroporto_destino | Sigla 3 Dígitos
| data | DATE
| horario_saida | TIME
| horario_chegada | TIME
| preco | decimal

**99Planes**

| Campo | Formato
|--|--|
| voo | Identificador do voo
| origem | Sigla 3 Dígitos
| destino | Sigla 3 Dígitos
| data | DATE
| saida | TIME
| chegada | TIME
| valor | decimal

**Objetivo:**
- Precisamos de 1 (um) endpoint em REST que receba o `Aeroporto de Origem`, `Aeroporto de Destino` e `Data do voo` e nos retorna um JSON com todos os voos disponíveis das duas operadoras (UberAir e 99Planes) obedecendo os critérios da busca, ordenados por horário.
- Precisamos de 1 (um) endpoint em REST que nos retorne a lista de todos os aeroportos para o Frontend poder utilizar para popular um SelectBox.
- Escalas de voo devem ser exibidas desde que o horário entre os dois voos (o tempo de espera) sejam inferiores a 12h. 
- O número máximo de escalas fica a seu critério.
- Será avaliado a solução do problema e qualidade do código.

**Exemplo de Response:**

```json
[
	{
		"origem": "GRU",
		"destino": "LOA",
		"saida": "YYYY-MM-DDTHH:mm:ss.sssZ",
		"chegada": "YYYY-MM-DDTHH:mm:ss.sssZ",
		"trechos": [
			{
				"origem": "GRU",
				"destino": "NYC",
				"saida": "YYYY-MM-DDTHH:mm:ss.sssZ",
				"chegada": "YYYY-MM-DDTHH:mm:ss.sssZ",
				"operadora": "UberAir",
				"preco": 1400.00
			},
			{
				"origem": "NYC",
				"destino": "LOA",
				"saida": "YYYY-MM-DDTHH:mm:ss.sssZ",
				"chegada": "YYYY-MM-DDTHH:mm:ss.sssZ",
				"operadora": "UberAir",
				"preco": 350.00
			}
		]
	}
]
```

**Extras:**

Caso deseje, você pode adicionar dependencias ou outros recursos que julgar necessário em seu código. Abaixo temos alguns exemplos, mas não fique limitado a eles:

- Documentação da API (Swagger, etc)
- Cache
- Docker

**Entrega:**
A entrega deve ser feita em um repositório do Bitbucket ou Github público, e este repositório deve conter:

- O Projeto
- Readme explicando as etapas necessárias para rodar ele.

---

## Teste de Frontend: Criar o Buscador

**Objetivo:**
Criar um SPA (Single Page Aplication) para Busca de Voos.

**Premissas:**
- O Projeto deve ser feito em React.
- Temos uma API que pode ser acessada no link `http://api-voadora.tegra.com.br`.
- A lista de aeroportos pode ser obtida com um GET da URL `https://api-voadora.dev.tegra.com.br/flight/companies`.
- A lista de voos por dia é um POST na `https://api-voadora.dev.tegra.com.br/flight`, com o Body seguindo este padrão em Json:
```json
{
	"from": "BSB",
	"to": "VCP",
	"date": "2019-02-10"
}
```
- Importante: Só existem dados na API do intervalo do dia 10/02/2019 ao dia 18/02/2019

**Objetivo:**

- Precisamos de uma tela onde o usuário possa selecionar o `Aeroporto de Origem`, `Aeroporto de Destino`, `Data de Saída`, através de Dropdowns ou Pickers.
- Será necessário após a busca, exibir a lista de voos, sejam eles diretos ou com escalas.
- Será necessário poder ordenar por Preço Total ou por Tempo Total de voo.
- É responsabilidade do Frontend calcular o preço total e o tempo total de voo, considerando as esperas entre as escalas.

**Extras:**

Caso deseje, você pode adicionar dependencias ou outros recursos que julgar necessário em seu código. Abaixo temos alguns exemplos, mas não fique limitado a eles:

- Typescript
- RxJs
- Redux
- Docker
- Testes Unitários
- CSS customizado
- Docker

**Entrega:**
A entrega deve ser feita em um repositório do Bitbucket ou Github, público, e este repositório deve conter:

- O Projeto
- Readme explicando as etapas necessárias para rodar ele.
