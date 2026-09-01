<h1 align="center">🧪 Rick and Morty — Memory Game 🧳</h1>

<p align="center">
  <strong>Jogo da memória interativo desenvolvido em Vanilla JavaScript, HTML5 e CSS3, com geração procedural de tabuleiro, animações tridimensionais (CSS 3D Transforms) e temática retro inspirada no universo de Rick and Morty.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript ES6+" />
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5" />
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3" />
  <img src="https://img.shields.io/badge/Google_Fonts-Press_Start_2P-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Google Fonts" />
  <img src="https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen?style=for-the-badge" alt="Status" />
  <img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge" alt="License" />
</p>

<p align="center">
  <img src="images/logo.png" width="400px" alt="Rick and Morty Memory Game Logo" />
</p>

---

## 📖 Visão Geral

O **Rick and Morty Memory Game** é um jogo da memória web que combina lógica algorítmica no navegador com uma interface gráfica estilizada em pixel art de 8 bits. O objetivo do jogador é encontrar todos os 10 pares de cartas temáticas de personagens da série animada *Rick and Morty* no menor número de tentativas possível.

A aplicação foi construída com foco em práticas essenciais de engenharia web moderna sem o uso de bibliotecas pesadas ou frameworks reativos:
- Manipulação direta e eficiente da árvore DOM.
- Persistência e ciclo de vida de sessão no cliente via `localStorage`.
- Renderização visual realista com perspectiva 3D e rotações no eixo Y em CSS (`preserve-3d`, `rotateY`).
- Controle assíncrono de eventos e fluxo de temporizadores (`setTimeout`).

---

## ✨ Funcionalidades

- 🔑 **Fluxo de Login & Sessão do Jogador:** Validação de formulário em tempo real que bloqueia nomes com menos de 3 caracteres e armazena a identificação do jogador localmente via `localStorage`.
- 🎴 **Geração Procedural de Tabuleiro:** Embaralhamento dinâmico a cada partida com duplicação automática da lista de 10 personagens, totalizando 20 cartas em um grid 5x4.
- 🔄 **Animação Realista de Flip 3D:** Cartas com faces frontal e traseira independentes que realizam rotação tridimensional de 180 graus com transição suave de 400ms.
- 🎯 **Verificação Automática de Pares:** Comparação de atributos `data-character` entre a primeira e a segunda carta revelada.
- 🚫 **Desativação Visual de Cartas Acertadas:** Aplicação de filtro dessaturado (`filter: saturate(0); opacity: 0.5`) para pares já concluídos, impedindo novos cliques.
- 🏆 **Detecção de Fim de Jogo & Vitória:** Monitoramento em tempo real da quantidade de cartas desabilitadas e disparo do alerta de comemoração ao atingir os 10 pares (20 cartas).
- 🧹 **Gerenciamento Seguro de Memória:** Limpeza automática da chave `player` do `localStorage` no evento `beforeunload` para evitar sessões órfãs.

---

## 🎯 Diferenciais e Destaques Técnicos

1. **Efeito de Rotação Tridimensional (CSS 3D Transforms):**
   - Uso de `transform-style: preserve-3d` no contêiner da carta (`.card`) e `backface-visibility: hidden` na face posterior (`.back`).
   - A classe `.reveal-card` aplica `transform: rotateY(180deg)`, criando a ilusão física de virada de carta sem necessidade de bibliotecas de animação externas.

2. **Lógica de Estado sem Dependências:**
   - Controle de estado em variáveis de escopo (`firstCard` e `secondCard`) que atuam como uma máquina de estados finita simples:
     - Estado 0: Nenhuma carta selecionada.
     - Estado 1: 1ª carta virada e aguardando clique da 2ª carta.
     - Estado 2: 2ª carta virada, iniciando comparação com *delay* de 500ms para cartas incompatíveis.

3. **Arquitetura Client-Side Pura:**
   - Zero dependências de pacotes NPM, bundlers ou compilação prévia. O projeto roda nativamente em qualquer navegador moderno.

---

## 🏗️ Arquitetura e Estrutura de Pastas

```text
RickAndMorty_MemoryGame/
├── index.html            # Tela inicial e formulário de login do jogador
├── README.md             # Documentação técnica completa do projeto
├── pages/                # Páginas internas da aplicação
│   └── game.html         # Arena principal do jogo da memória (tabuleiro)
├── css/                  # Folhas de estilo modulares
│   ├── reset.css         # Reset global, box-sizing e importação da fonte Press Start 2P
│   ├── login.css         # Estilização e centralização da tela de login
│   └── game.css          # Grid 5x4, animações 3D de flip e estados das cartas
├── js/                   # Controladores e regras de negócio JavaScript
│   ├── login.js          # Validação reativa do input e controle de início de sessão
│   └── game.js           # Geração do grid, embaralhamento, eventos de flip e match
└── images/               # Assets gráficos, texturas e avatares dos personagens
    ├── bg.jpg            # Imagem de fundo espacial temática
    ├── logo.png          # Logo do Rick and Morty
    ├── brain.png         # Ícone do cérebro na tela inicial
    ├── back.png          # Textura da face oculta das cartas (portal)
    ├── rick.png          # Face do Rick Sanchez
    ├── morty.png         # Face do Morty Smith
    ├── beth.png          # Face da Beth Smith
    ├── jerry.png         # Face do Jerry Smith
    ├── summer.png        # Face da Summer Smith
    ├── pickle-rick.png   # Face do Pickle Rick
    ├── pessoa-passaro.png# Face do Birdperson (Pessoa Pássaro)
    ├── meeseeks.png      # Face do Mr. Meeseeks
    ├── jessica.png       # Face da Jessica
    ├── scroopy.png       # Face do Scroopy Noopers
    └── ericky.png        # Avatar do desenvolvedor
```

---

## 🎨 UX, Animações e Interfaces

- **Estética Retro Arcade:** Tipografia pixel art clássica (*Press Start 2P*) importada do Google Fonts combinada com paleta de cores temática.
- **Feedback Reativo:** O botão de login transita visualmente de cinza desabilitado (`#eee`) para vermelho vivo (`#ee665c`) com cursor ponteiro assim que o usuário digita 3 ou mais caracteres.
- **Transições Visuais:** Efeito suave de rotação (`400ms ease`) e dessaturação gradual nas cartas emparelhadas.

### 🔄 Fluxo de Estados da Aplicação

```text
[ Usuário acessa index.html ]
              │
              ▼
[ Digitação no Input (login.js) ]
              │
              ├─► (Caracteres <= 2) ──► [ Botão 'Play' Desabilitado ]
              │
              └─► (Caracteres > 2)  ──► [ Botão 'Play' Habilitado ]
                                                │
                                                ▼ (Submit)
                                   [ Salva 'player' no localStorage ]
                                                │
                                                ▼
                                   [ Redireciona para /pages/game.html ]
                                                │
                                                ▼
                                   [ Verifica 'player' no localStorage ]
                                                │
                     ┌──────────────────────────┴──────────────────────────┐
                     ▼ (Nulo)                                              ▼ (Existe)
        [ Redireciona para / ]                                [ Duplica lista de 10 personagens ]
                                                                           │
                                                                           ▼
                                                              [ Embaralha array (20 cartas) ]
                                                                           │
                                                                           ▼
                                                              [ Renderiza cartas no CSS Grid ]
                                                                           │
                                                                           ▼
                                                              [ Loop de Partida: Cliques ]
                                                                           │
                                    ┌──────────────────────────────────────┴──────────────────────────────────────┐
                                    ▼ (1ª Carta Clicada)                                                         ▼ (2ª Carta Clicada)
                         [ Adiciona .reveal-card ]                                                    [ Adiciona .reveal-card ]
                         [ Guarda em firstCard ]                                                      [ Compara data-character ]
                                                                                                                   │
                                                                           ┌───────────────────────────────────────┴───────────────────────────────────────┐
                                                                           ▼ (Iguais / Match)                                                              ▼ (Diferentes)
                                                            [ Adiciona .disabled-card ]                                                     [ Aguarda 500ms ]
                                                            [ Reseta firstCard / secondCard ]                                               [ Remove .reveal-card ]
                                                                           │                                                                [ Reseta seleções ]
                                                                           ▼
                                                            [ Total de .disabled-card === 20? ]
                                                                           │
                                                                           ├─► (NÃO) ──► [ Continua Partida ]
                                                                           │
                                                                           └─► (SIM) ──► [ Alerta de Vitória! ]
```

---

## 👾 Personagens Integrados

O baralho do jogo é formado por 10 pares distintos de personagens:

| Personagem | Identificador (`data-character`) | Caminho do Asset |
| :--- | :--- | :--- |
| **Rick Sanchez** | `rick` | `images/rick.png` |
| **Morty Smith** | `morty` | `images/morty.png` |
| **Beth Smith** | `beth` | `images/beth.png` |
| **Jerry Smith** | `jerry` | `images/jerry.png` |
| **Summer Smith** | `summer` | `images/summer.png` |
| **Pickle Rick** | `pickle-rick` | `images/pickle-rick.png` |
| **Pessoa Pássaro** | `pessoa-passaro` | `images/pessoa-passaro.png` |
| **Mr. Meeseeks** | `meeseeks` | `images/meeseeks.png` |
| **Jessica** | `jessica` | `images/jessica.png` |
| **Scroopy Noopers** | `scroopy` | `images/scroopy.png` |

---

## 🧭 Guia de Uso Passo a Passo

1. **Identificação:** Na tela inicial, digite seu nome no campo de texto (mínimo de 3 caracteres).
2. **Iniciar Jogo:** Clique no botão **Play** para ser redirecionado para a arena de cartas.
3. **Virar Cartas:** Clique em uma carta para revelar o personagem oculto e, em seguida, clique em uma segunda carta.
4. **Acertos e Erros:** Se as cartas forem idênticas, elas permanecerão reveladas e ficarão translúcidas. Se forem diferentes, elas serão desviradas automaticamente após 500ms.
5. **Conclusão:** Continue até encontrar todos os 10 pares para receber a mensagem de vitória.

---

## 🛡️ Análise Técnica e Boas Práticas

- **✅ Pontos Positivos:**
  - Aplicação leve e auto-suficiente que executa localmente sem necessidade de conexão com internet ou backend.
  - Baixo consumo de CPU/GPU com aceleração de hardware nativa para as transformações 3D em CSS.
  - Código desacoplado em módulos de estilo e script bem delineados.

- **⚠️ Riscos Identificados e Plano de Mitigação:**
  - *Risco:* Utilização do `alert()` nativo para a mensagem de vitória, que pausa a execução síncrona do navegador.
    *Mitigação:* Desenvolver um modal customizado em HTML/CSS com tema pixel art e opção de reiniciar a partida.
  - *Risco:* Embaralhamento via `sort(() => Math.random() - 0.5)` possui distribuição não perfeitamente uniforme.
    *Mitigação:* Implementar o algoritmo padrão **Fisher-Yates Shuffle**.
  - *Risco:* Possibilidade de cliques múltiplos rápidos durante o intervalo de 500ms entre cartas incompatíveis.
    *Mitigação:* Introduzir uma trava booleana (`isLocked = true`) durante a validação assíncrona.

---

## ⚙️ Requisitos e Instalação

### Pré-requisitos
- Qualquer navegador web moderno (Google Chrome, Firefox, Edge, Safari ou Brave).
- Opcionalmente, Git para clonar o repositório.

### Clonando o Repositório
```bash
# Clone o repositório
git clone https://github.com/erickystn/RickAndMorty_MemoryGame.git

# Acesse o diretório
cd RickAndMorty_MemoryGame
```

---

## 🚀 Como Executar

Por ser uma aplicação web estática pura, você pode executar o projeto de qualquer uma das seguintes formas:

### Opção 1: Servidor Local Python (Recomendado)
```bash
# Python 3
python3 -m http.server 8000
```
Acesse no navegador: `http://localhost:8000`

### Opção 2: Node.js (`npx serve`)
```bash
# Executa servidor estático
npx serve .
```

### Opção 3: Extensão Live Server (VS Code)
1. Abra a pasta do projeto no **VS Code**.
2. Clique com o botão direito no arquivo `index.html`.
3. Selecione **"Open with Live Server"**.

### Opção 4: Abertura Direta
Abra o arquivo `index.html` diretamente em seu navegador dando um duplo clique sobre ele.

---

## 💻 Exemplos de Uso e Código

### 1. Validação de Login e Controle de Sessão (`js/login.js`)
```javascript
const input = document.querySelector('.login__input');
const button = document.querySelector('.login__button');
const form = document.querySelector('.login-form');

const validateInput = ({ target }) => {
  if (target.value.length > 2) {
    button.removeAttribute('disabled');
    return;
  }
  button.setAttribute('disabled', '');
};

const handleSubmit = (event) => {
  event.preventDefault();
  localStorage.setItem('player', input.value);
  window.location = 'pages/game.html';
};

input.addEventListener('input', validateInput);
form.addEventListener('submit', handleSubmit);
```

### 2. Criação Dinâmica de Elementos e Efeito 3D (`js/game.js` e `css/game.css`)
```javascript
const createElement = (tag, className) => {
  const element = document.createElement(tag);
  element.className = className;
  return element;
};

const createCard = (character) => {
  const card = createElement('div', 'card');
  const front = createElement('div', 'face front');
  const back = createElement('div', 'face back');

  front.style.backgroundImage = `url('../images/${character}.png')`;

  card.appendChild(front);
  card.appendChild(back);

  card.addEventListener('click', revealCard);
  card.setAttribute('data-character', character);

  return card;
};
```

```css
.card {
  aspect-ratio: 3/4;
  width: 100%;
  border-radius: 5px;
  position: relative;
  transition: all 400ms ease;
  transform-style: preserve-3d;
}

.face {
  width: 100%;
  height: 100%;
  position: absolute;
  background-size: cover;
  background-position: center;
  border: 2px solid #39813a;
  border-radius: 5px;
  transition: all 400ms ease;
}

.front {
  transform: rotateY(180deg);
}

.back {
  background-image: url('../images/back.png');
  backface-visibility: hidden;
}

.reveal-card {
  transform: rotateY(180deg);
}

.disabled-card {
  filter: saturate(0);
  opacity: 0.5;
}
```

### 3. Comparação de Cartas e Checagem de Fim de Partida (`js/game.js`)
```javascript
const checkCards = () => {
  const firstCharacter = firstCard.getAttribute('data-character');
  const secondCharacter = secondCard.getAttribute('data-character');

  if (firstCharacter === secondCharacter) {
    firstCard.firstChild.classList.add('disabled-card');
    secondCard.firstChild.classList.add('disabled-card');

    firstCard = '';
    secondCard = '';

    checkEndGame();
  } else {
    setTimeout(() => {
      firstCard.classList.remove('reveal-card');
      secondCard.classList.remove('reveal-card');

      firstCard = '';
      secondCard = '';
    }, 500);
  }
};

const checkEndGame = () => {
  const disabledCards = document.querySelectorAll('.disabled-card');

  if (disabledCards.length === 20) {
    setTimeout(() => {
      alert('Parabéns, você conseguiu!');
    }, 600);
  }
};
```

---

## 🧪 Validação e Testes Manuais

A aplicação foi submetida a baterias de testes manuais em diferentes cenários:
- **Fluxo de Autenticação:** Validação de bloqueio do botão com 0, 1 e 2 caracteres, liberação com 3 ou mais, e persistência correta no `localStorage`.
- **Proteção de Rota:** Acesso direto a `pages/game.html` sem sessão prévia resulta em redirecionamento imediato para a tela de login.
- **Mecânica do Jogo:** Testes de acerto (cartas permanecem viradas e entram em estado desabilitado) e erro (cartas desviram após 500ms).
- **Encerramento da Partida:** Validação de contagem das 20 cartas desabilitadas e disparo do alerta final.
- **Reinicialização de Sessão:** Verificação de limpeza do `player` no fechamento de aba/recarregamento via `beforeunload`.

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Finalidade |
| :--- | :--- |
| ![JavaScript](https://img.shields.io/badge/JavaScript_ES6+-F7DF1E?style=flat-square&logo=javascript&logoColor=black) | Lógica de jogo, controle de fluxo, manipulação do DOM e eventos. |
| ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white) | Estruturação semântica das páginas de login e arena de jogo. |
| ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white) | CSS Grid (5 colunas), Flexbox, efeitos tridimensionais (`preserve-3d`, `rotateY`). |
| ![Google Fonts](https://img.shields.io/badge/Google_Fonts-Press_Start_2P-yellow?style=flat-square) | Tipografia estilizada no padrão arcade/pixel art de 8 bits. |

---

## 📈 Melhorias e Próximos Passos (Roadmap)

- [ ] Implementar cronômetro regressivo/progressivo e contador de movimentos/tentativas.
- [ ] Criar sistema de ranking local (High Scores) com persistência em `localStorage`.
- [ ] Desenvolver modal customizado de vitória em pixel art substituindo o `alert()`.
- [ ] Adicionar suporte a múltiplos níveis de dificuldade (Grid 4x3, 4x4, 5x4).
- [ ] Incluir efeitos sonoros temáticos (virada de cartas, acertos, erro e vitória).
- [ ] Otimização para layout mobile-first em telas menores.

---

## 🤝 Como Contribuir

1. Faça um **Fork** do projeto.
2. Crie uma branch para sua modificação:
   ```bash
   git checkout -b feature/novo-recurso
   ```
3. Commit suas alterações:
   ```bash
   git commit -m "feat: adiciona sistema de pontuação"
   ```
4. Envie a branch para seu repositório remoto:
   ```bash
   git push origin feature/novo-recurso
   ```
5. Abra um **Pull Request**.

---

## 👤 Autor

Desenvolvido por **[Ericky Sant'ana](https://github.com/erickystn)**.

---

## 📄 Licença

Este projeto é distribuído sob a licença **MIT**. Consulte o arquivo de licença para mais informações.
