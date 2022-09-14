# Documentação v1

Data criação: September 12, 2022 2:56 PM
Data última alteração: September 14, 2022 9:47 AM
Status: Em progresso 🙌
Type: Especificação técnica

# Histórico de versões

| Versão | Modificado por | Alterações |
| --- | --- | --- |
| 1 | Daniel Schmitz, Mateus Cavalcante, Lucas Michalski | Criação da documentação |

# Sumário

# Visão geral

## /getListaOrdemColeta

**Método:** GET

**Rota:** /…/getListaOrdemColeta

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
    "numeroVarianteContrato": 2,
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
| Principal | numeroTotalNotas | Number (30) | Número total de notas vinculadas à OC  |
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
| 500 | Erro interno do servidor. |

---

## /finalizaEmissao

**Método:** POST

**Rota:** /…/finalizaEmissao

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | numeroOrdemColeta | S | Number (8) | Número da ordem de coleta do Maxys a ser finalizada |
| Principal | CPFUsuario | S | String (14) | Usuário que está finalizando a emissão da documentação |
| Principal | numeroAverbacao | N | String (40) | Número da averbação do CT-e |
| Principal | tipoServico | N | Number (2) | Tipo de serviço (TABELA 01) |
| Principal | chaveCTeMultimodal | N | String (60) | Chave de acesso do CT-e multimodal |
| Principal | indicadorNegociacao | N | Number (1) | Indicador de negociação (0 - Sim / 1 - Não) |
| Principal | Notas | S | Array | Nota para a finalização do CT-e |
|  |  |  |  |  |
| Notas  | numero | S | Number (15,3) | Número da nota fiscal |
| Notas | serie | S | String (3) | Série da nota fiscal |
| Notas | chaveAcesso | S | String (60) | Número da chave de acesso da nota fiscal para emissão automática de CT-e |
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
| Principal | numeroOrdemColeta |  | Number (8) | Número da ordem de coleta do Maxys a ser finalizada |
| Principal | status |  | String (200) | Status da ordem de carregamento na fila de emissão de CT-e |

Códigos de tipos de status (status)

| Código | Descrição |
| --- | --- |
| N | Não processado |
| P | Processando |
| F | Finalizado |
| A | Aguardando Emissão |
| E | Erro |

### Exemplo de Response

```json
{
    "nrOrdemCarregMaxys": 12345679,
    "status": "A"
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Validação de dados para finalização da Ordem de Carregamento |
| 404 | Não foi encontrada nenhuma ordem de carregamento para a finalização |
| 500 | Finalização de OC para emissão de CT-e/NFS-e |

---

## /consultar

**Método:** GET

**Rota:** /…/consultar

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
| Ordem Carregamento | emiteParcelaAdto | String (1) | Define se será emitida a parcela de adiantamento para o frete |
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
|  |  |  |  |
| Ordem Carregamento | geraNFSE | Boolean | Indica se deve gerar NFSE |
| Ordem Carregamento | geraDACTE | Boolean | Indica se deve gerar DACTE |
| Ordem Carregamento | geraMDFE | Boolean | Indica se deve gerar MDFE |
| Ordem Carregamento | geraTermoEstadia | Boolean | Indica se deve gerar Termo de Estadia |
| Ordem Carregamento | geraCFe | Boolean | Indica se deve gerar CFe |
| Ordem Carregamento | geraContratoFrete | Boolean | Indica se deve gerar Contrato Frete |
| Ordem Carregamento | geraCartaFrete | Boolean | Indica se deve gerar Carta Frete |
| Ordem Carregamento | dataCancelamento | Date (”DD/MM/RRRR HH24:MI:SS”) | Data de cancelamento da Ordem de Coleta |
| Ordem Carregamento | statusFilaEmissao | String (1) | Status da fila de emissao da Ordem de Coleta (Tabela 01) |
| Ordem Carregamento | statusEmissao | Number (1) | Status da emissão do CT-e (Tabela 02) |
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
| Juncao | descStatus | String (4000) | Descrição do status da junção |
| Juncao | observacaoGR | String (4000) | Observação sobre alteração de status da junção |
| Juncao | emiteCTe | Boolean | Indica se deve emitir CT-e |
|  |  |  |  |
| Ordem Carregamento | documentos | Array |  |
|  |  |  |  |
| Documentos | empresa | Number (4) | Código da empresa do CT-e |
| Documentos | numeroLancamento | Number (7) | Número de lançamento do CT-e |
| Documentos | numero | Number (10) | Número do CT-e |
| Documentos | serie | String (5) | Série do CT-e |
| Documentos | tipoLancamento | Number (1) | Código de status do CT-e(Tabela 03) |
|  |  |  |  |
| Ordem Carregamento | gerenciamentoRisco | Object |  |
|  |  |  |  |
| Gerenciamento Risco | liberacaoRastreamentoExterno | String (15) | Número da liberação da gerenciadora de risco externa |
| Gerenciamento Risco | codigoGerenciadora | Number (4) | Código da gerenciadora de risco |
|  |  |  |  |
| Ordem Carregamento | validaGerenciamentoRisco | Boolean | Indica se realizará a validação do gerenciamento de risco para emissão de CT-e |
| Ordem Carregamento | valoresTransportador | Object |  |
|  |  |  |  |
| Valores Transportador | tarifaTransportador | Number (15,3) | Tarifa do transportador |
| Valores Transportador | valorFrete | Number (15,3) | Valor do Frete |
| Valores Transportador | valorPedagio | Number (15,3) | Valor do Pedágio |
| Valores Transportador | valorAdiantamento | Number (15,3) | Valor do Adiantamento |
| Valores Transportador | valeCombustivel | Object |  |
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
                "placaCarreta3": "DNS4A67",
                "descStatus": "Exemplo de descrição da junção",
                "observacaoGR": "Observação de alteração de status da junção",
                "emiteCTe": true
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
            "gerenciamentoRisco": {
                "liberacaoRastreamentoExterno": "ABVC123456",
                "codigoGerenciadora": 84
            },
            "validaGerenciamentoRisco": true,
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
| 500 | Falha ao processar sua requisição |

---

## /getOperadorasCfe

**Método:** GET

**Rota:** /…/getOperadorasCfe?filialMaxys={filialMaxys}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | filialMaxys | S | Number (4) | Código da filial no Maxys |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | Operadoras |  | Operadoras cadastradas |
| Operadoras | codOperadora | Number (2) | Código da operadora |
| Operadoras | descOperadora | String (60) | Nome da operadora |
| Operadoras | urlImagem | String (400) | URL da imagem da operadora |
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
            "urlImagem": "http://pamcary.com.br/imagem",
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
| 500 | Erro de execução |

---

## /getTiposDocumento

**Método:** GET

**Rota:** /…/getTiposDocumento?empresa={empresa}&serie={serie}&lancamento={lancamento}&tipoFaturamento={tipofaturamento}&numero={numero}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | empresa | S | Number (4) | Empresa de emissão do CT-e |
| Principal | serie | S | String (5) | Código da série do CT-e |
| Principal | tipoFaturamento | S | String (1) | Tipo de faturamento do CT-e |
| Principal | lancamento | S | Number (7) | Número do lançamento do CT-e |
| Principal | numero | S | Number (10) | Número do CT-exemplo de Request |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | tipoDocumento | Number (2) | Tipo de documento |
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

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 400 | Requisição inválida |
| 500 | Erro de execução |

---

## /getDocumento

**Método:** GET

**Rota:** /…/getDocumento?empresa={empresa}&lancamento={lancamento}&serie={serie}&tipoFaturamento={tipoFaturamento]&numero={numero}&tipoDocumento={tipoDocumento}&ordemColeta={ordemColeta}&CPFUsuario={CPFUsuario}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | empresa | S | Number (4) | Código da empresa de emissão do CT-e |
| Principal | serie | S | String (5) | Código de série do CT-e |
| Principal | tipoFaturamento | N | String (1) | Tipo de faturamento de CT-e |
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
| Principal | arquivo | Arquivo PDF | Arquivo impresso de acordo com o tipo de documento |

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 404 | Nenhum documento encontrado para os dados informados |
| 500 | Erro de execução |

---

## /cancelarCTe

**Método: POST**

**Rota:** /…/cancelarCTe

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | numeroAgrupamento | N | Number (15) | Número do agrupamento de CT-es a serem cancelados |
| Principal | codigoFilial | N | Number (4) | Código da empresa do CT-e a ser cancelado |
| Principal | numeroLancamento | N | Number (7) | Número do lançamento do CT-e a ser cancelado |
| Principal | serieDocumento | N | String (5) | Série do CT-e a ser cancelado |
| Principal | tipoFaturamento | N | String (1) | Tipo de faturamento do CT-e cancelado (0 - Entrada / 1 - Saída) |
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
  "tipoFaturamento": "1",
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
| 500 | Falha ao processar sua requisição |

---

## /getMotivos

**Método:** GET

**Rota:** /…/getMotivos?codigo={codigo}&descricao={descricao}

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
| Principal | totalDocs | Number  | Número total de motivos de cancelamento |
| Principal | limit | Number  | Quantidade de registros por página |
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
    ],
    "totalDocs": 1,
    "limit": 25,
    "page": 1,
    "totalPages": 1
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 500 | Erro no processamento da requisição |

---

## /getNotaCompleta

**Método:** GET

**Rota:** /…/getNotaCompleta?numeroChaveAcesso={numeroChaveAcesso}&cliforPagador={cliforPagador}&dataInicio={dataInicio}&cliforOrigem={cliforOrigem}&cliforDestino={cliforDestino}&cliforExpedidor={cliforExpedidor}&cliforRecebedor={cliforRecebedor}&descProduto={descProduto}&numeroNCM={numeroNCM}&dataFim={dataFim}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | numeroChaveAcesso | S | String (60) | Número da chave de acesso da nota fiscal |
| Principal | cliforPagador | S | String (14) | CPF/CNPJ do clifor pagador |
| Principal | cliforOrigem | N | String (14) | CPF/CNPJ do clifor de origem |
| Principal | cliforDestino | N | String (14) | CPF/CNPJ do clifor de destino |
| Principal | cliforExpedidor | N | String (14) | CPF/CNPJ do clifor expedidor |
| Principal | cliforRecebedor | N | String (14) | CPF/CNPJ do clifor recebedor  |
| Principal | descProduto | N | String (60) | Descrição do produto |
| Principal | numeroNCM | N | String (8) | Número do NCM |
| Principal | dataInicio | S | Date | Data de inicio da nota fiscal |
| Principal | dataFim | N | Date | Data de fim da nota fiscal |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | notas | Array | Array de notas fiscais |
| notas | chaveAcesso | String (60) | Número da chave de acesso da nota fiscal |
| notas  | XML | Arquivo .XML | Arquivo XML da nota fiscal |
| Principal | totalDocs | Number | Número total de motivos de cancelamento |
| Principal | page | Number | Página atual |
| Principal | totalPages | Number | Número total de páginas |
| Principal | limit | Number | Quantidade de registros por página |

### Exemplo de Response

```json
{
    "notas": [
        {
            "chaveAcesso": "43200603640719000185570010001793651000000003",
            "XML": "<arquivoXML>"
        }
    ],
    "totalDocs": 1,
    "page": 1,
    "totalPages": 1,
    "limit": 25
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 400 | Requisição inválida |
| 500 | Falha ao processar sua requisição |

---

## /cancelamentoCTe/consultar

**Método:** GET

**Rota:** /…/cancelamentoCTe/consultar?numeroAgrupamento={numeroAgrupamento}&codigoFilial={codigoFilial}&numeroLancamento={numeroLancamento}&serieDocumento={serieDocumento}&tipoFaturamento{tipoFaturamento}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | numeroAgrupamento | N | Number (15) | Número de agrupamento para CT-e com Carta Frete única |
| Principal | codigoFilial | S | Number (4) | Código da Filial do CT-e |
| Principal | numeroLancamento | S | Number (7) | Número de Lançamento do CT-e |
| Principal | serieDocumento | S | String (5) | Série do CT-e |
| Principal | tipoFaturamento | S | String (1) | Tipo de Faturamento do CT-e |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | documentos | Array | Array de documentos |
|  |  |  |  |
| Documentos | cancelamento | Object | Objeto de cancelamentos |
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
|  |  |  |  |
| Principal | totalDocs | Number | Número total de CT-e cancelados |
| Principal | limit | Number | Quantidade de registros por página |
| Principal | page | Number | Página atual |
| Principal | totalPages | Number | Número total de páginas |

### Exemplo de Response

```json
{
    "documentos": [
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
    ],
    "totalPages": 1,
    "page": 1,
    "limit": 25,
    "totalDocs": 1
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 500 | Falha ao processar sua requisição. Verifique a mensagem. |
| 404 | Não foi encontrado nenhum CT-e com os dados informados. |

---

## /getOperadorasVPE

**Método: GET**

**Rota:** /…/getOperadorasVPE?filialMaxys={filialMaxys}&pagamentoPegadioAntecipado={pagamentoPegadioAntecipado}

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
| Principal | pagamentoPedagioAntecipado | S | Boolean | Status se possui pagamento de pedágio antecipado |
| Principal | filialMaxys | S | Number (4) | Código da filial no Maxys |

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
| Principal | tipoPagamentoPegadio | Array | Tipo de pagamento do pedágio |
| tipoPagamentoPegadio | codPagamento | Number (2) | Código do tipo de pagamento |
| tipoPagamentoPegadio | descPagamento | String (60) | Descrição do tipo de pagamento |
| tipoPagamentoPegadio | obrigaNrCartao | Boolean | Indica se é obrigatório o número do cartão |
| tipoPagamentoPegadio | urlImagem | String (400) | URL da imagem da operadora |

### Exemplo de Response

```json
{
    "tipoPagamentoPedagio": [
        {
            "codPagamento": 7,
            "descPagamento": "Tag - Target Via Facil",
            "obrigaNrCartao": false,
            "urlImagem": ""
        }
    ]
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Não foi possível processar a transação |
| 500 | Falha ao processar sua requisição |

---

## /postOrdemColeta

**Método: POST**

**Rota:** /…/postOrdemColeta

### Relação de campos - Reques

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
| Principal | linkGetDocumento | String (200) | Link do documento  |

### Exemplo de Response

```json
{
    "tipoPagamentoPedagio": [
        {
            "codPagamento": 7,
            "descPagamento": "Tag - Target Via Facil",
            "obrigaNrCartao": false,
            "urlImagem": ""
        }
    ]
}
```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
| 422 | Não foi possível processar a transação |
| 500 | Falha ao processar sua requisição |

---

## /getConjunto

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

## /postConjunto

**Método: POST**

**Rota:** /…/postConjunto

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |
|  |  |  |  |  |

### Códigos de status

| Código | Descrição |
| --- | --- |
|  |  |
|  |  |

### Exemplo de Request

```json

```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |

### Exemplo de Response

```json

```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
|  |  |
|  |  |

---

# EXEMPLO

## /getListaOrdemColeta

**Método:** GET

**Rota:** /…

### Relação de campos - Request

| Nível | Campo | Obrigatório | Tipo de dado | Descrição |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |
|  |  |  |  |  |

### Códigos de status

| Código | Descrição |
| --- | --- |
|  |  |
|  |  |

### Exemplo de Request

```json

```

### Relação de campos - Response

| Nível | Campo | Tipo de dado | Descrição |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |

### Exemplo de Response

```json

```

### Possíveis códigos de erro

| Código | Descrição |
| --- | --- |
|  |  |
|  |  |