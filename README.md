# Learning to Forecast under External Influence Using Temporal Knowledge Graphs: Datasets, Methods and Benchmarks

## Overview
This project addresses the challenge of forecasting stock market trends by constructing a **Temporally-Aware Heterogeneous Knowledge Graph (STOCKnowledge,)**. STOCKnowledge, captures inter-stock relationships, financial statements, analyst sentiments, corporate events, and macroeconomic factors from stock assets listed on India and USA markets. By leveraging time-aware embeddings, this project ranks stock assets based on their potential return on investment over various holding periods.

## Data Sources

The datasets used in this project include :
- NASDAQ100, S&P500 (from Yahoo Finance)
- NIFTY500 (from NSE)

## Requirements

To run this project, you’ll need to install the required dependencies. These can be found in the `requirements.txt` file.

```bash
pip install -r requirements.txt
```
The `requirements.txt` file includes essential Python libraries.

## Running the Project

You can run the project in two ways, depending on your requirements

### Approach 1: Without Temporal Point Process
1. Navigate to the Phase-Stock-KG folder, which contains the main.py file along with model_imports.py and all necessary model files in the models folder.
2. The main parameters include ENCODER_LAYER, which can be set to either "transf" for transfomer or "lstm" for generating sequential embeddings.
3. For the Graph Convolutions, USE_GRAPH parameter set to hgat, which includes the HEAT Convolution
4. Set the INDEX according to the dataset you want to run: nasdaq100, sp500, or nifty500
4. Ensure the dataset is prepared and placed in the required directory.
5. Run the command:
   ```bash
   python3 main.py --INDEX nasdaq100
   ```
6. All remaining parameters are defined in the model_imports.py file.


### Approach 2: With Temporal Point Process
1. Navigate to the Stock_KG_TPP folder, which includes the main_TPP.py file and the necessary model files in the models folder.
2. Run the command:
   ```bash
   python3 main_TPP.py --tpp_batch_size 4096 --INDEX nifty500 --D_MODEL 20 --REL_EMB 16 --TPP_EMB 128 --gpu 1 --ENCODER_LAYER transf
   ```
- --tpp_batch_size 4096: Sets the batch size for training the Temporal Point Process (TPP) model in a phased manner.

- --INDEX nasdaq100: Indicates the dataset to be used. Replace nasdaq100 with your desired index or dataset name.

- --D_MODEL 20: Sets the model dimension for sequential embeddings to 20.

- --REL_EMB 16: Specifies the size of the relation embeddings (16).

- --TPP_EMB 128: Sets the embedding size for each node and relation in the TPP to 128.

- --ENCODER_LAYER transf: Uses a Transformer-based encoder layer.

## Data Preparation

Ensure the data is formatted as described below:

Data files for the encoder model (for sequential embeddings) are available in the Stock_Market_Hawkes/Phase-Stock-KG/data/pickle folder for each dataset.

Data files for graph convolution are located in Stock_Market_Hawkes/Phase-Stock-KG/kg/tkg_create, with:

temporal_kg_nifty.pkl for NIFTY

temporal_kg.pkl for NASDAQ and S&P

The temporal embeddings are trained and saved in /Stock_Market_Hawkes/Stock_KG_TPP/TPP/HPP_files/, and are extracted during integration with the main model.

