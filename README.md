# Previsão de Resultados da Premier League usando Aprendizado de Máquina

### Autor
Edson Menin - 171947@upf.br

## Introdução

Este projeto tem como objetivo prever os resultados das partidas da Premier League, a liga de futebol da Inglaterra, utilizando técnicas de Aprendizado de Máquina. O objetivo é explorar um conjunto de dados históricos das partidas e desenvolver modelos capazes de prever se um determinado jogo resultará em vitória do time da casa, vitória do time visitante ou empate.

## Dataset

A fonte de dados utilizada nesta pesquisa é o site https://www.football-data.co.uk, que fornece dados históricos sobre partidas de futebol em várias ligas ao redor do mundo. O dataset utilizado consiste em informações sobre partidas de futebol realizadas nas últimas doze temporadas da liga principal da Inglaterra, a Premier League, tendo como data final 25/05/2023, no qual corresponde ao ultimo jogo antes da rodada final.

O dataset inclui informações como data e horário das partidas, equipes que jogaram em casa e fora, número de gols marcados e sofridos por cada equipe, resultado final (vitória para a equipe da casa, vitória para a equipe visitante ou empate) e estatísticas de chutes a gol para cada equipe.

As colunas do dataset foram obtidas a partir do arquivo "notes.txt" disponível no seguinte link https://www.football-data.co.uk/notes.txt. O dataset contém as seguintes colunas:

- Div: Divisão da liga (E0 para Premier League)
- Date: Data da partida
- HomeTeam: Time da casa
- AwayTeam: Time visitante
- FTHG: Gols marcados pelo time da casa
- FTAG: Gols marcados pelo time visitante
- FTR: Resultado da partida (H para vitória do time da casa, A para vitória do time visitante, D para empate)
- HS: Chutes a gol do time da casa
- AS: Chutes a gol do time visitante

## Pré-processamento dos Dados

Inicialmente, realizamos uma validação para verificar se havia valores faltantes em algumas colunas consideradas importantes para a análise, como Div, Date, HomeTeam, AwayTeam, FTHG, FTAG, FTR, HS e AS. Felizmente, todas essas colunas estavam devidamente preenchidas, sem valores faltantes.

Em seguida, mapeamos os valores da coluna FTR, que indicam o resultado da partida (H = Home Win, D = Draw, A = Away Win), para valores numéricos (0 = Home Win, 1 = Draw, 2 = Away Win). Essa conversão numérica facilita a análise e o treinamento do nosso modelo.

Para aprimorar o treinamento do modelo, criamos duas colunas adicionais: HomeTeam_id e AwayTeam_id. Cada equipe no conjunto de dados recebeu um identificador único, permitindo uma melhor representação e compreensão da rede.

Também adicionamos uma nova coluna chamada Season para indicar a temporada correspondente a cada partida. Para determinar a temporada, consideramos a data da partida e o conhecimento geral de que as temporadas de futebol geralmente começam no segundo semestre do ano anterior e terminam no primeiro semestre do ano seguinte. Para isso, implementamos um loop que percorre as linhas do DataFrame, adicionando a temporada correspondente a cada partida.

Para identificar os clubes que foram promovidos para a Premier League em cada temporada de 2011 a 2022, criamos um dicionário. Em seguida, adicionamos duas colunas ao DataFrame, chamadas HomePromoted e AwayPromoted, ambas inicializadas com o valor 0. Depois, implementamos um loop que percorre cada partida no DataFrame. Para cada partida, verificamos se a equipe da casa ou a equipe visitante está presente no dicionário de clubes promovidos para a temporada correspondente. Se alguma das equipes estiver presente, a coluna correspondente (HomePromoted ou AwayPromoted) é atualizada com o valor 1, indicando que a respectiva equipe foi promovida para a Premier League naquela temporada. Essa abordagem permite identificar automaticamente e com precisão quais equipes em cada partida foram recém-promovidas para a Premier League na temporada correspondente.

Por fim, adicionamos para cada equipe em cada temporada, o número de vitórias, derrotas e empates, o número de gols marcados e sofridos, o número de chutes a gol e o número total de partidas disputadas na temporada. Além disso, incluímos uma coluna chamada "Round" para categorizar a rodada em que cada partida foi realizada, o que será utilizado para representar graficamente os dados em nossa pesquisa. Esses dados serão utilizados para avaliar o desempenho das equipes ao longo da temporada.

Também foi realizado um segundo treinamento e teste, no qual foi feita uma alteração no dataset, utilizando a codificação 0 = Home Win e 1 = Draw ou Away Win. Neste teste, o objetivo era identificar apenas se o time da casa ganhou ou perdeu a partida, sem levar em consideração o empate.

## Modelos Utilizados

Optou-se por utilizar neste trabalho a rede MLP em razão do seu treinamento de forma supervisionada com o algoritmo de retropropagação de erro.

## Treinamento

Para treinamento da rede, foram utilizados as seguintes informações sobre cada partida: os IDs dos times da casa e visitante, número de vitórias e derrotas, número de empates, gols marcados, gols sofridos, total de chutes, total de jogos de cada equipe e se a equipe foi promovida ou não para a Premier League. A lista Y, por outro lado, contém as saídas esperadas para cada partida, ou seja, o resultado final do jogo (FTR, na sigla em inglês).

## Resultados

No teste A, foi obtido uma acurácia de 54.03\% e F1 Score de 54.03\% nos dados de teste, enquanto no conjunto de treinamento, o modelo obteve um desempenho com acurácia de 53.62\%.

Comparativo de acertos e erros do Teste A

![Comparativo de acertos e erros](https://raw.githubusercontent.com/EdsonMenin/tcc/main/PREV_BAR_1.png)

Para o teste B, houve uma melhoria significativa nos resultados obtidos, no qual alcançou uma  acurácia de 64.47\% e F1 Score de 64.47\% nos dados de teste, e no conjunto de treinamento, o modelo obteve o mesmo desempenho, com acurácia de 64.47\%.

Comparativo de acertos e erros do Teste B

![Comparativo de acertos e erros](https://raw.githubusercontent.com/EdsonMenin/tcc/main/PREV_BAR_2.png)

## Implementação

O código-fonte completo do projeto pode ser encontrado no repositório do projeto no GitHub, disponível em https://github.com/EdsonMenin/tcc.
