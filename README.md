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
