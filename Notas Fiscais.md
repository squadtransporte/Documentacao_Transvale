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
