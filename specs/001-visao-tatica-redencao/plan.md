# Plano de Implementação: Visão Tática Redenção

**Ramo**: `001-visao-tatica-redencao` | **Data**: 2026-10-01 | **Especificação**: [spec.md](spec.md)

**Entrada**: Especificação da funcionalidade em [spec.md](spec.md)

**Nota**: Este plano documenta a execução técnica da funcionalidade.

## Resumo

O Projeto Redenção será um Mockup Funcional client-side estático para acesso restrito,
monitoramento espacial 3D de Guanambi e inteligência IoT simulada. A solução será composta por
`index.html` e `dashboard.html`, com HTML5 semântico, CSS3 e Vanilla JavaScript. Mapbox GL JS
v2.14.1 e Turf.js v6.5.0 serão carregados por CDN para a visão espacial e a geometria das rotas;
RandomUser e Google Maps Embed fornecerão recursos remotos de demonstração. Os dados de
autenticação, alvos, veículos e eventos permanecerão em memória no navegador.

## Contexto Técnico

<!--
  ACTION REQUIRED: Replace the content in this section with the technical details
  for the project. The structure here is presented in advisory capacity to guide
  the iteration process.
-->

**Linguagem/Versão**: HTML5, CSS3 e Vanilla JavaScript (JavaScript executado pelo navegador)

**Dependências Principais**: Mapbox GL JS v2.14.1 e Turf.js v6.5.0 via CDN; Share Tech Mono ou Courier Prime via Google Fonts CDN; RandomUser e Google Maps Embed como APIs de demonstração

**Armazenamento**: N/A; mock de dados mantido exclusivamente na memória do navegador

**Testes**: Teste manual de layout e comportamento documentado; nenhum Jest, Mocha ou outro arquivo de teste automatizado

**Plataforma-Alvo**: Navegadores modernos em desktop, com suporte a WebGL e carregamento de recursos via CDN

**Tipo de Projeto**: Aplicação web estática client-side

**Metas de Desempenho**: Primeiro evento do terminal em até 10 segundos; três tipos de evento em até 30 segundos; navegação do mapa sem travamento perceptível durante a demonstração

**Restrições**: Sem back-end, Node.js, Python ou SQL; sem frameworks pesados; token do Mapbox deve permanecer configurável; `body` sem rolagem global; conteúdo integralmente em Português do Brasil, salvo nomes técnicos; dados externos somente para fotos e visão de satélite simuladas

**Escala/Escopo**: Uma tela de autenticação, um painel tático, uma cidade (Guanambi), alvos e eventos fictícios em memória; sem persistência, cadastro, recuperação de senha ou integração com fontes reais

## Verificação da Constituição

_PORTÃO: deve passar antes da Fase 0 de pesquisa e ser reavaliado após o design da Fase 1._

- **Qualidade de código**: PASS. A divisão de `index.html` e `dashboard.html` mantém responsabilidades separadas; a lógica simulada ficará em funções JavaScript nomeadas e comentadas em Português do Brasil.
- **Arquitetura estática**: PASS. Não haverá back-end nem instalação de pacotes; Mapbox GL JS, Turf.js e a fonte serão consumidos por CDN, enquanto RandomUser e Google Maps Embed serão usados apenas como recursos remotos do mock.
- **Redenção e Vigilância Ativa**: PASS. O acesso precede o painel, e mapa, popups e logs usarão contexto de Mandados, Quebra de IP, ALPR e LGPD.
- **Interface governamental**: PASS. O plano cobre fundo preto/cinza chumbo, verde neon, vermelho alerta, tipografia monoespaçada, mapa em viewport total e terminal sobreposto.
- **Teste manual**: PASS. `quickstart.md` documentará os fluxos de autenticação, mapa, alvos, terminal, auto-scroll e estados de falha; não serão criados testes automatizados.
- **Idioma**: PASS. Artefatos, textos de interface, alertas, logs e comentários serão produzidos em Português do Brasil; somente tecnologias, bibliotecas e comandos conservarão seus nomes originais.

## Estrutura do Projeto

### Documentação (esta funcionalidade)

```text
specs/001-visao-tatica-redencao/
├── plan.md              # Este plano
├── research.md          # Decisões técnicas e alternativas
├── data-model.md        # Entidades e estados do mock
├── quickstart.md        # Validação manual ponta a ponta
├── contracts/
│   └── ui.md            # Contratos de interação das telas
├── checklists/
│   └── requirements.md  # Checklist da especificação
└── tasks.md             # Gerado posteriormente por /speckit-tasks
```

### Código-Fonte (raiz do repositório)

```text
redencao/
├── index.html       # Tela inicial simulando terminal de segurança governamental
└── dashboard.html   # Painel tático com mapa e terminal de logs
```

**Decisão de Estrutura**: Projeto estático de dois documentos HTML, conforme a constituição.
Cada página terá seus estilos e sua lógica JavaScript organizados por responsabilidade, sem
introduzir diretórios de back-end, módulos de servidor ou suítes automatizadas.

## Decisões de Implementação

### Acesso e sessão simulada

- `index.html` exibirá os dois campos obrigatórios, sem cadastro ou recuperação de senha.
- A validação front-end aceitará valores de demonstração e redirecionará para `dashboard.html`.
- O estado de autorização será transitório e não representará autenticação de produção.

### Mapa e câmera

- O código deixará `mapboxgl.accessToken` com o placeholder explícito
  `COLOQUE_SEU_TOKEN_MAPBOX_AQUI` para configuração manual posterior.
- A inicialização usará centro `[-42.7816, -14.2263]`, `pitch: 60`, `bearing: -17.6` e
  `zoom: 15.5`.
- No evento `style.load`, será adicionada a camada `3d-buildings` do tipo `fill-extrusion`,
  usando atributos de altura e base para produzir a volumetria urbana.
- Marcadores vermelhos serão criados a partir de uma coleção fixa e de uma geração aleatória a
  cada 8 segundos, sempre em um raio máximo de 2 km do centro; os alvos gerados terão dossiês com
  foto RandomUser, status, IP, infração e iframe Google Maps Embed interativo.

### Terminal IoT

- Um array fixo de strings HTML controladas representará os eventos ALPR, Match Facial e IP
  Suspeito, com classes visuais verde ou vermelha.
- `window.setInterval()` executará a cada 3500 ms, escolherá um evento, prefixará a hora atual
  obtida por `new Date()` e o injetará no terminal.
- Após cada inserção, `scrollTop` será ajustado para o fim do conteúdo; como as strings são
  constantes do próprio mock, nenhuma entrada externa será interpolada.

### Geometria e patrulha ALPR

- Turf.js v6.5.0 será carregado por CDN e fornecerá três `Feature<LineString>` GeoJSON com
  coordenadas simuladas de avenidas próximas ao centro.
- `turf.length()` calculará o comprimento de cada rota e `turf.along()` produzirá a coordenada do
  veículo em cada ciclo.
- Uma Source GeoJSON `veiculos-alpr` e uma camada `circle` azul serão atualizadas no
  `requestAnimationFrame`; um fallback temporizado manterá a simulação em abas suspensas.
- Cada conclusão de rota emitirá um log ALPR bem-sucedido no terminal.

### Recursos OSINT simulados

- Fotos serão referenciadas por `https://randomuser.me/api/portraits/men/{indice}.jpg`.
- A visão de satélite usará `https://maps.google.com/maps?q={lat},{lng}&t=k&z=17&output=embed`,
  com `pointer-events: auto` para permitir interação no iframe.

### Estilos e composição

- A fonte `Share Tech Mono` ou `Courier Prime` será importada pelo Google Fonts CDN, com fallback
  para `Courier New` e `Consolas`.
- A tela de login será centralizada, com borda verde neon de 1 px, inputs transparentes, outline
  removido e hover do botão invertendo fundo e texto.
- O mapa usará `position: absolute`, `top: 0`, `left: 0`, `width: 100%`, `height: 100%` e
  `z-index: 1`.
- O painel IoT usará `position: absolute`, `top: 20px`, `right: 20px`, `width: 350px`,
  `height: 400px`, fundo `rgba(0,0,0,0.85)`, borda `1px solid #333`, sombra neon verde sutil,
  `overflow-y: auto` e `z-index: 10`.

## Controle de Complexidade

Não há violações da constituição que exijam justificativa. A solução de dois arquivos HTML e
dados em memória é a alternativa mais simples compatível com o Mockup Funcional solicitado.
