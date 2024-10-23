| Versão | Modificado por | Alterações |
| --- | --- | --- |
| 1 | Frederico Ferro | Juntando documentação de consulta de notas e criada nova para geração de notas fiscais |

# Sumário

[Listar todas os documentos do MaxysXML](#listar-todas-os-documentos-do-maxysXML)

[Emite Nota Fiscal](#emite-nota-fiscal)

---
# Listar todas os documentos do MaxysXML

Esse método permite consultas todas as notas que existem no MaxysXML.

**Método:** GET

**Rota:** /integrador-transvale/notaFiscal/getNotaCompleta?limit={limit}&page={page}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | limit | S | Number | Número de Registros |
| Principal | page | S | Number | Número de Páginas |
| Principal | numeroChaveAcesso | N | String(32000) | Chave(s) de acesso(s) da nota fiscal |
| Principal | cliforPagador | N | String(60) | Clifor do Pagador |
| Principal | cliforOrigem | N | String(60) | Clifor de Origem |
| Principal | cliforDestino | N | String(60) | Clifor de Destino  |
| Principal | cliforExpedidor | N | String(60) | Clifor do Expedidor  |
| Principal | cliforRecebedor | N | String(60) | Clifor do Recebedor |
| Principal | descProduto | N | String(60) | Descrição do Produto |
| Principal | numeroNCM | N | String(255) | Ncm do Produto |
| Principal | dataInicio | N | String(60) | Data de Inicio |
| Principal | dataFim | N | String(60) | Data de Fim |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number (3) | Código de retorno |
| Principal | message | String (2000) | Mensagem de retorno |
| Principal | notasFiscais | Array | Lista de nota fiscal |
| Principal | totalDocs | Number(2) | Número total de documentos |
| Principal | limit | Number(2) | Número de limite de dados por página |
| Principal | page | Number(2) | Número de Páginas  |
| Principal | totalPages | Number(2) | Total de Páginas |
| Principal | notaFiscal | Object | Objeto com nota fiscal |
| Nota Fiscal | chaveAcesso | String (60) | Número da chave de acesso da nota fiscal |
| Nota Fiscal | numeroNota | Number (10) | Número da nota fiscal |
| Nota Fiscal | serie | String (5) | Código de série da nota fiscal |
| Nota Fiscal | especie | String (5) | Código de espécie da nota fiscal |
| Nota Fiscal | emissao | Date | Data da emissão da nota fiscal |
| Nota Fiscal | valor | Number (15,3) | Valor da nota fiscal |
| Nota Fiscal | pesoNF | Number (15,3) | Peso da nota fiscal |
| Nota Fiscal | pesoLiquido | Number (15,3) | Peso liquido |
| Nota Fiscal | cpfCnpjPagador | String (18) | CPF ou CNPJ do Pagador |
| Nota Fiscal | razaoSocialPagador |  | Razão Social do Pagador |
| Nota Fiscal | emissor | Object | Objeto com informações do Emissor |
| Emissor | CPFCNPJ | String (18) | Valor da base de cálculo do imposto |
| Emissor | razaoSocial | String (60) | Valor do imposto de substituição tributária |
| Emissor | endereco | Object | Objeto com informações do endereço |
| Emissor | logradouro | String (100) | Endereço do Emissor |
| Emissor | numero | String (7) | Número do endereço Emissor |
| Emissor | complemento | String (60) | Complemento do Emissor |
| Emissor | bairro | String (60) | Bairro do Emissor |
| Emissor | UF | String (2) | UF do Emissor |
| Emissor | CEP | String (8) | CEP do Emissor |
| Emissor | IBGEMunicipio | Number (7) | Código do Município IBGE do Emissor |
| Emissor | nomeMunicipio | String (60) | Nome do Município do Emissor  |
| Emissor | telefone | String (15) | Telefone do Emissor |
| Nota Fiscal | destinatario | Object | Objeto contendo as informações do Destinatário  |
| Destinatário  | codigoMaxys | Number(7) | Código do Destinatário no maxys  |
| Destinatário  | CPFCNPJ | String (18) | CPF ou CNPJ do Destinatário  |
| Destinatário  | razaoSocial |  | Razão Social do Destinatário |
| Destinatário  | endereco | Object | Objeto com informações do endereço |
| Destinatário  | logradouro | String (100) | Endereço do Destinatário |
| Destinatário  | numero | String (7) | Numero do endereço do Destinatário |
| Destinatário  | bairro | String (60) | Bairro do Destinatário |
| Destinatário  | UF | String (2) | UF do Destinatário |
| Destinatário  | IBGEMunicipio | Number (7) | Código do Município IBGE do Destinatário |
| Nota Fiscal | expedidor | Object | Objeto contendo informações do expedidor |
| Expedidor | endereco | Object | Objeto com informações do endereço |
| Expedidor | logradouro | String (100) | Endereço do Expedidor |
| Expedidor | numero | String (7) | Número de endereço do Expedidor |
| Expedidor | bairro | String (60) | Bairro do Expedidor |
| Expedidor | UF | String (2) | UF do Expedidor |
| Expedidor | IBGEMunicipio | Number (7) | Código do Município IBGE do Expedidor |
| Nota Fiscal | recebedor | Object | Objeto contendo informações do recebedor |
| Recebedor | endereco | Object | Objeto com informações do endereço |
| Recebedor | logradouro | String (100) | Endereço do Recebedor |
| Recebedor | numero | String (7) | Número de endereço do Recebedor |
| Recebedor | bairro | String (60) | Bairro do Recebedor |
| Recebedor | UF | String (2) | UF do Recebedor |
| Recebedor | IBGEMunicipio | Number (7) | Código do Município IBGE do Recebedor |
| Nota Fiscal | mensagemDigitada | String(100) | Mensagem sobre o Lançamento da nota |
| Nota Fiscal | transporte | Object | Objeto com informações do transporte |
| Transporte | cavalo | String(15) | Placa do Cavalo |
| Transporte | UFCavalo | String(2) | UF do cavalo |
| Transporte | CPFCNPJTransportador | String (18) | CPF/CNPJ do Transportador  |
| Nota Fiscal | itens | Object | Objeto com itens da nota |
| Itens | descricao | String (60) | Descrição do item da nota |
| Itens | unidadeMedida | String(2) | Unidade de medida do item da nota |
| Itens | CFOP | Number(6) | CFOP da nota |
| Itens | quantidadeAtendida | Number (15,3) | Quatidade atendida da nota |
| Itens | valorDesconto | Number (15,3) | Valor de desconto da nota |
| Itens | valorUnitario | Number (15,3) | Valor Unitário da nota |
| Itens | valorFrete | Number (15,3) | Valor de Frete da nota |
| Itens | valorSeguro | Number (15,3) | Valor de Seguro da nota |
| Itens | valorOutros | Number (15,3) | Outros Valores da nota |
| Itens | valorTotal | Number (15,3) | Valor total da nota |
| Itens | NCM | String(60) | NCM do item da nota |
| Itens | CEAN | String(60) | CEAN da nota |

### Exemplo Response

```json
{
    "code": 200,
    "message": "Sucesso",
    "notasFiscais": [
        {
            "notaFiscal": {
                "chaveAcesso": "",
                "numeroNota": 0,
                "serie": "0",
                "especie": "",
                "emissao": "",
                "valor": 0,
                "pesoNF": 0,
                "pesoLiquido": 0,
                "cpfCnpjPagador": "",
                "razaoSocialPagador": "",
                "emissor": {
                    "CPFCNPJ": "",
                    "razaoSocial": "",
                    "endereco": {
                        "logradouro": "",
                        "numero": "",
                        "complemento": "",
                        "bairro": "",
                        "UF": "",
                        "CEP": "",
                        "IBGEMunicipio": 0,
                        "nomeMunicipio": "",
                        "telefone": ""
                    }
                },
                "destinatario": {
                    "codigoMaxys": 0,
                    "CPFCNPJ": "",
                    "razaoSocial": "",
                    "endereco": {
                        "logradouro": "",
                        "numero": "",
                        "bairro": "",
                        "UF": "",
                        "IBGEMunicipio": 0
                    }
                },
                "expedidor": {
                    "codigoMaxys": 0,
                    "CPFCNPJ": "",
                    "razaoSocial": "",
                    "endereco": {
                        "logradouro": "",
                        "numero": "",
                        "bairro": "",
                        "UF": "",
                        "IBGEMunicipio": 0
                    }
                },
                "recebedor": {
                    "codigoMaxys": 0,
                    "CPFCNPJ": "",
                    "razaoSocial": "",
                    "endereco": {
                        "logradouro": "",
                        "numero": "",
                        "bairro": "",
                        "UF": "",
                        "IBGEMunicipio": 0
                    }
                },
                "mensagemDigitada": "",
                "transporte": {
                    "cavalo": "",
                    "UFCavalo": "",
                    "CPFCNPJTransportador": ""
                },
                "itens": [
                    {
                        "descricao": "",
                        "unidadeMedida": "",
                        "CFOP": 0,
                        "quantidadeAtendida": 0,
                        "valorDesconto": 0,
                        "valorUnitario": 0,
                        "valorFrete": 0,
                        "valorSeguro": 0,
                        "valorOutros": 0,
                        "valorTotal": 0,
                        "NCM": "",
                        "CEAN": ""
                    }
                ]
            }
        }
    ],
    "totalDocs": 0,
    "limit": 0,
    "page": 0,
    "totalPages": 0
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 400 | Bad Request |
| 500 | Falha ao processar sua requisição de consultas de historico |

---
---

# Emite Nota Físcal

### Este Método irá Escriturar Notas Físcais e quando houver despesas frota realizar o lançamento.

---

**Método:** POST

**Rota:** notaFiscal/postEmitirNotaEntrada

---

**Relação de Campos - Body Request.**

| Nível | Campo | Obrigatório | Tipo de Dado | Descrição |
| --- | --- | --- | --- | --- |
| listaNotas | notas |  | List Object | Lista contendo as notas a serem escrituradas |
| notas | filial | S | Number | Código da Empresa da Nota |
| notas | usuarioLancamento | S | String | Usuário do lançamento da Nota |
| notas | chaveAcesso | S | String | Chave de acesso da Nota a ser escriturada |
| notas | cpfCnpjFornecedor | S | Number | CPF/CNPJ do Clifor da Nota |
| notas | codigoEndereco | S | Number | Código do endereço do Clifor |
| notas | numeroNota | S | Number | Número da Nota fornecedor |
| notas | serieNota | S | String | Série da Nota fornecedor |
| notas | especieNota | S | String | Espécie da Nota fornecedor |
| notas | dataEmissao | S | Date | Data de emissão da Nota  |
| notas | formaPagamento | S | String | Forma de pagametno |
| notas | dataVencimento | S | Date | Data de vencimento da Nota |
| notas | valorDespesasAcessorias | N | Number | Valor de despesas quando necessário |
| notas | valorDesconto | N | Number | Valor de desconto quando necessário |
| notas | valorNota | S | Number | Valor total da nota |
| notas | centroCusto | S - Caso não haja rateio | Number | Centro de Custo da Nota |
| notas | itens |  | List Object | Lista contendo os Itens |
| itens | item | S | Number | Código do item |
| itens | movimentacao | S | Number | Código da Movimentação |
| itens | negocio | S | Number | Código do Negócio |
| itens | cfo | S | Number | Código CFOP |
| itens | tipoUnidade | S | String | Unidade de medida do item |
| itens | peso | S - caso não haja quantidade | Number | Peso do item |
| itens | quantidade | S - caso não haja peso | Number | Quantidade do item |
| itens | valorUnitario | S | Number | Valor unitário do item |
| itens | valorTotal | S  | Number | Valor total do item |
| itens | valorDesconto | N | Number | Valor desconto do item |
| itens | origemMercadoria | N | Number | Origem da mercadoria |
| itens | rateioCentroCusto |  | List Object | Lista contendo o rateio de centro de custos por item |
| rateioCentroCusto | centroCusto | S  - Caso não haja Centro de Custo no nível da nota | Number | Código do Centro de Custo |
| rateioCentroCusto | negocio | S  - Caso não haja Centro de Custo no nível da nota | Number | Código do negócio |
| rateioCentroCusto | movimentacao | S  - Caso não haja Centro de Custo no nível da nota | Number | Código da movimentação |
| rateioCentroCusto | percentual | S  - Caso não haja Centro de Custo no nível da nota | Number | Percentual do rateio |
| rateioCentroCusto | valor | S  - Caso não haja Centro de Custo no nível da nota | Number | Valor do rateio para o centro de custo |
| notas | despesaFrota |  | List Object | Lista contendo despesa frota da Nota |
| despesaFrota | tipoDespesa | N | Number | Código da despesa |
| despesaFrota | competencia | N | Number | Mês ano competência Ex: 01/2024 |
| despesaFrota | placa | N | String | Placa do veículo |
| despesaFrota | kmVeiculo | N | Number | Quilometragem do veiculo |

## JSON Exemplo Body Request

```json
[
  {
    "filial": 84,
    "usuarioLancamento": "MAX",
    "chaveAcesso": "41241000095441300043550010000000561000000567",
    "cpfCnpjFornecedor": "95441300043",
    "codigoEndereco": 1,
    "numeroNota": 1233219,
    "serieNota": "1",
    "especieNota": "NFE",
    "dataEmissao": "22/10/2024",
    "formaPagamento": "CA",
    "condicaoPagamento": 800,
    "dataVencimento": "25/10/2024",
    "valorDespesasAcessorias": 123,
    "valorDesconto": 1.5,
    "valorNota": 123.45,
    "centroCusto":null,
    "itens": [
      {
        "item": 3210,
        "movimentacao": 2303,
        "negocio": 1,
        "cfo": 1199,
        "tipoUnidade": "UN",
        "peso": 30000,
        "quantidade": 3,
        "valorUnitario": 123,
        "valorTotal": 123,
        "valorDesconto": 0,
        "origemMercadoria": 1,
        "rateioCentroCusto": [
          {
            "centroCusto": 1,
            "negocio": 1,
            "movimentacao": 2303,
            "percentual": 10,
            "valor": 100
          }
        ]
      }
    ],
    "despesaFrota": {
      "tipoDespesa": null,
      "competencia": "",
      "placa": "",
      "kmVeiculo": null
    }
  }
]
```

---

**Relação de Campos - Response Sucesso**

| Campo | Tipo de Dado | Descrição |
| --- | --- | --- |
| code | Number | Código do Response |
| message | String | Mensagem do Response |
| notas [{ | List Object | Lista com as notas emitidas |
| filial | Number | Empresa da Nota |
| cpfCnpjFornecedor | Number | Clifor da Nota |
| chaveAcesso | Number | Chave de acesso da nota |
| numeroNota | Number | Número da Nota |
| serieNota | String | Série da Nota |
| especieNota | String | Espécie da Nota |
| dataEmissao | Date | Data de emissão da Nota |
| lancamento }] | Number | Lançamento gerado na emissão da Nota |

**Relação de Campos - Response Erro**

| Campo | Tipo de Dado | Descrição |
| --- | --- | --- |
| code | Number | Código do Response |
| cause | String | Causa do erro para melhor rastreio |
| message | String | Mensagem do Response |

## JSON Exemplo Response

---

Possíveis Códigos de Retorno

| Código | Descrição |
| --- | --- |
| 200 | Sucesso na transação |
| 400,405,500 | Erro ao emitira nota físcal |

### 1 - Nota Físcal Emitida

```json
{
    "code": 200,
    "message:": "Sucesso",
    "notas": [
        {
            "filial": 84,
            "cpfCnpjFornecedor": "95441300043",
            "chaveAcesso": "41241000095441300043550010000000561000000567",
            "numeroNota": 1233219,
            "serieNota": "1",
            "especieNota": "NFE",
            "dataEmissao": "22/10/2024",
            "lancamento": 203923
        }
    ]
}
```

### 3- Erro

```json
	{
		"code": 500,
		"cause": "Erro ao lancar a Nota.",
		"message": "MOVIMENTACAO 108 NAO E DO TIPO CC"
	}
```
