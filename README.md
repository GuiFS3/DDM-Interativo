# Drift Diffusion Model — Simulador Interativo

Um simulador interativo baseado em navegador para o **Modelo de Difusão por Drift (DDM)** — um framework matemático amplamente utilizado em psicologia cognitiva e neurociência para modelar processos de decisão entre duas alternativas.

Desenvolvido com HTML, CSS e JavaScript puro. Sem dependências, sem etapa de build, sem servidor necessário.

---

## Screenshot

> <img width="1259" height="748" alt="image" src="https://github.com/user-attachments/assets/68da32d1-bd46-470c-ada3-ebb746f49358" />


---

## O que é o Modelo de Difusão por Drift?

No DDM, a evidência se acumula ao longo do tempo como um passeio aleatório com ruído (um processo de Wiener com drift). A decisão é tomada quando a evidência acumulada ultrapassa um dos dois limites. O modelo captura o **trade-off entre velocidade e acurácia**: limites mais amplos levam a respostas mais lentas, porém mais precisas.

O simulador exibe:

| Painel | Conteúdo |
|---|---|
| **Superior** | Distribuição dos tempos de reação para respostas corretas (acertos no limite superior) |
| **Central** | Trajetórias individuais da evidência ao longo do tempo |
| **Inferior** | Distribuição dos tempos de reação para respostas incorretas (acertos no limite inferior) |

---

## Parâmetros

| Símbolo | Nome | Descrição |
|---|---|---|
| **v** | Drift rate | Velocidade e direção do acúmulo de evidência. Valores positivos favorecem o limite superior. |
| **a** | Threshold | Distância entre os dois limites de decisão. Maior = mais cauteloso. |
| **z** | Bias | Ponto de partida do acúmulo de evidência em relação ao ponto médio (0 = neutro). |
| **σ** | Ruído | Desvio padrão do ruído de difusão dentro de cada tentativa. |
| **ndt** | Tempo de não-decisão | Tempo (s) consumido por percepção e execução motora, adicionado a cada TR. |
| **n** | Tentativas | Número de trajetórias simuladas exibidas no gráfico. |

---

## Funcionalidades

- **Renderização em tempo real** — cada ajuste no slider re-executa a simulação e redesenha o canvas imediatamente
- **Eixo de tempo fixo** — o eixo x sempre vai de 0 a 1,5 s, facilitando a comparação entre configurações
- **Distribuições por KDE** — densidades dos tempos de reação calculadas por estimativa de densidade por kernel (regra de Scott)
- **Estatísticas ao vivo** — contagem de corretas/incorretas, acurácia % e TR médio atualizados a cada renderização
- **Layout responsivo** — desktop: gráfico à esquerda, controles à direita; mobile: gráfico no topo, sliders abaixo
- **PRNG com semente** — a mesma semente é reutilizada ao arrastar os sliders; clique em **↺ Nova simulação** para gerar novas trajetórias
- **Autocontido** — arquivo HTML único, sem bibliotecas externas, funciona offline

---

## Como usar

### Opção 1 — Abrir diretamente

Baixe o arquivo [`index.html`](index.html) e abra-o em qualquer navegador moderno. Só isso.

### Opção 2 — GitHub Pages

1. Faça um fork ou clone deste repositório
2. Acesse **Settings → Pages**
3. Defina a fonte como branch `main`, pasta `/ (root)` ou `/ddm-web`
4. Acesse a URL gerada

### Opção 3 — Servidor local (opcional)

```bash
cd ddm-web
python3 -m http.server 8080
# abra http://localhost:8080
```

---

## Notas de Implementação

- **PRNG**: [Mulberry32](https://gist.github.com/tommyettinger/46a874533244883189143505d203312c) — rápido, com semente, 32 bits
- **Amostras normais**: transformação de Box-Muller
- **Largura de banda do KDE**: regra de Scott — `1,06 × σ × n^(−1/5)`
- **Simulação**: discretização de Euler-Maruyama com `dt = 0,001 s`, limite de segurança de 10.000 passos por tentativa
- **Renderização no canvas**: compatível com HiDPI (escalonamento via `devicePixelRatio`)

---

## Estrutura de Arquivos

```
ddm-web/
└── index.html   # app completo — HTML + CSS + JS em um único arquivo
└── README.md    # este arquivo
```

---

## Referência

Ratcliff, R., & McKoon, G. (2008). The diffusion decision model: Theory and data for two-choice decision tasks. *Neural Computation, 20*(4), 873–922. https://doi.org/10.1162/neco.2008.12-06-420

---

## Autor

**Guilherme da Silva Freitas**  
Agosto de 2026  
[guilherme.f@ufrgs.br](mailto:guilherme.f@ufrgs.br)  
[orcid.org/0009-0004-4002-3175](https://orcid.org/0009-0004-4002-3175)

---

## Licença

MIT — livre para usar, modificar e distribuir com atribuição.
