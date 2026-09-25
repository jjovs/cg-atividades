# cg-atividades

Atividades da disciplina de **Computação Gráfica**.

## Atividades

| # | Atividade | Arquivo | Abrir online |
|---|---|---|---|
| 1 | Flor, robô e carro | [`flor-robo-carro.html`](flor-robo-carro.html) | [abrir](https://jjovs.github.io/cg-atividades/flor-robo-carro.html) |
| 2 | Retas com Bresenham | [`exercicio1-bresenham-reta.html`](exercicio1-bresenham-reta.html) | [abrir](https://jjovs.github.io/cg-atividades/exercicio1-bresenham-reta.html) |
| 3 | Retas e triângulos com Bresenham | [`exercicio2-bresenham-triangulo.html`](exercicio2-bresenham-triangulo.html) | [abrir](https://jjovs.github.io/cg-atividades/exercicio2-bresenham-triangulo.html) |
| 4 | Pong | [`pong-webgl.html`](pong-webgl.html) | [abrir](https://jjovs.github.io/cg-atividades/pong-webgl.html) |
| 5 | Robô animado | [`robo-animado.html`](robo-animado.html) | [abrir](https://jjovs.github.io/cg-atividades/robo-animado.html) |
| 6 | Helicóptero | [`helicoptero.html`](helicoptero.html) | [abrir](https://jjovs.github.io/cg-atividades/helicoptero.html) |

---

### 1. Retas com Bresenham

Traçado de retas pixel a pixel pelo algoritmo de Bresenham, usando `gl.POINTS`
(sem `GL_LINES`).

- 1º clique: ponto inicial
- 2º clique: ponto final — a reta é traçada
- Teclas `0` a `9`: trocam a cor da reta

### 2. Retas e triângulos com Bresenham

Mesma ideia do exercício 1, agora com triângulos. Apenas uma figura é exibida
por vez: a anterior é apagada.

- Tecla `R`: modo reta (2 cliques)
- Tecla `T`: modo triângulo (3 cliques)
- Cliques definem os vértices
- Teclas `0` a `9`: trocam a cor da figura

### 3. Flor, robô e carro

Três cenas desenhadas lado a lado, cada uma em seu próprio canvas, montadas a
partir de primitivas (triângulos e retângulos) com cor por vértice.

### 4. Pong

Jogo com transformações 2D aplicadas por matrizes 3×3
(`mat3`) enviadas ao vertex shader como uniform.

**Controles**

| Ação | Tecla |
|---|---|
| Barra verde (esquerda) | `W` sobe / `S` desce |
| Barra azul (direita) | `↑` sobe / `↓` desce |
| Reiniciar a partida | `R` |

**Regras e mecânicas**

- Partida até **5 pontos**; ao terminar, o vencedor é exibido e o jogo congela.
- O ângulo de saída da bola depende de onde ela bate na barra (até 45° na ponta).
- A bola acelera progressivamente: +3% a cada rebatida e +4% no saque a cada
  ponto disputado, limitada ao dobro da velocidade inicial.
- Toda a animação usa **delta time**, então a velocidade é a mesma em monitores
  de 60 Hz, 120 Hz ou 144 Hz.

**Detalhes de implementação**

- Barras: dois triângulos (6 vértices) formando um retângulo.
- Bola: círculo aproximado por 30 triângulos a partir do centro.
- Posicionamento de cada objeto por matriz de translação (`m3.translation`),
  recalculada a cada quadro.
- Cor de cada objeto definida por um `uniform vec3` no fragment shader.

### 6. Helicóptero

Helicóptero 3D (WebGL 2, matrizes 4×4 `m4`) montado a partir do
[exemplo da disciplina](https://github.com/martinslemosana/cg-02-2026/tree/main/helicoptero),
movimentado pelo teclado.

**Controles**

| Ação | Tecla |
|---|---|
| Subir / descer | `↑` / `↓` |
| Esquerda / direita | `←` / `→` |

**Comportamento**

- As duas hélices giram continuamente, parado ou em movimento:
  - **hélice superior**: gira em torno do eixo Y (a haste passa pela origem);
  - **hélice da cauda**: é levada à origem, gira em Z e volta ao lugar
    (`T(c) · Rz(θ) · T(-c)`).
- A rotação acompanha o movimento: acelera ao subir e ao andar para os lados,
  desacelera ao descer. A hélice da cauda (anti-torque) gira sempre 1,5× mais
  rápido que a principal. As rotações por minuto aparecem abaixo do canvas.
- O helicóptero vira o bico para o lado em que está andando e inclina o bico
  para baixo proporcionalmente à velocidade horizontal.
- Aceleração e frenagem suaves, com **delta time**, e limites para não sair da tela.
- Hierarquia de transformações:
  `corpo = T(posição) · câmera · Ry(direção) · Rz(inclinação) · S`;
  cada hélice aplica a sua rotação sobre a matriz do corpo.
