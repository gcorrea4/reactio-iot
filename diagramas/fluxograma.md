# Fluxograma: do dado à ação

O diagrama mostra o caminho dos dados desde a coleta, no sensor e nos botões, até o resultado na tela e a atualização do painel.

```mermaid
flowchart TD
    A["Pessoa se aproxima do totem"] --> B["Sensor PIR detecta movimento ou um botão é apertado"]
    B --> C["Raspberry Pi ativa a tela e inicia a sessão"]
    C --> D{"Há conexão com a API?"}

    D -- "Sim" --> E["Busca a afirmação na API por HTTPS"]
    D -- "Não" --> F["Busca a afirmação no cache local"]
    E --> G["Tela mostra a afirmação em texto"]
    F --> G

    G --> H{"Botão pressionado antes do tempo limite?"}
    H -- "Não" --> I["Encerra a sessão e apaga a tela"]
    H -- "Sim" --> J["Raspberry Pi registra VERDADEIRO, FALSO ou DEPENDE"]
    J --> K{"Há conexão com a API?"}

    K -- "Sim" --> L["Envia o JSON anônimo com token do dispositivo"]
    L --> M["API Java avalia a resposta"]
    M --> N["Banco do grupo soma a contagem agregada"]
    N --> O["Painel agregado é atualizado"]
    O --> P["Equipe de conteúdo, professores e organizadores usam os dados"]
    M --> Q["API devolve resultado, explicação e fonte"]

    K -- "Não" --> R["Avalia a resposta com o conteúdo do cache"]
    R --> S["Acumula a contagem no totem"]
    S --> T["Conexão volta: envia o lote à API"]
    T --> N

    Q --> U["Tela mostra resultado, explicação e fonte"]
    R --> U
    U --> V["LED ou buzzer reforça, sempre com texto na tela"]
    V --> W{"Pessoa continua interagindo?"}
    W -- "Sim" --> D
    W -- "Não" --> I
```

## Como ler

| Etapa | Blocos | O que acontece |
|---|---|---|
| Coleta | A a C, H, J | O sensor percebe a presença e os botões captam a resposta. A presença não sai do totem |
| Conteúdo | D a G | A afirmação vem da API ou, sem conexão, do cache |
| Comunicação | K, L, Q | O totem envia o JSON anônimo e recebe o retorno da API |
| Modo offline | R a T | O totem avalia pelo cache e envia as contagens quando a conexão volta |
| Processamento e destino | M a P | A API avalia, o banco soma a contagem e o painel mostra os totais |
| Ação | U, V | O participante vê o resultado e a explicação, com a fonte |
| Encerramento | W, I | Sem nova interação, a sessão termina |

Se ninguém apertar um botão ou continuar interagindo, a sessão termina e a tela apaga. Assim, a pessoa seguinte não vê o que a anterior estava fazendo.

## Exemplo de mensagem do bloco L

```json
{"tema":"radiacao","afirmacaoId":3,"resposta":"DEPENDE"}
```
