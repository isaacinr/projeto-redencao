# Tarefas: Visão Tática Redenção

**Entrada**: Documentos de design em `specs/001-visao-tatica-redencao/`

**Pré-requisitos**: `plan.md`, `spec.md`, `research.md`, `data-model.md`, `contracts/ui.md` e `quickstart.md`.

**Estratégia**: Execução linear em cinco fases. Cada tarefa deve ser concluída antes da próxima,
exceto quando a própria tarefa indicar uma verificação independente. Não serão criados testes
automatizados; a validação será manual e documentada.

## Fase 1: SETUP E FUNDAÇÃO

**Objetivo**: Criar a base mínima do Mockup Funcional estático conforme `plan.md`.

- [x] T001 Criar a estrutura do diretório `redencao/` na raiz do projeto, mantendo somente a organização estática prevista para a aplicação.
- [x] T002 Criar o arquivo em branco `redencao/index.html` para a tela inicial de terminal de segurança governamental.
- [x] T003 Criar o arquivo em branco `redencao/dashboard.html` para o painel tático com mapa e terminal de logs.

**Critério de conclusão**: Os dois arquivos existem na raiz do projeto e não há diretórios de
back-end, servidor ou suíte de testes automatizados.

## Fase 2: DESENVOLVIMENTO DO MÓDULO DE ACESSO (`index.html`)

**História atendida**: `[US1]` Validar acesso de agente ou perito.

**Objetivo**: Entregar uma tela de acesso restrito capaz de conduzir o agente autenticado ao painel.

- [x] T004 [US1] Estruturar `redencao/index.html` com HTML5 semântico, título do Projeto Redenção, formulário e os campos obrigatórios `Credencial de Agente/Perito` e `Chave de Acesso Governamental`.
- [x] T005 [US1] Implementar o CSS interno em `redencao/index.html` com Dark Mode / Cyber, formulário centralizado, borda sólida de 1 px verde neon, inputs transparentes, `outline: 0` e texto verde.
- [x] T006 [US1] Adicionar em `redencao/index.html` o botão de submissão com hover que inverte fundo verde e texto preto, sem criar ações `Esqueci minha senha` ou `Cadastrar`.
- [x] T007 [US1] Implementar em `redencao/index.html` o script do formulário para validar os dois campos, exibir alerta em Português do Brasil quando algum estiver vazio e redirecionar os valores preenchidos com `window.location.href` para `dashboard.html`.

**Teste independente**: Abrir `redencao/index.html`, confirmar os rótulos e a ausência das ações
proibidas, testar campo vazio e validar o redirecionamento após preencher os dois campos.

## Fase 3: DESENVOLVIMENTO DO MÓDULO GOD'S EYE (`dashboard.html` - Parte 1)

**Histórias atendidas**: `[US2]` Observar a cidade pela visão God's Eye e `[US3]` Investigar alvos geolocalizados.

**Objetivo**: Entregar mapa noturno interativo de Guanambi com câmera inclinada, volumetria urbana
e dois alvos simulados consultáveis.

- [x] T008 [US2] Importar em `redencao/dashboard.html` o CSS e o JavaScript do Mapbox GL JS v2.14.1 via CDN e a fonte `Share Tech Mono` ou `Courier Prime` via Google Fonts CDN.
- [x] T009 [US2] Configurar em `redencao/dashboard.html` o placeholder explícito `COLOQUE_SEU_TOKEN_MAPBOX_AQUI` em `mapboxgl.accessToken`, sem versionar um token real.
- [x] T010 [US2] Inicializar em `redencao/dashboard.html` o objeto `mapboxgl.Map` com estilo noturno `dark-v11`, centro em Guanambi, Bahia (`[-42.7816, -14.2263]`) e a configuração inicial `zoom: 15.5`.
- [x] T011 [US2] Aplicar em `redencao/dashboard.html` as configurações de câmera 3D `pitch: 60` e `bearing: -17.6`, preservando a navegação de deslocamento e aproximação.
- [x] T012 [US2] Implementar em `redencao/dashboard.html` o evento `style.load` para adicionar a camada `3d-buildings` do tipo `fill-extrusion`, usando a volumetria e a altura dos prédios.
- [x] T013 [US3] Criar em `redencao/dashboard.html` exatamente 2 instâncias de `mapboxgl.Marker` em vermelho, representando dispositivos interceptados com coordenadas simuladas dentro da área de Guanambi.
- [x] T014 [US3] Associar a cada marcador de `redencao/dashboard.html` um popup com IP, status investigativo e infração em Português do Brasil, incluindo exemplos como `IP: 192.168.0.1`, `Status: Interceptado` e `Infração: Vazamento de Dados`.

**Teste independente**: Abrir o painel após o acesso, confirmar o centro e a câmera, observar os
prédios em 3D, selecionar cada um dos dois marcadores e verificar seu popup correspondente.

## Fase 4: DESENVOLVIMENTO DO MÓDULO DE INTELIGÊNCIA IOT (`dashboard.html` - Parte 2)

**História atendida**: `[US4]` Acompanhar inteligência IoT em tempo real.

**Objetivo**: Entregar o terminal lateral sobreposto ao mapa com eventos simulados, cores
operacionais e rolagem automática.

- [x] T015 [US4] Criar em `redencao/dashboard.html` a div flutuante `.painel-iot` sobreposta ao mapa e posicionada à direita.
- [x] T016 [US4] Aplicar em `redencao/dashboard.html` o estilo do `.painel-iot` com `position: absolute`, `top: 20px`, `right: 20px`, `width: 350px`, `height: 400px`, `background: rgba(0,0,0,0.85)`, borda `1px solid #333`, sombra neon verde sutil, `overflow-y: auto` e `z-index: 10`.
- [x] T017 [US4] Garantir em `redencao/dashboard.html` que o container do mapa use `position: absolute`, `top: 0`, `left: 0`, `width: 100%`, `height: 100%` e `z-index: 1`, sem barras de rolagem globais no `body`.
- [x] T018 [US4] Criar em `redencao/dashboard.html` o array fixo de strings HTML controladas com eventos ALPR OK, IP Suspeito e Face Match, usando classes verdes para ALPR OK e vermelhas para IP Suspeito e Face Match, alinhados à narrativa da Operação Redenção.
- [x] T019 [US4] Implementar em `redencao/dashboard.html` o motor de logs com `window.setInterval()` a cada `3500ms`, seleção de uma string aleatória, concatenação da hora atual por `new Date()` e injeção na div do terminal por `innerHTML` apenas com strings internas controladas.
- [x] T020 [US4] Ajustar em `redencao/dashboard.html` o `scrollTop` do terminal após cada inserção para manter o evento mais recente visível na parte inferior.
- [x] T021 [US3] Implementar em `redencao/dashboard.html` a geração de novos alvos vermelhos a cada 8 segundos dentro de um raio máximo de 2 km do centro de Guanambi.
- [x] T022 [US3] Construir em `redencao/dashboard.html` o dossiê HTML do alvo gerado com foto RandomUser, nome fictício, IP, status `MANDADO ATIVO`, infração e iframe Google Maps Embed com `pointer-events: auto`.
- [x] T023 [US5] Importar Turf.js v6.5.0 via CDN em `redencao/dashboard.html` e manter a dependência sem instalação de pacotes ou back-end.
- [x] T024 [US5] Definir em `redencao/dashboard.html` três rotas GeoJSON `Feature<LineString>` com coordenadas simuladas de avenidas próximas a Guanambi.
- [x] T025 [US5] Criar em `redencao/dashboard.html` a Source GeoJSON `veiculos-alpr` e a camada Mapbox de círculos azuis brilhantes para os três veículos.
- [x] T026 [US5] Implementar em `redencao/dashboard.html` `turf.length()`, `turf.along()` e `requestAnimationFrame` para atualizar os veículos continuamente ao longo das rotas.
- [x] T027 [US5] Emitir em `redencao/dashboard.html` um log ALPR ao concluir cada ciclo de rota e manter uma atualização temporizada de fallback para abas suspensas.

**Teste independente**: Observar o painel por pelo menos 30 segundos, confirmar os três tipos de
evento, as cores verde/vermelho e o auto-scroll sem recarregar a página.

## Fase 5: VALIDAÇÃO E ENTREGA

**Objetivo**: Confirmar funcionamento visual, responsividade e evidências manuais sem criar testes
automatizados.

- [x] T028 Executar `redencao/index.html` no navegador e validar em `specs/001-visao-tatica-redencao/quickstart.md` a responsividade da tela, os campos obrigatórios, a ausência de cadastro/recuperação e o redirecionamento para `dashboard.html`.
- [ ] T029 Inserir manualmente um token válido no placeholder de `redencao/dashboard.html` e validar em `specs/001-visao-tatica-redencao/quickstart.md` o carregamento dos tiles, o estilo `dark-v11`, a camada `fill-extrusion` e a volumetria 3D.
- [x] T030 Validar em `specs/001-visao-tatica-redencao/quickstart.md` os 2 marcadores, os popups, os eventos ALPR/IP/Face Match, o intervalo de 3500 ms, as cores dos alertas e o auto-scroll.
- [x] T031 Repetir a validação em viewport estreita e registrar em `specs/001-visao-tatica-redencao/quickstart.md` qualquer sobreposição, perda de legibilidade, falha de carregamento ou criação indevida de rolagem global.
- [ ] T032 Tirar print screen de `redencao/index.html` e `redencao/dashboard.html` em pleno funcionamento e anexar as duas evidências ao PDF de entrega da atividade.
- [ ] T033 Confirmar em `specs/001-visao-tatica-redencao/quickstart.md` o resultado final de todos os fluxos e assegurar que nenhum arquivo de teste automatizado foi criado.

**Critério de conclusão**: O roteiro manual está preenchido, as duas telas funcionam com token
válido, as evidências visuais foram capturadas e todos os itens desta lista estão concluídos.

## Dependências e Ordem de Execução

A ordem é linear e obrigatória:

`T001 -> T002 -> T003 -> T004 -> T005 -> T006 -> T007 -> T008 -> T009 -> T010 -> T011 -> T012 -> T013 -> T014 -> T015 -> T016 -> T017 -> T018 -> T019 -> T020 -> T021 -> T022 -> T023 -> T024 -> T025 -> T026 -> T027 -> T028 -> T029 -> T030 -> T031 -> T032 -> T033 -> T034 -> T035 -> T036 -> T037 -> T038`

- `[US1]` depende de `T001` a `T003` e é pré-requisito operacional para o painel.
- `[US2]` depende de `[US1]` e cobre a inicialização, câmera, estilo e camada 3D.
- `[US3]` depende de `[US2]` para posicionar e abrir os marcadores no mapa.
- `[US4]` depende da estrutura de `dashboard.html`, mas sua validação final ocorre junto com `[US2]` e `[US3]`.
- `[US5]` depende de `[US2]` para a Source GeoJSON e de `[US4]` para registrar as leituras no terminal.
- A entrega depende de todas as histórias concluídas e do preenchimento do roteiro manual.

## Oportunidades de Execução Paralela

O pedido prioriza execução linear; portanto nenhuma tarefa foi marcada com `[P]`. As verificações
de `[US2]`, `[US3]` e `[US4]` são separáveis como critérios de teste, mas devem ser executadas
após a fundação comum e registradas na ordem definida para evitar divergência entre o mapa e o
terminal.

## Estratégia de MVP

O MVP é `[US1]`: tela de acesso restrito funcional, com campos obrigatórios, validação simulada e
redirecionamento para `dashboard.html`. A entrega completa adiciona a visão God's Eye, os dois
marcadores, o terminal IoT e a evidência visual exigida na Fase 5.

## Fase 6: SUPER-FUNCIONALIDADES TÁTICAS

**Objetivo**: Registrar os incrementos avançados de alertas, geofencing, comunicação e OSINT
entregues após a primeira versão do checklist.

- [x] T034 Implementar em `redencao/dashboard.html` o painel `ALERTAS CRÍTICOS` abaixo do cabeçalho, com pulso vermelho e botão `SILENCIAR ALARME`.
- [x] T035 Implementar em `redencao/dashboard.html` a predição Turf.js de fuga até BR-030, a camada de linha pontilhada animada e os campos de distância e tempo de interceptação no dossiê.
- [x] T036 Implementar em `redencao/dashboard.html` o botão `GRAMPEAR COMUNICAÇÃO` e o subterminal com escrita progressiva de pacotes HEX e texto interceptado.
- [x] T037 Expandir em `redencao/dashboard.html` o dossiê OSINT com nome, idade, CPF, RG, endereço, veículos, placas, IPs, ISP e histórico investigativo.
- [x] T038 Validar no navegador alertas, silenciamento, dossiê, geofence, grampo e compatibilidade com a sessão `sessionStorage`.

**Critério de conclusão**: Os cinco incrementos estão funcionais em client-side e os estados
visuais permanecem compatíveis com a identidade Cyber-Forensic.

## Resumo de Tarefas

- **Total**: 38 tarefas.
- **Setup e fundação**: 3 tarefas.
- **Módulo de acesso `[US1]`**: 4 tarefas.
- **Módulo God's Eye `[US2]` e alvos `[US3]`**: 7 tarefas.
- **Módulo de inteligência IoT `[US4]`**: 6 tarefas.
- **OSINT e patrulha ALPR `[US3]/[US5]`**: 7 tarefas.
- **Super-funcionalidades táticas**: 5 tarefas.
- **Validação e entrega**: 6 tarefas.
- **Testes automatizados**: 0 tarefas, conforme a constituição.
- **Formato**: todas as tarefas usam checkbox, ID sequencial, rótulo de história quando aplicável e caminho de arquivo.
