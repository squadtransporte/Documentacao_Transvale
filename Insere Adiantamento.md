# Insere Adiantamento

Este método gera um adiantamento no maxys, em seguida monta o processo de caixa do adiantamento, e caso informado os dados necessários, executa o processo de caixa.

**Método**: POST

**Rota:** ProcessoCaixa/postProcessoCaixa

**Relação de campos - Request**

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | empresa | S | Number(4) | Código da empresa utilizado no maxys. |
| Principal | cpfCnpjFavorecido | S | Number(14) | CPF/CNPJ do favorecido do adiantamento. |
| Principal | dataLancamento | S | Date | Data de lançamento. |
| Principal | dataVencimento | S | Date | Data de vencimento. |
| Principal | dataPrevVencimento | S | Date | Data prévia de vencimento. |
| Principal | dataPagamentoProcesso | S | Date | Data de pagamento do Processo. |
| Principal | dataInicioCorrecao | S | Date | Data do início da correção |
| Principal | valorAdiantamento | S | Number(15,3) | Valor do adiantamento. |
| Principal | cdFormaPagto | S | Varchar2(2) | Código da forma de pagamento. |
| Principal | historico | S | Number(5) | Código do histórico contábil utilizado no maxys. |
| Principal | negocio | S | Number(4) | Código do negócio utilizado no maxys. |
| Principal | tipoPedido | S | Varchar2(2) | Tipo de pedido cadastrado no TFN011. |
| Principal | tipoAdiantamento | S | Number(5) | Tipo de contas pagamento/receber. |
| Principal | observacao | S | Varchar2(500) | Observação. |
| Principal | dadosPagamento | N | Objeto |  |
| dadosPagamento | banco | N | Number(3) | Código do banco cadastrado para o clifor no TCF001. |
| dadosPagamento | agencia | N | Number(6) | Código da Agência cadastrada para o clifor no TCF001. |
| dadosPagamento | conta | N | varchar2(10) | Número da conta cadastrada para o clifor no TCF001. |
| dadosPagamento | chavePix | N | varchar2(77) | Chave pix cadastrada para o clifor no TCF001. |
| Principal | baixaAutomatica | N | Objeto |  |
| baixaAutomatica | dataMovimento | N | Date | Data que foi efetuada a baixa do processo de caixa. |
| baixaAutomatica | historicoBaixa | N | Number(5) | Código do histórico da baixa. |

**Exemplo de Request:**

```jsx
{
  "empresa": 84,
  "cpfCnpjFavorecido": "65922391000147",
  "dataLancamento": "30/08/2024",
  "dataVencimento": "30/08/2024",
  "dataPrevVencimento": "30/08/2024",
  "dataPagamentoProcesso": "30/08/2024",
  "dataInicioCorrecao": "30/08/2024",
  "valorAdiantamento": 12300,
  "cdFormaPagto": "CC",
  "historico": 1100,
  "negocio": 1,
  "tipoPedido": "AC",
  "tipoAdiantamento": 108,
  "observacao": "TESTE OBSERVAÇÃO",
  "dadosPagamento": {
					  					"banco": 341,
					  					"agencia": 3838,
					  					"conta": 1212,
					  					"chavePix": null
										},
  "baixaAutomatica":{
					  					"dataMovimento": "30/08/2024",
					  					"historicoBaixa": 1
										}
}
```

**Relação de Campos → Response**

| **Campo** | **Tipo de Dados** | **Observação** |
| --- | --- | --- |
| code | Number(3) | Código de retorno |
| message | String(4000) | Mensagem de retorno |
| nrProcessoCaixa | Number(8) | Número do processo caixa gerado/baixado. |

**Exemplo de Response**

```jsx
{
	"code": 200,
	"message": "Sucesso",
	"nrProcessoCaixa": 126301
}
```

**Possíveis códigos de erro**

| Código | Descrição |
| --- | --- |
| 200 | Sucesso na transação |
| 404 | Erro ao montar/executar processocaixa. |
| 500 | Erro interno do servidor. Verificar a tag message. |