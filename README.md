# Neon Swarm

Survivor de arena em neon feito do zero com **JavaScript puro e Canvas 2D**, sem engine e sem dependências. Você sobrevive a hordas cada vez maiores, escolhe upgrades a cada nível e enfrenta chefes.

<!-- Adicione um GIF da partida em docs/gameplay.gif e descomente a linha abaixo:
![Gameplay](docs/gameplay.gif)
-->

**Jogar online:** https://lauradeola.github.io/neon-swarm/

## Como jogar

| Ação | Controle |
|---|---|
| Mover | `WASD` ou setas (no celular, arraste o dedo) |
| Dash | `Espaço` (recarga de 1,2 s, invencível por um instante) |
| Pausar | `P` |
| Escolher upgrade | `1`, `2`, `3` ou clique |

O tiro é automático no inimigo mais próximo.

## O que tem no jogo

- **Inimigos:** perseguidores, rápidos, tanques, atiradores (mantêm distância), divisores (viram 3 ao morrer) e explosivos.
- **Chefes** a cada minuto, alternando entre um que atira anéis de projéteis e outro que dá investidas.
- **Hordas** que cercam o jogador a cada 35 s.
- **Armas e upgrades:** tiro múltiplo, perfuração, lâminas orbitais, pulso de energia e uma evolução que combina lâminas e pulso.
- **Itens:** cura, ímã de gemas e bomba de tela.
- **Recorde** salvo no navegador.

## Detalhes técnicos

- **Game feel:** aceleração e atrito no movimento, hit stop em mortes grandes, screen shake, flash ao acertar, rastro e zoom no dash, números de dano flutuantes.
- **Spatial hash** (células de 64 px) para colisão tiro-inimigo e separação entre inimigos, em vez de comparar todos com todos.
- **Bloom** feito reduzindo a imagem do canvas em duas escalas e somando de volta com composição aditiva. Funciona em qualquer navegador, sem WebGL.
- **Áudio sintetizado** com Web Audio, sem arquivos de som.
- **Passo de tempo limitado** (`dt` máximo de 50 ms) para a simulação não explodir quando a aba perde foco.

## Estrutura

```
index.html        página e ordem de carregamento dos scripts
css/style.css     estilos
js/core.js        canvas, estado global, teclado
js/data.js        upgrades e tipos de inimigo
js/audio.js       efeitos sonoros
js/spatial.js     spatial hash
js/bloom.js       pós-processamento
js/world.js       reset, início, partículas, escolha de upgrade
js/update.js      simulação de cada frame
js/render.js      desenho, HUD e telas
js/input.js       teclado, mouse e toque
js/main.js        inicialização e game loop
```

Os arquivos são scripts clássicos que compartilham estado global, carregados em ordem pelo `index.html`.

## Rodar localmente

```bash
git clone https://github.com/SEU-USUARIO/neon-swarm.git
cd neon-swarm
python3 -m http.server 8000
```

Abra `http://localhost:8000`.

## Deploy

O workflow em `.github/workflows/pages.yml` valida a sintaxe dos scripts e publica no GitHub Pages a cada push na `main`. Para ativar: **Settings → Pages → Source: GitHub Actions**.

## Próximos passos

- Migrar para módulos ES (ou TypeScript) com estado encapsulado, no lugar das variáveis globais.
- Separar as regras (dano, XP, spawn) da renderização para poder testá-las.
- Reaproveitar objetos (pooling) para reduzir coleta de lixo.
- Mais armas, chefes e personagens, com meta-progressão entre partidas.
- Bloom e distorção com shaders em WebGL.
- Opção para reduzir tremor de tela e flashes.

## Licença

MIT. Veja `LICENSE`.
