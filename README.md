# Sistema de Recomendação de Receitas por Regressão

Trabalho prático desenvolvido para a disciplina de Inteligência Artificial da Universidade Federal de São João del-Rei (UFSJ).

O objetivo do projeto é sugerir receitas que possam ser preparadas integralmente com os ingredientes disponíveis na casa do usuário, reduzindo o desperdício de alimentos e auxiliando na tomada de decisão sobre o que cozinhar.

---

## Engenharia de Atributos e Abordagem

Diferentemente de abordagens tradicionais baseadas em regras simples ou classificação binária, este sistema modela a recomendação como um problema de **regressão supervisionada**.

### Modelagem do Target (`AcceptanceScore`)

Para simular o comportamento e o interesse de um usuário, foi criada a métrica **AcceptanceScore**, um valor contínuo entre `0.0` e `1.0`.

O score é calculado por meio de uma combinação linear ponderada, atribuindo peso igual aos seguintes critérios:

* **Tempo Total de Preparo:** penaliza receitas com mais de 60 minutos de duração por meio de uma função de decaimento linear.
* **Categorias Preferidas:** bonifica receitas pertencentes a categorias de interesse do usuário, como *Desserts*, *Breakfast*, *Vegetables* e *South American*.
* **Avaliação da Receita (`AggregatedRating`):** utiliza a nota média histórica da receita normalizada.
* **Popularidade (`ReviewCount`):** considera a quantidade de avaliações recebidas pela receita na plataforma.

---

## Pipeline de Dados e Algoritmo

O modelo foi desenvolvido utilizando o algoritmo **Random Forest Regressor**.

A escolha desse algoritmo se deve à sua robustez diante da alta dimensionalidade gerada pelo processo de codificação das variáveis categóricas e à sua capacidade de reduzir problemas de overfitting em tarefas de regressão.

O pipeline foi estruturado com o uso do **ColumnTransformer** da biblioteca Scikit-Learn, garantindo que todas as etapas de pré-processamento fossem aplicadas corretamente e sem vazamento de dados entre os conjuntos de treino e teste.

---

## Performance do Modelo

Após a divisão da base de dados em:

* **80% para treinamento**
* **20% para testes**

foram obtidos os seguintes resultados:

| Métrica                          | Resultado |
| -------------------------------- | --------: |
| RMSE (Root Mean Squared Error)   |    0.0071 |
| R² (Coeficiente de Determinação) |    0.9988 |

Os resultados indicam que o modelo conseguiu reproduzir com alta precisão a função heurística utilizada para representar as preferências do usuário, tornando-se capaz de inferir o nível de aceitação de receitas inéditas ou ainda não avaliadas.

---

## Requisitos e Dependências

Para executar o projeto localmente ou em ambiente de nuvem, é necessário possuir Python 3 e as seguintes bibliotecas:

* **pandas**: manipulação e limpeza de dados.
* **numpy**: operações matemáticas e vetorizadas.
* **scikit-learn**: pipeline de processamento, codificação de atributos e treinamento do modelo.
* **kagglehub**: download automatizado do conjunto de dados.
* **isodate**: conversão de durações no padrão ISO 8601 para minutos.

Instalação das dependências:

```bash
pip install pandas numpy scikit-learn kagglehub isodate notebook
```

---

## Como Executar

### Opção 1: Google Colab

O projeto foi originalmente desenvolvido no Google Colab.

Como o notebook utiliza o `kagglehub`, o conjunto de dados é baixado automaticamente e armazenado em cache durante a execução.

1. Faça upload do arquivo `Sistema_IA_para_Receitas.ipynb` para o Google Colab.
2. Execute as células sequencialmente.
3. Ao final da execução, utilize o prompt interativo para informar os ingredientes disponíveis.

### Opção 2: Execução Local

1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
```

2. Crie e ative um ambiente virtual.

3. Instale as dependências:

```bash
pip install pandas numpy scikit-learn kagglehub isodate notebook
```

4. Inicie o Jupyter Notebook:

```bash
jupyter notebook
```

5. Abra o arquivo `Sistema_IA_para_Receitas.ipynb` e execute as células.

---

## Estrutura do Projeto

```text
.
└── Sistema_IA_para_Receitas.ipynb
```

### Arquivo Principal

* **Sistema_IA_para_Receitas.ipynb**

  * Download do dataset do Kaggle.
  * Parsing de ingredientes utilizando expressões regulares (Regex).
  * Tratamento de dados ausentes.
  * Construção do atributo `AcceptanceScore`.
  * Treinamento e avaliação do modelo Random Forest.
  * Interface interativa para recomendação de receitas.

---

## Desenvolvedores

* André Arcuri Martins - https://github.com/kojumax
* Gabriel da Silva Souza - https://github.com/Gabriel-Souza18
* Giulia Mota Apinagés dos Santos - https://github.com/Giulia-Mota
* Guilherme De Luca Testoni Neiva Pereira - https://github.com/delucaguilherme
* José Vitor Santos Alves - https://github.com/JoseVitor2004
