# Trabalho-2-FIA---Machine-Learning-com-CNN-
Discentes:

- Micael Gerrar
- Franscico Brilhante
- Tharcio Assunção 
- Davi Emanuel
- Hanna Mesquita

Emails:
- micael.gerrar@icomp.ufam.edu.br
- fransciscobraga99@gmail.com
- tharcio.assuncao@icomp.ufam.edu.br
- Davi.emanuel@icomp.ufam.edu.br
- hanna.mesquita@icomp.ufam.edu.br

# Visão Geral

Este projeto explora uma aplicação prática de Inteligência Artificial voltada para a área ambiental. Com o aumento do volume de resíduos e a necessidade urgente de melhorar os processos de reciclagem, sistemas automáticos de identificação de lixo tornam-se aliados importantes para a sustentabilidade.

A proposta consiste em criar um modelo de classificação de imagens capaz de distinguir diferentes tipos de materiais descartados, contribuindo para a otimização da triagem em centros de reciclagem.

Categorias de Materiais

O classificador trabalha com seis grupos distintos de resíduos, todos identificados a partir de imagens no formato 224×224×3:
- Plástico, Papel, Papelão, Vidro, Metal, Rejeito/Lixo comum

# O Dataset: TrashNet
O projeto utiliza o dataset TrashNet, disponível no Kaggle.
- Fonte: Kaggle - Garbage Classification
- Conteúdo: 2.527 imagens (redimensionadas para 512x384 pixels).
- Classes: 6 pastas, cada uma representando uma classe de lixo.
- O Desafio: O dataset é considerado pequeno e desbalanceado. A classe trash, por exemplo,
possui apenas 137 imagens. Isso torna o overfitting (quando o modelo "decora" os dados de
treino) o principal desafio a ser superado.
Ferramentas e Metodologia
Para desenvolver este classificador, foram utilizadas as seguintes ferramentas e técnicas:
- Linguagem: Python 3.10
- Ambiente: Conda (ambiente tf-final com suporte a GPU)
- Bibliotecas Principais: TensorFlow (Keras), Scikit-learn, Pandas, Matplotlib, Seaborn.
- Modelo: Uma Rede Neural Convolucional (CNN) padrão, seguindo o que foi solicitado:
     - 3 Blocos de Conv2D -> ReLU -> Dropout -> MaxPooling2D.
     - 1 Classificador Flatten -> Dense -> Dropout -> Dense.
- Técnica Chave (Combate ao Overfitting): Para lidar com o dataset pequeno, foi aplicado um
Data Augmentation agressivo no gerador de dados de treino (ImageDataGenerator). Isto cria
novas imagens "falsas" em tempo real para o modelo treinar, aumentando a variabilidade:
     - rescale=1./255
     - validation_split=0.15
     - horizontal_flip=True
     - vertical_flip=True
     - zoom_range = 0.5
     - width_shift_range = 0.3
     - height_shift_range = 0.3
     - rotation_range=50
- Estratégia de Treino: O modelo foi treinado usando o callback EarlyStopping, que monitora a
val_loss (perda na validação) e encerra o treino automaticamente se o modelo parar de
aprender. O treino foi interrompido após 52 épocas.

# Motivação e Objetivos

A separação manual de materiais recicláveis é um processo lento e frequentemente impreciso. Utilizando técnicas de Deep Learning, é possível desenvolver um sistema que automatize essa etapa, reduzindo erros e aumentando a eficiência das operações.

O projeto busca:

- Processar imagens de resíduos e extrair padrões relevantes
- Atribuir automaticamente a cada imagem uma das seis categorias disponíveis
- Medir o desempenho do modelo por meio de métricas apropriadas para classificações multiclasse

# Resultados

O modelo de CNN foi treinado com sucesso e atingiu uma acurácia de validação de 57,6%. O Relatório de Classificação e a Matriz de Confusão mostram que o modelo aprendeu a identificar com alta confiança classes como paper (F1 de 71%) e metal (F1 de 60%).
 
![WhatsApp Image 2025-11-16 at 21 06 07](https://github.com/user-attachments/assets/d103bc40-704f-4a1c-8109-4d7280f2da65)

No entanto, o desempenho foi baixo para classes como plastic (26%) e trash (26%), que o modelo confundiu massivamente com paper e glass. Isso se deve a dois fatores: (1) o desbalanceamento do dataset (poucas imagens de trash) e (2) a alta similaridade visual entre plásticos transparentes e vidro/papel.

![WhatsApp Image 2025-11-16 at 21 06 21](https://github.com/user-attachments/assets/6e61efda-7e1f-4859-baf7-b4012a38d1b7)

O gráfico de acurácia (do Bloco 10) mostrou um claro "gap" de overfitting, provando que, embora o data augmentation tenha sido crucial para ajudar o modelo a generalizar (evitando um colapso total), ele não foi suficiente para superar os desafios de um dataset pequeno e complexo.

# Como Executar o Projeto
Clone este repositório:
```
git clone https://github.com/icompgerrar/Trabalho-2-FIA---Machine-Learning-com-CNN-.git
cd Trabalho-2-FIA---Machine-Learning-com-CNN-
```
 Instale as dependências necessárias
```
pip install matplotlib pandas seaborn jupyterlab ipykernel scikit-learn
```
Execute o jupyter lab
```
jupyter lab
```
Abra o arquivo .ipynb e execute as células. (Lembre-se de ajustar o data_path no Bloco 2 para o local onde você baixou o dataset).






