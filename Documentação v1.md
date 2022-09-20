# Documentação Centro de Manifesto Compartilhado

# Histórico de versões

| Versão | Modificado por | Alterações |
| --- | --- | --- |
| 1 | Daniel Schmitz, Mateus Cavalcante, Lucas Michalski | Criação da documentação |

# Sumário

[Obter ordens de coleta](#obter-ordens-de-coleta)

[Finalizar a emissão de um carregamento](#finalizar-a-emissão-de-um-carregamento)

[Consultar ordem de coleta](#consultar-ordem-de-coleta)

[Listar operadoras de Carta Frete Eletrônica](#listar-operadoras-de-carta-frete-eletrônica)

[Obter tipos de documento disponíveis para impressão](#obter-tipos-de-documento-disponíveis-para-impressão)

[Imprimir Documentos](#imprimir-documentos)

[Efetuar cancelamento de CT-e](#efetuar-cancelamento-de-ct-e)

[Obter motivos de cancelamento](#obter-motivos-de-cancelamento)

[Consultar nota fiscal](#consultar-nota-fiscal)

[Consultar cancelamento de CT-e](#consultar-cancelamento-de-ct-e)

[Listar operadoras de VP-e disponíveis](#listar-operadoras-de-vp-e-disponíveis)

[Inserir Ordem de Coleta](#inserir-ordem-de-coleta)

[Consultar conjunto](#consultar-conjunto)

[Cadastro de conjunto](#cadastro-de-conjunto)

[Consultar CT-e](#consultar-ct-e)

# Visão geral

Esta API foi criada para facilitar a comunicação entre o Centro de Manifesto Compartilhado da Transvale e o Maxys.

Será disponibilizado dois ambientes:

**Homologação**: [http://177.124.178.167:5056/integrador-transvale](http://177.124.178.167:5056/integrador-transvale)

**Produção**: [http://177.124.178.167:5055/integrador-transvale](http://177.124.178.167:5055/integrador-transvale)

## Autenticação

A autenticação é feita através do método basica, o usuário e senha deve ser solicitado ao TI da Transvale.

## Obter ordens de coleta

Este método lista todas as ordens de coleta emitidas com informações para visualização. Oferece a mesma visão do TAF107 no Maxys.

**Método:** GET

**Rota:** /OrdemColeta/getListaOrdemColeta

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | dataInicioEmissaoOC | N | Date | Data inicial da emissão da Ordem de Coleta  |
| Principal | dataFimEmissaoOC | N | Date | Data final da emissão da Ordem de Coleta |
| Principal | codigoEmpresa | N | Number (4) | Código da Empresa emissora |
| Principal | codigoMotorista | N | Number (7) | Código do Motorista |
| Principal | cpfCnpjMotorista | N | String (18) | CPF/CNPJ do Motorista |
| Principal | codigoCliforPagador | N | Number (7) | Código do Clifor Pagador |
| Principal | cpfCnpjCliforPagador | N | String (18) | CPF/CNPJ do Clifor Pagador |
| Principal | numeroOrdemColeta | N | Number (8) | Número da Ordem de Coleta |
| Principal | numeroPlacaCavalo | N | String (15) | Placa do Cavalo |
| Principal | empresaContrato | N | Number (4) | Código da empresa do Contrato |
| Principal | numeroContrato | N | Number (8) | Número do Contrato |
| Principal | numeroVarianteContrato | N | Number (4) | Número de variante do Contrato |
| Principal | statusProcessamento | N | String (1) | Status de processamento da Ordem de Coleta |
| Principal | dataInicioEmissaoCte | N | Date | Data inicial da emissão do CT-e |
| Principal | dataFimEmissaoCte | N | Date | Data final da emissão do CT-e |

Obs: Ao menos um dos filtros deve ser informado.

### Códigos de status (statusProcessamento)

| Código | Descrição |
| --- | --- |
| A | Aguardando emissão |
| F | Emissão finalizada |
| N | Na fila para emissão |
| P | Processando emissão |
| E | Erro na emissão |
| C | Cancelada |
| T | Todos |

### Exemplo de Request

```json
{
    "dataInicioEmissaoOC": "01/09/2022",
    "dataFimEmissaoOC": "12/09/2022",
    "codigoEmpresa": 5,
    "codigoMotorista": 123,
    "cpfCnpjMotorista": "73.398.029/0001-47",
    "codigoCliforPagador": 987,
    "cpfCnpjCliforPagador": "383.573.010-02",
    "numeroOrdemColeta": 15995123,
    "placaCavalo": "TES1A34",
	  "empresaContrato": 5,
    "numeroVarianteContrato": 2,
		"numeroContrato": 1234,
    "statusProcessamento": "A",
    "dataInicioEmissaoCte": "01/09/2022",
    "dataFimEmissaoCte": "12/09/2022"
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | codigoEmpresa | Number (4) | Código da Empresa emissora |
| Principal | numeroOrdemColeta | Number (8) | Número da Ordem de Coleta |
| Principal | dataAgendamentoOC | Date | Data de agendamento da Ordem de Coleta |
| Principal | empresaContrato | Number(4) | Código da empresa do Contrato |
| Principal | numeroContrato | Number (8) | Número do Contrato |
| Principal | numeroVarianteContrato | Number (4) | Número de variante do Contrato |
| Principal | codigoCliforPagador | Number (8) | Código do Clifor Pagador |
| Principal | nomeCliforPagador | String (60) | Nome do Clifor Pagador |
| Principal | numeroPlacaCavalo | String (15) | Placa Cavalo |
| Principal | codigoMotorista | Number (7) | Código do Motorista |
| Principal | nomeMotorista | String (60) | Nome do Motorista |
| Principal | statusProcessamento | String (1) | Status de processamento da Ordem de Coleta |
| Principal | nomeEmpresa | String (60) | Nome da Empresa/Filial |
| Principal | codigoIBGEOrigem | Number (7) | Código IBGE Origem |
| Principal | codigoIBGEDestino | Number (7) | Código IBGE Destino |
| Principal | codigoNaturezaCarga | Number (5) | Código de Natureza da Carga |
| Principal | descNaturezaCarga | String (60) | Descrição da Natureza da Carga |
| Principal | dataInicioProcessamento | Date (”DD/MM/YYYY hh24:mi:ss”) | Data de início do processamento |
| Principal | dataFimProcessamento | Date (”DD/MM/YYYY hh24:mi:ss”) | Data de fim do processamento |
| Principal | numeroTotalNotas | Number (30) | Número total de notas vinculadas à OC (via match ou manualmente) |
| Principal | pesoTotalNotas  | Number (15,3) | Peso total das notas vinculadas à OC |
| Principal | valorTotalNotas  | Number (15,3) | Valor total das notas vinculadas à OC |
| Principal | mensagemProcessamento  | String (4000) | Mensagem de processamento |
| Principal | detalhesProcessamento  | String (4000) | Detalhes de progresso da emissão |

### Exemplo de Response

```json
[
    {
        "codigoEmpresa": 5,
        "numeroOrdemColeta": 15995123,
        "dataAgendamentoOC": "10/09/2022",
        "numeroContrato": 1000,
        "numeroVarianteContrato": 2,
        "codigoCliforPagador": 987,
        "nomeCliforPagador": "João da Silva",
        "numeroPlacaCavalo": "TES1Q34",
        "codigoMotorista": 123,
        "nomeMotorista": "José dos Santos",
        "statusProcessamento": "A",
        "nomeEmpresa": "Maxicon Sistemas",
				"codigoIBGEOrigem": 4127700,
				"codigoIBGEDestino": 3509205,
        "codigoNaturezaCarga": 1,
        "descNaturezaCarga": "Soja",
        "dataInicioProcessamento": "11/09/2022 09:31:27",
        "dataFimProcessamento": "11/09/2022 09:31:28",
        "numeroTotalNotas": 2,
        "pesoTotalNotas": 26320.000, 
        "valorTotalNotas": 41999.940,
        "mensagemProcessamento": "Mensagem de processamento", 
        "detalhesProcessamento": "Detalhes do processamento"
    }
]
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 404 | Não foram encontradas ordens de coleta para os filtros informados. |
| 500 | Erro interno do servidor. Verificar a tag message |

---

## Insere a emissão de um carregamento

Este método insere a ordem de coleta na fila para emissão. A partir desse momento é iniciado a emissão de todos os documentos necessários para o carregamento (CT-e, MDF-e, CF-e, VP-e e averbação)

**Método:** POST

**Rota:** /OrdemColeta/inserir

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | nrOrdemCarregMaxys | N  | Number (8) | Número da ordem de coleta no Maxys |
| Principal | CPFUsuario | S | String (14) | CPF do usuário que está finalizando a emissão da documentação |
| Principal | CPFMotorista | S | String (14) | CPF do motorista |
| Principal | placaCavalo | S | String (15) | Placa do Cavalo |
| Principal | placaCarreta | N | String (15) | Placa da primeira carreta |
| Principal | placaCarreta2 | N | String (15) | Placa da segunda carreta |
| Principal | placaCarreta3 | N | String (15) | Placa da terceira carreta |
| Principal | CPFCNPJRemetente | S | String (14) | CPF/CNPJ do remetente |
| Principal | IBGEMunicipioRemetente | S | Number (7) | Código IBGE do municipio do remetente |
| Principal | CPFCNPJDestinatario | S | String (14) | CPF/CNPJ do destinatário |
| Principal | IBGEMunicipioDestinatario | S | Number (7) | Código IBGE do municipio do destinatário |
| Principal | CPFCNPJExpedidor | N | String (14) | CPF/CNPJ do expedidor |
| Principal | IBGEMunicipioExpedidor | N | Number (7) | Código IBGE do municipio do expedidor |
| Principal | CPFCNPJRecebedor | N | String (14) | CPF/CNPJ do recebedor |
| Principal | IBGEMunicipioRecebedor | N | Number (7) | Código IBGE do municipio do recebedor |
| Principal | contratoMaxys | S | Number (8) | Código do contrato no Maxys |
| Principal | varianteContratoMaxys | N | Number (4) | Variante do contrato do Maxys |
| Principal | observacao | N | String (600) | Observação que contém no contrato |
| Principal | emiteParcelaAdto | N | String (1 ) | Indica de irá emitir parcela de adiantamento |
| Principal | pesoAgendado | N | Number (15,3) | Peso agendado |
| Principal | numeroContainer | N | String (20) | Número do container |
| Principal | tara | N | Number (15,3) | Valor da tara |
| Principal | tipoMovimentacao | N | String (60) | Tipo da movimentação |
| Principal | localCarregamento | N | String (60) | Descrição do local de despacho. |
| Principal | dataHoraProgCarregamento | N | Date | Data/hora programada para coleta de container |
| Principal | localDescarga | N | String (60) | Local de entrega do container cheio |
| Principal | dataHoraProgDescarga | N | Date | Data/hora programada para descarga de container. |
| Principal | lacre | N | String (20) | Número do lacre |
| Principal | numeroReservaBooking | N | String (20) | Número de reserva/booking |
| Principal | navio | N | String (60) | Descrição do navio |
| Principal | tipoLancamento | S | Number (1) | Tipo do documento que será emitido (TABELA 01) |
| Principal | observacaoCtrc | N | String (400) | Observação do CT-e |
| Principal | dataAgendamento | N | Date | Data do carregamento |
| Principal | CteAutomatico | N | Boolean | Indica se irá emitir o CT-e automatico |
| Principal | TrocarNotas | N | Boolean | Indica se ira ocorrer troca de notas |
| Principal | informacoesAdicPagador | N | String (4000) | Informações adicionais do pagador |
|  |  |  |  |  |
| Principal | cartaFrete | N | Object |  |
| cartaFrete | codOperadora | N | Number (2) | Código da operadora |
| cartaFrete | codOperacaoOperadora | N | String (10) | Categoria de veículo para a emissão de CF-e. |
| cartaFrete | codFavorecido | N | Number (1) | Código do favorecido |
|  |  |  |  |  |
| Principal | notas | N | Array |  |
| notas | numero | S | Number (15,3) | Número da nota fiscal |
| notas | serie | S | String (3) | Série da nota fiscal |
| notas | chaveAcesso | S | String (60) | Número da chave de acesso da nota fiscal |
| notas | especie | S | String (5) | Espécie da nota fiscal |
| notas | peso | S | Number (15,3) | Peso da nota fiscal |
| notas | pesoLiquido | S | Number (15,3) | Peso liquido da nota fiscal |
| notas | volumesNota | S | Number (5) | Quantidade de itens da nota fiscal |
| notas | valor | S | Number (15,3) | Valor da nota fiscal |
| notas | dataEmissao | S | Date | Data de emissão da nota fiscal |
| notas | CFOP | S | Number (6) | CFOP da nota fiscal |
| notas | selecionadaEmissao | S | Boolean | Status para saber se a nota foi selecionada para emissão de CT-e |
|  |  |  |  |  |
| Principal | pedagio | N | Object |  |
| pedagio | tipoPagamentoCartao | N | String (3) | Tipo de pagamendo do pedagio |
| pedagio | valorPedagioTerceiro | N | Number (15,3) | Valor do pedagio terceiro |
| pedagio | numeroCartaoTerceiro | N | Number (16) | Número do cartão de terceiro |

### TABELA 01 - Códigos de tipos de serviços (tipoServico/tipoDocumento)

| Código | Descrição |
| --- | --- |
| 0 | Normal |
| 1 | Subcontratação |
| 2 | Redespacho |
| 3 | Redespacho intermediário |
| 4 | Serviço vinculado a multimodal |
| 6 | Multimodal |

### Exemplo de Request

```json
{
    "nrOrdemCarregMaxys": null,
    "CPFUsuario": "12345678901",
    "CPFMotorista": "12345678901",
    "placaCavalo": "ABC1234",
    "placaCarreta": "ABC1234",
    "placaCarreta2": "ABC1234",
    "placaCarreta3": "ABC1234",
    "CPFCNPJRemetente": "12345678901",
    "IBGEMunicipioRemetente": 4317202,
    "CPFCNPJDestinatario": "12345678901",
    "IBGEMunicipioDestinatario": 4317202,
    "CPFCNPJExpedidor": null,
    "IBGEMunicipioExpedidor": null,
    "CPFCNPJRecebedor": null,
    "IBGEMunicipioRecebedor": null,
    "contratoMaxys": 5000574,
    "varianteContratoMaxys": 1,
    "observacao": "TESTE EMISSÃO BLOQUEIO INFORMAÇÕES",
    "emiteParcelaAdto": "S",
    "pesoAgendado": 90000,
    "numeroContainer": null,
    "tara": null,
    "tipoMovimentacao": null,
    "localCarregamento": "frutal",
    "dataHoraProgCarregamento": "01/01/2022",
    "localDescarga": "Santa Rosa",
    "dataHoraProgDescarga": null,
    "lacre": null,
    "numeroReservaBooking": null,
    "navio": "",
    "tipoLancamento": "CTE",
    "observacaoCtrc": "Observação teste CTRC",
    "dataAgendamento": "'01/01/2022'",
    "CteAutomatico": true,
    "TrocarNotas": false,
    "informacoesAdicPagador": "testes",
    "cartaFrete": {
        "codOperadora": 6,
        "codOperacaoOperadora": null,
        "codFavorecido": null
    },
    "pedagio": {
        "tipoPagamentoCartao": null,
        "numeroCartaoTerceiro": null,
        "valorPedagioTerceiro": null
    },
    "notas": [
        {
            "numero": 12345,
            "serie": "1",
            "especie": "NFE",
            "chaveAcesso": "52220901598504000118550010000879521001981394",
            "peso": 30000,
            "valor": 90000,
            "volumesNota": 30000,
            "pesoLiquido": 30000,
            "dataEmissao": "12/09/2022",
            "CFOP": 5906,
            "selecionadaEmissao": true
        }
    ]
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | nrOrdemCarregMaxys | Number (3) | Código de retorno |

### Exemplo de Response

```json
{
    "nrOrdemCarregMaxys": 1235465
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Validação de dados para finalização da Ordem de Carregamento |
| 404 | Não foi encontrada nenhuma ordem de carregamento para a finalização |
| 500 | Erro interno do servidor. Verifique a tag message. |

---

## Finalizar a emissão de um carregamento

Este método insere a ordem de coleta na fila para emissão. A partir desse momento é iniciado a emissão de todos os documentos necessários para o carregamento (CT-e, MDF-e, CF-e, VP-e e averbação)

**Método:** POST

**Rota:** /OrdemColeta/finalizaEmissao

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | numeroOrdemColeta | S | Number (8) | Número da ordem de coleta do Maxys a ser finalizada |
| Principal | CPFUsuario | S | String (14) | Usuário que está finalizando a emissão da documentação |
| Principal | numeroAverbacao | N | String (40) | Número da averbação do CT-e. Caso não seja informado será utilizado o número obtivo via integração com a AT&M |
| Principal | tipoServico | N | Number (2) | Tipo de serviço (TABELA 01) |
| Principal | chaveCTeMultimodal | N | String (60) | Chave de acesso do CT-e multimodal |
| Principal | indicadorNegociacao | N | Number (1) | Indicador de negociação do CT-e multimodal(0 - Não negociável / 1 - Negociável). Obrigatório quando CT-e multimodal. |
| Principal | Notas | S | Array | Notas de mercadoria para emissão do CT-e |
|  |  |  |  |  |
| Notas  | numero | S | Number (15,3) | Número da nota fiscal |
| Notas | serie | S | String (3) | Série da nota fiscal |
| Notas | chaveAcesso | S | String (60) | Número da chave de acesso da nota fiscal |
| Notas | especie | S | String (5) | Espécie da nota fiscal |
| Notas | peso | S | Number (15,3) | Peso da nota fiscal |
| Notas | pesoLiquido | S | Number (15,3) | Peso liquido da nota fiscal |
| Notas | volumesNota | S | Number (5) | Quantidade de itens da nota fiscal |
| Notas | valor | S | Number (15,3) | Valor da nota fiscal |
| Notas | dataEmissao | S | Date | Data de emissão da nota fiscal |
| Notas | CFOP | S | Number (6) | CFOP da nota fiscal |
| Notas | selecionadaEmissao | S | Boolean | Status para saber se a nota foi selecionada para emissão de CT-e |
|  |  |  |  |  |
| Principal | Documentos | N | Array | Documentos anteriores |
|  |  |  |  |  |
| Documentos | chaveAcessoCTe | S | String (60) | Número da chave de acesso do CT-e |
| Documentos | tipoDocumento | S | String (2) | Tipo do documento emitido (TABELA 01) |
| Documentos | subSerieDoc | S | String (2) | Subsérie do documento  |
|  |  |  |  |  |
| Principal | valorTarifaAtualizado | N | Number (15,2) | Valor da tarifa a ser atualizada, caso o valor da tarifa seja diferente da negociada no contrato  |

### TABELA 01 - Códigos de tipos de serviços (tipoServico/tipoDocumento)

| Código | Descrição |
| --- | --- |
| 0 | Normal |
| 1 | Subcontratação |
| 2 | Redespacho |
| 3 | Redespacho intermediário |
| 4 | Serviço vinculado a multimodal |
| 6 | Multimodal |

### Exemplo de Request

```json
{
    "nrOrdemCarregMaxys": 12345679,
    "CPFUsuario": "01234567891",
    "numeroAverbacao": null,
    "tipoServico": 0,
    "chaveCTeMultimodal": null,
    "indicadorNegociacao": null,
    "notas": [
        {
            "numero": 12345,
            "serie": "1",
            "especie": "NFE",
            "chaveAcesso": "52220901598504000118550010000879521001981394",
            "peso": 30000,
            "valor": 90000,
            "volumesNota": 30000,
            "pesoLiquido": 30000,
            "dataEmissao": "12/09/2022",
            "CFOP": 5906,
            "selecionadaEmissao": true
        }
    ],
    "documentos": [
        {
            "chaveAcessoCTe": "42220901598504000118550010000879521001981394",
            "tipoDocumento": 0,
            "subSerieDoc": "1"
        }
    ],
    "valorTarifaAtualizado": null
}
```

### Relação de campos - Response

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | code |  | Number (3) | Código de retorno |
| Principal | message |  | String (2000) | Mensagem de retorno |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "Sucesso"
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Validação de dados para finalização da Ordem de Carregamento |
| 404 | Não foi encontrada nenhuma ordem de carregamento para a finalização |
| 500 | Erro interno do servidor. Verifique a tag message. |

---

## Consultar ordem de coleta

Este método permite a consulta de uma ordem de coleta, retornando informações informações gerais e status da mesma.

**Método:** GET

**Rota:** /OrdemColeta/consultar

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | CPFUsuario | N | String (14) | CPF do usuário |
| Principal | CPFUsuarioOC | N | String (14) | CPF do usuário da Ordem de Coleta |
| Principal | codFilialMaxys | N | Number (4) | Código da Filial no Maxys |
| Principal | nomeFilialMaxys | N | String (60) | Nome da Filial no Maxys |
| Principal | dataAgendamentoInicio | N | Date | Data de inicio do agendamento da OC |
| Principal | dataAgendamentoFim | N | Date | Data de fim do agendamento da OC |
| Principal | nrOrdemCarregMaxys | N | Number (20) | Número da Ordem de Carregamento no Maxys |
| Principal | contratoMaxys | N | Number (8) | Número do Contrato no Maxys |
| Principal | varianteContratoMaxys | N | Number (4) | Número de variante do contrato no Maxys |
| Principal | placaCavalo | N | String (15) | Placa do cavalo |
| Principal | CPFMotorista | N | String (14) | CPF do Motorista |
| Principal | nomeMotorista | N | String (60) | Nome do Motorista |
| Principal | statusFilaEmissao | N | String (1) | Status da fila de Emissão de OC |
| Principal | lancamentoCtrc | N | Number (7) | Número de lançamento do CT-e |
| Principal | empresaCtrc | N | Number (4) | Código da Empresa do CT-e |
| Principal | serieCtrc | N | String (5) | Série do CT-e |
| Principal | numeroCtrc | N | Number (10) | Número do CT-e |
| Principal | CPFUsuarioContrato | N | String (14) | CPF do usuário de criação contrato |

*É obrigatório informar ao menos um dos filtros

### Códigos de status (statusFilaEmissao)

| Código | Descrição |
| --- | --- |
| A | Aguardando emissão |
| F | Emissão finalizada |
| N | Na fila para emissão |
| P | Processando emissão |
| E | Erro na emissão |
| C | Cancelada |
| T | Todos |

### Exemplo de Request

```json
{
    "CPFUsuario": "39258896041",
    "CPFUsuarioOC": "13088114034",
    "codFilialMaxys": 5,
    "nomeFilialMaxys": "Maxicon Sistemas",
    "dataAgendamentoInicio": "10/09/2022",
    "dataAgendamentoFim": "12/09/2022",
    "nrOrdemCarregMaxys": 2302,
    "contratoMaxys": 5000764,
    "varianteContratoMaxys": 1,
    "placaCavalo": "TES1A234",
    "CPFMotorista": "81145923038",
    "nomeMotorista": "Fulano da Silva",
    "statusFilaEmissao": "F",
    "lancamentoCtrc": 7894561,
    "empresaCtrc": 5,
    "serieCtrc": "U",
    "numeroCtrc": 10022,
    "CPFUsuarioContrato": "11520880090"
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number (3) | Código de retorno HTTP |
| Principal | message | String | Mensagem de retorno |
| Principal | ordensCarregamento | Array |  |
|  |  |  |  |
| Ordem Carregamento | nrOrdemCarregMaxys | Number (8) | Número da Ordem de Coleta |
| Ordem Carregamento | codFilialMaxys | Number (4) | Código da Filial no Maxys |
| Ordem Carregamento | nomeFilialMaxys | String (60) | Nome da Filial no Maxys |
| Ordem Carregamento | dataAgendamento | Date | Data do agendamento da Ordem de Coleta |
| Ordem Carregamento | observacao | String (240) | Observação da Ordem de Coleta |
| Ordem Carregamento | observacaoCtrc | String (400) | Observação do CT-e |
| Ordem Carregamento | emiteParcelaAdto | String (1) | Define se será emitida a parcela de adiantamento para o frete (S- sim ou N - Não) |
| Ordem Carregamento | exigeInfoAdicPagador | Boolean | Indica se deve obrigar o número do pedido, número loud, termo de transportes e outros |
| Ordem Carregamento | textoAdicPagador | String (240) | Texto adicional do TAF001 |
| Ordem Carregamento | informacoesAdicPagador | String (4000) | Informações adicionais exigidas pelo Clifor pagador para emissão do CT-e automático |
| Ordem Carregamento | pesoAgendado | Number (15,3) | Peso agendado |
| Ordem Carregamento | valorMercEfeitoSeguro | Number (15,3) | Valor da mercadoria para efeito seguro |
| Ordem Carregamento | pesoNotasVinculadas | Number (15,3) | Peso das notas fiscais vinculadas à Ordem de Coleta |
| Ordem Carregamento | qtdeNotasVinculadas | Number (15,3) | Quantidade de notas fiscais vinculadas à Ordem de Coleta |
| Ordem Carregamento | valorTarifaTransportador | Number (15,3) | Valor da Tarifa do Transportador |
| Ordem Carregamento | notas | Array |  |
|  |  |  |  |
| Notas | numero | Numer (15,3) | Número da nota fiscal |
| Notas | serie | String (3) | Série da nota fiscal |
| Notas | especie | String (5) | Espécie da nota fiscal |
| Notas | chaveAcesso | String(60) | Número da chave de acesso da NF para emissão automática de CT-e |
| Notas | peso | Number (15,3) | Peso da nota fiscal |
| Notas | valor | Number (15,3) | Valor da nota fiscal |
| Notas | volumesNota | Number (5) | Quantidade de itens da nota fiscal |
| Notas | pesoLiquido | Number (15,3) | Peso líquido da nota fiscal |
| Notas | dataEmissao | Date | Data de emissão da nota fiscal |
| Notas | CFOP | Number (6) | CFOP da nota fiscal |
| Notas | selecionadaEmissao | Boolean | Indica se a nota foi selecionada para emissão de CT-e |
| Notas | notaDigitada | Boolean | Indica se a nota foi digitada  |
|  |  |  |  |
| Ordem Carregamento | geraNFSE | Boolean | Indica se deve gerar NFSE |
| Ordem Carregamento | geraDACTE | Boolean | Indica se deve gerar DACTE |
| Ordem Carregamento | geraMDFE | Boolean | Indica se deve gerar MDFE |
| Ordem Carregamento | geraTermoEstadia | Boolean | Indica se deve gerar Termo de Estadia |
| Ordem Carregamento | geraCFe | Boolean | Indica se deve gerar CF-e |
| Ordem Carregamento | geraContratoFrete | Boolean | Indica se deve gerar Contrato Frete |
| Ordem Carregamento | geraCartaFrete | Boolean | Indica se deve gerar Carta Frete |
| Ordem Carregamento | dataCancelamento | Date (”DD/MM/RRRR HH24:MI:SS”) | Data de cancelamento da Ordem de Coleta |
| Ordem Carregamento | statusFilaEmissao | String (1) | Status da fila de emissão da Ordem de Coleta (Tabela 01) |
| Ordem Carregamento | statusEmissao | Number (1) | Status da emissão do CT-e (Tabela 02) |
| Ordem Carregamento | notaDifitada | Boolean | Indica se a nota foi digitada |
| Ordem Carregamento | mensagemFilaEmissao | String (2000)  | Mensagem da fila de emissão |
| Ordem Carregamento | pagamentoPedagioAntecipado | Boolean | Indica se o pedágio foi pago antecipadamente pelo Clifor pagador |
| Ordem Carregamento | contrato | Object |  |
|  |  |  |  |
| Contrato | contratoMaxys | Number (8) | Número do contrato no Maxys |
| Contrato | filialMaxys | Number (4) | Código da Filial do contrato no Maxys |
| Contrato | varianteContratoMaxys | Number (4) | Número de variante do contrato no Maxys |
| Contrato | responsavelSeguroCTe | Number (1) | Status do responsável pelo seguro (Tabela 04) |
| Contrato | tipoServico | Number (2) | Indica o tipo de serviço do CT-e (Tabela 05) |
| Contrato | tipoServicoMultimodal | Boolean | Indica se o tipo de serviço é vinculado a Multimodal |
| Contrato | tipoMultimodal | Boolean | Indica se é Multimodal |
|  |  |  |  |
| Ordem Carregamento | juncao | Object |  |
|  |  |  |  |
| Juncao | CPFMotorista | String (14) | CPF do Motorista |
| Juncao | nomeMotorista | String (60) | Nome do Motorista |
| Juncao | placaCavalo | String (15) | Placa do cavalo |
| Juncao | placaCarreta | String (15) | Placa da carreta |
| Juncao | placaCarreta2 | String (15) | Placa da carreta 2 |
| Juncao | placaCarreta3 | String (15) | Placa da carreta 3 |
|  |  |  |  |
| Ordem Carregamento | documentos | Array |  |
|  |  |  |  |
| Documentos | empresa | Number (4) | Código da empresa do CT-e |
| Documentos | numeroLancamento | Number (7) | Número de lançamento do CT-e |
| Documentos | numero | Number (10) | Número do CT-e |
| Documentos | serie | String (5) | Série do CT-e |
| Documentos | tipoLancamento | String (20) | Código de status do CT-e(Tabela 03) |
|  |  |  |  |
| Ordem Carregamento | valoresTransportador | Object |  |
|  |  |  |  |
| Valores Transportador | tarifaTransportador | Number (15,3) | Tarifa do transportador |
| Valores Transportador | valorFrete | Number (15,3) | Valor do Frete |
| Valores Transportador | valorPedagio | Number (15,3) | Valor do Pedágio |
| Valores Transportador | valorAdiantamento | Number (15,3) | Valor do Adiantamento |
| Valores Transportador | valeCombustivel | Object |  |
|  |  |  |  |
| Valores Transportador | percentualValeCombustivel | Number (15,3) | Percentual do Vale Combustível |
| Valores Transportador | valorValeCombustivel | Number (15,3) | Valor do Vale Combustível |
|  |  |  |  |
| Principal | totalDocs | Number | Número total de documentos da Ordem de Coleta |
| Principal | limit | Number | Quantidade de registros por página |
| Principal | page | Number | Página atual |
| Principal | totalPages | Number | Número total de páginas |

### Tabela 01 - Códigos de status (statusFilaEmissao)

| Código | Descrição |
| --- | --- |
| A | Aguardando emissão |
| F | Emissão finalizada |
| N | Na fila para emissão |
| P | Processando emissão |
| E | Erro na emissão |
| C | Cancelada |
| T | Todos |

### Tabela 02 - Códigos de status (statusEmissao)

| Código | Descrição |
| --- | --- |
| 1 | Aguardando NF-e |
| 2 | Emitir CT-e |
| 3 | Processando Emissão |
| 4 | CT-e emitido |
| 5 | Erro na Emissão |
| 6 | Recusado |

### Tabela 03 - Códigos de status (tipoLancamento)

| Código | Descrição |
| --- | --- |
| 1 | CT-e |
| 2 | Simulação |
| 5 | NFS-e |

### Tabela 04 - Códigos de status (responsavelSeguroCTe)

| Código | Descrição |
| --- | --- |
| 0 | Remetente |
| 1 | Expedidor |
| 2 | Recebedor |
| 3 | Destinatário |
| 4 | Emitente do CT-e |
| 5 | Pagador do Frete |

### Tabela 05 - Códigos de status (tipoServico)

| Código | Descrição |
| --- | --- |
| 0 | Normal |
| 1 | Subcontratação |
| 4 | Serviço Vinculado a Multimodal |
| 6 | Multimodal |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "Mensagem de retorno de sucesso",
    "ordensCarregamento": [
        {
            "nrOrdemCarregMaxys": 2302,
            "codFilialMaxys": 5,
            "nomeFilialMaxys": "Maxicon Sistemas",
            "dataAgendamento": "11/09/2022",
            "observacao": "Observação de exemplo",
            "observacaoCtrc": "Observação de exemplo do CTRC",
            "emiteParcelaAdto": "S",
            "exigeInfoAdicPagador": true,
            "textoAdicPagador": "Texto adicional de exemplo",
            "informacoesAdicPagador": "Informações adicionais exigidas para emissão de CT-e",
            "pesoAgendado": 27800.130,
            "valorMercEfeitoSeguro": 30125.600,
            "pesoNotasVinculadas": 27800.130,
            "qtdeNotasVinculadas": 1,
            "valorTarifaTransportador": 250.120,
            "notas": [
                {
                    "numero": 1356811,
                    "serie": "1",
                    "especie": "NFE",
                    "chaveAcesso": "41190576107770002909550000000364511113921003XX",
                    "peso": 27800.130,
                    "valor": 30125.600,
                    "volumesNota": 1,
                    "pesoLiquido": 27800.130,
                    "dataEmissao": "11/09/2022",
                    "CFOP": 5102,
                    "selecionadaEmissao": true
                }
            ],
            "geraNFSE": true,
            "geraDACTE": false,
            "geraMDFE": false,
            "geraTermoEstadia": false,
            "geraCFe": true,
            "geraContratoFrete": true,
            "geraCartaFrete": false,
            "dataCancelamento": "12/09/2022 14:51:23",
            "statusFilaEmissao": "C",
            "statusEmissao": 6,
            "mensagemFilaEmissao": "Mensagem de exemplo da fila de emissão",
            "pagamentoPedagioAntecipado": true,
            "contrato": {
                "contratoMaxys": 35041,
                "filialMaxys": 5,
                "varianteContratoMaxys": 1,
                "responsavelSeguroCTe": 4,
                "tipoServico": 1,
                "tipoServicoMultimodal": true,
                "tipoMultimodal": true
            },
            "juncao": {
                "CPFMotorista": 21045657077,
                "nomeMotorista": "Beltrano da Silva",
                "placaCavalo": "TES1A34",
                "placaCarreta": "MHE2A45",
                "placaCarreta2": "LAL3A56",
                "placaCarreta3": "DNS4A67"
            },
            "documentos": [
                {
                    "empresa": 5,
                    "numeroLancamento": 987321,
                    "numero": 36974123,
                    "serie": "U",
                    "tipoLancamento": 1
                }
            ],
            "valoresTransportador": {
                "tarifaTransportador" : 180.000,
                "valorFrete" : 5004.023,
                "valorPedagio" : 450.000,
                "valorAdiantamento" : 2001.600,
                "valeCombustivel" : {
                    "percentualValeCombustivel" : 50,
                    "valorValeCombustivel" : 2001.600
                }
            }

        }
    ],
    "totalDocs": 1,
    "limit": 10,
    "page": 1,
    "totalPages": 1
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 404 | Não foi encontrada nenhuma Ordem de Coleta com os dados informados |
| 500 | Erro interno do servidor. Verifique a tag message. |

---

## Listar operadoras de Carta Frete Eletrônica

Este método retorna as operadoras cadastradas no Maxys e disponíveis para emissão de Carta Frete eletrônica.

**Método:** GET

**Rota:** /cadastros/getOperadorasCfe

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | filialMaxys | S | Number (4) | Código da filial do Maxys |

### Exemplo de Request

```json
{
    "filialMaxys": 5
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | Operadoras |  | Operadoras cadastradas |
| Operadoras | codOperadora | Number (2) | Código da operadora |
| Operadoras | descOperadora | String (60) | Nome da operadora |
| Operadoras | Operacoes | Array | ** |
|  |  |  |  |
| Operacoes | codOperacao | Number (10) | Código da operação |
| Operacoes | descOperacao | String (100) | Descrição da operação |
| Operadoras | Favorecidos | Array | Caso a operadora seja a pamcary retornara os favorecidos |
|  |  |  |  |
| Favorecidos | codFavorecido | Number (2) | Código do favorecido (TABELA 01) |
| Favorecidos | descFavorecido | String (60) | Descrição do favorecido |

### TABELA 01 - Códigos de favorecidos (codFavorecido)

| Código | Descrição |
| --- | --- |
| 1 | Contratado |
| 3 | Motorista |

### Exemplo de Response

```json
{
    "Operadoras": [
        {
            "codOperadora": 1,
            "descOperadora": "PAMCARY",
            "operacoes": [
                {
                    "codOperacao": 1,
                    "descOperacao": "CAVALO"
                }
            ],
            "favorecidos": [
                {
                    "codFavorecido": 1,
                    "descFavorecido": "Contratado"
                },
                {
                    "codFavorecido": 3,
                    "descFavorecido": "Motorista"
                }
            ]
        }
    ]
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 404 | Nenhuma operadora cadastrada |
| 500 | Erro de execução |

---

## Obter tipos de documento disponíveis para impressão

Este método recebe os dados de um CT-e e retorna os documentos (PDF) que foram gerados e estão disponíveis para impressão.

**Método:** GET

**Rota:** /OrdemColeta/getTiposDocumento?empresa={empresa}&serie={serie}&lancamento={lancamento}&numero={numero}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | empresa | S | Number (4) | Empresa de emissão do CT-e |
| Principal | serie | S | String (5) | Código da série do CT-e |
| Principal | lancamento | S | Number (7) | Número do lançamento do CT-e |
| Principal | numero | S | Number (10) | Número do CT-e |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | tipoDocumento | Number (2) | Tipo de documento (TABELA 01) |
| Principal | descricaoDocumento | String (60) | Descrição do tipo de documento |

### Exemplo de Response

```json
[
    {
        "tipoDocumento": 1,
        "descricaoDocumento": "DACTE IMPRESSO"
    }
]
```

### TABELA 01 - Códigos de tipos de documentos(tipoDocumento)

| Código | Descrição |
| --- | --- |
| 1 | DACTE |
| 2 | MDFE |
| 3 | NFSE |
| 4 | CIOT |
| 5 | CONTRATO DE FRETE |
| 6 | TERMO ESTADIA |
| 7 | CARTA FRETE |
| 9 | CARTA FRETE AUTONOMO |

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 400 | Requisição inválida |
| 404 | CT-e informado não encontrado |
| 500 | Erro interno do servidor. Verifique a tag message. |

---

## Imprimir Documentos

Esse método retorna o documento em PDF.

**Método:** GET

**Rota:** /Cte/getDocumento?empresa={empresa}&lancamento={lancamento}&serie={serie}&numero={numero}&tipoDocumento={tipoDocumento}&ordemColeta={ordemColeta}&CPFUsuario={CPFUsuario}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | empresa | S | Number (4) | Código da empresa de emissão do CT-e |
| Principal | serie | S | String (5) | Código de série do CT-e |
| Principal | lancamento | S | Number (7) | Número do lançamento do CT-e |
| Principal | numero | S | Number (10) | Número do CT-e |
| Principal | tipoDocumento | S | Number (2) | Código do Tipo de documento (TABELA 01) |
| Principal | ordemColeta | N | Number (8) | Número da ordem de coleta |
| Principal | CPFUsuario | N | String (14) | CPF/CNPJ do usuário |

### TABELA 01 - Códigos de tipos de documentos(tipoDocumento)

| Código | Descrição |
| --- | --- |
| 1 | DACTE |
| 2 | MDFE |
| 3 | NFSE |
| 4 | CIOT |
| 5 | CONTRATO DE FRETE |
| 6 | TERMO ESTADIA |
| 7 | CARTA FRETE |
| 9 | CARTA FRETE AUTONOMO |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | arquivo | Arquivo PDF | Arquivo gerado de acordo com o tipo de documento |

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 404 | Nenhum documento encontrado para os dados informados |
| 500 | Erro de execução |

---

## Efetuar cancelamento de CT-e

Esse método efetua o cancelamento de um CT-e e todos os seus documentos em cascata.

**Método: POST**

**Rota:** /Cte/cancelarCTe

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | numeroAgrupamento | N | Number (15) | Número do agrupamento de CT-es a serem cancelados |
| Principal | codigoFilial | N | Number (4) | Código da empresa do CT-e a ser cancelado |
| Principal | numeroLancamento | N | Number (7) | Número do lançamento do CT-e a ser cancelado |
| Principal | serieDocumento | N | String (5) | Série do CT-e a ser cancelado |
| Principal | geraCFAvulsa | N | String (1) | Status para saber se gera carta frete avulsa ou cancela todas as parcelas (TABELA 01) |
| Principal | CPFUsuarioCancelamento | S | String (14) | CPF do usuário que está efetuando o cancelamento |
| Principal  | codigoMotivoCancelamento | S | Number (5) | Motivo do cancelamento |

Obs: é necessário informar ao menos o numero de agrupamento ou a chave do CT-e (codigoFilial, numeroLancamento, serieDocumento, tipoFaturamento)

### TABELA 01 - Códigos de status (geraCFAvulsa)

| Código | Descrição |
| --- | --- |
| S | Cancela somente o recebimento |
| N | Cancela todas as parcelas |

### Exemplo de Request

```json
{
  "numeroAgrupamento": null,
  "codigoFilial": 5,
  "numeroLancamento": 18942,
  "serieDocumento": "3",
  "geraCFAvulsa": "N",
  "CPFUsuarioCancelamento": "12345678901",
  "codigoMotivoCancelamento": 1
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number | Código retorno HTTP |
| Principal | message | String | Mensagem de retorno |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "CT-e incluido na fila de cancelamento com sucesso."
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Não foi possível processar a transação |
| 500 | Erro interno do servidor. Verifique a tag message. |

---

## Obter motivos de cancelamento

Esse método lista os motivos de cancelamento que podem ser usados para cancelamento dos documentos.

**Método:** GET

**Rota:** /Cte/getMotivos?codigo={codigo}&descricao={descricao}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | codigo | N | Number (5) | Código do motivo de cancelamento |
| Principal | descricao | N | String (60) | Descrição do motivo de cancelamento |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number (5) | Código de retorno HTTP |
| Principal | message | String (2000) | Mensagem de retorno |
| Principal | motivosCancelamento | Array | Array de motivos de cancelamento |
|  |  |  |  |
| motivosCancelamento | codigo | Number(5) | Código do motivo de cancelamento |
| motivosCancelamento | descricao | String (60) | Descrição do motivo de cancelamento |
|  |  |  |  |
| Principal | totalDocs | Number | Número total de documentos da Ordem de Coleta |
| Principal | limit | Number | Quantidade de registros por página |
| Principal | page | Number | Página atual |
| Principal | totalPages | Number | Número total de páginas |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "",
    "motivosCancelamento": [
        {
            "codigo": 1,
            "descricao": "VALOR INCORRETO"
        }
    ]
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 500 | Erro interno do servidor. Verifique a tag message |

---

## Consultar nota fiscal

Esse método retornas os dados principais de uma nota fiscal, buscando no MaxysXML.

**Método:** GET

**Rota:** /NotaFiscal/getNotaCompleta?numeroChaveAcesso={numeroChaveAcesso}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | numeroChaveAcesso | S | String (60) | Número da chave de acesso da nota fiscal |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number (3) | Código de retorno |
| Principal | message | String (2000) | Mensagem de retorno |
| Principal | chaveAcesso | String (60) | Número da chave de acesso da nota fiscal |
| Principal | numero | Number (10) | Número da nota fiscal |
| Principal | codigoSerie | String (5) | Código de série da nota fiscal |
| Principal | codigoEspecie | String (5) | Código de espécie da nota fiscal |
| Principal | dataEmissao | Date | Data da emissão da nota fiscal |
| Principal | quantidadeVolume | Number (15,3) | Quantidade de volumes |
| Principal | pesoNotaFiscal | Number (15,3) | Peso da nota fiscal |
| Principal | valorNotaFiscal | Number (15,3) | Valor da nota fiscal |
| Principal | valorMercadoria | Number (15,3) | Valor da mercadoria  |
| Principal | pesoLiquido | Number (15,3) | Peso liquido |
| Principal | codigoCfo | Number (6) | Código do CFO |
| Principal | descCfo | String (60) | Descrição do CFO |
| Principal | valorImpostobcalc | Number (15,3) | Valor da base de cálculo do imposto |
| Principal | valorImposto | Number (15,3) | Valor do imposto |
| Principal | valorImpostobcalcsub | Number (15,3) | Valor da base de cálculo do imposto |
| Principal | valorImpostosubstrib | Number (15,3) | Valor do imposto de substituição tributária |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "Sucesso",
    "chaveAcesso": "43200603640719000185570010001793651000000003",
    "numeroNffornec": 11324,
    "codigoSeriefornec": 3,
    "codigoEspecienf": "NF",
    "dataEmissao": "14/04/2022",
    "quantidadeVolume": 1,
    "pesoNotaFiscal": 30000.000,
    "valorNotaFiscal": 5000.000,
    "valorMercadoria": 2500.000,
    "pesoLiquido": 1000.00,
    "codigoCfo": 1122,
    "descCfo": "COMPRA P/IND.MERC.REMET.P/FORN.SEM TRANSITAR P/ESTAB.ADQ.A O",
    "valorImpostobcalc": 125.20,
    "valorImposto": 125.20,
    "valorImpostobcalcsub": 125.20,
    "valorImpostosubstrib": 125.20
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 400 | Requisição inválida |
| 404 | Nota fiscal não encontrada |
| 500 | Erro interno do servidor. Verifique a tag message. |

---

## Consultar cancelamento de CT-e

Esse método permite consultar o status de cancelamento de todos os documentos gerados.

**Método:** GET

**Rota:** /Cte/cancelamentoCTe/consultar?numeroAgrupamento={numeroAgrupamento}&codigoFilial={codigoFilial}&numeroLancamento={numeroLancamento}&serieDocumento={serieDocumento}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | numeroAgrupamento | N | Number (15) | Número de agrupamento para CT-e com Carta Frete única |
| Principal | codigoFilial | S | Number (4) | Código da Filial do CT-e |
| Principal | numeroLancamento | S | Number (7) | Número de Lançamento do CT-e |
| Principal | serieDocumento | S | String (5) | Série do CT-e |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | documentos | Array | Array de documentos |
|  |  |  |  |
| Cancelamento | status | String (2000) | Descrição do status da fila de cancelamento  |
| Cancelamento | mensagemProcessamento | String (2000) | Mensagem de erro no cancelamento |
| Cancelamento | seqFilaProcessamento | Number (15) | Sequencial da fila de processamento de CT-e |
|  |  |  |  |
| Documentos | documento | Object | Objeto referente a documento |
|  |  |  |  |
| Documento | codigoFilial | Number (4) | Código da Filial do CT-e |
| Documento | nomeFilial | String (60) | Nome da Filial do CT-e |
| Documento | numeroLancamento | Number (7) | Número de Lançamento do CT-e |
| Documento | serieDocumento | String (5) | Série do CT-e |
| Documento | tipoFaturamento | String (1) | Tipo de Faturamento do CT-e |
| Documento | numeroAgrupamento | Number (15) | Número do Agrupamento para CT-e com Carta Frete única |
| Documento | numeroDocumento | Number (10) | Número do CT-e |
| Documento | dataEmissao | Date | Data de emissão do CT-e |
| Documento | placaCavalo | String (15) | Placa do Cavalo |
| Documento | CPFCNPJPagador | String (14) | CPF/CNPJ do Clifor Pagador |
| Documento | nomePagador | String (60) | Nome do Clifor Pagador |
| Documento | CPFMotorista | String (14) | CPF do Motorista |
| Documento | nomeMotorista | String (60) | Nome do Motorista |
| Documento | status | String (15) | Status do CT-e  |
| Documento | exigeMotivoNFSePrefeitura | Boolean | Indica se exige motivo de NFSe (Prefeitura) |
|  |  |  |  |
| Documentos | pedagio | Object | Objeto referente ao pedágio |
| Pedagio | status | String (2000) | Status do pedágio eletrônico |
|  |  |  |  |
| Documentos | cartaFrete | Object | Objeto referente à Carta Frete |
| Carta Frete | status | String (2000) | Status da Carta Frete |
|  |  |  |  |
| Documentos | financeiro | Object | Objeto referente ao financeiro |
| Financeiro | status | String (2000) | Status do financeiro |
|  |  |  |  |
| Documentos | CTe | Object | Objeto referente ao CTe |
| CTe | status | String (2000) | Status do CTe |
|  |  |  |  |
| Documentos | averbacao | Object | Objeto referente à averbação |
| Averbacao | status | String (2000) | Status da averbação |
|  |  |  |  |
| Documentos | microSeguro | Object | Objeto referente ao Micro Seguro |
| Micro Seguro | status | String (2000) | Status do Micro Seguro |
|  |  |  |  |
| Documentos | MDFe | Object | Objeto referente ao MDFe |
| MDFe | status | String (2000) | Status do MDFe |
|  |  |  |  |
| Documentos | NFSe | Object | Objeto referente à NFSe |
| NFSe | status | String (2000) | Status da NFSe |

### Exemplo de Response

```json

     {
          "cancelamento": {
              "status": "",
              "mensagemErroProcessamento": "",
              "seqFilaProcessamento": null
          },
          "documento": {
              "codigoFilial": 5,
              "nomeFilial": "Maxicon Sitemas",
              "numeroLancamento": 15586,
              "serieDocumento": "1",
              "tipoFaturamento": 1,
              "numeroAgrupamento": null,
              "numeroDocumento": 10423,
              "dataEmissao": "19/01/2018",
              "placaCavalo": "JFF0001",
              "CPFCNPJPagador": "15996351196",
              "nomePagador": "Fulano de Souza",
              "CPFMotorista": "23554700063",
              "nomeMotorsita": "Sicrano da Silva",
              "status": "Cancelado",
              "exigeMotivoNFSePrefeitura": false
          },
          "pedagio": {
              "status": "Sem Pedágio Eletrônico"
          },
          "cartaFrete": {
              "status": "Sem Carta Frete Eletrônica"
          },
          "financeiro": {
              "status": "Cancelado"
          },
          "CTe": {
              "status": "Sem CT-e Eletrônico"
          },
          "averbacao": {
              "status": "Sem Averbação"
          },
          "microSeguro": {
              "status": "Não contratado"
          },
          "MDFe": {
              "status": "Sem MDF-e"
          },
          "NFSe": {
              "status": "Sem NFS-e"
          }
      }
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 500 | Falha ao processar sua requisição. Verifique a mensagem. |
| 404 | Não foi encontrado nenhum CT-e com os dados informados. |

---

## Listar operadoras de VP-e disponíveis

Esse método retorna todas as operadores de Vale Pedágio eletrônico disponíveis para emissão.

**Método: GET**

**Rota:** /cadastro/getOperadorasVPE

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | tipoPagamentoPegadio | Array | Tipo de pagamento do pedágio |
| tipoPagamentoPegadio | codPagamento | Number (2) | Código do tipo de pagamento |
| tipoPagamentoPegadio | descPagamento | String (60) | Descrição do tipo de pagamento |
| tipoPagamentoPegadio | obrigaNrCartao | Boolean | Indica se é obrigatório o número do cartão |

### Exemplo de Response

```json
{
    "tipoPagamentoPedagio": [
        {
            "codPagamento": 7,
            "descPagamento": "Tag - Target Via Facil",
            "obrigaNrCartao": false
        }
    ]
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 404 | Nenhuma operadora de VP-e cadastrada |
| 422 | Não foi possível processar a transação |
| 500 | Falha ao processar sua requisição. Verifique a tag message. |

---

## Inserir Ordem de Coleta

Esse método permite o cadastro de uma Ordem de Coleta.

**Método: POST**

**Rota:** /OrdemColeta/postOrdemColeta

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | codigoFilialContrato | S | Number (4) | Código da Filial do Contrato |
| Principal | numeroContrato | S | Number (8) | Número do Contrato |
| Principal | sequencialVariante | S | Number (4) | Sequencial de variante do Contrato |
| Principal | valorMercadoriaGerenciamentoRisco | S | Number (15,3) | Valor da Mercadoria em Gerenciamento de Risco |
| Principal | placaCavalo | S | String (15) | Placa do cavalo |
| Principal | placaCarreta1 | N | String (15) | Placa da carreta 1 |
| Principal | placaCarreta2 | N | String (15) | Placa da carreta 2 |
| Principal | placaCarreta3 | N | String (15) | Placa da carreta 3 |
| Principal | cpfMotorista | S | String (14) | CPF do Motorista |
| Principal | codigoRemetente | S | Number (7) | Código do remetente |
| Principal | codigoEnderecoRemetente | S | Number (2) | Código do endereço do remetente |
| Principal | codigoDestinatario | S | Number (7) | Código do destinatário |
| Principal | codigoEnderecoDestinatario | S | Number (2) | Código do endereço do destinatário |
| Principal | dataColeta | S | Date | Data da Ordem de Coleta |
| Principal | descricaoUsuario | S | String (2000) | Descrição do usuário |
| Principal | itensColeta | S | Array | Array de Itens da Coleta |
|  |  |  |  |  |
| Itens Coleta | descricaoItem | S | String (60) | Descrição do Item |
| Itens Coleta | quantidade | S | Number (15,3) | Quantidade do item |
| Itens Coleta | peso | S | Number (15,3) | Peso do item |
|  |  |  |  |  |
| Principal | codigoConsignatario | N | Number (7) | Código do consignatário |
| Principal | codigoEnderecoConsignatario | N * | Number (2) | Código de endereço do consignatário |
| Principal | codigoExpedidor | N | Number (7) | Código do expedidor |
| Principal | codigoEnderecoExpedidor | N * | Number (2) | Código de endereço do expedidor |
| Principal | codigoRecebedor | N | Number (7) | Código do recebedor |
| Principal | codigoEnderecoRecebedor | N * | Number (2) | Código de endereço do recebedor |

* Caso o campo diretamente acima seja informado, passa a ser obrigatório.

### Exemplo de Request

```json
{
    "codigoFilialContrato": "1",
    "numeroContrato": "123724",
    "sequencialVariante": 1,
    "valorMercadoriaGerenciamentoRisco": "100000",
    "placaCavalo": "QTR9605",
    "placaCarreta1": "RBK7218",
    "placaCarreta2": "RBK7048",
    "placaCarreta3": "RBK7128",
    "cpfMotorista": "75228033149",
    "codigoRemetente": "6264778",
    "codigoEnderecoRemetente": "1",
    "codigoDestinatario": "5138736",
    "codigoEnderecoDestinatario": "1",
    "dataColeta": "13/09/2021",
    "descricaoUsuario": "Sicrano dos Santos",
    "itensColeta": [
        {
            "quantidade": "10000",
            "peso": "15000",
            "descricaoItem": "SOJA"
        }
    ]
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number (3) | Código de retorno do HTTP |
| Principal | message | String (2000) | Mensagem de retorno |
| Principal | filialOrdemColeta | Number (4) | Código da filial do contrato |
| Principal | numeroOrdemColeta | Number (8) | Número da Ordem de Coleta |
| Principal | linkGetDocumento | String (200) | Link do PDF da Ordem de Coleta |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "Sucesso",
    "filialOrdemColeta": 1,
    "numeroOrdemColeta": 4,
    "linkGetDocumento": "/maxys-webhook/documentoCTe/getDocumento?tipoDocumento=8&empresa=1&ordemColeta=4"
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 500 | Falha ao processar sua requisição. Verifique a mensagem de erro. |

---

## Consultar conjunto

Esse método permite a consulta de um conjunto a partir da placa do cavalo.

**Método:** GET

**Rota:** /…/getConjunto?nrPlaca={nrPlaca}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | nrPlaca | S | String (15) | Número da placa do cavalo |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | idConjunto | Number (15) | Identificador do conjunto |
| Principal | cpfMotorista | String (14) | CPF do motorista do conjunto |
| Principal | nomeMotorista | String(60) | Nome do motorista do conjunto |
|  |  |  |  |
| Principal | contato | Array | Contatos do conjunto |
| contato | telefone | String (15) | Numero de telefone do conjunto |
|  |  |  |  |
| Principal | dataUltimoCarregamento | Date | Data do ultimo carregamento com o conjunto |
| Principal | cavalo | String (15) | Placa do cavalo  |
| Principal | tipoCavalo | String (60) | Tipo do veiculo |
| Principal | documentoPropCavalo | String (14) | CPF/CNPJ do proprietário do cavalo |
| Principal | nomePropCavalo | String(60) | Nome do proprietário do cavalo |
| Principal | carreta1 | String (15) | Placa da primeira carreta do conjunto |
| Principal | tipoCarreta1 | String (60) | Tipo do veiculo |
| Principal | documentoPropCarreta1 | String (14) | CPF/CNPJ do proprietário da primeira carreta |
| Principal | nomePropCarreta1 | String(60) | Nome do proprietário da primeira carreta |
| Principal | carreta2 | String (15) | Placa da segunda carreta do conjunto |
| Principal | tipoCarreta2 | String (60) | Tipo do veiculo |
| Principal | documentoPropCarreta2 | String (14) | CPF/CNPJ do proprietário da segunda carreta |
| Principal | nomePropCarreta2 | String(60) | Nome do proprietário da segunda carreta |
| Principal | carreta3 | String (15) | Placa da terceira carreta do conjunto |
| Principal | tipoCarreta3 | String (60) | Tipo do veiculo |
| Principal | documentoPropCarreta3 | String (14) | CPF/CNPJ do proprietário da terceira carreta |
| Principal | nomePropCarreta3 | String(60) | Nome do proprietário da terceira carreta |

### Exemplo de Response

```json
{
    "idConjunto": 1,
    "cpfMotorista": "12345678901",
    "nomeMotorista": "",
    "contato": [
        {
            "telefone": "34998250447"
        }
    ],
    "dataUltimoCarregamento": "",
    "cavalo": "ABC1234",
    "tipoCavalo": "CAVALO",
    "documentoPropCavalo": "12345678901",
    "nomePropCavalo": "TRANSPORTES LTDA",
    "carreta1": "CBA1234",
    "tipoCarreta1": "CARRETA",
    "documentoPropCarreta1": "29139893000132",
    "nomePropCarreta1": "TRANSPORTES LTDA",
    "carreta2": "",
    "tipoCarreta2": "",
    "documentoPropCarreta2": "",
    "nomePropCarreta2": "",
    "carreta3": "",
    "tipoCarreta3": "",
    "documentoPropCarreta3": "",
    "nomePropCarreta3": ""
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 404 | Não foi encontrado nenhum conjunto para a placa informada |
| 500 | Erro ao consultar dados do conjunto |

---

## Cadastro de conjunto

Esse método permite o cadastro de um conjunto no Maxys.

**Método: POST**

**Rota:** /Conjunto/postConjunto

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | ExternalId | N | Number | Código identificador único da junção no gerenciamento de risco |
| Principal | Comments | N | String (4000) | Observações da junção |
| Principal | ProductValue | N | Number | Valor de mercadoria |
| Principal | Driver | S |  | Seção de dados do motorista |
|  |  |  |  |  |
| Driver | Document | S | String (11) | CPF do motorista |
| Driver | Name | S | String (60) | Nome do motorista |
| Driver | DateOfBirthday | S | Date | Data de nascimento do motorista |
| Driver | Document2 | S | String (20) | Número do RG do motorista |
| Driver | IssueDateDocument2 | S | Date | Data de emissão do RG do motorista |
| Driver | IssueStateDocument2 | S | String (2) | Unidade Federativa de emissão do RG do motorista |
| Driver | Document3 | S | String (15) | Número da CNH do motorista |
| Driver | CategoryDocument3 | S | String (2) | Categoria da CNH do motorista |
| Driver | DueDateDocument3 | S | Date | Data de vencimento da CNH do motorista |
| Driver | EmitterDocument3 | S | String (2) | Unidade Federativa de emissão da CNH do motorista |
| Driver | IssueCityDocument3 | S | Number (7) | Código IBGE do município de emissão da CNH do motorista |
| Driver | FirstDateDocument3 | S | Date | Data de emissão da primeira CNH do motorista |
| Driver | FatherName | S | String (60) | Nome do pai do motorista |
| Driver | MotherName | S | String (60) | Nome da mãe do motorista |
| Driver | Postcode | S | String (8) | CEP do endereço do motorista |
| Driver | Address | S | String (60) | Nome da rua do endereço do motorista |
| Driver | Number | S | String (7) | Número do endereço do motorista |
| Driver | Complement | N | String (30) | Complemento do endereço do motorista |
| Driver | County | S | String (100) | Bairro do endereço do motorista |
| Driver | City | S | Number (7) | Código IBGE do município do endereço do motorista |
| Driver | Landline | N | String (15) | Número de telefone do motorista |
| Driver | CommercialLandline | N | String (60) | Número de telefone da referência comercial do motorista |
| Driver | CommercialContact | N | String (15) | Descrição da referência comercial do motorista |
| Driver | ReferenceLandline | N | String (60) | Número de telefone da referência pessoal do motorista |
| Driver | ReferenceContact | N | String (15) | Descrição da referência pessoal do motorista |
| Driver | DriverProfileCode | N | Number | Código do perfil do motorista (TABELA 02) |
| Driver | Pis | N | Number | Número do PIS do motorista |
| Driver | References | N | Array | Vetor com 3 seções de referências para o motorista |
| Driver.References | Phone | N | String (15) | Número de telefone da referência |
| Driver.References | Name | N | String (60) | Descrição da referência |
|  |  |  |  |  |
| Principal | DeviceRegisters | S | Array | Vetor com as seções de informações dos veículos |
| DeviceRegisters | Document | S | String (14) | CPF ou CNPJ do proprietário do veículo |
| DeviceRegisters | Name | S | String (60) | Nome do proprietário do veículo |
| DeviceRegisters | Postcode | S | String (8) | CEP do endereço do proprietário do veículo |
| DeviceRegisters | Address | S | String (60) | Nome da rua do endereço do proprietário do veículo |
| DeviceRegisters | Number | S | String (7) | Número do endereço do proprietário do veículo |
| DeviceRegisters | Complement | N | String (30) | Complemento do endereço do proprietário do veículo |
| DeviceRegisters | County | S | String (100) | Bairro do endereço do proprietário do veículo |
| DeviceRegisters | City | S | Number (7) | Código IBGE do município do endereço do proprietário do veículo |
| DeviceRegisters | Landline | N | String (15) | Número de telefone do proprietário do veículo |
| DeviceRegisters | Plate | S | String (15) | Placa do veículo |
| DeviceRegisters | CityPlate | S | Number (7) | Código IBGE de registro do veículo |
| DeviceRegisters | Document3 | S | String (12) | Número do Renavam do veículo |
| DeviceRegisters | DeviceBrand | S | String (100) | Marca do veículo (enviar código identificador, para relacionamento com DE/PARA) |
| DeviceRegisters | DeviceModel | S | String (100) | Modelo do veículo (enviar código identificador, para relacionamento com DE/PARA) |
| DeviceRegisters | DeviceType | S | String (100) | Tipo do veículo (enviar código identificador, para relacionamento com DE/PARA) |
| DeviceRegisters | Document4 | S | String (30) | Chassis do veículo |
| DeviceRegisters | Year | S | Number (4) | Ano de fabricação do veículo |
| DeviceRegisters | Document2 | S | String (20) | Número do RNTRC |
| DeviceRegisters | NameDocument2 | S | String (60) | Nome do proprietário do RNTRC |
| DeviceRegisters | DueDocument2 | S | Date | Data de vencimento do RNTRC |
| DeviceRegisters | Document5 | N | String (14) | CPF ou CNPJ do proprietário do RNTRC, caso diferente do proprietário do veículo |
| DeviceRegisters | Postcode5 | N | String (8) | CEP do endereço do proprietário do RNTRC, caso diferente do proprietário do veículo |
| DeviceRegisters | Address5 | N | String (60) | Nome da rua do endereço do proprietário do RNTRC, caso diferente do proprietário do veículo |
| DeviceRegisters | Number5 | N | String (7) | Número do endereço do proprietário do RNTRC, caso diferente do proprietário do veículo |
| DeviceRegisters | Complement5 | N | String (30) | Complemento do endereço do proprietário do RNTRC, caso diferente do proprietário do veículo |
| DeviceRegisters | County5 | N | String (100) | Bairro do endereço do proprietário do RNTRC, caso diferente do proprietário do veículo |
| DeviceRegisters | City5 | N | Number (7) | Código IBGE do município do endereço do proprietário do RNTRC, caso diferente do proprietário do veículo |
| DeviceRegisters | Color | N | String | Cor do veículo |
| DeviceRegisters | Axes | N | Number | Número de eixos do veículo |
| DeviceRegisters | pisOwner | N | Number | Número do PIS do proprietário do veículo |
| DeviceRegisters | pisTenant | N | Number | Número do PIS do locatário do veículo |
| DeviceRegisters | ownerMatchedTAC | N | Boolean | Indica se o proprietário do veículo é TAC/TAC equiparado (Transportador autônomo de cargas) |
| DeviceRegisters | tenantMatchedTAC | N | Boolean | Indica se o locatário do veículo é TAC/TAC equiparado (Transportador autônomo de cargas) |
|  |  |  |  |  |
| Principal | Document | N | Array | Vetor com as seções de documentos anexados |
| Document | DocumentContent | S | Base 64 | Imagem no formate Base 64 |
| Document | DocumentType | S | Number | Código do tipo do documento (TABELA 01) |
| Document | Observation | N | String | Observações do documento |

### TABELA 01 - **Códigos de tipo de documento**

| Código | Descrição |
| --- | --- |
| 0 | CNH do Motorista |
| 1 | Comprovante de endereço do motorista |
| 2 | CRLV do cavalo |
| 3 | CRLV da carreta 01 |
| 4 | CRLV da carreta 02 |
| 5 | CRLV da carreta 03 |
| 6 | Foto do motorista |
| 7 | Foto do cavalo |
| 8 | Foto da carreta 01 |
| 9 | Foto da carreta 02 |
| 10 | Foto da carreta 03 |
| 11 | Foto do chassi do cavalo |
| 12 | Foto do chassi da carreta 01 |
| 13 | Foto do chassi da carreta 02 |
| 14 | Foto do chassi da carreta 03 |
| 15 | RNTRC do cavalo |
| 16 | RNTRC da carreta 01 |
| 17 | RNTRC da carreta 02 |
| 18 | RNTRC da carreta 03 |
| 19 | Outros 01 |
| 20 | Outros 02 |
| 21 | Outros 03 |
| 22 | Outros 04 |

### TABELA 02 - **Códigos de perfil de motorista**

| Código | Descrição |
| --- | --- |
| 1 | Agregado |
| 2 | Autônomo |
| 3 | Frota |
| 4 | RH |
| 5 | Terceiro |

### Exemplo de Request

```json
{
  "ExternalId": null,
  "Driver": {
    "Document": "52771345579",
    "Name": "Emanuel Cláudio Silva",
    "DateOfBirthday": "04/11/1997",
    "Document2": "425195855",
    "IssueDateDocument2": "01/02/2015",
    "IssueStateDocument2": "PR",
    "Document3": "32425979301",
    "CategoryDocument3": "E",
    "DueDateDocument3": "31/12/2023",
    "IssueCityDocument3": "3169109",
    "IssueStateDocument3": "MG",
    "FirstDateDocument3": "31/12/2010",
    "FatherName": "Melissa Mirella",
    "MotherName": "Cauã Otávio Silva",
    "Postcode": "85807090",
    "Address": "RUA FORTALEZA",
    "Number": "216",
    "Complement": "ENDERECO TESTE",
    "County": "TROPICAL",
    "City": "4104808",
    "State": "PR",
    "Landline": "45989225437",
    "CommercialLandline": "526686",
    "CommercialContact": "TESTE",
    "ReferenceLandline": "526685",
    "ReferenceContact": "TESTE",
    "DriverProfileCode": "1",
    "Pis": "123456789",
    "References": [
      {
        "Phone": "44998049893",
        "Name": "TESTE1"
      },
      {
        "Phone": "44998049893",
        "Name": "TESTE 2"
      },
      {
        "Phone": "44998049893",
        "Name": "TESTE 3"
      }
    ]
  },
  "DeviceRegisters": [
    {
      "Document": "20426272919",
      "Name": "EDSON LEVI DA CRUZ",
      "Postcode": "85807090",
      "Address": "RUA FORTALEZA",
      "Number": "216",
      "Complement": "ENDERECO TESTE",
      "County": "TROPICAL",
      "City": "4104808",
      "Landline": "45989225437",
      "Contact": "EDSON LEVI DA CRUZ",
      "CommercialLandline": "526685",
      "Plate": "JYX1812",
      "CityPlate": "4127700",
      "Document3": "76367066106",
      "DeviceBrand": "1",
      "DeviceModel": "11",
      "DeviceType": "1",
      "Document4": "654153495487",
      "Year": "2009",
      "Document2": "46546854170",
      "NameDocument2": "Emanuel Cláudio Silva",
      "DueDocument2": "31/12/2030",
      "Document5": "20426272919",
      "Postcode5": "85807090",
      "Address5": "RUA FORTALEZA",
      "Number5": "216",
      "Complement5": "ENDERECO TESTE",
      "County5": "TROPICAL",
      "City5": "4104808",
      "Color": "Azul",
      "Axes": "1",
      "pisOwner": "123456789",
      "pisTenant": "123456789",
      "matchedTAC": true
    }
  ],
  "Comments": "TESTE DE ENVIO DE FICHA - AMBIENTE DE TESTE",
  "Document":[
      {
        "DocumentContent": "image/png;base64,sgsgsfrwgyerwghs",
        "DocumentType": "0",
        "Observation": "Observação"
      }
   ]
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number (3) | Código de retorno  |
| Principal | message | String (2000) | Mensagem de retorno |
| Principal | externalId | Number (10) | Código identificador único da junção no gerenciamento de risco |
| Principal | securityAnalysis | Boolean | Identificador de análise de segurança |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "Sucesso",
    "ExternalId": 71,
    "securityAnalysis": true
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 500 | Erro de execução. Verifique a tag message. |

---

## Consultar CT-e

Esse método permite a consulta de um CT-e emitido.

**Método:** GET

**Rota:** /Cte/getCte

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | cpfMotorista | S * | String (15) | CPF do Motorista |
| Principal | numeroCte | S * | Number (10) | Número do CT-e |
| Principal | serieCte | S* | String (5) | Série do CT-e |
| Principal | chaveCfe | N | String (30) | Código de barras da CF-e  |
| Principal | chaveCte | N | String (60) | Chave de acesso do CT-e |

*: Ao menos um dos campos deve ser informado

### Exemplo de Request

```json
{
    "cpfMotorista": "43575080968",
    "numeroCte": 378869,
    "serieCte": "1"
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number (3) | Código da requisição HTTP |
| Principal | cause | String (2000) | Descrição da causa da mensagem |
| Principal | message | String (2000) | Mensagem de retorno |
| Principal | numeroCte | Number (10) | Número do CT-e |
| Principal | serieCte | String (5) | Série do CT-e |
| Principal | codigoFilial | Number (4) | Código da filial |
| Principal | nomeFilial | String (60) | Nome da filial |
| Principal | contrato | Number (8) | Número do contrato |
| Principal | varianteContrato | Number (4) | Número de variante do contrato |
| Principal | dataEmissaoCte | Date | Data de emissão do CT-e |
| Principal | valorMotorista | Number (15,3) | Valor do frete motorista |
| Principal | valorAdiantamentoMotorista | Number (15,3) | Valor de adiantamento ao motorista |
| Principal | valorAdiantamentoSaldo | Number (15,3) | Valor do saldo de adiantamento |
| Principal | produto | String(70) | Descrição do produto |
| Principal | pesoCarregado | Number (15,3) | Peso bruto do CT-e |
| Principal | cpfMotorista | String (14) | CPF do Motorista |
| Principal | nomeMotorista | String (60) | Nome do Motorista |
| Principal | placaCavalo | String (15) | Placa do cavalo |
| Principal | valeCombustivel | Object | Objeto referente ao Vale Combustível |
|  |  |  |  |
| Vale Combustivel | percentualValeCombustivel | Number (15,3) | Percentual do Vale Combustível |
| Vale Combustivel | valorValeCombustivel | Number (15,3) | Valor do Vale Combustível |

### Exemplo de Response

```json
{
    "code": 200,
    "cause": "Sucesso",
    "message": "Sucesso",
    "numeroCte": 378869,
    "serieCte": "1",
    "codigoFilial": 32,
    "nomeFilial": "UBERLANDIA - GO",
    "contrato": 123456,
    "varianteContrato": 1,
    "dataEmissaoCte": "13/09/2022",
    "valorMotorista": 5000.000,
    "valorAdiantamentoMotorista": 2500.000,
    "valorAdiantamentoSaldo": 1000.000,
    "produto": "1 - SOJA",
    "pesoCarregado": 32000.000,
    "cpfMotorista": "12345678901",
    "nomeMotorista": "TESTE MOTORISTA",
    "placaCavalo": "ABC1234",
    "valeCombustivel": {
        "percentualValeCombustivel": 50.000,
        "valorValeCombustivel": 2001.600
    }
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 406 | Nem todos os campos obrigatórios foram informados |
| 404 | CT-e não encontrado |
| 500 | Erro inesperado. Verifique a tag message. |