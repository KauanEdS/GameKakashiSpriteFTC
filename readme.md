# Animação de Personagem com Autómato Finito em Pygame: Kakashi Hatake

![Linguagem](https://img.shields.io/badge/Python-3.x-blue.svg)
![Biblioteca](https://img.shields.io/badge/Framework-Pygame-red.svg)
![Conceito](https://img.shields.io/badge/Teoria-Autómato%20Finito-purple.svg)
![Licença](https://img.shields.io/badge/Licen%C3%A7a-MIT-informational.svg)

## 🎯 Sobre o Projeto

Este projeto é uma demonstração técnica de como um **Autómato Finito Determinístico (AFD)** pode ser utilizado para gerir estados e animações de uma personagem 2D complexa. Utilizando a biblioteca **Pygame**, a personagem Kakashi Hatake (de Naruto) ganha vida com transições de estado fluidas e bem definidas para uma variedade de ações.

O objetivo principal é aplicar os conceitos teóricos da Teoria da Computação num projeto prático e visual, mostrando como a máquina de estados finitos é uma ferramenta poderosa para o desenvolvimento de jogos e simulações.

---

## ✨ Funcionalidades e Animações

A personagem é capaz de realizar diversas ações, cada uma representando um estado no Autómato, controladas por um conjunto de regras de transição bem definidas.

| Ação | Descrição |
| :--- | :--- |
| 🚶 **Andar/Correr** | Movimento básico e acelerado, com transições suaves. |
| 🤸 **Pular** | Executa um arco de pulo com física simples, permitindo movimento aéreo. |
| 🧎 **Agachar** | Permite que a personagem se agache e se mova lentamente. |
| 💥 **Ataques** | Combos de ataques básicos, aéreos, agachados e em corrida. |
| ⚡ **Raikiri** | Habilidade especial com animação dedicada, efeitos sonoros e movimento para a frente. |
| 👁️ **Sharingan** | Ativa o Sharingan, com efeitos visuais, som e uma troca dinâmica do cenário para simular um genjutsu. |
| 🐶 **Invocação (Nindogs)** | Executa o jutsu de invocação dos Cães Ninjas (Nindogs). |
| 🎉 **Vitória** | Animação de vitória que finaliza a execução do programa. |

---

## 📸 Galeria Visual

| Mapa Principal (Vila da Folha) | Mapa do Sharingan (Genjutsu) |
| :---: | :---: |
| <img src="Mapa/mapa4.jpg" width="400"> | <img src="Mapa/mapa3.jpg" width="400"> |

| Animação de Raikiri | Animação de Invocação |
| :---: | :---: |
| <img src="Sprite/raikiri/raikiri-6.png" width="400"> | <img src="Sprite/ninDogs/ninDogs-21.png" width="400"> |

---

## 🚀 Como Executar o Projeto

Siga os passos abaixo para rodar a simulação na sua máquina.

### **Pré-requisitos**

* **Python 3.x**
* **Pygame**: A biblioteca pode ser instalada facilmente via pip.
  ```bash
  pip install pygame
  ```

### **Instalação**

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/KauanEdS/GameKakashiSpriteFTC.git
    ```
2.  **Navegue até à pasta do projeto:**
    ```bash
    cd GameSpriteFTC
    ```
3.  **Execute o script principal:**
    ```bash
    python main.py
    ```

O jogo será iniciado em tela cheia. Para sair, pode esperar a animação de "vitória" terminar ou pressionar `Alt + F4` (Windows) / `Cmd + Q` (macOS).

---

## ⌨️ Controles do Personagem

As ações são controladas pelo teclado, onde cada tecla ou combinação representa um **símbolo de entrada** para o nosso AFD.

| Tecla(s) | Ação |
| :--- | :--- |
| `A` / `D` | Andar para a Esquerda / Direita |
| `SHIFT` + `A` / `D` | Correr para a Esquerda / Direita |
| `S` | Agachar |
| `S` + `A` / `D` | Andar Agachado |
| `ESPAÇO` | Pular |
| `H` | Ataque Básico |
| `U` | Ataque para Cima |
| `R` + `T` | **Habilidade Especial: Raikiri** |
| `J` | **Habilidade Especial: Sharingan** |
| `M` | **Habilidade Especial: Invocação** |
| `P` | Animação de Vitória (encerra o jogo) |

---

## 🔧 Estrutura do Código: O AFD em Ação

O núcleo do projeto é a implementação do Autómato Finito Determinístico.

#### 1. Estados (`State`)
Os estados possíveis da personagem são definidos numa `Enum`, o que torna o código mais limpo e legível.

```python
class State(Enum):
    IDLE = auto()
    WALK_RIGHT = auto()
    JUMP = auto()
    ATTACK = auto()
    SHARINGAN = auto()
    # ... e todos os outros estados
```

#### 2. Tabela de Transições (`transitions`)
A lógica do AFD é centralizada num dicionário que mapeia `(estado_atual, simbolo_de_entrada)` para um `proximo_estado`. Esta é a função de transição (δ) do autómato.

```python
transitions: dict[tuple[State, Symbol], State] = {
    (State.IDLE,      'D'): State.WALK_RIGHT,
    (State.WALK_RIGHT, 'SHIFT+D'): State.RUN_RIGHT,
    (State.RUN_RIGHT, None): State.IDLE, # Retorna ao estado parado se nenhuma tecla for pressionada
    # ... todas as outras transições
}
```

#### 3. Loop Principal
O loop principal do jogo é responsável por:
1.  **Ler a Entrada:** Captura as teclas pressionadas e converte-as num `símbolo` para o AFD.
2.  **Atualizar o Estado:** Usa a tabela de transições para encontrar o novo estado da personagem.
3.  **Gerir Animações:** Com base no estado atual, seleciona a lista de frames correta e avança a animação.
4.  **Aplicar Física:** Atualiza a posição da personagem na tela, aplicando movimento e gravidade simulada para o pulo.
5.  **Renderizar na Tela:** Desenha o cenário e o sprite da personagem.

---

## 📂 Estrutura de Pastas

O projeto está organizado da seguinte maneira para facilitar a gestão dos assets:

```
├── main.py             # Script principal do jogo
├── readme.md           # Este ficheiro
├── Sprite/             # Contém todas as animações da personagem
│   ├── attack/
│   ├── jump/
│   ├── run/
│   └── ... (outras pastas de animação)
├── Sons/               # Efeitos sonoros das habilidades
│   ├── raikiri.mp3
│   └── sharingan.mp3
└── Mapa/               # Imagens de fundo
    ├── mapa3.jpg
    └── mapa4.jpg
```

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

