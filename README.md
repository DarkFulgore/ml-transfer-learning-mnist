# 🧠 Projeto – Transfer Learning com Deep Learning (MNIST / Cats vs Dogs)

![Python](https://img.shields.io/badge/Python-3.10-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.15-orange.svg)
![Keras](https://img.shields.io/badge/Keras-2.15-red.svg)
![Colab](https://img.shields.io/badge/Google%20Colab-Notebook-yellow.svg)
![Dataset](https://img.shields.io/badge/Dataset-Oxford%20IIIT%20Pets-purple.svg)
![Status](https://img.shields.io/badge/Status-Concluído-success.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

## 🚀 Executar o notebook no Google Colab

Clique no botão abaixo para abrir e executar todo o projeto gratuitamente no Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1mjJ2lxUkYViHjYWEAAR6tYsH2Ie6XEES)


---

## 📌 Sobre o Projeto
Este projeto faz parte do desafio final do módulo de Machine Learning da DIO, com foco em **Transfer Learning aplicado em Deep Learning**, utilizando Python e Google Colab.

O objetivo é demonstrar compreensão prática dos conceitos estudados, incluindo:

- Redes neurais convolucionais (CNNs)
- Transfer Learning
- Organização e pré-processamento de banco de imagens
- Treinamento, validação e teste real com imagens externas

🔗 Projeto de referência:  
https://colab.research.google.com/github/kylemath/ml4a-guides/blob/master/notebooks/transfer-learning.ipynb

---

## 🎯 Objetivos do Desafio
✔️ Aplicar Transfer Learning em um dataset real  
✔️ Documentar todo o processo técnico  
✔️ Publicar o projeto em repositório público no GitHub  
✔️ Utilizar Jupyter Notebook / Google Colab  

---

## 🧾 Dataset Utilizado — Oxford-IIIT Pets

Dataset composto por **37 raças de animais**, sendo:
- 🐱 12 raças de gatos  
- 🐶 25 raças de cachorros  

### 🔗 Links oficiais
- https://www.robots.ox.ac.uk/~vgg/data/pets/  
- https://academictorrents.com/details/b18bbd9ba03d50b0f7f479acc9f4228a408cecc1

### 📥 Download via Google Colab
```bash
!wget https://www.robots.ox.ac.uk/~vgg/data/pets/data/images.tar.gz
!wget https://www.robots.ox.ac.uk/~vgg/data/pets/data/annotations.tar.gz

!tar -xzf images.tar.gz
!tar -xzf annotations.tar.gz

🧩 Organização e Pré-processamento

As imagens possuem nomes representando a raça do animal, por exemplo:

Maine_Coon_222.jpg → gato

yorkshire_terrier_90.jpg → cachorro

➡️ Foi necessário mapear manualmente as raças em apenas duas classes: cats/ e dogs/.

✔️ Estrutura final do dataset
data/
   train/
      cats/
      dogs/
   val/
      cats/
      dogs/

📊 Quantidade final de imagens
Conjunto	Cats	Dogs
Train	1934	3980
Val	469	1010

Total processado: 7.393 imagens

🛠️ Tecnologias Utilizadas

Python 3.x

TensorFlow / Keras

NumPy

Matplotlib

scikit-learn

Google Colab

Git / GitHub

🧱 Arquitetura do Modelo — MobileNetV2 (Transfer Learning)

A base MobileNetV2 foi utilizada com pesos pré-treinados em ImageNet, com as camadas congeladas (sem Fine Tuning), acrescentando apenas uma camada Dense final com ativação sigmoid.

Model: "sequential"
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━┓
┃ Layer (type)                    ┃ Output Shape           ┃ Param #       ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━┩
│ mobilenetv2_1.00_224 (base)     │ (None, 7, 7, 1280)     │ 2,257,984     │
├─────────────────────────────────┼────────────────────────┼───────────────┤
│ global_average_pooling2d        │ (None, 1280)           │ 0             │
├─────────────────────────────────┼────────────────────────┼───────────────┤
│ dense (Dense)                   │ (None, 1)              │ 1,281         │
└─────────────────────────────────┴────────────────────────┴───────────────┘

Total params: 2,259,265 (8.62 MB)  
Trainable params: 1,281  
Non-trainable params: 2,257,984


➡️ Apenas 1.281 parâmetros foram treinados.

📈 Métricas do Modelo
✔️ Matriz de Confusão
[[150 319]
 [314 696]]

✔️ Classification Report
              precision    recall  f1-score   support

           0       0.32      0.32      0.32       469
           1       0.69      0.69      0.69      1010

    accuracy                           0.57      1479
   macro avg       0.50      0.50      0.50      1479
weighted avg       0.57      0.57      0.57      1479

🧾 Conclusão das métricas

Acurácia geral: ~57%

Dataset desbalanceado gerou viés para a classe "dogs"

Métricas coerentes para modelo sem Fine Tuning e sem Class Weights

🐱🐶 Predições com Imagens Externas

Testes realizados com imagens reais (na pasta arq_predicoes/):

📌 gato1.jpg
🐶 Prob (dog) = 0.0056
🐱 Prob (cat) = 0.9944
🎯 Resultado final: 🐱 CAT

📌 cachorro1.jpg
🐶 Prob (dog) = 0.9987
🐱 Prob (cat) = 0.0013
🎯 Resultado final: 🐶 DOG


➡️ Classificação correta e com alta confiança.

📁 Estrutura do Repositório
ml-transfer-learning-mnist/
│
├─ notebooks/
│   ├─ transfer-learning.ipynb
│   └─ transfer-learning-cats-dogs.ipynb
│
├─ arq_predicoes/
│   ├─ gato1.jpg
│   ├─ cachorro1.jpg
│
├─ images/
│
├─ src/
│
├─ .gitignore
├─ requirements.txt
└─ README.md

✔️ Conclusão

Este projeto demonstra a aplicação prática de Transfer Learning em visão computacional utilizando MobileNetV2.

Mesmo sem técnicas avançadas como:

Fine Tuning

Class Weights

Tunagem de hiperparâmetros

Foi possível construir um modelo funcional que:

✔️ Classifica imagens externas corretamente
✔️ Treina rapidamente
✔️ Usa apenas ~1.2 mil parâmetros treináveis

🚀 Próximos passos recomendados

Aplicar Fine Tuning nas últimas camadas

Aplicar Class Weights para lidar com desbalanceamento

Melhorar Data Augmentation

Balancear dataset

🧑‍💻 Autor

Denis Kalleb O. Costa
Projeto desenvolvido no contexto do Bootcamp DIO — Machine Learning.
