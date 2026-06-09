# Global Solution - AstraVision: Applied Computer Vision

## Integrantes do grupo

- Aline Fernandes Zeppelini - RM97966

- Camilly Breitbach Ishida - RM551474

- Julia Leite Galvão - RM550201

---

## Definição do problema

O AstraVision é um módulo de Visão Computacional desenvolvido para auxiliar missões espaciais na análise preliminar de amostras coletadas em superfícies planetárias, asteroides ou outros corpos celestes.

Em missões espaciais, a quantidade de amostras que pode ser transportada para análise em laboratórios terrestres é limitada. Dessa forma, torna-se importante realizar uma triagem inicial ainda durante a missão, identificando quais amostras possuem maior potencial científico.

Para resolver esse problema, foi desenvolvido um sistema de classificação de imagens baseado em Redes Neurais Convolucionais (CNNs), capaz de identificar automaticamente o tipo de amostra presente em uma imagem.

A solução está diretamente relacionada ao contexto da Indústria Espacial, pois permite automatizar parte do processo de análise visual de materiais encontrados em ambientes extraterrestres, reduzindo o tempo necessário para tomada de decisão e auxiliando operadores e cientistas na seleção das amostras mais relevantes para coleta e estudo.

---

## Dataset utilizado

### Origem das imagens

O conjunto de dados foi construído pela equipe utilizando imagens públicas obtidas em bancos de imagens gratuitos (Pexels) disponíveis na internet e também de um dataset pronto (Kaggle) sobre rochas. As imagens foram selecionadas manualmente para representar visualmente materiais semelhantes aos encontrados em cenários de exploração espacial.

### Classes utilizadas

Foram definidas quatro classes:

| Classe | Descrição |
|---------|---------|
| Gelo | Superfícies congeladas e formações de gelo |
| Rocha | Rochas e minerais |
| Solo Arenoso | Solos claros com textura arenosa |
| Solo Escuro | Solos escuros e vulcânicos |

### Quantidade de imagens

| Classe | Quantidade de Imagens |
|---------|---------|
| Gelo | 40 |
| Rocha | 39 |
| Solo Arenoso | 40 |
| Solo Escuro | 33 |
| Total | 152 |

### Divisão dos Dados

Foi utilizada a divisão:

- 70% Treinamento
- 15% Validação
- 15% Teste

A divisão foi realizada automaticamente pelo TensorFlow utilizando uma semente fixa para garantir reprodutibilidade.

### Pré-processamento

As seguintes etapas foram aplicadas:

- Redimensionamento para 224x224 pixels;
- Conversão automática para RGB;
- Normalização dos pixels para o intervalo [0,1];
-Data Augmentation:
  - Flip horizontal;
  - Rotação aleatória;
  - Zoom aleatório;
  - Ajuste de contraste.

Essas técnicas aumentaram a variabilidade do conjunto de treinamento e ajudaram a reduzir overfitting.

> Observação: as imagens do dataset nesse reposítório compõem apenas uma pequena parte do dataset utilizado no projeto, pois devido às limitações de tamanho de arquivo do Github, não foi possível colocar todas
---

## Treinamento das CNNs

Foram desenvolvidas duas arquiteturas de CNN implementadas manualmente utilizando TensorFlow/Keras, sem utilização de modelos pré-treinados.

### CNN 1

Arquitetura composta por:

- Camada Conv2D (16 filtros)
- MaxPooling
- Camada Conv2D (32 filtros)
- MaxPooling
- Camada Conv2D (64 filtros)
- MaxPooling
- Flatten
- Dense (128 neurônios)
- Dense (4 neurônios)

Características:

- Menor complexidade;
- Menor quantidade de parâmetros;
- Menor risco de overfitting.

### CNN 2

Arquitetura composta por:

- Camada Conv2D (32 filtros)
- MaxPooling
- Camada Conv2D (64 filtros)
- MaxPooling
- Camada Conv2D (128 filtros)
- MaxPooling
- Dropout
- Flatten
- Dense (128 neurônios)
- Dense (4 neurônios)

Características:

- Arquitetura mais profunda;
- Maior quantidade de parâmetros;
- Maior capacidade de aprendizado;
- Maior risco de instabilidade com datasets pequenos.

Durante o treinamento foram monitoradas:

- Accuracy
- Loss
- Validation Accuracy
- Validation Loss

Ao longo das épocas foi possível observar a evolução do aprendizado das redes e comparar seu comportamento.

---

## Avaliação dos modelos

Foram utilizadas:

- Accuracy
- Loss
- Matriz de Confusão
- Análise qualitativa de erros

### Resultados obtidos

| Modelo | Accuracy |
|---------|---------|
| CNN 1 | 95% |
| CNN 2 | 45% |

A CNN 1 apresentou excelente capacidade de generalização, classificando corretamente a maioria das amostras das quatro classes.

Também foram realizados testes com imagens inéditas, demonstrando que o modelo consegue identificar corretamente materiais semelhantes aos utilizados no treinamento.

Já a CNN 2 apresentou instabilidade durante o treinamento e maior dificuldade de generalização, classificando incorretamente diversas imagens de solo como gelo. Esse comportamento foi evidenciado pela matriz de confusão e pelos elevados valores de loss observados durante o treinamento.

---

## Comparação entre as arquiteturas

A comparação dos resultados demonstrou que a CNN 1 apresentou desempenho significativamente superior.

### CNN 1

Vantagens:

- Estrutura mais simples;
- Menor número de parâmetros;
- Treinamento mais estável;
- Melhor generalização.

### CNN 2

Vantagens:

- Maior capacidade teórica de aprendizado.

Limitações:

- Maior complexidade;
- Necessidade de mais dados;
- Instabilidade durante o treinamento;
- Overfitting.

Conclui-se que, para o tamanho do dataset utilizado, a CNN 1 apresentou melhor equilíbrio entre complexidade e capacidade de generalização, sendo escolhida como modelo final do AstraVision.

--- 

## Modelo Treinado

O arquivo do modelo treinado não foi incluído diretamente no repositório devido às limitações de tamanho do GitHub.

O modelo pode ser obtido através do link abaixo:

**Modelo CNN 1 (AstraVision):**
https://www.dropbox.com/scl/fi/y4ao5i93000pe07dj6tbk/astravision_weights.weights.h5?rlkey=ubgtdi388fnrns6qhrjwsm9fu&st=ht34iyiv&dl=0

---

## Link para o vídeo explicativo

https://youtu.be/Hn_nydXUQcQ


