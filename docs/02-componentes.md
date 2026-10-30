# 2. Componentes, sensores e funções

Esta lista descreve a função de cada peça na proposta. Nenhuma peça foi comprada ou testada, e modelos e custos não foram definidos nesta etapa.

## No totem

| Componente | Tipo | O que mede ou executa | Onde fica |
|---|---|---|---|
| Raspberry Pi | Computador de placa única | Roda o programa do totem (Python ou Node.js), lê o sensor e os botões, controla tela, LED e buzzer, conversa com a API e guarda o cache de conteúdo | Dentro da estrutura do totem, protegido do acesso do público |
| Sensor PIR | Sensor de presença | Detecta movimento de uma pessoa próxima, sem captar imagem. Ativa a tela e inicia a sessão | Na frente do totem, voltado para a área de aproximação |
| Display touch ou monitor | Atuador (saída) | Mostra a afirmação, o resultado, a explicação e a fonte em texto | Na frente do totem, em altura de leitura |
| 3 botões físicos | Entrada | Registram a resposta: VERDADEIRO, FALSO ou DEPENDE | No painel frontal, abaixo da tela e ao alcance das mãos |
| Rótulos em texto | Identificação | Dizem a função de cada botão, no próprio botão e na lateral, para não depender de cor | Em cada botão e ao lado dele |
| LED ou buzzer | Atuador (saída) | Reforça que a resposta foi registrada. Sempre acompanhado de texto na tela | Perto dos botões |

## Fora do totem

| Componente | Função | Onde fica |
|---|---|---|
| Rede Wi-Fi | Liga o totem à internet | Infraestrutura da escola ou do evento |
| API Java (Spring) | Fornece as afirmações, avalia as respostas e registra as contagens | Servidor do grupo |
| Banco de dados do grupo | Guarda o conteúdo e as contagens agregadas | Servidor do grupo |
| Painel agregado | Mostra as contagens por tema e por afirmação | Página acessada pela equipe, por professores e por organizadores |

## Onde o totem pode ser instalado

- **Escolas:** corredores, pátios cobertos ou bibliotecas, perto de uma tomada e com sinal de Wi-Fi.
- **Eventos:** estandes e áreas de circulação de feiras de ciência e tecnologia.

O local precisa estar protegido de chuva e ter espaço livre à frente, para que o sensor perceba a aproximação e a pessoa consiga ler e responder com calma.

## Decisões de projeto

- **Sensor PIR em vez de câmera:** o sensor só indica que houve movimento. Ele atende ao objetivo de acordar o totem sem captar imagem de ninguém.
- **Botões físicos:** dão uma resposta clara ao toque, são fáceis de entender à distância e funcionam com um monitor comum, sem tela sensível ao toque.
- **Sem depender de cor ou som:** o texto na tela é sempre a informação principal. O LED e o buzzer só reforçam, e o totem continua compreensível se o som estiver desligado.
- **Botão também inicia a sessão:** se o sensor não perceber a pessoa, apertar qualquer botão ativa a tela, sem contar como resposta.
- **Sem sensor de radiação:** o totem educa sobre o tema e não mede radiação, então esse sensor não teria função no fluxo.
