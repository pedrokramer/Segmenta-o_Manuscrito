# Segmentação_Manuscrito

Este repositório contém o projeto desenvolvido para a disciplina **Práticas Computacionais Avançadas**, com foco em **segmentação de linhas manuscritas** a partir de diferentes abordagens de processamento de imagem e aprendizado de máquina. O estudo explora técnicas baseadas em **contornos**, **projeção horizontal** e **clusterização morfológica de documentos**.
- Gabriela Frajtag, João P. Mariano, Laís Ruela, Pedro H. Kramer  
- **Orientador:** Prof. Dr. James de Almeida

---

## Objetivo

Investigar métodos de segmentação de linhas em textos manuscritos, avaliando suas performances em imagens com diferentes origens e características gráficas. As técnicas testadas envolvem:

- Clusterização via K-Means sobre histogramas de cor e embeddings da VGG16  
- Processamento morfológico com OpenCV  
- Segmentação por projeção horizontal  

---
## Organização do Repositório

imagens/ # Imagens utilizadas (exemplares do IMS, CE-DOHS, BNDigital)
/ # Pasta com clusters
.ipynb  # Notebook com clusterização
Segmentação_por_histograma.ipynb  # Notebook com projeção de histograma 
Galeria.ipynb  # Notebook com projeção de histograma em comparação 
Segmentacao_Lais.ipynb # Notebook com segmentação por contorno
README.md # Este arquivo

## Metodologia
### 1. Clusterização das Imagens

- **K-Means** sobre:
  - Histogramas de cor (R, G, B)
  - Embeddings extraídos da **VGG16** (sem camada final)  
- Escolha do número de clusters com:
  - Método do cotovelo
  - Índice de Silhueta

### 2. Segmentação por Contornos (OpenCV)

- Detecção de contornos (`cv2.findContours`)
- Filtragem por área (>500 px) e aspect ratio
- Unificação de bounding boxes com centros verticais sobrepostos

### 3. Segmentação por Projeção Horizontal

- Soma de pixels por linha → histograma de projeção  
- Suavização com filtro Gaussiano  
- Identificação de vales com `scipy.signal.find_peaks` (versão negativa da projeção)  
- Foram testado vários parâmetros: `threshold_value` (binarização), `distance` e `prominence`

## Resultados

- A segmentação por contornos apresentou bons resultados, mas sensíveis à morfologia do texto.
- O método de projeção horizontal foi eficaz especialmente para linhas retas e bem espaçadas.
- A clusterização de imagens permitiu agrupar documentos com similaridades morfológicas, sugerindo rotas diferentes de segmentação conforme o cluster.
- A suavização da projeção antes da detecção de vales foi uma contribuição própria e importante para estabilidade da segmentação.

## Requisitos

- Python ≥ 3.8  
- OpenCV  
- NumPy  
- SciPy  
- scikit-learn  
- matplotlib  
- tensorflow / keras (para VGG16)

## Referências

- [1] GARRIDO-MUNOZ, C.; RIOS-VILA, A.; CALVO-ZARAGOZA, J. Handwritten Text Recognition: A Survey. arXiv:2502.08417, 2025.
- [2] ARON, I. Forensic Graphoscopy. Bulletin of the Transilvania University of Braşov, 2024.
- [3] BLUCHE, T. Deep Neural Networks for Large Vocabulary Handwritten Text Recognition. s.d.
- [4] BRASIL, E.; NASCIMENTO, L. F. História Digital. Estudos Históricos, v. 33, n. 69, abr. 2020.
- [5] SIMONYAN, K.; ZISSERMAN, A. Very Deep Convolutional Networks for Large-Scale Image Recognition. arXiv:1409.1556
- [6] https://github.com/computervisionpro/yt/tree/main/line-text-segmentation
- [7] https://github.com/muthuspark/line-segmentation-handwritten-doc/
