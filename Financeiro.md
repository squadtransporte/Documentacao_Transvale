| Versão | Modificado por | Alterações |
| --- | --- | --- |
| 1 | Matheus Gobo | Juntando documentação de Geração de Adiantamentos com a nova integração de montagem e execução de processo de caixa |

# Sumário

[Insere Adiantamento](#insere-adiantamento)

[Monta ou Executa Processo de Caixa](#monta-ou-executa-processo-de-caixa)

---

## Insere Adiantamento

Este método gera um adiantamento no maxys, em seguida monta o processo de caixa do adiantamento, e caso informado os dados necessários, executa o processo de caixa.

**Método**: POST

**Rota:** financeiro/postGerarAdiantamento

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
| dadosPagamento | digitoConta | N | varchar2(2) | Digito Verificador da Conta |
| dadosPagamento | chavePix | N | varchar2(77) | Chave pix cadastrada para o clifor no TCF001. |
| Principal | baixaAutomatica | N | Objeto |  |
| baixaAutomatica | dataMovimento | N | Date | Data que foi efetuada a baixa do processo de caixa. |
| baixaAutomatica | historicoBaixa | N | Number(5) | Código do histórico da baixa. |

**Exemplo de Request:**

```json
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
    "conta": "1212",
    "digitoConta": "12",
    "chavePix": null
  },
  "baixaAutomatica": {
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

```json
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

---

---

## Monta ou Executa Processo de Caixa

### Este Método irá Montar e Executar processos de caixa para Notas ou Adiantamentos.

1. Poderá ser somente montado o processo de caixa, sem necessidade de execução.
2. Não é obrigatório enviar Contas a Pagar e Receber, com apenas um dos dois já será possível montar/executar o processo.

---

**Método:** POST

**Rota:** financeiro/postMontaExecProcCaixa

---

**Relação de Campos - Body Request.**

| Nível | Campo | Obrigatório | Tipo de Dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | cdEmpresa | S | Number | Código da empresa de execução do processo |
| Principal | cpfCnpjUsuario | S | String | CPF/CNPJ do Usuário de Montagem ou Execução |
| Principal | cpfCnpjFavorecido | S | String | CPF/CNPJ do favorecido do processo |
| Principal | dataVencimento | N | String | Data de Vencimento/Pagamento do processo. Se não vier pega dos parâmetros de caixa. Caso não tenha será a Data Atual (SYSDATE). Formato YYYY/MM/DD |
| Principal | cdFormaPagto | N | String | Forma de pagamento, se não informado Default “DI” |
| Principal | cdTipoPedido | S | String | Tipo de pedido relacionado ao FCT001 no ANV008. Obs: Cadastrar um especifico para integração, para poder rastrear origem do processo posteriormente. |
| Principal | pagamentos |  | Array Object |  |
| pagamentos | cdEmpresa | S | Number | Empresa do documento a Pagar |
| pagamentos | cdClifor | S | Number | Clifor do adiantamento |
| pagamentos | nrLancamento | S | Number | Número do lançamento do contas |
| pagamentos | cdTipoCtaPagRec | S | Number | Tipo de contas “Ex: 220” |
| pagamentos | nrParcela | S | Number | Número da parcela ”Ex: 0”   |
| pagamentos | vlUtilizado | N | Number | Valor utilizado do contas. Obs: Se não vier será utilizado todo saldo restante |
| Principal | recebimentos |  | Array Object |  |
| recebimentos | cdEmpresa | S | Number | Empresa do documento a receber |
| recebimentos | cdClifor | S | Number | Clifor do adiantamento |
| recebimentos | nrLancamento | S | Number | Número do lançamento do contas |
| recebimentos | cdTipoCtaPagRec | S | Number | Tipo de contas “Ex: 220” |
| recebimentos | nrParcela | S | Number | Número da parcela ”Ex: 0”   |
| recebimentos | vlUtilizado | N | Number | Valor utilizado do contas. Obs: Se não vier será utilizado todo saldo restante |
| Principal | execucao | N | Object |  |
| execucao | operacao | S - caso for executar | String | Tipo de operação para baixa, aceitos somente (D - Dinheiro ou B - Banco) |
| execucao | cdHistorico | S - caso for executar | Number | Código do Histórico da baixa |

## JSON Exemplo Body Request

```json
{
	"cdEmpresa": 10,
	"cpfCnpjUsuario": "9813913931",
	"cpfCnpjFavorecido": "9139319139",
	"dataVencimento": "2024/10/18",
	"cdFormaPagto": "CA",
	"cdTipoPedido": "IP",
	"pagamentos": [
		{
			"cdEmpresa": 10,
			"cdClifor": 1389,
			"nrLancamento": 8319,
			"cdTipoCtaPagRec": 230,
			"nrParcela": 0,
			"vlUtilizado": 129.90
		},
		{
			"cdEmpresa": 10,
			"cdClifor": 132,
			"nrLancamento": 991,
			"cdTipoCtaPagRec": 230,
			"nrParcela": 0
		}
	],
	"recebimentos": [
		{
			"cdEmpresa": 10,
			"cdClifor": 1389,
			"nrLancamento": 8319,
			"cdTipoCtaPagRec": 230,
			"nrParcela": 0,
			"vlUtilizado": 200.90
		},
		{
			"cdEmpresa": 10,
			"cdClifor": 132,
			"nrLancamento": 991,
			"cdTipoCtaPagRec": 230,
			"nrParcela": 0
		}
	],
	"execucao": {
		"operacao": "D",
		"cdHistorico": 647
	}
}
```

---

**Relação de Campos - Response Sucesso**

| Campo | Tipo de Dado | Descrição |
| --- | --- | --- |
| code | Number | Código do Response |
| message | String | Mensagem do Response |
| cdEmprProc | Number | Empresa do Processo de caixa |
| nrProcessoPagamento | Number | Número do processo de caixa de Pagamento |
| nrProcessoRecebimento | Number | Número do processo de caixa de Recebimento |
| nrLoteProcesso | Number | Número do Lote de execução do Processo |
| nrLoteExterno | Number | Quando processo é Somente Montado é inserido o Número de lote Externo |

**Relação de Campos - Response Erro**

| Campo | Tipo de Dado | Descrição |
| --- | --- | --- |
| code | Number | Código do Response |
| message | String | Mensagem do Response |
| detalhe | String | Detalhes da Mensagem |

## JSON Exemplo Response

---

Possíveis Códigos de Retorno

| Código | Descrição |
| --- | --- |
| 200 | Sucesso na transação |
| 400 | Erro ao montar/executar Processo de Caixa. Verificar a tag message. |

### 1 - Processo de caixa somente Montado

```json
{
    "code": 200,
    "message": "Sucesso",
    "cdEmprProc": 84,
    "nrProcessoRecebimento": 160382,
    "nrLoteExterno": 8
}
```

### 2 - Processo de caixa Executado

```json
{
    "code": 200,
    "message": "Sucesso",
    "cdEmprProc": 84,
    "nrProcessoPagamento": 160379,
    "nrProcessoRecebimento": 160380,
    "nrLoteProcesso": 360023
}
```

### 3- Erro

```json
{
	"code": 400,
	"message": "Usuário com CPF/CNPJ (00882770000115) não encontrado, Verifique!",
	"detalhe": "¥[MONTA_EXEC_PROCCAIXA]¥ Usuário com CPF/CNPJ (00882770000115) não encontrado, Verifique!¢MPM=MAX033803¢"
}
```
