# Guia de Validação Manual: Visão Tática Redenção

**Data**: 2026-10-01

Este guia valida a demonstração ponta a ponta sem testes automatizados. A execução depende de um
navegador moderno, conexão com a Internet para os CDNs e um token de demonstração do Mapbox
configurado manualmente no código local. O token não deve ser versionado.

## Pré-requisitos

- Abrir a raiz do projeto em um navegador moderno.
- Configurar manualmente o placeholder `COLOQUE_SEU_TOKEN_MAPBOX_AQUI` com um token válido para a
  demonstração do Mapbox.
- Garantir que o navegador permita carregar recursos externos por CDN.
- Usar uma viewport desktop e repetir a inspeção em uma viewport estreita.

## Execução

1. Abrir `index.html` diretamente no navegador.
2. Preencher `Credencial de Agente/Perito` e `Chave de Acesso Governamental` com valores de
   demonstração.
3. Confirmar o acesso e verificar a transição para `dashboard.html`.

## Roteiro de aceitação

### Acesso restrito

- Confirmar que os dois campos aparecem com seus rótulos exatos.
- Confirmar que `Esqueci minha senha` e `Cadastrar` não aparecem.
- Tentar confirmar com um campo vazio; registrar que um alerta em Português do Brasil aparece e a
  tela não muda.
- Preencher os dois campos e registrar que o painel é aberto.
- Tentar abrir o painel sem validar a sessão; registrar que os dados operacionais permanecem
  bloqueados.

### Visão espacial

- Confirmar que o mapa ocupa a viewport e não cria rolagem global.
- Confirmar o centro em Guanambi pelas coordenadas `-14.2263, -42.7816`.
- Confirmar perspectiva inclinada, com pitch 60, bearing -17.6 e zoom 15.5.
- Confirmar estilo noturno de alto contraste e prédios com volumetria 3D.
- Arrastar, aproximar e afastar o mapa; registrar que a navegação permanece responsiva.

### Alvos e popups

- Confirmar a presença de marcadores vermelhos geolocalizados.
- Selecionar um marcador e registrar que o popup mostra IP, status e infração.
- Fechar o popup e selecionar outro marcador; registrar que os dados mudam para o novo alvo.
- Clicar em uma área sem marcador; registrar que nenhum popup é aberto.

### Terminal IoT

- Confirmar que o terminal está sobreposto à direita, com 350 px por 400 px na viewport desktop.
- Aguardar pelo menos 10 segundos e registrar a chegada de eventos sem recarregar a página.
- Aguardar até 30 segundos e confirmar ALPR, Rastreamento IP e Reconhecimento Facial.
- Confirmar que ALPR OK aparece em verde e que Match Facial e IP Suspeito aparecem em vermelho.
- Confirmar que cada linha comunica Vigilância Ativa em Português do Brasil.
- Aguardar linhas suficientes para ultrapassar a área visível e registrar que o auto-scroll mantém o
  evento mais recente na parte inferior.

### Vazamentos e dossiês OSINT

- Aguardar pelo menos 8 segundos e confirmar o surgimento de um novo marcador vermelho dentro do
  raio operacional de Guanambi.
- Selecionar o marcador `VAZAMENTO DE DADOS` e confirmar foto, nome fictício, IP, status `MANDADO
ATIVO`, infração e coordenadas.
- Interagir com o iframe de satélite e confirmar que a coordenada exibida corresponde ao marcador.
- Bloquear temporariamente RandomUser ou Google Maps Embed e confirmar que a interface mantém o
  restante do dossiê legível.

### Patrulha ALPR com Turf.js

- Confirmar três pontos azuis brilhantes sobre as rotas simuladas.
- Observar os pontos por pelo menos 15 segundos e confirmar que percorrem as LineStrings sem saltos
  visuais.
- Aguardar a conclusão de uma rota e confirmar o log `[ALPR // R-01]`, `[ALPR // R-02]` ou
  `[ALPR // R-03]`.
- Colocar a aba em segundo plano e confirmar que o fallback temporizado continua avançando os ciclos
  da simulação.

### Alertas, geofencing e grampo tático

- Aguardar um novo vazamento e confirmar o pulso vermelho no painel `ALERTAS CRÍTICOS`.
- Acionar `SILENCIAR ALARME` e confirmar a troca para `REATIVAR ALARME`, sem interromper os novos
  registros.
- Selecionar qualquer marcador vermelho e confirmar a linha pontilhada animada em direção à BR-030,
  além da distância e do tempo de interceptação no dossiê.
- Acionar `GRAMPEAR COMUNICAÇÃO` e confirmar o subterminal, as linhas `HEX` e o texto interceptado
  com efeito de máquina de escrever.
- Confirmar no dossiê nome, idade, CPF simulado, RG, endereço, veículos, IPs, ISP e histórico.

### Responsividade e falhas

- Repetir a inspeção em viewport estreita; registrar que mapa, terminal, textos, popups e alertas
  continuam legíveis sem rolagem global.
- Remover temporariamente o token ou bloquear o CDN; registrar uma mensagem de falha em Português
  do Brasil sem simular que o mapa está operacional.
- Simular uma coleção vazia de alvos; registrar que a visão continua navegável e informa que não
  há alvos ativos.

## Registro do resultado

Registro parcial executado em 2026-10-01 no navegador integrado do VS Code:

- **Data e navegador**: 2026-10-01, navegador integrado do VS Code.
- **Resultado do acesso**: aprovado; os dois campos foram preenchidos e o redirecionamento para
  `dashboard.html` ocorreu. O acesso direto sem sessão exibiu `ACESSO NEGADO`.
- **Resultado da visão espacial**: estrutura aprovada; o mapa, os controles, a câmera configurada
  e os marcadores foram criados. Tiles e volumetria 3D aguardam token válido.
- **Resultado dos popups**: aprovado; o marcador `DISPOSITIVO INTERCEPTADO` exibiu IP, status e
  infração coerentes.
- **Resultado do terminal e auto-scroll**: aprovado; houve novo evento após 3500 ms e os tipos de
  log previstos foram renderizados.
- **Resultado responsivo e de falhas**: aprovado na viewport estreita de 390 x 844; o painel e o
  terminal permaneceram visíveis. Sem token válido, o painel exibiu alerta de falha de autorização.
- **Desvios observados**: tiles e volumetria 3D ainda não foram confirmados porque o projeto contém
  somente o placeholder do token Mapbox.

Pendências de entrega: configurar um token válido localmente, confirmar tiles/volumetria, capturar
prints das duas telas e anexá-los ao PDF da atividade.

Nenhum arquivo de teste automatizado deve ser criado como parte desta validação.
