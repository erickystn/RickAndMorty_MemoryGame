# 🧪 Rick and Morty — Memory Game

![Rick and Morty Memory Game Banner](images/logo.png)

<p align="center">
  <img src="https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript ES6+" />
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5" />
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3" />
  <img src="https://img.shields.io/badge/Google_Fonts-Press_Start_2P-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Google Fonts" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License" />
</p>

---

## 📖 Visão Geral

O **Rick and Morty Memory Game** é uma aplicação web interativa desenvolvida em Vanilla JavaScript (ES6+), HTML5 e CSS3, inspirada no universo da série de animação *Rick and Morty*.

O jogo implementa um fluxo completo de autenticação simulada de jogador via `localStorage`, geração procedural de tabuleiro (grid) com embaralhamento dinâmico de 20 cartas (10 pares temáticos), animações tridimensionais de flip em CSS (`3D transforms`), controle de estados assíncronos e validação de vitória.

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Finalidade |
| :--- | :--- |
| ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white) | Estruturação semântica das páginas de login e arena de jogo. |
| ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white) | Layout em CSS Grid, Flexbox, estilização retrô e animações 3D (`preserve-3d`, `rotateY`). |
| ![JavaScript](https://img.shields.io/badge/JavaScript_ES6+-F7DF1E?style=flat-square&logo=javascript&logoColor=black) | Manipulação do DOM, controle de eventos, persistência em `localStorage` e algoritmos de embaralhamento. |
| ![Google Fonts](https://img.shields.io/badge/Font-Press_Start_2P-yellow?style=flat-square) | Tipografia estilizada no padrão arcade/pixel art de 8 bits. |

---

## 🏗️ Arquitetura e Estrutura do Projeto

O projeto adota uma arquitetura modular baseada em separação de responsabilidades para projetos puramente client-side:

```text
RickAndMorty_MemoryGame/
├── css/
│   ├── game.css          # Estilos do grid de cartas, cabeçalho e animações 3D
│   ├── login.css         # Estilização do formulário e validação de login
│   └── reset.css         # Normalização de estilos globais e import da fonte Press Start 2P
├── images/
│   ├── back.png          # Textura da face oculta das cartas (portal/verso)
│   ├── beth.png          # Face do personagem Beth Smith
│   ├── bg.jpg            # Plano de fundo espacial temático
│   ├── brain.png         # Ícone ilustrativo do cérebro na tela inicial
│   ├── ericky.png        # Avatar do desenvolvedor
│   ├── jerry.png         # Face do personagem Jerry Smith
│   ├── jessica.png       # Face da personagem Jessica
│   ├── logo.png          # Logo oficial Rick and Morty
│   ├── meeseeks.png      # Face do personagem Mr. Meeseeks
│   ├── morty.png         # Face do personagem Morty Smith
│   ├── pessoa-passaro.png# Face do personagem Birdperson (Pessoa Pássaro)
│   ├── pickle-rick.png   # Face do personagem Pickle Rick
│   ├── rick.png          # Face do personagem Rick Sanchez
│   ├── scroopy.png       # Face do personagem Scroopy Noopers
│   └── summer.png        # Face da personagem Summer Smith
├── js/
│   ├── game.js           # Lógica do jogo (geração de cartas, flip, match, endgame)
│   └── login.js          # Validação em tempo real do formulário e controle de sessão
├── pages/
│   └── game.html         # Página principal do jogo (tabuleiro)
├── index.html            # Ponto de entrada da aplicação (tela de login)
└── README.md             # Documentação técnica do projeto
```

### Detalhamento das Camadas e Papel dos Arquivos

1. **`index.html` & `js/login.js`**: Ponto de entrada que gerencia a captura do nome do usuário. O botão de submissão só é liberado após a validação dinâmica de tamanho mínimo de caracteres (`target.value.length > 2`). O nome é persistido no armazenamento local (`localStorage.setItem('player', ...)`).
2. **`pages/game.html` & `js/game.js`**: Arena do jogo. Verifica a existência de uma sessão ativa do jogador (redirecionando para a raiz caso ausente). Monta programmaticamente os elementos do tabuleiro, lida com o estado de revelação e comparação de cartas, e dispara o evento de término de partida.
3. **`css/`**:
   - `reset.css`: Aplica o `box-sizing: border-box`, remove margens e paddings padrões e carrega a tipografia pixel art.
   - `login.css`: Centraliza o formulário com Flexbox (`height: 100vh`) e aplica feedback visual para estados ativos/desativados do botão.
   - `game.css`: Configura o CSS Grid (`grid-template-columns: repeat(5, 1fr)`), define `preserve-3d` e rotações no eixo Y (`rotateY(180deg)`) para efeito realista de rotação de cartas.

---

## 🔄 Fluxo de Dados e Ciclo de Vida da Aplicação

```text
[Usuário acessa index.html]
         │
         ▼
[Digita o nome (login.js)] ─── (Tamanho <= 2) ───► [Botão 'Play' Desabilitado]
         │
         │ (Tamanho > 2)
         ▼
[Botão Habilitado] ──► [Submit: Salva no localStorage ('player')] ──► [Redireciona para /pages/game.html]
                                                                                │
                                                                                ▼
[Verifica se 'player' existe] ◄─────────────────────────────────────────────────┘
         │
         ├─► [NÃO] ──► [Redireciona de volta para /]
         │
         └─► [SIM] ──► [Duplica array de 10 personagens em 20 itens]
                             │
                             ▼
                       [Embaralha array via Math.random]
                             │
                             ▼
                       [Cria e insere cartas no DOM (Grid)]
                             │
                             ▼
                       [Loop do Jogo: Cliques nas cartas]
                             │
                             ├─► [1ª Carta Revelada] ──► [Aguardando 2ª Carta]
                             │
                             └─► [2ª Carta Revelada] ──► [Compara data-character]
                                                               │
                                       ┌───────────────────────┴───────────────────────┐
                                       ▼                                               ▼
                              [Cartas Iguais (Match)]                        [Cartas Diferentes]
                                       │                                               │
                                       ▼                                               ▼
                        [Adiciona .disabled-card]                       [Aguardar 500ms e Desvirar]
                                       │
                                       ▼
                       [Checa se disabledCards === 20]
                                       │
                                       ▼ (SIM)
                        [Exibe Alerta de Vitória!]
```

---

## ⚙️ Requisitos e Instalação

### Pré-requisitos

Para executar o projeto localmente, você precisa apenas de:
- Um navegador web moderno com suporte a JavaScript ES6+ (Google Chrome, Mozilla Firefox, Microsoft Edge, Safari ou Brave).
- **Git** instalado no sistema (opcional, para clonagem do repositório).
- Opcionalmente, um servidor HTTP estático local (como extensões de IDE ou utilitários de linha de comando como Python ou Node.js).

### Passo a Passo de Instalação

1. **Clonar o Repositório**:
   ```bash
   git clone https://github.com/erickystn/RickAndMorty_MemoryGame.git
   ```

2. **Acessar o Diretório do Projeto**:
   ```bash
   cd RickAndMorty_MemoryGame
   ```

---

## 🚀 Como Executar

Por se tratar de uma aplicação client-side estática sem dependência de build steps (como Webpack ou Vite), o projeto pode ser executado de múltiplas formas:

### Opção 1: Via Servidor Local Python (Recomendado)
Para evitar eventuais restrições de resolução de caminhos relativos ao navegar entre páginas:
```bash
# Python 3.x
python3 -m http.server 8000

# Ou Python 2.x
python -m SimpleHTTPServer 8000
```
Abra o navegador em `http://localhost:8000`.

### Opção 2: Via Node.js (`npx serve` ou `http-server`)
```bash
# Utilizando npx serve
npx serve .

# Ou utilizando http-server
npx http-server . -p 8080
```
Abra o navegador no endereço indicado no terminal.

### Opção 3: Extensão Live Server (VS Code)
1. Abra a pasta `RickAndMorty_MemoryGame` no Visual Studio Code.
2. Clique com o botão direito no arquivo `index.html`.
3. Selecione **"Open with Live Server"**.

### Opção 4: Abertura Direta
Dê um duplo clique no arquivo `index.html` para abrir diretamente no seu navegador padrão.

---

## 💻 Exemplos de Uso e Arquitetura de Código

Abaixo estão detalhados os principais blocos de código que regem a lógica e comportamento do jogo:

### 1. Validação de Input e Persistência de Sessão (`js/login.js`)
O formulário de login utiliza escuta de eventos reativa para habilitar dinamicamente o botão de início de jogo:

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

### 2. Geração Dinâmica de Elementos e Efeito 3D (`js/game.js` e `css/game.css`)
Cada carta é composta por um contêiner estrutural com faces frontal e traseira, estilizadas para suporte à perspectiva 3D:

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

Regras CSS de rotação tridimensional associadas:

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

### 3. Validação de Pares e Condição de Vitória (`js/game.js`)
Ao virar duas cartas, o algoritmo compara os atributos `data-character` para aplicar os estados visuais e checar o encerramento da partida:

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

## 👾 Personagens Integrados

O tabuleiro conta com 10 pares (totalizando 20 cartas) com os seguintes personagens:

| Personagem | Identificador (`data-character`) | Asset |
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

## 📈 Melhorias e Próximos Passos (Roadmap)

- [ ] Implementação de cronômetro e contador de movimentos.
- [ ] Sistema de Recordes e Ranking (High Scores) persistidos localmente.
- [ ] Otimização e responsividade aprimorada para dispositivos móveis (`Mobile-first`).
- [ ] Inclusão de efeitos sonoros temáticos para virada de cartas, acertos e vitória.
- [ ] Múltiplos níveis de dificuldade (Grid 4x3, 4x4, 5x4).

---

## 👤 Autor

Desenvolvido por **[Ericky Sant'ana](https://github.com/erickystn)**.

---

## 📄 Licença

Este projeto é distribuído sob a licença **MIT**. Consulte o arquivo de licença para mais detalhes.
