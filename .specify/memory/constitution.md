<!--
Sync Impact Report
Version change: scaffold sem versão efetiva -> 1.0.0
Modified principles: placeholders do scaffold -> cinco princípios do Projeto Redenção
Added sections: Restrições Técnicas e de Produto; Processo de Desenvolvimento e Qualidade
Removed sections: nenhuma seção normativa anterior
Follow-up TODOs: confirmar a data histórica de ratificação do projeto
-->

# Constituição do Projeto Redenção

## Princípios Fundamentais

### I. Qualidade de Código e Separação de Responsabilidades

O código MUST seguir as melhores práticas de HTML5 semântico, CSS3 e Vanilla JavaScript.
A lógica de negócio e a simulação de dados MUST permanecer isoladas em funções claras de
JavaScript e NUNCA ser misturadas à marcação HTML. Cada bloco de código MUST conter comentários
em Português do Brasil que expliquem sua funcionalidade, com atenção especial à renderização 3D
do Mapbox. Essa separação reduz ambiguidade, facilita manutenção e torna o comportamento
demonstrado auditável.

### II. Arquitetura Client-Side Estática

O sistema MUST ser um Mockup Funcional client-side estático, sem dependência de back-end.
`index.html` MUST concentrar a autenticação e `dashboard.html` MUST concentrar o painel tático
principal, mantendo os arquivos isolados por responsabilidade. Bibliotecas externas MUST ser
consumidas exclusivamente via CDN; para mapas, a dependência permitida é Mapbox GL JS. A
arquitetura deve permitir execução direta sem instalação de pacotes.

### III. Redenção, Vigilância Ativa e Responsabilização

O conceito central MUST ser a Redenção: a intersecção entre a revelação da verdade, por meio de
rastreamento e quebra de sigilo, e a penitência, por meio da responsabilização legal por crimes
cibernéticos e infrações à LGPD. O usuário MUST acessar a visão tática da cidade somente após a
validação de uma credencial governamental na tela inicial. Toda informação plotada no mapa ou
exibida no terminal MUST transmitir Vigilância Ativa e inteligência federal, usando contextos
coerentes como Mandados, Quebra de IP e ALPR.

### IV. Interface Cyber Forensic de Nível Governamental

O visual MUST adotar Dark Mode / Cyber Forensic de nível militar e governamental. O `body` MUST
usar `overflow: hidden`, sem barras de rolagem globais, e o mapa MUST preencher 100% da viewport.
A tipografia MUST ser monoespaçada, usando Courier New, Roboto Mono ou Consolas. A paleta MUST
usar fundo preto sólido (`#000000`), cinza chumbo (`#0a0a0a`), Verde Neon (`#00ff00`) para
textos normais e Vermelho Alerta (`#ff3333`) para alertas críticos e alvos.

### V. Teste Manual e Evidência Visual

Toda funcionalidade visual demonstrada MUST possuir um teste manual de layout documentado, cobrindo
no mínimo autenticação, transição para o painel, mapa em viewport completa, terminal e estados de
alerta. O projeto MUST NOT gerar arquivos de testes automatizados, incluindo Jest e Mocha. A
validação manual deve registrar o resultado e qualquer desvio observável antes da entrega.

## Restrições Técnicas e de Produto

Todos os textos do projeto, incluindo documentação, arquivos `.md`, requisitos, comentários,
alertas do painel, regras de negócio e saídas de comandos do Spec Kit, MUST estar em Português
do Brasil. Nomes de tecnologias, bibliotecas e comandos, como JavaScript, Mapbox GL JS e
`/speckit-plan`, são a única exceção e MUST permanecer em sua forma original.

O painel é uma simulação funcional e MUST deixar claro, por seu contexto de uso e dados
controlados, que não substitui uma operação real. Credenciais, eventos, alvos e coordenadas
simulados MUST ser mantidos em funções de negócio identificáveis, sem exigir serviço externo além
do CDN autorizado.

## Processo de Desenvolvimento e Qualidade

Cada mudança MUST ser revisada contra todos os princípios desta constituição antes da entrega.
Uma implementação só é considerada concluída quando a estrutura semântica, a separação entre
apresentação e simulação, o fluxo de autenticação, a composição visual e o teste manual de layout
estão verificáveis. Alterações que introduzam uma nova biblioteca, um novo fluxo ou um novo estado
visual MUST atualizar a documentação correspondente e seu teste manual.

## Governance

Esta constituição prevalece sobre práticas conflitantes do projeto. Qualquer alteração MUST
documentar o princípio afetado, a motivação, o impacto e a forma de validação. Uma emenda MUST
preservar as regras permanentes de idioma, arquitetura, fluxo de autenticação, identidade visual
e testes, salvo se a própria constituição for explicitamente alterada.

O versionamento segue SemVer: MAJOR para remoção ou redefinição incompatível de princípio, MINOR
para novo princípio ou expansão normativa relevante e PATCH para esclarecimentos sem mudança de
obrigações. A revisão de conformidade MUST ocorrer antes de cada entrega funcional e sempre que
uma ferramenta, biblioteca ou fluxo de tela for alterado.

**Versão**: 1.0.0 | **Ratificada**: TODO(RATIFICATION_DATE): confirmar data histórica | **Última
alteração**: 2026-10-01
