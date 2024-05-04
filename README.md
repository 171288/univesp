# univesp

Projeto: acompanhhamento de vendas

import pandas as pd

import matplotlib.pyplot as plt

tabela = pd.read_excel(r"C:\Users\elism\OneDrive\Área de Trabalho\analise vendas2.xlsx")

tabela = tabela.astype('float64', errors='ignore')

pd.options.display.float_format = '{:,.0f}'.format 

display(tabela) 

tabela.info()

	Mês 	Joao 	Maria 	Mateus 	Ana 	Thiago 	Joana 	Pedro 	Talita 	Davi 	Leticia
0 	Janeiro 	98,556 	101,258 	102,145 	108,125 	88,789 	100,489 	99,879 	95,265 	99,878 	105,487
1 	Fevereiro 	101,000 	103,657 	104,956 	108,578 	89,456 	72,235 	99,911 	99,460 	101,235 	102,547
2 	Março 	97,564 	99,258 	101,255 	101,256 	95,123 	101,478 	99,225 	99,783 	100,451 	81,256
3 	Abril 	87,999 	98,456 	107,894 	99,991 	99,878 	102,657 	99,878 	99,258 	99,985 	103,245
4 	Maio 	110,000 	87,234 	99,998 	102,456 	97,456 	103,568 	99,632 	99,663 	99,213 	106,245
5 	Junho 	89,568 	98,498 	100,437 	104,258 	101,256 	99,878 	99,456 	99,147 	99,413 	99,784
6 	Julho 	99,123 	89,266 	101,258 	100,657 	89,124 	99,999 	100,101 	105,258 	106,512 	101,287
7 	Agosto 	111,012 	103,125 	109,527 	100,877 	97,124 	100,389 	101,223 	99,785 	102,478 	100,258
8 	Setembro 	88,456 	102,789 	97,456 	105,999 	98,527 	100,987 	99,987 	97,456 	103,546 	100,698
9 	Outubro 	99,134 	99,998 	95,231 	103,522 	96,327 	100,111 	100,123 	99,412 	100,258 	105,477
10 	Novembro 	99,761 	99,124 	100,553 	99,878 	100,258 	101,256 	99,823 	99,249 	99,784 	105,789
11 	Dezembro 	104,983 	104,125 	100,738 	110,223 	98,321 	99,899 	99,632 	107,534 	100,111 	108,468

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 12 entries, 0 to 11
Data columns (total 11 columns):
 #   Column   Non-Null Count  Dtype  
---  ------   --------------  -----  
 0   Mês      12 non-null     object 
 1   Joao     12 non-null     float64
 2   Maria    12 non-null     float64
 3   Mateus   12 non-null     float64
 4   Ana      12 non-null     float64
 5   Thiago   12 non-null     float64
 6   Joana    12 non-null     float64
 7   Pedro    12 non-null     float64
 8   Talita   12 non-null     float64
 9   Davi     12 non-null     float64
 10  Leticia  12 non-null     float64
dtypes: float64(10), object(1)
memory usage: 1.2+ KB

tabela.plot(figsize=(10,4), kind="bar")

plt.xlabel('Meses')

plt.ylabel('Venda')

plt.title('Evolução venda x meses')

labels=['janeiro','fevereiro','março','abril','maio','junho','julho','agosto','setembro','outubro','novembro','dezembro']

labels=tabela.index.tolist()

plt.legend(ncol=1,loc='upper right', bbox_to_anchor=(1.15,1))

plt.show()

​

for coluna in tabela.set_index('Mês').columns:

    ax = tabela.set_index('Mês')[coluna].plot(kind='bar', figsize=(12,6))

    plt.bar_label(ax.containers[0])

    plt.xlabel('Mês')

    plt.ylabel('Venda')

    plt.title(f'Acompanhamento vendas {coluna}')

    plt.xticks(rotation=0)

    plt.show()

    

    

Média de venda por vendedor

media_vendedor=tabela.mean(numeric_only=True)

display(media_vendedor)

plt.plot(media_vendedor,marker='o')

plt.xlabel('Vendedores')

plt.ylabel('Media total venda por vendedor (em milhares de reais)')

plt.grid(True)

plt.title('Média de venda')

plt.show()

Joao       98,930
Maria      98,899
Mateus    101,787
Ana       103,818
Thiago     95,970
Joana      98,579
Pedro      99,906
Talita    100,106
Davi      101,072
Leticia   101,712
dtype: float64

Melhor mês de venda por vendedor

tabela_max = pd.DataFrame()

tabela_max['Mês'] = tabela.set_index('Mês').idxmax()

tabela_max['Vendas'] = tabela.set_index('Mês').max()

tabela_max

	Mês 	Vendas
Joao 	Agosto 	111,012
Maria 	Dezembro 	104,125
Mateus 	Agosto 	109,527
Ana 	Dezembro 	110,223
Thiago 	Junho 	101,256
Joana 	Maio 	103,568
Pedro 	Agosto 	101,223
Talita 	Dezembro 	107,534
Davi 	Julho 	106,512
Leticia 	Dezembro 	108,468

plt.figure(figsize=(8,5))

grafico = plt.bar(tabela_max.index, tabela_max['Vendas'])

plt.xlabel('Vendedores')

plt.ylabel('Vendas')

plt.bar_label(grafico)

plt.title('Melhor mês de venda por vendedor')

plt.show()

Menor mês de venda por vendedor

tabela_min = pd.DataFrame()

tabela_min['Mês'] = tabela.set_index('Mês').idxmin()

tabela_min['Vendas'] = tabela.set_index('Mês').min()

tabela_min

	Mês 	Vendas
Joao 	Abril 	87,999
Maria 	Maio 	87,234
Mateus 	Outubro 	95,231
Ana 	Novembro 	99,878
Thiago 	Janeiro 	88,789
Joana 	Fevereiro 	72,235
Pedro 	Março 	99,225
Talita 	Janeiro 	95,265
Davi 	Maio 	99,213
Leticia 	Março 	81,256

plt.figure(figsize=(8,5))

grafico = plt.bar(tabela_min.index, tabela_min['Vendas'])

plt.xlabel('Vendedores')

plt.ylabel('Vendas')

plt.bar_label(grafico)

plt.title('Menor mês de venda por vendedor')

plt.show()

​
