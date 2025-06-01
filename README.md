# Dados CVM
Análise Financeira de Empresas de Capital Aberto no Brasil via Dados da CVM e Visualização em Tableau

## 1. Introdução e Contexto do Projeto

### Problema/Oportunidade
A CVM fornece os dados, mas eles estão em formatos brutos (XML, CSV para download, PDFs antigos) e espalhados, o que torna a coleta, limpeza e organização manual um processo demorado e propenso a erros. Este projeto pode ajudar a gerar insights para criar uma ferramenta que automatize essa coleta e padronização, permitindo análises comparativas rápidas entre empresas do mesmo setor, ao longo do tempo, ou em relação a benchmarks. Isso agiliza o processo de due diligence e a identificação de tendências.

### Ferramentas Utilizadas
- Python para converter os arquivos para a codificação UTF-8;
- SQL para organizar e filtrar parte dos dados;
- Microsoft Excel para remoção de duplicatas e união entre as tabelas dos diferentes períodos;
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
- Datas que variavam entre trimestres, semestres, final do ano, etc;
- Algumas contas estavam com o valores representados em milhares de reais outras contas estavam representadas em unidades;
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

Fórmula básica:

![CodeCogsEqn](https://github.com/user-attachments/assets/f80e8521-4e1b-4604-b47b-ea1b4430f55f)

Onde:
- EG = Endividamento geral
- PE = Passivo exigível
- AT = Ativo total

2) Liquidez Corrente - A Liquidez Corrente é um indicador financeiro que mede a capacidade de uma empresa de cumprir suas obrigações de curto prazo (dívidas) com seus ativos de curto prazo (disponibilidades). Em outras palavras, ela mostra quanto a empresa tem em ativos que podem ser convertidos em dinheiro rapidamente para pagar o que deve em menos de um ano. É um dos indicadores de liquidez mais populares e serve como um termômetro da solvência de curto prazo de uma organização.

Fórmula básica:

![CodeCogsEqn (1)](https://github.com/user-attachments/assets/aa196ae2-4fb3-4d6a-98da-e6bbb017e206)


Onde:
- LC = Liquidez corrente
- AC = Ativo circulante
- PC = Passivo circulante

3) Patrimônio Líquido - O Patrimônio Líquido representa o valor residual dos ativos de uma empresa depois que todos os seus passivos (dívidas e obrigações) foram pagos. Em termos mais simples, é a parte do capital da empresa que pertence, de fato, aos seus proprietários/acionistas. É o que resta para os acionistas se a empresa fosse liquidada e todos os seus credores fossem pagos.

Fórmula Básica:

![CodeCogsEqn (2)](https://github.com/user-attachments/assets/231ed095-f572-482f-8620-025ed169cc5a)


Ferramentas Utilizadas: Para o cálcula das novas features utilizou-se o Microsoft Excel.

## 5. Modelagem e Organização dos Dados

### Estruturação para o Tableau
Os dados foram transformados em um formato tabular otimizado para o Tableau e para facilitar a vizualização dos dados de todos os anos foi realizado a união entre as tabelas, excluindo as informações das empresas que não apresentaram os valores das contas para todos os anos (Ex.: apresentou ativo circulante em 2019, porém, sem valores para essa conta para 2020)

### Uso de SQL
Foi utilizado consultas SQL para filtrar os dados, onde foi possível obter valores diferentes de 0, com unidade em milhares e data adequada (final de dezembro de cada ano).

### Dicionário de Dados

![dicionario de dados CVM](https://github.com/user-attachments/assets/4838fbec-2495-48d9-9cd3-1bfc8b26d339)

## 6. Visualização e Dashboard no Tableau

### Objetivo da Visualização
Desenvolvimento de dashboards interativos no Tableau para facilitar a visualização de indicadores financeiros de empresas de capital aberto.

### Tipos de Gráficos
Gráficos de barras horizontais para comparações entre as empresas.

### Interatividade
Implementação de filtros dinâmicos por e período, valor e tipo de conta, permitindo que o usuário personalize sua análise.

## 7. Resultados e Insights Obtidos
   
### Principais Descobertas
É possível observar que as contas variam bastante de um ano para o outro, mudando sempre os nomes das empresas com os maiores valores que se encontram no topo do gráfico.

### Valor Gerado
O projeto facilita a tomada de decisão para investidores, permitindo uma análise rápida e visual do desempenho financeiro das empresas, sem a necessidade de processamento manual dos dados da CVM, além disso, facilita o desenvolvimento de ferramentas de automação para dados dos próximos anos, trazendo pontos importantes das etapas iniciais de limpeza, conversão e geração de novos atributos para análise.

### Resposta ao Problema/Oportunidade
Foi possível desenvolver metodologias para filtrar, limpar e organizar os dados vindos diretamente do site da CVM para facilitar o processo de automação da atividade.

## 8. Próximos Passos 

### Melhorias Futuras 
Inclusão de dados ESG, integração com ferramentas de machine learning para previsão de desempenho, automação total do processo de extração, tratamento e carregamento dos dados e criação de um modelo de scoring financeiro.

## 9. Acesso ao Projeto
### Link para o Repositório: 
- [Dados CVM](https://github.com/WalterMatheus/Dados_CVM)

### Link para o Dashboard no Tableau Public:
  
- [Indicadores financeiros](https://public.tableau.com/views/IndicadoresB3/AeP?:language=pt-BR&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
- [Ganhos/perdas antes dos impostos](https://public.tableau.com/views/EBTB3/Planilha1?:language=pt-BR&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
