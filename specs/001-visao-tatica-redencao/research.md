# Pesquisa e Decisões: Visão Tática Redenção

**Data**: 2026-10-01

## Decisão 1: Aplicação estática sem camada de servidor

**Decisão**: Usar somente HTML5, CSS3 e Vanilla JavaScript, com os dados fictícios mantidos em
memória no navegador.

**Justificativa**: A constituição define um Mockup Funcional client-side estático e exige execução
sem instalação de pacotes ou dependência de back-end. A solução reduz a superfície do projeto,
facilita a demonstração local e mantém a simulação explicitamente separada de qualquer operação
real.

**Alternativas consideradas**:

- React ou Angular: rejeitados por adicionarem frameworks pesados que não são necessários para
  duas telas estáticas.
- Node.js, Python ou SQL: rejeitados porque a funcionalidade não precisa de servidor, persistência
  ou banco de dados.

## Decisão 2: Mapbox GL JS v2.14.1 via CDN

**Decisão**: Carregar o CSS e o JavaScript de Mapbox GL JS v2.14.1 por CDN e manter um placeholder
explícito para o token.

**Justificativa**: Mapbox GL JS fornece navegação interativa, câmera inclinada e camada de
prédios em três dimensões, atendendo ao módulo God's Eye sem instalar dependências. A versão foi
fixada pelo pedido do plano para tornar a demonstração reproduzível.

**Alternativas consideradas**:

- Biblioteca de mapas diferente: rejeitada porque não atende diretamente à camada de prédios
  `fill-extrusion` já prevista na especificação.
- Mapa estático sem interação: rejeitado porque não permite navegação, seleção de alvos nem a
  perspectiva espacial solicitada.

## Decisão 3: Camada urbana adicionada após `style.load`

**Decisão**: Adicionar a camada `3d-buildings` do tipo `fill-extrusion` no evento `style.load`.

**Justificativa**: A camada depende do estilo carregado. Executar a configuração nesse ponto evita
referenciar uma fonte ou camada antes de o mapa estar pronto e permite aplicar altura e base dos
prédios à visualização inclinada.

**Alternativas consideradas**:

- Adicionar a camada imediatamente na criação do mapa: rejeitado porque o estilo ainda pode não
  ter terminado de carregar.
- Desenhar prédios manualmente: rejeitado por duplicar dados espaciais e aumentar a complexidade
  do mock.

## Decisão 4: Eventos IoT determinísticos no formato visual do terminal

**Decisão**: Manter um array fixo de strings HTML controladas, com classes para ALPR OK, Match
Facial e IP Suspeito; a cada 3500 ms uma entrada será escolhida, receberá a hora atual e será
inserida no terminal com auto-scroll.

**Justificativa**: O array fixo torna a simulação previsível, demonstrável e independente de
fontes externas. `window.setInterval()` reproduz a passagem de eventos, enquanto `scrollTop`
garante que o evento mais recente permaneça visível.

**Alternativas consideradas**:

- WebSocket ou fonte real de IoT: rejeitados porque violam o escopo estático e poderiam sugerir
  monitoramento real.
- Texto sem classes visuais: rejeitado porque não distingue os níveis operacionais exigidos pelo
  terminal.

**Controle de segurança da decisão**: As strings HTML serão constantes internas do mock. Nenhuma
entrada do agente, token, coordenada ou dado externo será concatenado diretamente nelas.

## Decisão 5: Fonte monoespaçada por Google Fonts CDN

**Decisão**: Importar Share Tech Mono ou Courier Prime por Google Fonts CDN, com fallback para
Courier New e Consolas.

**Justificativa**: A tipografia reforça a leitura de terminal e atende à constituição sem criar
arquivos de fonte no projeto.

**Alternativas consideradas**:

- Fonte proporcional: rejeitada porque enfraquece a identidade de terminal e a leitura alinhada
  de logs.
- Fonte local obrigatória: rejeitada porque poderia variar entre máquinas de demonstração.

## Decisão 6: Geometria de patrulha com Turf.js v6.5.0

**Decisão**: Carregar Turf.js v6.5.0 por CDN e usar `turf.length()` e `turf.along()` sobre três
`Feature<LineString>` GeoJSON para posicionar os veículos ALPR em uma Source do Mapbox.

**Justificativa**: A geometria fica explícita, reproduzível e separada da apresentação. O veículo
segue os pontos da rota simulada, em vez de atravessar livremente o mapa por interpolação de
latitude/longitude sem contexto de via.

**Alternativas consideradas**:

- Interpolação manual entre dois pontos: rejeitada porque não representa uma LineString nem oferece
  cálculo de comprimento e posição ao longo da rota.
- Consulta de vias reais em tempo de execução: rejeitada porque introduziria uma dependência de
  dados externos e excederia o escopo do Mockup Funcional.

## Decisão 7: Recursos OSINT remotos controlados

**Decisão**: Usar RandomUser para retratos simulados e Google Maps Embed para a visão de satélite
dos alvos gerados, sem enviar dados reais de pessoas ou investigações.

**Justificativa**: Os dois recursos atendem à experiência visual solicitada sem back-end e deixam
claro que o dossiê é uma simulação. As coordenadas são geradas localmente e o iframe recebe apenas
essa posição fictícia.

**Alternativas consideradas**:

- Armazenar imagens e mapas localmente: rejeitado porque aumentaria o artefato e reduziria a
  variedade visual da demonstração.
- Usar fontes de investigação reais: rejeitado por incompatibilidade com o escopo, privacidade e
  constituição do projeto.

## Pendências resolvidas

Não há pendências de esclarecimento. O placeholder do token não é uma pendência de escopo: é uma
configuração manual obrigatória antes de uma execução com mapa real e não deve conter um segredo
versionado no projeto.
