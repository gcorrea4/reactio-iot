# 5. Limitações e considerações de privacidade

Esta é uma proposta conceitual e nada foi testado em campo. Os limites e tempos citados abaixo precisariam ser definidos em testes com um protótipo.

## Resumo

| Limitação | Risco | Como a proposta lida |
|---|---|---|
| Conexão | Wi-Fi cai ou bloqueia o totem | Modo offline com conteúdo em cache |
| Latência | Espera depois de apertar o botão | Mensagem em texto e uso do cache se a API demorar |
| Segurança | Token roubado ou contagem adulterada | HTTPS, token por dispositivo e limite de envios |
| Energia | Totem desligado ou falta de luz | Dados gravados em memória não volátil e retomada automática |
| Privacidade | Exposição de dados de participantes | Sem câmera e sem identificação |

## Conexão

**Queda de Wi-Fi.** O totem não pode parar quando a rede cair. Por isso, ele funciona em modo offline:

- Baixa um pacote com afirmações, classificação, explicação e fonte quando há conexão.
- Sem conexão, mostra as afirmações do cache e avalia as respostas localmente.
- Acumula as contagens no próprio totem e as envia em lote quando a conexão volta. O `loteId` evita a contagem em dobro.
- Mostra em texto que está em modo offline, sem atrapalhar a resposta.

**O que o modo offline não resolve:**

- O painel fica desatualizado até a conexão voltar.
- Um conteúdo corrigido na API só chega ao totem na sincronização seguinte. O pacote precisa ter uma versão, para o totem saber que está desatualizado.
- Se o totem ligar pela primeira vez sem rede, não haverá cache. O pacote precisa ser baixado antes da instalação.
- Dependendo do modelo, o Raspberry Pi pode não manter o relógio sem energia ou sem rede. A data de uma contagem offline pode ficar errada, o que afetaria o painel do dia.

**Redes restritas.** Redes de escolas e eventos podem exigir login em portal, bloquear dispositivos desconhecidos ou limitar o tráfego. A rede precisa ser combinada com o responsável pelo local antes da instalação.

## Latência

Pela internet, o tempo de resposta da API varia com o Wi-Fi, a lotação da rede e a carga do servidor. Para que a pessoa não fique sem retorno:

- A tela confirma em texto, logo após o toque, que a resposta foi recebida.
- Se a API passar de um tempo limite, o totem usa o cache e deixa a contagem para o envio posterior.

O fluxo não depende de tempo real, porque ninguém compete por tempo e a trilha não tem cronômetro. O painel também não precisa ser instantâneo.

## Segurança

**Medidas previstas:** HTTPS em toda a comunicação, token próprio de cada totem, permissão mínima e revogação individual.

**Riscos que permanecem:**

- **Acesso físico:** quem abrir o totem pode copiar o token. O Raspberry Pi precisa ficar em uma estrutura fechada, e o token, poder ser revogado a qualquer momento.
- **Contagens infladas:** apertos repetidos ou envios falsos distorcem os totais. O totem ignora repetições acidentais, aceita uma resposta por afirmação exibida, e a API limita a quantidade de envios por token.
- **Painel:** o acesso precisa de autenticação própria, separada do token dos totens.
- **Atualizações:** o sistema do Raspberry Pi precisa receber atualizações de segurança, o que gera trabalho de manutenção.

## Energia

- O totem precisa de uma tomada próxima, o que limita os locais de instalação. Bateria não faz parte desta proposta, porque a tela e o Raspberry Pi ficam em uso durante todo o evento ou horário escolar.
- A tela fica apagada enquanto não há ninguém por perto, graças ao sensor PIR, o que reduz o consumo e o desgaste. O consumo real não foi medido.
- Uma queda de energia pode corromper o armazenamento ou perder as contagens ainda não gravadas. As contagens devem ser gravadas logo após cada resposta, e o programa deve iniciar sozinho quando o totem ligar.

## Privacidade

Como o totem pode ficar em escolas, onde há menores de idade, a proposta segue a minimização de dados: coletar só o necessário para a finalidade.

- **Sem câmera nem reconhecimento facial:** o sensor PIR só detecta movimento e não capta imagem.
- **Sem microfone.**
- **Sem identificação:** não há login, nome, RM, e-mail ou identificador de sessão.
- **Sem horário exato:** as contagens são guardadas por dia.
- **Presença fica no totem:** o sinal do sensor não é enviado nem guardado.
- **Tela limpa:** ao fim da sessão, a tela apaga, e a pessoa seguinte não vê o que a anterior fez.

**Cuidado que permanece:** em dias com pouquíssimas respostas, um total pequeno pode sugerir quem respondeu se alguém observou o totem. O painel mostra só os totais por afirmação, sem horário, o que reduz esse risco. A instalação em uma escola ainda precisa de autorização da instituição.

## Limitações da abordagem

- **PIR:** sensores de presença podem disparar com pessoas apenas de passagem e, em locais lotados, a tela pode ficar sempre ativa. O disparo falso só acende a tela e não gera contagem.
- **Qualidade dos dados:** sem identificação, não é possível saber se a mesma pessoa respondeu várias vezes. As contagens indicam tendências e não medem aprendizado.
- **Acessibilidade:** a altura da tela e dos botões, o contraste e o uso por pessoas com deficiência visual ou motora precisam ser avaliados em um protótipo. O texto e os botões rotulados ajudam, mas não resolvem tudo.
- **Custo:** a manutenção e o custo por totem não foram estimados nesta entrega.
