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
- Algumas contas estavam com variação de letra maiúscula e minúscula para uma mesma empresa ao longo dos anos (Ex.: Resultado antes dos Tributos sobre o Lucro em 2019 e Resultado Antes dos Tributos sobre o Lucro em 2020), o que é um ponto de atenção para linguagens case sensitive;
- Algumas contas estavam com a conta em milhares de reais outras contas estavam representadas em unidades.
- Algumas contas de ativos foram apresentadas com o valor igual a 0;
- Algumas empresas apresentavam determinada conta para 2019 e não apresentava a mesma conta para 2020.

## 4. Limpeza e Pré-processamento de Dados
   
### Tratamento de Dados Ausentes/Duplicados
- Para as empresas quee não possuíam dados para as contas Ativo Circulante, Ativo Total, Passivo Circulante, Passivo Nao Circulante, Passivo Total e Resultado Antes dos Tributos sobre o Lucro, suas informações foram excluídas do dataset;
- Para os dados duplicados, o tratamento foi de remoção das duplicatas.

### Padronização e Transformação
Foi unificado os dados de todos os anos das empresas que possuíam as contas desejadas em uma única tabela para facilitar a análise no Tableau.

### Engenharia de Features
Foram criadas para este projeto 3 novas features:

1) Endividamento Geral - O Endividamento Geral é um indicador que mede a proporção dos ativos de uma empresa que é financiada por capital de terceiros, ou seja, por dívidas. Ele nos diz quanto do patrimônio da empresa (seus bens e direitos) é sustentado por recursos que não pertencem aos acionistas, mas sim a bancos, fornecedores, governos, etc.

Fórmula Básica:

![CodeCogsEqn](https://github.com/user-attachments/assets/f80e8521-4e1b-4604-b47b-ea1b4430f55f)

Onde:
- EG - Endividamento geral
- PE - Passivo exigível
- AT - Ativo total

2)

Ferramentas Utilizadas: Mencione as bibliotecas Python (Pandas, NumPy) e as operações SQL que foram cruciais aqui.
