# REACTIO - proposta de IoT e Redes

Proposta conceitual da disciplina de IoT / IoB / IA Generativa (Sprint 1), Challenge FIAP 2026. Este repositório contém apenas documentação: nenhum dispositivo foi montado ou programado.

## Integrantes

| Nome | RM |
|---|---|
| Kayque | 567980 |
| Eric | 567398 |
| Gabriel | 567903 |

**Parceiro:** Marinha do Brasil / CTMSP (AMAZUL), Challenge FIAP 2026.

## Resumo da proposta

Um totem educativo em escolas e eventos leva a trilha de microlições do REACTIO a quem não instalaria o app.
Um sensor de presença ativa a tela, e a pessoa responde a afirmações sobre tecnologia nuclear por três botões físicos.
O totem recebe o conteúdo da API Java pela rede e envia apenas respostas anônimas, somadas em contagens agregadas.

## Tecnologias previstas

- Raspberry Pi
- Sensor PIR
- Botões físicos
- Display (touch ou monitor)
- LED ou buzzer
- Python ou Node.js no dispositivo
- Wi-Fi
- HTTP/REST sobre HTTPS, com MQTT como alternativa avaliada
- API Java (Spring)

Nada disso foi implementado nesta entrega, e não há sensor de radiação, câmera nem IA na proposta.

## Links

- **Vídeo no YouTube (não listado):** https://youtu.be/5IxaSjNf3q0
- **Repositório:** https://github.com/gcorrea4/reactio-iot

## Como ler a documentação

Leia os arquivos nesta ordem:

| Ordem | Arquivo | Conteúdo |
|---|---|---|
| 1 | [docs/01-aplicacao.md](docs/01-aplicacao.md) | O que o totem faz, onde IoT e Redes se aplicam e a necessidade atendida |
| 2 | [docs/02-componentes.md](docs/02-componentes.md) | Sensores e dispositivos, função de cada um e onde ficam |
| 3 | [docs/03-comunicacao.md](docs/03-comunicacao.md) | Rede, protocolo, formato das mensagens e segurança |
| 4 | [docs/04-dados-e-resposta.md](docs/04-dados-e-resposta.md) | Destino dos dados, processamento, quem usa e benefício |
| 5 | [diagramas/fluxograma.md](diagramas/fluxograma.md) | Fluxograma em Mermaid, do dado à ação |
| 6 | [docs/05-limitacoes.md](docs/05-limitacoes.md) | Conexão, latência, segurança, energia e privacidade |

## Requisitos da entrega

| Item | Onde |
|---|---|
| Descrição do totem e contribuição | [docs/01-aplicacao.md](docs/01-aplicacao.md) |
| Componentes | [docs/02-componentes.md](docs/02-componentes.md) |
| Comunicação e exemplo de payload | [docs/03-comunicacao.md](docs/03-comunicacao.md) |
| Fluxograma | [diagramas/fluxograma.md](diagramas/fluxograma.md) |
| Destino dos dados e quem usa | [docs/04-dados-e-resposta.md](docs/04-dados-e-resposta.md) |
| Resposta ou benefício | [docs/04-dados-e-resposta.md](docs/04-dados-e-resposta.md) |
| Limitações | [docs/05-limitacoes.md](docs/05-limitacoes.md) |

## Estrutura

```text
reactio-iot/
├── README.md
├── docs/
│   ├── 01-aplicacao.md
│   ├── 02-componentes.md
│   ├── 03-comunicacao.md
│   ├── 04-dados-e-resposta.md
│   └── 05-limitacoes.md
├── diagramas/
│   └── fluxograma.md
└── .gitignore
```
