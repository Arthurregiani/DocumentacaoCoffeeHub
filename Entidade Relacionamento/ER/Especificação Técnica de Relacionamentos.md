# Especificação Técnica de Relacionamentos
## Sistema Integrado de Rastreabilidade e Gestão para Cafeicultura

Esta especificação técnica documenta todos os relacionamentos entre as entidades do modelo ER, organizados por módulos funcionais e com detalhes sobre cardinalidade, obrigatoriedade e descrição funcional.

## Índice
1. [Cadastro e Estrutura](#1-cadastro-e-estrutura)
2. [Ciclo e Monitoramento](#2-ciclo-e-monitoramento)
3. [Recursos](#3-recursos)
4. [Insumos e Aplicações](#4-insumos-e-aplicações)
5. [Produção e Processamento](#5-produção-e-processamento)
6. [Qualidade e Comercialização](#6-qualidade-e-comercialização)
7. [Controle e Certificações](#7-controle-e-certificações)
8. [Financeiro e RH](#8-financeiro-e-rh)
9. [Relacionamentos entre Módulos](#9-relacionamentos-entre-módulos)

## Legenda de Cardinalidade
- **1:1** - Um para um
- **1:N** - Um para muitos
- **N:1** - Muitos para um
- **N:M** - Muitos para muitos

## 1. Cadastro e Estrutura

| Entidade Origem | Cardinalidade | Entidade Destino | Obrigatoriedade | Descrição Funcional |
|-----------------|---------------|------------------|-----------------|---------------------|
| Produtor | 1:N | Propriedade | Obrigatório | Um produtor pode possuir várias propriedades. Cada propriedade deve pertencer a um produtor. |
| Produtor | 1:0..1 | Conjuge | Opcional | Um produtor pode ter um cônjuge registrado. |
| Propriedade | 1:N | Talhao | Obrigatório | Uma propriedade é subdividida em vários talhões. Cada talhão deve pertencer a uma propriedade. |
| Propriedade | 1:N | AreaPreservacao | Obrigatório | Uma propriedade pode ter várias áreas de preservação. Cada área de preservação deve estar vinculada a uma propriedade. |
| Propriedade | 1:0..1 | CAR | Obrigatório | Uma propriedade deve ter um registro CAR. Um registro CAR pertence a uma propriedade específica. |
| Talhao | 1:N | HistoricoTalhao | Obrigatório | Um talhão pode ter vários registros históricos de alterações. Cada registro histórico pertence a um talhão específico. |
| Talhao | N:1 | VariedadeCafe | Opcional | Um talhão pode ser plantado com uma variedade de café. Uma variedade pode ser plantada em vários talhões. |
| Talhao | 1:N | ProducaoTalhao | Obrigatório | Um talhão pode ter vários registros de produção (por safra). Cada registro de produção pertence a um talhão específico. |
| CAR | 1:N | AreaPreservacao | Opcional | Um registro CAR pode estar relacionado a várias áreas de preservação. Uma área de preservação pode estar vinculada a um registro CAR. |

## 2. Ciclo e Monitoramento

| Entidade Origem | Cardinalidade | Entidade Destino | Obrigatoriedade | Descrição Funcional |
|-----------------|---------------|------------------|-----------------|---------------------|
| Talhao | 1:N | CicloFenologico | Obrigatório | Um talhão pode ter vários ciclos fenológicos registrados. Cada ciclo fenológico pertence a um talhão específico. |
| Talhao | 1:N | Monitoramento | Obrigatório | Um talhão pode ter vários monitoramentos. Cada monitoramento está associado a um talhão específico. |
| Talhao | 1:N | Irrigacao | Obrigatório | Um talhão pode receber várias irrigações. Cada irrigação é aplicada a um talhão específico. |
| Talhao | 1:N | Manejo | Obrigatório | Um talhão pode receber vários manejos. Cada manejo é aplicado a um talhão específico. |
| Talhao | N:M | Clima | Opcional | Um talhão pode ter vários registros climáticos. Um registro climático pode estar associado a um talhão específico ou à propriedade como um todo. |
| Propriedade | N:M | Clima | Opcional | Uma propriedade pode ter vários registros climáticos. Um registro climático pode estar associado a uma propriedade como um todo. |

## 3. Recursos

| Entidade Origem | Cardinalidade | Entidade Destino | Obrigatoriedade | Descrição Funcional |
|-----------------|---------------|------------------|-----------------|---------------------|
| Funcionario | 1:N | EquipeMaoObra | Obrigatório | Um funcionário pode liderar várias equipes de mão de obra. Cada equipe deve ter um líder. |
| EquipeMaoObra | 1:N | MembroEquipe | Obrigatório | Uma equipe é composta por vários membros. Cada registro de membro pertence a uma equipe específica. |
| Funcionario | 1:N | MembroEquipe | Obrigatório | Um funcionário pode participar de várias equipes como membro. Cada registro de membro está associado a um funcionário específico. |

## 4. Insumos e Aplicações

| Entidade Origem | Cardinalidade | Entidade Destino | Obrigatoriedade | Descrição Funcional |
|-----------------|---------------|------------------|-----------------|---------------------|
| Insumo | 1:1 | Fertilizante | Especialização | Um insumo pode ser especializado como fertilizante. Relação de herança/especialização. |
| Insumo | 1:1 | Agroquimico | Especialização | Um insumo pode ser especializado como agroquímico. Relação de herança/especialização. |
| Insumo | 1:N | EstoqueInsumo | Obrigatório | Um insumo pode ter vários registros de estoque. Cada registro de estoque está associado a um insumo específico. |
| Insumo | 1:N | Aplicacao | Obrigatório | Um insumo pode ter várias aplicações. Cada aplicação utiliza um insumo específico. |
| Talhao | N:M | Aplicacao | Opcional | Um talhão pode receber várias aplicações. Uma aplicação pode ser realizada em um talhão específico. |
| Propriedade | N:M | Aplicacao | Opcional | Uma propriedade pode receber várias aplicações (quando não específicas a um talhão). Uma aplicação pode ser realizada em uma propriedade como um todo. |
| Propriedade | N:M | EstoqueInsumo | Opcional | Uma propriedade pode ter vários registros de estoque. Um registro de estoque pode estar associado a uma propriedade específica. |

## 5. Produção e Processamento

| Entidade Origem | Cardinalidade | Entidade Destino | Obrigatoriedade | Descrição Funcional |
|-----------------|---------------|------------------|-----------------|---------------------|
| Talhao | 1:N | Colheita | Obrigatório | Um talhão pode ter várias colheitas. Cada colheita é realizada em um talhão específico. |
| Colheita | 1:N | Lote | Obrigatório | Uma colheita pode gerar vários lotes. Cada lote é gerado a partir de uma colheita específica. |
| Lote | 1:N | RecebimentoMoega | Obrigatório | Um lote pode ter vários recebimentos na moega. Cada recebimento está associado a um lote específico. |
| Lote | 1:N | ProcessamentoCafe | Obrigatório | Um lote pode passar por vários processamentos. Cada processamento está associado a um lote específico. |
| ProcessamentoCafe | 1:N | EtapaPreparoCafe | Obrigatório | Um processamento pode ter várias etapas de preparo. Cada etapa de preparo pertence a um processamento específico. |
| ProcessamentoCafe | 1:N | EtapaSecagem | Obrigatório | Um processamento pode ter várias etapas de secagem. Cada etapa de secagem pertence a um processamento específico. |
| ProcessamentoCafe | 1:N | EtapaBeneficiamento | Obrigatório | Um processamento pode ter várias etapas de beneficiamento. Cada etapa de beneficiamento pertence a um processamento específico. |
| Lote | N:M | Armazenamento | Opcional | Um lote pode ter vários registros de armazenamento. Um armazenamento está associado a um lote específico. |
| Lote | 1:N | LoteComposicao (como origem) | Obrigatório | Um lote pode ser origem de várias composições. Cada composição tem um lote de origem específico. |
| Lote | 1:N | LoteComposicao (como destino) | Obrigatório | Um lote pode ser destino de várias composições. Cada composição tem um lote de destino específico. |

## 6. Qualidade e Comercialização

| Entidade Origem | Cardinalidade | Entidade Destino | Obrigatoriedade | Descrição Funcional |
|-----------------|---------------|------------------|-----------------|---------------------|
| Lote | 1:N | ClassificacaoCafe | Obrigatório | Um lote pode ter várias classificações. Cada classificação está associada a um lote específico. |
| Lote | 1:N | PerfilSensorial | Obrigatório | Um lote pode ter vários perfis sensoriais. Cada perfil sensorial está associado a um lote específico. |
| Lote | 1:N | MovimentacaoLote | Obrigatório | Um lote pode ter várias movimentações. Cada movimentação está associada a um lote específico. |
| Lote | 1:N | Comercializacao | Obrigatório | Um lote pode ter várias comercializações. Cada comercialização está associada a um lote específico. |

## 7. Controle e Certificações

| Entidade Origem | Cardinalidade | Entidade Destino | Obrigatoriedade | Descrição Funcional |
|-----------------|---------------|------------------|-----------------|---------------------|
| Produtor | 1:N | Certificacao | Obrigatório | Um produtor pode ter várias certificações. Cada certificação está associada a um produtor específico. |
| Propriedade | N:M | Certificacao | Opcional | Uma propriedade pode ter várias certificações. Uma certificação pode estar associada a uma propriedade específica. |
| Produtor | 1:N | EntregaEmbalagens | Obrigatório | Um produtor pode ter vários registros de entrega de embalagens. Cada entrega está associada a um produtor específico. |
| Lote | N:M | RastreabilidadeQR | Opcional | Um lote pode ter vários códigos QR de rastreabilidade. Um código QR pode estar associado a um lote específico. |
| Talhao | N:M | RastreabilidadeQR | Opcional | Um talhão pode ter vários códigos QR de rastreabilidade. Um código QR pode estar associado a um talhão específico. |
| Propriedade | N:M | RastreabilidadeQR | Opcional | Uma propriedade pode ter vários códigos QR de rastreabilidade. Um código QR pode estar associado a uma propriedade específica. |

## 8. Financeiro e RH

| Entidade Origem | Cardinalidade | Entidade Destino | Obrigatoriedade | Descrição Funcional |
|-----------------|---------------|------------------|-----------------|---------------------|
| Produtor | 1:N | Funcionario | Obrigatório | Um produtor pode empregar vários funcionários. Cada funcionário está associado a um produtor específico. |
| Produtor | 1:N | Capacitacao | Obrigatório | Um produtor pode participar de várias capacitações. Cada capacitação está associada a um produtor específico. |
| Funcionario | N:M | Capacitacao | Opcional | Um funcionário pode receber várias capacitações. Uma capacitação pode ser fornecida a vários funcionários. |
| IndicadorDesempenho | 1:N | MedicaoIndicador | Obrigatório | Um indicador pode ter várias medições. Cada medição está associada a um indicador específico. |
| Propriedade | N:M | MedicaoIndicador | Opcional | Uma propriedade pode ter várias medições de indicadores. Uma medição pode estar associada a uma propriedade específica. |
| Talhao | N:M | MedicaoIndicador | Opcional | Um talhão pode ter várias medições de indicadores. Uma medição pode estar associada a um talhão específico. |

## 9. Relacionamentos entre Módulos

| Entidade Origem | Cardinalidade | Entidade Destino | Obrigatoriedade | Descrição Funcional |
|-----------------|---------------|------------------|-----------------|---------------------|
| Funcionario | N:M | Monitoramento | Opcional | Um funcionário pode executar vários monitoramentos. Um monitoramento pode ser executado por um funcionário específico. |
| Funcionario | N:M | Irrigacao | Opcional | Um funcionário pode executar várias irrigações. Uma irrigação pode ser executada por um funcionário específico. |
| Funcionario | N:M | Manejo | Opcional | Um funcionário pode executar vários manejos. Um manejo pode ser executado por um funcionário específico. |
| Funcionario | N:M | Aplicacao | Opcional | Um funcionário pode executar várias aplicações. Uma aplicação pode ser executada por um funcionário específico. |
| Funcionario | N:M | RecebimentoMoega | Opcional | Um funcionário pode operar vários recebimentos na moega. Um recebimento pode ser operado por um funcionário específico. |
| Funcionario | N:M | ProcessamentoCafe | Opcional | Um funcionário pode ser responsável por vários processamentos. Um processamento pode ter um funcionário responsável específico. |
| Funcionario | N:M | ClassificacaoCafe | Obrigatório | Um funcionário pode classificar vários lotes. Uma classificação deve ser realizada por um funcionário específico (classificador). |
| Funcionario | N:M | PerfilSensorial | Obrigatório | Um funcionário pode degustar vários lotes. Uma análise sensorial deve ser realizada por um funcionário específico (degustador). |
| Equipamento | N:M | Irrigacao | Opcional | Um equipamento pode ser utilizado em várias irrigações. Uma irrigação pode utilizar um equipamento específico. |
| Equipamento | N:M | Manejo | Opcional | Um equipamento pode ser utilizado em vários manejos. Um manejo pode utilizar um equipamento específico. |
| Equipamento | N:M | Aplicacao | Opcional | Um equipamento pode ser utilizado em várias aplicações. Uma aplicação pode utilizar um equipamento específico. |
| Equipamento | N:M | Colheita | Opcional | Um equipamento pode ser utilizado em várias colheitas. Uma colheita pode utilizar um equipamento específico. |
| Equipamento | N:M | RecebimentoMoega | Opcional | Um equipamento pode ser utilizado em vários recebimentos na moega. Um recebimento pode utilizar um equipamento específico. |
| EquipeMaoObra | N:M | Colheita | Opcional | Uma equipe pode realizar várias colheitas. Uma colheita pode ser realizada por uma equipe específica. |
| EquipeMaoObra | N:M | Aplicacao | Opcional | Uma equipe pode realizar várias aplicações. Uma aplicação pode ser realizada por uma equipe específica. |
| Operacao | 1:N | Colheita | Opcional | Uma operação financeira pode financiar várias colheitas. Uma colheita pode estar associada a uma operação financeira específica. |
| Operacao | 1:N | Aplicacao | Opcional | Uma operação financeira pode financiar várias aplicações. Uma aplicação pode estar associada a uma operação financeira específica. |
| Operacao | 1:N | ProcessamentoCafe | Opcional | Uma operação financeira pode financiar vários processamentos. Um processamento pode estar associado a uma operação financeira específica. |
| Operacao | 1:N | ClassificacaoCafe | Opcional | Uma operação financeira pode financiar várias classificações. Uma classificação pode estar associada a uma operação financeira específica. |
| Operacao | 1:N | PerfilSensorial | Opcional | Uma operação financeira pode financiar várias análises sensoriais. Uma análise sensorial pode estar associada a uma operação financeira específica. |
| Operacao | 1:N | Capacitacao | Opcional | Uma operação financeira pode financiar várias capacitações. Uma capacitação pode estar associada a uma operação financeira específica. |
| Operacao | 1:N | Comercializacao | Opcional | Uma operação financeira pode registrar várias comercializações. Uma comercialização pode estar associada a uma operação financeira específica. |
| Operacao | 1:N | MovimentacaoLote | Opcional | Uma operação financeira pode financiar várias movimentações de lote. Uma movimentação pode estar associada a uma operação financeira específica. |
| Operacao | 1:N | Monitoramento | Opcional | Uma operação financeira pode financiar vários monitoramentos. Um monitoramento pode estar associada a uma operação financeira específica. |
| Operacao | 1:N | Irrigacao | Opcional | Uma operação financeira pode financiar várias irrigações. Uma irrigação pode estar associada a uma operação financeira específica. |
| Operacao | 1:N | Manejo | Opcional | Uma operação financeira pode financiar vários manejos. Um manejo pode estar associado a uma operação financeira específica. |
| Operacao | 1:N | Armazenamento | Opcional | Uma operação financeira pode financiar vários armazenamentos. Um armazenamento pode estar associado a uma operação financeira específica. |
| Colheita | 1:N | EventoRastreabilidade | Opcional | Uma colheita pode gerar vários eventos de rastreabilidade. Um evento pode estar associado a uma colheita específica. |
| Aplicacao | 1:N | EventoRastreabilidade | Opcional | Uma aplicação pode gerar vários eventos de rastreabilidade. Um evento pode estar associado a uma aplicação específica. |
| ProcessamentoCafe | 1:N | EventoRastreabilidade | Opcional | Um processamento pode gerar vários eventos de rastreabilidade. Um evento pode estar associado a um processamento específico. |
| MovimentacaoLote | 1:N | EventoRastreabilidade | Opcional | Uma movimentação pode gerar vários eventos de rastreabilidade. Um evento pode estar associado a uma movimentação específica. |
| Comercializacao | 1:N | EventoRastreabilidade | Opcional | Uma comercialização pode gerar vários eventos de rastreabilidade. Um evento pode estar associado a uma comercialização específica. |

## Notas Adicionais

1. **Relacionamentos Obrigatórios vs. Opcionais**:
   - Relacionamentos marcados como "Obrigatório" indicam que a entidade destino deve estar associada à entidade origem.
   - Relacionamentos marcados como "Opcional" indicam que a associação é permitida mas não obrigatória.

2. **Chaves Estrangeiras**:
   - Todas as relações são implementadas através de chaves estrangeiras (FK) nas tabelas correspondentes.
   - Em relacionamentos N:M, existem tabelas de junção implícitas que não foram detalhadas nesta especificação.

3. **Rastreabilidade**:
   - O sistema de rastreabilidade é implementado através de códigos de rastreio padronizados em várias entidades.
   - A entidade EventoRastreabilidade centraliza os eventos de rastreabilidade para facilitar consultas.
   - A entidade RastreabilidadeQR permite acesso externo às informações de rastreabilidade via códigos QR.

4. **Herança/Especialização**:
   - As entidades Fertilizante e Agroquimico são especializações da entidade Insumo, implementadas como tabelas separadas com chave primária que também é chave estrangeira para Insumo.
