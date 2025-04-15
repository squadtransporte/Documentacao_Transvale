# Documentação API's Transvale

# Histórico de versões

| Versão | Modificado por | Alterações |
| --- | --- | --- |
| 1 | Daniel Schmitz, Mateus Cavalcante, Lucas Michalski | Criação da documentação |
| 2 | Daniel Schmitz | Incluído endpoints para pagamento de carta frete |
| 3 | Daniel Schmitz | Incluído endpoint para estorno de processo de caixa |
| 4 | Simon Luca | Incluído endpoint para quitação de CFe |
| 5 | Simon Luca | Incluído endpoint para geração de Fatura |
| 6 | Simon Luca | Incluído endpoint para geração de Despesa |

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

[GET Pagamento CT-e](#get-pagamentocte)

[GET Adicionais](#get-adicionais)

[POST Pagamento CT-e](#post-postpagamentocte)

[POST Processa Lote](#post-processalote)

[Estorno de Processo de Caixa](#estorno-de-processos-de-caixa)

[GET Voucher](#get-voucher)

[Vincular Nota Fiscal ao voucher](#vincula-nota)

[Gera fatura Voucher](#gera-fatura-voucher)

[POST Encerra MDFE](#post-encerramdfe)

[POST Quitar CFe](#post-quitar-cfe)

[POST Gerar Fatura](#post-gerar-fatura)

[POST Gerar Despesa](#post-gerar-despesa)

# Visão geral

Esta API foi criada para facilitar a comunicação entre o Centro de Manifesto Compartilhado da Transvale e o Maxys.

Será disponibilizado dois ambientes:

**Homologação**: [http://177.124.178.167:5056/integrador-transvale](http://177.124.178.167:5056/integrador-transvale)

**Produção**: [http://177.124.178.167:5055/integrador-transvale](http://177.124.178.167:5055/integrador-transvale)

## Autenticação

A autenticação é feita através do método basic, o usuário e senha deve ser solicitado ao TI da Transvale.

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

## GET PagamentoCte

Este método exibe as informações da geração de relação no TAF007 para ser possivel ter uma noção dos valores antes de realizar o processo. Oferece a mesma visão do TAF007 no Maxys.

**Método: GET**

**Rota:** /pagamentoCte/getPagamento?getPagamento?numeroCte={numeroCte}&cpfMotorista={cpfMotorista}&serieCte={serieCte}&numeroParcela={numeroParcela}&pesoDestino={pesoDestino}

### Relação de campos - Response

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | numeroCte | S | Number (10) | Numero do CT-e para ser consultado |
| Principal | cpfMotorista | S | String (11) | Cpf do Motorista relacionado ao CT-e |
| Principal | serieCte | S | Number (5) | Série do CT-e informado |
| Principal | chaveCte | N | String(60) | Chave de acesso do CT-e |
| Principal | chaveCfe | N | Number(15) | Chave da CF-e |
| Principal | numeroParcela | S | Number(1) | Numero da Parcela TAF007 (TABELA01) |
| Principal | tipoPagamento | S | String(1) | Pagamento referente ao TAF007 (TABELA02) Padrão “D” |
| Principal | pesoDestino | N | Number(15,3) | Peso destino para simular o adicional de quebra. OBS: Usado somente com a parcela 2 |

### TABELA 01 - Parcela referente ao TAF007

| Código | Descrição |
| --- | --- |
| 1 | Adiantamento |
| 2 | Saldo da Carta |

### TABELA 02 - Pagamento referente ao TAF007

| Código | Descrição |
| --- | --- |
| D | Com Documento |
| A | Antecipado |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number(3) | Código do retorno |
| Principal | message | String(1000) | Mensagem de retorno |
| Principal | documento | Objetct |  |
| documento | chaveDocumento | String(17) | Chave retornada no getPagamento |
| documento | numeroParcela | Number(1) | Numero da parcela correspondente (TABELA01) |
| documento | codigoTipoContaPagRec | Number(4) | Código do tipo da conta |
| documento | codigoClifor | Number(7) | Código do clifor |
| documento | nomeClifor | String(60) | Nome do clifor  |
| documento | numeroDocumento | Number(10) | Numero do documento |
| documento | valorSaldo | Number(15,3) | Valor do saldo |
| documento | codigoCmi | Number(5) | Código do CMI |
| documento | numeroCartaFrete | Number(15) | Numero da carta frete |
| documento | codigoContrato | Number(8) | Código do contrato de frete |
| documento | codigoEmprContrato | Number(4) | Empresa do contrato de frete |
| documento | codigoSeqContrato | Number(4) | Variante do contrato de frete |
| documento | codigoTransportador | Number(7) | Código do transportador  |
| documento | codigoEnderTransportador | Number(2) | Código do endereço do transportador |
| documento | numeroCfe | Number(15) | Numero da Carta Frete Eletronica |
| documento | codigoOperadoraCfe | Number(2) | Código da operadora  |
| documento | placaCavalo | String(7) | Placa do cavalo |
| documento | quantidadeVolumeDest | Number(15,3) | Quantidade de volume |
| documento | codigoCliforPagador | Number(7) | Código do clifor pagador |
| documento | nomeCliforPagador | String(60) | Nome do clifor pagador |
| documento | valorTarifaAgenc | Number(15,3) | Valor da tarifa agenciado |
| documento | valorFreteAgenc | Number(15,3) | Valor do frete agenciado |
| documento | valorAdiantamento | Number(15,3) | Valor do adiantamento |
| documento | valorPedagio | Number(15,3) | Valor do pedagio |
| documento | pesoLiquido | Number(15,3) | Peso liquido do frete |
| documento | pesoBrutoDestino | Number(15,3) | Peso bruto no destino (Quando cadastrado) |
| documento | percentualTolerancia | Number(6,2) | Percentual de tolerancia |
| documento | tipoTolerancia | String(1) | Tipo da tolerancia (Contrato TTB121) |
| documento | valorUnitarioFrete | Number(15,3) | Valor unitário do frete |
| documento | statusLocacao | String(1) | Status da locação |
| documento | ftCalculo | Number(12,6) | Fator de calculo  |
| documento | codigoTipoCalculoFrete | Number(3) | Código do tipo de calculo |
| documento | quantidadePesoTolerado | Number(15,3) | Quantidade de peso tolerado |
| documento | somaPedagioAdiantamento | Number(15,3) | Soma do pedagio adiantamento |
| documento | codigoSitDupl | Number(2) | Código da situação da duplicata (TABELA 02) |
| documento | valorSaldoCheio | Number(15,3) | Valor do saldo cheio |
| documento | valorAdiantamentoCheio | Number(15,3) | Valor adiantamento cheio |
| documento | valorTarifaMotCheio | Number(15,3) | Valor da tarifa motorista cheio |
| documento | valorFreteAgencCheio | Number(15,3) | Valor frete agenciado cheio |
| documento | codigoMotorista | Number(7) | Código do motorista |
| documento | nomeMotorista | String(60) | Nome do motorista |
| documento | valeCombustivel | Boolean | Indica se o CT-e possui vale combustivel |
| documento | adicionais  | Array |  |
| adicionais | codigoAdicional | Number(4) | Código do adicional de frete (TTB034) |
| adicionais | descricaoAdicional | String(60) | Descrição do adicional de frete |
| adicionais | tipoAdicional | String(5) | Tipo do adicional de frete (D - DIMINIU / S - SOMA) |
| adicionais | valorAdicional | Number(15,3) | Valor do adicional |
| documento | numeroAgrupamento | Number(15) | Código do CT-e agrupado |

### TABELA 01 - Parcela referente ao TAF007

| Código | Descrição |
| --- | --- |
| 1 | Adiantamento |
| 2 | Saldo da Carta |

### TABELA 01 - Códigos da situaçao de duplicata

| Código | Descrição |
| --- | --- |
| 0 | Pendente total |
| 1 | Liquidado parcialmente |
| 2 | Liquidado total |
| 8 | Programação financeira bloqueada |
| 9 | Cancelado |
| 10 | Pendente total - central |
| 11 | Liquidado parcialmente - central |
| 12 | liquidado total - central |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "Sucesso",
    "documento": {
        "chaveDocumento": "00050008042000031",
        "numeroParcela": 2,
        "codigoTipoContaPagRec": 206,
        "codigoClifor": 909432,
        "nomeClifor": "LUCAS MICHALSKI PF",
        "numeroDocumento": 20498,
        "valorSaldo": 789,
        "codigoCmi": null,
        "numeroCartaFrete": 20498,
        "codigoContrato": 105228,
        "codigoEmprContrato": 5,
        "codigoSeqContrato": 1,
        "codigoTransportador": 909432,
        "codigoEnderTransportador": 1,
        "numeroCfe": null,
        "codigoOperadoraCfe": "",
        "placaCavalo": "LAL1111",
        "quantidadeVolumeDest": null,
        "codigoCliforPagador": 909424,
        "nomeCliforPagador": "LUCAS MICHALSKI PJ",
        "valorTarifaAgenc": 50,
        "valorFreteAgenc": 1316,
        "valorAdiantamento": 527,
        "valorPedagio": 0,
        "pesoLiquido": 26320,
        "pesoBrutoDestino": null,
        "percentualTolerancia": 0.25,
        "tipoTolerancia": "T",
        "valorUnitarioFrete": 250,
        "statusLotacao": "N",
        "ftCalculo": 1000,
        "codigoTipoCalculoFrete": 9,
        "quantidadePesoTolerado": null,
        "somaPedagioAdiantamento": "N",
        "codigoSitDupl": 0,
        "valorSaldoCheio": 789,
        "valorAdiantamentoCheio": 527,
        "valorTarifaMotCheio": 50,
        "valorFreteAgencCheio": 100,
        "codigoMotorista": 909440,
        "nomeMotorista": "LUCAS MICHALSKI MOTORISTA",
        "valeCombustivel": true,
        "adicionais": [
            {
                "codigoAdicional": 26,
                "descricaoAdicional": "TAXA DE SEGURO DE CARGA",
                "tipoAdicional": "D",
                "valorAdicional": 219.21
            },
            {
                "codigoAdicional": 35,
                "descricaoAdicional": "MICRO SEGURO",
                "tipoAdicional": "D",
                "valorAdicional": 5.9
            },
            {
                "codigoAdicional": 1,
                "descricaoAdicional": "FALTA DE PESO/PRODUTO",
                "tipoAdicional": "D",
                "valorAdicional": 41969.61
            }
        ],
        "numeroAgrupamento": null
    }
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Não foi possivel consultar CT-e/CF-e |
| 500 | Erro ao consultar CT-e/CF-e. |

---

## GET Adicionais

Este método lista os adicionais existentes no maxys, retornando os dados referente a tela TTB034 do maxys.

**Método: GET**

**Rota:** /Cte/getAdicionais?codigoAdicional={codigoAdicional}&descricaoAdicional={descricaoAdicional}&tipoAdicional={tipoAdicional}&tipoRecPag={tipoRecPag}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | codigoAdicional | N | Number (4) | Código do adicional |
| Principal | descricaoAdicional | N | String (60) | Descrição do adicional |
| Principal | tipoAdicional | N | String (5) | Tipo do adicional. S - Soma / D - Diminui |
| Principal | tipoRecPag | N | String (1) | Indica se é recebimento (0) ou pagamento (1) |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number (3) | Código de retorno |
| Principal | message | String (200) | Mensagem de retorno |
| Principal | adicionais | Array | Array de adicionais |
|  |  |  |  |
| adicionais | codigoAdicional | Number (4) | Código do adicional |
| adicionais | descricaoAdicional | String (60) | Descrição do adicional |
| adicionais | tipoAdicional | String (5) | Tipo do Adicional. S- Soma / D- Diminui |
| adicionais | tipoRecPag | String (1) | Indica se é recebimento (0) ou pagamento (1) |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "Sucesso",
    "adicionais": [
        {
            "codigoAdicional": 1,
            "descricaoAdicional": "FALTA DE MERCADORIA MOTORISTA",
            "tipoAdicional": "D",
            "tipoRecPag": "P"
        }
    ]
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Erro ao consultar tipo adicional de frete. |
| 500 | Erro ao consultar tipo adicional de frete. Verifique a tag message. |

---

## POST postPagamentoCte

Este método irá realizar todo o processo de geração de relação do TAF007 até a execução do processo de caixa no FCT003

**Método: POST**

**Rota:** /pagamentoCte/postPagamento

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | cpfCnpjBeneficiario | S | String(14) | CPF ou CNPJ do beneficiário do pagamento |
| Principal | empresa | S | Number(4) | Código da empresa |
| Principal | formaPagamento | S | String(1) | Forma de pagamento usada no FCT003 (B - BANCO / H - CHEQUE) |
| Principal | cheques | S | Array |  |
| cheques | numeroCheque | S | Number(8) | Numero do cheque quando for a forma de pagamento “B” |
| cheques | serieCheque | S | String(3) | Serie do cheque |
| cheques | valorCheque | S | Number(15,3) | Valor a ser usado no cheque |
| cheques | codigoBanco | N | Number(3) | Código do banco. OBS: Somente necessário quando a forma de pagamento for “H” |
| Principal | documentos | Array |  |  |
| documentos | chaveDocumento | S | String(17) | Chave retornada do getPagamentoCte |
| documentos | numeroParcela | S | Number(2) | Parcela a ser paga referente ao TAF007 |
| documentos | pesoDestino | N | Number(15,3) | Peso de chegada somente quando for numero da parcela 2 |
| documentos | adicionais | Array |  |  |
| adicionais | codigoAdicional | S | Number(4) | Código do adicional de frete |
| adicionais | descricaoAdicional | S | String(60) | Descrição do adicional de frete |
| adicionais | tipoAdicional | S | String(5) | Tipo do adicional de frete |
| adicionais | statusAdicional | S | String(1) | Status do adicional de frete |
| adicionais | valorAdicional | S | Number(15,3) | Valor do adicional de frete |
| adicionais | dtChegada | N | Date | Data e Hora da chegada do motorista  |
| adicionais | hrTolerancia | N | Number | Quantidade de horas de tolerancia |
| adicionais | dtSaida | N | Date | Data e Hora da saida do motorista |
| adicionais | vlTarifa | N | Number(15,3) | Valor da tarifa da estadia |
| adicionais | vlEstadia | N | Number(15,3) | Valor da estadia |
| adicionais | vlPagoestadia | N | Number(15,3) | Valor que será pago |
| adicionais | hrRetroagir | N | Number | Quantidade de horas a retroagir |
| adicionais | dsObservpagto | N | String | Observação da Estadia |

```json
{
    "cpfCnpjBeneficiario": "81738290042",
    "empresa": 5,
    "formaPagamento": "H",
    "cheques": [
        {
            "numeroCheque": null,
            "serieCheque": "A",
            "valorCheque": 281.93,
            "codigoBanco": 1,
            "codigoAgencia": 285,
            "numeroConta": 2156574
        },
        {
            "numeroCheque": null,
            "serieCheque": "A",
            "valorCheque": 281.96,
            "codigoBanco": 1,
            "codigoAgencia": 285,
            "numeroConta": 2156574
        }
    ],
    "documentos": [
        {
            "chaveDocumento": "00050008038000031",
            "numeroParcela": 2,
            "pesoDestino": 26320,
            "adicionais": [
                {
                    "codigoAdicional": 26,
                    "descricaoAdicional": "TAXA DE SEGURO DE CARGA",
                    "tipoAdicional": "D",
                    "statusAdicional": "N",
                    "valorAdicional": 219.21
                },
                {
                    "codigoAdicional": 35,
                    "descricaoAdicional": "MICRO SEGURO",
                    "tipoAdicional": "D",
                    "statusAdicional": "N",
                    "valorAdicional": 5.9
                },
								{
                    "codigoAdicional": 5,
                    "descricaoAdicional": "PAGAMENTO ESTADIA",
                    "tipoAdicional": "S",
                    "dtChegada": "01/02/2023 13:30:00",
                    "dtSaida": "03/02/2023 17:20:00",
                    "hrTolerancia": 24, 
                    "vlTarifa": 0.2,  
                    "valorAdicional":  209.68,  
                    "vlEstadia": 209.68,    
                    "vlPagoestadia": 209.68 ,
                    "hrRetroagir": 12

                }
            ]
        }
    ]
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
|  Principal | code | Number(3) | Código do retorno |
|  Principal | message | String(1000) | Mensagem de retorno |
|  Principal | empresaRelacao | Number(4) | Empresa da relação do TAF007 |
|  Principal | idRelacao | Number(8) | Id da relação referente ao TAF007 |
|  Principal | numeroProcesso | Number(8) | Numero do processo de caixa |
|  Principal | statusProcesso | String(20) | Status do processo de caixa |
| Principal | idProcesso | String(12) | Id do processo que sera usado para o endpoint de processaLote |

### Exemplo de Response

```json
{
	"code": 200,
	"message": "Sucesso",
	"empresaRelacao": 5,
	"idRelacao": 1756,
	"numeroProcesso": 103073,
	"stastusProcesso": "Executado",
	"idProcesso": "000100000001"
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Erro ao gravar relação ou executar o processo de caixa. Verifique |
| 500 | Erro ao gravar relação ou executar o processo de caixa. Erro. |

---

## POST processaLote

Este método irá realizar a amarração dos processos que forem enviados em um lote externo para ser realizado a execução do processo de caixa via FCT003

**Método: POST**

**Rota:** /pagamentoCte/processaLote

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | processos | S | Array | Dentro desse array é enviado todos os idProcesso que são retornados no postPagamento |
| Principal | formaPagamento | S | String(15) | Forma de pagamento |

```json
{
    "formaPagamento": "DINHEIRO",
     "processos": [
          "000500103837",
          "000500103836"
          
     ]
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
|  Principal | code | Number(3) | Código do retorno |
|  Principal | message | String(1000) | Mensagem de retorno |
|  Principal | cause | String(1000) | Causa do retorno |
| Principal | idLoteExterno | Number(8) | Lote do processo externo para ser consultado no FCT003 |

### Exemplo de Response

```json
{
    "code": 200,
    "cause": "Sucesso",
    "message": "OK",
    "idLoteExterno": 7
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Erro ao gravar relação ou executar o processo de caixa. Verifique |
| 500 | Erro ao gravar relação ou executar o processo de caixa. Erro. |

---
## Estorno de Processos de Caixa

Método responsável por estornar os processo de caixas que pertencem a um frete lançado no sistema.

**Método:** POST

**Rota:** /pagamentoCte/postEstorno

## **Relação de campos - Request**

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | idProcesso | S | String(12) | Id do processo retornado ao gera-lo via API. |
| Principal | documentoUsuario | S | String(14) | CPF/CNPJ do usuário que está efetuando o estorno. |
| Principal | motivoCancelamento | S | Number(5) | Código do motivo do cancelamento. |

```json
{
  "idProcesso": "009900000736",
  "documentoUsuario": "21078384000135",
  "motivoCancelamento": 1
}
```

## **Relação de campos - Response**

| Nível | Campo | Tipo de Dados | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number(3) | Código do retorno |
| Principal | message | String(1000) | Mensagem de retorno |

```json
{
	"code": 200,
	"message": "Sucesso"
}
```

## **Possíveis códigos de erro**

| Código | Descrição |
| --- | --- |
| 422 | Erro ao estornar processo de caixa. Verifique. |
| 500 | Erro ao estornar processo de caixa. |
---

## GET Voucher

Este método exibe as informações do Voucher e caso seja enviado as tags para consumo, é realizada uma baixa do valor e então retornado o valor atualizado do voucher.

**Método:** **GET**

**Rota:** /integrador-transvale/Cte/getVoucher?idVoucher={idVoucher}&cpfCnpj={cpfMotorista}&registroUtilizacao=true&vlConsumir=100

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | idVoucher | S | Varchar2(100) | Id do Voucher |
| Principal | vlConsumir | N | Number | Valor a ser consumido do Voucher |
| Principal | registroUtilizacao | N | Varchar2(10) | Verifica se ira ou não usar o Voucher |
| Principal | cpfCnpj | S | Varchar2(14) | CPF do Motorista |

### Exemplo de Request

```json
{
    "idVoucher": "27",
    "vlConsumir": "1500",
    "registroUtilizacao": "true",
    "cpfCnpj": "75372114002"
}
```

### Relação de campos - Response

| Nível | Campo               | Tipo de dado   | Descrição                                                                                                       |
| --- |---------------------|----------------|-----------------------------------------------------------------------------------------------------------------|
| Principal | DtEmissaoVoucher    | Date           | Data de Emissão do CT-e                                                                                         |
| Principal | vltotalVoucher      | Number(15,3)   | Valor total do Voucher                                                                                          |
| Principal | vlDisponivelVoucher | Number(15,3)   | Valor disponível do Voucher                                                                                     |
| Principal | status              | Varchar2(1)    | Retorna Status “E” Emitido, “C” Cancelado, “P” Utilizado Voucher Parcialmente, “T” Utilizado Voucher Totalmente |
| Principal | cpfMotorista        | Varchar2(14)   | CPF do Motorista                                                                                                |
| Principal | nomeMotorista       | Varchar2(60)   | Nome do Motorista                                                                                               |
| Principal | fotoMotorista       | Varchar2(2000) | Foto do Motorista em base64                                                                                     |
| Principal | idTransacao         | Number(30)     | Identificador da transação de consumo                                                                           |

### Exemplo de Response

```json
{
    "DtEmissaoVoucher": "18/05/23",
    "vltotalVoucher": 1316,
    "vlDisponivelVoucher": 0,
    "status": "E",
    "cpfMotorista": "75372114002",
    "nomeMotorista": "LUCAS MICHALSKI MOTORISTA",
    "fotoMotorista": "LzlqLzRBQVFTa1pKUmdBQkFRQUFBUUFCQUFELzJ3QkRBQUVCQVFFQ"
    "idTransacao": 123
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Erro não foi possível consultar o voucher |
| 500 | Erro ao consultar voucher |

## Vincula Nota

Este endpoint vincula uma nota fiscal a um ou mais consumos de voucher, e faz a entrada da nota automaticamente

**Rota:** /integrador-transvale/Cte/cte/vinculaVoucher

### Relação de campos - Request

| Nível | Campo        | Obrigatório | Tipo de dado     | Descrição                                                  |
| --- |--------------|-------------|------------------|------------------------------------------------------------|
| Principal | vouchers     | S           | Array de objetos | Lista de vouchers                                          |
| vouchers | idVoucher    | S           | Number           | Identificador do Voucher a ser vinculado                   |
| vouchers | chavesAcesso | S           | Array de Varchar | Lista com as chaves de acesso das notas a serem vinculadas |
| vouchers | transacoes   | S           | Array de number  | Identificador das transações a serem vinculadas a nota     |

### Exemplo de Request

```json
{
    "vouchers":[
        {
            "idVoucher":1,
            "chavesAcesso": [
                "12345678901234567890123456789012345678901234"
            ],
            "transacoes": [
                123,
                321
            ]
        }
    ]
}
```

### **Relação de campos - Response**

| Nível | Campo | Tipo de Dados | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number(3) | Código do retorno |
| Principal | message | String(1000) | Mensagem de retorno |

```json
{
	"code": 200,
	"message": "Sucesso"
}
```

### **Possíveis códigos de erro**

| Código | Descrição                                |
| --- |------------------------------------------|
| 422 | Erro ao vincular nota fiscal. Verifique. |
| 500 | Erro ao vincular nota fiscal.            |


# Gera Fatura Voucher

## POST geraFaturaVoucher

Esse método fará com que gere uma fatura no maxys sobre a nota fiscal vinculada ao voucher

**Método:** POST

**Rota:** /integrador-transvale/Cte/geraFaturaVoucher

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | chavesAcesso | S | String(100) | Chave de acesso usada na emissão da nota do voucher |
| Principal | formaPagamento | S | String(2) | Forma de Pagamento |
| Principal | cpfCnpjBeneficiario | S | String(14) | CPF/CNPJ do beneficiário do processo |
| Principal | dataPagamento | S | String(10) | Data de pagamento para o processo |

### Exemplo de Request

```json
{
    "chavesAcesso": ["15230510197621000241550010000592841000379508"],
    "formaPagamento": "CA",
    "cpfCnpjBeneficiario": "12332144411",
    "dataPagamento": "25/06/2024"
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | idProcesso | Number(8) | Número do processo gerado |
| Principal | idEmpresa | Number(4) | Empresa do processo gerado |

### Exemplo de Response

```json
{
    "code": 200,
    "message": "Sucesso",
    "idProcesso": 1053,
    "idEmpresa": 99
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Erro ao gerar fatura do voucher |
| 500 | Falha ao processar a requisição de gerar a fatura do voucher |

# POST encerraMdfe

Esse método fará com que encerre uma MDFE

**Método:** POST

**Rota:** /integrador-transvale/Cte/encerraMdfe

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | empresaCte | S | Number(4) | Empresa do CTe |
| Principal | lancamentoCte | S | Number(6) | Lançamento do CTe |
| Principal | serieCte | S | String(1) | Série do CTe |
| Principal | fatesCte | S | String(1) | Tipo faturamento do CTe |
| Principal | empresaMdfe | S | Number(4) | Empresa MDFE |
| Principal | numeroMdfe | S | Number(6) | Núemro MDFE |
| Principal | serieMdfe | S | Number(1) | Série MDFE |

### Exemplo de Request

```json
{
    "cte": [
        {
            "empresaCte": 1,
            "lancamentoCte": 1,
            "serieCte": "1",
            "fatesCte": "1"
        }
    ],
    "mdfe": [
        {
            "empresaMdfe": 1,
            "numeroMdfe": 1,
            "serieMdfe": 1
        }
    ]
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | String | 200 (Sucesso) |
| Principal | message | String | Sucesso |

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
| 422 | Erro interno |
| 500 | Falha ao processar a requisição |

# Quitar CFe

## POST quitar CFe

Este método irá efetuar a liberação da parcela da CFe para que possa ser quitada.

**Método:** POST

**Rota:** /acertoCfe/quitar

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | chaveDocumento | S | String(17) | Chave retornada no getPagamento e getPagamentoCte  |
| Principal | usuario | S | String(14) | CPF do usuário que está fazendo a requisição |
| Principal | numeroParcela | S | Number (4) | Número da parcela que será liberada |

### Exemplo de Request

```json
{
    "chaveDocumento": "00050008042000031",
    "usuario": "61420325019",
    "numeroParcela": 1
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
    "message": "Sucesso."
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 404 | Não foram encontradas ordens de coleta para os filtros informados. |
| 500 | Erro interno do servidor. Verificar a tag message |

---

# Gerar Fatura

## POST Gerar Fatura

Este método irá gerar a fatura com base nos documentos repassados e retornar um layout de fatura para recebimento.

**Método:** POST

**Rota:** /recebimentoCte/postRecebimento

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | cliente | S | Number | Código do cliente para geração da Fatura  |
| Principal | filialFatura | S | Number | Filial para geração da Fatura  |
| Principal | codigoBanco | S | Number | Código do banco para geração da Fatura  |
| Principal | codigoAgencia | S | Number | Código da agência para geração da Fatura  |
| Principal | formaPagamento | S | String(5) | Forma de pagamento da Fatura  |
| Principal | contaCorrente | S | String(20) | Código da conta corrente  |
| Principal | dataEmissao | N | String(10) | Data de emissão da fatura |
| Principal | dataVencimento | N | String(10) | Data de vencimento da fatura |
| Principal | documentos | S | Array de Objetos | Relação de documentos para gerar a Fatura |
| documentos | empresa | S | Number | Código da empresa do documento |
| documentos | lancamento | S | Number | Número de lançamento do documento |
| documentos | serie | S | Number | Série do documento |

### Exemplo de Request

```json
{
		"cliente": 909980,
		"filialFatura": 99,
		"codigoBanco": 1,
		"codigoAgencia": 1,
		"formaPagamento": "CA",
		"contaCorrente": "0033",
	
		"documentos": [
				{
						"empresa": 99,
						"lancamento": 2051,
						"serie": "4"
				},
				{
						"empresa": 99,
						"lancamento": 2067,
						"serie": "4"
				},
				{
						"empresa": 99,
						"lancamento": 2072,
						"serie": "4"
				}
		]
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number | Código retorno HTTP |
| Principal | message | String | Mensagem de retorno |
| Principal | numeroFatura | Number | Código da fatura gerada |
| Principal | FATURA | Objeto | Objeto com informações da geração do layout da Fatura |
| FATURA | url | String | Url para geração do PDF do layout de fatura |
| FATURA | id | String | Código identificador |
| FATURA | mensagemErro | String | Mensagem de erro caso ocorra durante a geração da Fatura |

### Exemplo de Response

```json
{
	"code": 200,
	"message": "Sucesso",
	"numeroFatura": 185,
	"FATURA": {
		"url": "HTTP://WINVM-SQUADTRANSP/MAXICONREPORT/EasyPrint?c=%5C%5Cwinvm-squadtransp%5Cmaxicon%5CMaxicon%5CPrincipal%5CDFE023.rpx&m=ST_ATUALIZA=N%7CNR_SID=46592575&exportar=true&t=PDF",
		"id": "46592575",
		"mensagemErro": []
	}
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Erro interno |
| 500 | Falha ao processar a requisição |

---

# Gerar Despesa

## POST Gerar Despesa
Este método irá gerar uma despesa de frota, sendo possível efetuar o rateio por centro de custo.

**Método:** POST

**Rota:** /recebimentoCte/postRecebimento

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | dataCompetencia | S | String(10) | Data de competência da despesa  |
| Principal | codigoFilial | S | Number | Filial para geração da despesa  |
| Principal | numeroPlaca | S | String(10) | Número da placa do veículo  |
| Principal | codigoRota | S | Number | Código da rota  |
| Principal | codigoMotorista | S | String(5) | Código do motorista |
| Principal | codigoNegocio | S | String(20) | Código do negocio  |
| Principal | numeroDocumento | N | String(10) | Número do documento da despesa |
| Principal | horimetroRefrigerador | N | String(10) | Horímetro do bau refrigerador |
| Principal | dataLancamento | S | String(10) | Data de lançamento da despesa |
| Principal | kilometragemFinal | S | Number | Kilometragem final do veículo |
| Principal | condicaoPagamento | S | Number | Condição de pagamento |
| Principal | usuario | N | String(5) | Código do usuário do lançamento |
| Principal | centrosCusto | S | Array de Objetos | Relação de centros de custo que será gerada a despesa |
| centrosCusto | codigo | S | Number | Código do centro de custo |
| Principal | itens | S | Array de Objetos | Relação de Itens da despesa |
| itens | codigoDespesa | N | Number | Código da despesa |
| itens | pesoAtendido | S | Number | Peso do item |
| itens | codigoMovimentacao | S | Number | Código da movimentação |
| itens | valor | S | Number | Valor total do item |
| itens | observacao | N | String(60) | Observação do item |
| itens | codigoItem | S | Number | Código do item |

### Exemplo de Request

```json
{
          "dataCompetencia": "04/2025",
          "codigoFilial": 99,
          "numeroPlaca": "SEM0J22",
          "codigoRota": 280,
          "codigoMotorista": 403300,
          "codigoNegocio": 1,
          "numeroDocumento": "244413",
          "horimetroRefrigerador": "32",
          "dataLancamento": "15/04/2025",
          "kilometragemFinal": 5.300,
          "usuario": "SLR",
          "centrosCusto": [
                           {
                            "codigo": 1
                           }
                          ],
          "itens": [
                    {
                     "codigoDespesa": null,
                     "pesoAtendido": 30.000,
                     "codigoMovimentacao": 3000,
                     "valor": 10000,
                     "observacao": "OBSERVACAO DE TESTE",
                     "codigoItem": 1
                    }
                   ]
}
```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | code | Number | Código retorno HTTP |
| Principal | message | String | Mensagem de retorno |
| Principal | lancamentoDespesas | String(100) | Números dos lançamentos das despesas separados por "," |

### Exemplo de Response

```json
{
  "code" : 200,
  "message" : "Sucesso",
  "lancamentoDespesas" : "181,182"
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Erro interno |
| 500 | Falha ao processar a requisição |

---
