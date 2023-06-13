# Previsão - Séries Temporais

![capa_st](https://github.com/Cassiophysics/Previsao_Serie_Temporal/assets/108491443/92ed3c47-1b80-4db1-a3c5-9af5faa056bd)

Este projeto tem como objetivo aplicar técnicas de ciência de dados para prever a produção de energia elétrica. A previsão é baseada em séries temporais que nada mais são que dados coletados ao longo do tempo, onde cada observação é registrada em uma ordem cronológica.

Tais dados foram obtidos em: https://fred.stlouisfed.org/series/IPG2211A2N

Embora a limpeza de dados e a engenharia de recursos sejam etapas importantes na análise de dados de séries temporais, o foco principal deste projeto foi a compreensão dos modelos ARIMA e XGBoost e como eles podem ser aplicados na análise e previsão de séries temporais.

Assim, o projeto apresenta uma visão detalhada dos modelos ARIMA e XGBoost, explicando seus conceitos teóricos e como eles podem ser implementados na prática. O objetivo é fornecer um conhecimento sólido e prático sobre esses modelos e como eles podem ser aplicados na análise de séries temporais em diferentes áreas.

O modelo ARIMA (AutoRegressive Integrated Moving Average) é um modelo estatístico que permite a previsão de séries temporais estacionárias, ou seja, séries temporais que possuem uma média e variância constantes ao longo do tempo. Já o modelo XGBoost (Extreme Gradient Boosting) é uma técnica de aprendizado de máquina que pode ser aplicada na análise de séries temporais, entre outras áreas.

A seguir uma breve explicação de como funciona os modelos utilizados neste projeto:

# ARIMA

Cada termo do ARIMA representa uma parte específica do modelo.

Autoregressive (AR): refere-se a um modelo que utiliza valores passados da série temporal para prever valores futuros. O termo AR representa o número de valores passados que são usados para prever o valor futuro.

Integrated (I): refere-se à ordem de integração da série temporal. A ordem de integração é o número de vezes que a série precisa ser diferenciada para se tornar estacionária.

Moving Average (MA): refere-se a um modelo que utiliza erros passados para prever valores futuros. O termo MA representa o número de erros passados que são usados para prever o valor futuro.

A ordem do modelo ARIMA é representada por (p, d, q), onde p é a ordem do modelo autoregressivo, d é a ordem de diferenciação e q é a ordem do modelo de média móvel. Juntos, esses termos ajudam a modelar e prever valores futuros de uma série temporal.

Quando a série temporal apresenta sazonalidade passamos a utilizar o SARIMA (Seasonal Autoregressive Integrated Moving Average) que é uma extensão do modelo ARIMA. Assim como o modelo ARIMA, o SARIMA também é representado por (p, d, q), mas inclui mais três termos para modelar a sazonalidade: P, D e Q. O termo P representa a ordem do modelo autoregressivo sazonal, D representa a ordem de diferenciação sazonal e Q representa a ordem do modelo de média móvel sazonal.

O modelo SARIMA é utilizado quando há uma clara sazonalidade nos dados. Ao incluir os termos de sazonalidade, o modelo SARIMA é capaz de prever valores futuros que levam em consideração a sazonalidade presente na série temporal.

A ordem do modelo SARIMA é representada por (p, d, q)(P, D, Q)s, onde s é o período da sazonalidade. Juntos, esses termos ajudam a modelar e prever valores futuros de uma série temporal com sazonalidade.

# XGBoost

Já o modelo XGBoost (Extreme Gradient Boosting) é uma técnica de aprendizado de máquina que pode ser aplicada para previsão de séries temporais. O XGBoost utiliza uma abordagem baseada em árvore de decisão, onde cada árvore aprende a prever os valores da série temporal a partir dos dados de entrada. 

Embora o XGBoost não tenha sido desenvolvido especificamente para lidar com problemas de séries temporais, pode ser adaptado para essa finalidade por meio da transformação do problema de séries temporais em um problema de aprendizado supervisionado.

O problema de séries temporais envolve a previsão de valores futuros com base em dados históricos. No entanto, o XGBoost é projetado para prever valores com base em características do conjunto de dados, em vez de dependências temporais.

Para transformar o problema de séries temporais em um problema de aprendizado supervisionado, é necessário criar recursos (features) a partir dos dados de séries temporais. Isso pode ser feito usando por exemplo a técnica de janelas deslizantes. 

A ideia por trás da criação de recursos (features) a partir de janelas deslizantes é que os valores anteriores da série temporal fornecem informações relevantes para prever os valores futuros. Então, ao aplicar a técnica de janelas deslizantes, selecionamos um tamanho de janela e movemos essa janela ao longo da série temporal, coletando um subconjunto de valores para cada posição. Esse subconjunto é então usado como uma observação no conjunto de dados de treinamento.

Uma vez que os recursos foram criados, o problema de séries temporais pode ser transformado em um problema de aprendizado supervisionado, onde cada exemplo de treinamento consiste em um vetor de recursos e uma saída correspondente.

O XGBoost pode ser treinado com os exemplos de treinamento transformados, e os modelos resultantes podem ser usados para fazer previsões em novos dados de séries temporais. É importante notar que, embora essa abordagem possa funcionar bem em muitos casos, ela pode não capturar todas as complexidades das séries temporais, especialmente se houver padrões temporais complexos ou variações sazonais.


## Estrutura do Projeto:

# Análise Exploratória

Aqui foi realizado uma análise exploratória dos dados de maneira automatizada onde foi possível verificar e compreender diversas características dos dados.

Em seguida foi feita uma decomposição temporal da série através de gráficos de modo a identificar padrões, tendências e sazonalidade.

Também foi executado testes estatísticos para detectar se a série é estacionária ou não.

# Pré Processamento

Aqui foi realizado um corte nos dados, pois a série temporal apresenta valores demasiadamente antigos que poderiam induzir ruídos desnecessários.

A série temporal foi separada em dados de treino e teste, com o teste contendo os últimos 12 meses.
Foi aplicado a diferenciação e a diferenciação sazonal para transformar a série temporal em estacionária, pois o modelo ARIMA requer que a série temporal seja estacionária.

Uma análise dos gráficos ACF e PACF foi efetuada para tentar descobrir os melhores parâmetros do modelo ARIMA de forma manual.

# Modelagem

Nesta parte foi utilizado o Auto Arima da biblioteca pmdarima para encontrar os melhores parâmetros de maneira automatizada ajudando a reduzir a complexidade do processo de ajuste do modelo.

Também foi feita uma análise para identificar a adequação dos resíduos do modelo, se há autocorrelação não explicada e heteroscedasticidade nos erros.

O modelo foi treinado para fazer previsões tanto dentro da amostra como fora da amostra e fez-se uso da Validação Walk Forward para que o modelo seja avaliado de maneira mais realista.

Para o XGBoost foi utilizada a biblioteca Sktime que é ideal para lidar com problemas de séries temporais. Também foi utilizada a Validação Walk-Forward, além da otimização dos hiperparâmetros.

# Avaliação Final

Uma comparação dos modelos finais do ARIMA e do XGBoost foi feita por gráficos e diversas métricas diferentes, onde o modelo ARIMA apresentou resultados um pouco melhores do que o Modelo XGBoost.


