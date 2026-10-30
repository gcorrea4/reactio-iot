# 3. Comunicação entre dispositivos e API

## Visão geral

```text
Sensor PIR e botões ──(sinal digital, GPIO)──> Raspberry Pi ──(Wi-Fi + HTTPS)──> API Java (Spring) ──> Banco do grupo
Tela, LED e buzzer <──(saída local)─────────── Raspberry Pi <──(JSON)─────────── API Java (Spring)
```

Há dois trechos com características diferentes:

- **Local, dentro do totem:** o sensor e os botões enviam sinais digitais ao Raspberry Pi pelos pinos de GPIO. O Raspberry Pi aciona a tela, o LED e o buzzer. Nada disso passa pela rede.
- **Em rede, do totem até a API:** o Raspberry Pi usa o Wi-Fi do local para chegar à API pela internet.

## Rede

O totem se conecta ao Wi-Fi da escola ou do evento. As credenciais da rede ficam apenas no próprio dispositivo e nunca neste repositório.

## Protocolo escolhido: HTTP REST sobre HTTPS

| Critério | HTTP REST | MQTT com broker |
|---|---|---|
| Padrão de uso | Pedido e resposta: o totem envia a resposta e espera o resultado | Publicação e assinatura, voltado a mensagens contínuas |
| Encaixe no projeto | A API Java (Spring) já é o ponto central do REACTIO | Exige um broker e uma ponte até a API |
| Componentes novos | Nenhum | Broker para hospedar e manter |
| Quando faria sentido | Poucos totens e mensagens só quando alguém responde | Muitos totens ou comandos enviados da central para eles em tempo real |

**Decisão:** usar HTTP REST. O totem só troca mensagens quando alguém interage, e cada resposta precisa de um retorno imediato, o que combina com o modelo de pedido e resposta. O MQTT fica como alternativa, caso o projeto passe a ter muitos totens ou precise enviar comandos a eles em tempo real.

## Rotas propostas

Estas rotas são uma proposta para a API do grupo e ainda não foram implementadas.

| Método e rota | Função |
|---|---|
| `GET /api/totem/pacote` | Baixa o pacote de conteúdo para o cache: afirmações, classificação, explicação e fonte |
| `GET /api/afirmacoes/proxima?tema=radiacao` | Busca a próxima afirmação de um tema |
| `POST /api/respostas` | Envia uma resposta e recebe o resultado |
| `POST /api/respostas/lote` | Envia as contagens acumuladas enquanto o totem estava sem conexão |

## Formato das mensagens

As mensagens usam JSON. Os valores abaixo são ilustrativos.

**Envio de uma resposta**, do totem para a API:

```http
POST /api/respostas HTTP/1.1
Host: api.reactio.example
Authorization: Bearer <TOKEN_DO_DISPOSITIVO>
Content-Type: application/json
```

```json
{"tema":"radiacao","afirmacaoId":3,"resposta":"DEPENDE"}
```

| Campo | Tipo | Valores |
|---|---|---|
| `tema` | texto | `radiacao` ou `aplicacoes` |
| `afirmacaoId` | número | Identificador da afirmação |
| `resposta` | texto | `VERDADEIRO`, `FALSO` ou `DEPENDE` |

O payload não tem nome, RM, e-mail, identificador de sessão, imagem nem horário exato. O token identifica o dispositivo, e não a pessoa que respondeu.

**Retorno da API** para o totem:

```json
{
  "resultado": "CORRETO",
  "classificacaoCorreta": "DEPENDE",
  "explicacao": "<texto da explicação cadastrada para a afirmação>",
  "fonte": "<nome e link da fonte cadastrada para a afirmação>"
}
```

**Envio em lote**, depois de um período sem conexão. Cada item soma as respostas iguais de um mesmo dia:

```json
{
  "loteId": "<identificador gerado pelo totem para este envio>",
  "contagens": [
    {"data":"<AAAA-MM-DD>","tema":"radiacao","afirmacaoId":3,"resposta":"DEPENDE","quantidade":4}
  ]
}
```

O `loteId` evita a contagem em dobro: se o totem reenviar um lote porque não recebeu a confirmação, a API reconhece o identificador e não soma de novo. Ele identifica o envio, e não uma pessoa.

## Segurança na comunicação

- **HTTPS:** toda a comunicação com a API é criptografada, inclusive em redes abertas.
- **Token por dispositivo:** cada totem tem um token próprio, enviado no cabeçalho `Authorization`. Se um totem for perdido ou violado, basta revogar o token dele, sem afetar os outros.
- **Permissão mínima:** o token só permite baixar conteúdo e enviar respostas. Ele não dá acesso ao painel nem à edição de afirmações.
- **Fora do repositório:** tokens, chaves, senhas de Wi-Fi e IPs internos nunca são versionados. O endereço `api.reactio.example` é apenas um exemplo.

Os riscos que permanecem estão em [05-limitacoes.md](05-limitacoes.md).
