# StoreSaleForecasting

This study is an investigation into the effectiveness of Long Short-Term Memory (LSTM) and Transformer
models in forecasting retail sales time series. It aims to highlight the potential of the LSTM model
in outperforming the Transformer in terms of loss performance, underscoring its utility for accurate
sales prediction in retail environments like Corporacion Favorita. The study will demonstrate how 
these models can enable retailers to forecast product demand more precisely, leading to optimized
inventory management, enhanced customer satisfaction, and reduced surplus, ultimately contributing to increased profitability

The data and general overview of the problem statement can be found at this [Kaggle contest](https://www.kaggle.com/competitions/store-sales-time-series-forecasting).

**Disclaimer:** This paper was not actually published as part of the ICLR 2024 conference. It is a mock report intended to simply use the ICLR paper template in order to better structure the overall study.

# Description

The Transformer model, introduced in ”Attention is All You Need”, Vaswani et al. (2017), represents a significant shift in sequence learning, particularly for natural language
processing. Its core is the self-attention mechanism, enabling the model to process input sequences
in parallel and capture long-range dependencies, a departure from the sequential processing of RNNs
and LSTMs. The architecture comprises an encoder and decoder, each with multiple layers of
multi-head self-attention blocks and feed-forward networks. Positional encodings are employed to retain
sequence order information. For time series forecasting, the Transformer’s ability to handle longrange dependencies and its efficient parallel processing make it a promising candidate, suggesting
potential advancements in forecasting accuracy and efficiency to the other model explored, the Long Short-term Memory (LSTM) model.

A more in-depth overview of the steps taken in exploratory data analysis, sequence construction, and model architecture can be found in the [mock research paper](mock_research_paper.pdf).

# Hyperparameters

| HYPERPARAMETER | VALUE       |
|----------------|-------------|
| Batch Size     | 32          |
| # Epochs       | 10          |
| Learning Rate  | 0.001       |
| Optimizer      | Adam        |
| Scheduler      | MultiStepLR |

The loss criterion used in both models was the root mean squared log error. This is a form of loss that incurs a
larger penalty for underestimation of results than overestimation. This is important in the store sales
prediction case as it is much more profitable and useful for a store to have a surplus of a product
than a deficit. For the DataLoader, shuffle was set to 'False' in order to preserve the sequential nature of the time data.

## LSTM Specific Hyperparameters

| HYPERPARAMETER | VALUE | DESCRIPTION                                                |
|----------------|-------|------------------------------------------------------------|
| hidden_dim     | 128   | The dimension of the hidden/latent layer of the LSTM model |
| num_layers     | 3     | The number of LSTM layers                                  |
| num_features   | 3     | The number of continuous features                          |
| output_dim     | 1     | The output sales value from the feature dimension          |

## Transformer Specific Hyperparameters

| HYPERPARAMETER    | VALUE | DESCRIPTION                                       |
|-------------------|-------|---------------------------------------------------|
| model_dim         | 512   | The hidden dimension of the model, d_k            |
| num_layers        | 6     | The number of encoder and decoder blocks          |
| num_heads         | 8     | The number of heads of multi-head attention       |
| num_features      | 3     | The number of continuous features                 |
| forward_expansion | 4     | The scaling factor in the feed forward network    |
| N_enc             | 15    | The input sequence length for the encoder         |
| N_dec             | 1     | The input sequence length for the decoder         |
| output_dim        | 1     | The output sales value from the feature dimension |

# Results

When the LSTM model was submitted to the Kaggle competition, a score of 3.02217 was obtained for the final testing
data submission CSV file. For the Transformer, a score of 3.9873 was obtained. In-depth analysis of the results is presented within the "Results" section in the mock research paper. Based on the presented results, it is evident that in the context of the evaluated dataset or task,
the LSTM model outperforms the Transformer model in terms of loss performance. The statistical
analysis reveals that the LSTM not only maintains a lower average loss but also exhibits a tighter
distribution of loss values, as indicated by its lower standard deviation. Additionally, the LSTM
shows more favorable results in both the median and the maximum loss recorded, suggesting its
consistency in maintaining lower loss values across various segments of the dataset. This is further
compounded visually in Figures 1 and 2, with the Transformer having higher values across all stores
and categories. While these findings highlight the LSTM’s efficiency in this specific scenario, it’s
crucial to note that this conclusion is based solely on loss metrics. For a thorough assessment, other
performance indicators and the model’s applicability to the task at hand should also be taken into
account. Nonetheless, in the realm of loss minimization, the LSTM model demonstrates a clear
advantage over the Transformer model for this particular application.

