# PDS – Parte 2

Mini Projeto Integrador: **Análise Multidomínio de um Sinal e de um Sistema** (Processamento Digital de Sinais, IFPB).
Aplicação escolhida: **circuito RC passa-baixas** (R = 1,6 kΩ, C = 1 µF, τ = 1,6 ms, fc ≈ 99,5 Hz).

## Estrutura

```
PDS-Parte-2/
├── relatorio/                  # relatório final (a preencher)
├── simulacoes/                 # simulações dos tópicos da Parte 2 (a preencher)
│   ├── fourier/
│   ├── dft-fft/
│   ├── nyquist-aliasing/
│   ├── janelamento/
│   ├── laplace/
│   └── transformada-z/
├── mini-projeto/
│   ├── codigo/
│   │   └── mini_projeto_rc.ipynb   # <- notebook principal (10 etapas)
│   ├── dados/                      # sinal amostrado (CSV)
│   ├── figuras/                    # 14 figuras geradas pelo notebook (PNG)
│   └── requirements.txt
├── resultados/                 # tabelas finais (CSV)
└── README.md
```

## Como executar (VS Code)

1. Instale as dependências: `pip install -r mini-projeto/requirements.txt`
2. Abra `mini-projeto/codigo/mini_projeto_rc.ipynb` no VS Code e selecione um kernel Python.
3. Execute **Run All** (as células dependem umas das outras, de cima para baixo).

> As figuras vão para `mini-projeto/figuras/`, os dados para `mini-projeto/dados/` e as tabelas para `resultados/`.
> Os caminhos são relativos à pasta do notebook (`mini-projeto/codigo/`); o VS Code usa essa pasta por padrão.

## Mapa do notebook × roteiro

| Etapa | Conteúdo | Figuras |
|---|---|---|
| 1 | Aplicação: circuito RC, H(s), τ, fc | 01 |
| 2 | Geração do sinal (50 Hz + 400 Hz), entrada × saída | 02 |
| 3 | Amostragem, Nyquist (fs = 2000 Hz) | 03 |
| 4 | FFT: tempo, magnitude, fase, resolução | 04 |
| 5 | Aliasing (fs = 2000, 1000, 700, 500 Hz) + prova matemática | 05, 06 |
| 6 | Janelamento: retangular × Hann × Hamming, resolução e faixa dinâmica | 07, 08, 09 |
| 7 | Modelo contínuo: polo, plano-s, Bode, respostas temporais | 10, 11 |
| 8 | Modelo discreto (ZOH): polo, plano-z, h[n], estabilidade | 12 |
| 9 | Relação z = e^(sTs), estabilidade nos dois planos | 13, 14 |
| 10 | Discussão (11 perguntas) + tabela-resumo | — |

## Parâmetros que podem ser alterados

No início das Etapas 1 e 2: `R`, `C`, `f1`, `f2`, `A1`, `A2`, `phi1`, `phi2`, `T_obs` e `NOISE_STD` (ruído de sensor).
Os textos da Etapa 10 citam os valores atuais; se mudar os parâmetros, revise esses números.
