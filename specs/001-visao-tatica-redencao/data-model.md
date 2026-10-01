# Modelo de Dados: Visão Tática Redenção

**Data**: 2026-10-01

Os dados abaixo são entidades de simulação em memória. Não existe persistência nem fonte real de
inteligência.

## Credencial de Acesso

Representa os dados preenchidos pelo agente na tela inicial.

| Campo              | Tipo conceitual | Obrigatório | Regra                 |
| ------------------ | --------------- | ----------: | --------------------- |
| credencialAgente   | texto           |         Sim | Não pode estar vazio. |
| chaveGovernamental | texto           |         Sim | Não pode estar vazia. |

**Transição**: `não preenchida` -> `preenchida` -> `validada` ou `rejeitada`.

A validação é demonstrativa e front-end. A entidade não representa uma credencial governamental
real e não deve ser persistida.

## Sessão de Agente

Representa o estado temporário que autoriza a visão tática.

| Campo      | Tipo conceitual | Regra                                                                |
| ---------- | --------------- | -------------------------------------------------------------------- |
| autorizada | booleano        | Só fica verdadeira após os dois campos obrigatórios serem validados. |
| destino    | texto           | Deve apontar para `dashboard.html` quando autorizada.                |

**Transição**: `não autorizada` -> `autorizada` -> `encerrada`.

Enquanto a sessão estiver `não autorizada` ou `encerrada`, os dados operacionais não devem ser
apresentados.

## Alvo Investigativo

Representa um dispositivo, servidor ou indivíduo simulado no mapa.

| Campo     | Tipo conceitual | Obrigatório | Regra                                         |
| --------- | --------------- | ----------: | --------------------------------------------- |
| id        | identificador   |         Sim | Único dentro da coleção do mock.              |
| tipo      | enumeração      |         Sim | `dispositivo`, `servidor` ou `individuo`.     |
| latitude  | número          |         Sim | Coordenada geográfica válida.                 |
| longitude | número          |         Sim | Coordenada geográfica válida.                 |
| ip        | texto           |         Sim | Exibido no popup como dado sigiloso simulado. |
| status    | texto           |         Sim | Exemplo: `Interceptado`.                      |
| infracao  | texto           |         Sim | Exemplo: `Vazamento de Dados`.                |
| descricao | texto           |         Não | Contexto adicional da ocorrência.             |

**Relação**: uma sessão autorizada pode consultar vários alvos; um popup aberto referencia um
único alvo por vez.

## Evento de Inteligência

Representa uma linha do terminal lateral.

| Campo        | Tipo conceitual       | Obrigatório | Regra                                                         |
| ------------ | --------------------- | ----------: | ------------------------------------------------------------- |
| tipo         | enumeração            |         Sim | `ALPR`, `Rastreamento IP` ou `Reconhecimento Facial`.         |
| horario      | horário formatado     |         Sim | Obtido no momento da inserção.                                |
| mensagem     | texto/HTML controlado |         Sim | Deve estar em Português do Brasil.                            |
| classeVisual | enumeração            |         Sim | Verde para ALPR OK; vermelho para Match Facial e IP Suspeito. |
| severidade   | enumeração            |         Sim | `informativo` ou `alerta`.                                    |

### Categorias de evento

- **ALPR**: placa, avenida principal e indicação de roubo ou pendência legal.
- **Rastreamento IP**: dispositivo móvel, rede pública e indicação de tráfego suspeito.
- **Reconhecimento Facial**: câmera do "Olho Vivo", correspondência e mandado de prisão em
  aberto.

**Transição**: `disponível no array` -> `selecionado` -> `exibido` -> `visível no fim do terminal`.

## Configuração da Visão Espacial

Representa os valores fixos necessários para o estado inicial do mapa.

| Campo           | Valor                                  |
| --------------- | -------------------------------------- |
| centroLatitude  | `-14.2263`                             |
| centroLongitude | `-42.7816`                             |
| pitch           | `60` graus                             |
| bearing         | `-17.6` graus                          |
| zoom            | `15.5`                                 |
| estilo          | noturno e de alto contraste            |
| camadaUrbana    | `3d-buildings` com extrusão de prédios |

O token de acesso é uma configuração manual externa ao modelo de dados, representada apenas pelo
placeholder `COLOQUE_SEU_TOKEN_MAPBOX_AQUI`.

## Dossiê de Vazamento

Representa o card OSINT de um alvo gerado durante a operação simulada.

| Campo         | Tipo conceitual | Regra                                                         |
| ------------- | --------------- | ------------------------------------------------------------- |
| id            | identificador   | Único por ocorrência gerada.                                  |
| nome          | texto           | Selecionado de uma lista de nomes fictícios.                  |
| fotoUrl       | URL             | Aponta para um retrato masculino do RandomUser.               |
| ip            | texto           | Endereço fictício exibido como IP rastreado.                  |
| status        | texto fixo      | Deve ser `MANDADO ATIVO`.                                     |
| infracao      | texto           | Deve descrever uma infração simulada à LGPD.                  |
| coordenadas   | par numérico    | Deve estar no raio máximo de 2 km do centro de Guanambi.      |
| visaoLocalUrl | URL             | Google Maps Embed com a coordenada exata e visão de satélite. |

**Transição**: `não gerado` -> `marcador exibido` -> `dossiê aberto` -> `dossiê fechado`.

## Rota de Patrulha ALPR

Representa uma rota GeoJSON `Feature<LineString>` usada exclusivamente pela simulação.

| Campo         | Tipo conceitual    | Regra                                                 |
| ------------- | ------------------ | ----------------------------------------------------- |
| identificador | texto              | Identifica `R-01`, `R-02` ou `R-03`.                  |
| geometria     | GeoJSON LineString | Contém coordenadas ordenadas de uma avenida simulada. |
| duracao       | número             | Duração do ciclo em milissegundos.                    |
| distanciaKm   | número             | Calculada por Turf.js com `turf.length()`.            |

## Veículo ALPR Móvel

Representa o ponto azul que percorre uma Rota de Patrulha ALPR.

| Campo         | Tipo conceitual       | Regra                                       |
| ------------- | --------------------- | ------------------------------------------- |
| rota          | Rota de Patrulha ALPR | Obrigatória.                                |
| pontoAtual    | GeoJSON Point         | Calculado por Turf.js com `turf.along()`.   |
| cicloAnterior | número                | Evita duplicar o log de conclusão da rota.  |
| identificador | texto                 | Deve corresponder ao identificador da rota. |

**Transição**: `posicionado` -> `em movimento` -> `rota concluída` -> `em movimento`.

Ao concluir um ciclo, o veículo produz um Evento de Inteligência de leitura ALPR bem-sucedida.
