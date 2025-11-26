# 🚀 PySpark Big Data Pipeline: Análise e Otimização de Estatísticas do YouTube

**Descrição:** Projeto de Big Data ponta a ponta (E2E) desenvolvido em **PySpark** no Google Colab. O pipeline cobre ingestão de dados, ETL, Análise Exploratória (EDA), Engenharia de Features para Machine Learning, Modelagem de Regressão Linear para previsão de Engajamento, e otimização de performance de Joins e I/O.

## 📋 Tabela de Conteúdo

1. [Visão Geral do Projeto](#1-visão-geral-do-projeto)
2. [Ferramentas e Tecnologias](#2-ferramentas-e-tecnologias)
3. [Estrutura do Pipeline (Etapas)](#3-estrutura-do-pipeline-etapas)
4. [Módulos Notebooks](#4-módulos-notebooks)
5. [Como Executar o Projeto](#5-como-executar-o-projeto)
6. [Resultados e Conclusão](#6-resultados-e-conclusão)

---

## 1. Visão Geral do Projeto

Este projeto demonstra a aplicação de **PySpark** para processamento e análise de grandes volumes de dados de estatísticas de vídeos do YouTube. O foco principal é simular um pipeline de dados completo, desde a manipulação inicial dos arquivos até a aplicação de técnicas avançadas de Big Data, Machine Learning e otimização de performance.

## 2. Ferramentas e Tecnologias

| Área | Ferramenta / Tecnologia | Uso no Projeto |
| :--- | :--- | :--- |
| **Big Data Framework** | **PySpark (Apache Spark)** | Processamento distribuído, ETL e Computação In-Memory. |
| **Linguagem** | **Python** | Linguagem principal para desenvolvimento. |
| **Ambiente** | **Google Colab** | Ambiente de desenvolvimento e execução (Notebooks Jupyter). |
| **Armazenamento** | **Parquet** | Formato de arquivo colunar otimizado para I/O em Big Data. |
| **Análise** | **Spark SQL** | Consultas e operações de transformação de dados. |
| **Machine Learning** | **Spark MLlib** | Engenharia de Features, Regressão Linear. |

---

## 3. Estrutura do Pipeline (Etapas)

O projeto foi dividido em etapas modulares, garantindo a rastreabilidade e a organização do fluxo de trabalho.

### **Fase I: ETL (Extract, Transform, Load) e Análise**

| Etapa | Notebook Principal | Habilidades Demonstradas |
| :--- | :--- | :--- |
| **1. Ingestão e Armazenamento** | `leitura_escrita.ipynb` | Leitura de dados CSV, inferência e definição de Schema. **Conversão e escrita eficiente** em formato **Parquet**. |
| **2. Tratamento e Transformação** | `tratamento.ipynb` | Manipulação de valores nulos (preenchimento com **0** ou remoção). Conversão de tipos de dados (`Date`, `Integer`). Criação da *feature* **`Interaction`** (Likes + Comments + Views). Junção de múltiplas fontes de dados (Left Join e Join complexo). |
| **3. Análise Exploratória (EDA) e Agregação** | `agregacao.ipynb` | Cálculo de estatísticas descritivas (Média, Variância, Max, Min) agrupadas por `Keyword`. Análise de tendências temporais. Aplicação de **Window Functions (Funções de Janela)** para calcular médias acumulativas. |

---

### **Fase II: Machine Learning e Otimização**

| Etapa | Notebook Principal | Habilidades Demonstradas |
| :--- | :--- | :--- |
| **4. Engenharia de Features** | `preparacao.ipynb` | Extração de features temporais (`Year`, `Month`). Codificação de variáveis categóricas (**`StringIndexer`**). Criação de vetor de features (**`VectorAssembler`**). Aplicação de **Normalização** e **Redução de Dimensionalidade (PCA)** nos vetores. |
| **5. Modelagem de Machine Learning** | `preparacao.ipynb` | Treinamento de modelo de **Regressão Linear** (`LinearRegression`) para prever o número de `Comments` (Engajamento). Avaliação do modelo usando métrica **RMSE**. |
| **6. Otimização de Performance** | `otimizacao.ipynb` | Criação de Views Temporárias SQL. Comparação de Planos de Execução (`explain(extended=True)`). Demonstração de otimizações de I/O e computação com **Project Pushdown** e **Filter Pushdown**. Controle de particionamento (`coalesce`/`repartition`) para escrita e otimização do *Small Files Problem*. |

---

## 4. Módulos Notebooks

| Arquivo (`.ipynb`) | Foco Principal |
| :--- | :--- |
| `leitura_escrita.ipynb` | Ingestão de dados e conversão para Parquet. |
| `tratamento.ipynb` | Limpeza de dados, transformações e junção de múltiplas fontes. |
| `agregacao.ipynb` | Cálculos estatísticos, EDA e aplicação de Window Functions. |
| `preparacao.ipynb` | Engenharia de Features, Modelagem ML (Regressão Linear) e Avaliação (RMSE). |
| `otimizacao.ipynb` | Técnicas de otimização de Joins e gerenciamento de partições. |

---

## 5. Como Executar o Projeto

O projeto foi desenvolvido 100% no **Google Colab**.

1.  **Pré-requisitos:** Uma conta Google para acesso ao Google Colab.
2.  **Instalação:** Todos os notebooks iniciam com a instalação da biblioteca PySpark: `!pip install pyspark`.
3.  **Dados:** Os arquivos de dados CSV (não incluídos no repositório final) são necessários e devem ser carregados no ambiente de execução do Colab antes de rodar os notebooks de ETL.
4.  **Ordem de Execução:** Os notebooks devem ser executados sequencialmente para que os arquivos Parquet gerados em uma etapa sejam utilizados na etapa seguinte:
    * `leitura_escrita.ipynb` (Gera arquivos Parquet iniciais)
    * `tratamento.ipynb` (Gera arquivos Parquet tratados, ex: `videos-comments-tratados-parquet`)
    * `preparacao.ipynb` (Gera arquivos Parquet preparados para ML, ex: `videos-preparados-parquet`)
    * `agregacao.ipynb` (Lê os dados preparados e executa a EDA)
    * `otimizacao.ipynb` (Lê os dados tratados e os comentários para os testes de Join)

---

## 6. Resultados e Conclusão

Este projeto serviu como uma demonstração prática do poder do PySpark em todas as etapas de um projeto de Big Data. As principais conclusões foram:

* A conversão para o formato **Parquet** otimizou significativamente o tempo de leitura e a eficiência de armazenamento.
* A aplicação de técnicas de **Otimização (Pushdown)** resultou em planos de execução mais eficientes, fundamentais para a escalabilidade em grandes volumes de dados.
* O pipeline de Engenharia de Features provou ser eficaz para preparar dados não estruturados para um modelo de **Regressão Linear**, alcançando um **RMSE** de `43345.23` na previsão de Comentários, o que representa um ponto de partida para análises preditivas mais aprofundadas sobre o engajamento de vídeos.
