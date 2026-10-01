# Contratos de Interface: Visão Tática Redenção

**Data**: 2026-10-01

Este documento descreve os contratos observáveis da interface entre o agente e as duas telas.
Não há API pública nem contrato de back-end.

## Contrato da Tela de Acesso (`index.html`)

### Entradas

- Campo rotulado exatamente como `Credencial de Agente/Perito`.
- Campo rotulado exatamente como `Chave de Acesso Governamental`.
- Ação única de validação do acesso.

### Saídas

- Sucesso: transição para `dashboard.html`.
- Campo ausente: alerta em Português do Brasil e permanência na tela de acesso.
- Acesso não autorizado: painel e dados operacionais não são apresentados.

### Restrições observáveis

- Não exibir `Esqueci minha senha`.
- Não exibir `Cadastrar`.
- Usar composição de terminal, tipografia monoespaçada e bordas verde neon.

## Contrato do Painel (`dashboard.html`)

### Estado inicial

- A visão espacial ocupa toda a viewport e permanece atrás dos elementos sobrepostos.
- O centro inicial é Guanambi, Bahia: latitude `-14.2263`, longitude `-42.7816`.
- A câmera inicia com inclinação de 60 graus, direção `-17.6` e aproximação `15.5`.
- A camada urbana apresenta volumetria 3D dos prédios.

### Contrato de alvo

- Cada alvo visível é identificado por marcador vermelho.
- Selecionar um marcador abre um popup único.
- O popup exibe IP, status investigativo e infração.
- Fechar o popup remove os dados sigilosos da superfície da visão.

### Contrato de vazamento e dossiê OSINT

- Um novo marcador vermelho deve surgir a cada 8 segundos dentro de 2 km do centro operacional.
- O marcador gerado deve abrir um dossiê com foto remota, nome fictício, IP, status `MANDADO ATIVO`
  e infração à LGPD.
- O dossiê deve conter um iframe de Google Maps Embed com a coordenada do alvo, visão de satélite
  e interação de mouse permitida.

### Contrato de patrulha ALPR

- Três pontos azuis devem representar veículos nas rotas GeoJSON predefinidas.
- As rotas são `Feature<LineString>` e seus pontos devem ser calculados por Turf.js.
- A camada de veículos deve ser atualizada continuamente e emitir uma leitura ALPR ao concluir
  cada ciclo.

### Contrato do terminal IoT

- O terminal fica sobreposto à direita do mapa.
- Uma linha nova aparece automaticamente a cada 3500 ms.
- O terminal suporta os tipos ALPR, Rastreamento IP e Reconhecimento Facial.
- ALPR OK usa indicação verde; Match Facial e IP Suspeito usam indicação vermelha.
- A inserção de linha leva a rolagem para o evento mais recente.

## Contrato de linguagem

Todos os rótulos, mensagens, popups, logs e alertas são em Português do Brasil, exceto nomes de
tecnologias, bibliotecas e comandos. Dados exibidos são fictícios e devem manter linguagem de
Vigilância Ativa sem sugerir acesso a investigações reais.
