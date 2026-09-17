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
