# Dados CVM
Análise Financeira de Empresas de Capital Aberto no Brasil via Dados da CVM e Visualização em Tableau

## 1. Introdução e Contexto do Projeto

### Problema/Oportunidade
A CVM fornece os dados, mas eles estão em formatos brutos (XML, CSV para download, PDFs antigos) e espalhados, o que torna a coleta, limpeza e organização manual um processo demorado e propenso a erros. Este projeto pode ajudar a gerar insights para criar uma ferramenta que automatize essa coleta e padronização, permitindo análises comparativas rápidas entre empresas do mesmo setor, ao longo do tempo, ou em relação a benchmarks. Isso agiliza o processo de due diligence e a identificação de tendências.

### Ferramentas Utilizadas
- Python para converter os arquivos para a codificação UTF-8;
- SQL para organizar e filtrar parte dos dados;
- Tableau para visualização;
- GitHub para controle de versão e portfólio.

## 2. Coleta e Aquisição de Dados

### Fonte dos Dados
Dataset da CVM: https://dados.cvm.gov.br/dataset/cia_aberta-doc-dfp

### Método de Coleta
Download de arquivos CSV e utilização de scripts Python para conversão dos arquivos para a codificação UTF-8.

## 3. Análise Exploratória de Dados

### Primeiras Observações
Foi encontrado dados duplicados e com nomenclatura diferente para uma mesma conta (Ex.: Adiantamento a Fornecedor e Adiantamento a Fornecedores).


### Desafios Identificados
- Todos os arquivos estavam codificados em latin-1, formato que pode gerar complicações ao se trabalhar em pataformas como Google Cloud;
- Algumas contas estavam com variação de letra maiúscula e minúscula para uma mesma empresa ao longo dos anos (Ex.: Resultado antes dos Tributos sobre o Lucro e Resultado Antes dos Tributos sobre o Lucro), o que é um ponto de atenção para linguagens case sensitive;
- Algumas empresas apresentavam determinada conta para 2019 e não apresentava a mesma conta para 2020.

