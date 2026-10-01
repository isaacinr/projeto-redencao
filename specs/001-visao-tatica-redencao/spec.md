# Especificação de Funcionalidade: Visão Tática Redenção

**Ramo da funcionalidade**: `001-visao-tatica-redencao`

**Criado em**: 2026-10-01

**Status**: Rascunho

**Entrada**: Descrição do usuário: criar as funcionalidades do sistema do Projeto Redenção, incluindo acesso restrito, visão espacial 3D God's Eye e terminal lateral de inteligência IoT.

## Cenários de Usuário e Testes

### História de Usuário 1 - Validar acesso de agente ou perito (Prioridade: P1)

Como agente ou perito autorizado, quero informar minha credencial profissional e minha chave de acesso governamental em uma tela inicial de terminal, para entrar na visão tática restrita do Projeto Redenção.

**Por que esta prioridade**: Sem a validação inicial, nenhuma informação operacional deve ser apresentada. Esta é a barreira de acesso que protege a experiência e estabelece o contexto de força-tarefa restrita.

**Teste independente**: Abrir a tela inicial, verificar os dois campos obrigatórios, informar credenciais de simulação e confirmar que o painel tático é exibido. A jornada é válida mesmo sem os módulos de mapa e terminal concluídos.

**Cenários de aceitação**:

1. **Dado** que o visitante abriu o sistema, **quando** a tela inicial for carregada, **então** serão exibidos os campos "Credencial de Agente/Perito" e "Chave de Acesso Governamental".
2. **Dado** que a tela inicial está disponível, **quando** o visitante a examinar, **então** não existirão ações de "Esqueci minha senha" nem "Cadastrar".
3. **Dado** que os dois campos foram preenchidos com valores de simulação, **quando** o visitante confirmar o acesso, **então** o sistema exibirá o painel de monitoramento em `dashboard.html`.
4. **Dado** que um dos campos obrigatórios está vazio, **quando** o visitante tentar confirmar o acesso, **então** o sistema exibirá um alerta em Português do Brasil e permanecerá na tela inicial.
5. **Dado** que o painel ainda não foi autorizado, **quando** o visitante tentar acessar diretamente a visão tática, **então** o sistema bloqueará a apresentação dos dados operacionais e orientará o retorno à validação inicial.

---

### História de Usuário 2 - Observar a cidade pela visão God's Eye (Prioridade: P1)

Como agente autenticado, quero visualizar uma representação espacial 3D de Guanambi, Bahia, para compreender a distribuição territorial dos alvos e acompanhar a cidade sob uma perspectiva de vigilância ativa.

**Por que esta prioridade**: A visão espacial é o núcleo operacional do painel. Ela transforma eventos dispersos em uma leitura territorial que sustenta a investigação.

**Teste independente**: Após o acesso autorizado, confirmar que a cidade aparece em uma área de mapa que ocupa toda a viewport, com perspectiva inclinada, prédios volumétricos, estilo noturno e centro geográfico correto.

**Cenários de aceitação**:

1. **Dado** que o agente concluiu a validação, **quando** o painel for carregado, **então** o mapa ocupará toda a área disponível do navegador sem barras de rolagem globais.
2. **Dado** que a visão espacial foi carregada, **quando** o agente observar a posição inicial, **então** o centro será Guanambi, Bahia, nas coordenadas latitude `-14.2263` e longitude `-42.7816`.
3. **Dado** que a visão espacial foi carregada, **quando** o agente observar a perspectiva inicial, **então** ela será inclinada ou isométrica, semelhante à visão de um drone ou satélite militar.
4. **Dado** que a cidade está sendo exibida, **quando** o agente observar a área urbana, **então** prédios terão volumetria e altura perceptíveis em três dimensões.
5. **Dado** que a visão espacial está pronta, **quando** o agente interagir com ela, **então** poderá deslocar, aproximar e afastar a visão sem perder o contexto territorial.
6. **Dado** que o painel foi carregado, **quando** o agente observar a aparência geral, **então** o estilo será noturno, de alto contraste e coerente com uma operação governamental de vigilância ativa.

---

### História de Usuário 3 - Investigar alvos geolocalizados (Prioridade: P1)

Como agente autenticado, quero identificar alvos plotados em vermelho e consultar seus dados sigilosos, para relacionar localização, dispositivo, pessoa ou servidor a uma investigação de violação da LGPD.

**Por que esta prioridade**: A localização dos alvos e a consulta de evidências são a ponte entre a visão territorial e a responsabilização prevista no conceito de Redenção.

**Teste independente**: Localizar um marcador vermelho, selecioná-lo e verificar se o popup exibe dados sigilosos coerentes com uma investigação.

**Cenários de aceitação**:

1. **Dado** que existem ocorrências simuladas, **quando** o mapa for carregado, **então** serão exibidos marcadores geolocalizados em vermelho para dispositivos, servidores ou indivíduos sob investigação por violação da LGPD.
2. **Dado** que um marcador vermelho está visível, **quando** o agente clicar nele, **então** será aberto um popup associado exclusivamente àquele alvo.
3. **Dado** que o popup de um alvo foi aberto, **quando** o agente consultar seu conteúdo, **então** verá, no mínimo, um IP, um status investigativo e uma infração, como `IP: 192.168.0.1`, `Status: Interceptado` e `Infração: Vazamento de Dados`.
4. **Dado** que o agente fechou o popup, **quando** selecionar outro marcador, **então** os dados exibidos serão atualizados para o novo alvo e não permanecerão vinculados ao alvo anterior.
5. **Dado** que não há marcador selecionado, **quando** o agente observar o mapa, **então** nenhuma informação sigilosa ficará aberta sobre a superfície da visão espacial.

---

### História de Usuário 4 - Acompanhar inteligência IoT em tempo real (Prioridade: P1)

Como agente autenticado, quero acompanhar um terminal lateral com eventos da cidade inteligente, para correlacionar leituras de placas, rastreamento IP e reconhecimento facial durante a vigilância ativa.

**Por que esta prioridade**: O terminal fornece a dimensão temporal da operação e complementa a dimensão espacial do mapa com uma sequência contínua de inteligência operacional.

**Teste independente**: Observar o painel lateral por tempo suficiente para receber novas linhas, confirmar os três tipos de evento e verificar que o evento mais recente fica visível na parte inferior.

**Cenários de aceitação**:

1. **Dado** que o agente autenticado está no painel, **quando** o terminal lateral for exibido, **então** ele estará sobreposto ao mapa e posicionado à direita.
2. **Dado** que o terminal está ativo, **quando** transcorrerem alguns segundos, **então** uma nova linha de log será adicionada automaticamente sem recarregar a página.
3. **Dado** que o terminal registrar um evento ALPR, **quando** o agente ler a linha, **então** ela indicará a placa observada, a avenida principal e se há restrição de roubo ou pendência legal.
4. **Dado** que o terminal registrar um evento de rastreamento IP, **quando** o agente ler a linha, **então** ela indicará um dispositivo móvel conectado a uma rede pública e sinalizará tráfego suspeito.
5. **Dado** que o terminal registrar um reconhecimento facial, **quando** houver correspondência com indivíduo procurado, **então** a linha será um alerta vermelho e indicará que câmeras do "Olho Vivo" detectaram alguém com mandado de prisão em aberto.
6. **Dado** que novas linhas foram inseridas, **quando** o conteúdo ultrapassar a área visível, **então** o terminal realizará rolagem automática e manterá o evento mais recente visível na parte inferior.
7. **Dado** que um evento é exibido no terminal, **quando** o agente interpretar sua mensagem, **então** o texto estará em Português do Brasil e comunicará Vigilância Ativa ou inteligência federal.

---

### História de Usuário 5 - Acompanhar patrulha espacial ALPR (Prioridade: P1)

Como agente autenticado, quero acompanhar veículos simulados percorrendo rotas GeoJSON sobre as
avenidas da cidade, para correlacionar movimento, leitura de placas e atividade de vigilância.

**Por que esta prioridade**: O deslocamento contínuo dá dimensão operacional ao mapa e conecta a
inteligência ALPR aos vetores espaciais da visão God's Eye.

**Teste independente**: Abrir o painel com uma sessão autorizada, observar três pontos azuis em
movimento sobre as rotas e aguardar a conclusão de uma rota para confirmar o log de leitura ALPR.

**Cenários de aceitação**:

1. **Dado** que o painel autorizado foi carregado, **quando** o mapa estiver pronto, **então** três
   veículos simulados serão exibidos como pontos azuis brilhantes.
2. **Dado** que os veículos estão em patrulha, **quando** o agente observar o mapa, **então** eles
   seguirão rotas GeoJSON predefinidas sobre linhas de avenidas sem saltar para fora da rota.
3. **Dado** que um veículo completou uma rota, **quando** o ciclo reiniciar, **então** o terminal
   exibirá uma leitura de placa ALPR bem-sucedida identificando o veículo.
4. **Dado** que a aba do navegador esteja em segundo plano, **quando** a animação visual for
   suspensa pelo navegador, **então** a simulação manterá a atualização temporal dos veículos e
   dos ciclos de rota.

---

### Casos-limite

- Quando a credencial ou a chave estiver ausente, o acesso deve ser recusado sem revelar o painel.
- Quando o mapa não conseguir carregar, o painel deve apresentar uma mensagem de falha em Português do Brasil, sem fingir que a visão espacial está operacional.
- Quando não houver ocorrências simuladas disponíveis, o mapa deve continuar navegável e informar que não há alvos ativos, sem exibir dados sigilosos vazios.
- Quando um alvo estiver fora do enquadramento atual, seus dados não devem aparecer até que o agente navegue até seu marcador.
- Quando o agente clicar em uma área sem marcador, nenhum popup deve ser aberto.
- Quando o terminal receber vários eventos em sequência, as linhas não devem se sobrepor nem ocultar o evento mais recente.
- Quando o terminal ainda não tiver recebido eventos, deve exibir um estado inicial informativo em vez de uma área vazia ambígua.
- Quando o navegador tiver viewport estreita, o mapa, o terminal, os textos e os controles devem permanecer legíveis sem criar rolagem global.
- Quando o agente retornar à tela inicial após sair do painel, a visão tática não deve permanecer disponível sem nova validação.

## Requisitos

### Requisitos Funcionais

- **RF-001**: O sistema MUST apresentar uma tela inicial de terminal com os campos "Credencial de Agente/Perito" e "Chave de Acesso Governamental".
- **RF-002**: O sistema MUST ocultar as ações "Esqueci minha senha" e "Cadastrar" da tela de acesso restrito.
- **RF-003**: O sistema MUST simular a validação front-end da credencial e da chave, sem depender de um serviço externo de autenticação.
- **RF-004**: O sistema MUST encaminhar o agente aprovado para o painel de monitoramento em `dashboard.html`.
- **RF-005**: O sistema MUST impedir a apresentação da visão tática quando a validação inicial não tiver sido concluída.
- **RF-006**: O sistema MUST renderizar uma visão espacial interativa ocupando 100% da viewport disponível após o acesso autorizado.
- **RF-007**: O sistema MUST iniciar a visão espacial centrada em Guanambi, Bahia, nas coordenadas `-14.2263, -42.7816`.
- **RF-008**: O sistema MUST iniciar a visão espacial com perspectiva inclinada ou isométrica, incluindo volumetria e altura perceptíveis dos prédios da cidade em três dimensões.
- **RF-009**: O sistema MUST aplicar à visão espacial um estilo noturno e de alto contraste, coerente com o design Cyber Forensic do projeto.
- **RF-010**: O sistema MUST plotar marcadores vermelhos geolocalizados para dispositivos, servidores ou indivíduos sob investigação por violação da LGPD.
- **RF-011**: O sistema MUST abrir um popup ao selecionar um marcador, contendo pelo menos IP, status investigativo e infração associada.
- **RF-012**: O sistema MUST exibir um terminal de logs sobreposto ao mapa e posicionado à direita do painel.
- **RF-013**: O terminal MUST inserir automaticamente uma nova linha de evento a cada poucos segundos enquanto o painel estiver ativo.
- **RF-014**: O terminal MUST produzir eventos fictícios dos tipos ALPR, Rastreamento IP e Reconhecimento Facial (Matches).
- **RF-015**: Cada evento ALPR MUST informar leitura de placa em avenida principal e indicar restrição de roubo ou pendência legal.
- **RF-016**: Cada evento de Rastreamento IP MUST informar conexão de dispositivo móvel a rede pública e sinalizar tráfego suspeito.
- **RF-017**: Cada evento de Reconhecimento Facial MUST usar alerta vermelho quando uma câmera do "Olho Vivo" identificar indivíduo com mandado de prisão em aberto.
- **RF-018**: O terminal MUST realizar auto-scroll para manter o evento mais recente visível na parte inferior.
- **RF-019**: Todo texto de interface, alerta, popup, log, requisito e documentação MUST estar em Português do Brasil, exceto nomes de tecnologias, bibliotecas e comandos.
- **RF-020**: O sistema MUST manter o mapa sem barras de rolagem globais e MUST preservar a legibilidade do mapa, terminal, marcadores, popups e alertas em diferentes larguras de viewport.
- **RF-021**: A funcionalidade visual entregue MUST possuir teste manual de layout documentado para autenticação, transição ao painel, visão espacial, popup, terminal, auto-scroll e estados de alerta.
- **RF-022**: O projeto MUST NOT gerar arquivos de testes automatizados, incluindo Jest e Mocha.
- **RF-023**: O sistema MUST gerar um novo marcador vermelho de vazamento em intervalo de 8 segundos,
  usando coordenadas aleatórias dentro de um raio máximo de 2 km do centro de Guanambi.
- **RF-024**: O popup de cada marcador gerado MUST apresentar um dossiê HTML estilizado com foto
  simulada do RandomUser, nome fictício, IP rastreado, status `MANDADO ATIVO` e infração à LGPD.
- **RF-025**: O dossiê MUST incluir um iframe do Google Maps Embed com a latitude e longitude exatas
  do alvo, visão de satélite e `pointer-events: auto`.
- **RF-026**: O sistema MUST carregar Turf.js v6.5.0 via CDN e definir pelo menos três rotas GeoJSON
  do tipo `Feature<LineString>` para a patrulha ALPR.
- **RF-027**: O sistema MUST calcular pontos das rotas com `turf.length()` e `turf.along()` e
  atualizar uma Source GeoJSON do Mapbox a cada quadro de `requestAnimationFrame`.
- **RF-028**: O terminal MUST emitir um log de leitura ALPR bem-sucedida sempre que um veículo
  completar um ciclo de sua rota.
- **RF-029**: O painel MUST exibir `ALERTAS CRÍTICOS` abaixo do cabeçalho da operação, pulsar em
  vermelho neon quando um alvo novo for gerado e oferecer `SILENCIAR ALARME` sem interromper a
  geração dos eventos.
- **RF-030**: Ao selecionar qualquer marcador vermelho, o sistema MUST calcular com Turf.js uma
  rota provável até uma saída rodoviária simulada como BR-030 e desenhar uma linha vermelha
  pontilhada animada no mapa.
- **RF-031**: O dossiê MUST informar distância estimada da fuga e tempo de interceptação calculados
  a partir da rota prevista.
- **RF-032**: O dossiê MUST oferecer `GRAMPEAR COMUNICAÇÃO`, abrindo um subterminal com efeito de
  máquina de escrever, pacotes HEX e texto interceptado simulado em tempo real.
- **RF-033**: O dossiê OSINT MUST conter nome completo, idade, CPF simulado, RG, endereço em
  Guanambi-BA, veículos e placas monitoradas, IPs associados, ISP e histórico investigativo.

### Entidades Principais

- **Credencial de Acesso**: Conjunto simulado formado pela credencial de agente ou perito e pela chave de acesso governamental; controla a entrada na visão tática.
- **Sessão de Agente**: Estado temporário que representa o acesso autorizado ao painel e a possibilidade de consultar os módulos operacionais.
- **Alvo Investigativo**: Dispositivo, servidor ou indivíduo geolocalizado, com IP, status, infração, coordenadas e dados sigilosos associados.
- **Evento de Inteligência**: Registro temporal fictício exibido no terminal, classificado como ALPR, Rastreamento IP ou Reconhecimento Facial.
- **Ocorrência ALPR**: Leitura de placa com via observada e indicação de restrição de roubo ou pendência legal.
- **Alerta de Rastreamento IP**: Evento de dispositivo móvel conectado a rede pública com indicação de tráfego suspeito.
- **Correspondência Facial**: Evento de câmera do "Olho Vivo" que relaciona um indivíduo a um mandado de prisão em aberto.
- **Dossiê de Vazamento**: Card HTML de um alvo gerado, com identidade fictícia, foto remota,
  status `MANDADO ATIVO`, IP, infração e iframe de visão de satélite.
- **Rota de Patrulha ALPR**: `Feature<LineString>` GeoJSON com coordenadas simuladas de uma avenida,
  duração do ciclo e identificador do veículo.
- **Veículo ALPR**: Ponto móvel derivado de uma Rota de Patrulha ALPR e atualizado na Source GeoJSON.

## Critérios de Sucesso

### Resultados Mensuráveis

- **CS-001**: Em uma avaliação manual, 100% dos acessos com os dois campos preenchidos devem chegar ao painel de monitoramento simulado sem apresentar uma tela intermediária não especificada.
- **CS-002**: Em uma avaliação manual, 100% das tentativas com campo obrigatório vazio devem permanecer na tela inicial e apresentar uma orientação compreensível em Português do Brasil.
- **CS-003**: Em 100% das avaliações do painel autorizado, o mapa deve ocupar a viewport, iniciar centrado em Guanambi e apresentar perspectiva inclinada, estilo noturno e volumetria urbana.
- **CS-004**: Em 100% das avaliações com alvos disponíveis, cada marcador vermelho selecionável deve abrir um popup com IP, status e infração correspondentes ao alvo escolhido.
- **CS-005**: Em até 10 segundos após a abertura do painel, o terminal deve exibir pelo menos um evento e, em até 30 segundos, deve ter exibido os três tipos de inteligência definidos.
- **CS-006**: Em 100% das avaliações com mais linhas do que a área visível do terminal, o evento mais recente deve permanecer visível na parte inferior sem intervenção manual do agente.
- **CS-007**: Em uma revisão visual, nenhum texto essencial, marcador, popup ou alerta deve ficar ilegível, sobreposto de forma incoerente ou fora da viewport em larguras de tela previstas para a demonstração.
- **CS-008**: Em uma revisão de conformidade, 100% dos textos criados para a funcionalidade devem estar em Português do Brasil, com exceção apenas de nomes de tecnologias, bibliotecas e comandos.
- **CS-009**: Antes da entrega, deve existir um registro de teste manual cobrindo todos os fluxos e estados visuais definidos nesta especificação, sem arquivos de testes automatizados.
- **CS-010**: Em 100% das avaliações de 10 segundos ou mais, pelo menos um novo alvo vermelho deve
  ser criado dentro do raio de 2 km e gerar um log de vazamento.
- **CS-011**: Em 100% das avaliações de um alvo gerado, o dossiê deve conter foto, nome, status,
  IP, infração, coordenadas e iframe de satélite interativo.
- **CS-012**: Em até 15 segundos de observação, pelo menos um dos três veículos deve completar sua
  rota e gerar um log ALPR sem intervenção manual.
- **CS-013**: Em 100% das gerações de alvo, o painel de alertas deve exibir o evento e iniciar o
  pulso vermelho até o agente silenciar ou reativar o alarme.
- **CS-014**: Em 100% dos cliques em marcadores, a linha de fuga, a distância e o tempo de
  interceptação devem ser exibidos de forma coerente com o dossiê.
- **CS-015**: Em 100% dos acionamentos de grampo, o subterminal deve iniciar e apresentar ao menos
  uma linha HEX e uma mensagem textual interceptada.

## Pressupostos

- O público-alvo é composto por agentes, peritos ou avaliadores autorizados a operar uma simulação de inteligência federal; não existe fluxo de cadastro público.
- A validação de acesso é demonstrativa e front-end; ela não representa autenticação governamental real nem deve ser interpretada como mecanismo de segurança de produção.
- Os alvos, coordenadas, IPs, infrações e eventos do terminal são dados fictícios para demonstração e não representam pessoas, dispositivos ou investigações reais.
- A visão espacial poderá usar a biblioteca de mapas autorizada pela constituição e os recursos necessários para apresentar terreno urbano e prédios em três dimensões.
- O painel será demonstrado em navegadores modernos com suporte à renderização gráfica necessária para a visão espacial.
- A primeira versão contempla somente a cidade de Guanambi, Bahia; outras cidades, filtros avançados, persistência de investigações e integração com fontes reais estão fora do escopo.
- A periodicidade "a cada poucos segundos" será considerada como um intervalo entre 2 e 5 segundos para fins de teste manual.
- As APIs RandomUser e Google Maps Embed são fontes externas de demonstração; falhas de rede devem
  deixar o restante do dossiê legível e não podem ser tratadas como dados reais.
- Turf.js v6.5.0 será consumido via CDN exclusivamente para geometria das rotas simuladas; não haverá
  consulta a tráfego, vias ou pessoas reais.
- O teste manual de layout será documentado como evidência de aceitação; não serão criados testes automatizados ou dependências de ferramentas de teste.
