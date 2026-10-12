# Do sinal ao espectro: removendo o zumbido de 60 Hz de uma voz

Sistematização da disciplina **Métodos Matemáticos** (CEUB).
Autor: **Reuel Andre Amarro Santos**, Engenharia da Computação (trabalho individual).

[Abrir no Google Colab](https://colab.research.google.com/github/REUELAndre/sistematizacao-fourier-laplace/blob/main/sistematizacao_fourier_laplace.ipynb)

## Resumo

Este projeto usa a minha gravação de voz (8,9 s, pitch perto de 96 Hz) contaminada por zumbido da rede elétrica (60, 120 e 180 Hz). O trabalho analisa, filtra e reconstrói o sinal e depois modela o filtro como um sistema linear.

| Etapa | Conteúdo | Resultado |
|---|---|---|
| 1 · Série de Fourier | Onda quadrada, coeficientes, forma complexa, fenômeno de Gibbs | Overshoot converge para 8,95% do salto |
| 2 · FFT | Espectro, espectrograma, Nyquist e aliasing | Zumbido identificado como três raias estreitas; a gravação já tinha zumbido real em 60 Hz |
| 3 · Filtragem | Três notches com largura de 2 Hz, Y = H(jω)·X, FFT inversa | Raias atenuadas de 62 a 95 dB; SNR de −8,5 dB para +18,5 dB (t > 1 s) |
| 4 · Laplace | H(s), resposta ao impulso, polos/zeros e estabilidade | Todos os polos em Re{s} = −6,28 (estável); τ ≈ 160 ms |

## Estrutura

```
├── sistematizacao_fourier_laplace.ipynb   # notebook completo (código + interpretação)
├── voz.wav                                # gravação original (sinal usado)
├── audios/
│   ├── voz_limpa.wav
│   ├── voz_com_zumbido.wav
│   ├── voz_filtrada.wav                   # notch H(jω) via FFT
│   ├── voz_filtrada_fase_zero.wav         # |H(jω)|², melhor resultado para ouvir
│   └── voz_filtrada_tempo_real.wav        # versão causal (bilinear)
├── roteiro_video.md
├── requirements.txt
└── README.md
```

## Como executar

**No Google Colab:**
1. Abra o notebook pelo link acima.
2. No painel **Arquivos**, envie o `voz.wav` para a pasta principal.
3. Clique em *Ambiente de execução → Executar tudo*.

**Na sua máquina:**
```bash
pip install -r requirements.txt
jupyter notebook sistematizacao_fourier_laplace.ipynb
```

**Observações:**
- Sem o `voz.wav`, o notebook gera uma voz sintética (modelo fonte-filtro) e executa do mesmo jeito.
- O zumbido e o ruído são somados por código, com semente fixa, então os resultados são reprodutíveis.

## Vídeo

Link:(https://youtu.be/eqs-wpBw2rQ)
