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
