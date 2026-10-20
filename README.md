# bb84-quantum-lab

> **BB84, o Token do Satélite** — um laboratório interativo para entender, na prática, como a física quântica protege informações.

Em uma missão de três pessoas, você envia uma chave secreta da Estação Antártica para um satélite enquanto um espião tenta interceptá-la. A segurança não vem de uma senha mais difícil: vem das leis da mecânica quântica. Cada fóton carrega uma base e um bit; qualquer tentativa de espionagem deixa erros detectáveis.

O projeto é um **simulador educacional do protocolo BB84** (Bennett & Brassard, 1984), feito em um único arquivo HTML, sem dependências e sem servidor. Roda no navegador, inclusive em celular.

---

## A missão

1. O **Emissor** prepara 10 fótons com bases e bits sorteados.
2. O **Espião** intercepta os fótons e tenta medi-los sem ser notado.
3. O **Receptor** mede o que chega e guarda apenas os bits em que sua base coincide com a do Emissor.
4. No fim, os dois lados legítimos comparam uma pequena amostra. Se a taxa de erro passar de **11%**, a física denunciou a espionagem e a chave é descartada.

O simulador transforma esse experimento em um jogo de cartas e moedas, com sincronização entre dispositivos por um token de texto.

## O que você vai aprender

- O que são **fótons**, **polarização** e **bases** retilínea (`+`) e diagonal (`X`).
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
| 🛰️ **Receptor** | Mede os fótons com sua própria base. | Obter a mesma chave do Emissor e detectar a espionagem. |

## Como jogar

### Em trio (um dispositivo por pessoa)

1. Abra o simulador e preencha os nomes do trio.
2. O **Emissor** joga as moedas dos 10 fótons e gera o token.
3. Envie o token ao **Espião** (WhatsApp, chat, etc.). Ele importa, faz suas medições e gera um novo token.
4. Envie esse token ao **Receptor**, que faz suas medições.
5. Ao final, o relatório mostra a tabela das rodadas, as chaves e a taxa de erro.

### Sozinho (modo demonstração)

1. Escolha um papel e jogue as rodadas, ou use **⚡ Preencher Restantes**.
2. Gere o token e use **Alternar para Visão do Espião/Receptor**.
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
- tabelas das moedas e dos quatro estados;
- passo a passo do jogo;
- explicação do token e do relatório;
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
| **Fóton** | Quantum de luz; a menor porção de energia luminosa. |
| **Polarização** | Orientação da oscilação da luz, usada para codificar bits. |
| **Base** | Par de direções usado para preparar ou medir um fóton. |
| **Superposição** | Estado quântico que combina possibilidades antes da medição. |
| **Colapso** | Mudança irreversível do estado ao ser medido. |
| **Não clonagem** | Impossibilidade de copiar perfeitamente um estado quântico desconhecido. |
| **Peneiramento** | Seleção dos bits em que as bases coincidiram (sifting). |
| **QBER** | Taxa de erro quântica entre os bits mantidos. |
| **Chave** | Sequência de bits compartilhada para cifrar mensagens. |

## Créditos

**bb84-quantum-lab** integra o **Projeto Córtex — Curso 2: Princípios da Física Quântica**.

- Formadora: Dra. Judite
- Mentora: Dra. Viridiana Alves de Lara

Simulador didático de código aberto para explorar o protocolo BB84. Referência original: Bennett, C. H.; Brassard, G. *Quantum cryptography: Public key distribution and coin tossing* (1984).
