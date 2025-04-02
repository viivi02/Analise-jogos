## Tratamento de Dados no Jupyter Notebook

Para manipular os dados do arquivo `vgsales.csv`, utilizamos o Pandas no Jupyter Notebook. Abaixo estão os passos realizados:

### 1. Leitura do Arquivo CSV
```python
import pandas as pd
df = pd.read_csv("archive/vgsales.csv")
print(df.head())
```
### 2. Verificação de Valores Nulos
```python
print(df.isnull().sum())
```
#### Saída esperada:
```mathematica
Rank              0
Name              0
Platform          0
Year            271
Genre             0
Publisher        58
NA_Sales          0
EU_Sales          0
JP_Sales          0
Other_Sales       0
Global_Sales      0
dtype: int64
```
### 3. Tratamento de Dados Ausentes
```python
df.dropna(inplace=True)
df["Year"] = df["Year"].fillna(df["Year"].median())
df["Year"] = pd.to_numeric(df["Year"], errors="coerce").astype("Int64")
```
### 4. Verificação dos Tipos de Dados
```python
print(df.dtypes)
```
#### Saída esperada:
```mathematica
Rank              int64
Name             object
Platform         object
Year              Int64
Genre            object
Publisher        object
NA_Sales        float64
EU_Sales        float64
JP_Sales        float64
Other_Sales     float64
Global_Sales    float64
dtype: object
```
### 5. Cálculo das Vendas Totais por Região
```python
df["Total_Regional_Sales"] = df["NA_Sales"] + df["EU_Sales"] + df["JP_Sales"] + df["Other_Sales"]
print(df.dtypes)
```
#### Novo campo adicionado:
```python
Total_Regional_Sales    float64
```
### 6. Seleção dos 10 Jogos Mais Vendidos
```python
top_games = df[["Name", "Global_Sales"]].sort_values(by="Global_Sales", ascending=False).head(10)
print(top_games)
```
#### Saída esperada:

```mathematica
                        Name  Global_Sales
0                 Wii Sports         82.74
1          Super Mario Bros.         40.24
2             Mario Kart Wii         35.82
3          Wii Sports Resort         33.00
4   Pokemon Red/Pokemon Blue         31.37
5                     Tetris         30.26
6      New Super Mario Bros.         30.01
7                   Wii Play         29.02
8  New Super Mario Bros. Wii         28.62
9                  Duck Hunt         28.31
```
### 7. Salvamento dos Dados Processados
```python
df.to_csv("vgsales.csv", index=False, sep=";", decimal=",")
```
Agora, o arquivo [vgsales.csv](https://github.com/viivi02/Analise-jogos/blob/4f45906d37076adc5e02b1bd66a669b8648e6698/vgsales.csv) contém os dados tratados e formatados.
