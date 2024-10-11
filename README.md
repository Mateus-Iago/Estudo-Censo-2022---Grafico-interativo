# Estudo censo 2022 IBGE - Gráfico de Crescimento Populacional

## Sobre
A ideia desse projeto surgiu quando descobri que o IBGE disponibilizava publicamente os dados do censo realizado a cada 10 anos. Além disso, eles oferecem uma API com suporte para Python, o que facilita a importação dos dados para dentro do código.

---

## Dados
A tabela é importada por meio de uma função da biblioteca `sidrapy` chamada `.get_table()`. Com os parâmetros corretos, conseguimos de forma simples trazer a base para o trabalho.

```python
  import pandas as pd
  import sidrapy

pop = sidrapy.get_table(
    table_code='4709',               # t (table_code) - é o codigo da tabela no site da sidra IBGE;
    territorial_level='6',           # n (territorial_level) - especifica os niveis territoriais;
    ibge_territorial_code='all',     # n/ (ibge_territorial_code) - inserido dentro do nivel territorial, especificar o codigo territorial do IBGE;
    period='all',                    # p (period) - utilizado para especificar o periodo;
    variable='all',                  # v (variable) - para especificar as variaveis desejadas;
)
```
### Output:
![Tabela importada para o sydra](caminho/para/imagem)
---

## Tratamentos
A tabela vem com os dados de uma maneira que podem ser melhor organizados para a criação do gráfico

### Removendo acentos
```python
# Removendo acentos para facilitar o estudo
pop = pop.apply(lambda x: x.str.normalize('NFKD').str.encode('ascii', errors='ignore').str.decode('utf-8') if x.dtype == 'object' else x) # EsSa função é aplicada em todas as linhas do tipo object do data frame
# Removendo primeira linha
pop = pop.iloc[1:] # removemos a linha com indice zero que não é uma legenda dos dados

pop.head()
```
