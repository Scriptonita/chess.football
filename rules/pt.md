# Chess.Football — Regras do jogo

> Jogo de estratégia por turnos para dois jogadores que combina o movimento das peças do xadrez com o objetivo do futebol: marcar mais golos que o adversário lançando a bola contra o seu rei.

---

## 1. Visão geral

- **Jogadores**: 2 (brancas e pretas).
- **Objetivo**: marcar mais golos que o adversário. Marca-se um golo quando um passe alcança a casa do rei adversário.
- **Turnos**: alternados. Em cada turno, o jogador ativo dispõe de um número de **Pontos de Ação (PA)** configurável ao criar a partida (entre **1 e 5**; por defeito, 5).

---

## 2. O tabuleiro

O tabuleiro é retangular: **9 colunas (A–I) × 12 linhas (1–12)**, num total de 108 casas.

<img src="../assets/gameboard.png" alt="Tabuleiro de Chess.Football" width="400">

### As áreas

Cada equipa tem uma **área de 5×2 casas** no seu lado do campo:

- **Área branca**: colunas C–G, linhas 1–2.
- **Área preta**: colunas C–G, linhas 11–12.

Regras sobre as áreas:

1. O **rei só pode mover-se dentro da sua própria área**. Nunca pode sair, nem mesmo conduzindo a bola.
2. As **restantes peças da mesma equipa não podem entrar na sua própria área**.
3. As peças adversárias **podem** entrar livremente na área contrária.
4. O **rei é intocável**: nenhuma peça adversária pode pisar a sua casa. Apenas a bola (mediante um passe) pode alcançá-lo.

---

## 3. As peças

Cada equipa dispõe de **8 peças** com movimentos inspirados no xadrez:

| Peça          | Quantidade | Posição inicial (brancas) | Função                       |
|---------------|------------|---------------------------|------------------------------|
| Rei (K)       | 1          | E2                        | Baliza / objetivo            |
| Dama (Q)      | 1          | E6                        | Médio                        |
| Torre (R)     | 2          | A2, I2                    | Defesas laterais             |
| Bispo (B)     | 2          | D3, F3                    | Defesas centrais             |
| Cavalo (N)    | 2          | C5, G5                    | Avançados                    |

As peças pretas colocam-se em posição espelhada no lado oposto do campo.

### Movimentos

| Peça    | Movimento                                          | Salta peças? | Restrição de área                |
|---------|----------------------------------------------------|--------------|----------------------------------|
| Rei     | 1 casa em qualquer direção                         | Não          | **Apenas dentro da sua área**    |
| Dama    | Casas ilimitadas em qualquer direção               | Não          | Não pode entrar na sua área      |
| Torre   | Casas ilimitadas na horizontal ou vertical         | Não          | Não pode entrar na sua área      |
| Bispo   | Casas ilimitadas na diagonal                       | Não          | Não pode entrar na sua área      |
| Cavalo  | Em forma de L (2+1)                                | **Sim**      | Não pode entrar na sua área      |

Regras adicionais:

- **Bloqueio**: todas as peças exceto o cavalo são bloqueadas por outras peças no seu caminho. O cavalo salta sobre qualquer peça.
- **Não podes mover-te para uma casa ocupada por uma peça tua.**
- **Podes mover-te para a casa de uma peça adversária apenas se essa peça tiver a bola** (entrada/desarme) — **exceto o rei adversário, que é intocável**.

---

## 4. Estrutura do turno

Em cada turno, o jogador ativo recebe os **Pontos de Ação (PA)** definidos ao criar a partida — um valor configurável entre **1 e 5** (5 por defeito). Cada ação custa 1 PA.

### Pontapé inicial

Quem dá o pontapé inicial do primeiro turno depende do modo de jogo:

- **Partida online (PvP)**: as **brancas** começam sempre.
- **Treino (vs IA)**: começa o lado **escolhido pelo jogador** ao criar a partida.

Em ambos os casos o pontapé inicial é dado pela **dama** da equipa que começa, que inicia com a bola na sua casa central. Os pontapés iniciais **após um golo** seguem a regra da [secção 7](#7-depois-de-um-golo) (começa a equipa que sofreu o golo).

### Ações disponíveis

1. **Mover** — deslocar uma peça tua para uma casa válida.
   - Cada peça só pode mover-se **uma vez por turno**.
   - Se a peça tiver a bola, esta desloca-se com ela (*condução*).

2. **Passar** — a peça com a bola lança-a para uma casa de destino.
   - A peça não se move, apenas a bola viaja.
   - A bola voa seguindo o padrão direcional da peça.
   - As **peças da tua equipa** no trajeto **não afetam o passe**: a bola voa por cima delas.
   - Uma **peça adversária** no trajeto **interceta o passe** (ou é **golo** se essa peça for o rei). Os passes do **cavalo** são a exceção: saltam sobre tudo, conta apenas a casa de destino.

3. **Terminar o turno** — finalizar o turno voluntariamente, cedendo os PA restantes.

### Quando termina o turno

- Ao chegar a 0 PA.
- Quando o jogador termina o turno voluntariamente.
- Ao ocorrer uma **interceção** ou um **golo** (fim forçado).

### Restrições

- Uma peça que já se moveu neste turno não pode voltar a mover-se.
- Uma peça **pode mover-se e passar no mesmo turno** (2 PA no total).
- Podes mover várias peças diferentes no mesmo turno.
- Só podes fazer um passe se uma das tuas peças tiver a bola.

---

## 5. A bola

A bola está sempre numa casa do tabuleiro. Pode estar **solta** ou **em posse** de uma peça.

### Como ganhar a posse

- **Captura no trajeto**: se uma peça linear (rei, dama, torre ou bispo) se move e a bola está no seu trajeto, recolhe-a automaticamente.
- **Captura no destino**: qualquer peça (incluindo o cavalo) que termine o seu movimento na casa da bola solta apanha-a.
- **Entrada (desarme)**: ao moveres-te para a casa de uma peça adversária que tem a bola, roubas-lhe a posse e a peça adversária é deslocada para uma casa ortogonal adjacente livre.
  - **Não podes desarmar o rei adversário.**
  - O deslocamento segue uma **prioridade fixa**: direita → esquerda → cima → baixo. A peça adversária ocupa a primeira casa ortogonal livre nessa ordem.
  - A casa que o atacante **acaba de deixar** conta como livre para o deslocamento: se as outras 4 ortogonais estiverem ocupadas mas o atacante vier de uma delas, o adversário fica nessa.
  - Se após aplicar o anterior **não restar nenhuma casa livre** para o deslocado, a entrada **não é permitida** (movimento ilegal).

### Condução

Quando uma peça com a bola se move, a bola viaja com ela. O custo é 1 PA, igual a um movimento normal. O rei pode conduzir a bola, mas **continua sem poder sair da sua área**.

### Passar

- A peça com a bola lança-a para uma casa válida sem se mover.
- Os destinos do passe seguem o mesmo padrão direcional que o movimento da peça. As peças no trajeto **não eliminam casas da lista de destinos** (podes apontar para qualquer casa do raio direcional), mas se uma peça adversária se encontrar no caminho **intercetará o passe** — ou, se essa peça adversária for o rei, será **golo**. Ver [Interceção](#interceção) e [Como marcar um golo](#6-como-marcar-um-golo).
- Custo: 1 PA.

### Interceção

Quando uma peça **não cavalo** realiza um passe, a bola viaja em linha reta. Se uma peça adversária (que não seja o seu rei) estiver nesse caminho:

- A peça adversária **mais próxima do passador** interceta a bola.
- O turno do jogador que passou **termina imediatamente** (os PA passam a 0).

> **Importante**: os passes do cavalo **não podem ser intercetados**. A bola "salta" até ao destino exato.

---

## 6. Como marcar um golo

Marca-se golo quando um **passe** alcança a casa do rei adversário:

- **Passes lineares** (dama, torre, bispo, rei): a bola viaja pelo caminho. A primeira peça adversária que encontra:
  - Se for o **rei adversário** → **GOLO!** (a bola para na casa do rei e o turno termina).
  - Se for **outra peça adversária** → interceção.
- **Passes de cavalo**: importa apenas a casa exata de destino. Se o destino for o rei adversário → **GOLO!**

> Truque tático: um passe dirigido **para além do rei** em linha reta também é golo — a bola para no rei por ser a primeira peça adversária do caminho.

---

## 7. Depois de um golo

1. O marcador atualiza-se (+1 para a equipa que marcou).
2. O tabuleiro é reposto na formação inicial.
3. A equipa **que sofreu** o golo começa: a sua dama inicia com a bola no centro.
4. A equipa que sofreu o golo joga o primeiro turno depois do golo.

---

## 8. Final do jogo

O jogo termina quando uma equipa alcança o **número de golos objetivo** definido ao criar a partida.

- O objetivo de golos é **configurável entre 1 e 10** (por defeito, 3).
- Assim que um lado atinge esse número, o jogo termina imediatamente e esse lado é declarado vencedor.
- **Não existem empates**: como o objetivo de golos exige sempre um marcador, há sempre um vencedor.

---

## 9. Regras especiais do rei

### 9a. O rei não pode reter a bola mais de um turno

O rei pode receber a bola e mantê-la durante esse turno, mas **deve largá-la antes de terminar o seu turno seguinte**.

- Se o rei terminar o turno com a bola, fica marcada a condição *o rei deve largar*.
- No **turno seguinte** dessa equipa, o rei é obrigado a passar a bola.
- Se o jogador não passou com o rei ao chegar ao último PA, o sistema **larga a bola automaticamente** numa casa **adjacente livre** do rei (consumindo esse último PA). Tentam-se primeiro as 4 casas ortogonais e, se estiverem todas ocupadas, as 4 diagonais.
- O indicador do último PA ativo transforma-se numa coroa (👑) para avisar o jogador.

**Motivo**: evita que um jogador em vantagem estacione a bola com o seu rei para ganhar tempo.

### 9b. Recuo para o guarda-redes

Uma vez que o rei larga a bola (voluntária ou automaticamente), **nenhuma peça da mesma equipa pode devolver-lhe a bola** até que uma peça adversária a toque.

- Quando o rei passa, fica bloqueado como recetor.
- A casa do rei é excluída dos destinos válidos de passe para os seus colegas.
- O bloqueio é levantado quando uma **peça adversária toca na bola** (por interceção, desarme ou golo).

**Motivo**: reflete a regra de recuo para o guarda-redes no futebol — evita que a equipa passe repetidamente para o rei para perder tempo.

---

## 10. Glossário rápido

- **PA (Pontos de Ação)**: configurável entre 1 e 5 ao criar a partida (5 por defeito); cada ação custa 1 PA.
- **Conduzir**: mover uma peça com a bola.
- **Passar**: lançar a bola sem mover a peça.
- **Entrada / Desarme**: moveres-te para a casa de um adversário com a bola para lha roubar.
- **Interceção**: peça adversária que captura um passe no seu trajeto; o turno do passador termina.
- **Golo**: passe que alcança a casa do rei adversário.
- **Área**: zona de 5×2 casas em cada extremo do campo; só o rei defensor pode pisá-la.

---
