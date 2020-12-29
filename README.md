<img align="center" width="100" src="https://raw.githubusercontent.com/MuriloKrominski/COVID-Maringa/main/Imagens/link.png"> <h1>COVID - Maringá & Londrina</h1>

Em janeiro de 2021, retornarei ao Brasil após um período de desenvolvimento pessoal e profissional na Europa.<br>
Ainda estou a me decidir quanto a cidade em que pretendo viver, e já tenha duas cidades a encabeçar minha lista de cidades pretendidas; as cidades de Maringá e de Londrina, ambas no Estado do Parana.<br>
Hoje, dia 27/12/2020, decidi verificar por mim mesmo, como andam os casos de Covid nestas cidades, apenas para experimentar uma nova técnica para Exploratory Data Analysis com grafico animado.<br>
<br>

# Objetivo
A qualquer hora, basta rodar o script, para gerar bancos de dados atualizados sobre o Convid no Brasil e em cidades expecificas de sua preferencia (atualizados automaticamente, uma vez ao dia) - Base de dados do Brasil.io.
Depois de processados, os dados estao prontos para serem usados dentro da plataforma Flourish, para gerar o grafico animado (meu primeiro contato com essa ferramenta, e motivo de criar este repositorio).

```diff
ATENÇÃO:
+ Permitido usar livremente, inclusive copiar e usar para gerar Dataframes e graficos de outros municípios.
- Proibida a monetização, comercialização de todo ou de parte ou usar para alguma outra forma de auferir receita, sem o consentimento.
```

# Animação Gráfica:
<a href="https://flo.uri.sh/visualisation/4802203/embed" target="_parent"><img src="https://raw.githubusercontent.com/MuriloKrominski/COVID-Maringa/main/Imagens/link_graficoanimado.png" alt="Gráfico Animado"/><br>
Clique na imagem para ver a animação gráfica.</a><br> 

# Colaboratory:
<a href="https://colab.research.google.com/github/MuriloKrominski/COVID-Maringa/blob/main/COVID-Maringa.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Abrir no Colab"/></a><br>

# Dados:
```python
pip install -qr requirements.txt
```


```python
import numpy as np
import pandas as pd
import requests
import io
import os
```


```python
fonte = "https://data.brasil.io/dataset/covid19/caso_full.csv.gz"
resposta = requests.get(fonte)
content = resposta.content
print(type(content))
dados = pd.read_csv(io.BytesIO(content), sep=",", compression="gzip", index_col=0, quotechar='"')
dados.to_csv("/home/mk/Documentos/maringa/caso_full.csv", index=True)
dados
```

    <class 'bytes'>





<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city_ibge_code</th>
      <th>date</th>
      <th>epidemiological_week</th>
      <th>estimated_population</th>
      <th>estimated_population_2019</th>
      <th>is_last</th>
      <th>is_repeated</th>
      <th>last_available_confirmed</th>
      <th>last_available_confirmed_per_100k_inhabitants</th>
      <th>last_available_date</th>
      <th>last_available_death_rate</th>
      <th>last_available_deaths</th>
      <th>order_for_place</th>
      <th>place_type</th>
      <th>state</th>
      <th>new_confirmed</th>
      <th>new_deaths</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>São Paulo</th>
      <td>3550308.0</td>
      <td>2020-02-25</td>
      <td>9</td>
      <td>12325232.0</td>
      <td>12252023.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.00811</td>
      <td>2020-02-25</td>
      <td>0.0000</td>
      <td>0</td>
      <td>1</td>
      <td>city</td>
      <td>SP</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>NaN</th>
      <td>35.0</td>
      <td>2020-02-25</td>
      <td>9</td>
      <td>46289333.0</td>
      <td>45919049.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.00216</td>
      <td>2020-02-25</td>
      <td>0.0000</td>
      <td>0</td>
      <td>1</td>
      <td>state</td>
      <td>SP</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>São Paulo</th>
      <td>3550308.0</td>
      <td>2020-02-26</td>
      <td>9</td>
      <td>12325232.0</td>
      <td>12252023.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.00811</td>
      <td>2020-02-26</td>
      <td>0.0000</td>
      <td>0</td>
      <td>2</td>
      <td>city</td>
      <td>SP</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>NaN</th>
      <td>35.0</td>
      <td>2020-02-26</td>
      <td>9</td>
      <td>46289333.0</td>
      <td>45919049.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.00216</td>
      <td>2020-02-26</td>
      <td>0.0000</td>
      <td>0</td>
      <td>2</td>
      <td>state</td>
      <td>SP</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>São Paulo</th>
      <td>3550308.0</td>
      <td>2020-02-27</td>
      <td>9</td>
      <td>12325232.0</td>
      <td>12252023.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.00811</td>
      <td>2020-02-27</td>
      <td>0.0000</td>
      <td>0</td>
      <td>3</td>
      <td>city</td>
      <td>SP</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>NaN</th>
      <td>43.0</td>
      <td>2020-12-28</td>
      <td>53</td>
      <td>11422973.0</td>
      <td>11377239.0</td>
      <td>True</td>
      <td>False</td>
      <td>432241</td>
      <td>3783.96237</td>
      <td>2020-12-28</td>
      <td>0.0197</td>
      <td>8536</td>
      <td>294</td>
      <td>state</td>
      <td>RS</td>
      <td>638</td>
      <td>44</td>
    </tr>
    <tr>
      <th>NaN</th>
      <td>42.0</td>
      <td>2020-12-28</td>
      <td>53</td>
      <td>7252502.0</td>
      <td>7164788.0</td>
      <td>True</td>
      <td>False</td>
      <td>482129</td>
      <td>6647.76101</td>
      <td>2020-12-28</td>
      <td>0.0105</td>
      <td>5082</td>
      <td>292</td>
      <td>state</td>
      <td>SC</td>
      <td>2182</td>
      <td>43</td>
    </tr>
    <tr>
      <th>NaN</th>
      <td>28.0</td>
      <td>2020-12-28</td>
      <td>53</td>
      <td>2318822.0</td>
      <td>2298696.0</td>
      <td>True</td>
      <td>False</td>
      <td>110001</td>
      <td>4743.83113</td>
      <td>2020-12-28</td>
      <td>0.0224</td>
      <td>2461</td>
      <td>290</td>
      <td>state</td>
      <td>SE</td>
      <td>1058</td>
      <td>7</td>
    </tr>
    <tr>
      <th>NaN</th>
      <td>35.0</td>
      <td>2020-12-28</td>
      <td>53</td>
      <td>46289333.0</td>
      <td>45919049.0</td>
      <td>True</td>
      <td>False</td>
      <td>1427752</td>
      <td>3084.40824</td>
      <td>2020-12-28</td>
      <td>0.0321</td>
      <td>45902</td>
      <td>308</td>
      <td>state</td>
      <td>SP</td>
      <td>1576</td>
      <td>39</td>
    </tr>
    <tr>
      <th>NaN</th>
      <td>17.0</td>
      <td>2020-12-28</td>
      <td>53</td>
      <td>1590248.0</td>
      <td>1572866.0</td>
      <td>False</td>
      <td>True</td>
      <td>89410</td>
      <td>5622.39349</td>
      <td>2020-12-27</td>
      <td>0.0137</td>
      <td>1226</td>
      <td>286</td>
      <td>state</td>
      <td>TO</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>1303980 rows × 17 columns</p>
</div>




```python
cidade1 =  dados.query('city == "Maringá"')
cidade1.to_csv("/home/mk/Documentos/maringa/maringa.csv", index=True)
cidade1
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city_ibge_code</th>
      <th>date</th>
      <th>epidemiological_week</th>
      <th>estimated_population</th>
      <th>estimated_population_2019</th>
      <th>is_last</th>
      <th>is_repeated</th>
      <th>last_available_confirmed</th>
      <th>last_available_confirmed_per_100k_inhabitants</th>
      <th>last_available_date</th>
      <th>last_available_death_rate</th>
      <th>last_available_deaths</th>
      <th>order_for_place</th>
      <th>place_type</th>
      <th>state</th>
      <th>new_confirmed</th>
      <th>new_deaths</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-03-18</td>
      <td>12</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.23247</td>
      <td>2020-03-18</td>
      <td>0.0000</td>
      <td>0</td>
      <td>1</td>
      <td>city</td>
      <td>PR</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-03-19</td>
      <td>12</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.23247</td>
      <td>2020-03-19</td>
      <td>0.0000</td>
      <td>0</td>
      <td>2</td>
      <td>city</td>
      <td>PR</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-03-20</td>
      <td>12</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.23247</td>
      <td>2020-03-20</td>
      <td>0.0000</td>
      <td>0</td>
      <td>3</td>
      <td>city</td>
      <td>PR</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-03-21</td>
      <td>12</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.23247</td>
      <td>2020-03-21</td>
      <td>0.0000</td>
      <td>0</td>
      <td>4</td>
      <td>city</td>
      <td>PR</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-03-22</td>
      <td>13</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.23247</td>
      <td>2020-03-22</td>
      <td>0.0000</td>
      <td>0</td>
      <td>5</td>
      <td>city</td>
      <td>PR</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-12-24</td>
      <td>52</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>False</td>
      <td>False</td>
      <td>20847</td>
      <td>4846.37005</td>
      <td>2020-12-24</td>
      <td>0.0145</td>
      <td>303</td>
      <td>282</td>
      <td>city</td>
      <td>PR</td>
      <td>291</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-12-25</td>
      <td>52</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>False</td>
      <td>False</td>
      <td>21112</td>
      <td>4907.97546</td>
      <td>2020-12-25</td>
      <td>0.0145</td>
      <td>307</td>
      <td>283</td>
      <td>city</td>
      <td>PR</td>
      <td>265</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-12-26</td>
      <td>52</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>False</td>
      <td>False</td>
      <td>21112</td>
      <td>4907.97546</td>
      <td>2020-12-26</td>
      <td>0.0145</td>
      <td>307</td>
      <td>284</td>
      <td>city</td>
      <td>PR</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-12-27</td>
      <td>53</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>False</td>
      <td>False</td>
      <td>21126</td>
      <td>4911.23009</td>
      <td>2020-12-27</td>
      <td>0.0145</td>
      <td>307</td>
      <td>285</td>
      <td>city</td>
      <td>PR</td>
      <td>14</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Maringá</th>
      <td>4115200.0</td>
      <td>2020-12-28</td>
      <td>53</td>
      <td>430157.0</td>
      <td>423666.0</td>
      <td>True</td>
      <td>False</td>
      <td>21403</td>
      <td>4975.62518</td>
      <td>2020-12-28</td>
      <td>0.0145</td>
      <td>311</td>
      <td>286</td>
      <td>city</td>
      <td>PR</td>
      <td>277</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
<p>286 rows × 17 columns</p>
</div>




```python
cidade_sel1 = cidade1.filter(items=['date', 'last_available_confirmed', 'last_available_deaths'])
```


```python
cidade_sel1.T
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>city</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>...</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
      <th>Maringá</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>date</th>
      <td>2020-03-18</td>
      <td>2020-03-19</td>
      <td>2020-03-20</td>
      <td>2020-03-21</td>
      <td>2020-03-22</td>
      <td>2020-03-23</td>
      <td>2020-03-24</td>
      <td>2020-03-25</td>
      <td>2020-03-26</td>
      <td>2020-03-27</td>
      <td>...</td>
      <td>2020-12-19</td>
      <td>2020-12-20</td>
      <td>2020-12-21</td>
      <td>2020-12-22</td>
      <td>2020-12-23</td>
      <td>2020-12-24</td>
      <td>2020-12-25</td>
      <td>2020-12-26</td>
      <td>2020-12-27</td>
      <td>2020-12-28</td>
    </tr>
    <tr>
      <th>last_available_confirmed</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>7</td>
      <td>...</td>
      <td>18992</td>
      <td>19431</td>
      <td>19871</td>
      <td>20264</td>
      <td>20556</td>
      <td>20847</td>
      <td>21112</td>
      <td>21112</td>
      <td>21126</td>
      <td>21403</td>
    </tr>
    <tr>
      <th>last_available_deaths</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>...</td>
      <td>279</td>
      <td>279</td>
      <td>280</td>
      <td>290</td>
      <td>300</td>
      <td>303</td>
      <td>307</td>
      <td>307</td>
      <td>307</td>
      <td>311</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 286 columns</p>
</div>




```python
cidade_sel1.to_csv("/home/mk/Documentos/maringa_sel.csv", index=True)
```


```python
cidade_sel1.T.to_csv("/home/mk/Documentos/maringa_selT.csv", index=False)
```


```python
cidade2 =  dados.query('city == "Londrina"')
cidade2.to_csv("/home/mk/Documentos/maringa/londrina.csv", index=True)
cidade2
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city_ibge_code</th>
      <th>date</th>
      <th>epidemiological_week</th>
      <th>estimated_population</th>
      <th>estimated_population_2019</th>
      <th>is_last</th>
      <th>is_repeated</th>
      <th>last_available_confirmed</th>
      <th>last_available_confirmed_per_100k_inhabitants</th>
      <th>last_available_date</th>
      <th>last_available_death_rate</th>
      <th>last_available_deaths</th>
      <th>order_for_place</th>
      <th>place_type</th>
      <th>state</th>
      <th>new_confirmed</th>
      <th>new_deaths</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-03-17</td>
      <td>12</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.17380</td>
      <td>2020-03-17</td>
      <td>0.0000</td>
      <td>0</td>
      <td>1</td>
      <td>city</td>
      <td>PR</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-03-18</td>
      <td>12</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.17380</td>
      <td>2020-03-18</td>
      <td>0.0000</td>
      <td>0</td>
      <td>2</td>
      <td>city</td>
      <td>PR</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-03-19</td>
      <td>12</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>0.17380</td>
      <td>2020-03-19</td>
      <td>0.0000</td>
      <td>0</td>
      <td>3</td>
      <td>city</td>
      <td>PR</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-03-20</td>
      <td>12</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>False</td>
      <td>False</td>
      <td>3</td>
      <td>0.52140</td>
      <td>2020-03-20</td>
      <td>0.0000</td>
      <td>0</td>
      <td>4</td>
      <td>city</td>
      <td>PR</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-03-21</td>
      <td>12</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>False</td>
      <td>False</td>
      <td>3</td>
      <td>0.52140</td>
      <td>2020-03-21</td>
      <td>0.0000</td>
      <td>0</td>
      <td>5</td>
      <td>city</td>
      <td>PR</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-12-24</td>
      <td>52</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>False</td>
      <td>False</td>
      <td>21959</td>
      <td>3816.45426</td>
      <td>2020-12-24</td>
      <td>0.0173</td>
      <td>379</td>
      <td>283</td>
      <td>city</td>
      <td>PR</td>
      <td>361</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-12-25</td>
      <td>52</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>False</td>
      <td>False</td>
      <td>22140</td>
      <td>3847.91189</td>
      <td>2020-12-25</td>
      <td>0.0171</td>
      <td>379</td>
      <td>284</td>
      <td>city</td>
      <td>PR</td>
      <td>181</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-12-26</td>
      <td>52</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>False</td>
      <td>False</td>
      <td>22196</td>
      <td>3857.64464</td>
      <td>2020-12-26</td>
      <td>0.0171</td>
      <td>379</td>
      <td>285</td>
      <td>city</td>
      <td>PR</td>
      <td>56</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-12-27</td>
      <td>53</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>False</td>
      <td>False</td>
      <td>22330</td>
      <td>3880.93372</td>
      <td>2020-12-27</td>
      <td>0.0170</td>
      <td>379</td>
      <td>286</td>
      <td>city</td>
      <td>PR</td>
      <td>134</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Londrina</th>
      <td>4113700.0</td>
      <td>2020-12-28</td>
      <td>53</td>
      <td>575377.0</td>
      <td>569733.0</td>
      <td>True</td>
      <td>False</td>
      <td>22500</td>
      <td>3910.47956</td>
      <td>2020-12-28</td>
      <td>0.0168</td>
      <td>379</td>
      <td>287</td>
      <td>city</td>
      <td>PR</td>
      <td>170</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>287 rows × 17 columns</p>
</div>




```python
cidade_sel2 = cidade2.filter(items=['date', 'last_available_confirmed', 'last_available_deaths'])
```


```python
cidade_sel2.T
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>city</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>...</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
      <th>Londrina</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>date</th>
      <td>2020-03-17</td>
      <td>2020-03-18</td>
      <td>2020-03-19</td>
      <td>2020-03-20</td>
      <td>2020-03-21</td>
      <td>2020-03-22</td>
      <td>2020-03-23</td>
      <td>2020-03-24</td>
      <td>2020-03-25</td>
      <td>2020-03-26</td>
      <td>...</td>
      <td>2020-12-19</td>
      <td>2020-12-20</td>
      <td>2020-12-21</td>
      <td>2020-12-22</td>
      <td>2020-12-23</td>
      <td>2020-12-24</td>
      <td>2020-12-25</td>
      <td>2020-12-26</td>
      <td>2020-12-27</td>
      <td>2020-12-28</td>
    </tr>
    <tr>
      <th>last_available_confirmed</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>...</td>
      <td>20290</td>
      <td>20508</td>
      <td>20632</td>
      <td>21198</td>
      <td>21598</td>
      <td>21959</td>
      <td>22140</td>
      <td>22196</td>
      <td>22330</td>
      <td>22500</td>
    </tr>
    <tr>
      <th>last_available_deaths</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>377</td>
      <td>377</td>
      <td>377</td>
      <td>378</td>
      <td>379</td>
      <td>379</td>
      <td>379</td>
      <td>379</td>
      <td>379</td>
      <td>379</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 287 columns</p>
</div>




```python
cidade_sel2.to_csv("/home/mk/Documentos/londrina_sel.csv", index=True)
```


```python
cidade_sel1.T.to_csv("/home/mk/Documentos/maringa_selT.csv", index=False)
```


```python
frames = [cidade_sel1, cidade_sel2]
final = pd.concat(frames)
final = final.T
```


```python
final.to_csv("/home/mk/Documentos/maringa/final.csv", index=True)
```


```python
os.system('spd-say "Murilo Krominski"')
```
