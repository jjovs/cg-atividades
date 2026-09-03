# cg-atividades

Atividades de Computação Gráfica — DCT/UNIFESP.

Todos os exercícios são páginas HTML autocontidas com WebGL2: basta abrir o
arquivo no navegador, sem instalação ou servidor.

| Arquivo | Conteúdo |
| --- | --- |
| `flor-robo-carro.html` | Cenas (flor, robô e carro) montadas com primitivas de triângulos |
| `exercicio1-bresenham-reta.html` | Lista 28/03 — ex. 1: traçado de retas com o algoritmo de Bresenham |
| `exercicio2-bresenham-triangulo.html` | Lista 28/03 — ex. 2: retas e triângulos com o algoritmo de Bresenham |

## Conversão matricial — retas (lista p/ 28/03)

Em ambos os exercícios a rasterização é feita pelo algoritmo de Bresenham
(aritmética inteira, válido para os 8 octantes). Cada pixel calculado é
desenhado com `gl.POINTS` de tamanho 1 — `GL_LINES` **não** é utilizado.
As coordenadas seguem a convenção clássica de `gluOrtho2D(0, w, 0, h)`, com a
origem `(0,0)` no canto inferior esquerdo da tela.

### Exercício 1 — `exercicio1-bresenham-reta.html`

Duas funções: `tracarLinha(x0, y0, x1, y1, cor)` e `alterarCor(indice)`.

- A reta inicial é `(0,0) - (0,0)` na cor azul.
- O 1º clique com o botão esquerdo define o ponto inicial e o 2º clique define
  o ponto final; a reta é traçada imediatamente na nova posição.
- As teclas `0` a `9` selecionam cores previamente indexadas e a reta é
  redesenhada na hora com a nova cor.

### Exercício 2 — `exercicio2-bresenham-triangulo.html`

Três funções: `tracarLinha`, `alterarCor` (do exercício 1) e
`tracarTriangulo(v0, v1, v2)`, que traça apenas as três linhas que formam o
triângulo.

- A figura inicial é a reta `(0,0) - (0,0)` na cor azul.
- Apenas uma figura é apresentada de cada vez: a figura anterior é apagada.
- Tecla `r` ou `R` ativa o traçado de retas (2 cliques);
  tecla `t` ou `T` ativa o traçado de triângulos (3 cliques seguidos).
- As teclas `0` a `9` alteram a cor da figura corrente.

### Cores indexadas

| Tecla | Cor | Tecla | Cor |
| --- | --- | --- | --- |
| 0 | azul (padrão) | 5 | ciano |
| 1 | vermelho | 6 | laranja |
| 2 | verde | 7 | roxo |
| 3 | amarelo | 8 | marrom |
| 4 | magenta | 9 | preto |
