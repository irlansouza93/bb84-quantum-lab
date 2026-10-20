# bb84-quantum-lab

> **BB84, o Token do Satélite** — um laboratório interativo para entender, na prática, como a física quântica protege informações.

Em uma missão de três pessoas, você envia uma chave secreta da Estação Antártica para um satélite enquanto um espião tenta interceptá-la. A segurança não vem de uma senha mais difícil: vem das leis da mecânica quântica. Cada fóton carrega uma base e um bit; qualquer tentativa de espionagem deixa erros detectáveis.

A apresentação conta a origem do protocolo — proposto em **1984** por Charles Bennett e Gilles Brassard — e convida você a testar a ideia na prática. O botão **Conhecer a história** abre uma wiki curta sobre o BB84, com link para o [verbete da Wikipédia](https://pt.wikipedia.org/wiki/BB84).

O projeto é um **simulador educacional do protocolo BB84**, feito em um único arquivo HTML, sem dependências e sem servidor. Roda no navegador, inclusive em celular, com temas claro e escuro.

---

## A missão

1. O **Emissor** prepara 10 fótons com bases e bits sorteados.
2. O **Espião** intercepta os fótons e tenta medi-los sem ser notado.
3. O **Receptor** mede o que chega e guarda apenas os bits em que sua base coincide com a do Emissor.
4. No fim, os dois lados legítimos comparam uma pequena amostra. Se a taxa de erro passar de **11%**, a física denunciou a espionagem e a chave é descartada.

O simulador transforma esse experimento em um jogo de cartas e moedas, com sincronização entre dispositivos por um token de texto.

## O que você vai aprender

- O que são **fótons**, **polarização** e **bases** retilínea (`+`) e diagonal (`X`).
- Que cada fóton é o **veículo de 1 bit de informação** — a base é o alfabeto, a polarização é a escrita e o bit é a mensagem.
- Como quatro estados quânticos codificam os bits `0` e `1`.
- Por que medir com a base errada causa **colapso** e gera erros.
- Por que o **teorema da não clonagem** impede uma cópia perfeita.
- O que é **peneiramento** (sifting) e por que só parte dos bits vira chave.
- O que é **QBER** e por que o limite de **11%** indica a presença de um espião.
- A diferença entre **codificação** (Base64) e **criptografia**.

## O jogo em três papéis

| Papel | Responsabilidade | Objetivo |
| --- | --- | --- |
| 📡 **Emissor** | Escolhe base e bit de cada fóton. | Gerar uma chave que o Receptor consiga reconstruir. |
| 🕵️ **Espião** | Mede cada fóton com uma base secreta. | Passar despercebido (erro ≤ 11%) e adivinhar a chave. |
| 🛰️ **Receptor** | Mede os fótons com sua própria base. | Obter a mesma chave do Emissor, detectar a espionagem e gerar o relatório final. |

## Fluxo do jogo

1. **Apresentação:** história curta do BB84, contexto da missão, função de cada papel e objetivo final. Botões **Iniciar prática** e **Conhecer a história**.
2. **Preparação:** cada integrante entra no próprio dispositivo, digita o próprio nome e escolhe um papel — Emissor, Espião ou Receptor. A experiência completa usa três pessoas diferentes.
3. **Missão:** o guia narrativo acompanha cada fóton, explica o que aconteceu e indica o próximo passo.
4. **Recepção da transmissão:** o Espião recebe o token do Emissor; o Receptor recebe o token do Espião. A etapa só começa depois dessa recepção.
5. **Resultado dos sorteios:** após cada moeda girar, aparece a mensagem do que caiu e o que isso significa.
6. **Relatório:** gerado pelo Receptor, com tabela das rodadas, peneiramento, chaves e taxa de erro.

## Como jogar

### Em trio (um dispositivo por pessoa)

1. Abra o simulador, clique em **Iniciar prática**, digite seu nome e escolha seu papel. Repita o processo no dispositivo de cada integrante, com um papel diferente por pessoa.
2. O **Emissor** joga as moedas dos 10 fótons e gera o token.
3. Envie o token ao **Espião** (WhatsApp, chat, etc.). No dispositivo dele, escolha o papel Espião e cole o token na tela de **Recepção da transmissão**. Depois ele mede e gera um novo token.
4. Envie esse token ao **Receptor**. Ele o carrega na tela de recebimento, faz as medições e gera o **relatório final**.
5. O relatório mostra a tabela das rodadas, as chaves e a taxa de erro.

### Sozinho (modo demonstração)

1. Escolha um papel e jogue as rodadas, ou use **⚡ Preencher Restantes**.
2. Ao concluir cada etapa, use **Continuar sozinho (demonstração)**: os dados seguem carregados e não é preciso colar token. O fluxo funciona, mas a lógica do Espião só faz sentido quando outra pessoa preparou os fótons.
3. Repita até o relatório final. Para ver o efeito da espionagem, rode uma partida com o Espião e outra sem.

## A física em um minuto

O BB84 usa duas bases, cada uma com dois estados:

| Base | Símbolo | Bit | Estado |
| --- | --- | --- | --- |
| Retilínea (`+`) | `\|` | 1 | Vertical |
| Retilínea (`+`) | `-` | 0 | Horizontal |
| Diagonal (`X`) | `/` | 1 | 45° |
| Diagonal (`X`) | `\` | 0 | 135° |

Se o Receptor mede com a mesma base usada pelo Emissor, recupera o bit com certeza. Se mede com a base errada, o resultado é aleatório e o estado original é destruído — o **colapso**. O Espião não pode copiar o fóton (não clonagem), então precisa medir e repassar; quando erra a base, introduz erros.

## As duas moedas

| Moeda | Cara | Coroa | O que define |
| --- | --- | --- | --- |
| **Moeda 1 — Base** | `+` retilínea | `X` diagonal | Como o fóton é preparado ou medido. |
| **Moeda 2 — Bit** | `1` | `0` | O dado transportado. |

No Emissor, a Moeda 2 é a informação escolhida. No Espião, vira um chute quando ele erra a base. No Receptor, é a leitura após o colapso. As escolhas travam após o lançamento, como uma medição quântica real.

## Relatório e limite de 11%

O relatório consolidado traz:

- **Mantidos (N):** fótons em que Emissor e Receptor usaram a mesma base.
- **Descartados:** fótons com bases diferentes, removidos no peneiramento.
- **QBER amostral:** erro nos 2 primeiros bits mantidos, revelados publicamente.
- **Taxa global (M/N):** erro em todos os bits mantidos.
- **Chaves:** bruta do Emissor, bruta do Receptor e chave secreta final (sem os 2 bits da amostra).
- **Veredito:** acima de 11%, espião detectado e chave abortada.

Em um ataque de interceptação e reenvio, o erro esperado nos bits mantidos fica em torno de **25%**. O limite de 11% é o que protocolos reais conseguem tolerar após correção de erros e amplificação de privacidade.

> **Nota estatística:** com apenas 2 bits de amostra, o QBER é uma indicação didática, não uma prova. Um resultado 0% em 2 bits não garante ausência de espião — por isso o relatório também exibe a taxa global.

## Manual embutido

O botão **📖 Manual de Instruções** abre um guia completo com:

- elenco e objetivos;
- explicação de fótons, bases, superposição, colapso e não clonagem;
- o papel do fóton como veículo de 1 bit de informação;
- tabelas das moedas e dos quatro estados;
- passo a passo do jogo, da apresentação ao relatório;
- guia narrativo que reage a cada escolha;
- o fluxo do token entre Emissor, Espião e Receptor, sem importação durante a medição;
- explicação do relatório e do limite de 11%;
- limitações didáticas e glossário.

## Rodando localmente

Não há build nem instalação. Basta abrir `index.html` no navegador.

Se preferir um servidor local:

```bash
python -m http.server 8000
```

Depois acesse `http://localhost:8000`.

## Publicando no GitHub Pages

1. Crie o repositório `bb84-quantum-lab` no GitHub.
2. Envie a branch `main`:

```bash
git remote add origin https://github.com/SEU-USUARIO/bb84-quantum-lab.git
git push -u origin main
```

3. No GitHub, acesse **Settings → Pages**.
4. Em **Source**, selecione **Deploy from a branch**, branch `main` e pasta `/ (root)`.
5. O site ficará em `https://SEU-USUARIO.github.io/bb84-quantum-lab/`.

O arquivo principal já se chama `index.html`, então é servido automaticamente na raiz.

## Estrutura

```
bb84-quantum-lab/
├── index.html   # aplicação completa (HTML, CSS e JS)
├── .gitignore
└── README.md
```

## Limitações didáticas

Este é um modelo simplificado, não uma implementação criptográfica:

- não há ruído no canal: sem espião, o erro é 0%;
- o Espião intercepta todos os fótons e sempre repassa um estado;
- a amostra pública tem apenas 2 bits;
- não há correção de erro, amplificação de privacidade nem autenticação do canal clássico;
- o token é Base64, ou seja, codificação reversível, não criptografia;
- são 10 fótons para caber em uma aula.

## Roadmap

- [ ] Modo com ruído de canal configurável
- [ ] Ataques parciais e seletivos do espião
- [ ] Amostra pública configurável e análise estatística
- [ ] Modo sala de aula com placar
- [ ] Exportação do relatório em PDF aprimorada
- [ ] Versão em inglês

## Glossário

| Termo | Definição |
| --- | --- |
| **Fóton** | Quantum de luz; no BB84, é o veículo que transporta 1 bit de informação. |
| **Polarização** | Orientação da oscilação da luz, usada para codificar bits. |
| **Base** | Par de direções usado para preparar ou medir um fóton. |
| **Superposição** | Estado quântico que combina possibilidades antes da medição. |
| **Colapso** | Mudança irreversível do estado ao ser medido. |
| **Não clonagem** | Impossibilidade de copiar perfeitamente um estado quântico desconhecido. |
| **Peneiramento** | Seleção dos bits em que as bases coincidiram (sifting). |
| **QBER** | Taxa de erro quântica entre os bits mantidos. |
| **Chave** | Sequência de bits compartilhada para cifrar mensagens. |
| **Token** | Texto em Base64 que transporta o estado dos 10 fótons entre etapas; gerado por quem conclui uma etapa e carregado por quem inicia a próxima. |

## Créditos

**bb84-quantum-lab** é um simulador didático de código aberto para explorar o protocolo BB84 em aulas de física, computação e segurança da informação.

Referência original: Bennett, C. H.; Brassard, G. *Quantum cryptography: Public key distribution and coin tossing* (1984).
