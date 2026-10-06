# Processamento Digital de Sinais (PDS) — Roteiro 1

Repositório com as simulações, gráficos e resultados do **Roteiro 1 de Processamento Digital de Sinais**, desenvolvido no **IFPB – Campus Campina Grande** (NAPMT), 2026.

O trabalho percorre os fundamentos de sinais e sistemas em tempo discreto: da definição de sinal até a convolução como filtragem digital. Ele termina com um **mini projeto** que simula uma cadeia completa de aquisição e processamento de sinais (temperatura ambiente ao longo de 48 horas).

> Cada tópico segue o mesmo roteiro: **resumo conceitual → formulação matemática → exemplo → simulação → resultados → discussão**. O relatório completo (em LaTeX/PDF) traz a teoria e as demonstrações; este repositório reúne o código e os gráficos gerados.

---

## Sumário

- [Tecnologias](#tecnologias)
- [Estrutura do repositório](#estrutura-do-repositório)
- [Como executar](#como-executar)
- [Conceitos abordados](#conceitos-abordados)
- [Principais resultados](#principais-resultados)
- [Mini projeto](#mini-projeto)
- [Referências](#referências)

---

## Tecnologias

- **Python 3**
- **NumPy** — geração de sinais, somatórios e convolução (`np.convolve`)
- **Matplotlib** — gráficos contínuos (`plot`) e discretos (`stem`)
- **Jupyter Notebook** — ambiente das simulações

> As simulações também podem ser reproduzidas em GNU Octave ou MATLAB.

## Estrutura do repositório

| Tópico | Assunto | Notebook |
|:-:|---|---|
| 1 | Sinais contínuos e discretos | [`tópico_1.ipynb`](Roteiro%201/t%C3%B3pico_1.ipynb) |
| 2 | Amostragem e aliasing | [`Amostragem.ipynb`](PDS-Parte-1/Simula%C3%A7%C3%B5es/Amostragem.ipynb) |
| 3 | Quantização e resolução | [`Quantização e Resolução.ipynb`](PDS-Parte-1/Simula%C3%A7%C3%B5es/Quantiza%C3%A7%C3%A3o%20e%20Resolu%C3%A7%C3%A3o.ipynb) |
| 4 | Sequências fundamentais | [`Sequencias_Fundamentais.ipynb`](PDS-Parte-1/Simula%C3%A7%C3%B5es/Sequencias_Fundamentais.ipynb) |
| 5 | Operações com sinais | [`Operações com sinais.ipynb`](PDS-Parte-1/Simula%C3%A7%C3%B5es/Opera%C3%A7%C3%B5es%20com%20sinais.ipynb) |
| 6 | Energia e potência | [`Energia_e_Potencia.ipynb`](PDS-Parte-1/Simula%C3%A7%C3%B5es/Energia_e_Potencia.ipynb) |
| 7 | Sistemas discretos | [`Sistemas_Discretos.ipynb`](PDS-Parte-1/Simula%C3%A7%C3%B5es/Sistemas_Discretos.ipynb) |
| 8 | Sistemas LTI | [`Sistemas_LTI.ipynb`](PDS-Parte-1/Simula%C3%A7%C3%B5es/Sistemas_LTI.ipynb) |
| 9 | Convolução discreta | [`Convolução Discreta.ipynb`](PDS-Parte-1/Simula%C3%A7%C3%B5es/Convolu%C3%A7%C3%A3o%20Discreta.ipynb) |
| 10 | Convolução como filtragem | [`Convolução_Como_Filtragem.ipynb`](PDS-Parte-1/Simula%C3%A7%C3%B5es/Convolu%C3%A7%C3%A3o_Como_Filtragem.ipynb) |
| — | Mini projeto | _(adicionar link)_ |

## Como executar

```bash
# 1. Clone o repositório
git clone https://github.com/GuiMendespy/PDS.git
cd PDS

# 2. Instale as dependências
pip install numpy matplotlib jupyter

# 3. Abra os notebooks
jupyter notebook
```

Os notebooks também podem ser abertos diretamente no Google Colab ou no VS Code.

---

## Conceitos abordados

### 1. Sinais contínuos e discretos

Um sinal é uma função que carrega informação sobre um fenômeno físico. Em tempo contínuo, $x(t)$ com $t \in \mathbb{R}$; em tempo discreto, $x[n]$ com $n \in \mathbb{Z}$, definido apenas nos instantes $t_n = nT_s$.

$$x[n] = x(nT_s) = A\sin(\Omega_0 n + \phi), \qquad \Omega_0 = 2\pi f_0 T_s$$

### 2. Amostragem

Conversão de $x(t)$ em $x[n]$ por registros espaçados de $T_s$ (com $f_s = 1/T_s$). Pelo **Teorema de Nyquist–Shannon**, a reconstrução fiel exige

$$f_s > 2 f_{max}$$

Se violado, ocorre **aliasing**: altas frequências aparecem como baixas, de forma irreversível.

$$f_{aliased} = \lvert f_0 - k f_s \rvert, \quad k \in \mathbb{Z}$$

### 3. Quantização e resolução

Discretiza a **amplitude** do sinal. Com $N$ bits há $L = 2^N$ níveis:

$$\Delta V = \frac{V_{ref}}{2^N}, \qquad x_q(t) = \text{round}\!\left(\frac{x(t)}{\Delta V}\right)\Delta V, \qquad e_{max} = \pm\frac{\Delta V}{2}$$

Mais bits significam passo menor e menor ruído de quantização.

### 4. Sequências fundamentais

| Sequência | Definição |
|---|---|
| Impulso unitário | $\delta[n] = 1$ se $n=0$; $0$ caso contrário |
| Degrau unitário | $u[n] = 1$ se $n \ge 0$; $0$ caso contrário |
| Rampa unitária | $r[n] = n\,u[n]$ |
| Exponencial | $a^n u[n]$ — decai se $\lvert a\rvert<1$, cresce se $\lvert a\rvert>1$ |
| Senoide discreta | $\cos(\Omega_0 n + \phi)$ |

Relação importante: $\delta[n] = u[n] - u[n-1]$.

### 5. Operações com sinais

- **Deslocamento:** $x[n-n_0]$ (atraso) e $x[n+n_0]$ (avanço)
- **Inversão temporal:** $x[-n]$
- **Escalonamento de amplitude:** $A\,x[n]$
- **Soma:** $x_1[n] + x_2[n]$

### 6. Energia e potência

$$E_x = \sum_{n=-\infty}^{\infty} \lvert x[n]\rvert^2, \qquad P_x = \lim_{N\to\infty}\frac{1}{2N+1}\sum_{n=-N}^{N}\lvert x[n]\rvert^2$$

- **Sinal de energia:** $0 < E_x < \infty$ (e $P_x = 0$)
- **Sinal de potência:** $0 < P_x < \infty$ (e $E_x = \infty$)

### 7. Sistemas discretos

Um sistema é um operador $y[n] = \mathcal{T}\{x[n]\}$, classificado por cinco propriedades: **memória**, **causalidade**, **linearidade**, **invariância no tempo** e **estabilidade BIBO**.

| Sistema | Memória | Causal | Linear | Invariante | BIBO |
|---|:-:|:-:|:-:|:-:|:-:|
| $y[n]=2x[n]$ | não | sim | sim | sim | sim |
| $y[n]=x[n]+x[n-1]$ | sim | sim | sim | sim | sim |
| $y[n]=x^2[n]$ | não | sim | **não** | sim | sim |
| $y[n]=x[n+1]$ | sim | **não** | sim | sim | sim |
| $y[n]=n\,x[n]$ | não | sim | sim | **não** | **não** |

### 8. Sistemas LTI

Todo sistema LTI é totalmente caracterizado por sua resposta ao impulso $h[n]$:

$$y[n] = \sum_{k=-\infty}^{\infty} x[k]\,h[n-k] = x[n] * h[n]$$

- **Causal** se $h[n] = 0$ para $n < 0$
- **BIBO estável** se $\sum_{n}\lvert h[n]\rvert < \infty$

### 9. Convolução discreta

Operação de quatro etapas: **inverter**, **deslocar**, **multiplicar** e **somar**. O comprimento da saída é

$$N_y = N_x + N_h - 1$$

Exemplo: $x[n]=\{1,2,1\}$ e $h[n]=\{1,1\}$ resultam em $y[n]=\{1,3,3,1\}$.

### 10. Convolução como filtragem

A resposta ao impulso funciona como um filtro digital:

| Filtro | $h[n]$ | Efeito |
|---|---|---|
| **Passa-baixas** (média móvel de $M$ pontos) | $\frac{1}{M}\sum_{k=0}^{M-1}\delta[n-k]$ | Suaviza e atenua ruído |
| **Passa-altas** (diferença finita) | $\delta[n]-\delta[n-1]$ | Destaca bordas e variações rápidas |

---

## Principais resultados

| Tópico | Resultado |
|---|---|
| Amostragem | Sinal de 10 Hz com $f_s = 100$ Hz é reconstruído fielmente; com $f_s = 12$ Hz aparece como **2 Hz** (aliasing) |
| Quantização | $N = 3, 4, 8$ bits dão $\Delta V = 125{,}0;\ 62{,}5;\ 3{,}9$ mV; erro RMS cai de 33,9 mV para 1,2 mV |
| Energia/potência | $\{1,2,3,2,1\}$ tem $E=19$; $(0{,}7)^n u[n]$ tem $E\to 1{,}9608$; $\cos(\pi n/4)$ tem $P = 0{,}5$ |
| Sistemas LTI | $(0{,}5)^n u[n]$ é estável (soma = 2); $(1{,}2)^n u[n]$ é instável (soma diverge) |
| Convolução | Resultado manual coincide com `np.convolve` |
| Filtragem | Média móvel recupera a senoide base; diferenciador isola o ruído |

> Os gráficos correspondentes (sinais contínuos × discretos, aliasing, "escada" da quantização, stem plots das sequências, saídas dos filtros etc.) estão nos respectivos notebooks.

---

## Mini projeto

Modelagem e processamento da **temperatura ambiente de uma estação meteorológica ao longo de 48 h**:

$$x(t) = T_0 + A_1\cos(2\pi f_1 t + \phi_1) + A_2\cos(2\pi f_2 t + \phi_2)$$

| Etapa | Configuração |
|---|---|
| Modelo | $T_0 = 25\,°C$, $A_1 = 6\,°C$ (ciclo de 24 h), $A_2 = 1{,}2\,°C$ (ciclo de 12 h) |
| Amostragem | $T_s = 300$ s (uma amostra a cada 5 min); $f_s \approx 3{,}33\times10^{-3}$ Hz, muito acima de Nyquist |
| Quantização | Faixa de 10 a 40 °C: 4 bits ($\Delta = 1{,}875\,°C$) e 8 bits ($\Delta \approx 0{,}117\,°C$) |
| Ruído | Gaussiano branco, $\sigma = 0{,}8\,°C$ |
| Filtro LTI | Média móvel de $M = 7$ amostras (janela de 35 min) |

**Conclusões:** o filtro reduziu a variância do ruído por um fator ≈ $M$ ($0{,}64 \to \approx 0{,}091\,°C^2$), ao custo de um atraso de $(M-1)/2 = 3$ amostras (15 min) e de leve atenuação dos picos. Melhorias possíveis: componentes sazonais e de tendência no modelo; filtros FIR por janelamento ou Butterworth (IIR) no lugar da média móvel.

---

## Referências

1. OPPENHEIM, A. V.; SCHAFER, R. W. *Processamento em Tempo Discreto de Sinais*. 3. ed. São Paulo: Pearson, 2012.
2. PROAKIS, J. G.; MANOLAKIS, D. G. *Digital Signal Processing: Principles, Algorithms, and Applications*. 4th ed. Pearson Prentice Hall, 2007.
3. LATHI, B. P. *Sinais e Sistemas Lineares*. 2. ed. Porto Alegre: Bookman, 2006.
4. HAYKIN, S.; VAN VEEN, B. *Sinais e Sistemas*. Porto Alegre: Bookman, 2001.
5. DINIZ, P. S. R.; DA SILVA, E. A. B.; NETTO, S. L. *Digital Signal Processing: System Analysis and Design*. 2nd ed. Cambridge University Press, 2010.

---

**Autor:** Guilherme — IFPB, Campus Campina Grande