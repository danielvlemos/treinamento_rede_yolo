# Projeto de Detecção de Semáforos e Placas de Pare com YOLOv5

Este repositório contém o código e os resultados do treinamento de um modelo YOLOv5 para detectar especificamente semáforos (`traffic light`) e placas de pare (`stop sign`).

## 🎯 Objetivo

O objetivo principal deste projeto foi realizar o fine-tuning de um modelo YOLOv5s pré-treinado para identificar apenas duas classes (`traffic light` e `stop sign`) a partir de um subset do dataset COCO128. O projeto abordou os desafios da configuração do ambiente, preparação dos dados e treinamento da rede para um domínio específico.

## ⚙️ Tecnologias Utilizadas

* **Python**
* **PyTorch**
* **YOLOv5** (implementação Ultralytics)
* **Anaconda/Miniconda** (para gerenciamento de ambiente)
* **Git** e **GitHub** (para controle de versão)
* **Google Colab** (ambiente de desenvolvimento e treinamento, conforme notebook)

## 📊 Dataset

Para este projeto, foi utilizado um subset do dataset COCO128, que contém um número limitado de instâncias das classes alvo.

* **Nome:** COCO128
* **Classes Alvo:**
    * `traffic light` (remapeado para ID: 0)
    * `stop sign` (remapeado para ID: 1)
* **Observação:** Devido ao tamanho limitado do dataset (128 imagens no total, com poucas instâncias das classes alvo), os resultados de desempenho foram iniciais e indicam a necessidade de um dataset maior para um modelo robusto.

## 🚀 Como Executar o Projeto

Para replicar o treinamento ou utilizar o modelo:

1.  **Clone este repositório:**
    ```bash
    git clone [https://github.com/danielvlemos/treinamento_rede_yolo.git](https://github.com/danielvlemos/treinamento_rede_yolo.git)
    cd treinamento_rede_yolo
    ```

2.  **Crie e ative o ambiente virtual (opcional, mas recomendado):**
    ```bash
    # Com conda
    conda create -n yolov5_env python=3.9
    conda activate yolov5_env

    # Ou com venv
    python -m venv venv
    .\venv\Scripts\activate # No Windows
    source venv/bin/activate # No Linux/macOS
    ```

3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```
    *Se você não tem um `requirements.txt`, pode criar um com `pip freeze > requirements.txt` no seu ambiente com as libs instaladas, ou listar as principais:*
    ```
    torch
    torchvision
    ultralytics
    matplotlib
    numpy
    pandas
    tqdm
    PyYAML
    seaborn
    ```

4.  **Estrutura de Pastas (Esperada):**
    Certifique-se de que a estrutura de pastas para os dados esteja conforme o esperado pelo YOLOv5 e configurada no arquivo `data.yaml`.
    ```
    .
    ├── Projeto_de_criação_de_uma_base_de_dados_e_treinamento_da_rede_YOLO.ipynb
    ├── data.yaml
    ├── requirements.txt
    ├── runs/ # Gerado após o treinamento (ignoradas pelo .gitignore)
    ├── yolov5/ # Pasta do YOLOv5 (se você a clonou aqui ou fez download)
    └── README.md
    └── .gitignore
    ```

5.  **Treinamento do Modelo:**
    Você pode executar o treinamento utilizando o notebook Jupyter `Projeto_de_criação_de_uma_base_de_dados_e_treinamento_da_rede_YOLO.ipynb` em um ambiente como o Google Colab ou localmente.
    Alternativamente, o comando de treinamento via terminal seria similar a:
    ```bash
    python yolov5/train.py --img 640 --batch 16 --epochs 100 --data data.yaml --weights yolov5s.pt --name traffic_signs_run
    ```
    (Ajuste os caminhos e parâmetros conforme sua configuração.)

## 📈 Resultados do Treinamento

O treinamento foi realizado por 100 épocas. Os resultados de validação iniciais são os seguintes:

| Class             | Images | Instances | P         | R         | mAP50     | mAP50-95  |
| :---------------- | :----- | :-------- | :-------- | :-------- | :-------- | :-------- |
| **all** | 128    | 23        | 0.00322   | 0.639     | 0.284     | 0.175     |
| traffic light     | 128    | 14        | 0.00467   | 0.5       | 0.169     | 0.126     |
| stop sign         | 128    | 9         | 0.00177   | 0.778     | 0.4       | 0.224     |

**Observações sobre os resultados:**
* As métricas de mAP (mAP50 e mAP50-95) são baixas, indicando que o modelo tem dificuldades em fazer detecções precisas e bem localizadas.
* A precisão (P) é extremamente baixa para ambas as classes, sugerindo uma alta taxa de falsos positivos (o modelo detecta muitos objetos que não são as classes alvo).
* O recall (R) é razoável, especialmente para 'stop sign', o que significa que o modelo consegue encontrar uma boa parte dos objetos reais, mas não os localiza com precisão ou com muitos falsos positivos.
* **A principal causa para esses resultados iniciais é o tamanho reduzido do dataset utilizado para treinamento e validação.**

## 🔮 Melhorias Futuras

Para aprimorar o desempenho do modelo, as seguintes ações são recomendadas:

* **Expansão do Dataset:** Aumentar significativamente o volume e a diversidade de imagens com semáforos e placas de pare, anotadas com alta qualidade. Utilizar datasets maiores ou coletar e anotar dados personalizados.
* **Mais Épocas de Treinamento:** Com um dataset maior, pode ser benéfico treinar por mais épocas.
* **Aumento de Dados (Data Augmentation):** Aplicar técnicas de aumento de dados mais agressivas para variar o dataset existente.
* **Ajuste de Hiperparâmetros:** Experimentar diferentes configurações de hiperparâmetros para otimizar o treinamento.

## 🤝 Contribuições

Contribuições são bem-vindas! Se você tiver sugestões, melhorias ou encontrar algum problema, sinta-se à vontade para abrir uma issue ou enviar um pull request.

---

## 📧 Contato

*  **Daniel Lemos**
* **LinkedIn:** [https://www.linkedin.com/in/danielvlemos/]
* **Email:** [danielvlemos@gmail.com]

---
