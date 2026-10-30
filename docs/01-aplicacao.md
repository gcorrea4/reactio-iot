# 1. Onde IoT e Redes se aplicam ao REACTIO

## O projeto

O REACTIO é um app educativo sobre tecnologia nuclear, feito em parceria com a Marinha do Brasil / CTMSP (AMAZUL). Ele funciona como uma trilha de microlições: o participante recebe uma afirmação, responde **Verdadeiro**, **Falso** ou **Depende do contexto** e, em seguida, recebe a explicação e a fonte.

Uma API Java (Spring) fornece as afirmações e avalia as respostas. Um app Flutter mostra a trilha e os desafios. Os temas iniciais são "Radiação no cotidiano" e "Aplicações no cotidiano".

## A necessidade atendida

O app só alcança quem decide instalá-lo. Em uma escola ou em um evento, muitas pessoas passam pelo tema sem esse interesse prévio, e nem todas têm um celular disponível ou querem instalar algo para responder a uma pergunta.

A proposta leva a mesma trilha para o espaço físico: a pessoa se aproxima, responde a uma afirmação em poucos toques e vai embora sem cadastro.

## A proposta: totem educativo conectado

O totem é um ponto educativo instalado em uma escola ou em um evento. Ele consome o mesmo conteúdo do app, pela rede, a partir da API do REACTIO.

**O que o totem faz:**

1. Percebe que alguém se aproximou, por meio de um sensor de presença, e ativa a tela.
2. Mostra uma afirmação em texto.
3. Recebe a resposta por três botões físicos: VERDADEIRO, FALSO e DEPENDE.
4. Mostra o resultado, a explicação e a fonte na tela, com um reforço de LED ou buzzer.
5. Envia a resposta à API de forma anônima, para atualizar as contagens agregadas.

## Onde cada área entra

| Área | Papel na proposta |
|---|---|
| **IoT** | Dispositivo físico que percebe o ambiente (presença), recebe entradas (botões) e executa ações (tela, LED, buzzer). |
| **Redes** | Conexão Wi-Fi do totem com a API por HTTPS, para receber o conteúdo e enviar as respostas. |

## Como contribui para o projeto

- **Alcance:** leva a trilha a quem não instalaria o app.
- **Reuso:** usa a mesma API e o mesmo conteúdo revisado do app, sem uma segunda base de afirmações.
- **Retorno para a equipe:** as contagens por afirmação mostram quais afirmações geram mais dúvida, o que apoia a avaliação da trilha.
- **Privacidade:** não há câmera, cadastro nem identificação, o que é adequado a um ambiente escolar.

## Recorte

Esta entrega é conceitual: explica como IoT e Redes se aplicariam, sem construir o sistema. Sensores de radiação e IA ficam fora do recorte, porque o objetivo do totem é educar e nenhuma etapa do fluxo precisa medir radiação ou gerar conteúdo.
