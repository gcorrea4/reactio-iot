# Roteiro do vídeo de 5 minutos

**Duração:** cerca de 5 minutos. **Formato:** slides e fluxograma na tela, narrados pelos integrantes. **Publicação:** YouTube, como não listado.

A divisão de falas é uma sugestão. Como a entrega é conceitual, o vídeo mostra a proposta e não um protótipo: não apresente o totem como se já estivesse construído.

## Antes de gravar

- [ ] Prepare um slide por bloco, usando as tabelas de [02-componentes.md](02-componentes.md) e [03-comunicacao.md](03-comunicacao.md).
- [ ] Abra o fluxograma de [diagramas/fluxograma.md](../diagramas/fluxograma.md) no GitHub ou no mermaid.live, com zoom suficiente para a leitura.
- [ ] Faça um ensaio cronometrado. Se passar de 5 minutos, encurte as falas.
- [ ] Depois de publicar, coloque o link no README e no `entrega.txt`.

## Sequência

### 1. Problema: 0:00 a 0:45 (Kayque)

**Tela:** título do projeto, integrantes e parceiro.

> "Olá, nós somos Kayque, Eric e Gabriel, e este é o REACTIO, do Challenge FIAP 2026, com a Marinha do Brasil, por meio do CTMSP e da AMAZUL. A tecnologia nuclear é pouco compreendida pela população, e isso abre espaço para dúvidas e ideias erradas. O desafio é aproximar as pessoas desse tema com informação clara e com fonte."

### 2. Solução: 0:45 a 1:30 (Kayque)

**Tela:** exemplo de afirmação com as três alternativas e a fonte.

> "O REACTIO é uma trilha de microlições. A pessoa recebe uma afirmação, como 'Todos os seres vivos estão expostos a alguma radiação', e responde Verdadeiro, Falso ou Depende do contexto. Depois, recebe a explicação e a fonte. Neste exemplo, a resposta é Verdadeiro, e a fonte é a NRC, a agência reguladora nuclear dos Estados Unidos. Uma API Java fornece as afirmações e avalia as respostas, e um app Flutter mostra a trilha. Mas um app só alcança quem decide instalá-lo."

### 3. Aplicação de IoT e Redes: 1:30 a 3:30 (Eric)

**Tela:** desenho simples do totem (1:30 a 2:30); depois, o exemplo de JSON e a comparação entre HTTP e MQTT (2:30 a 3:30).

> "É aí que entram IoT e Redes. Nossa proposta é um totem educativo para escolas e eventos, que leva a mesma trilha para o espaço físico, sem instalação e sem cadastro."

> "O centro do totem é um Raspberry Pi conectado ao Wi-Fi. Um sensor PIR detecta o movimento de quem se aproxima, ativa a tela e inicia a sessão. Ele só percebe movimento: não há câmera. A tela mostra a afirmação e o resultado em texto. Três botões físicos recebem a resposta: Verdadeiro, Falso e Depende. Cada um tem um rótulo em texto, para não depender de cor. Um LED ou buzzer reforça o registro da resposta, sempre com texto na tela."

> "Na comunicação, o Raspberry Pi usa HTTP REST sobre HTTPS para falar com a API Java. Escolhemos REST em vez de MQTT porque cada resposta pede um retorno imediato, e a API já é o ponto central do projeto. O MQTT exigiria um broker e só compensaria com muitos totens ou comandos em tempo real. A mensagem é um JSON com o tema, o identificador da afirmação e a resposta. Não há nome nem dado do participante. O token que acompanha a mensagem identifica o totem, e não a pessoa. Se o Wi-Fi cair, o totem segue funcionando com o conteúdo em cache e envia as contagens quando a conexão voltar."

### 4. Fluxograma: 3:30 a 4:30 (Gabriel)

**Tela:** fluxograma. Aponte cada etapa enquanto fala.

> "Vamos percorrer o caminho do dado. A pessoa se aproxima, e o sensor faz o Raspberry Pi ativar a tela. O totem verifica a conexão e busca a afirmação na API ou no cache. A pessoa aperta um botão. Com conexão, o totem envia o JSON anônimo, a API avalia a resposta e devolve o resultado, a explicação e a fonte, que aparecem na tela. Ao mesmo tempo, o banco do grupo soma a contagem agregada, e o painel é atualizado para a equipe de conteúdo, os professores e os organizadores. Sem conexão, o totem avalia pelo cache, acumula a contagem e envia o lote depois. Quando a pessoa sai, a sessão termina e a tela apaga."

### 5. Benefício e encerramento: 4:30 a 5:00 (Gabriel)

**Tela:** lista de benefícios e principais limitações.

> "O participante aprende na hora, e a equipe descobre quais afirmações geram mais dúvida, sem coletar dados pessoais. A proposta ainda tem limites de conexão, energia e segurança, descritos na nossa documentação. Este foi o REACTIO. Obrigado!"

## Cobertura do enunciado

| Item | Bloco |
|---|---|
| Descrição do totem e contribuição | 3 |
| Componentes, função e local | 3 |
| Comunicação e payload | 3 |
| Fluxograma | 4 |
| Destino dos dados e quem usa | 4 |
| Resposta ou benefício | 4 e 5 |
| Limitações | 3 (Wi-Fi) e 5 |

## Fonte da afirmação usada no exemplo

- "Todos os seres vivos estão expostos a alguma radiação." Classificação: Verdadeiro. Fonte: [NRC, Sources of Radiation](https://www.nrc.gov/about-nrc/radiation/around-us/sources.html).
