# 4. Destino, processamento e uso dos dados

## Quais dados existem

| Dado | Origem | Sai do totem? | Destino |
|---|---|---|---|
| Presença (movimento) | Sensor PIR | Não | Usado na hora para ativar a tela, sem ser guardado |
| Resposta (tema, afirmação e opção) | Botões | Sim, de forma anônima | API Java, depois o banco do grupo |
| Conteúdo (afirmação, classificação, explicação e fonte) | API Java | Vem da API para o totem | Tela e cache local |

O totem não coleta nome, RM, imagem, voz nem identificador do aparelho do participante.

## Para onde os dados vão

```text
Totem ──> API Java (Spring) ──> Banco do grupo ──> Painel agregado
```

1. **API Java:** recebe a resposta, valida o token do dispositivo e avalia a resposta.
2. **Banco do grupo:** guarda apenas contagens agregadas. A resposta individual não é armazenada.
3. **Painel agregado:** lê as contagens e as apresenta por tema e por afirmação.

## Processamento

**No totem:**

- Decide quando ativar a tela e quando encerrar a sessão por inatividade.
- Lê o botão pressionado e ignora repetições acidentais de um mesmo toque.
- Monta o payload JSON e o envia à API.
- Sem conexão, usa o conteúdo do cache para avaliar a resposta e acumula as contagens para enviar depois.

**Na API:**

- Compara a resposta com a classificação cadastrada para a afirmação.
- Devolve o resultado, a explicação e a fonte.
- Soma 1 ao contador correspondente.

**Modelo das contagens.** Cada linha é um total, e não o registro de uma pessoa:

| data | tema | afirmacaoId | resposta | quantidade |
|---|---|---|---|---|
| `<dia>` | radiacao | 3 | VERDADEIRO | `<total>` |
| `<dia>` | radiacao | 3 | FALSO | `<total>` |
| `<dia>` | radiacao | 3 | DEPENDE | `<total>` |

A data permite atualizar o painel de contagem do dia. O horário exato não é guardado, para que não seja possível ligar uma resposta a quem estava no local naquele momento.

## Quem usa e para quê

| Público | O que vê | Para que usa |
|---|---|---|
| Participante | Resultado, explicação e fonte na tela do totem | Aprender sobre o tema na hora |
| Equipe de conteúdo | Contagens por afirmação | Identificar afirmações que geram mais dúvida e revisar textos pouco claros |
| Professores | Contagens por tema e por afirmação | Escolher assuntos para retomar em aula |
| Organizadores do evento | Contagem do dia | Acompanhar o uso do ponto educativo |

## Resposta e benefício

**Ação imediata no totem:**

- A tela mostra o resultado, a classificação correta, a explicação e a fonte.
- O LED ou o buzzer reforça o registro da resposta, sempre com texto na tela.
- Errar leva à mesma explicação de quem acertou, sem penalidade.

**Ação no sistema:**

- O painel de contagem do dia é atualizado.

**Benefício para o projeto:**

- Apoia a avaliação da trilha, com indicação de quais afirmações geram mais erros ou mais respostas "Depende".
- Leva o conteúdo a pessoas que não instalariam o app.
- Gera informação útil para a equipe sem coletar dados pessoais.

## Como ler as contagens

As contagens indicam tendências e não medem aprendizado individual. Uma mesma pessoa pode responder várias vezes, e o sistema não tem como saber disso, porque não há identificação. Essa limitação é aceita em troca da privacidade.

Nesta proposta, as contagens também não são separadas por totem, porque o recorte registra apenas tema e afirmação. Se professores e organizadores precisarem ver só o próprio local, a separação por ponto educativo poderá ser avaliada depois, ainda sem nenhum dado de participante.
