# Roteiro do vídeo (4 min 30 s)

**Tema:** Do sinal ao espectro: removendo o zumbido de 60 Hz de uma voz
**Apresentação:** Reuel Andre Amarro Santos

**Preparação antes de gravar:**
- Deixe o notebook já executado no Colab, com o `voz.wav` enviado.
- Grave a tela com o som do sistema ligado, para que os áudios apareçam no vídeo.

---

## 0:00–0:30 · Abertura

**Tela:** título do notebook.

> "Olá, eu sou o Reuel, de Engenharia da Computação. Neste trabalho eu gravei a minha voz, somei o zumbido da rede elétrica, de 60 hertz, e usei Fourier e Laplace para analisar, filtrar e explicar o filtro."

**Tela:** tocar o áudio "voz + zumbido" (Etapa 2) por uns 3 segundos.

> "É esse zumbido grave que a gente vai tirar."

---

## 0:30–1:20 · Etapa 1: Série de Fourier

**Tela:** grade com N = 1, 5, 15 e 51.

> "Antes do sinal real, o caso clássico: a onda quadrada. Ela é ímpar, então só tem senos, com b_n igual a 4 sobre n pi para n ímpar. Somando mais harmônicos, a aproximação melhora."

**Tela:** tabela de coeficientes e matriz identidade.

> "Os coeficientes numéricos batem com a fórmula, e a matriz identidade mostra a ortogonalidade da base. Na forma complexa, D_n vale menos 2j sobre n pi e dá o mesmo resultado."

**Tela:** zoom do Gibbs.

> "E aqui o fenômeno de Gibbs: perto do salto sempre sobra um pico de cerca de 9%, não importa quantos termos eu some. Guardem isso, porque ele volta na Etapa 3."

---

## 1:20–2:20 · Etapa 2: FFT

**Tela:** gráfico no tempo com zoom de 100 ms.

> "Agora a minha voz, amostrada a 16 kHz, então Nyquist é 8 kHz. Na pausa, sobra essa ondulação com período de 16,7 milissegundos, que é 1 sobre 60."

**Tela:** espectro com zoom de 0 a 500 Hz.

> "Na frequência fica claro: três raias finas em 60, 120 e 180 hertz, que são o zumbido. A minha voz tem o pitch perto de 96 hertz, com harmônicos em 192, 284, 377."

**Tela:** saída "A gravação original já tinha zumbido real da rede?".

> "Um detalhe interessante: a minha gravação original já tinha um pouco de zumbido real em 60 hertz, captado pelo microfone."

**Tela:** espectrograma.

> "No espectrograma, o zumbido são essas três linhas contínuas, até no silêncio, e a voz aparece palavra por palavra."

---

## 2:20–3:30 · Etapa 3: Filtro e reconstrução

**Tela:** |H(jω)|.

> "Como o ruído é estreito, usei três notches com a mesma largura de 2 hertz. Isso importa porque o segundo harmônico da minha voz passa perto de 180 hertz, e um notch mais largo cortaria a voz."

**Tela:** tabela de SNR e atenuação das raias.

> "Eu faço a FFT, multiplico por H de j ômega e volto para o tempo com a transformada inversa. As raias caem entre 62 e 95 dB, e o SNR sai de menos 8,5 para mais 18,5 dB."

**Tela:** tocar "antes" e depois `voz_filtrada_fase_zero.wav`.

> "Ouçam o antes... e o depois."

**Tela:** gráfico do zumbido residual.

> "O pouco que sobra fica no primeiro segundo: a FFT emenda o fim do sinal com o começo, e isso cria um salto, o mesmo tipo de descontinuidade do Gibbs. A versão em tempo real, feita com a transformada bilinear, tem um transitório parecido, de uns 0,8 segundos."

---

## 3:30–4:20 · Etapa 4: Laplace e polos/zeros

**Tela:** H(s) no sympy.

> "Aplicando Laplace na equação diferencial do circuito, chego nesta H de s."

**Tela:** mapa de polos e zeros.

> "Os zeros ficam sobre o eixo j ômega, em 60, 120 e 180 hertz, e por isso o ganho zera ali. Os polos ficam todos na mesma coluna, em menos 6,28, bem pertinho do eixo. Como têm parte real negativa, o sistema é estável."

**Tela:** gráfico do produto de distâncias.

> "Essa distância de 6,28 define duas coisas: a largura de 2 hertz do vale e a constante de tempo de 160 milissegundos, que é exatamente o transitório que a gente viu. É a mesma história contada no plano s e no espectro."

---

## 4:20–4:30 · Fechamento

> "Resumindo: Fourier mostrou onde estava o ruído, o filtro removeu, e Laplace explicou o comportamento do filtro. O código e os áudios estão no GitHub. Obrigado!"
