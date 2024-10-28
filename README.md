# Mineração Estatística de Dados - Projeto Final

Alunos:
* Ismael Alves Lima
* Matheus Victor Alves Braga Maciel

Este repositório contém todos os scripts utilizados para a elaboração do projeto final da disciplina de Mineração Estatística de Dados. A descrição completa do projeto pode ser encontrada [aqui](https://sig-arq.ufpb.br/arquivos/202402107810c26801618ae90755bae0d/projeto.pdf).

## Descrição dos Processos

### Coleta dos Dados

Primeiramente foram coletados via download, os arquivos `.csv` disponíveis na API do Sistema de Informações Contábeis e Fiscais do Setor Público Brasileiro (SICONFI), no intervalo entre 2016 e 2023. Semelhante a imagem abaixo:

![Consulta_SICONFI](https://github.com/user-attachments/assets/b312974b-11b4-48fc-a536-8ea0e578afc6)

Depois, os arquivos `.csv` foram salvos em uma pasta no Google Drive para posterior tratamento.

### Agregação 

Para facilitar as etapas de tratamento dos dados, os arquivos `.csv` foram agregados em um só, filtrando as cidades e impostos solicitados na descrição do projeto. Além disso, foram removidos dos `.csv` as entradas de dados referentes a valores totais anuais e previsões.

Os detalhes mais específicos relacionados ao código podem ser obtidos em `Data_Mining_Coleta_e_Agregação.ipynb`.

### Tratamento

Com respeito ao tratamento dos dados, a principal tarefa realizada foi de preenchimento de dados faltantes, pois para algumas cidades, estavam faltando datas de coleta. Portanto foi necessário preencher completamente as entradas faltantes.

Para isso, primeiramente foram identificadas as datas faltantes para cada cidade e imposto, utilizando uma série temporal de referência entre os Janeiro de 2016 e Dezembro de 2023. Sabendo quais datas estavam faltando, facilmente foram preenchidas as variáveis não númericas, para as númericas foi necessária a utilização de ferramentas preditivas.

Como dito anteriormente, para as variáveis numéricas, `População` e `Valor`, foi necessário o uso de ferramentas de predição. No caso da `População` utilizamos regressão linear, devido a natureza da própria variável. Em contrapartida, para o `Valor`, correspondente a quantidade coletada de um imposto em uma cidade em um período de tempo, utilizamos a biblioteca `Prophet`, de modo a se beneficiar das propriedades das séries temporais dos valores, isto é, tendência, sazonalidade, ciclo e ruído.

Os detalhes mais específicos relacionados ao código podem ser obtidos em `Data_Mining_Preenchimento.ipynb`.

### Regressão

Para a etapa de regressão, foi utilizado o `Prophet` para modelar as séries temporais dos valores dos impostos em cada cidade. Esse processo envolveu:

* Preparo dos Dados: Os dados foram filtrados para cada cidade e imposto, sendo renomeados para os formatos exigidos pelo `Prophet` (`ds` para `data` e `y` para `valor`).
* Treinamento e Validação: O processo de seleção do parâmetro `K` envolveu a divisão dos dados em partes para determinar o número de períodos ideais para o treinamento do modelo. Foram gerados diferentes modelos para valores de `K` entre 2 e 6, e calculado o erro médio quadrático (MSE) para cada um, selecionando o menor MSE.
* Previsão Final: Após definir o valor de `K`, o modelo foi treinado com os dados correspondentes e ajustado para prever os valores futuros, abrangendo 24 meses à frente (2024 e 2025).
* Armazenamento dos Resultados: As previsões finais foram consolidadas em um novo DataFrame, df_final, incluindo variáveis como Ano, Mês, Instituição e Conta, e o resultado foi exportado como `Dados_Regressao.csv` para posterior carregamento na ferramenta de visualização.

Esses detalhes podem ser visualizados em maior profundidade no arquivo `Data_Mining_Regression.ipynb`.

### Clusterização

Nessa etapa, foram utilizados diferentes métodos de clusterização, além de técnicas de redução de dimensionalidade, num processo que envolveu:

* Preparo dos Dados: O conjunto de dados foi agregado com soma, utilizando as variáveis `Instituição`, `Conta` e `Ano`. Depois, foi feito o cálculo da váriação percentual para cada ano e a criação de um conjunto de dados onde cada `Conta_Ano` representa a váriação percentual do imposto anual para uma cidade, e ao mesmo tempo, uma coordenada $X_n$ para uma cidade.
* Aplicação da Clusterização (raw): A clusterização foi feita utilizando primeiramente os algoritmos AGNES (bottom-up) e DIANA (top-down), com o número de clusters `K` definido como 4.
* Aplicação da Clusterização + PCA: Essa etapa foi feita utilizando o algoritmo K-Means e uma redução de dimensionalidade com PCA de 2 fatores.
* Análise de disciminante e adição de novas cidades: Foram escolhidas cinco novas cidades para aplicar a análise de discriminante e estabelecer a que grupo cada nova cidade pertence. Para essas novas cidades, os mesmos processos anteriores foram realizados.
* Vizualização: A visualização dos resultados de clusterização foi feita utilizando grafos, com o auxílio da biblioteca `NetworkX`.

Esses detalhes podem ser visualizados em maior profundidade no arquivo `Data_Mining_Clustering.ipynb`.

### Modelagem Dimensional

Etapa extra, foi feita com o objetivo de simplificar a elaboração do Dashboard no Qlik. Os dados foram separados nas seguintes dimensões:

* Geografia: Diz respeito ao Código do IBGE, nome da cidade, estado e região.
* Tipo de Imposto: Cada tipo de imposto que foi coletado.
* Tempo: A granularidade de coleta de cada imposto, anual ou mensal.

Os detalhes mais específicos relacionados ao código podem ser obtidos em `Data_Mining_Modeling.ipynb`.
