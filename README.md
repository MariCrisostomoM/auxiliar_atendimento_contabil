# Auxiliar de Atendimento Contabil

O modelo final se encontra no diretório [BERTimbau finetuned model](https://github.com/MariCrisostomoM/auxiliar_atendimento_contabil/tree/main/BERTimbau_finetuned_model).

Se trata do modelo [BERTimbau](https://huggingface.co/neuralmind/bert-base-portuguese-cased) com fine tuning no contexto de aplicação do classificador. O dataset rotulado utilizado no fine tuning está disponível no [link](https://drive.google.com/drive/folders/1hmCnqI353NZ7hhF5iefoT415IwthCdKx?usp=sharing) e o fine tuning pode ser econtrado nesse [link](https://colab.research.google.com/drive/1Xt_SWsSjIOOL8iv6dxG789XjUqdg_rKR?usp=sharing).

Em comparação com o modelo, foram avaliadas duas outras estratégias: [BERTimbau Finetuned + Classificador](https://colab.research.google.com/drive/14-kOaC4dNSeq1jTl7YKNJyD2F-j0f4re?usp=sharing) e [BERTimbau + Classificador](https://colab.research.google.com/drive/19YIaK2rbdg20NWe9eozsHgXJ2KUGBQHY?usp=sharing). O resultado pode ser visto na tabela abaixo.

| **Abordageem**                      | **Acurácia** | **Precisão** | **Recall** | **F1**  |
|-------------------------------------|--------------|--------------|------------|---------|
| BERTimbau + Finetuning              | _0.888_      | _0.911_      | _0.912_    | _0.908_ |
| BERTimbau Finetuned + Classificador | 0.875        | 0.908        | 0.895      | 0.897   |
| BERTimbau + Classificador           | 0.819        | 0.868        | 0.750      | 0.758   |

## Execução do modelo

A execução do modelo deve ser realizada em python utilizando as bibliotecas contidas no arquito texto [requirements.txt](https://github.com/MariCrisostomoM/auxiliar_atendimento_contabil/blob/main/requirements.txt).

Segue o código exemplo para execução do modelo:

```python
from transformers import pipeline

classifier = pipeline("text-classification",
                      model="BERTimbau_finetuned_model/",
                      tokenizer="BERTimbau_finetuned_model/")

mensagem = "Bom dia, gostaria de receber a taxa de conodomínio de vencimento no dia 15/02."

classe = classifier(x)[0]['label']
```

### Mapeamento classe - tarefa

As classes podem ser mapeadas para as tarefas elicitadas seguindo a relação:

| **Classe** | **Tarefa**                               |
|------------|------------------------------------------|
| 0          | Atendimento                              |
| 1          | Emissão/envio de boleto                  |
| 2          | Verificação de inadimplência             |
| 3          | Emissão de carta de quitação/nada consta |
| 4          | Saudação                                 |
