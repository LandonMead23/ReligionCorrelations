# I don't like how this turned out

I'm really not happy with this at all and so I'm sorry if the horrid level of quality shows.

There was a lot of use of Gemini because time shortages and it made the project itself really feel lifeless to me. I want to try this again at a later time with a different research question, one that I can find a more solid correlation.


```python
import pandas as pd
import matplotlib.pyplot as plt
import plotly.express as px
import numpy as np
import plotly.figure_factory as ff
```


```python

#get df
dataf = pd.read_csv("https://query.data.world/s/atsel7i6wsljadsc5nbul2skjl6f2d?dws=00000")

#grab every country by the same year
df2010 = dataf[dataf["year"] == 2010]

#get new df with columns name and religious generalizations for the year 2000
religiongenpct_columns = [col for col in df2010.columns if col == ("pop") or col == ("chrstgenpct") or col == ("islmgenpct") or col == ("budgenpct") or col==("hindgenpct") or col==("sikhgenpct") or col==("judgenpct") or col==("confgenpct") or col==("othrgenpct") or col==("nonreligpct") or col==("sumreligpct")]
new_dfgenpct = df2010[["name"] + religiongenpct_columns]
new_dfgenpct.reset_index(drop=True, inplace=True)
new_dfgenpct
```





  <div id="df-07d06050-8c0c-4ff2-a46d-8226abb6efa0" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>pop</th>
      <th>chrstgenpct</th>
      <th>judgenpct</th>
      <th>islmgenpct</th>
      <th>budgenpct</th>
      <th>hindgenpct</th>
      <th>sikhgenpct</th>
      <th>confgenpct</th>
      <th>nonreligpct</th>
      <th>othrgenpct</th>
      <th>sumreligpct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>312750000</td>
      <td>0.7454</td>
      <td>0.0190</td>
      <td>0.0090</td>
      <td>0.0109</td>
      <td>0.0057</td>
      <td>0.0013</td>
      <td>0.0003</td>
      <td>0.1900</td>
      <td>0.0025</td>
      <td>0.9975</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CAN</td>
      <td>34500000</td>
      <td>0.7661</td>
      <td>0.0099</td>
      <td>0.0194</td>
      <td>0.0194</td>
      <td>0.0080</td>
      <td>0.0080</td>
      <td>0.0001</td>
      <td>0.1643</td>
      <td>0.0010</td>
      <td>0.9990</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BHM</td>
      <td>313312</td>
      <td>0.9660</td>
      <td>0.0010</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0290</td>
      <td>0.0005</td>
      <td>0.9995</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CUB</td>
      <td>11241161</td>
      <td>0.6589</td>
      <td>0.0001</td>
      <td>0.0007</td>
      <td>0.0000</td>
      <td>0.0022</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.1315</td>
      <td>0.0000</td>
      <td>1.2935</td>
    </tr>
    <tr>
      <th>4</th>
      <td>HAI</td>
      <td>9760832</td>
      <td>0.8200</td>
      <td>0.0000</td>
      <td>0.0002</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.1000</td>
      <td>0.0000</td>
      <td>1.3711</td>
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
    </tr>
    <tr>
      <th>189</th>
      <td>NAU</td>
      <td>9937</td>
      <td>0.9699</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0301</td>
      <td>0.9699</td>
    </tr>
    <tr>
      <th>190</th>
      <td>MSI</td>
      <td>54566</td>
      <td>0.9341</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0220</td>
      <td>0.0017</td>
      <td>0.9983</td>
    </tr>
    <tr>
      <th>191</th>
      <td>PAL</td>
      <td>21370</td>
      <td>0.8606</td>
      <td>0.0000</td>
      <td>0.0220</td>
      <td>0.0085</td>
      <td>0.0013</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0153</td>
      <td>0.0010</td>
      <td>0.9990</td>
    </tr>
    <tr>
      <th>192</th>
      <td>FSM</td>
      <td>110971</td>
      <td>0.8651</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0059</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0315</td>
      <td>0.0197</td>
      <td>0.9803</td>
    </tr>
    <tr>
      <th>193</th>
      <td>WSM</td>
      <td>188861</td>
      <td>0.9538</td>
      <td>0.0000</td>
      <td>0.0003</td>
      <td>0.0001</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0146</td>
      <td>0.0258</td>
      <td>0.9742</td>
    </tr>
  </tbody>
</table>
<p>194 rows × 12 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-07d06050-8c0c-4ff2-a46d-8226abb6efa0')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-07d06050-8c0c-4ff2-a46d-8226abb6efa0 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-07d06050-8c0c-4ff2-a46d-8226abb6efa0');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-50ae83b5-1d40-4fcd-bfef-2605c8f73566">
  <button class="colab-df-quickchart" onclick="quickchart('df-50ae83b5-1d40-4fcd-bfef-2605c8f73566')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-50ae83b5-1d40-4fcd-bfef-2605c8f73566 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_d6c47f45-0eed-467f-9176-6461f5566127">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('new_dfgenpct')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_d6c47f45-0eed-467f-9176-6461f5566127 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('new_dfgenpct');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
gdppercapdf = pd.read_csv("https://pastebin.com/raw/2GAsbJTS")
gdppercapdf.rename(columns={'Country Code': 'name'}, inplace=True)
gdppercapdf
```





  <div id="df-86a5f0eb-c60a-44bc-ac02-38db267c83e5" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>1995</th>
      <th>2000</th>
      <th>2005</th>
      <th>2010</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AFG</td>
      <td>0.000000</td>
      <td>180.188369</td>
      <td>254.115276</td>
      <td>562.499222</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ALB</td>
      <td>750.604449</td>
      <td>1126.683340</td>
      <td>2673.787816</td>
      <td>4094.349686</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DZA</td>
      <td>1466.544680</td>
      <td>1780.376063</td>
      <td>3248.099814</td>
      <td>4958.259379</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ASM</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8733.014287</td>
      <td>10446.863206</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AND</td>
      <td>18731.650185</td>
      <td>21674.299722</td>
      <td>39599.680444</td>
      <td>48237.891174</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>212</th>
      <td>VIR</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>40828.746093</td>
      <td>39905.128418</td>
    </tr>
    <tr>
      <th>213</th>
      <td>PSE</td>
      <td>1326.562857</td>
      <td>1476.171850</td>
      <td>1543.701414</td>
      <td>2557.075624</td>
    </tr>
    <tr>
      <th>214</th>
      <td>YEM</td>
      <td>794.639278</td>
      <td>519.591639</td>
      <td>784.757981</td>
      <td>1249.063085</td>
    </tr>
    <tr>
      <th>215</th>
      <td>ZMB</td>
      <td>438.383721</td>
      <td>364.026145</td>
      <td>720.446505</td>
      <td>1469.361450</td>
    </tr>
    <tr>
      <th>216</th>
      <td>ZWE</td>
      <td>646.829560</td>
      <td>565.284390</td>
      <td>470.783761</td>
      <td>937.840340</td>
    </tr>
  </tbody>
</table>
<p>217 rows × 5 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-86a5f0eb-c60a-44bc-ac02-38db267c83e5')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-86a5f0eb-c60a-44bc-ac02-38db267c83e5 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-86a5f0eb-c60a-44bc-ac02-38db267c83e5');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-3ebb1689-cb41-426e-9361-7be5e2d47d34">
  <button class="colab-df-quickchart" onclick="quickchart('df-3ebb1689-cb41-426e-9361-7be5e2d47d34')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-3ebb1689-cb41-426e-9361-7be5e2d47d34 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_7d5f1c23-998e-459b-9148-cf59a36d7dfb">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('gdppercapdf')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_7d5f1c23-998e-459b-9148-cf59a36d7dfb button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('gdppercapdf');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
# prompt: assign gdppercap values to the corresponding country code for the column for year 2010

#get df
dataf = pd.read_csv("https://query.data.world/s/atsel7i6wsljadsc5nbul2skjl6f2d?dws=00000")

#grab every country by the same year
df2010 = dataf[dataf["year"] == 2010]

#get new df with columns name and religious generalizations for the year 2000
religiongenpct_columns = [col for col in df2010.columns if col == ("pop") or col == ("chrstgenpct") or col == ("islmgenpct") or col == ("budgenpct") or col==("hindgenpct") or col==("sikhgenpct") or col==("judgenpct") or col==("confgenpct") or col==("othrgenpct") or col==("nonreligpct") or col==("sumreligpct")]
new_dfgenpct = df2010[["name"] + religiongenpct_columns]
new_dfgenpct.reset_index(drop=True, inplace=True)
new_dfgenpct
gdppercapdf = pd.read_csv("https://pastebin.com/raw/2GAsbJTS")
gdppercapdf.rename(columns={'Country Code': 'name'}, inplace=True)

# Merge the DataFrames based on the 'name' column
merged_df = pd.merge(new_dfgenpct, gdppercapdf[['name', '2010']], on='name', how='left')

# Now, the '2010' column in merged_df contains the GDP per capita for the year 2010
# for each country that exists in both DataFrames.

merged_df
```





  <div id="df-dd44f9be-a254-484d-b9a0-8ddd1f82c1e9" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>pop</th>
      <th>chrstgenpct</th>
      <th>judgenpct</th>
      <th>islmgenpct</th>
      <th>budgenpct</th>
      <th>hindgenpct</th>
      <th>sikhgenpct</th>
      <th>confgenpct</th>
      <th>nonreligpct</th>
      <th>othrgenpct</th>
      <th>sumreligpct</th>
      <th>2010</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>312750000</td>
      <td>0.7454</td>
      <td>0.0190</td>
      <td>0.0090</td>
      <td>0.0109</td>
      <td>0.0057</td>
      <td>0.0013</td>
      <td>0.0003</td>
      <td>0.1900</td>
      <td>0.0025</td>
      <td>0.9975</td>
      <td>48650.664323</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CAN</td>
      <td>34500000</td>
      <td>0.7661</td>
      <td>0.0099</td>
      <td>0.0194</td>
      <td>0.0194</td>
      <td>0.0080</td>
      <td>0.0080</td>
      <td>0.0001</td>
      <td>0.1643</td>
      <td>0.0010</td>
      <td>0.9990</td>
      <td>47560.666601</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BHM</td>
      <td>313312</td>
      <td>0.9660</td>
      <td>0.0010</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0290</td>
      <td>0.0005</td>
      <td>0.9995</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CUB</td>
      <td>11241161</td>
      <td>0.6589</td>
      <td>0.0001</td>
      <td>0.0007</td>
      <td>0.0000</td>
      <td>0.0022</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.1315</td>
      <td>0.0000</td>
      <td>1.2935</td>
      <td>5275.532601</td>
    </tr>
    <tr>
      <th>4</th>
      <td>HAI</td>
      <td>9760832</td>
      <td>0.8200</td>
      <td>0.0000</td>
      <td>0.0002</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.1000</td>
      <td>0.0000</td>
      <td>1.3711</td>
      <td>NaN</td>
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
    </tr>
    <tr>
      <th>189</th>
      <td>NAU</td>
      <td>9937</td>
      <td>0.9699</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0301</td>
      <td>0.9699</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>190</th>
      <td>MSI</td>
      <td>54566</td>
      <td>0.9341</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0220</td>
      <td>0.0017</td>
      <td>0.9983</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>191</th>
      <td>PAL</td>
      <td>21370</td>
      <td>0.8606</td>
      <td>0.0000</td>
      <td>0.0220</td>
      <td>0.0085</td>
      <td>0.0013</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0153</td>
      <td>0.0010</td>
      <td>0.9990</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>192</th>
      <td>FSM</td>
      <td>110971</td>
      <td>0.8651</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0059</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0315</td>
      <td>0.0197</td>
      <td>0.9803</td>
      <td>2760.011340</td>
    </tr>
    <tr>
      <th>193</th>
      <td>WSM</td>
      <td>188861</td>
      <td>0.9538</td>
      <td>0.0000</td>
      <td>0.0003</td>
      <td>0.0001</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0146</td>
      <td>0.0258</td>
      <td>0.9742</td>
      <td>3494.395225</td>
    </tr>
  </tbody>
</table>
<p>194 rows × 13 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-dd44f9be-a254-484d-b9a0-8ddd1f82c1e9')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-dd44f9be-a254-484d-b9a0-8ddd1f82c1e9 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-dd44f9be-a254-484d-b9a0-8ddd1f82c1e9');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-592a3724-3cfb-4245-8beb-d773016b32f1">
  <button class="colab-df-quickchart" onclick="quickchart('df-592a3724-3cfb-4245-8beb-d773016b32f1')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-592a3724-3cfb-4245-8beb-d773016b32f1 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_ce11781d-53ab-4daf-b6d2-666574ed93ab">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('merged_df')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_ce11781d-53ab-4daf-b6d2-666574ed93ab button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('merged_df');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
# prompt: turn the NaN in the 2010 column into nulls


# ... (Your existing code) ...

# Merge the DataFrames based on the 'name' column
merged_df = pd.merge(new_dfgenpct, gdppercapdf[['name', '2010']], on='name', how='left')

merged_df.rename(columns={'2010': 'GDP/Cap for 2010'}, inplace=True)
# Replace NaN values in the '2010' column with None
merged_df['GDP/Cap for 2010'] = merged_df['GDP/Cap for 2010'].fillna(0)

merged_df
```





  <div id="df-7a4efa5c-99b7-46e5-a62e-1fed3f30b690" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>pop</th>
      <th>chrstgenpct</th>
      <th>judgenpct</th>
      <th>islmgenpct</th>
      <th>budgenpct</th>
      <th>hindgenpct</th>
      <th>sikhgenpct</th>
      <th>confgenpct</th>
      <th>nonreligpct</th>
      <th>othrgenpct</th>
      <th>sumreligpct</th>
      <th>GDP/Cap for 2010</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>312750000</td>
      <td>0.7454</td>
      <td>0.0190</td>
      <td>0.0090</td>
      <td>0.0109</td>
      <td>0.0057</td>
      <td>0.0013</td>
      <td>0.0003</td>
      <td>0.1900</td>
      <td>0.0025</td>
      <td>0.9975</td>
      <td>48650.664323</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CAN</td>
      <td>34500000</td>
      <td>0.7661</td>
      <td>0.0099</td>
      <td>0.0194</td>
      <td>0.0194</td>
      <td>0.0080</td>
      <td>0.0080</td>
      <td>0.0001</td>
      <td>0.1643</td>
      <td>0.0010</td>
      <td>0.9990</td>
      <td>47560.666601</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BHM</td>
      <td>313312</td>
      <td>0.9660</td>
      <td>0.0010</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0290</td>
      <td>0.0005</td>
      <td>0.9995</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CUB</td>
      <td>11241161</td>
      <td>0.6589</td>
      <td>0.0001</td>
      <td>0.0007</td>
      <td>0.0000</td>
      <td>0.0022</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.1315</td>
      <td>0.0000</td>
      <td>1.2935</td>
      <td>5275.532601</td>
    </tr>
    <tr>
      <th>4</th>
      <td>HAI</td>
      <td>9760832</td>
      <td>0.8200</td>
      <td>0.0000</td>
      <td>0.0002</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.1000</td>
      <td>0.0000</td>
      <td>1.3711</td>
      <td>0.000000</td>
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
    </tr>
    <tr>
      <th>189</th>
      <td>NAU</td>
      <td>9937</td>
      <td>0.9699</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0301</td>
      <td>0.9699</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>190</th>
      <td>MSI</td>
      <td>54566</td>
      <td>0.9341</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0220</td>
      <td>0.0017</td>
      <td>0.9983</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>191</th>
      <td>PAL</td>
      <td>21370</td>
      <td>0.8606</td>
      <td>0.0000</td>
      <td>0.0220</td>
      <td>0.0085</td>
      <td>0.0013</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0153</td>
      <td>0.0010</td>
      <td>0.9990</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>192</th>
      <td>FSM</td>
      <td>110971</td>
      <td>0.8651</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0059</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0315</td>
      <td>0.0197</td>
      <td>0.9803</td>
      <td>2760.011340</td>
    </tr>
    <tr>
      <th>193</th>
      <td>WSM</td>
      <td>188861</td>
      <td>0.9538</td>
      <td>0.0000</td>
      <td>0.0003</td>
      <td>0.0001</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0146</td>
      <td>0.0258</td>
      <td>0.9742</td>
      <td>3494.395225</td>
    </tr>
  </tbody>
</table>
<p>194 rows × 13 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-7a4efa5c-99b7-46e5-a62e-1fed3f30b690')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-7a4efa5c-99b7-46e5-a62e-1fed3f30b690 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-7a4efa5c-99b7-46e5-a62e-1fed3f30b690');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-4bc58c82-666f-4a69-8fac-1eb94cfa72a9">
  <button class="colab-df-quickchart" onclick="quickchart('df-4bc58c82-666f-4a69-8fac-1eb94cfa72a9')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-4bc58c82-666f-4a69-8fac-1eb94cfa72a9 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_fce5e5ac-69d7-41ae-a47e-75c8734a87d3">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('merged_df')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_fce5e5ac-69d7-41ae-a47e-75c8734a87d3 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('merged_df');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
# prompt: write a piece of code to fix the countries in merged_df with sum of the religious percentages column, denoted by "sumreligct", greater than 1 and make them equal to the sum of each of the religious affiliation percentages

# ... (Your existing code) ...

# Iterate through the rows of the DataFrame
for index, row in merged_df.iterrows():
  if row['sumreligpct'] > 1:
    # Calculate the sum of religious affiliation percentages
    religious_percentages = [
        row['chrstgenpct'], row['islmgenpct'], row['budgenpct'],
        row['hindgenpct'], row['sikhgenpct'], row['judgenpct'],
        row['confgenpct'], row['othrgenpct']
    ]

    # Replace NaN values with 0 if present in the religious_percentages
    religious_percentages = [0 if pd.isnull(x) else x for x in religious_percentages]

    # Recalculate sumreligpct with the existing percentages
    sum_religious_percentages = sum(religious_percentages)

    # Update the sumreligpct value if it is greater than 1
    if sum_religious_percentages < 1:
      merged_df.at[index, 'sumreligpct'] = sum_religious_percentages

# ... (Rest of your code) ...
```


```python
merged_df = merged_df.dropna(subset=['GDP/Cap for 2010'])
```


```python
dfedu = pd.read_csv("GDL-Custom-set-of-indicators-(2010)-data.csv")
dfedu.rename(columns={'ISO_Code': 'name'}, inplace=True)
dfedu.drop(columns=['Country', 'Continent', 'Level'], inplace=True)
dfedu
```





  <div id="df-6b2af772-8559-418d-85b5-30746f69098e" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>GDLCODE</th>
      <th>Region</th>
      <th>Educational index</th>
      <th>Mean years schooling</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AFG</td>
      <td>AFGt</td>
      <td>Total</td>
      <td>0.318</td>
      <td>1.890</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ALB</td>
      <td>ALBt</td>
      <td>Total</td>
      <td>0.715</td>
      <td>9.627</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DZA</td>
      <td>DZAt</td>
      <td>Total</td>
      <td>0.639</td>
      <td>7.320</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AND</td>
      <td>ANDt</td>
      <td>Total</td>
      <td>0.693</td>
      <td>10.530</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AGO</td>
      <td>AGOt</td>
      <td>Total</td>
      <td>0.380</td>
      <td>3.829</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>182</th>
      <td>VNM</td>
      <td>VNMt</td>
      <td>Total</td>
      <td>0.602</td>
      <td>7.627</td>
    </tr>
    <tr>
      <th>183</th>
      <td>PSE</td>
      <td>PSEt</td>
      <td>Total</td>
      <td>0.649</td>
      <td>8.306</td>
    </tr>
    <tr>
      <th>184</th>
      <td>YEM</td>
      <td>YEMt</td>
      <td>Total</td>
      <td>0.309</td>
      <td>2.600</td>
    </tr>
    <tr>
      <th>185</th>
      <td>ZMB</td>
      <td>ZMBt</td>
      <td>Total</td>
      <td>0.515</td>
      <td>6.301</td>
    </tr>
    <tr>
      <th>186</th>
      <td>ZWE</td>
      <td>ZWEt</td>
      <td>Total</td>
      <td>0.555</td>
      <td>7.666</td>
    </tr>
  </tbody>
</table>
<p>187 rows × 5 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-6b2af772-8559-418d-85b5-30746f69098e')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-6b2af772-8559-418d-85b5-30746f69098e button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-6b2af772-8559-418d-85b5-30746f69098e');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-e93ec21a-1bcb-4f0c-a9f4-04dd78a57be4">
  <button class="colab-df-quickchart" onclick="quickchart('df-e93ec21a-1bcb-4f0c-a9f4-04dd78a57be4')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-e93ec21a-1bcb-4f0c-a9f4-04dd78a57be4 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_1daa6d7d-c687-400c-9ce0-813395a6efb4">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('dfedu')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_1daa6d7d-c687-400c-9ce0-813395a6efb4 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('dfedu');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
# prompt: merge dfedu and merged_df where each country code matches

# Merge dfedu and merged_df based on the 'name' column
merged_df_edu = pd.merge(merged_df, dfedu, on='name', how='left')
merged_df_edu.drop(columns=['Region', 'GDLCODE'], inplace=True)
merged_df_edu.head()
# Now, merged_df_edu contains the data from both merged_df and dfedu,
# with matching country codes.
```





  <div id="df-39ca4401-b268-40ad-a5a4-fecda70f1bf1" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>pop</th>
      <th>chrstgenpct</th>
      <th>judgenpct</th>
      <th>islmgenpct</th>
      <th>budgenpct</th>
      <th>hindgenpct</th>
      <th>sikhgenpct</th>
      <th>confgenpct</th>
      <th>nonreligpct</th>
      <th>othrgenpct</th>
      <th>sumreligpct</th>
      <th>GDP/Cap for 2010</th>
      <th>Educational index</th>
      <th>Mean years schooling</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>312750000</td>
      <td>0.7454</td>
      <td>0.0190</td>
      <td>0.0090</td>
      <td>0.0109</td>
      <td>0.0057</td>
      <td>0.0013</td>
      <td>0.0003</td>
      <td>0.1900</td>
      <td>0.0025</td>
      <td>0.9975</td>
      <td>48650.664323</td>
      <td>0.891</td>
      <td>13.05</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CAN</td>
      <td>34500000</td>
      <td>0.7661</td>
      <td>0.0099</td>
      <td>0.0194</td>
      <td>0.0194</td>
      <td>0.0080</td>
      <td>0.0080</td>
      <td>0.0001</td>
      <td>0.1643</td>
      <td>0.0010</td>
      <td>0.9990</td>
      <td>47560.666601</td>
      <td>0.872</td>
      <td>13.51</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BHM</td>
      <td>313312</td>
      <td>0.9660</td>
      <td>0.0010</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0290</td>
      <td>0.0005</td>
      <td>0.9995</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CUB</td>
      <td>11241161</td>
      <td>0.6589</td>
      <td>0.0001</td>
      <td>0.0007</td>
      <td>0.0000</td>
      <td>0.0022</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.1315</td>
      <td>0.0000</td>
      <td>0.6619</td>
      <td>5275.532601</td>
      <td>0.826</td>
      <td>11.23</td>
    </tr>
    <tr>
      <th>4</th>
      <td>HAI</td>
      <td>9760832</td>
      <td>0.8200</td>
      <td>0.0000</td>
      <td>0.0002</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.1000</td>
      <td>0.0000</td>
      <td>0.8202</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-39ca4401-b268-40ad-a5a4-fecda70f1bf1')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-39ca4401-b268-40ad-a5a4-fecda70f1bf1 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-39ca4401-b268-40ad-a5a4-fecda70f1bf1');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-f8ded978-683b-45a2-a40a-5db5975fa220">
  <button class="colab-df-quickchart" onclick="quickchart('df-f8ded978-683b-45a2-a40a-5db5975fa220')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-f8ded978-683b-45a2-a40a-5db5975fa220 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

    </div>
  </div>





```python
HouseIncomeandUnemployment = pd.read_csv("HouseholdIncome.csv")
HouseIncomeandUnemployment
```





  <div id="df-958725f1-f752-468b-8b16-6c5c64c651c6" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>2014 Unemployment Rate (percent)</th>
      <th>2015 Unemployment Rate (percent)</th>
      <th>2016 Unemployment Rate (percent)</th>
      <th>2017 Unemployment Rate (percent)</th>
      <th>2018 Unemployment Rate (percent)</th>
      <th>2019 Unemployment Rate (percent)</th>
      <th>2020 Unemployment Rate (percent)</th>
      <th>2021 Unemployment Rate (percent)</th>
      <th>2022 Unemployment Rate (percent)</th>
      <th>Median Household Income (2021)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alabama</td>
      <td>6.7</td>
      <td>6.1</td>
      <td>5.9</td>
      <td>4.5</td>
      <td>3.9</td>
      <td>3.2</td>
      <td>6.4</td>
      <td>3.4</td>
      <td>2.5</td>
      <td>$53,990.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alaska</td>
      <td>6.7</td>
      <td>6.3</td>
      <td>6.6</td>
      <td>6.5</td>
      <td>6.0</td>
      <td>5.6</td>
      <td>8.3</td>
      <td>6.4</td>
      <td>4.2</td>
      <td>$78,437.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arizona</td>
      <td>6.8</td>
      <td>6.1</td>
      <td>5.5</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>4.8</td>
      <td>7.8</td>
      <td>5.1</td>
      <td>3.8</td>
      <td>$68,967.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Arkansas</td>
      <td>5.9</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>3.7</td>
      <td>3.7</td>
      <td>3.5</td>
      <td>6.2</td>
      <td>4.0</td>
      <td>3.2</td>
      <td>$52,577.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>California</td>
      <td>7.6</td>
      <td>6.3</td>
      <td>5.5</td>
      <td>4.8</td>
      <td>4.2</td>
      <td>4.1</td>
      <td>10.1</td>
      <td>7.3</td>
      <td>4.3</td>
      <td>$84,831.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Colorado</td>
      <td>5.0</td>
      <td>3.7</td>
      <td>3.1</td>
      <td>2.6</td>
      <td>3.0</td>
      <td>2.7</td>
      <td>6.8</td>
      <td>5.5</td>
      <td>3.1</td>
      <td>$82,228.00</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Connecticut</td>
      <td>6.6</td>
      <td>5.6</td>
      <td>4.8</td>
      <td>4.4</td>
      <td>3.9</td>
      <td>3.6</td>
      <td>8.0</td>
      <td>6.4</td>
      <td>4.1</td>
      <td>$83,628.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Delaware</td>
      <td>5.6</td>
      <td>4.8</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>3.7</td>
      <td>3.6</td>
      <td>7.5</td>
      <td>5.5</td>
      <td>4.3</td>
      <td>$71,636.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>District of Columbia</td>
      <td>7.7</td>
      <td>6.9</td>
      <td>6.2</td>
      <td>6.1</td>
      <td>5.7</td>
      <td>5.5</td>
      <td>7.9</td>
      <td>6.8</td>
      <td>4.7</td>
      <td>$91,072.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Florida</td>
      <td>6.4</td>
      <td>5.5</td>
      <td>4.9</td>
      <td>4.3</td>
      <td>3.6</td>
      <td>3.3</td>
      <td>8.1</td>
      <td>4.7</td>
      <td>3.0</td>
      <td>$63,054.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Georgia</td>
      <td>7.1</td>
      <td>6.1</td>
      <td>5.4</td>
      <td>4.8</td>
      <td>4.0</td>
      <td>3.6</td>
      <td>6.5</td>
      <td>3.9</td>
      <td>3.1</td>
      <td>$66,507.00</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Hawaii</td>
      <td>4.2</td>
      <td>3.4</td>
      <td>2.9</td>
      <td>2.2</td>
      <td>2.4</td>
      <td>2.5</td>
      <td>11.7</td>
      <td>6.0</td>
      <td>3.3</td>
      <td>$85,547.00</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Idaho</td>
      <td>4.4</td>
      <td>3.9</td>
      <td>3.7</td>
      <td>3.2</td>
      <td>2.9</td>
      <td>2.9</td>
      <td>5.5</td>
      <td>3.6</td>
      <td>2.8</td>
      <td>$66,318.00</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Illinois</td>
      <td>7.2</td>
      <td>6.0</td>
      <td>5.9</td>
      <td>4.9</td>
      <td>4.4</td>
      <td>4.0</td>
      <td>9.3</td>
      <td>6.1</td>
      <td>4.6</td>
      <td>$72,215.00</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Indiana</td>
      <td>5.9</td>
      <td>4.8</td>
      <td>4.4</td>
      <td>3.5</td>
      <td>3.4</td>
      <td>3.3</td>
      <td>7.3</td>
      <td>3.9</td>
      <td>3.1</td>
      <td>$62,723.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Iowa</td>
      <td>4.2</td>
      <td>3.7</td>
      <td>3.6</td>
      <td>3.1</td>
      <td>2.6</td>
      <td>2.7</td>
      <td>5.2</td>
      <td>3.8</td>
      <td>2.8</td>
      <td>$65,645.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Kansas</td>
      <td>4.5</td>
      <td>4.2</td>
      <td>4.0</td>
      <td>3.6</td>
      <td>3.4</td>
      <td>3.2</td>
      <td>5.8</td>
      <td>3.3</td>
      <td>2.6</td>
      <td>$64,128.00</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Kentucky</td>
      <td>6.4</td>
      <td>5.2</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>4.2</td>
      <td>4.1</td>
      <td>6.5</td>
      <td>4.5</td>
      <td>4.0</td>
      <td>$55,532.00</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Louisiana</td>
      <td>6.3</td>
      <td>6.3</td>
      <td>6.1</td>
      <td>5.1</td>
      <td>4.8</td>
      <td>4.6</td>
      <td>8.6</td>
      <td>5.6</td>
      <td>3.7</td>
      <td>$52,090.00</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Maine</td>
      <td>5.6</td>
      <td>4.4</td>
      <td>3.8</td>
      <td>3.4</td>
      <td>3.2</td>
      <td>2.9</td>
      <td>5.1</td>
      <td>4.7</td>
      <td>2.8</td>
      <td>$64,823.00</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Maryland</td>
      <td>5.7</td>
      <td>5.0</td>
      <td>4.3</td>
      <td>4.0</td>
      <td>3.8</td>
      <td>3.4</td>
      <td>6.4</td>
      <td>5.2</td>
      <td>3.0</td>
      <td>$90,129.00</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Massachusetts</td>
      <td>5.7</td>
      <td>4.8</td>
      <td>4.0</td>
      <td>3.8</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>9.3</td>
      <td>5.4</td>
      <td>3.7</td>
      <td>$89,577.00</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Michigan</td>
      <td>7.2</td>
      <td>5.4</td>
      <td>5.0</td>
      <td>4.6</td>
      <td>4.2</td>
      <td>4.1</td>
      <td>10.0</td>
      <td>5.7</td>
      <td>4.1</td>
      <td>$63,444.00</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Minnesota</td>
      <td>4.3</td>
      <td>3.8</td>
      <td>3.9</td>
      <td>3.5</td>
      <td>3.0</td>
      <td>3.3</td>
      <td>6.3</td>
      <td>3.7</td>
      <td>2.6</td>
      <td>$77,712.00</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Mississippi</td>
      <td>7.6</td>
      <td>6.5</td>
      <td>5.9</td>
      <td>5.2</td>
      <td>4.9</td>
      <td>5.5</td>
      <td>8.0</td>
      <td>5.4</td>
      <td>3.8</td>
      <td>$48,871.00</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Missouri</td>
      <td>6.2</td>
      <td>5.1</td>
      <td>4.5</td>
      <td>3.7</td>
      <td>3.2</td>
      <td>3.2</td>
      <td>6.2</td>
      <td>4.2</td>
      <td>2.6</td>
      <td>$61,815.00</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Montana</td>
      <td>4.7</td>
      <td>4.3</td>
      <td>4.3</td>
      <td>4.1</td>
      <td>3.7</td>
      <td>3.5</td>
      <td>5.8</td>
      <td>3.4</td>
      <td>2.7</td>
      <td>$63,357.00</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Nebraska</td>
      <td>3.3</td>
      <td>3.0</td>
      <td>3.1</td>
      <td>3.0</td>
      <td>2.9</td>
      <td>3.1</td>
      <td>4.3</td>
      <td>2.6</td>
      <td>2.2</td>
      <td>$66,949.00</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Nevada</td>
      <td>8.2</td>
      <td>6.8</td>
      <td>5.8</td>
      <td>5.0</td>
      <td>4.4</td>
      <td>4.1</td>
      <td>13.5</td>
      <td>6.8</td>
      <td>5.2</td>
      <td>$66,194.00</td>
    </tr>
    <tr>
      <th>29</th>
      <td>New Hampshire</td>
      <td>4.3</td>
      <td>3.4</td>
      <td>2.9</td>
      <td>2.8</td>
      <td>2.6</td>
      <td>2.6</td>
      <td>6.7</td>
      <td>3.4</td>
      <td>2.3</td>
      <td>$88,268.00</td>
    </tr>
    <tr>
      <th>30</th>
      <td>New Jersey</td>
      <td>6.7</td>
      <td>5.7</td>
      <td>4.9</td>
      <td>4.5</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>9.4</td>
      <td>6.7</td>
      <td>3.9</td>
      <td>$89,227.00</td>
    </tr>
    <tr>
      <th>31</th>
      <td>New Mexico</td>
      <td>6.6</td>
      <td>6.6</td>
      <td>6.7</td>
      <td>6.1</td>
      <td>4.9</td>
      <td>5.0</td>
      <td>7.9</td>
      <td>7.1</td>
      <td>4.1</td>
      <td>$54,304.00</td>
    </tr>
    <tr>
      <th>32</th>
      <td>New York</td>
      <td>6.3</td>
      <td>5.2</td>
      <td>4.9</td>
      <td>4.6</td>
      <td>4.1</td>
      <td>3.9</td>
      <td>9.8</td>
      <td>7.1</td>
      <td>4.3</td>
      <td>$74,230.00</td>
    </tr>
    <tr>
      <th>33</th>
      <td>North Carolina</td>
      <td>6.1</td>
      <td>5.7</td>
      <td>5.1</td>
      <td>4.5</td>
      <td>4.0</td>
      <td>3.9</td>
      <td>7.2</td>
      <td>4.9</td>
      <td>3.7</td>
      <td>$61,997.00</td>
    </tr>
    <tr>
      <th>34</th>
      <td>North Dakota</td>
      <td>2.6</td>
      <td>2.8</td>
      <td>3.1</td>
      <td>2.6</td>
      <td>2.4</td>
      <td>2.2</td>
      <td>4.9</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>$67,603.00</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Ohio</td>
      <td>5.8</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>4.2</td>
      <td>8.2</td>
      <td>5.1</td>
      <td>4.0</td>
      <td>$62,286.00</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Oklahoma</td>
      <td>4.3</td>
      <td>4.3</td>
      <td>4.6</td>
      <td>4.0</td>
      <td>3.3</td>
      <td>3.1</td>
      <td>6.3</td>
      <td>4.0</td>
      <td>3.1</td>
      <td>$55,829.00</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Oregon</td>
      <td>6.7</td>
      <td>5.5</td>
      <td>4.7</td>
      <td>4.1</td>
      <td>4.0</td>
      <td>3.7</td>
      <td>7.6</td>
      <td>5.2</td>
      <td>3.9</td>
      <td>$71,441.00</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Pennsylvania</td>
      <td>5.9</td>
      <td>5.4</td>
      <td>5.3</td>
      <td>5.0</td>
      <td>4.4</td>
      <td>4.3</td>
      <td>8.9</td>
      <td>5.9</td>
      <td>4.1</td>
      <td>$68,931.00</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Rhode Island</td>
      <td>7.8</td>
      <td>6.0</td>
      <td>5.2</td>
      <td>4.5</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>9.2</td>
      <td>5.5</td>
      <td>3.2</td>
      <td>$73,324.00</td>
    </tr>
    <tr>
      <th>40</th>
      <td>South Carolina</td>
      <td>6.3</td>
      <td>5.9</td>
      <td>4.9</td>
      <td>4.2</td>
      <td>3.4</td>
      <td>2.8</td>
      <td>6.0</td>
      <td>3.9</td>
      <td>3.2</td>
      <td>$59,447.00</td>
    </tr>
    <tr>
      <th>41</th>
      <td>South Dakota</td>
      <td>3.3</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>3.1</td>
      <td>2.8</td>
      <td>2.8</td>
      <td>4.2</td>
      <td>2.6</td>
      <td>2.0</td>
      <td>$66,843.00</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Tennessee</td>
      <td>6.6</td>
      <td>5.6</td>
      <td>4.7</td>
      <td>3.7</td>
      <td>3.5</td>
      <td>3.3</td>
      <td>7.4</td>
      <td>4.5</td>
      <td>3.4</td>
      <td>$59,698.00</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Texas</td>
      <td>5.2</td>
      <td>4.5</td>
      <td>4.6</td>
      <td>4.3</td>
      <td>3.9</td>
      <td>3.5</td>
      <td>7.7</td>
      <td>5.6</td>
      <td>3.9</td>
      <td>$66,959.00</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Utah</td>
      <td>3.6</td>
      <td>3.5</td>
      <td>3.3</td>
      <td>3.1</td>
      <td>2.9</td>
      <td>2.5</td>
      <td>4.8</td>
      <td>2.8</td>
      <td>2.4</td>
      <td>$79,449.00</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Vermont</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>3.1</td>
      <td>3.0</td>
      <td>2.5</td>
      <td>2.1</td>
      <td>5.6</td>
      <td>3.6</td>
      <td>2.3</td>
      <td>$72,415.00</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Virginia</td>
      <td>5.1</td>
      <td>4.4</td>
      <td>4.0</td>
      <td>3.7</td>
      <td>3.0</td>
      <td>2.8</td>
      <td>6.4</td>
      <td>3.9</td>
      <td>2.8</td>
      <td>$80,926.00</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Washington</td>
      <td>5.9</td>
      <td>5.4</td>
      <td>5.2</td>
      <td>4.6</td>
      <td>4.4</td>
      <td>4.2</td>
      <td>8.5</td>
      <td>5.2</td>
      <td>4.1</td>
      <td>$84,155.00</td>
    </tr>
    <tr>
      <th>48</th>
      <td>West Virginia</td>
      <td>6.5</td>
      <td>6.6</td>
      <td>6.1</td>
      <td>5.2</td>
      <td>5.1</td>
      <td>5.0</td>
      <td>8.2</td>
      <td>5.1</td>
      <td>3.9</td>
      <td>$51,122.00</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Wisconsin</td>
      <td>5.3</td>
      <td>4.4</td>
      <td>3.9</td>
      <td>3.3</td>
      <td>3.0</td>
      <td>3.2</td>
      <td>6.4</td>
      <td>3.9</td>
      <td>2.9</td>
      <td>$67,150.00</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Wyoming</td>
      <td>4.3</td>
      <td>4.2</td>
      <td>5.4</td>
      <td>4.3</td>
      <td>4.1</td>
      <td>3.7</td>
      <td>5.9</td>
      <td>4.5</td>
      <td>3.4</td>
      <td>$66,508.00</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Puerto Rico</td>
      <td>13.9</td>
      <td>12.0</td>
      <td>11.8</td>
      <td>10.8</td>
      <td>9.2</td>
      <td>8.3</td>
      <td>NaN</td>
      <td>7.9</td>
      <td>6.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-958725f1-f752-468b-8b16-6c5c64c651c6')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-958725f1-f752-468b-8b16-6c5c64c651c6 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-958725f1-f752-468b-8b16-6c5c64c651c6');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-8e111860-76fa-4b94-b70c-833acc14223f">
  <button class="colab-df-quickchart" onclick="quickchart('df-8e111860-76fa-4b94-b70c-833acc14223f')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-8e111860-76fa-4b94-b70c-833acc14223f button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_402290d9-7437-4433-ae53-33b0318ffd62">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('HouseIncomeandUnemployment')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_402290d9-7437-4433-ae53-33b0318ffd62 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('HouseIncomeandUnemployment');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
IncomeByCountyandState = pd.read_csv('Personal_Income_By_County.csv')
IncomeByCountyandState.drop('Unnamed: 9', axis=1, inplace=True)
```


```python
# prompt: use the incomebycountyandstate and make a new dataframe called incomebycounty that takes all of the data, but excludes the rows where the state and county column names are the same

IncomebyCounty = IncomeByCountyandState[IncomeByCountyandState['State'] != IncomeByCountyandState['County']]
IncomebyCounty
```





  <div id="df-cba661d2-1c46-4c5f-b3d6-442410d7a09e" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>State</th>
      <th>County</th>
      <th>2020 Income</th>
      <th>2021 Income</th>
      <th>2022 Income</th>
      <th>2021 Rank In State</th>
      <th>2021 Percent Change</th>
      <th>2022 Percent Change</th>
      <th>2022 Rank in State</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Alabama</td>
      <td>Autauga</td>
      <td>45,151</td>
      <td>48,914</td>
      <td>49,391</td>
      <td>9</td>
      <td>8.3</td>
      <td>1.0</td>
      <td>29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alabama</td>
      <td>Baldwin</td>
      <td>51,230</td>
      <td>55,865</td>
      <td>56,747</td>
      <td>4</td>
      <td>9.0</td>
      <td>1.6</td>
      <td>21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alabama</td>
      <td>Barbour</td>
      <td>37,111</td>
      <td>40,795</td>
      <td>40,560</td>
      <td>52</td>
      <td>9.9</td>
      <td>-0.6</td>
      <td>53</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alabama</td>
      <td>Bibb</td>
      <td>34,938</td>
      <td>37,175</td>
      <td>37,513</td>
      <td>66</td>
      <td>6.4</td>
      <td>0.9</td>
      <td>30</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Alabama</td>
      <td>Blount</td>
      <td>38,133</td>
      <td>42,852</td>
      <td>43,744</td>
      <td>33</td>
      <td>12.4</td>
      <td>2.1</td>
      <td>16</td>
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
    </tr>
    <tr>
      <th>3128</th>
      <td>Wyoming</td>
      <td>Sweetwater</td>
      <td>54,708</td>
      <td>56,252</td>
      <td>58,374</td>
      <td>12</td>
      <td>2.8</td>
      <td>3.8</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3129</th>
      <td>Wyoming</td>
      <td>Teton</td>
      <td>300,665</td>
      <td>362,522</td>
      <td>406,054</td>
      <td>1</td>
      <td>20.6</td>
      <td>12.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3130</th>
      <td>Wyoming</td>
      <td>Uinta</td>
      <td>42,289</td>
      <td>44,358</td>
      <td>44,775</td>
      <td>23</td>
      <td>4.9</td>
      <td>0.9</td>
      <td>17</td>
    </tr>
    <tr>
      <th>3131</th>
      <td>Wyoming</td>
      <td>Washakie</td>
      <td>55,098</td>
      <td>54,898</td>
      <td>55,288</td>
      <td>16</td>
      <td>-0.4</td>
      <td>0.7</td>
      <td>19</td>
    </tr>
    <tr>
      <th>3132</th>
      <td>Wyoming</td>
      <td>Weston</td>
      <td>49,854</td>
      <td>49,734</td>
      <td>50,987</td>
      <td>19</td>
      <td>-0.2</td>
      <td>2.5</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
<p>3076 rows × 9 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-cba661d2-1c46-4c5f-b3d6-442410d7a09e')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-cba661d2-1c46-4c5f-b3d6-442410d7a09e button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-cba661d2-1c46-4c5f-b3d6-442410d7a09e');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-c7e7d983-080c-46ee-b583-7f468e7d5fcd">
  <button class="colab-df-quickchart" onclick="quickchart('df-c7e7d983-080c-46ee-b583-7f468e7d5fcd')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-c7e7d983-080c-46ee-b583-7f468e7d5fcd button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_bb7de64a-b667-4858-89bb-6175ce9e07e4">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('IncomebyCounty')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_bb7de64a-b667-4858-89bb-6175ce9e07e4 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('IncomebyCounty');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
religionbycounty = pd.read_csv('ReligionByCountyUSCensus.csv')

# prompt: make all values incolumn TOTRATE_2020, if greater than 100, to NaN

# Assuming 'religionbycounty' is your DataFrame
religionbycounty.loc[religionbycounty['TOTRATE_2020'] > 100, 'TOTRATE_2020'] = np.nan
religionbycounty['TOTRATE_2020'].max()
```




    98.9600067138672



Reading the file of the US Census data, while incomplete, shed's light on the large Christian population.

This second part will eliminate all the big outliers that make my trends horrible fits


```python
# prompt: organize the county names in religionbycounty by state alphabetical orger, and county alphabetical order

# Sort religionbycounty by state and then county alphabetically
religionbycounty_sorted = religionbycounty.sort_values(['STATNAM', 'COUNAM'], ascending=[True, True])

# Display the sorted DataFrame
religionbycounty_sorted
```





  <div id="df-fde15f2a-7629-44a5-9dcb-812e7706e698" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>STCOD</th>
      <th>CTYCOD</th>
      <th>FIPS</th>
      <th>COUNAM</th>
      <th>STABBREV</th>
      <th>STATNAM</th>
      <th>POP1980</th>
      <th>POP1990</th>
      <th>POP2000</th>
      <th>POP2010</th>
      <th>...</th>
      <th>WELSADH_2020</th>
      <th>WELSRATE_2020</th>
      <th>WMCOCNG_2020</th>
      <th>WMCOADH_2020</th>
      <th>WMCORATE_2020</th>
      <th>WMCOICNG_2020</th>
      <th>WMCOIADH_2020</th>
      <th>WMCOIRATE_2020</th>
      <th>SIKHCNG_2020</th>
      <th>ZOROCNG_2020</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2257</th>
      <td>1</td>
      <td>1</td>
      <td>1001</td>
      <td>Autauga County</td>
      <td>AL</td>
      <td>Alabama</td>
      <td>32259.0</td>
      <td>34222.0</td>
      <td>43671.0</td>
      <td>54571.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2847</th>
      <td>1</td>
      <td>3</td>
      <td>1003</td>
      <td>Baldwin County</td>
      <td>AL</td>
      <td>Alabama</td>
      <td>78556.0</td>
      <td>98280.0</td>
      <td>140415.0</td>
      <td>182265.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1548</th>
      <td>1</td>
      <td>5</td>
      <td>1005</td>
      <td>Barbour County</td>
      <td>AL</td>
      <td>Alabama</td>
      <td>24756.0</td>
      <td>25417.0</td>
      <td>29038.0</td>
      <td>27457.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1444</th>
      <td>1</td>
      <td>7</td>
      <td>1007</td>
      <td>Bibb County</td>
      <td>AL</td>
      <td>Alabama</td>
      <td>15723.0</td>
      <td>16576.0</td>
      <td>20826.0</td>
      <td>22915.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2261</th>
      <td>1</td>
      <td>9</td>
      <td>1009</td>
      <td>Blount County</td>
      <td>AL</td>
      <td>Alabama</td>
      <td>36459.0</td>
      <td>39248.0</td>
      <td>51024.0</td>
      <td>57322.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>56</td>
      <td>37</td>
      <td>56037</td>
      <td>Sweetwater County</td>
      <td>WY</td>
      <td>Wyoming</td>
      <td>41723.0</td>
      <td>38823.0</td>
      <td>37613.0</td>
      <td>43806.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1475</th>
      <td>56</td>
      <td>39</td>
      <td>56039</td>
      <td>Teton County</td>
      <td>WY</td>
      <td>Wyoming</td>
      <td>9355.0</td>
      <td>11172.0</td>
      <td>18251.0</td>
      <td>21294.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1348</th>
      <td>56</td>
      <td>41</td>
      <td>56041</td>
      <td>Uinta County</td>
      <td>WY</td>
      <td>Wyoming</td>
      <td>13021.0</td>
      <td>18705.0</td>
      <td>19742.0</td>
      <td>21118.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>544</th>
      <td>56</td>
      <td>43</td>
      <td>56043</td>
      <td>Washakie County</td>
      <td>WY</td>
      <td>Wyoming</td>
      <td>9496.0</td>
      <td>8388.0</td>
      <td>8289.0</td>
      <td>8533.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>472</th>
      <td>56</td>
      <td>45</td>
      <td>56045</td>
      <td>Weston County</td>
      <td>WY</td>
      <td>Wyoming</td>
      <td>7106.0</td>
      <td>6518.0</td>
      <td>6644.0</td>
      <td>7208.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>3143 rows × 838 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-fde15f2a-7629-44a5-9dcb-812e7706e698')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-fde15f2a-7629-44a5-9dcb-812e7706e698 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-fde15f2a-7629-44a5-9dcb-812e7706e698');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-3fdcf056-c9d0-4b43-aedf-068faf530cff">
  <button class="colab-df-quickchart" onclick="quickchart('df-3fdcf056-c9d0-4b43-aedf-068faf530cff')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-3fdcf056-c9d0-4b43-aedf-068faf530cff button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_d9e766de-0d20-4da3-93fb-39b7e46a2492">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('religionbycounty_sorted')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_d9e766de-0d20-4da3-93fb-39b7e46a2492 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('religionbycounty_sorted');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
# prompt: merge religionbycounty and incomebycounty where STATNAM and State are equal and so are the first word in COUNAM and County

# Assuming 'religionbycounty' and 'IncomebyCounty' are your DataFrames

# Convert the 'COUNAM' column to string type in both DataFrames
religionbycounty['COUNAM'] = religionbycounty['COUNAM'].astype(str)
IncomebyCounty['County'] = IncomebyCounty['County'].astype(str)

# Extract the first word from the 'COUNAM' column in religionbycounty
religionbycounty['FirstWord_COUNAM'] = religionbycounty['COUNAM'].str.split().str[0]

# Extract the first word from the 'County' column in IncomebyCounty
IncomebyCounty['FirstWord_County'] = IncomebyCounty['County'].str.split().str[0]

# Merge the DataFrames on 'STATNAM' and 'State', and 'FirstWord_COUNAM' and 'FirstWord_County'
IncomeAndReligionByCounty = pd.merge(religionbycounty, IncomebyCounty,
                    left_on=['STATNAM', 'FirstWord_COUNAM'],
                    right_on=['State', 'FirstWord_County'],
                    how='inner')

# Now 'merged_df' contains the merged data where the 'STATNAM' and 'State' columns match,
# and the first word of 'COUNAM' and 'County' also match.
IncomeAndReligionByCounty.drop(columns=['STCOD', 'CTYCOD', 'FIPS', 'STABBREV'], inplace=True)
IncomeAndReligionByCounty
```





  <div id="df-6173ccee-8e5d-49d5-b2c7-0b0451f685b8" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>COUNAM</th>
      <th>STATNAM</th>
      <th>POP1980</th>
      <th>POP1990</th>
      <th>POP2000</th>
      <th>POP2010</th>
      <th>POP2020</th>
      <th>TOTCNG_2020</th>
      <th>TOTADH_2020</th>
      <th>TOTRATE_2020</th>
      <th>...</th>
      <th>State</th>
      <th>County</th>
      <th>2020 Income</th>
      <th>2021 Income</th>
      <th>2022 Income</th>
      <th>2021 Rank In State</th>
      <th>2021 Percent Change</th>
      <th>2022 Percent Change</th>
      <th>2022 Rank in State</th>
      <th>FirstWord_County</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Loving County</td>
      <td>Texas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>82.0</td>
      <td>64</td>
      <td>0</td>
      <td>0</td>
      <td>0.000000</td>
      <td>...</td>
      <td>Texas</td>
      <td>Loving</td>
      <td>108,092</td>
      <td>123,456</td>
      <td>141,373</td>
      <td>2</td>
      <td>14.2</td>
      <td>14.5</td>
      <td>9</td>
      <td>Loving</td>
    </tr>
    <tr>
      <th>1</th>
      <td>King County</td>
      <td>Texas</td>
      <td>425.0</td>
      <td>354.0</td>
      <td>356.0</td>
      <td>286.0</td>
      <td>265</td>
      <td>2</td>
      <td>1199</td>
      <td>52.726473</td>
      <td>...</td>
      <td>Texas</td>
      <td>King</td>
      <td>82,906</td>
      <td>87,145</td>
      <td>113,494</td>
      <td>7</td>
      <td>5.1</td>
      <td>30.2</td>
      <td>1</td>
      <td>King</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kenedy County</td>
      <td>Texas</td>
      <td>543.0</td>
      <td>460.0</td>
      <td>414.0</td>
      <td>416.0</td>
      <td>350</td>
      <td>1</td>
      <td>221</td>
      <td>63.139999</td>
      <td>...</td>
      <td>Texas</td>
      <td>Kenedy</td>
      <td>49,464</td>
      <td>41,424</td>
      <td>38,232</td>
      <td>241</td>
      <td>-16.3</td>
      <td>-7.7</td>
      <td>244</td>
      <td>Kenedy</td>
    </tr>
    <tr>
      <th>3</th>
      <td>McPherson County</td>
      <td>Nebraska</td>
      <td>593.0</td>
      <td>546.0</td>
      <td>533.0</td>
      <td>539.0</td>
      <td>399</td>
      <td>2</td>
      <td>134</td>
      <td>33.590000</td>
      <td>...</td>
      <td>Nebraska</td>
      <td>McPherson</td>
      <td>67,559</td>
      <td>59,652</td>
      <td>55,976</td>
      <td>64</td>
      <td>-11.7</td>
      <td>-6.2</td>
      <td>72</td>
      <td>McPherson</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blaine County</td>
      <td>Nebraska</td>
      <td>867.0</td>
      <td>675.0</td>
      <td>583.0</td>
      <td>478.0</td>
      <td>431</td>
      <td>5</td>
      <td>253</td>
      <td>58.699997</td>
      <td>...</td>
      <td>Nebraska</td>
      <td>Blaine</td>
      <td>70,770</td>
      <td>58,297</td>
      <td>54,658</td>
      <td>72</td>
      <td>-17.6</td>
      <td>-6.2</td>
      <td>73</td>
      <td>Blaine</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3234</th>
      <td>San Diego County</td>
      <td>California</td>
      <td>1861846.0</td>
      <td>2498016.0</td>
      <td>2813833.0</td>
      <td>3095313.0</td>
      <td>3298634</td>
      <td>1748</td>
      <td>1366334</td>
      <td>41.410000</td>
      <td>...</td>
      <td>California</td>
      <td>San Mateo</td>
      <td>141,882</td>
      <td>174,668</td>
      <td>175,070</td>
      <td>1</td>
      <td>23.1</td>
      <td>0.2</td>
      <td>18</td>
      <td>San</td>
    </tr>
    <tr>
      <th>3235</th>
      <td>Maricopa County</td>
      <td>Arizona</td>
      <td>1509052.0</td>
      <td>2122101.0</td>
      <td>3072149.0</td>
      <td>3817117.0</td>
      <td>4420568</td>
      <td>2655</td>
      <td>2088166</td>
      <td>47.209999</td>
      <td>...</td>
      <td>Arizona</td>
      <td>Maricopa</td>
      <td>56,024</td>
      <td>61,008</td>
      <td>63,461</td>
      <td>1</td>
      <td>8.9</td>
      <td>4.0</td>
      <td>6</td>
      <td>Maricopa</td>
    </tr>
    <tr>
      <th>3236</th>
      <td>Harris County</td>
      <td>Texas</td>
      <td>2409547.0</td>
      <td>2818199.0</td>
      <td>3400578.0</td>
      <td>4092459.0</td>
      <td>4731145</td>
      <td>3414</td>
      <td>2777971</td>
      <td>58.739998</td>
      <td>...</td>
      <td>Texas</td>
      <td>Harris</td>
      <td>59,099</td>
      <td>66,140</td>
      <td>69,154</td>
      <td>39</td>
      <td>11.9</td>
      <td>4.6</td>
      <td>51</td>
      <td>Harris</td>
    </tr>
    <tr>
      <th>3237</th>
      <td>Cook County</td>
      <td>Illinois</td>
      <td>5253655.0</td>
      <td>5105067.0</td>
      <td>5376741.0</td>
      <td>5194675.0</td>
      <td>5275541</td>
      <td>3534</td>
      <td>2862646</td>
      <td>54.210003</td>
      <td>...</td>
      <td>Illinois</td>
      <td>Cook</td>
      <td>66,952</td>
      <td>72,979</td>
      <td>72,847</td>
      <td>5</td>
      <td>9.0</td>
      <td>-0.2</td>
      <td>65</td>
      <td>Cook</td>
    </tr>
    <tr>
      <th>3238</th>
      <td>Los Angeles County</td>
      <td>California</td>
      <td>7477503.0</td>
      <td>8863164.0</td>
      <td>9519338.0</td>
      <td>9818605.0</td>
      <td>10014009</td>
      <td>5645</td>
      <td>5111616</td>
      <td>50.970001</td>
      <td>...</td>
      <td>California</td>
      <td>Los Angeles</td>
      <td>67,383</td>
      <td>73,385</td>
      <td>74,142</td>
      <td>16</td>
      <td>8.9</td>
      <td>1.0</td>
      <td>15</td>
      <td>Los</td>
    </tr>
  </tbody>
</table>
<p>3239 rows × 845 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-6173ccee-8e5d-49d5-b2c7-0b0451f685b8')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-6173ccee-8e5d-49d5-b2c7-0b0451f685b8 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-6173ccee-8e5d-49d5-b2c7-0b0451f685b8');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-36505d9b-aaa4-4fb4-bd4b-b6258b530b47">
  <button class="colab-df-quickchart" onclick="quickchart('df-36505d9b-aaa4-4fb4-bd4b-b6258b530b47')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-36505d9b-aaa4-4fb4-bd4b-b6258b530b47 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_eb159722-0b79-4d9b-91fb-1ddb4755c5c6">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('IncomeAndReligionByCounty')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_eb159722-0b79-4d9b-91fb-1ddb4755c5c6 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('IncomeAndReligionByCounty');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
# prompt: Make a graph from IncomeAndReligionByCounty that has 2020 income on the x and total christian adherents on the y (the sum (y-value) is described by the sum of the row's values in  "PRTADH", "CATHADH",  "EVANADH", "ORTHADH", "ACCADH", "OCGADH", and "AMEADH" in the each column's name)


# Assuming IncomeAndReligionByCounty is your DataFrame

# Calculate the total Christian adherents for each row
IncomeAndReligionByCounty['TotalChristianAdherents'] = IncomeAndReligionByCounty['BPRTADH_2020'] + IncomeAndReligionByCounty['CATHADH_2020'] + \
                                                       IncomeAndReligionByCounty['EVANADH_2020'] + IncomeAndReligionByCounty['ORTHADH_2020'] + \
                                                       IncomeAndReligionByCounty['ACCADH_2020'] + IncomeAndReligionByCounty['AMEADH_2020']
```


```python
# prompt: convert the 2020 Income column into an integer column

# Assuming IncomeAndReligionByCounty is your DataFrame

# Convert the '2020 Income' column to numeric, handling non-numeric values
IncomeAndReligionByCounty['2020 Income'] = (IncomeAndReligionByCounty['2020 Income'].str.replace(',', '')
                                              .str.replace('$', '').astype(float))
```


```python
IncomeAndReligionByCounty['ChrstAdherentsPerCapita'] = IncomeAndReligionByCounty['TotalChristianAdherents'] / IncomeAndReligionByCounty['POP2020']
```


```python
merged_df_edu_cleaned = merged_df_edu.dropna(subset=['GDP/Cap for 2010'])
```

# All Dataframes created

After sorting out all of my data that I could find, though I wish I found more and more completed datasets, I found myself thinking, "Theres gotta be some correlations I can find with this."


```python
# prompt: draw a graph x axis being the gdp per capita, y axis being the educational index (disclude educational index for countries with NaN), and the color profile of each point being the sumreligpct


# Create the scatter plot
fig = px.scatter(merged_df_edu_cleaned, x='GDP/Cap for 2010', y='Educational index ',
                 color='chrstgenpct',
                 hover_data=['name'])

fig.update_layout(
    title='GDP per Capita vs. Educational Index (2010)',
    xaxis_title='GDP per Capita',
    yaxis_title='Educational Index'
)

fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
        <script charset="utf-8" src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>                <div id="b9d38fd9-234c-4988-a375-239e86d7b5a7" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("b9d38fd9-234c-4988-a375-239e86d7b5a7")) {                    Plotly.newPlot(                        "b9d38fd9-234c-4988-a375-239e86d7b5a7",                        [{"customdata":[["USA"],["CAN"],["BHM"],["CUB"],["HAI"],["DOM"],["JAM"],["TRI"],["BAR"],["DMA"],["GRN"],["SLU"],["SVG"],["AAB"],["SKN"],["MEX"],["BLZ"],["GUA"],["HON"],["SAL"],["NIC"],["COS"],["PAN"],["COL"],["VEN"],["GUY"],["SUR"],["ECU"],["PER"],["BRA"],["BOL"],["PAR"],["CHL"],["ARG"],["URU"],["UKG"],["IRE"],["NTH"],["BEL"],["LUX"],["FRN"],["MNC"],["LIE"],["SWZ"],["SPN"],["AND"],["POR"],["GMY"],["POL"],["AUS"],["HUN"],["CZR"],["SLO"],["ITA"],["SNM"],["MLT"],["ALB"],["MNG"],["MAC"],["CRO"],["YUG"],["BOS"],["KOS"],["SLV"],["GRC"],["CYP"],["BUL"],["MLD"],["ROM"],["RUS"],["EST"],["LAT"],["LIT"],["UKR"],["BLR"],["ARM"],["GRG"],["AZE"],["FIN"],["SWD"],["NOR"],["DEN"],["ICE"],["CAP"],["STP"],["GNB"],["EQG"],["GAM"],["MLI"],["SEN"],["BEN"],["MAA"],["NIR"],["CDI"],["GUI"],["BFO"],["LBR"],["SIE"],["GHA"],["TOG"],["CAO"],["NIG"],["GAB"],["CEN"],["CHA"],["CON"],["DRC"],["UGA"],["KEN"],["TAZ"],["BUI"],["RWA"],["SOM"],["DJI"],["ETH"],["ERI"],["ANG"],["MZM"],["ZAM"],["ZIM"],["MAW"],["SAF"],["NAM"],["LES"],["BOT"],["SWA"],["MAG"],["COM"],["MAS"],["SEY"],["MOR"],["ALG"],["TUN"],["LIB"],["SUD"],["IRN"],["TUR"],["IRQ"],["EGY"],["SYR"],["LEB"],["JOR"],["ISR"],["SAU"],["YEM"],["KUW"],["BAH"],["QAT"],["UAE"],["OMA"],["AFG"],["TKM"],["TAJ"],["KYR"],["UZB"],["KZK"],["CHN"],["MON"],["TAW"],["PRK"],["ROK"],["JPN"],["IND"],["BHU"],["PAK"],["BNG"],["MYA"],["SRI"],["MAD"],["NEP"],["THI"],["CAM"],["LAO"],["DRV"],["MAL"],["SIN"],["BRU"],["PHI"],["INS"],["ETM"],["AUL"],["PNG"],["NEW"],["VAN"],["SOL"],["KIR"],["TUV"],["FIJ"],["TON"],["NAU"],["MSI"],["PAL"],["FSM"],["WSM"]],"hovertemplate":"GDP\u002fCap for 2010=%{x}\u003cbr\u003eEducational index =%{y}\u003cbr\u003ename=%{customdata[0]}\u003cbr\u003echrstgenpct=%{marker.color}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","marker":{"color":[0.7454,0.7661,0.966,0.6589,0.82,0.87,0.6881,0.5588,0.6434,0.92,0.87,0.9218,0.899,0.914,0.8979,0.9686,0.7365,0.95,0.89,0.861,0.9005,0.8822,0.9793,0.9701,0.95,0.5575,0.48,0.903,0.938,0.8823,0.9426,0.951,0.9128,0.8515,0.8183,0.6263,0.9299,0.5794,0.692,0.9106,0.7019,0.802,0.8678,0.8056,0.8056,0.907,0.8573,0.7078,0.9046,0.73,0.6736,0.2138,0.7548,0.7939,0.8631,0.9727,0.2144,0.7593,0.6374,0.9137,0.9122,0.52,0.0369,0.67,0.9438,0.7453,0.8227,0.8213,0.9751,0.7423,0.2837,0.7902,0.8296,0.852,0.5684,0.951,0.798,0.0241,0.794,0.7606,0.8401,0.8172,0.9155,0.9478,0.9441,0.1088,0.892,0.0435,0.03,0.0349,0.4,0.0026,0.039,0.375,0.08,0.2935,0.85,0.1905,0.7034,0.48,0.4952,0.42,0.7472,0.492,0.34,0.8063,0.9302,0.833,0.8063,0.4777,0.889,0.8945,0.0005,0.0139,0.6156,0.575,0.8912,0.4734,0.87,0.8188,0.7228,0.8094,0.87,0.9418,0.692,0.7843,0.5858,0.0013,0.3252,0.9365,0.01,0.008,0.0035,0.03,0.0715,0.0016,0.0042,0.0189,0.1212,0.0752,0.407,0.03,0.02,0.03,0.0,0.0,0.098,0.1445,0.0714,0.0334,0.0003,0.09,0.0202,0.1007,0.05,0.29,0.058,0.0194,0.0541,0.0166,0.2859,0.0196,0.0234,0.0122,0.017,0.002,0.0776,0.0726,0.0045,0.0142,0.006,0.0037,0.015,0.091,0.0826,0.1821,0.03,0.9174,0.106,0.98,0.6145,0.96,0.5407,0.85,0.9,0.96,0.9699,0.64,0.9421,0.9699,0.9341,0.8606,0.8651,0.9538],"coloraxis":"coloraxis","symbol":"circle"},"mode":"markers","name":"","orientation":"v","showlegend":false,"x":[48650.6643227232,47560.6666009406,0.0,5275.53260105122,0.0,5509.56803417837,4835.79108651148,0.0,0.0,7182.40020254419,0.0,0.0,0.0,0.0,0.0,9823.16407459477,5399.06209583265,0.0,0.0,0.0,1495.72918990272,0.0,8124.55830734871,6392.75802564031,13692.9149666211,4589.87249766592,7999.50739437676,4546.57877452911,5047.2046433225,11249.2918904352,1922.05857050664,0.0,12764.5931178671,10385.9644319555,0.0,0.0,0.0,0.0,44184.946353964,110885.991378721,0.0,0.0,141466.827324144,4035.53448063299,0.0,48237.8911738235,0.0,0.0,12504.2501856093,52147.0241942843,13217.5045951108,0.0,0.0,36035.6449950691,0.0,21798.9142935915,4094.34968570481,2660.28817507398,50676.3870819204,0.0,0.0,0.0,0.0,3017.3073947577,26716.6488260274,31105.02734375,0.0,0.0,0.0,10674.990234375,14663.0446126465,0.0,0.0,3078.41479492188,6034.67885177216,3143.0294799683,0.0,5843.5337683582,46505.3031791811,0.0,88163.2085931423,0.0,0.0,0.0,1043.28142666295,599.859967945903,0.0,0.0,688.327865858558,1286.60496647046,1009.48949478478,0.0,0.0,0.0,0.0,0.0,497.020365397034,0.0,1258.96419689048,0.0,0.0,0.0,8399.59734808121,0.0,0.0,0.0,0.0,824.73767112214,1093.63962367926,0.0,0.0,594.115673355408,223.487606875311,1227.82085311429,335.438495270931,504.972460176652,0.0,0.0,0.0,0.0,0.0,0.0,5445.42006302741,0.0,0.0,0.0,0.0,1384.06328257479,0.0,0.0,0.0,0.0,4241.01190951928,0.0,0.0,6458.57395613765,10622.7020439723,4430.42624189518,2509.77203417522,2748.32269383475,0.0,3914.70123105389,31266.6053174383,17958.9444813361,1249.06308529856,0.0,0.0,73021.3097525035,0.0,0.0,562.499221552971,4286.88050515414,0.0,0.0,1742.34925645077,0.0,4550.47394356715,0.0,0.0,0.0,0.0,44968.1562349739,1350.63447029137,0.0,1011.59718017727,0.0,0.0,0.0,0.0,0.0,0.0,0.0,1127.83482203842,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,1879.24055902232,0.0,0.0,0.0,1528.89975749675,3043.16668029498,0.0,3416.11069898939,0.0,0.0,0.0,2760.0113395546,3494.39522455198],"xaxis":"x","y":[0.891,0.872,null,0.826,null,0.609,0.647,null,null,0.68,null,null,null,null,null,0.64,0.694,null,null,null,0.496,null,0.669,0.647,0.681,0.559,0.574,0.669,0.674,0.614,0.653,null,0.748,0.826,null,null,null,null,0.881,0.813,null,null,0.805,0.473,null,0.693,null,null,0.848,0.901,0.826,null,null,0.778,null,null,0.715,0.736,null,null,null,null,null,0.549,0.818,0.77,null,null,null,0.81,0.903,null,null,0.802,0.808,0.716,null,0.701,0.887,null,0.905,null,null,null,0.458,0.36,null,null,0.266,0.3,0.382,null,null,null,null,null,0.415,null,0.54,null,null,null,0.585,null,null,null,null,0.497,0.49,null,null,0.432,0.235,0.241,0.294,0.355,null,null,null,null,null,null,0.533,null,null,null,null,0.442,null,null,null,null,0.612,null,null,0.698,0.624,0.516,0.557,0.544,null,0.641,0.834,0.667,0.309,null,null,0.634,null,null,0.318,0.644,null,null,0.687,null,0.587,null,null,null,null,0.843,0.461,null,0.321,null,null,null,null,null,null,null,0.445,null,null,null,null,null,null,null,null,0.36,null,null,null,0.593,0.641,null,0.772,null,null,null,0.608,0.721],"yaxis":"y","type":"scatter"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"GDP per Capita"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Educational Index"}},"coloraxis":{"colorbar":{"title":{"text":"chrstgenpct"}},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"legend":{"tracegroupgap":0},"margin":{"t":60},"title":{"text":"GDP per Capita vs. Educational Index (2010)"}},                        {"responsive": true}                    )               };                            </script>        </div>
</body>
</html>



```python

# Create the scatter plot
fig = px.scatter(merged_df_edu_cleaned, x=np.log(merged_df_edu_cleaned['GDP/Cap for 2010'] + 1), y='Educational index ',
                 color='nonreligpct',
                 hover_data=['name'],
                 trendline='ols', trendline_color_override='red')

fig.update_layout(
    title='Log of GDP per Capita vs. Educational Index (2010)',
    xaxis_title='Log of GDP per Capita',
    yaxis_title='Educational Index'
)

fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
        <script charset="utf-8" src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>                <div id="63ba0164-d9b0-4d83-b954-9b00f3a82f89" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("63ba0164-d9b0-4d83-b954-9b00f3a82f89")) {                    Plotly.newPlot(                        "63ba0164-d9b0-4d83-b954-9b00f3a82f89",                        [{"customdata":[["USA"],["CAN"],["BHM"],["CUB"],["HAI"],["DOM"],["JAM"],["TRI"],["BAR"],["DMA"],["GRN"],["SLU"],["SVG"],["AAB"],["SKN"],["MEX"],["BLZ"],["GUA"],["HON"],["SAL"],["NIC"],["COS"],["PAN"],["COL"],["VEN"],["GUY"],["SUR"],["ECU"],["PER"],["BRA"],["BOL"],["PAR"],["CHL"],["ARG"],["URU"],["UKG"],["IRE"],["NTH"],["BEL"],["LUX"],["FRN"],["MNC"],["LIE"],["SWZ"],["SPN"],["AND"],["POR"],["GMY"],["POL"],["AUS"],["HUN"],["CZR"],["SLO"],["ITA"],["SNM"],["MLT"],["ALB"],["MNG"],["MAC"],["CRO"],["YUG"],["BOS"],["KOS"],["SLV"],["GRC"],["CYP"],["BUL"],["MLD"],["ROM"],["RUS"],["EST"],["LAT"],["LIT"],["UKR"],["BLR"],["ARM"],["GRG"],["AZE"],["FIN"],["SWD"],["NOR"],["DEN"],["ICE"],["CAP"],["STP"],["GNB"],["EQG"],["GAM"],["MLI"],["SEN"],["BEN"],["MAA"],["NIR"],["CDI"],["GUI"],["BFO"],["LBR"],["SIE"],["GHA"],["TOG"],["CAO"],["NIG"],["GAB"],["CEN"],["CHA"],["CON"],["DRC"],["UGA"],["KEN"],["TAZ"],["BUI"],["RWA"],["SOM"],["DJI"],["ETH"],["ERI"],["ANG"],["MZM"],["ZAM"],["ZIM"],["MAW"],["SAF"],["NAM"],["LES"],["BOT"],["SWA"],["MAG"],["COM"],["MAS"],["SEY"],["MOR"],["ALG"],["TUN"],["LIB"],["SUD"],["IRN"],["TUR"],["IRQ"],["EGY"],["SYR"],["LEB"],["JOR"],["ISR"],["SAU"],["YEM"],["KUW"],["BAH"],["QAT"],["UAE"],["OMA"],["AFG"],["TKM"],["TAJ"],["KYR"],["UZB"],["KZK"],["CHN"],["MON"],["TAW"],["PRK"],["ROK"],["JPN"],["IND"],["BHU"],["PAK"],["BNG"],["MYA"],["SRI"],["MAD"],["NEP"],["THI"],["CAM"],["LAO"],["DRV"],["MAL"],["SIN"],["BRU"],["PHI"],["INS"],["ETM"],["AUL"],["PNG"],["NEW"],["VAN"],["SOL"],["KIR"],["TUV"],["FIJ"],["TON"],["NAU"],["MSI"],["PAL"],["FSM"],["WSM"]],"hovertemplate":"x=%{x}\u003cbr\u003eEducational index =%{y}\u003cbr\u003ename=%{customdata[0]}\u003cbr\u003enonreligpct=%{marker.color}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","marker":{"color":[0.19,0.1643,0.029,0.1315,0.1,0.12,0.1994,0.1346,0.205,0.06,0.0481,0.059,0.019,0.059,0.0888,0.0272,0.1562,0.0459,0.1,0.111,0.09,0.1,0.0,0.015,0.0439,0.05,0.0,0.085,0.04,0.085,0.04,0.03,0.06,0.12,0.172,0.2616,0.0605,0.34,0.192,0.0496,0.1915,0.129,0.0546,0.1342,0.16,0.0796,0.0691,0.23,0.08,0.1542,0.2716,0.7575,0.1344,0.1868,0.106,0.015,0.1507,0.0451,0.019,0.0565,0.0528,0.0293,0.0059,0.24,0.0261,0.032,0.0473,0.1404,0.0163,0.1404,0.6903,0.2006,0.1521,0.1348,0.411,0.0346,0.0876,0.0193,0.166,0.16,0.1105,0.1011,0.0325,0.0179,0.0124,0.0162,0.0344,0.0052,0.0019,0.0017,0.0334,0.0011,0.001,0.0058,0.0019,0.005,0.01,0.0122,0.06,0.0025,0.0073,0.0031,0.016,0.0124,0.0025,0.0737,0.0051,0.0043,0.0033,0.0089,0.0026,0.0035,0.0004,0.0096,0.0013,0.0128,0.0179,0.0088,0.0018,0.0256,0.0061,0.064,0.0193,0.0028,0.0249,0.0118,0.0061,0.0024,0.0071,0.0097,0.0,0.0,0.0,0.0,0.01,0.0036,0.005,0.011,0.01,0.0146,0.03,0.0,0.045,0.02,0.0,0.0,0.0,0.0177,0.0136,0.0,0.002,0.01,0.025,0.05,0.0179,0.1152,0.325,0.3095,0.07,0.6432,0.4542,0.095,0.0031,0.0003,0.001,0.0008,0.0049,0.0005,0.0,0.0019,0.01,0.0039,0.0111,0.364,0.0018,0.1178,0.0118,0.0093,0.0075,0.0039,0.3101,0.0052,0.3919,0.0331,0.0032,0.01,0.007,0.0105,0.0043,0.0,0.022,0.0153,0.0315,0.0146],"coloraxis":"coloraxis","symbol":"circle"},"mode":"markers","name":"","orientation":"v","showlegend":false,"x":[10.792441297156916,10.76978239226268,0.0,8.571024456629198,0.0,8.614422988335823,8.484006781175223,0.0,0.0,8.879528115759323,0.0,0.0,0.0,0.0,0.0,9.192600351651647,8.594165731714519,0.0,0.0,0.0,7.311037466186321,0.0,9.002769719587798,8.76307748493126,9.524706850126247,8.43182537162787,8.987260242947832,8.422350232843476,8.526787942884786,9.328149353112442,7.561672203006716,0.0,9.454508792980567,9.248306878937314,0.0,0.0,0.0,0.0,10.69616206171446,11.616266865995831,0.0,0.0,11.859827601479275,8.303141801009161,0.0,10.783920845519637,0.0,0.0,9.433903849957591,10.861841572736775,9.489372990147483,0.0,0.0,10.492291616242218,0.0,9.989661317282824,8.317607385975874,7.886565560895402,10.833235075922067,0.0,0.0,0.0,0.0,8.012451487937502,10.193079630741071,10.345156884654784,0.0,0.0,0.0,9.275752595797039,9.593153831839416,0.0,0.0,8.03249485626628,8.705443613000469,8.053260530085385,0.0,8.673262104832178,10.747343134629526,0.0,11.386956361372793,0.0,0.0,0.0,6.9510842978853695,6.398361908960739,0.0,0.0,6.535717015388946,7.160539156570414,6.918190140733011,0.0,0.0,0.0,0.0,0.0,6.210640970560055,0.0,7.138838584375519,0.0,0.0,0.0,9.036058095169816,0.0,0.0,0.0,0.0,6.716277133638263,6.998180477286562,0.0,0.0,6.388755795651335,5.413820502430541,7.113810332557267,5.81841535458076,6.226482241277933,0.0,0.0,0.0,0.0,0.0,0.0,8.602713802654932,0.0,0.0,0.0,0.0,7.233501108967359,0.0,0.0,0.0,0.0,8.35279294264527,0.0,0.0,8.773318643539497,9.270842825763095,8.396476761990561,7.828345568168514,7.919109867174478,0.0,8.2727497063205,10.350337866689182,9.795899250611775,7.130949297261716,0.0,0.0,11.198520286488366,0.0,0.0,6.334165952028958,8.363547835094181,0.0,0.0,7.463563402068518,0.0,8.423206403127715,0.0,0.0,0.0,0.0,10.713732116746254,7.209069857837933,0.0,6.920273774796863,0.0,0.0,0.0,0.0,0.0,0.0,0.0,7.028941248785702,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,7.539155004564972,0.0,0.0,0.0,7.332957494264105,8.02098247447819,0.0,8.136550648134108,0.0,0.0,0.0,7.923352318967936,8.159201731122018],"xaxis":"x","y":[0.891,0.872,null,0.826,null,0.609,0.647,null,null,0.68,null,null,null,null,null,0.64,0.694,null,null,null,0.496,null,0.669,0.647,0.681,0.559,0.574,0.669,0.674,0.614,0.653,null,0.748,0.826,null,null,null,null,0.881,0.813,null,null,0.805,0.473,null,0.693,null,null,0.848,0.901,0.826,null,null,0.778,null,null,0.715,0.736,null,null,null,null,null,0.549,0.818,0.77,null,null,null,0.81,0.903,null,null,0.802,0.808,0.716,null,0.701,0.887,null,0.905,null,null,null,0.458,0.36,null,null,0.266,0.3,0.382,null,null,null,null,null,0.415,null,0.54,null,null,null,0.585,null,null,null,null,0.497,0.49,null,null,0.432,0.235,0.241,0.294,0.355,null,null,null,null,null,null,0.533,null,null,null,null,0.442,null,null,null,null,0.612,null,null,0.698,0.624,0.516,0.557,0.544,null,0.641,0.834,0.667,0.309,null,null,0.634,null,null,0.318,0.644,null,null,0.687,null,0.587,null,null,null,null,0.843,0.461,null,0.321,null,null,null,null,null,null,null,0.445,null,null,null,null,null,null,null,null,0.36,null,null,null,0.593,0.641,null,0.772,null,null,null,0.608,0.721],"yaxis":"y","type":"scatter"},{"hovertemplate":"\u003cb\u003eOLS trendline\u003c\u002fb\u003e\u003cbr\u003eEducational index  = 0.101121 * x + -0.238413\u003cbr\u003eR\u003csup\u003e2\u003c\u002fsup\u003e=0.675879\u003cbr\u003e\u003cbr\u003ex=%{x}\u003cbr\u003eEducational index =%{y} \u003cb\u003e(trend)\u003c\u002fb\u003e\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","line":{"color":"red"},"marker":{"symbol":"circle"},"mode":"lines","name":"","showlegend":false,"x":[5.413820502430541,5.81841535458076,6.210640970560055,6.226482241277933,6.334165952028958,6.388755795651335,6.398361908960739,6.535717015388946,6.716277133638263,6.918190140733011,6.920273774796863,6.9510842978853695,6.998180477286562,7.028941248785702,7.113810332557267,7.130949297261716,7.138838584375519,7.160539156570414,7.209069857837933,7.233501108967359,7.311037466186321,7.332957494264105,7.463563402068518,7.539155004564972,7.561672203006716,7.828345568168514,7.886565560895402,7.919109867174478,7.923352318967936,8.012451487937502,8.02098247447819,8.03249485626628,8.053260530085385,8.136550648134108,8.159201731122018,8.2727497063205,8.303141801009161,8.317607385975874,8.35279294264527,8.363547835094181,8.396476761990561,8.422350232843476,8.423206403127715,8.43182537162787,8.484006781175223,8.526787942884786,8.571024456629198,8.594165731714519,8.602713802654932,8.614422988335823,8.673262104832178,8.705443613000469,8.76307748493126,8.773318643539497,8.879528115759323,8.987260242947832,9.002769719587798,9.036058095169816,9.192600351651647,9.248306878937314,9.270842825763095,9.275752595797039,9.328149353112442,9.433903849957591,9.454508792980567,9.489372990147483,9.524706850126247,9.593153831839416,9.795899250611775,10.193079630741071,10.345156884654784,10.350337866689182,10.492291616242218,10.69616206171446,10.713732116746254,10.747343134629526,10.76978239226268,10.783920845519637,10.792441297156916,10.861841572736775,11.198520286488366,11.386956361372793,11.616266865995831,11.859827601479275],"xaxis":"x","y":[0.30904041440068175,0.34995364709354293,0.3896160842436419,0.3912179770793681,0.4021071139326262,0.4076273200423173,0.4085987044952162,0.4224882569721802,0.44074676444879535,0.4611645077766705,0.4613752079495671,0.4644908138298931,0.4692532494776662,0.4723638244033427,0.4809459122730291,0.4826790298531003,0.4834768062898306,0.485671200398059,0.4905786970287094,0.493049221448691,0.500889813112666,0.5031063989258919,0.5163134624084504,0.5239573975849054,0.5262343701527531,0.5532007771247381,0.559088069306418,0.5623789979194423,0.5628080009492425,0.5718178413202193,0.572680507356586,0.5738446565108376,0.5759445123060113,0.5843669328154004,0.5866574439875138,0.5981395839762201,0.6012128777549531,0.6026756592031999,0.6062336749806926,0.6073212256873083,0.6106510477087155,0.6132674115303299,0.6133539887417739,0.6142255516446266,0.6195022133216261,0.6238283079681403,0.6283015699751273,0.630641650100575,0.6315060437368302,0.6326900939931799,0.6386399928904697,0.6418942348193997,0.6477222575951802,0.6487578587723987,0.6594979184346069,0.6703919512299721,0.6719602925554812,0.6753264625621346,0.6911562481653601,0.6967893749865177,0.69906824341882,0.6995647266607585,0.7048631646240783,0.7155572165002885,0.7176408189585055,0.7211663383855551,0.7247393508140755,0.7316608113197449,0.7521627293534556,0.7923261996173718,0.8077044775257447,0.8082283861282005,0.8225829602317067,0.8431986426371425,0.8449753527117314,0.8483741487873466,0.8506432398648065,0.8520729412684325,0.8529345419997112,0.8599524009978117,0.8939978528498231,0.9130527887653535,0.9362410077570189,0.9608702312696769],"yaxis":"y","type":"scatter"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Log of GDP per Capita"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Educational Index"}},"coloraxis":{"colorbar":{"title":{"text":"nonreligpct"}},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"legend":{"tracegroupgap":0},"margin":{"t":60},"title":{"text":"Log of GDP per Capita vs. Educational Index (2010)"}},                        {"responsive": true}                    )               };                            </script>        </div>
</body>
</html>



```python
# prompt: Find r squared for the graph above

import statsmodels.formula.api as sm

# Assuming 'merged_df_edu_cleaned' is your DataFrame
# Fit a linear regression model
model = sm.ols('Q("Educational index ") ~ np.log(Q("GDP/Cap for 2010")+ 1)', data=merged_df_edu_cleaned).fit()

# Get the R-squared value
r_squared = model.rsquared

print(f"R-squared: {r_squared}")
```

    R-squared: 0.6758790178865637


# Turns out I could find some correlation

With an R^2 value of .675879, this isn't a horrible correlation.

It makes sense when you think about it, more GDP per capita, more education because the government is likely to spend some of that bigger GDP the education systems. Although, it is not always true, so this is not a necessarily a causation.


```python
fig = px.bar(merged_df_edu_cleaned, x="name",
             y=['chrstgenpct','islmgenpct','budgenpct','hindgenpct', 'sikhgenpct', 'judgenpct','confgenpct','othrgenpct'])
fig.update_layout(
    title="Log of Log GDP per Capita vs. Percentage of Population Religious",
    xaxis_title="Log GDP/Cap for 2010",
    yaxis_title="Percent Religious"
)
fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
        <script charset="utf-8" src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>                <div id="72b32cec-54e3-4390-bb4e-1e3c4a6c4771" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("72b32cec-54e3-4390-bb4e-1e3c4a6c4771")) {                    Plotly.newPlot(                        "72b32cec-54e3-4390-bb4e-1e3c4a6c4771",                        [{"alignmentgroup":"True","hovertemplate":"variable=chrstgenpct\u003cbr\u003ename=%{x}\u003cbr\u003evalue=%{y}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"chrstgenpct","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"chrstgenpct","offsetgroup":"chrstgenpct","orientation":"v","showlegend":true,"textposition":"auto","x":["USA","CAN","BHM","CUB","HAI","DOM","JAM","TRI","BAR","DMA","GRN","SLU","SVG","AAB","SKN","MEX","BLZ","GUA","HON","SAL","NIC","COS","PAN","COL","VEN","GUY","SUR","ECU","PER","BRA","BOL","PAR","CHL","ARG","URU","UKG","IRE","NTH","BEL","LUX","FRN","MNC","LIE","SWZ","SPN","AND","POR","GMY","POL","AUS","HUN","CZR","SLO","ITA","SNM","MLT","ALB","MNG","MAC","CRO","YUG","BOS","KOS","SLV","GRC","CYP","BUL","MLD","ROM","RUS","EST","LAT","LIT","UKR","BLR","ARM","GRG","AZE","FIN","SWD","NOR","DEN","ICE","CAP","STP","GNB","EQG","GAM","MLI","SEN","BEN","MAA","NIR","CDI","GUI","BFO","LBR","SIE","GHA","TOG","CAO","NIG","GAB","CEN","CHA","CON","DRC","UGA","KEN","TAZ","BUI","RWA","SOM","DJI","ETH","ERI","ANG","MZM","ZAM","ZIM","MAW","SAF","NAM","LES","BOT","SWA","MAG","COM","MAS","SEY","MOR","ALG","TUN","LIB","SUD","IRN","TUR","IRQ","EGY","SYR","LEB","JOR","ISR","SAU","YEM","KUW","BAH","QAT","UAE","OMA","AFG","TKM","TAJ","KYR","UZB","KZK","CHN","MON","TAW","PRK","ROK","JPN","IND","BHU","PAK","BNG","MYA","SRI","MAD","NEP","THI","CAM","LAO","DRV","MAL","SIN","BRU","PHI","INS","ETM","AUL","PNG","NEW","VAN","SOL","KIR","TUV","FIJ","TON","NAU","MSI","PAL","FSM","WSM"],"xaxis":"x","y":[0.7454,0.7661,0.966,0.6589,0.82,0.87,0.6881,0.5588,0.6434,0.92,0.87,0.9218,0.899,0.914,0.8979,0.9686,0.7365,0.95,0.89,0.861,0.9005,0.8822,0.9793,0.9701,0.95,0.5575,0.48,0.903,0.938,0.8823,0.9426,0.951,0.9128,0.8515,0.8183,0.6263,0.9299,0.5794,0.692,0.9106,0.7019,0.802,0.8678,0.8056,0.8056,0.907,0.8573,0.7078,0.9046,0.73,0.6736,0.2138,0.7548,0.7939,0.8631,0.9727,0.2144,0.7593,0.6374,0.9137,0.9122,0.52,0.0369,0.67,0.9438,0.7453,0.8227,0.8213,0.9751,0.7423,0.2837,0.7902,0.8296,0.852,0.5684,0.951,0.798,0.0241,0.794,0.7606,0.8401,0.8172,0.9155,0.9478,0.9441,0.1088,0.892,0.0435,0.03,0.0349,0.4,0.0026,0.039,0.375,0.08,0.2935,0.85,0.1905,0.7034,0.48,0.4952,0.42,0.7472,0.492,0.34,0.8063,0.9302,0.833,0.8063,0.4777,0.889,0.8945,0.0005,0.0139,0.6156,0.575,0.8912,0.4734,0.87,0.8188,0.7228,0.8094,0.87,0.9418,0.692,0.7843,0.5858,0.0013,0.3252,0.9365,0.01,0.008,0.0035,0.03,0.0715,0.0016,0.0042,0.0189,0.1212,0.0752,0.407,0.03,0.02,0.03,0.0,0.0,0.098,0.1445,0.0714,0.0334,0.0003,0.09,0.0202,0.1007,0.05,0.29,0.058,0.0194,0.0541,0.0166,0.2859,0.0196,0.0234,0.0122,0.017,0.002,0.0776,0.0726,0.0045,0.0142,0.006,0.0037,0.015,0.091,0.0826,0.1821,0.03,0.9174,0.106,0.98,0.6145,0.96,0.5407,0.85,0.9,0.96,0.9699,0.64,0.9421,0.9699,0.9341,0.8606,0.8651,0.9538],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"variable=islmgenpct\u003cbr\u003ename=%{x}\u003cbr\u003evalue=%{y}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"islmgenpct","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"islmgenpct","offsetgroup":"islmgenpct","orientation":"v","showlegend":true,"textposition":"auto","x":["USA","CAN","BHM","CUB","HAI","DOM","JAM","TRI","BAR","DMA","GRN","SLU","SVG","AAB","SKN","MEX","BLZ","GUA","HON","SAL","NIC","COS","PAN","COL","VEN","GUY","SUR","ECU","PER","BRA","BOL","PAR","CHL","ARG","URU","UKG","IRE","NTH","BEL","LUX","FRN","MNC","LIE","SWZ","SPN","AND","POR","GMY","POL","AUS","HUN","CZR","SLO","ITA","SNM","MLT","ALB","MNG","MAC","CRO","YUG","BOS","KOS","SLV","GRC","CYP","BUL","MLD","ROM","RUS","EST","LAT","LIT","UKR","BLR","ARM","GRG","AZE","FIN","SWD","NOR","DEN","ICE","CAP","STP","GNB","EQG","GAM","MLI","SEN","BEN","MAA","NIR","CDI","GUI","BFO","LBR","SIE","GHA","TOG","CAO","NIG","GAB","CEN","CHA","CON","DRC","UGA","KEN","TAZ","BUI","RWA","SOM","DJI","ETH","ERI","ANG","MZM","ZAM","ZIM","MAW","SAF","NAM","LES","BOT","SWA","MAG","COM","MAS","SEY","MOR","ALG","TUN","LIB","SUD","IRN","TUR","IRQ","EGY","SYR","LEB","JOR","ISR","SAU","YEM","KUW","BAH","QAT","UAE","OMA","AFG","TKM","TAJ","KYR","UZB","KZK","CHN","MON","TAW","PRK","ROK","JPN","IND","BHU","PAK","BNG","MYA","SRI","MAD","NEP","THI","CAM","LAO","DRV","MAL","SIN","BRU","PHI","INS","ETM","AUL","PNG","NEW","VAN","SOL","KIR","TUV","FIJ","TON","NAU","MSI","PAL","FSM","WSM"],"xaxis":"x","y":[0.009,0.0194,0.0,0.0007,0.0002,0.0,0.0005,0.0503,0.008,0.0,0.0049,0.001,0.001,0.0,0.0028,0.0,0.0019,0.0001,0.0,0.0003,0.0003,0.0,0.0031,0.0006,0.001,0.075,0.196,0.0001,0.0002,0.0002,0.0001,0.0006,0.0003,0.0151,0.0003,0.0434,0.0058,0.058,0.05,0.02,0.0789,0.008,0.0548,0.0411,0.0304,0.009,0.0085,0.049,0.0001,0.0475,0.0005,0.0001,0.0001,0.0116,0.0002,0.01,0.63,0.1911,0.342,0.0147,0.031,0.45,0.9561,0.03,0.024,0.2027,0.1289,0.036,0.004,0.1157,0.0015,0.0001,0.0008,0.0099,0.002,0.0003,0.099,0.95,0.0045,0.06,0.0204,0.0401,0.005,0.032,0.015,0.3991,0.0394,0.9,0.94,0.9389,0.2647,0.97,0.915,0.375,0.85,0.579,0.1125,0.5532,0.176,0.14,0.214,0.508,0.15,0.15,0.552,0.0193,0.013,0.12,0.1045,0.36,0.025,0.046,0.995,0.975,0.3444,0.4012,0.0104,0.2436,0.0055,0.0107,0.146,0.0169,0.0048,0.0008,0.0274,0.0066,0.0547,0.9806,0.1732,0.0168,0.9891,0.99,0.99,0.9695,0.71,0.99,0.9858,0.95,0.8643,0.902,0.54,0.97,0.1999,0.9382,0.99,0.9195,0.896,0.47,0.6748,0.8987,0.9956,0.89,0.9,0.7702,0.93,0.5932,0.025,0.03,0.0045,0.0,0.0015,0.0015,0.134,0.01,0.9569,0.897,0.0417,0.096,0.98,0.0439,0.1,0.0192,0.01,0.0011,0.61,0.1422,0.8129,0.0555,0.8399,0.007,0.0223,0.0003,0.0112,0.0,0.0032,0.0,0.001,0.06,0.0,0.0,0.0,0.022,0.0,0.0003],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"variable=budgenpct\u003cbr\u003ename=%{x}\u003cbr\u003evalue=%{y}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"budgenpct","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"budgenpct","offsetgroup":"budgenpct","orientation":"v","showlegend":true,"textposition":"auto","x":["USA","CAN","BHM","CUB","HAI","DOM","JAM","TRI","BAR","DMA","GRN","SLU","SVG","AAB","SKN","MEX","BLZ","GUA","HON","SAL","NIC","COS","PAN","COL","VEN","GUY","SUR","ECU","PER","BRA","BOL","PAR","CHL","ARG","URU","UKG","IRE","NTH","BEL","LUX","FRN","MNC","LIE","SWZ","SPN","AND","POR","GMY","POL","AUS","HUN","CZR","SLO","ITA","SNM","MLT","ALB","MNG","MAC","CRO","YUG","BOS","KOS","SLV","GRC","CYP","BUL","MLD","ROM","RUS","EST","LAT","LIT","UKR","BLR","ARM","GRG","AZE","FIN","SWD","NOR","DEN","ICE","CAP","STP","GNB","EQG","GAM","MLI","SEN","BEN","MAA","NIR","CDI","GUI","BFO","LBR","SIE","GHA","TOG","CAO","NIG","GAB","CEN","CHA","CON","DRC","UGA","KEN","TAZ","BUI","RWA","SOM","DJI","ETH","ERI","ANG","MZM","ZAM","ZIM","MAW","SAF","NAM","LES","BOT","SWA","MAG","COM","MAS","SEY","MOR","ALG","TUN","LIB","SUD","IRN","TUR","IRQ","EGY","SYR","LEB","JOR","ISR","SAU","YEM","KUW","BAH","QAT","UAE","OMA","AFG","TKM","TAJ","KYR","UZB","KZK","CHN","MON","TAW","PRK","ROK","JPN","IND","BHU","PAK","BNG","MYA","SRI","MAD","NEP","THI","CAM","LAO","DRV","MAL","SIN","BRU","PHI","INS","ETM","AUL","PNG","NEW","VAN","SOL","KIR","TUV","FIJ","TON","NAU","MSI","PAL","FSM","WSM"],"xaxis":"x","y":[0.0109,0.0194,0.0,0.0,0.0,0.0,0.0001,0.0,0.0004,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0025,0.0,0.0,0.0,0.0,0.0003,0.0038,0.0,0.0004,0.0,0.0,0.0005,0.0003,0.0013,0.0004,0.0023,0.0002,0.0002,0.0,0.004,0.0002,0.0121,0.003,0.0,0.0104,0.0,0.0041,0.0032,0.0002,0.0,0.0056,0.003,0.0,0.0,0.0,0.0,0.0,0.0001,0.0,0.0,0.0,0.0002,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.001,0.0001,0.0,0.001,0.0,0.0,0.0,0.0,0.0009,0.0,0.0028,0.0008,0.0034,0.0,0.0,0.0,0.0,0.0,0.0,0.0001,0.0,0.0,0.0,0.0005,0.0009,0.0,0.0,0.0,0.0,0.0,0.0,0.0001,0.0,0.0,0.0002,0.0,0.0001,0.0001,0.0,0.0002,0.0,0.0,0.0,0.0,0.0,0.0,0.0001,0.0001,0.0003,0.0,0.0,0.0032,0.0,0.0,0.0006,0.0,0.0003,0.0,0.0018,0.0038,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0184,0.0,0.0,0.0,0.0,0.0,0.0,0.0215,0.0035,0.003,0.0001,0.0001,0.0008,0.0,0.0,0.0,0.126,0.53,0.2508,0.0458,0.2255,0.6907,0.0077,0.8402,0.0006,0.006,0.7479,0.7026,0.0042,0.0904,0.87,0.9669,0.6773,0.49,0.192,0.3303,0.07,0.0011,0.008,0.001,0.0247,0.0004,0.021,0.002,0.0033,0.0001,0.0,0.0,0.0012,0.0,0.0,0.0085,0.0059,0.0001],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"variable=hindgenpct\u003cbr\u003ename=%{x}\u003cbr\u003evalue=%{y}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"hindgenpct","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"hindgenpct","offsetgroup":"hindgenpct","orientation":"v","showlegend":true,"textposition":"auto","x":["USA","CAN","BHM","CUB","HAI","DOM","JAM","TRI","BAR","DMA","GRN","SLU","SVG","AAB","SKN","MEX","BLZ","GUA","HON","SAL","NIC","COS","PAN","COL","VEN","GUY","SUR","ECU","PER","BRA","BOL","PAR","CHL","ARG","URU","UKG","IRE","NTH","BEL","LUX","FRN","MNC","LIE","SWZ","SPN","AND","POR","GMY","POL","AUS","HUN","CZR","SLO","ITA","SNM","MLT","ALB","MNG","MAC","CRO","YUG","BOS","KOS","SLV","GRC","CYP","BUL","MLD","ROM","RUS","EST","LAT","LIT","UKR","BLR","ARM","GRG","AZE","FIN","SWD","NOR","DEN","ICE","CAP","STP","GNB","EQG","GAM","MLI","SEN","BEN","MAA","NIR","CDI","GUI","BFO","LBR","SIE","GHA","TOG","CAO","NIG","GAB","CEN","CHA","CON","DRC","UGA","KEN","TAZ","BUI","RWA","SOM","DJI","ETH","ERI","ANG","MZM","ZAM","ZIM","MAW","SAF","NAM","LES","BOT","SWA","MAG","COM","MAS","SEY","MOR","ALG","TUN","LIB","SUD","IRN","TUR","IRQ","EGY","SYR","LEB","JOR","ISR","SAU","YEM","KUW","BAH","QAT","UAE","OMA","AFG","TKM","TAJ","KYR","UZB","KZK","CHN","MON","TAW","PRK","ROK","JPN","IND","BHU","PAK","BNG","MYA","SRI","MAD","NEP","THI","CAM","LAO","DRV","MAL","SIN","BRU","PHI","INS","ETM","AUL","PNG","NEW","VAN","SOL","KIR","TUV","FIJ","TON","NAU","MSI","PAL","FSM","WSM"],"xaxis":"x","y":[0.0057,0.008,0.0,0.0022,0.0,0.0,0.0056,0.184,0.0042,0.0,0.0024,0.003,0.003,0.0,0.0095,0.0,0.002,0.0,0.0,0.0,0.0,0.0001,0.0001,0.0002,0.0,0.295,0.274,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0131,0.0,0.0065,0.0007,0.0,0.0008,0.0,0.0,0.0031,0.0,0.0035,0.0006,0.0012,0.0,0.0,0.0,0.0,0.0,0.0001,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0003,0.0001,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0011,0.0,0.0,0.0,0.0,0.0,0.0005,0.0002,0.0,0.0,0.0,0.0,0.0,0.0001,0.0,0.0,0.0,0.0005,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0014,0.0058,0.0044,0.0075,0.0008,0.0,0.0006,0.0004,0.0001,0.0002,0.0,0.0016,0.005,0.0015,0.0023,0.015,0.0016,0.0006,0.0014,0.0015,0.0006,0.0,0.4859,0.0251,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.01,0.0,0.04,0.0,0.2648,0.2225,0.0262,0.0003,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0002,0.8045,0.1039,0.022,0.09,0.001,0.1246,0.0,0.8134,0.0008,0.0,0.0,0.0006,0.06,0.0505,0.0,0.0,0.015,0.0,0.0084,0.0,0.0199,0.0,0.0,0.0,0.0,0.28,0.001,0.0,0.0,0.0013,0.0,0.0],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"variable=sikhgenpct\u003cbr\u003ename=%{x}\u003cbr\u003evalue=%{y}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"sikhgenpct","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"sikhgenpct","offsetgroup":"sikhgenpct","orientation":"v","showlegend":true,"textposition":"auto","x":["USA","CAN","BHM","CUB","HAI","DOM","JAM","TRI","BAR","DMA","GRN","SLU","SVG","AAB","SKN","MEX","BLZ","GUA","HON","SAL","NIC","COS","PAN","COL","VEN","GUY","SUR","ECU","PER","BRA","BOL","PAR","CHL","ARG","URU","UKG","IRE","NTH","BEL","LUX","FRN","MNC","LIE","SWZ","SPN","AND","POR","GMY","POL","AUS","HUN","CZR","SLO","ITA","SNM","MLT","ALB","MNG","MAC","CRO","YUG","BOS","KOS","SLV","GRC","CYP","BUL","MLD","ROM","RUS","EST","LAT","LIT","UKR","BLR","ARM","GRG","AZE","FIN","SWD","NOR","DEN","ICE","CAP","STP","GNB","EQG","GAM","MLI","SEN","BEN","MAA","NIR","CDI","GUI","BFO","LBR","SIE","GHA","TOG","CAO","NIG","GAB","CEN","CHA","CON","DRC","UGA","KEN","TAZ","BUI","RWA","SOM","DJI","ETH","ERI","ANG","MZM","ZAM","ZIM","MAW","SAF","NAM","LES","BOT","SWA","MAG","COM","MAS","SEY","MOR","ALG","TUN","LIB","SUD","IRN","TUR","IRQ","EGY","SYR","LEB","JOR","ISR","SAU","YEM","KUW","BAH","QAT","UAE","OMA","AFG","TKM","TAJ","KYR","UZB","KZK","CHN","MON","TAW","PRK","ROK","JPN","IND","BHU","PAK","BNG","MYA","SRI","MAD","NEP","THI","CAM","LAO","DRV","MAL","SIN","BRU","PHI","INS","ETM","AUL","PNG","NEW","VAN","SOL","KIR","TUV","FIJ","TON","NAU","MSI","PAL","FSM","WSM"],"xaxis":"x","y":[0.0013,0.008,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0068,0.0,0.0008,0.0003,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0003,0.0,0.0,0.0,0.0,0.0,0.0004,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0002,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0002,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0001,0.0011,0.0003,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0001,0.0002,0.0,0.0,0.0001,0.0,0.0,0.0,0.0022,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0064,0.0001,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0187,0.0,0.0003,0.0001,0.0,0.0,0.0,0.0,0.0003,0.0,0.0,0.0,0.0,0.0034,0.0,0.0,0.0001,0.0,0.0014,0.0,0.0023,0.0,0.0,0.0,0.0,0.0049,0.0,0.0,0.0,0.0,0.0,0.0],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"variable=judgenpct\u003cbr\u003ename=%{x}\u003cbr\u003evalue=%{y}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"judgenpct","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"judgenpct","offsetgroup":"judgenpct","orientation":"v","showlegend":true,"textposition":"auto","x":["USA","CAN","BHM","CUB","HAI","DOM","JAM","TRI","BAR","DMA","GRN","SLU","SVG","AAB","SKN","MEX","BLZ","GUA","HON","SAL","NIC","COS","PAN","COL","VEN","GUY","SUR","ECU","PER","BRA","BOL","PAR","CHL","ARG","URU","UKG","IRE","NTH","BEL","LUX","FRN","MNC","LIE","SWZ","SPN","AND","POR","GMY","POL","AUS","HUN","CZR","SLO","ITA","SNM","MLT","ALB","MNG","MAC","CRO","YUG","BOS","KOS","SLV","GRC","CYP","BUL","MLD","ROM","RUS","EST","LAT","LIT","UKR","BLR","ARM","GRG","AZE","FIN","SWD","NOR","DEN","ICE","CAP","STP","GNB","EQG","GAM","MLI","SEN","BEN","MAA","NIR","CDI","GUI","BFO","LBR","SIE","GHA","TOG","CAO","NIG","GAB","CEN","CHA","CON","DRC","UGA","KEN","TAZ","BUI","RWA","SOM","DJI","ETH","ERI","ANG","MZM","ZAM","ZIM","MAW","SAF","NAM","LES","BOT","SWA","MAG","COM","MAS","SEY","MOR","ALG","TUN","LIB","SUD","IRN","TUR","IRQ","EGY","SYR","LEB","JOR","ISR","SAU","YEM","KUW","BAH","QAT","UAE","OMA","AFG","TKM","TAJ","KYR","UZB","KZK","CHN","MON","TAW","PRK","ROK","JPN","IND","BHU","PAK","BNG","MYA","SRI","MAD","NEP","THI","CAM","LAO","DRV","MAL","SIN","BRU","PHI","INS","ETM","AUL","PNG","NEW","VAN","SOL","KIR","TUV","FIJ","TON","NAU","MSI","PAL","FSM","WSM"],"xaxis":"x","y":[0.019,0.0099,0.001,0.0001,0.0,0.0,0.0002,0.0,0.0001,0.0,0.0,0.0,0.0,0.0,0.0,0.0006,0.0,0.0001,0.0,0.0001,0.0,0.0009,0.0015,0.0002,0.0006,0.0,0.0005,0.0001,0.0001,0.0006,0.0,0.0005,0.0012,0.0068,0.003,0.0042,0.0004,0.0015,0.0028,0.0012,0.0077,0.0151,0.0011,0.0022,0.0003,0.0,0.0003,0.0015,0.0,0.001,0.0011,0.0007,0.0004,0.0006,0.0,0.0001,0.0,0.0,0.0,0.0001,0.0001,0.0003,0.0,0.0001,0.0005,0.0002,0.0003,0.0011,0.0004,0.0014,0.0013,0.0027,0.0018,0.0015,0.0013,0.0002,0.0027,0.0009,0.0002,0.0021,0.0002,0.0004,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0001,0.0,0.0,0.0,0.0,0.0,0.0,0.0001,0.0,0.0,0.0,0.0001,0.0009,0.0,0.0016,0.0011,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0002,0.0,0.0001,0.0,0.0,0.0001,0.0002,0.0,0.0,0.0,0.0,0.0,0.731,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0001,0.0003,0.0001,0.0001,0.0002,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0001,0.0001,0.0,0.0,0.0,0.0045,0.0001,0.0011,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"variable=confgenpct\u003cbr\u003ename=%{x}\u003cbr\u003evalue=%{y}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"confgenpct","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"confgenpct","offsetgroup":"confgenpct","orientation":"v","showlegend":true,"textposition":"auto","x":["USA","CAN","BHM","CUB","HAI","DOM","JAM","TRI","BAR","DMA","GRN","SLU","SVG","AAB","SKN","MEX","BLZ","GUA","HON","SAL","NIC","COS","PAN","COL","VEN","GUY","SUR","ECU","PER","BRA","BOL","PAR","CHL","ARG","URU","UKG","IRE","NTH","BEL","LUX","FRN","MNC","LIE","SWZ","SPN","AND","POR","GMY","POL","AUS","HUN","CZR","SLO","ITA","SNM","MLT","ALB","MNG","MAC","CRO","YUG","BOS","KOS","SLV","GRC","CYP","BUL","MLD","ROM","RUS","EST","LAT","LIT","UKR","BLR","ARM","GRG","AZE","FIN","SWD","NOR","DEN","ICE","CAP","STP","GNB","EQG","GAM","MLI","SEN","BEN","MAA","NIR","CDI","GUI","BFO","LBR","SIE","GHA","TOG","CAO","NIG","GAB","CEN","CHA","CON","DRC","UGA","KEN","TAZ","BUI","RWA","SOM","DJI","ETH","ERI","ANG","MZM","ZAM","ZIM","MAW","SAF","NAM","LES","BOT","SWA","MAG","COM","MAS","SEY","MOR","ALG","TUN","LIB","SUD","IRN","TUR","IRQ","EGY","SYR","LEB","JOR","ISR","SAU","YEM","KUW","BAH","QAT","UAE","OMA","AFG","TKM","TAJ","KYR","UZB","KZK","CHN","MON","TAW","PRK","ROK","JPN","IND","BHU","PAK","BNG","MYA","SRI","MAD","NEP","THI","CAM","LAO","DRV","MAL","SIN","BRU","PHI","INS","ETM","AUL","PNG","NEW","VAN","SOL","KIR","TUV","FIJ","TON","NAU","MSI","PAL","FSM","WSM"],"xaxis":"x","y":[0.0003,0.0001,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0004,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0006,0.13,0.0067,0.0009,0.0,0.0,0.0,0.0,0.0018,0.0,0.0,0.0,0.0011,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0026,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"variable=othrgenpct\u003cbr\u003ename=%{x}\u003cbr\u003evalue=%{y}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"othrgenpct","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"othrgenpct","offsetgroup":"othrgenpct","orientation":"v","showlegend":true,"textposition":"auto","x":["USA","CAN","BHM","CUB","HAI","DOM","JAM","TRI","BAR","DMA","GRN","SLU","SVG","AAB","SKN","MEX","BLZ","GUA","HON","SAL","NIC","COS","PAN","COL","VEN","GUY","SUR","ECU","PER","BRA","BOL","PAR","CHL","ARG","URU","UKG","IRE","NTH","BEL","LUX","FRN","MNC","LIE","SWZ","SPN","AND","POR","GMY","POL","AUS","HUN","CZR","SLO","ITA","SNM","MLT","ALB","MNG","MAC","CRO","YUG","BOS","KOS","SLV","GRC","CYP","BUL","MLD","ROM","RUS","EST","LAT","LIT","UKR","BLR","ARM","GRG","AZE","FIN","SWD","NOR","DEN","ICE","CAP","STP","GNB","EQG","GAM","MLI","SEN","BEN","MAA","NIR","CDI","GUI","BFO","LBR","SIE","GHA","TOG","CAO","NIG","GAB","CEN","CHA","CON","DRC","UGA","KEN","TAZ","BUI","RWA","SOM","DJI","ETH","ERI","ANG","MZM","ZAM","ZIM","MAW","SAF","NAM","LES","BOT","SWA","MAG","COM","MAS","SEY","MOR","ALG","TUN","LIB","SUD","IRN","TUR","IRQ","EGY","SYR","LEB","JOR","ISR","SAU","YEM","KUW","BAH","QAT","UAE","OMA","AFG","TKM","TAJ","KYR","UZB","KZK","CHN","MON","TAW","PRK","ROK","JPN","IND","BHU","PAK","BNG","MYA","SRI","MAD","NEP","THI","CAM","LAO","DRV","MAL","SIN","BRU","PHI","INS","ETM","AUL","PNG","NEW","VAN","SOL","KIR","TUV","FIJ","TON","NAU","MSI","PAL","FSM","WSM"],"xaxis":"x","y":[0.0025,0.001,0.0005,0.0,0.0,0.01,0.106,0.0723,0.1389,0.02,0.0732,0.0152,0.0763,0.027,0.001,0.003,0.1002,0.0036,0.0099,0.0238,0.0092,0.0084,0.0055,0.0041,0.0016,0.0037,0.0,0.0088,0.0193,0.0063,0.0011,0.0102,0.0167,0.0055,0.0052,0.0351,0.0029,0.0008,0.0593,0.0154,0.0035,0.0459,0.0173,0.0099,0.0035,0.0009,0.0583,0.0071,0.0152,0.0673,0.0532,0.0279,0.11,0.0055,0.0216,0.0016,0.0027,0.0043,0.0016,0.015,0.0039,0.0004,0.0011,0.0599,0.0056,0.0198,0.0009,0.0003,0.0042,0.0002,0.018,0.0061,0.0157,0.0009,0.0173,0.0009,0.0077,0.0057,0.0332,0.0173,0.0246,0.0402,0.0378,0.001,0.0023,0.0006,0.0114,0.0022,0.0001,0.0025,0.0177,0.021,0.0041,0.0021,0.0013,0.0003,0.0001,0.0054,0.0076,0.0032,0.0017,0.0018,0.0025,0.0033,0.003,0.0417,0.0002,0.0011,0.0011,0.0048,0.0009,0.0133,0.0025,0.0002,0.0007,0.003,0.0044,0.0044,0.0013,0.0049,0.0004,0.0086,0.0017,0.0034,0.0166,0.0032,0.0002,0.0002,0.0004,0.0011,0.0007,0.002,0.0063,0.0005,0.0085,0.0007,0.0048,0.0201,0.0045,0.0082,0.0046,0.0,0.0042,0.0018,0.01,0.0405,0.006,0.0815,0.0041,0.0323,0.0014,0.0096,0.0532,0.079,0.002,0.0013,0.0027,0.0037,0.0084,0.0038,0.0135,0.0,0.0004,0.0011,0.0007,0.0004,0.0014,0.0037,0.0113,0.0004,0.0037,0.0036,0.0007,0.0003,0.0011,0.0014,0.0024,0.0024,0.0015,0.0015,0.0046,0.0035,0.0004,0.0198,0.0344,0.0099,0.0071,0.0004,0.0159,0.0301,0.0017,0.001,0.0197,0.0258],"yaxis":"y","type":"bar"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Log GDP\u002fCap for 2010"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Percent Religious"}},"legend":{"title":{"text":"variable"},"tracegroupgap":0},"margin":{"t":60},"barmode":"relative","title":{"text":"Log of Log GDP per Capita vs. Percentage of Population Religious"}},                        {"responsive": true}                    )              };                            </script>        </div>
</body>
</html>


This was just a simple way of looking at the religious percentage breakdowns per country. The blank space between the top of each bar and the height of 1 represents the percentage of the population that is not affiliated with any of the general religions.


```python
# prompt: make a graph of education index on the x axis and religious pct on the y with christian pct as the color

# Assuming 'merged_df_edu_cleaned' is your DataFrame with the necessary columns
# and 'Educational index ' is the column containing the educational index values
# and 'chrstgenpct' is the column containing the Christian percentage


# Create the scatter plot
fig = px.scatter(merged_df_edu_cleaned, x='Educational index ', y=np.log(merged_df_edu_cleaned['sumreligpct'] + 1),
                 color='chrstgenpct',
                 hover_data=['name'])

fig.update_layout(
    title='Education Index vs. Total Religious Percentage (2010)',
    xaxis_title='Education Index',
    yaxis_title='Total Religious Percentage',
)

fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
        <script charset="utf-8" src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>                <div id="dfa92f2d-6a16-4bde-9890-d9ae7769067f" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("dfa92f2d-6a16-4bde-9890-d9ae7769067f")) {                    Plotly.newPlot(                        "dfa92f2d-6a16-4bde-9890-d9ae7769067f",                        [{"customdata":[["USA"],["CAN"],["BHM"],["CUB"],["HAI"],["DOM"],["JAM"],["TRI"],["BAR"],["DMA"],["GRN"],["SLU"],["SVG"],["AAB"],["SKN"],["MEX"],["BLZ"],["GUA"],["HON"],["SAL"],["NIC"],["COS"],["PAN"],["COL"],["VEN"],["GUY"],["SUR"],["ECU"],["PER"],["BRA"],["BOL"],["PAR"],["CHL"],["ARG"],["URU"],["UKG"],["IRE"],["NTH"],["BEL"],["LUX"],["FRN"],["MNC"],["LIE"],["SWZ"],["SPN"],["AND"],["POR"],["GMY"],["POL"],["AUS"],["HUN"],["CZR"],["SLO"],["ITA"],["SNM"],["MLT"],["ALB"],["MNG"],["MAC"],["CRO"],["YUG"],["BOS"],["KOS"],["SLV"],["GRC"],["CYP"],["BUL"],["MLD"],["ROM"],["RUS"],["EST"],["LAT"],["LIT"],["UKR"],["BLR"],["ARM"],["GRG"],["AZE"],["FIN"],["SWD"],["NOR"],["DEN"],["ICE"],["CAP"],["STP"],["GNB"],["EQG"],["GAM"],["MLI"],["SEN"],["BEN"],["MAA"],["NIR"],["CDI"],["GUI"],["BFO"],["LBR"],["SIE"],["GHA"],["TOG"],["CAO"],["NIG"],["GAB"],["CEN"],["CHA"],["CON"],["DRC"],["UGA"],["KEN"],["TAZ"],["BUI"],["RWA"],["SOM"],["DJI"],["ETH"],["ERI"],["ANG"],["MZM"],["ZAM"],["ZIM"],["MAW"],["SAF"],["NAM"],["LES"],["BOT"],["SWA"],["MAG"],["COM"],["MAS"],["SEY"],["MOR"],["ALG"],["TUN"],["LIB"],["SUD"],["IRN"],["TUR"],["IRQ"],["EGY"],["SYR"],["LEB"],["JOR"],["ISR"],["SAU"],["YEM"],["KUW"],["BAH"],["QAT"],["UAE"],["OMA"],["AFG"],["TKM"],["TAJ"],["KYR"],["UZB"],["KZK"],["CHN"],["MON"],["TAW"],["PRK"],["ROK"],["JPN"],["IND"],["BHU"],["PAK"],["BNG"],["MYA"],["SRI"],["MAD"],["NEP"],["THI"],["CAM"],["LAO"],["DRV"],["MAL"],["SIN"],["BRU"],["PHI"],["INS"],["ETM"],["AUL"],["PNG"],["NEW"],["VAN"],["SOL"],["KIR"],["TUV"],["FIJ"],["TON"],["NAU"],["MSI"],["PAL"],["FSM"],["WSM"]],"hovertemplate":"Educational index =%{x}\u003cbr\u003ey=%{y}\u003cbr\u003ename=%{customdata[0]}\u003cbr\u003echrstgenpct=%{marker.color}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","marker":{"color":[0.7454,0.7661,0.966,0.6589,0.82,0.87,0.6881,0.5588,0.6434,0.92,0.87,0.9218,0.899,0.914,0.8979,0.9686,0.7365,0.95,0.89,0.861,0.9005,0.8822,0.9793,0.9701,0.95,0.5575,0.48,0.903,0.938,0.8823,0.9426,0.951,0.9128,0.8515,0.8183,0.6263,0.9299,0.5794,0.692,0.9106,0.7019,0.802,0.8678,0.8056,0.8056,0.907,0.8573,0.7078,0.9046,0.73,0.6736,0.2138,0.7548,0.7939,0.8631,0.9727,0.2144,0.7593,0.6374,0.9137,0.9122,0.52,0.0369,0.67,0.9438,0.7453,0.8227,0.8213,0.9751,0.7423,0.2837,0.7902,0.8296,0.852,0.5684,0.951,0.798,0.0241,0.794,0.7606,0.8401,0.8172,0.9155,0.9478,0.9441,0.1088,0.892,0.0435,0.03,0.0349,0.4,0.0026,0.039,0.375,0.08,0.2935,0.85,0.1905,0.7034,0.48,0.4952,0.42,0.7472,0.492,0.34,0.8063,0.9302,0.833,0.8063,0.4777,0.889,0.8945,0.0005,0.0139,0.6156,0.575,0.8912,0.4734,0.87,0.8188,0.7228,0.8094,0.87,0.9418,0.692,0.7843,0.5858,0.0013,0.3252,0.9365,0.01,0.008,0.0035,0.03,0.0715,0.0016,0.0042,0.0189,0.1212,0.0752,0.407,0.03,0.02,0.03,0.0,0.0,0.098,0.1445,0.0714,0.0334,0.0003,0.09,0.0202,0.1007,0.05,0.29,0.058,0.0194,0.0541,0.0166,0.2859,0.0196,0.0234,0.0122,0.017,0.002,0.0776,0.0726,0.0045,0.0142,0.006,0.0037,0.015,0.091,0.0826,0.1821,0.03,0.9174,0.106,0.98,0.6145,0.96,0.5407,0.85,0.9,0.96,0.9699,0.64,0.9421,0.9699,0.9341,0.8606,0.8651,0.9538],"coloraxis":"coloraxis","symbol":"circle"},"mode":"markers","name":"","orientation":"v","showlegend":false,"x":[0.891,0.872,null,0.826,null,0.609,0.647,null,null,0.68,null,null,null,null,null,0.64,0.694,null,null,null,0.496,null,0.669,0.647,0.681,0.559,0.574,0.669,0.674,0.614,0.653,null,0.748,0.826,null,null,null,null,0.881,0.813,null,null,0.805,0.473,null,0.693,null,null,0.848,0.901,0.826,null,null,0.778,null,null,0.715,0.736,null,null,null,null,null,0.549,0.818,0.77,null,null,null,0.81,0.903,null,null,0.802,0.808,0.716,null,0.701,0.887,null,0.905,null,null,null,0.458,0.36,null,null,0.266,0.3,0.382,null,null,null,null,null,0.415,null,0.54,null,null,null,0.585,null,null,null,null,0.497,0.49,null,null,0.432,0.235,0.241,0.294,0.355,null,null,null,null,null,null,0.533,null,null,null,null,0.442,null,null,null,null,0.612,null,null,0.698,0.624,0.516,0.557,0.544,null,0.641,0.834,0.667,0.309,null,null,0.634,null,null,0.318,0.644,null,null,0.687,null,0.587,null,null,null,null,0.843,0.461,null,0.321,null,null,null,null,null,null,null,0.445,null,null,null,null,null,null,null,null,0.36,null,null,null,0.593,0.641,null,0.772,null,null,null,0.608,0.721],"xaxis":"x","y":[0.6918963986582927,0.6926470555182631,0.692897149304736,0.5079615261513406,0.5989463851611182,0.688134638736401,0.6386909947638866,0.6563275824214087,0.6211677107677809,0.6830968447064438,0.6558605957739287,0.6855181533954542,0.6542504149299987,0.6795552270404782,0.6926470555182631,0.6916460544336781,0.641748617473945,0.6913455586133171,0.6881848887301304,0.6811758087787253,0.6885365680022622,0.6889383357858906,0.6903933923633242,0.6910950764338145,0.6923468603891761,0.691295467196471,0.6931471805599453,0.6887374720712452,0.6834503175810814,0.6899922088666441,0.6925970292544641,0.6880341311731223,0.684762124025505,0.6903933923633242,0.6905437946898305,0.6754413534410131,0.6916961282926306,0.6927471005386057,0.6630487327359125,0.685417382498004,0.691395647521139,0.6699297293837607,0.6844595521623797,0.6881848887301304,0.691395647521139,0.69269707927956,0.663563878018271,0.6895908643571682,0.6855181533954542,0.658917989009285,0.6661869989771623,0.6790989648338862,0.6365768290715511,0.6903933923633242,0.6822884372250695,0.6923468603891761,0.6917962684889891,0.6909948659918026,0.6923468603891761,0.6856189141391537,0.6911952768347,0.6929471605572782,0.6925970292544641,0.6627395181385198,0.690343253227211,0.6831978497062772,0.69269707927956,0.6929971693088202,0.6910449724680751,0.6930471755596119,0.6841064359077962,0.6900925198307166,0.6852662071090694,0.69269707927956,0.6844595521623797,0.69269707927956,0.6892897502326406,0.6902931115770389,0.6764078565556473,0.6844595521623797,0.6807709094918899,0.672842427219581,0.6740662927471535,0.6926470555182631,0.6919965188025493,0.6928471355509433,0.6874308735638361,0.6920465751159123,0.6930971793099037,0.6918963986582927,0.6842577867140281,0.6825916666204287,0.6910950764338145,0.6920966289237662,0.6924969692183589,0.6929971693088202,0.6930971793099037,0.6904435289856306,0.6893399422169912,0.6915458991929714,0.6922968191051063,0.6922467753167811,0.6918963986582927,0.6914958178107149,0.6916460544336781,0.6720767499406536,0.6930471755596119,0.6925970292544641,0.6925970292544641,0.690744295943635,0.69269707927956,0.6864749707918807,0.6918963986582927,0.6930471755596119,0.6927971192956498,0.6916460544336781,0.6909447570047452,0.6909447570047452,0.6924969692183589,0.6906941743988784,0.6929471605572782,0.6888379089718469,0.6922968191051063,0.6914457339201877,0.6848125437698876,0.6915458991929714,0.6930471755596119,0.6930471755596119,0.6929471605572782,0.6925970292544641,0.6927971192956498,0.6921466802263617,0.6899922088666441,0.692897149304736,0.6888881236395619,0.6927971192956498,0.690744295943635,0.6830463383805158,0.6908946455066516,0.6890387525154021,0.6908445314972698,0.6931471805599453,0.6910449724680751,0.6922467753167811,0.688134638736401,0.6726893386575491,0.6901426715396466,0.65154363070487,0.6910950764338145,0.6768653479856624,0.692446935445552,0.6883356235627233,0.6661869989771623,0.6528458837864196,0.6921466802263617,0.6924969692183589,0.6917962684889891,0.691295467196471,0.6889383357858906,0.691245373270349,0.6863742962725166,0.5381878405218021,0.6929471605572782,0.6925970292544641,0.6927971192956498,0.6929471605572782,0.692446935445552,0.691295467196471,0.6874811589333186,0.6929471605572782,0.691295467196471,0.6913455586133171,0.6927971192956498,0.6929971693088202,0.6925970292544641,0.692446935445552,0.6919464599834264,0.6919464599834264,0.6923968991692412,0.6923968991692412,0.6908445314972698,0.691395647521139,0.6929471605572782,0.6831978497062772,0.6757975422248323,0.6881848887301304,0.6895908643571682,0.6929471605572782,0.6851654108182876,0.6779827800401728,0.6922968191051063,0.6926470555182631,0.6832483483806977,0.6801632530016505],"yaxis":"y","type":"scatter"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Education Index"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Total Religious Percentage"}},"coloraxis":{"colorbar":{"title":{"text":"chrstgenpct"}},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"legend":{"tracegroupgap":0},"margin":{"t":60},"title":{"text":"Education Index vs. Total Religious Percentage (2010)"}},                        {"responsive": true}                    )               };                            </script>        </div>
</body>
</html>



```python
merged_df_edu_cleaned['Mean years schooling'] = merged_df_edu_cleaned['Mean years schooling'].astype(float)
fig = px.scatter_3d(merged_df_edu_cleaned, x=np.log(merged_df_edu_cleaned['GDP/Cap for 2010'] + 1), y=(merged_df_edu_cleaned['Educational index ']), z=np.log(merged_df_edu_cleaned['sumreligpct']),
              color='chrstgenpct',
              hover_data=['name'],
             )
fig.update_layout(
    title='Log of GDP per Capita vs. Educational Index (2010)',
    scene = dict(
      xaxis_title='Log GDP per Capita',
      yaxis_title='Educational Index',
      zaxis_title='Log Total Religious Percentage'
    )
)
#fig.update_layout(margin=dict(l=0, r=0, b=0, t=0))
fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
        <script charset="utf-8" src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>                <div id="fa279868-336a-4873-b557-f3aa26eb2a7d" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("fa279868-336a-4873-b557-f3aa26eb2a7d")) {                    Plotly.newPlot(                        "fa279868-336a-4873-b557-f3aa26eb2a7d",                        [{"customdata":[["USA"],["CAN"],["BHM"],["CUB"],["HAI"],["DOM"],["JAM"],["TRI"],["BAR"],["DMA"],["GRN"],["SLU"],["SVG"],["AAB"],["SKN"],["MEX"],["BLZ"],["GUA"],["HON"],["SAL"],["NIC"],["COS"],["PAN"],["COL"],["VEN"],["GUY"],["SUR"],["ECU"],["PER"],["BRA"],["BOL"],["PAR"],["CHL"],["ARG"],["URU"],["UKG"],["IRE"],["NTH"],["BEL"],["LUX"],["FRN"],["MNC"],["LIE"],["SWZ"],["SPN"],["AND"],["POR"],["GMY"],["POL"],["AUS"],["HUN"],["CZR"],["SLO"],["ITA"],["SNM"],["MLT"],["ALB"],["MNG"],["MAC"],["CRO"],["YUG"],["BOS"],["KOS"],["SLV"],["GRC"],["CYP"],["BUL"],["MLD"],["ROM"],["RUS"],["EST"],["LAT"],["LIT"],["UKR"],["BLR"],["ARM"],["GRG"],["AZE"],["FIN"],["SWD"],["NOR"],["DEN"],["ICE"],["CAP"],["STP"],["GNB"],["EQG"],["GAM"],["MLI"],["SEN"],["BEN"],["MAA"],["NIR"],["CDI"],["GUI"],["BFO"],["LBR"],["SIE"],["GHA"],["TOG"],["CAO"],["NIG"],["GAB"],["CEN"],["CHA"],["CON"],["DRC"],["UGA"],["KEN"],["TAZ"],["BUI"],["RWA"],["SOM"],["DJI"],["ETH"],["ERI"],["ANG"],["MZM"],["ZAM"],["ZIM"],["MAW"],["SAF"],["NAM"],["LES"],["BOT"],["SWA"],["MAG"],["COM"],["MAS"],["SEY"],["MOR"],["ALG"],["TUN"],["LIB"],["SUD"],["IRN"],["TUR"],["IRQ"],["EGY"],["SYR"],["LEB"],["JOR"],["ISR"],["SAU"],["YEM"],["KUW"],["BAH"],["QAT"],["UAE"],["OMA"],["AFG"],["TKM"],["TAJ"],["KYR"],["UZB"],["KZK"],["CHN"],["MON"],["TAW"],["PRK"],["ROK"],["JPN"],["IND"],["BHU"],["PAK"],["BNG"],["MYA"],["SRI"],["MAD"],["NEP"],["THI"],["CAM"],["LAO"],["DRV"],["MAL"],["SIN"],["BRU"],["PHI"],["INS"],["ETM"],["AUL"],["PNG"],["NEW"],["VAN"],["SOL"],["KIR"],["TUV"],["FIJ"],["TON"],["NAU"],["MSI"],["PAL"],["FSM"],["WSM"]],"hovertemplate":"x=%{x}\u003cbr\u003eEducational index =%{y}\u003cbr\u003ez=%{z}\u003cbr\u003ename=%{customdata[0]}\u003cbr\u003echrstgenpct=%{marker.color}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","marker":{"color":[0.7454,0.7661,0.966,0.6589,0.82,0.87,0.6881,0.5588,0.6434,0.92,0.87,0.9218,0.899,0.914,0.8979,0.9686,0.7365,0.95,0.89,0.861,0.9005,0.8822,0.9793,0.9701,0.95,0.5575,0.48,0.903,0.938,0.8823,0.9426,0.951,0.9128,0.8515,0.8183,0.6263,0.9299,0.5794,0.692,0.9106,0.7019,0.802,0.8678,0.8056,0.8056,0.907,0.8573,0.7078,0.9046,0.73,0.6736,0.2138,0.7548,0.7939,0.8631,0.9727,0.2144,0.7593,0.6374,0.9137,0.9122,0.52,0.0369,0.67,0.9438,0.7453,0.8227,0.8213,0.9751,0.7423,0.2837,0.7902,0.8296,0.852,0.5684,0.951,0.798,0.0241,0.794,0.7606,0.8401,0.8172,0.9155,0.9478,0.9441,0.1088,0.892,0.0435,0.03,0.0349,0.4,0.0026,0.039,0.375,0.08,0.2935,0.85,0.1905,0.7034,0.48,0.4952,0.42,0.7472,0.492,0.34,0.8063,0.9302,0.833,0.8063,0.4777,0.889,0.8945,0.0005,0.0139,0.6156,0.575,0.8912,0.4734,0.87,0.8188,0.7228,0.8094,0.87,0.9418,0.692,0.7843,0.5858,0.0013,0.3252,0.9365,0.01,0.008,0.0035,0.03,0.0715,0.0016,0.0042,0.0189,0.1212,0.0752,0.407,0.03,0.02,0.03,0.0,0.0,0.098,0.1445,0.0714,0.0334,0.0003,0.09,0.0202,0.1007,0.05,0.29,0.058,0.0194,0.0541,0.0166,0.2859,0.0196,0.0234,0.0122,0.017,0.002,0.0776,0.0726,0.0045,0.0142,0.006,0.0037,0.015,0.091,0.0826,0.1821,0.03,0.9174,0.106,0.98,0.6145,0.96,0.5407,0.85,0.9,0.96,0.9699,0.64,0.9421,0.9699,0.9341,0.8606,0.8651,0.9538],"coloraxis":"coloraxis","symbol":"circle"},"mode":"markers","name":"","scene":"scene","showlegend":false,"x":[10.792441297156916,10.76978239226268,0.0,8.571024456629198,0.0,8.614422988335823,8.484006781175223,0.0,0.0,8.879528115759323,0.0,0.0,0.0,0.0,0.0,9.192600351651647,8.594165731714519,0.0,0.0,0.0,7.311037466186321,0.0,9.002769719587798,8.76307748493126,9.524706850126247,8.43182537162787,8.987260242947832,8.422350232843476,8.526787942884786,9.328149353112442,7.561672203006716,0.0,9.454508792980567,9.248306878937314,0.0,0.0,0.0,0.0,10.69616206171446,11.616266865995831,0.0,0.0,11.859827601479275,8.303141801009161,0.0,10.783920845519637,0.0,0.0,9.433903849957591,10.861841572736775,9.489372990147483,0.0,0.0,10.492291616242218,0.0,9.989661317282824,8.317607385975874,7.886565560895402,10.833235075922067,0.0,0.0,0.0,0.0,8.012451487937502,10.193079630741071,10.345156884654784,0.0,0.0,0.0,9.275752595797039,9.593153831839416,0.0,0.0,8.03249485626628,8.705443613000469,8.053260530085385,0.0,8.673262104832178,10.747343134629526,0.0,11.386956361372793,0.0,0.0,0.0,6.9510842978853695,6.398361908960739,0.0,0.0,6.535717015388946,7.160539156570414,6.918190140733011,0.0,0.0,0.0,0.0,0.0,6.210640970560055,0.0,7.138838584375519,0.0,0.0,0.0,9.036058095169816,0.0,0.0,0.0,0.0,6.716277133638263,6.998180477286562,0.0,0.0,6.388755795651335,5.413820502430541,7.113810332557267,5.81841535458076,6.226482241277933,0.0,0.0,0.0,0.0,0.0,0.0,8.602713802654932,0.0,0.0,0.0,0.0,7.233501108967359,0.0,0.0,0.0,0.0,8.35279294264527,0.0,0.0,8.773318643539497,9.270842825763095,8.396476761990561,7.828345568168514,7.919109867174478,0.0,8.2727497063205,10.350337866689182,9.795899250611775,7.130949297261716,0.0,0.0,11.198520286488366,0.0,0.0,6.334165952028958,8.363547835094181,0.0,0.0,7.463563402068518,0.0,8.423206403127715,0.0,0.0,0.0,0.0,10.713732116746254,7.209069857837933,0.0,6.920273774796863,0.0,0.0,0.0,0.0,0.0,0.0,0.0,7.028941248785702,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,7.539155004564972,0.0,0.0,0.0,7.332957494264105,8.02098247447819,0.0,8.136550648134108,0.0,0.0,0.0,7.923352318967936,8.159201731122018],"y":[0.891,0.872,null,0.826,null,0.609,0.647,null,null,0.68,null,null,null,null,null,0.64,0.694,null,null,null,0.496,null,0.669,0.647,0.681,0.559,0.574,0.669,0.674,0.614,0.653,null,0.748,0.826,null,null,null,null,0.881,0.813,null,null,0.805,0.473,null,0.693,null,null,0.848,0.901,0.826,null,null,0.778,null,null,0.715,0.736,null,null,null,null,null,0.549,0.818,0.77,null,null,null,0.81,0.903,null,null,0.802,0.808,0.716,null,0.701,0.887,null,0.905,null,null,null,0.458,0.36,null,null,0.266,0.3,0.382,null,null,null,null,null,0.415,null,0.54,null,null,null,0.585,null,null,null,null,0.497,0.49,null,null,0.432,0.235,0.241,0.294,0.355,null,null,null,null,null,null,0.533,null,null,null,null,0.442,null,null,null,null,0.612,null,null,0.698,0.624,0.516,0.557,0.544,null,0.641,0.834,0.667,0.309,null,null,0.634,null,null,0.318,0.644,null,null,0.687,null,0.587,null,null,null,null,0.843,0.461,null,0.321,null,null,null,null,null,null,null,0.445,null,null,null,null,null,null,null,null,0.36,null,null,null,0.593,0.641,null,0.772,null,null,null,0.608,0.721],"z":[-0.002503130218118477,-0.0010005003335835344,-0.0005001250416822429,-0.4126407918572599,-0.19820706602417826,-0.01005033585350145,-0.11204950380862289,-0.07504687432291127,-0.14954463728001757,-0.020202707317519466,-0.07601748642391595,-0.015316704111893288,-0.0793679353835727,-0.027371196796132015,-0.0010005003335835344,-0.0030045090202987243,-0.10558276257506509,-0.003606495594111744,-0.009949330853668103,-0.024087795529089982,-0.009242581366932545,-0.008435478821101575,-0.005515180688110111,-0.004108428044543191,-0.0016012813669738792,-0.003706861931326512,0.0,-0.008838948667204392,-0.019488676583862413,-0.0063199287448193475,-0.0011006054440330039,-0.010252376464351353,-0.016841017196026556,-0.005515180688110111,-0.005213567052887434,-0.03573080995579895,-0.002904213147389827,-0.0008003201707691552,-0.06113100000423132,-0.015519811658036807,-0.00350613932928759,-0.04698679122433687,-0.017451393613755858,-0.009949330853668103,-0.00350613932928759,-0.0009004052431641551,-0.060068526466119515,-0.007125324942588627,-0.015316704111893288,-0.06967167324931926,-0.05466740134230821,-0.02829659915511379,-0.11653381625595151,-0.005515180688110111,-0.021836694609174406,-0.0016012813669738792,-0.002703651574314823,-0.004309271588098403,-0.0016012813669738792,-0.015113637810048184,-0.0039076248310170765,-0.00040008002133969133,-0.0011006054440330039,-0.06176902639763181,-0.005615738785635745,-0.01999864650668997,-0.0009004052431641551,-0.00030004500900199243,-0.004208844774054682,-0.0002000200026670447,-0.01816397062767118,-0.006118681008177177,-0.01582455034697146,-0.0009004052431641551,-0.017451393613755858,-0.0009004052431641551,-0.0077297980619412685,-0.005716306996109192,-0.033763630152809115,-0.017451393613755858,-0.02490763570618478,-0.04103034955799192,-0.038532949716783664,-0.0010005003335835344,-0.002302649062675558,-0.0006001800720324606,-0.011465478109278096,-0.0022024235552000394,-0.00010000500033334732,-0.002503130218118477,-0.017858518301313193,-0.021223636451626688,-0.004108428044543191,-0.0021022080918701985,-0.0013008457330480696,-0.00030004500900199243,-0.00010000500033334732,-0.005414632701498842,-0.007629027164491163,-0.0032051309489483358,-0.0017014466397575704,-0.0018016219466282088,-0.002503130218118477,-0.0033054570087264813,-0.0030045090202987243,-0.0425943976324205,-0.0002000200026670447,-0.0011006054440330039,-0.0011006054440330039,-0.004811556997222082,-0.0009004052431641551,-0.013389237119016052,-0.002503130218118477,-0.0002000200026670447,-0.0007002451143934259,-0.0030045090202987243,-0.004409708488700073,-0.004409708488700073,-0.0013008457330480696,-0.004912044361020641,-0.00040008002133969133,-0.008637193395663588,-0.0017014466397575704,-0.003405793134832821,-0.016739324004297996,-0.0032051309489483358,-0.0002000200026670447,-0.0002000200026670447,-0.00040008002133969133,-0.0011006054440330039,-0.0007002451143934259,-0.0020020026706730793,-0.0063199287448193475,-0.0005001250416822429,-0.008536331022286335,-0.0007002451143934259,-0.004811556997222082,-0.020304753340364273,-0.004510155477886019,-0.008233804927103542,-0.004610612557683294,0.0,-0.004208844774054682,-0.0018016219466282088,-0.01005033585350145,-0.04134296353438243,-0.006018072325563021,-0.08501337432695673,-0.004108428044543191,-0.03283315709524021,-0.0014009809156281003,-0.00964637705180545,-0.05466740134230821,-0.08229524272683016,-0.0020020026706730793,-0.0013008457330480696,-0.002703651574314823,-0.003706861931326512,-0.008435478821101575,-0.0038072383429540663,-0.013591953519466972,-0.3384141208585543,-0.00040008002133969133,-0.0011006054440330039,-0.0007002451143934259,-0.00040008002133969133,-0.0014009809156281003,-0.003706861931326512,-0.011364330079049759,-0.00040008002133969133,-0.003706861931326512,-0.003606495594111744,-0.0007002451143934259,-0.00030004500900199243,-0.0011006054440330039,-0.0014009809156281003,-0.002402884616310315,-0.002402884616310315,-0.0015011261262670914,-0.0015011261262670914,-0.004610612557683294,-0.00350613932928759,-0.00040008002133969133,-0.01999864650668997,-0.03500560919881529,-0.009949330853668103,-0.007125324942588627,-0.00040008002133969133,-0.01602776107719725,-0.03056230558263998,-0.0017014466397575704,-0.0010005003335835344,-0.019896631714456645,-0.02613865760969481],"type":"scatter3d"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"scene":{"domain":{"x":[0.0,1.0],"y":[0.0,1.0]},"xaxis":{"title":{"text":"Log GDP per Capita"}},"yaxis":{"title":{"text":"Educational Index"}},"zaxis":{"title":{"text":"Log Total Religious Percentage"}}},"coloraxis":{"colorbar":{"title":{"text":"chrstgenpct"}},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"legend":{"tracegroupgap":0},"margin":{"t":60},"title":{"text":"Log of GDP per Capita vs. Educational Index (2010)"}},                        {"responsive": true}                    )           };                            </script>        </div>
</body>
</html>


Similar to the graph just before, but taking the log of the GDP per cap. and adding it to the mix. Not much correlation between any of these. Although an interesting side-note is that there is very interesting dip in the religious afilliation when you increase the educational index. Nothing really mathematically showing though.


```python
# Create the scatter plot
fig = px.scatter(IncomeAndReligionByCounty, x = '2020 Income', y='TotalChristianAdherents', hover_data=['COUNAM', 'STATNAM'], trendline='ols', trendline_color_override='red')


fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
        <script charset="utf-8" src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>                <div id="0c8dfe05-7c1c-485e-9ea0-79f4676725f6" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("0c8dfe05-7c1c-485e-9ea0-79f4676725f6")) {                    Plotly.newPlot(                        "0c8dfe05-7c1c-485e-9ea0-79f4676725f6",                        [{"customdata":[["Loving County","Texas"],["King County","Texas"],["Kenedy County","Texas"],["McPherson County","Nebraska"],["Blaine County","Nebraska"],["Arthur County","Nebraska"],["Petroleum County","Montana"],["McMullen County","Texas"],["Loup County","Nebraska"],["Grant County","Nebraska"],["Borden County","Texas"],["Harding County","New Mexico"],["Thomas County","Nebraska"],["Banner County","Nebraska"],["San Juan County","Colorado"],["San Juan County","Colorado"],["Slope County","North Dakota"],["Hooker County","Nebraska"],["Logan County","Nebraska"],["Esmeralda County","Nevada"],["Kent County","Texas"],["Terrell County","Texas"],["Treasure County","Montana"],["Keya Paha County","Nebraska"],["Wheeler County","Nebraska"],["Hinsdale County","Colorado"],["Clark County","Idaho"],["Golden Valley County","Montana"],["Roberts County","Texas"],["Hayes County","Nebraska"],["Mineral County","Colorado"],["Jones County","South Dakota"],["Daggett County","Utah"],["Wibaux County","Montana"],["Billings County","North Dakota"],["Motley County","Texas"],["Camas County","Idaho"],["Prairie County","Montana"],["Foard County","Texas"],["Glasscock County","Texas"],["Sioux County","Nebraska"],["Garfield County","Montana"],["Alpine County","California"],["Stonewall County","Texas"],["Rock County","Nebraska"],["Hyde County","South Dakota"],["Sheridan County","North Dakota"],["Greeley County","Kansas"],["Harding County","South Dakota"],["Issaquena County","Mississippi"],["Sterling County","Texas"],["Campbell County","South Dakota"],["Jackson County","Colorado"],["Cottle County","Texas"],["Carter County","Montana"],["Edwards County","Texas"],["Briscoe County","Texas"],["Piute County","Utah"],["Throckmorton County","Texas"],["Kiowa County","Colorado"],["Sully County","South Dakota"],["Wheeler County","Oregon"],["Wallace County","Kansas"],["Irion County","Texas"],["Taliaferro County","Georgia"],["Lane County","Kansas"],["Dundy County","Nebraska"],["Daniels County","Montana"],["Jerauld County","South Dakota"],["Comanche County","Kansas"],["Powder River County","Montana"],["De Baca County","New Mexico"],["Hodgeman County","Kansas"],["McCone County","Montana"],["Golden Valley County","North Dakota"],["Cheyenne County","Colorado"],["Oldham County","Texas"],["Dickens County","Texas"],["Steele County","North Dakota"],["Boyd County","Nebraska"],["Garfield County","Nebraska"],["Deuel County","Nebraska"],["Armstrong County","Texas"],["Eureka County","Nevada"],["Sherman County","Oregon"],["Haakon County","South Dakota"],["Garden County","Nebraska"],["Logan County","North Dakota"],["Oliver County","North Dakota"],["Gosper County","Nebraska"],["Mellette County","South Dakota"],["Meagher County","Montana"],["Buffalo County","South Dakota"],["Liberty County","Montana"],["Menard County","Texas"],["Worth County","Missouri"],["Clark County","Kansas"],["Gilliam County","Oregon"],["Jeff Davis County","Texas"],["Judith Basin County","Montana"],["Keweenaw County","Michigan"],["Wheatland County","Montana"],["Stanton County","Kansas"],["Faulk County","South Dakota"],["Wichita County","Kansas"],["Towner County","North Dakota"],["Greeley County","Nebraska"],["Culberson County","Texas"],["Robertson County","Kentucky"],["Divide County","North Dakota"],["Adams County","North Dakota"],["Burke County","North Dakota"],["Highland County","Virginia"],["Quitman County","Georgia"],["Renville County","North Dakota"],["Garfield County","Washington"],["Cimarron County","Oklahoma"],["Miner County","South Dakota"],["Grant County","North Dakota"],["Griggs County","North Dakota"],["Dolores County","Colorado"],["Sanborn County","South Dakota"],["Eddy County","North Dakota"],["Webster County","Georgia"],["Kidder County","North Dakota"],["Sedgwick County","Colorado"],["McPherson County","South Dakota"],["Ziebach County","South Dakota"],["Graham County","Kansas"],["Sheridan County","Kansas"],["Schleicher County","Texas"],["Kiowa County","Kansas"],["Niobrara County","Wyoming"],["Potter County","South Dakota"],["Elk County","Kansas"],["Wayne County","Utah"],["Harmon County","Oklahoma"],["Hettinger County","North Dakota"],["Rich County","Utah"],["Hamilton County","Kansas"],["Frontier County","Nebraska"],["McIntosh County","North Dakota"],["Pawnee County","Nebraska"],["Cochran County","Texas"],["Rawlins County","Kansas"],["Chase County","Kansas"],["Butte County","Idaho"],["Cheyenne County","Kansas"],["Hitchcock County","Nebraska"],["Collingsworth County","Texas"],["Ness County","Kansas"],["Morton County","Kansas"],["Gove County","Kansas"],["Aurora County","South Dakota"],["Real County","Texas"],["Logan County","Kansas"],["Decatur County","Kansas"],["Sherman County","Texas"],["Jackson County","South Dakota"],["Trego County","Kansas"],["Hall County","Texas"],["Douglas County","South Dakota"],["Perkins County","South Dakota"],["Clay County","Georgia"],["Perkins County","Nebraska"],["Baker County","Georgia"],["Glascock County","Georgia"],["Franklin County","Nebraska"],["Brown County","Nebraska"],["Edwards County","Kansas"],["Jewell County","Kansas"],["Lincoln County","Kansas"],["Rush County","Kansas"],["Sherman County","Nebraska"],["Stanley County","South Dakota"],["Bowman County","North Dakota"],["Nelson County","North Dakota"],["Fallon County","Montana"],["Lipscomb County","Texas"],["Harlan County","Nebraska"],["Crockett County","Texas"],["Shackelford County","Texas"],["Woodson County","Kansas"],["Kinney County","Texas"],["Hand County","South Dakota"],["Hudspeth County","Texas"],["Sierra County","California"],["Tyrrell County","North Carolina"],["Donley County","Texas"],["Harper County","Oklahoma"],["Coke County","Texas"],["Emmons County","North Dakota"],["Concho County","Texas"],["Upton County","Texas"],["Granite County","Montana"],["Knox County","Texas"],["Traverse County","Minnesota"],["Sutton County","Texas"],["Chautauqua County","Kansas"],["Nance County","Nebraska"],["Bennett County","South Dakota"],["Hemphill County","Texas"],["Reagan County","Texas"],["Webster County","Nebraska"],["Foster County","North Dakota"],["Kimball County","Nebraska"],["Roger Mills County","Oklahoma"],["Hanson County","South Dakota"],["Baylor County","Texas"],["Costilla County","Colorado"],["Osborne County","Kansas"],["Baca County","Colorado"],["Lewis County","Idaho"],["Mercer County","Missouri"],["Sheridan County","Montana"],["Hardeman County","Texas"],["Smith County","Kansas"],["Catron County","New Mexico"],["Hardin County","Illinois"],["Fisher County","Texas"],["Sweet Grass County","Montana"],["Echols County","Georgia"],["Adams County","Iowa"],["Cavalier County","North Dakota"],["Lyman County","South Dakota"],["Knox County","Missouri"],["Ellis County","Oklahoma"],["Pope County","Illinois"],["Lake of the Woods County","Minnesota"],["Lake of the Woods County","Minnesota"],["Haskell County","Kansas"],["Sharkey County","Mississippi"],["Clark County","South Dakota"],["Sargent County","North Dakota"],["Chase County","Nebraska"],["Sioux County","North Dakota"],["Corson County","South Dakota"],["Red Lake County","Minnesota"],["Columbia County","Washington"],["Mason County","Texas"],["Wells County","North Dakota"],["Kearny County","Kansas"],["Edmunds County","South Dakota"],["Pierce County","North Dakota"],["Gregory County","South Dakota"],["Schuyler County","Missouri"],["Owsley County","Kentucky"],["Meade County","Kansas"],["Valley County","Nebraska"],["Stafford County","Kansas"],["Union County","New Mexico"],["LaMoure County","North Dakota"],["Nuckolls County","Nebraska"],["Dunn County","North Dakota"],["Storey County","Nevada"],["Tensas Parish","Louisiana"],["Grant County","Oklahoma"],["Hidalgo County","New Mexico"],["Mora County","New Mexico"],["Kittson County","Minnesota"],["Bath County","Virginia"],["Phillips County","Montana"],["Holt County","Missouri"],["Barber County","Kansas"],["Menominee County","Wisconsin"],["Custer County","Idaho"],["Kimble County","Texas"],["Deuel County","South Dakota"],["Marshall County","South Dakota"],["Adams County","Idaho"],["Wahkiakum County","Washington"],["Calhoun County","Illinois"],["Guadalupe County","New Mexico"],["Mills County","Texas"],["Dewey County","Oklahoma"],["Lincoln County","Nevada"],["Hickman County","Kentucky"],["Phillips County","Colorado"],["Mineral County","Montana"],["Schley County","Georgia"],["Cameron County","Pennsylvania"],["Mineral County","Nevada"],["Morrill County","Nebraska"],["Florence County","Wisconsin"],["Oneida County","Idaho"],["Hyde County","North Carolina"],["Hot Springs County","Wyoming"],["Furnas County","Nebraska"],["Ringgold County","Iowa"],["Republic County","Kansas"],["Crane County","Texas"],["Putnam County","Missouri"],["Custer County","Colorado"],["Scotland County","Missouri"],["Musselshell County","Montana"],["Calhoun County","Arkansas"],["Washington County","Colorado"],["Carlisle County","Kentucky"],["Jim Hogg County","Texas"],["Jim Hogg County","Texas"],["Ouray County","Colorado"],["Craig County","Virginia"],["Rooks County","Kansas"],["Gallatin County","Illinois"],["Scott County","Illinois"],["Toole County","Montana"],["Phillips County","Kansas"],["Wheeler County","Texas"],["Dickey County","North Dakota"],["Pickett County","Tennessee"],["Thayer County","Nebraska"],["Beaver County","Oklahoma"],["Garfield County","Utah"],["Hamilton County","New York"],["Lincoln County","Idaho"],["Sheridan County","Nebraska"],["Crosby County","Texas"],["Scott County","Kansas"],["Big Stone County","Minnesota"],["Kingsbury County","South Dakota"],["Pulaski County","Illinois"],["Wirt County","West Virginia"],["Carter County","Missouri"],["Polk County","Nebraska"],["Warren County","Georgia"],["Delta County","Texas"],["Martin County","Texas"],["Dewey County","South Dakota"],["Alexander County","Illinois"],["Brule County","South Dakota"],["Stevens County","Kansas"],["Coal County","Oklahoma"],["Hansford County","Texas"],["Johnson County","Nebraska"],["Atchison County","Missouri"],["Stewart County","Georgia"],["Walworth County","South Dakota"],["Jefferson County","Oklahoma"],["Luce County","Michigan"],["McHenry County","North Dakota"],["Boone County","Nebraska"],["Hartley County","Texas"],["Morris County","Kansas"],["Stark County","Illinois"],["Floyd County","Texas"],["Mahnomen County","Minnesota"],["Haskell County","Texas"],["Day County","South Dakota"],["Cherry County","Nebraska"],["Norton County","Kansas"],["Harper County","Kansas"],["Greer County","Oklahoma"],["Cotton County","Oklahoma"],["Washington County","Kansas"],["Fillmore County","Nebraska"],["Calhoun County","Georgia"],["Lynn County","Texas"],["Cook County","Minnesota"],["Dixon County","Nebraska"],["Cameron Parish","Louisiana"],["Tripp County","South Dakota"],["Putnam County","Illinois"],["Lincoln County","Minnesota"],["Bent County","Colorado"],["Gray County","Kansas"],["Audubon County","Iowa"],["Lincoln County","Colorado"],["McCook County","South Dakota"],["Alfalfa County","Oklahoma"],["Ransom County","North Dakota"],["San Saba County","Texas"],["San Saba County","Texas"],["San Saba County","Texas"],["San Saba County","Texas"],["Talbot County","Georgia"],["Lander County","Nevada"],["Ottawa County","Kansas"],["Mitchell County","Kansas"],["Carson County","Texas"],["Gilpin County","Colorado"],["Ontonagon County","Michigan"],["Garza County","Texas"],["Sullivan County","Pennsylvania"],["Stanton County","Nebraska"],["Cumberland County","Kentucky"],["Chouteau County","Montana"],["Taylor County","Iowa"],["Pondera County","Montana"],["Essex County","Vermont"],["Crowley County","Colorado"],["Sherman County","Kansas"],["Ohio County","Indiana"],["Benson County","North Dakota"],["Sullivan County","Missouri"],["Miller County","Georgia"],["Greenwood County","Kansas"],["Grant County","Minnesota"],["Reynolds County","Missouri"],["Shelby County","Missouri"],["Clay County","Nebraska"],["Menifee County","Kentucky"],["Presidio County","Texas"],["Iron County","Wisconsin"],["Pendleton County","West Virginia"],["Gentry County","Missouri"],["Hamlin County","South Dakota"],["Van Buren County","Tennessee"],["Quitman County","Mississippi"],["Osceola County","Iowa"],["Teton County","Montana"],["Calhoun County","West Virginia"],["Brown County","Illinois"],["Edwards County","Illinois"],["Pawnee County","Kansas"],["Woodruff County","Arkansas"],["Bland County","Virginia"],["Antelope County","Nebraska"],["Lafayette County","Arkansas"],["Moody County","South Dakota"],["Spink County","South Dakota"],["Saguache County","Colorado"],["Bear Lake County","Idaho"],["Ellsworth County","Kansas"],["Bottineau County","North Dakota"],["Henderson County","Illinois"],["Treutlen County","Georgia"],["Randolph County","Georgia"],["Norman County","Minnesota"],["Moore County","Tennessee"],["Howard County","Nebraska"],["Dallas County","Arkansas"],["Wayne County","Iowa"],["Wilkin County","Minnesota"],["Fulton County","Kentucky"],["Rio Blanco County","Colorado"],["Rio Blanco County","Colorado"],["Surry County","Virginia"],["Wolfe County","Kentucky"],["Fremont County","Iowa"],["King and Queen County","Virginia"],["King and Queen County","Virginia"],["King and Queen County","Virginia"],["Clark County","Missouri"],["Pershing County","Nevada"],["Hancock County","Tennessee"],["Childress County","Texas"],["La Salle County","Texas"],["Kearney County","Nebraska"],["Russell County","Kansas"],["Lac qui Parle County","Minnesota"],["Burt County","Nebraska"],["Refugio County","Texas"],["Clinch County","Georgia"],["Tucker County","West Virginia"],["Thurston County","Nebraska"],["Charles City County","Virginia"],["Broadwater County","Montana"],["Monroe County","Arkansas"],["Huerfano County","Colorado"],["Weston County","Wyoming"],["Pembina County","North Dakota"],["Wabaunsee County","Kansas"],["Schuyler County","Illinois"],["Bailey County","Texas"],["Powell County","Montana"],["Tillman County","Oklahoma"],["Swisher County","Texas"],["Forest County","Pennsylvania"],["Fall River County","South Dakota"],["Bon Homme County","South Dakota"],["Ida County","Iowa"],["Lake County","Tennessee"],["Goliad County","Texas"],["Caribou County","Idaho"],["Shannon County","Missouri"],["Blaine County","Montana"],["Beaver County","Utah"],["Nemaha County","Nebraska"],["Brooks County","Texas"],["Pocahontas County","Iowa"],["Kit Carson County","Colorado"],["Union County","Indiana"],["Dallam County","Texas"],["Ferry County","Washington"],["Crook County","Wyoming"],["Van Buren County","Iowa"],["Newton County","Arkansas"],["Grant County","Oregon"],["Jefferson County","Nebraska"],["Jefferson County","Mississippi"],["Jefferson County","Mississippi"],["Grand Isle County","Vermont"],["Pierce County","Nebraska"],["Pepin County","Wisconsin"],["Rappahannock County","Virginia"],["Grant County","Kansas"],["Elliott County","Kentucky"],["Castro County","Texas"],["Wallowa County","Oregon"],["Lee County","Kentucky"],["Chariton County","Missouri"],["Gilmer County","West Virginia"],["Hutchinson County","South Dakota"],["Lake County","Colorado"],["Worth County","Iowa"],["East Carroll Parish","Louisiana"],["East Carroll Parish","Louisiana"],["East Carroll Parish","Louisiana"],["Conejos County","Colorado"],["Kingman County","Kansas"],["Wheeler County","Georgia"],["Harney County","Oregon"],["Adair County","Iowa"],["Marion County","Georgia"],["Doniphan County","Kansas"],["Nicholas County","Kentucky"],["Cleveland County","Arkansas"],["Grant County","South Dakota"],["Dade County","Missouri"],["Monroe County","Iowa"],["Valley County","Montana"],["Clay County","Tennessee"],["Boise County","Idaho"],["Red River Parish","Louisiana"],["McCulloch County","Texas"],["Decatur County","Iowa"],["Benton County","Mississippi"],["Pleasants County","West Virginia"],["Kane County","Utah"],["Merrick County","Nebraska"],["Franklin County","Mississippi"],["Coleman County","Texas"],["Washakie County","Wyoming"],["Lincoln County","Georgia"],["Yoakum County","Texas"],["Ballard County","Kentucky"],["Greene County","Alabama"],["Major County","Oklahoma"],["Humphreys County","Mississippi"],["Winkler County","Texas"],["Doddridge County","West Virginia"],["Taylor County","Georgia"],["Searcy County","Arkansas"],["Anderson County","Kansas"],["Pocahontas County","West Virginia"],["Richardson County","Nebraska"],["Power County","Idaho"],["San Augustine County","Texas"],["San Augustine County","Texas"],["San Augustine County","Texas"],["San Augustine County","Texas"],["Thomas County","Kansas"],["Liberty County","Florida"],["Lemhi County","Idaho"],["Hamilton County","Illinois"],["Traill County","North Dakota"],["Twiggs County","Georgia"],["Graham County","North Carolina"],["Allendale County","South Carolina"],["Schoolcraft County","Michigan"],["Clay County","West Virginia"],["San Miguel County","Colorado"],["San Miguel County","Colorado"],["Clay County","Kansas"],["Harrison County","Missouri"],["Baraga County","Michigan"],["Lake County","Oregon"],["Murray County","Minnesota"],["Franklin city","Virginia"],["Dawes County","Nebraska"],["Oscoda County","Michigan"],["Hamilton County","Texas"],["Lafayette County","Florida"],["Choctaw County","Mississippi"],["Hickory County","Missouri"],["Prairie County","Arkansas"],["Houston County","Tennessee"],["Atkinson County","Georgia"],["Nevada County","Arkansas"],["Tyler County","West Virginia"],["Custer County","South Dakota"],["Rosebud County","Montana"],["Keith County","Nebraska"],["Mercer County","North Dakota"],["Coffey County","Kansas"],["Perry County","Tennessee"],["Butler County","Nebraska"],["Webster County","West Virginia"],["Cedar County","Nebraska"],["Knox County","Nebraska"],["Bracken County","Kentucky"],["Daviess County","Missouri"],["Maries County","Missouri"],["Warren County","Indiana"],["Ritchie County","West Virginia"],["Johnson County","Wyoming"],["Jack County","Texas"],["Trimble County","Kentucky"],["Montgomery County","Arkansas"],["Carroll County","Missouri"],["Kiowa County","Oklahoma"],["Perry County","Alabama"],["Clearwater County","Minnesota"],["Mathews County","Virginia"],["Ozark County","Missouri"],["Archer County","Texas"],["Wilkinson County","Mississippi"],["Lee County","Arkansas"],["Platte County","Wyoming"],["Montgomery County","Georgia"],["Dimmit County","Texas"],["Madison County","Montana"],["Wilson County","Kansas"],["Woods County","Oklahoma"],["Lucas County","Iowa"],["Oregon County","Missouri"],["Monroe County","Missouri"],["Turner County","South Dakota"],["Jenkins County","Georgia"],["Lyon County","Kentucky"],["Gallatin County","Kentucky"],["Modoc County","California"],["Benton County","Indiana"],["Sublette County","Wyoming"],["Clearwater County","Idaho"],["Hancock County","Georgia"],["Blaine County","Oklahoma"],["Quay County","New Mexico"],["Monona County","Iowa"],["Wilcox County","Georgia"],["Greene County","Iowa"],["Caldwell County","Missouri"],["Alger County","Michigan"],["Wilkinson County","Georgia"],["Livingston County","Kentucky"],["Catahoula Parish","Louisiana"],["Richmond County","Virginia"],["Dawson County","Montana"],["Stillwater County","Montana"],["Phelps County","Nebraska"],["Kemper County","Mississippi"],["Crittenden County","Kentucky"],["Mitchell County","Texas"],["Palo Alto County","Iowa"],["Turner County","Georgia"],["Cuming County","Nebraska"],["Cloud County","Kansas"],["Marshall County","Minnesota"],["White Pine County","Nevada"],["Hancock County","Kentucky"],["Stephens County","Texas"],["Davis County","Iowa"],["Claiborne County","Mississippi"],["Seminole County","Georgia"],["McLean County","Kentucky"],["Montmorency County","Michigan"],["Pratt County","Kansas"],["Jones County","North Carolina"],["Forest County","Wisconsin"],["Terrell County","Georgia"],["Johnson County","Georgia"],["Somervell County","Texas"],["Clinton County","Kentucky"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["Jasper County","Illinois"],["Todd County","South Dakota"],["Nowata County","Oklahoma"],["Beaverhead County","Montana"],["Charles Mix County","South Dakota"],["Emmet County","Iowa"],["Clear Creek County","Colorado"],["Deer Lodge County","Montana"],["Pipestone County","Minnesota"],["Rice County","Kansas"],["Hamilton County","Nebraska"],["Latimer County","Oklahoma"],["Cheyenne County","Nebraska"],["Howard County","Iowa"],["Brown County","Kansas"],["McCormick County","South Carolina"],["Yellow Medicine County","Minnesota"],["Benewah County","Idaho"],["Iron County","Missouri"],["Brewster County","Texas"],["Greenlee County","Arizona"],["Chattahoochee County","Georgia"],["Wilkes County","Georgia"],["Linn County","Kansas"],["Humboldt County","Iowa"],["Caldwell Parish","Louisiana"],["Irwin County","Georgia"],["Grand County","Utah"],["Zavala County","Texas"],["Stevens County","Minnesota"],["Cumberland County","Virginia"],["Wayne County","Nebraska"],["Rock County","Minnesota"],["Marion County","Texas"],["Switzerland County","Indiana"],["Clarke County","Iowa"],["West Carroll Parish","Louisiana"],["West Carroll Parish","Louisiana"],["West Carroll Parish","Louisiana"],["McLean County","North Dakota"],["Tunica County","Mississippi"],["Grundy County","Missouri"],["Mountrail County","North Dakota"],["Martin County","Indiana"],["Sac County","Iowa"],["Montgomery County","Mississippi"],["Emery County","Utah"],["Duval County","Texas"],["Scott County","Arkansas"],["Swift County","Minnesota"],["Pulaski County","Georgia"],["Parmer County","Texas"],["Lanier County","Georgia"],["Sabine County","Texas"],["Runnels County","Texas"],["Webster County","Mississippi"],["Calhoun County","Iowa"],["Yuma County","Colorado"],["Jackson County","Minnesota"],["Carroll County","Mississippi"],["Ochiltree County","Texas"],["Madison Parish","Louisiana"],["Perry County","Arkansas"],["Franklin County","Iowa"],["Lewis County","Missouri"],["Keokuk County","Iowa"],["Marshall County","Kansas"],["Holt County","Nebraska"],["Love County","Oklahoma"],["Howard County","Missouri"],["Alcona County","Michigan"],["Pike County","Arkansas"],["Chicot County","Arkansas"],["Clay County","Texas"],["Butte County","South Dakota"],["Johnston County","Oklahoma"],["Nemaha County","Kansas"],["Roberts County","South Dakota"],["Noxubee County","Mississippi"],["Metcalfe County","Kentucky"],["Lowndes County","Alabama"],["Montgomery County","Iowa"],["Ralls County","Missouri"],["Camden County","North Carolina"],["Bullock County","Alabama"],["Franklin County","Texas"],["Coosa County","Alabama"],["Cumberland County","Illinois"],["Carbon County","Montana"],["Gates County","North Carolina"],["Washington County","Idaho"],["Leslie County","Kentucky"],["Crawford County","Indiana"],["Bradley County","Arkansas"],["Custer County","Nebraska"],["Walsh County","North Dakota"],["Mitchell County","Iowa"],["Bollinger County","Missouri"],["Colfax County","Nebraska"],["Essex County","Virginia"],["Wilcox County","Alabama"],["Guthrie County","Iowa"],["Middlesex County","Virginia"],["Winnebago County","Iowa"],["Ripley County","Missouri"],["Red Willow County","Nebraska"],["Evans County","Georgia"],["Roosevelt County","Montana"],["Hancock County","Iowa"],["Carroll County","Kentucky"],["Pushmataha County","Oklahoma"],["Sussex County","Virginia"],["Mackinac County","Michigan"],["Louisa County","Iowa"],["Box Butte County","Nebraska"],["Barnes County","North Dakota"],["Early County","Georgia"],["Lincoln County","Washington"],["Alleghany County","North Carolina"],["Lake County","Minnesota"],["Lake County","Minnesota"],["Lancaster County","Virginia"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["Noble County","Oklahoma"],["Washita County","Oklahoma"],["Wayne County","Missouri"],["McIntosh County","Georgia"],["Grant County","West Virginia"],["Candler County","Georgia"],["Washington County","North Carolina"],["DeKalb County","Missouri"],["Lake County","South Dakota"],["Clay County","North Carolina"],["Green County","Kentucky"],["Bacon County","Georgia"],["Dooly County","Georgia"],["Watonwan County","Minnesota"],["Owen County","Kentucky"],["Martin County","Kentucky"],["Pope County","Minnesota"],["Okfuskee County","Oklahoma"],["Jefferson Davis County","Mississippi"],["Jefferson Davis County","Mississippi"],["Montgomery County","Missouri"],["Live Oak County","Texas"],["Monroe County","Kentucky"],["Wabash County","Illinois"],["Blanco County","Texas"],["Desha County","Arkansas"],["Heard County","Georgia"],["Decatur County","Tennessee"],["Fergus County","Montana"],["Richland County","Montana"],["Perry County","Mississippi"],["Cottonwood County","Minnesota"],["Big Horn County","Wyoming"],["Charlotte County","Virginia"],["Rio Grande County","Colorado"],["Rio Grande County","Colorado"],["Haskell County","Oklahoma"],["Sierra County","New Mexico"],["Douglas County","Missouri"],["Red River County","Texas"],["Conecuh County","Alabama"],["Ramsey County","North Dakota"],["Trousdale County","Tennessee"],["Jackson County","Tennessee"],["Teton County","Idaho"],["Iron County","Michigan"],["Magoffin County","Kentucky"],["Barton County","Missouri"],["Ward County","Texas"],["Cherokee County","Iowa"],["Marshall County","Illinois"],["Valley County","Idaho"],["Shelby County","Iowa"],["Juab County","Utah"],["Marion County","Kansas"],["Terry County","Texas"],["Northumberland County","Virginia"],["Custer County","Montana"],["Linn County","Missouri"],["Owyhee County","Idaho"],["Lyon County","Iowa"],["Lunenburg County","Virginia"],["Summers County","West Virginia"],["Morris County","Texas"],["Greene County","Illinois"],["Prowers County","Colorado"],["Chickasaw County","Iowa"],["Lawrence County","Mississippi"],["Little River County","Arkansas"],["Washington County","Kentucky"],["Skamania County","Washington"],["Boundary County","Idaho"],["Koochiching County","Minnesota"],["Fulton County","Arkansas"],["Macon County","Georgia"],["Jefferson County","Montana"],["Lake County","Michigan"],["Blackford County","Indiana"],["Glades County","Florida"],["Edmonson County","Kentucky"],["Crawford County","Georgia"],["Union County","Iowa"],["Rains County","Texas"],["Morrow County","Oregon"],["Rolette County","North Dakota"],["Newton County","Texas"],["Todd County","Kentucky"],["Pike County","Indiana"],["Pamlico County","North Carolina"],["Northampton County","Virginia"],["Morgan County","Utah"],["Menard County","Illinois"],["Appanoose County","Iowa"],["Grundy County","Iowa"],["Sumter County","Alabama"],["Stone County","Arkansas"],["Butler County","Kentucky"],["Monroe County","West Virginia"],["Colfax County","New Mexico"],["Sanders County","Montana"],["Braxton County","West Virginia"],["Franklin County","Florida"],["Dawson County","Texas"],["Camp County","Texas"],["Telfair County","Georgia"],["Yalobusha County","Mississippi"],["Towns County","Georgia"],["Goshen County","Wyoming"],["Pulaski County","Indiana"],["Charlton County","Georgia"],["Allen County","Kansas"],["Mississippi County","Missouri"],["Lewis County","Tennessee"],["Bleckley County","Georgia"],["Chippewa County","Minnesota"],["Madison County","Missouri"],["Caldwell County","Kentucky"],["Choctaw County","Alabama"],["Tallahatchie County","Mississippi"],["Amite County","Mississippi"],["Bath County","Kentucky"],["Meigs County","Tennessee"],["Howard County","Arkansas"],["Vinton County","Ohio"],["Wilbarger County","Texas"],["Lincoln County","Arkansas"],["Wright County","Iowa"],["Jackson County","Kentucky"],["Millard County","Utah"],["Bienville Parish","Louisiana"],["Presque Isle County","Michigan"],["Crawford County","Michigan"],["Perquimans County","North Carolina"],["Webster County","Kentucky"],["Cass County","Illinois"],["Lamb County","Texas"],["Lewis County","Kentucky"],["Mason County","Illinois"],["Big Horn County","Montana"],["Cass County","Iowa"],["Powell County","Kentucky"],["Shoshone County","Idaho"],["Crenshaw County","Alabama"],["Mono County","California"],["Jackson County","Kansas"],["Amelia County","Virginia"],["Calhoun County","Mississippi"],["Osage County","Missouri"],["Clay County","Illinois"],["Moffat County","Colorado"],["Johnson County","Illinois"],["Bamberg County","South Carolina"],["Buffalo County","Wisconsin"],["Archuleta County","Colorado"],["Hughes County","Oklahoma"],["Monroe County","Ohio"],["Fremont County","Idaho"],["Pend Oreille County","Washington"],["Madison County","Texas"],["Grundy County","Tennessee"],["Greene County","Mississippi"],["Ford County","Illinois"],["Izard County","Arkansas"],["Comanche County","Texas"],["Trinity County","Texas"],["Calhoun County","Florida"],["Stewart County","Tennessee"],["Union County","Kentucky"],["Oglala Lakota County","South Dakota"],["Chowan County","North Carolina"],["Callahan County","Texas"],["Breathitt County","Kentucky"],["Morgan County","Kentucky"],["Converse County","Wyoming"],["Winn Parish","Louisiana"],["Washington County","Illinois"],["Glacier County","Montana"],["Morgan County","Ohio"],["Newton County","Indiana"],["Madison County","Virginia"],["White County","Illinois"],["Walthall County","Mississippi"],["Zapata County","Texas"],["Murray County","Oklahoma"],["Crockett County","Tennessee"],["Faribault County","Minnesota"],["Lamar County","Alabama"],["Pennington County","Minnesota"],["Hamilton County","Florida"],["Roane County","West Virginia"],["Price County","Wisconsin"],["Allamakee County","Iowa"],["Trigg County","Kentucky"],["Wadena County","Minnesota"],["Screven County","Georgia"],["Craig County","Oklahoma"],["Noble County","Ohio"],["Swain County","North Carolina"],["Calhoun County","South Carolina"],["Dickenson County","Virginia"],["York County","Nebraska"],["Atoka County","Oklahoma"],["Estill County","Kentucky"],["Massac County","Illinois"],["Claiborne Parish","Louisiana"],["O'Brien County","Iowa"],["Cedar County","Missouri"],["Rusk County","Wisconsin"],["Gulf County","Florida"],["Franklin County","Idaho"],["Choctaw County","Oklahoma"],["Smith County","Mississippi"],["Clay County","Alabama"],["Knott County","Kentucky"],["Nantucket County","Massachusetts"],["Saline County","Nebraska"],["Hardy County","West Virginia"],["Butler County","Iowa"],["Bourbon County","Kansas"],["Gogebic County","Michigan"],["Dent County","Missouri"],["Wetzel County","West Virginia"],["Harrison County","Ohio"],["Mills County","Iowa"],["Cannon County","Tennessee"],["Jefferson County","Florida"],["San Juan County","Utah"],["Moultrie County","Illinois"],["Carbon County","Wyoming"],["Clay County","Arkansas"],["Las Animas County","Colorado"],["Fulton County","Pennsylvania"],["Livingston County","Missouri"],["Harrison County","Iowa"],["Jasper County","Georgia"],["Pendleton County","Kentucky"],["McKenzie County","North Dakota"],["Karnes County","Texas"],["Renville County","Minnesota"],["Nolan County","Texas"],["Pike County","Illinois"],["Reeves County","Texas"],["Nelson County","Virginia"],["Jeff Davis County","Georgia"],["Clarke County","Virginia"],["Hale County","Alabama"],["LaSalle Parish","Louisiana"],["Gasconade County","Missouri"],["Oglethorpe County","Georgia"],["Kossuth County","Iowa"],["Sibley County","Minnesota"],["Larue County","Kentucky"],["Mitchell County","North Carolina"],["Bledsoe County","Tennessee"],["Clay County","South Dakota"],["Jackson County","Texas"],["Arenac County","Michigan"],["Jackson Parish","Louisiana"],["Hamilton County","Iowa"],["Torrance County","New Mexico"],["Missaukee County","Michigan"],["Cleburne County","Alabama"],["Fleming County","Kentucky"],["Kingfisher County","Oklahoma"],["Pecos County","Texas"],["Macon County","Missouri"],["Page County","Iowa"],["Lawrence County","Illinois"],["West Feliciana Parish","Louisiana"],["West Feliciana Parish","Louisiana"],["West Feliciana Parish","Louisiana"],["Marshall County","Oklahoma"],["Roseau County","Minnesota"],["Grayson County","Virginia"],["Tipton County","Indiana"],["Washington County","Alabama"],["Redwood County","Minnesota"],["Vermillion County","Indiana"],["Clark County","Illinois"],["Barbour County","West Virginia"],["Moniteau County","Missouri"],["Brown County","Indiana"],["Floyd County","Virginia"],["De Witt County","Illinois"],["Pawnee County","Oklahoma"],["Marquette County","Wisconsin"],["Gooding County","Idaho"],["Clarke County","Mississippi"],["Floyd County","Iowa"],["Nottoway County","Virginia"],["Pemiscot County","Missouri"],["Jefferson County","Iowa"],["Henry County","Kentucky"],["Aitkin County","Minnesota"],["Mercer County","Illinois"],["Carroll County","Illinois"],["Jefferson County","Georgia"],["Grand County","Colorado"],["Leon County","Texas"],["Osage County","Kansas"],["Van Buren County","Arkansas"],["Richland County","Illinois"],["Sequatchie County","Tennessee"],["Sevier County","Arkansas"],["Brunswick County","Virginia"],["Benton County","Tennessee"],["Neosho County","Kansas"],["Otoe County","Nebraska"],["Casey County","Kentucky"],["Ashland County","Wisconsin"],["Kanabec County","Minnesota"],["Rockcastle County","Kentucky"],["Bates County","Missouri"],["Trinity County","California"],["Crawford County","Wisconsin"],["Appomattox County","Virginia"],["Union County","Florida"],["Parke County","Indiana"],["Long County","Georgia"],["Wayne County","Illinois"],["Lawrence County","Arkansas"],["Bayfield County","Wisconsin"],["Wayne County","Tennessee"],["Dade County","Georgia"],["Lawrence County","Kentucky"],["Brooks County","Georgia"],["Hill County","Montana"],["Fayette County","Alabama"],["Atchison County","Kansas"],["Jasper County","Mississippi"],["Alamosa County","Colorado"],["Clay County","Iowa"],["Potter County","Pennsylvania"],["New Madrid County","Missouri"],["Fountain County","Indiana"],["Madison County","Arkansas"],["Crawford County","Iowa"],["Burnett County","Wisconsin"],["Richland County","North Dakota"],["Lee County","South Carolina"],["Madison County","Iowa"],["La Paz County","Arizona"],["Phillips County","Arkansas"],["Socorro County","New Mexico"],["Lafayette County","Wisconsin"],["Washburn County","Wisconsin"],["Baker County","Oregon"],["Piatt County","Illinois"],["Taylor County","West Virginia"],["Bond County","Illinois"],["Rush County","Indiana"],["Jackson County","Arkansas"],["Robertson County","Texas"],["Dixie County","Florida"],["Giles County","Virginia"],["Piscataquis County","Maine"],["Union County","South Dakota"],["Buckingham County","Virginia"],["Marion County","Arkansas"],["Cross County","Arkansas"],["Warren County","Illinois"],["Edgar County","Illinois"],["Hardin County","Iowa"],["Rabun County","Georgia"],["McCreary County","Kentucky"],["Gunnison County","Colorado"],["Scurry County","Texas"],["Garrard County","Kentucky"],["Falls County","Texas"],["Holmes County","Mississippi"],["Lewis County","West Virginia"],["Clayton County","Iowa"],["Morgan County","West Virginia"],["Dallas County","Missouri"],["Franklin County","Arkansas"],["Cooper County","Missouri"],["Chickasaw County","Mississippi"],["Mason County","Kentucky"],["Mariposa County","California"],["Tama County","Iowa"],["Henry County","Alabama"],["Park County","Montana"],["Ben Hill County","Georgia"],["Cook County","Georgia"],["Union County","Illinois"],["Sharp County","Arkansas"],["Humboldt County","Nevada"],["Richland County","Wisconsin"],["Chester County","Tennessee"],["Drew County","Arkansas"],["Pitkin County","Colorado"],["Park County","Colorado"],["Northampton County","North Carolina"],["Lee County","Texas"],["Delaware County","Iowa"],["Polk County","Tennessee"],["Pike County","Missouri"],["Patrick County","Virginia"],["Seward County","Nebraska"],["Hancock County","Illinois"],["Burleson County","Texas"],["Dickinson County","Iowa"],["Winston County","Mississippi"],["Eastland County","Texas"],["Hughes County","South Dakota"],["San Juan County","Washington"],["Avery County","North Carolina"],["King William County","Virginia"],["King William County","Virginia"],["King William County","Virginia"],["Gilchrist County","Florida"],["Haywood County","Tennessee"],["Young County","Texas"],["Attala County","Mississippi"],["Schuyler County","New York"],["Unicoi County","Tennessee"],["Bertie County","North Carolina"],["Kalkaska County","Michigan"],["Johnson County","Tennessee"],["Grant County","Arkansas"],["Madison County","Florida"],["Benzie County","Michigan"],["Russell County","Kentucky"],["Brantley County","Georgia"],["Banks County","Georgia"],["Sawyer County","Wisconsin"],["Andrew County","Missouri"],["Montour County","Pennsylvania"],["Berrien County","Georgia"],["Wright County","Missouri"],["Bosque County","Texas"],["Stone County","Mississippi"],["Covington County","Mississippi"],["Jefferson County","Kansas"],["Frio County","Texas"],["Dickinson County","Kansas"],["Appling County","Georgia"],["Yancey County","North Carolina"],["Westmoreland County","Virginia"],["Ste. Genevieve County","Missouri"],["Fentress County","Tennessee"],["Lamar County","Georgia"],["Cedar County","Iowa"],["Hampton County","South Carolina"],["Randolph County","Arkansas"],["Deaf Smith County","Texas"],["Andrews County","Texas"],["Clay County","Mississippi"],["Warren County","North Carolina"],["Poweshiek County","Iowa"],["Crawford County","Illinois"],["Concordia Parish","Louisiana"],["Otero County","Colorado"],["Harrison County","Kentucky"],["Paulding County","Ohio"],["Houston County","Minnesota"],["Tishomingo County","Mississippi"],["Saluda County","South Carolina"],["Pike County","Georgia"],["Adair County","Kentucky"],["Greene County","Georgia"],["McIntosh County","Oklahoma"],["Perry County","Missouri"],["Waseca County","Minnesota"],["Humphreys County","Tennessee"],["Inyo County","California"],["Green Lake County","Wisconsin"],["Green Lake County","Wisconsin"],["Butler County","Alabama"],["Ashley County","Arkansas"],["McDowell County","West Virginia"],["Pickens County","Alabama"],["Gem County","Idaho"],["Beadle County","South Dakota"],["Perry County","Indiana"],["Roosevelt County","New Mexico"],["Kent County","Maryland"],["Polk County","Arkansas"],["Hart County","Kentucky"],["Marengo County","Alabama"],["Polk County","North Carolina"],["Cherokee County","Kansas"],["Benton County","Missouri"],["Los Alamos County","New Mexico"],["Freestone County","Texas"],["Chaffee County","Colorado"],["Jackson County","Iowa"],["Spencer County","Kentucky"],["Langlade County","Wisconsin"],["Adair County","Oklahoma"],["Fayette County","Iowa"],["Macon County","Alabama"],["East Feliciana Parish","Louisiana"],["East Feliciana Parish","Louisiana"],["East Feliciana Parish","Louisiana"],["Wayne County","Kentucky"],["Marion County","Kentucky"],["Lincoln County","Wyoming"],["Simpson County","Kentucky"],["Duchesne County","Utah"],["Elbert County","Georgia"],["Holmes County","Florida"],["Gonzales County","Texas"],["Jones County","Texas"],["Lincoln County","Montana"],["Vernon County","Missouri"],["Pierce County","Georgia"],["Douglas County","Illinois"],["Monroe County","Alabama"],["Franklin Parish","Louisiana"],["Wayne County","Mississippi"],["Plumas County","California"],["Tyler County","Texas"],["Union County","Tennessee"],["Spencer County","Indiana"],["DeWitt County","Texas"],["Orange County","Indiana"],["Smith County","Tennessee"],["Taylor County","Wisconsin"],["Dodge County","Georgia"],["Davison County","South Dakota"],["Montague County","Texas"],["Washington County","Georgia"],["Martin County","Minnesota"],["Richland Parish","Louisiana"],["Hempstead County","Arkansas"],["Winneshiek County","Iowa"],["DeKalb County","Tennessee"],["Morgan County","Georgia"],["Calhoun County","Texas"],["Crisp County","Georgia"],["Willacy County","Texas"],["Labette County","Kansas"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["Bourbon County","Kentucky"],["Yell County","Arkansas"],["Lincoln County","New Mexico"],["Carroll County","Indiana"],["Lavaca County","Texas"],["Clay County","Kentucky"],["Buchanan County","Virginia"],["Carbon County","Utah"],["Breckinridge County","Kentucky"],["Uinta County","Wyoming"],["Greene County","North Carolina"],["Lincoln County","West Virginia"],["Woodward County","Oklahoma"],["Jay County","Indiana"],["Fulton County","Indiana"],["Henry County","Iowa"],["Greene County","Virginia"],["Colorado County","Texas"],["Kewaunee County","Wisconsin"],["Buchanan County","Iowa"],["Allen County","Kentucky"],["Barnwell County","South Carolina"],["Dukes County","Massachusetts"],["Meriwether County","Georgia"],["Adams County","Washington"],["Hutchinson County","Texas"],["Jones County","Iowa"],["Adams County","Wisconsin"],["Conway County","Arkansas"],["Pointe Coupee Parish","Louisiana"],["Carroll County","Iowa"],["Ogemaw County","Michigan"],["Worth County","Georgia"],["Sullivan County","Indiana"],["Buena Vista County","Iowa"],["Bandera County","Texas"],["Washington County","Nebraska"],["Dodge County","Minnesota"],["Perry County","Illinois"],["Fairfield County","South Carolina"],["Shelby County","Illinois"],["Morgan County","Missouri"],["Morgan County","Tennessee"],["Assumption Parish","Louisiana"],["Union Parish","Louisiana"],["Logan County","Arkansas"],["Jackson County","Wisconsin"],["Clinton County","Missouri"],["Madison County","North Carolina"],["Gray County","Texas"],["Fillmore County","Minnesota"],["Nodaway County","Missouri"],["Llano County","Texas"],["Leake County","Mississippi"],["Newton County","Mississippi"],["Owen County","Indiana"],["Hubbard County","Minnesota"],["Moore County","Texas"],["Wyoming County","West Virginia"],["Texas County","Oklahoma"],["Wabasha County","Minnesota"],["Coahoma County","Mississippi"],["Clark County","Arkansas"],["Fayette County","Illinois"],["Jersey County","Illinois"],["Sevier County","Utah"],["Logan County","Colorado"],["Hockley County","Texas"],["Letcher County","Kentucky"],["Hertford County","North Carolina"],["Scott County","Virginia"],["Dakota County","Nebraska"],["Stutsman County","North Dakota"],["Gaines County","Texas"],["Minidoka County","Idaho"],["Lampasas County","Texas"],["Grenada County","Mississippi"],["McDuffie County","Georgia"],["Gage County","Nebraska"],["Mitchell County","Georgia"],["Taylor County","Florida"],["Boone County","West Virginia"],["Tippah County","Mississippi"],["Colusa County","California"],["Prince Edward County","Virginia"],["Scott County","Tennessee"],["Wyandot County","Ohio"],["Henry County","Missouri"],["Seward County","Kansas"],["Randolph County","Alabama"],["Martin County","North Carolina"],["Jo Daviess County","Illinois"],["Putnam County","Georgia"],["Anson County","North Carolina"],["Houston County","Texas"],["Limestone County","Texas"],["Sabine Parish","Louisiana"],["Grant Parish","Louisiana"],["Lee County","Virginia"],["Mahaska County","Iowa"],["Meigs County","Ohio"],["Saunders County","Nebraska"],["Asotin County","Washington"],["Nobles County","Minnesota"],["Bibb County","Alabama"],["Leelanau County","Michigan"],["Sumner County","Kansas"],["Beckham County","Oklahoma"],["Panola County","Texas"],["Overton County","Tennessee"],["Brooke County","West Virginia"],["Washington County","Iowa"],["Mercer County","Kentucky"],["Ouachita County","Arkansas"],["Johnson County","Kentucky"],["Klickitat County","Washington"],["Caswell County","North Carolina"],["Allen Parish","Louisiana"],["Emanuel County","Georgia"],["Franklin County","Indiana"],["Columbia County","Arkansas"],["Tattnall County","Georgia"],["Osceola County","Michigan"],["New Kent County","Virginia"],["Poinsett County","Arkansas"],["Vilas County","Wisconsin"],["Crawford County","Missouri"],["Clarke County","Alabama"],["St. Francis County","Arkansas"],["Hampshire County","West Virginia"],["Ray County","Missouri"],["McDonald County","Missouri"],["Yankton County","South Dakota"],["Teton County","Wyoming"],["Saline County","Missouri"],["Pacific County","Washington"],["Starke County","Indiana"],["Fayette County","Indiana"],["Meeker County","Minnesota"],["Franklin County","Georgia"],["Antrim County","Michigan"],["Curry County","Oregon"],["Roscommon County","Michigan"],["Menominee County","Michigan"],["Juniata County","Pennsylvania"],["Washington County","Missouri"],["Plaquemines Parish","Louisiana"],["Grainger County","Tennessee"],["Winston County","Alabama"],["Seminole County","Oklahoma"],["Mingo County","West Virginia"],["Page County","Virginia"],["Iowa County","Wisconsin"],["Saline County","Illinois"],["Ohio County","Kentucky"],["Upshur County","West Virginia"],["Aransas County","Texas"],["Anderson County","Kentucky"],["Itawamba County","Mississippi"],["Hood River County","Oregon"],["Shelby County","Texas"],["Bell County","Kentucky"],["Dawson County","Nebraska"],["Jerome County","Idaho"],["Blaine County","Idaho"],["Lincoln County","Kentucky"],["Abbeville County","South Carolina"],["George County","Mississippi"],["Scott County","Indiana"],["Fayette County","Texas"],["Marion County","Mississippi"],["Texas County","Missouri"],["Randolph County","Indiana"],["Jefferson County","Oregon"],["Waushara County","Wisconsin"],["Uvalde County","Texas"],["Burke County","Georgia"],["Nicholas County","West Virginia"],["Somerset County","Maryland"],["Union County","Georgia"],["Cassia County","Idaho"],["Rowan County","Kentucky"],["White County","Indiana"],["Teller County","Colorado"],["Cleburne County","Arkansas"],["Randolph County","Missouri"],["Miller County","Missouri"],["Goochland County","Virginia"],["Crook County","Oregon"],["Milam County","Texas"],["Yates County","New York"],["Jackson County","Oklahoma"],["Routt County","Colorado"],["Hickman County","Tennessee"],["Grant County","Kentucky"],["Audrain County","Missouri"],["Chattooga County","Georgia"],["Cherokee County","Alabama"],["Bremer County","Iowa"],["Prentiss County","Mississippi"],["Manistee County","Michigan"],["Otsego County","Michigan"],["Lauderdale County","Tennessee"],["Macon County","Tennessee"],["Posey County","Indiana"],["Barbour County","Alabama"],["Iosco County","Michigan"],["Todd County","Minnesota"],["Lyon County","Minnesota"],["Adair County","Missouri"],["Washington County","Florida"],["Fannin County","Georgia"],["Hardee County","Florida"],["Pottawatomie County","Kansas"],["Payette County","Idaho"],["Gladwin County","Michigan"],["Luna County","New Mexico"],["Butts County","Georgia"],["Mason County","West Virginia"],["Hardeman County","Tennessee"],["Barton County","Kansas"],["Churchill County","Nevada"],["Benton County","Iowa"],["Cheboygan County","Michigan"],["Morehouse Parish","Louisiana"],["Garvin County","Oklahoma"],["Edgefield County","South Carolina"],["Plymouth County","Iowa"],["Johnson County","Arkansas"],["Montgomery County","North Carolina"],["Lawrence County","South Dakota"],["Russell County","Virginia"],["Hart County","Georgia"],["Montezuma County","Colorado"],["McNairy County","Tennessee"],["Brown County","Minnesota"],["Lamoille County","Vermont"],["Dickinson County","Michigan"],["Simpson County","Mississippi"],["Sunflower County","Mississippi"],["Franklin County","Kansas"],["Taylor County","Kentucky"],["Charlevoix County","Michigan"],["Elbert County","Colorado"],["Wyoming County","Pennsylvania"],["Union County","Oregon"],["Grady County","Georgia"],["Grayson County","Kentucky"],["Mille Lacs County","Minnesota"],["Clay County","Indiana"],["Decatur County","Indiana"],["Ashe County","North Carolina"],["Lewis County","New York"],["Cass County","Nebraska"],["Carter County","Kentucky"],["Geneva County","Alabama"],["Oceana County","Michigan"],["Marlboro County","South Carolina"],["Wasco County","Oregon"],["Boone County","Iowa"],["Juneau County","Wisconsin"],["Carroll County","Ohio"],["King George County","Virginia"],["King George County","Virginia"],["King George County","Virginia"],["Gillespie County","Texas"],["Yazoo County","Mississippi"],["Stephens County","Georgia"],["Dawson County","Georgia"],["De Soto Parish","Louisiana"],["Harlan County","Kentucky"],["Hardin County","Tennessee"],["Woodford County","Kentucky"],["Mineral County","West Virginia"],["Caddo County","Oklahoma"],["Toombs County","Georgia"],["Iroquois County","Illinois"],["Pike County","Ohio"],["Cibola County","New Mexico"],["West Baton Rouge Parish","Louisiana"],["West Baton Rouge Parish","Louisiana"],["West Baton Rouge Parish","Louisiana"],["San Miguel County","New Mexico"],["San Miguel County","New Mexico"],["McDonough County","Illinois"],["Union County","South Carolina"],["Fluvanna County","Virginia"],["White County","Tennessee"],["Tillamook County","Oregon"],["Orleans County","Vermont"],["San Jacinto County","Texas"],["San Jacinto County","Texas"],["San Jacinto County","Texas"],["San Jacinto County","Texas"],["Logan County","Kentucky"],["Adams County","Ohio"],["Jennings County","Indiana"],["Henry County","Ohio"],["Upson County","Georgia"],["Del Norte County","California"],["Union County","Mississippi"],["Jackson County","West Virginia"],["Henderson County","Tennessee"],["Randolph County","West Virginia"],["Monroe County","Georgia"],["Peach County","Georgia"],["Logan County","Illinois"],["Scott County","Mississippi"],["White County","Georgia"],["Hocking County","Ohio"],["Tate County","Mississippi"],["Currituck County","North Carolina"],["Montgomery County","Kentucky"],["Wells County","Indiana"],["Washington County","Indiana"],["Grant County","New Mexico"],["Baker County","Florida"],["Carroll County","Arkansas"],["Dunklin County","Missouri"],["Montgomery County","Illinois"],["Wythe County","Virginia"],["Dillon County","South Carolina"],["Bradford County","Florida"],["Codington County","South Dakota"],["Leflore County","Mississippi"],["Jones County","Georgia"],["Copiah County","Mississippi"],["Palo Pinto County","Texas"],["Lincoln County","Wisconsin"],["Sanpete County","Utah"],["Carroll County","Tennessee"],["Cass County","Texas"],["Perry County","Kentucky"],["Custer County","Oklahoma"],["Marion County","Missouri"],["Elmore County","Idaho"],["Stoddard County","Missouri"],["Le Sueur County","Minnesota"],["Cherokee County","North Carolina"],["Jasper County","South Carolina"],["Garrett County","Maryland"],["Marion County","Tennessee"],["Pine County","Minnesota"],["Alpena County","Michigan"],["Glenn County","California"],["Van Wert County","Ohio"],["Ellis County","Kansas"],["Fayette County","Ohio"],["Ripley County","Indiana"],["Mason County","Michigan"],["Neshoba County","Mississippi"],["Hancock County","West Virginia"],["Morgan County","Colorado"],["Marion County","South Carolina"],["Gallia County","Ohio"],["Grimes County","Texas"],["Orange County","Vermont"],["Marion County","Alabama"],["Decatur County","Georgia"],["Franklin County","Maine"],["Adams County","Mississippi"],["Bladen County","North Carolina"],["Sumter County","Georgia"],["Park County","Wyoming"],["Schoharie County","New York"],["Smyth County","Virginia"],["Meade County","South Dakota"],["Haralson County","Georgia"],["Meade County","Kentucky"],["Cass County","Minnesota"],["Door County","Wisconsin"],["Madison County","Georgia"],["Wayne County","Georgia"],["Randolph County","Illinois"],["Austin County","Texas"],["Knox County","Kentucky"],["McPherson County","Kansas"],["Caledonia County","Vermont"],["Iberville Parish","Louisiana"],["Ottawa County","Oklahoma"],["Mecklenburg County","Virginia"],["Powhatan County","Virginia"],["Giles County","Tennessee"],["Marshall County","West Virginia"],["Boyle County","Kentucky"],["Hardin County","Ohio"],["Vernon County","Wisconsin"],["Trempealeau County","Wisconsin"],["Obion County","Tennessee"],["Greene County","Indiana"],["McCurtain County","Oklahoma"],["Clare County","Michigan"],["Caroline County","Virginia"],["Jefferson County","Idaho"],["Freeborn County","Minnesota"],["Sheridan County","Wyoming"],["Muhlenberg County","Kentucky"],["Wabash County","Indiana"],["Bolivar County","Mississippi"],["Elk County","Pennsylvania"],["Williamsburg County","South Carolina"],["Kleberg County","Texas"],["Bee County","Texas"],["Summit County","Colorado"],["Stone County","Missouri"],["Washington County","Maine"],["Lake County","Montana"],["Clarendon County","South Carolina"],["Pontotoc County","Mississippi"],["Polk County","Minnesota"],["Delta County","Colorado"],["Adams County","Nebraska"],["Titus County","Texas"],["Coos County","New Hampshire"],["Amherst County","Virginia"],["Gilmer County","Georgia"],["Huron County","Michigan"],["Montgomery County","Kansas"],["Polk County","Missouri"],["Malheur County","Oregon"],["Marshall County","Kentucky"],["Claiborne County","Tennessee"],["Franklin County","Alabama"],["Lyon County","Kansas"],["Henry County","Tennessee"],["Jefferson Davis Parish","Louisiana"],["Jefferson Davis Parish","Louisiana"],["Chester County","South Carolina"],["Evangeline Parish","Louisiana"],["Hale County","Texas"],["Dorchester County","Maryland"],["Logan County","West Virginia"],["Jackson County","Ohio"],["Lassen County","California"],["Rhea County","Tennessee"],["Weakley County","Tennessee"],["Morgan County","Illinois"],["Jasper County","Indiana"],["Jefferson County","Washington"],["Greenbrier County","West Virginia"],["Jasper County","Texas"],["Lafayette County","Missouri"],["Transylvania County","North Carolina"],["Pike County","Alabama"],["Gibson County","Indiana"],["Hot Spring County","Arkansas"],["Lawrence County","Alabama"],["Jefferson County","Indiana"],["Lee County","Georgia"],["Clinton County","Indiana"],["Panola County","Mississippi"],["Pickens County","Georgia"],["Bureau County","Illinois"],["Morton County","North Dakota"],["Caroline County","Maryland"],["Daviess County","Indiana"],["Accomack County","Virginia"],["Marion County","Iowa"],["Lincoln County","Oklahoma"],["Lumpkin County","Georgia"],["Lee County","Iowa"],["Botetourt County","Virginia"],["Fulton County","Illinois"],["Stark County","North Dakota"],["Wexford County","Michigan"],["Marshall County","Mississippi"],["Wakulla County","Florida"],["Pulaski County","Virginia"],["Seneca County","New York"],["DeSoto County","Florida"],["Morrison County","Minnesota"],["Halifax County","Virginia"],["Harvey County","Kansas"],["Christian County","Illinois"],["Emmet County","Michigan"],["Lee County","Illinois"],["Scotland County","North Carolina"],["Monroe County","Mississippi"],["Whitley County","Indiana"],["Miami County","Kansas"],["Preston County","West Virginia"],["Ford County","Kansas"],["Platte County","Nebraska"],["Marshall County","Tennessee"],["Brookings County","South Dakota"],["Steuben County","Indiana"],["Putnam County","Ohio"],["Nicollet County","Minnesota"],["Taos County","New Mexico"],["Barry County","Missouri"],["Cowley County","Kansas"],["Clark County","Wisconsin"],["Harris County","Georgia"],["Effingham County","Illinois"],["Lincoln County","Nebraska"],["Alcorn County","Mississippi"],["Chambers County","Alabama"],["Wasatch County","Utah"],["Howard County","Texas"],["Lincoln County","Mississippi"],["Morrow County","Ohio"],["Monroe County","Illinois"],["Silver Bow County","Montana"],["Becker County","Minnesota"],["Lincoln County","Maine"],["Lincoln County","Tennessee"],["Perry County","Ohio"],["Wapello County","Iowa"],["Warren County","Missouri"],["Madison County","Nebraska"],["Uintah County","Utah"],["Fannin County","Texas"],["Washington County","Texas"],["Adams County","Indiana"],["Livingston County","Illinois"],["Sioux County","Iowa"],["Hill County","Texas"],["Floyd County","Kentucky"],["Greene County","Pennsylvania"],["Miami County","Indiana"],["Greenup County","Kentucky"],["Cocke County","Tennessee"],["Laclede County","Missouri"],["Scotts Bluff County","Nebraska"],["Carlton County","Minnesota"],["Ware County","Georgia"],["Orange County","Virginia"],["Matagorda County","Texas"],["Knox County","Indiana"],["Alexander County","North Carolina"],["Beauregard Parish","Louisiana"],["Coshocton County","Ohio"],["Graves County","Kentucky"],["Huntington County","Indiana"],["Sagadahoc County","Maine"],["Okmulgee County","Oklahoma"],["Whitley County","Kentucky"],["Putnam County","Indiana"],["Geary County","Kansas"],["Escambia County","Alabama"],["McLeod County","Minnesota"],["Chippewa County","Michigan"],["Hopkins County","Texas"],["Dyer County","Tennessee"],["Clinton County","Illinois"],["Delta County","Michigan"],["Dare County","North Carolina"],["Webster Parish","Louisiana"],["Clark County","Kentucky"],["Webster County","Iowa"],["Macon County","North Carolina"],["Albany County","Wyoming"],["Green County","Wisconsin"],["Green County","Wisconsin"],["Williams County","Ohio"],["Calloway County","Kentucky"],["Jefferson County","Illinois"],["Dodge County","Nebraska"],["Yadkin County","North Carolina"],["Clarion County","Pennsylvania"],["Bennington County","Vermont"],["Houghton County","Michigan"],["Addison County","Vermont"],["Boone County","Arkansas"],["Essex County","New York"],["Steele County","Minnesota"],["Clinton County","Pennsylvania"],["Natchitoches Parish","Louisiana"],["Talbot County","Maryland"],["Covington County","Alabama"],["Louisa County","Virginia"],["Newberry County","South Carolina"],["Marion County","Illinois"],["Franklin County","Illinois"],["Jasper County","Iowa"],["Oneida County","Wisconsin"],["Cass County","Indiana"],["Montgomery County","Indiana"],["Independence County","Arkansas"],["Lawrence County","Missouri"],["Scott County","Missouri"],["Pontotoc County","Oklahoma"],["Brown County","Texas"],["Defiance County","Ohio"],["Brown County","South Dakota"],["Susquehanna County","Pennsylvania"],["Guernsey County","Ohio"],["Dallas County","Alabama"],["Woodford County","Illinois"],["Finney County","Kansas"],["Graham County","Arizona"],["Warren County","Pennsylvania"],["Colleton County","South Carolina"],["Isle of Wight County","Virginia"],["Gloucester County","Virginia"],["Champaign County","Ohio"],["Jim Wells County","Texas"],["Jim Wells County","Texas"],["Des Moines County","Iowa"],["Oconto County","Wisconsin"],["Crawford County","Kansas"],["Wayne County","West Virginia"],["Douglas County","Minnesota"],["Mayes County","Oklahoma"],["Union County","Arkansas"],["Webster County","Missouri"],["Person County","North Carolina"],["Fremont County","Wyoming"],["Campbell County","Tennessee"],["Sequoyah County","Oklahoma"],["Latah County","Idaho"],["Waldo County","Maine"],["Hendry County","Florida"],["Okeechobee County","Florida"],["Harrison County","Indiana"],["Avoyelles Parish","Louisiana"],["Mecosta County","Michigan"],["Snyder County","Pennsylvania"],["Howell County","Missouri"],["Murray County","Georgia"],["Mower County","Minnesota"],["Marshall County","Iowa"],["Pike County","Mississippi"],["Orleans County","New York"],["Rio Arriba County","New Mexico"],["Ottawa County","Ohio"],["Delaware County","Oklahoma"],["Tazewell County","Virginia"],["McKean County","Pennsylvania"],["Amador County","California"],["Fayette County","West Virginia"],["Wyoming County","New York"],["Pasquotank County","North Carolina"],["Knox County","Maine"],["Sanilac County","Michigan"],["Mississippi County","Arkansas"],["Warren County","Virginia"],["Shawano County","Wisconsin"],["Upshur County","Texas"],["Williams County","North Dakota"],["Warren County","Tennessee"],["Preble County","Ohio"],["Tioga County","Pennsylvania"],["Clatsop County","Oregon"],["Cheatham County","Tennessee"],["Isanti County","Minnesota"],["Tallapoosa County","Alabama"],["Tift County","Georgia"],["Benton County","Minnesota"],["Wharton County","Texas"],["Baxter County","Arkansas"],["McClain County","Oklahoma"],["Cooke County","Texas"],["Gratiot County","Michigan"],["Oconee County","Georgia"],["Marinette County","Wisconsin"],["Fayette County","Tennessee"],["Clinton County","Ohio"],["Crawford County","Ohio"],["Nez Perce County","Idaho"],["Okanogan County","Washington"],["Butler County","Missouri"],["Pierce County","Wisconsin"],["Sweetwater County","Wyoming"],["Summit County","Utah"],["Ohio County","West Virginia"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["Mercer County","Ohio"],["Erath County","Texas"],["Vance County","North Carolina"],["Miller County","Arkansas"],["Montrose County","Colorado"],["Union County","Pennsylvania"],["Davie County","North Carolina"],["Fulton County","Ohio"],["Camden County","Missouri"],["Franklin County","Tennessee"],["Stephens County","Oklahoma"],["Polk County","Georgia"],["Levy County","Florida"],["Douglas County","Washington"],["Richmond County","North Carolina"],["Pettis County","Missouri"],["Prince George County","Virginia"],["Sullivan County","New Hampshire"],["Coffee County","Georgia"],["Jackson County","North Carolina"],["Cerro Gordo County","Iowa"],["Muscatine County","Iowa"],["DeKalb County","Indiana"],["Chesterfield County","South Carolina"],["Highland County","Ohio"],["Suwannee County","Florida"],["Dubois County","Indiana"],["Brown County","Ohio"],["Kay County","Oklahoma"],["Kandiyohi County","Minnesota"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["Pittsburg County","Oklahoma"],["Baldwin County","Georgia"],["Madison County","Ohio"],["Gadsden County","Florida"],["Siskiyou County","California"],["Huntingdon County","Pennsylvania"],["Lawrence County","Tennessee"],["Ravalli County","Montana"],["Shenandoah County","Virginia"],["Holmes County","Ohio"],["Kendall County","Texas"],["Callaway County","Missouri"],["Douglas County","Wisconsin"],["Delaware County","New York"],["Kittitas County","Washington"],["Barren County","Kentucky"],["Jefferson County","Pennsylvania"],["Stokes County","North Carolina"],["McDowell County","North Carolina"],["Stephenson County","Illinois"],["Phelps County","Missouri"],["Beaufort County","North Carolina"],["Warren County","Mississippi"],["Bryan County","Georgia"],["Henderson County","Kentucky"],["Wood County","Texas"],["Branch County","Michigan"],["Washington County","Mississippi"],["Macoupin County","Illinois"],["Polk County","Wisconsin"],["Lawrence County","Indiana"],["Chilton County","Alabama"],["Itasca County","Minnesota"],["Shelby County","Indiana"],["Calaveras County","California"],["Hopkins County","Kentucky"],["Dunn County","Wisconsin"],["Washington Parish","Louisiana"],["Greene County","Arkansas"],["Hillsdale County","Michigan"],["Thomas County","Georgia"],["Osage County","Oklahoma"],["Perry County","Pennsylvania"],["Caldwell County","Texas"],["Colquitt County","Georgia"],["Windham County","Vermont"],["Habersham County","Georgia"],["Hancock County","Mississippi"],["Bryan County","Oklahoma"],["Marshall County","Indiana"],["Mifflin County","Pennsylvania"],["Logan County","Ohio"],["Beltrami County","Minnesota"],["Monroe County","Tennessee"],["Monroe County","Wisconsin"],["Auglaize County","Ohio"],["Jackson County","Indiana"],["Stevens County","Washington"],["Allegany County","New York"],["Clinton County","Iowa"],["Chambers County","Texas"],["Barron County","Wisconsin"],["Nelson County","Kentucky"],["Cortland County","New York"],["Coles County","Illinois"],["Campbell County","Wyoming"],["Cherokee County","Oklahoma"],["Bonner County","Idaho"],["Chenango County","New York"],["Jackson County","Florida"],["Noble County","Indiana"],["Franklin County","New York"],["Bedford County","Pennsylvania"],["Goodhue County","Minnesota"],["Val Verde County","Texas"],["Santa Cruz County","Arizona"],["Greene County","New York"],["Whitman County","Washington"],["Bingham County","Idaho"],["Carter County","Oklahoma"],["Shelby County","Kentucky"],["Le Flore County","Oklahoma"],["Crittenden County","Arkansas"],["Shelby County","Ohio"],["Boyd County","Kentucky"],["Lincoln Parish","Louisiana"],["Curry County","New Mexico"],["Tioga County","New York"],["Halifax County","North Carolina"],["Duplin County","North Carolina"],["Vernon Parish","Louisiana"],["Edgecombe County","North Carolina"],["Henry County","Indiana"],["Fremont County","Colorado"],["Atascosa County","Texas"],["Burnet County","Texas"],["Henry County","Illinois"],["Dale County","Alabama"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["Douglas County","Nevada"],["Montgomery County","New York"],["Logan County","Oklahoma"],["Laurens County","Georgia"],["Winona County","Minnesota"],["Wilson County","Texas"],["Queen Anne's County","Maryland"],["Franklin County","Vermont"],["Knox County","Illinois"],["Newaygo County","Michigan"],["Buffalo County","Nebraska"],["Lamar County","Texas"],["Carroll County","New Hampshire"],["Polk County","Texas"],["Bedford County","Tennessee"],["Lincoln County","Oregon"],["Cherokee County","Texas"],["Gibson County","Tennessee"],["Venango County","Pennsylvania"],["Somerset County","Maine"],["Columbus County","North Carolina"],["Dearborn County","Indiana"],["Medina County","Texas"],["Bristol County","Rhode Island"],["Wayne County","Pennsylvania"],["Franklin County","Kentucky"],["Cass County","Michigan"],["Nye County","Nevada"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["Ogle County","Illinois"],["Oktibbeha County","Mississippi"],["Waupaca County","Wisconsin"],["Darke County","Ohio"],["Grant County","Wisconsin"],["Hoke County","North Carolina"],["Rusk County","Texas"],["Warren County","Iowa"],["Calumet County","Wisconsin"],["Ashland County","Ohio"],["Washington County","Oklahoma"],["Worcester County","Maryland"],["Grundy County","Illinois"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["Culpeper County","Virginia"],["Jackson County","Alabama"],["Columbia County","Oregon"],["Kerr County","Texas"],["Navarro County","Texas"],["Madison County","Idaho"],["Jackson County","Illinois"],["Jessamine County","Kentucky"],["Gila County","Arizona"],["McMinn County","Tennessee"],["Tuscola County","Michigan"],["Fulton County","New York"],["Roane County","Tennessee"],["Boone County","Illinois"],["Coffee County","Alabama"],["Elko County","Nevada"],["Pulaski County","Missouri"],["Johnson County","Missouri"],["Watauga County","North Carolina"],["Saline County","Kansas"],["Dickson County","Tennessee"],["Franklin County","Virginia"],["Jefferson County","Tennessee"],["Camden County","Georgia"],["Grady County","Oklahoma"],["Loudon County","Tennessee"],["Seneca County","Ohio"],["Lenoir County","North Carolina"],["Hancock County","Maine"],["Tuolumne County","California"],["La Plata County","Colorado"],["Whiteside County","Illinois"],["Eagle County","Colorado"],["Lafayette County","Mississippi"],["Taney County","Missouri"],["Pearl River County","Mississippi"],["Marion County","West Virginia"],["Cherokee County","South Carolina"],["Hardin County","Texas"],["Carter County","Tennessee"],["Chisago County","Minnesota"],["Hawkins County","Tennessee"],["Waller County","Texas"],["Scott County","Kentucky"],["Colbert County","Alabama"],["Iron County","Utah"],["Vermilion Parish","Louisiana"],["Putnam County","West Virginia"],["Gordon County","Georgia"],["Acadia Parish","Louisiana"],["Box Elder County","Utah"],["Jefferson County","West Virginia"],["Windsor County","Vermont"],["Oxford County","Maine"],["Maverick County","Texas"],["Coffee County","Tennessee"],["Anderson County","Texas"],["Lawrence County","Ohio"],["Genesee County","New York"],["Columbia County","Wisconsin"],["Otsego County","New York"],["Pike County","Pennsylvania"],["Pickaway County","Ohio"],["Huron County","Ohio"],["Carson City","Nevada"],["Newton County","Missouri"],["Pike County","Kentucky"],["Autauga County","Alabama"],["Lowndes County","Mississippi"],["Sandusky County","Ohio"],["Sampson County","North Carolina"],["Blount County","Alabama"],["Russell County","Alabama"],["Lyon County","Nevada"],["Van Zandt County","Texas"],["Lincoln County","Missouri"],["Mercer County","West Virginia"],["Washington County","Ohio"],["Washington County","Vermont"],["Bradford County","Pennsylvania"],["Otter Tail County","Minnesota"],["Crawford County","Arkansas"],["Herkimer County","New York"],["Pender County","North Carolina"],["Rutland County","Vermont"],["St. Joseph County","Michigan"],["St. Joseph County","Michigan"],["Tipton County","Tennessee"],["Granville County","North Carolina"],["Cumberland County","Tennessee"],["Washington County","New York"],["Columbia County","New York"],["Hood County","Texas"],["Garfield County","Colorado"],["Livingston County","New York"],["Reno County","Kansas"],["Haywood County","North Carolina"],["Eddy County","New Mexico"],["Barry County","Michigan"],["Athens County","Ohio"],["Stanly County","North Carolina"],["Walla Walla County","Washington"],["Laurel County","Kentucky"],["Knox County","Ohio"],["Union County","Ohio"],["Garfield County","Oklahoma"],["Hall County","Nebraska"],["Darlington County","South Carolina"],["Lee County","North Carolina"],["Pope County","Arkansas"],["Georgetown County","South Carolina"],["Belknap County","New Hampshire"],["Warrick County","Indiana"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["Lamar County","Mississippi"],["Isabella County","Michigan"],["Rutherford County","North Carolina"],["Hamblen County","Tennessee"],["Nacogdoches County","Texas"],["Columbia County","Pennsylvania"],["Carbon County","Pennsylvania"],["Effingham County","Georgia"],["Salem County","New Jersey"],["Coos County","Oregon"],["Pulaski County","Kentucky"],["Chaves County","New Mexico"],["Lincoln County","South Dakota"],["Jefferson County","Ohio"],["Liberty County","Georgia"],["Clay County","Minnesota"],["Walker County","Alabama"],["Marion County","Ohio"],["Kershaw County","South Carolina"],["Armstrong County","Pennsylvania"],["Mason County","Washington"],["Adams County","Illinois"],["Warren County","New York"],["Sauk County","Wisconsin"],["Tehama County","California"],["Starr County","Texas"],["Harrison County","West Virginia"],["Wilkes County","North Carolina"],["Marquette County","Michigan"],["Apache County","Arizona"],["Crow Wing County","Minnesota"],["Chippewa County","Wisconsin"],["Muskogee County","Oklahoma"],["Belmont County","Ohio"],["Wayne County","Indiana"],["Montcalm County","Michigan"],["Grant County","Indiana"],["Ionia County","Michigan"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["Rice County","Minnesota"],["Aroostook County","Maine"],["Williamson County","Illinois"],["Jones County","Mississippi"],["Jefferson County","Arkansas"],["Spalding County","Georgia"],["Butler County","Kansas"],["Laurens County","South Carolina"],["Oldham County","Kentucky"],["Walker County","Georgia"],["Carteret County","North Carolina"],["Otero County","New Mexico"],["Catoosa County","Georgia"],["McCracken County","Kentucky"],["Madison County","New York"],["Shiawassee County","Michigan"],["Allegany County","Maryland"],["Lake County","California"],["Franklin County","North Carolina"],["Wise County","Texas"],["San Patricio County","Texas"],["San Patricio County","Texas"],["San Patricio County","Texas"],["San Patricio County","Texas"],["Harrison County","Texas"],["Blue Earth County","Minnesota"],["Greenwood County","South Carolina"],["Klamath County","Oregon"],["Troup County","Georgia"],["Columbia County","Florida"],["Ward County","North Dakota"],["Iberia Parish","Louisiana"],["Greene County","Tennessee"],["Portage County","Wisconsin"],["Boone County","Indiana"],["Lewis and Clark County","Montana"],["Franklin County","Massachusetts"],["Surry County","North Carolina"],["DeKalb County","Alabama"],["Creek County","Oklahoma"],["Morgan County","Indiana"],["Riley County","Kansas"],["Pottawatomie County","Oklahoma"],["Tooele County","Utah"],["Christian County","Kentucky"],["Robertson County","Tennessee"],["McKinley County","New Mexico"],["Fauquier County","Virginia"],["Lauderdale County","Mississippi"],["Grand Forks County","North Dakota"],["Kauai County","Hawaii"],["Putnam County","Florida"],["Scioto County","Ohio"],["Lonoke County","Arkansas"],["Broomfield County","Colorado"],["Somerset County","Pennsylvania"],["Vermilion County","Illinois"],["Wood County","Wisconsin"],["Lea County","New Mexico"],["Raleigh County","West Virginia"],["Hancock County","Ohio"],["Walton County","Florida"],["Van Buren County","Michigan"],["Erie County","Ohio"],["Grays Harbor County","Washington"],["Jackson County","Georgia"],["Valencia County","New Mexico"],["Cayuga County","New York"],["Chatham County","North Carolina"],["Walker County","Texas"],["Cheshire County","New Hampshire"],["White County","Arkansas"],["Cattaraugus County","New York"],["Ross County","Ohio"],["Anderson County","Tennessee"],["Clallam County","Washington"],["Cole County","Missouri"],["Forrest County","Mississippi"],["Oconee County","South Carolina"],["Sullivan County","New York"],["Wilson County","North Carolina"],["Chelan County","Washington"],["Clinton County","Michigan"],["Bedford County","Virginia"],["Hancock County","Indiana"],["Clinton County","New York"],["Putnam County","Tennessee"],["Natrona County","Wyoming"],["Umatilla County","Oregon"],["Kosciusko County","Indiana"],["Floyd County","Indiana"],["Clearfield County","Pennsylvania"],["Caldwell County","North Carolina"],["Wagoner County","Oklahoma"],["Bulloch County","Georgia"],["Manitowoc County","Wisconsin"],["Yuba County","California"],["Payne County","Oklahoma"],["Cape Girardeau County","Missouri"],["Leavenworth County","Kansas"],["Talladega County","Alabama"],["Lewis County","Washington"],["Henderson County","Texas"],["Bartholomew County","Indiana"],["Bullitt County","Kentucky"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["Monroe County","Florida"],["Coryell County","Texas"],["Indiana County","Pennsylvania"],["Lee County","Mississippi"],["Midland County","Michigan"],["Barrow County","Georgia"],["Howard County","Indiana"],["Crawford County","Pennsylvania"],["Chemung County","New York"],["Orangeburg County","South Carolina"],["Wood County","West Virginia"],["Cascade County","Montana"],["Glynn County","Georgia"],["Buchanan County","Missouri"],["Orange County","Texas"],["Jefferson County","Wisconsin"],["Newport County","Rhode Island"],["Dougherty County","Georgia"],["Lawrence County","Pennsylvania"],["Angelina County","Texas"],["Muskingum County","Ohio"],["Lincoln County","North Carolina"],["Island County","Washington"],["Bannock County","Idaho"],["Polk County","Oregon"],["Burke County","North Carolina"],["Cullman County","Alabama"],["Elmore County","Alabama"],["Josephine County","Oregon"],["Lapeer County","Michigan"],["Christian County","Missouri"],["Dodge County","Wisconsin"],["Twin Falls County","Idaho"],["Nassau County","Florida"],["Rockingham County","North Carolina"],["St. Clair County","Alabama"],["Grafton County","New Hampshire"],["Wayne County","New York"],["Victoria County","Texas"],["Ozaukee County","Wisconsin"],["Mendocino County","California"],["Liberty County","Texas"],["Northumberland County","Pennsylvania"],["Madison County","Kentucky"],["Calvert County","Maryland"],["Bowie County","Texas"],["Campbell County","Kentucky"],["Tuscarawas County","Ohio"],["St. Croix County","Wisconsin"],["Lauderdale County","Alabama"],["Rockdale County","Georgia"],["Steuben County","New York"],["Pottawattamie County","Iowa"],["Cabell County","West Virginia"],["Nash County","North Carolina"],["Benton County","Oregon"],["Grand Traverse County","Michigan"],["Rogers County","Oklahoma"],["Cape May County","New Jersey"],["Geauga County","Ohio"],["Lancaster County","South Carolina"],["Walton County","Georgia"],["Franklin County","Washington"],["Sherburne County","Minnesota"],["Bastrop County","Texas"],["Lafourche Parish","Louisiana"],["Ashtabula County","Ohio"],["Marshall County","Alabama"],["Putnam County","New York"],["Sevier County","Tennessee"],["Burleigh County","North Dakota"],["Story County","Iowa"],["Floyd County","Georgia"],["Madison County","Tennessee"],["Grant County","Washington"],["Dubuque County","Iowa"],["Lenawee County","Michigan"],["Cleveland County","North Carolina"],["Sutter County","California"],["Dallas County","Iowa"],["Moore County","North Carolina"],["Hunt County","Texas"],["Garland County","Arkansas"],["DeKalb County","Illinois"],["Laramie County","Wyoming"],["Craven County","North Carolina"],["Maury County","Tennessee"],["Highlands County","Florida"],["Columbiana County","Ohio"],["Allen County","Ohio"],["Nevada County","California"],["Whitfield County","Georgia"],["Daviess County","Kentucky"],["Etowah County","Alabama"],["Limestone County","Alabama"],["Wicomico County","Maryland"],["Cecil County","Maryland"],["Adams County","Pennsylvania"],["Bay County","Michigan"],["Macon County","Illinois"],["Fond du Lac County","Wisconsin"],["Flathead County","Montana"],["Franklin County","Missouri"],["Sumter County","South Carolina"],["Eau Claire County","Wisconsin"],["Tompkins County","New York"],["Monongalia County","West Virginia"],["Woodbury County","Iowa"],["Vigo County","Indiana"],["Walworth County","Wisconsin"],["Navajo County","Arizona"],["Platte County","Missouri"],["Carver County","Minnesota"],["Houston County","Alabama"],["Kankakee County","Illinois"],["Yamhill County","Oregon"],["Rockwall County","Texas"],["Cass County","Missouri"],["St. Lawrence County","New York"],["Bradley County","Tennessee"],["Miami County","Ohio"],["Bartow County","Georgia"],["Madison County","Mississippi"],["Eaton County","Michigan"],["Pennington County","South Dakota"],["Terrebonne Parish","Louisiana"],["Warren County","New Jersey"],["LaSalle County","Illinois"],["Hanover County","Virginia"],["Mercer County","Pennsylvania"],["Hardin County","Kentucky"],["Cowlitz County","Washington"],["Androscoggin County","Maine"],["Douglas County","Oregon"],["Craighead County","Arkansas"],["Delaware County","Indiana"],["LaPorte County","Indiana"],["Ontario County","New York"],["Newton County","Georgia"],["St. Mary's County","Maryland"],["Lycoming County","Pennsylvania"],["Flagler County","Florida"],["Henderson County","North Carolina"],["Windham County","Connecticut"],["Calhoun County","Alabama"],["Robeson County","North Carolina"],["Jefferson County","New York"],["Wayne County","Ohio"],["Wayne County","North Carolina"],["Oswego County","New York"],["Missoula County","Montana"],["Sheboygan County","Wisconsin"],["Lowndes County","Georgia"],["Potter County","Texas"],["Douglas County","Kansas"],["Gallatin County","Montana"],["Carroll County","Georgia"],["Fayette County","Georgia"],["Tom Green County","Texas"],["Allegan County","Michigan"],["La Crosse County","Wisconsin"],["Clark County","Indiana"],["Comanche County","Oklahoma"],["San Juan County","New Mexico"],["San Juan County","New Mexico"],["Berkeley County","West Virginia"],["Jasper County","Missouri"],["Blair County","Pennsylvania"],["Saline County","Arkansas"],["Morgan County","Alabama"],["Faulkner County","Arkansas"],["Kennebec County","Maine"],["Bonneville County","Idaho"],["Gregg County","Texas"],["Richland County","Ohio"],["Cochise County","Arizona"],["Ascension Parish","Louisiana"],["Chautauqua County","New York"],["Sebastian County","Arkansas"],["Linn County","Oregon"],["Clarke County","Georgia"],["Bossier Parish","Louisiana"],["Fayette County","Pennsylvania"],["Hunterdon County","New Jersey"],["Berkshire County","Massachusetts"],["Wichita County","Texas"],["Skagit County","Washington"],["Sumter County","Florida"],["Washington County","Rhode Island"],["Rapides Parish","Louisiana"],["Madison County","Indiana"],["Strafford County","New Hampshire"],["Black Hawk County","Iowa"],["Tazewell County","Illinois"],["Pickens County","South Carolina"],["Kendall County","Illinois"],["Wood County","Ohio"],["Washington County","Tennessee"],["Cache County","Utah"],["Tangipahoa Parish","Louisiana"],["Cambria County","Pennsylvania"],["Harnett County","North Carolina"],["Calhoun County","Michigan"],["Warren County","Kentucky"],["Blount County","Tennessee"],["Grayson County","Texas"],["Boone County","Kentucky"],["Clark County","Ohio"],["Humboldt County","California"],["Brunswick County","North Carolina"],["Washington County","Wisconsin"],["Florence County","South Carolina"],["Marathon County","Wisconsin"],["Napa County","California"],["Monroe County","Indiana"],["Randall County","Texas"],["Wright County","Minnesota"],["Livingston Parish","Louisiana"],["Schuylkill County","Pennsylvania"],["Taylor County","Texas"],["Jackson County","Mississippi"],["Lebanon County","Pennsylvania"],["Randolph County","North Carolina"],["Sussex County","New Jersey"],["Douglas County","Georgia"],["Rock Island County","Illinois"],["Coconino County","Arizona"],["Kaufman County","Texas"],["Coweta County","Georgia"],["Rowan County","North Carolina"],["Wilson County","Tennessee"],["Parker County","Texas"],["Orange County","North Carolina"],["Sandoval County","New Mexico"],["Tolland County","Connecticut"],["Scott County","Minnesota"],["Penobscot County","Maine"],["Kings County","California"],["Johnson County","Iowa"],["Merrimack County","New Hampshire"],["Citrus County","Florida"],["Cumberland County","New Jersey"],["Berrien County","Michigan"],["Canadian County","Oklahoma"],["Washington County","Maryland"],["Monroe County","Michigan"],["Santa Fe County","New Mexico"],["Mesa County","Colorado"],["Franklin County","Pennsylvania"],["Columbia County","Georgia"],["Madera County","California"],["Stafford County","Virginia"],["Rankin County","Mississippi"],["Bibb County","Georgia"],["Schenectady County","New York"],["Sullivan County","Tennessee"],["Centre County","Pennsylvania"],["Stearns County","Minnesota"],["Martin County","Florida"],["Fairfield County","Ohio"],["Indian River County","Florida"],["Jackson County","Michigan"],["Ouachita Parish","Louisiana"],["St. Clair County","Michigan"],["St. Clair County","Michigan"],["Catawba County","North Carolina"],["Rensselaer County","New York"],["Comal County","Texas"],["Dorchester County","South Carolina"],["Johnson County","Indiana"],["Portage County","Ohio"],["Hampshire County","Massachusetts"],["Olmsted County","Minnesota"],["Houston County","Georgia"],["Rock County","Wisconsin"],["Middlesex County","Connecticut"],["Yellowstone County","Montana"],["Maui County","Hawaii"],["Ector County","Texas"],["Charles County","Maryland"],["Greene County","Ohio"],["Pueblo County","Colorado"],["Beaver County","Pennsylvania"],["Chittenden County","Vermont"],["Monroe County","Pennsylvania"],["Paulding County","Georgia"],["Aiken County","South Carolina"],["Davidson County","North Carolina"],["Kenton County","Kentucky"],["Kenosha County","Wisconsin"],["Wyandotte County","Kansas"],["Midland County","Texas"],["Pitt County","North Carolina"],["Kent County","Rhode Island"],["McLean County","Illinois"],["Kootenai County","Idaho"],["Alamance County","North Carolina"],["Winnebago County","Wisconsin"],["Guadalupe County","Texas"],["Carroll County","Maryland"],["Porter County","Indiana"],["Lee County","Alabama"],["Scott County","Iowa"],["Hendricks County","Indiana"],["Bay County","Florida"],["Muskegon County","Michigan"],["Licking County","Ohio"],["Shawnee County","Kansas"],["Imperial County","California"],["Johnson County","Texas"],["Vanderburgh County","Indiana"],["Washington County","Utah"],["Kanawha County","West Virginia"],["Peoria County","Illinois"],["Kent County","Delaware"],["Ulster County","New York"],["Shasta County","California"],["Medina County","Ohio"],["Boone County","Missouri"],["Cass County","North Dakota"],["Litchfield County","Connecticut"],["DeSoto County","Mississippi"],["Tippecanoe County","Indiana"],["Iredell County","North Carolina"],["Charlotte County","Florida"],["Beaufort County","South Carolina"],["Santa Rosa County","Florida"],["Saginaw County","Michigan"],["Sarpy County","Nebraska"],["Outagamie County","Wisconsin"],["El Dorado County","California"],["Ellis County","Texas"],["Butler County","Pennsylvania"],["Livingston County","Michigan"],["Hernando County","Florida"],["Sumner County","Tennessee"],["Sangamon County","Illinois"],["Minnehaha County","South Dakota"],["Racine County","Wisconsin"],["Deschutes County","Oregon"],["Broome County","New York"],["St. Louis County","Minnesota"],["Trumbull County","Ohio"],["Hall County","Georgia"],["Anderson County","South Carolina"],["Yuma County","Arizona"],["Onslow County","North Carolina"],["Champaign County","Illinois"],["Richmond County","Georgia"],["Benton County","Washington"],["Muscogee County","Georgia"],["Elkhart County","Indiana"],["Clermont County","Ohio"],["Harrison County","Mississippi"],["Washington County","Pennsylvania"],["Butte County","California"],["Okaloosa County","Florida"],["York County","Maine"],["Niagara County","New York"],["Mohave County","Arizona"],["Delaware County","Ohio"],["Lackawanna County","Pennsylvania"],["Johnston County","North Carolina"],["Yolo County","California"],["Calcasieu Parish","Louisiana"],["Clay County","Florida"],["Montgomery County","Tennessee"],["Shelby County","Alabama"],["Jackson County","Oregon"],["New Hanover County","North Carolina"],["Cabarrus County","North Carolina"],["Richmond city","Virginia"],["Jefferson County","Missouri"],["Whatcom County","Washington"],["Tuscaloosa County","Alabama"],["Hinds County","Mississippi"],["Gaston County","North Carolina"],["Mahoning County","Ohio"],["Montgomery County","Alabama"],["Barnstable County","Massachusetts"],["Berkeley County","South Carolina"],["Linn County","Iowa"],["Canyon County","Idaho"],["Baldwin County","Alabama"],["Oneida County","New York"],["Lake County","Ohio"],["Smith County","Texas"],["Brazos County","Texas"],["Saratoga County","New York"],["Yavapai County","Arizona"],["Sussex County","Delaware"],["Caddo Parish","Louisiana"],["Union County","North Carolina"],["Arlington County","Virginia"],["Henry County","Georgia"],["Hays County","Texas"],["Lafayette Parish","Louisiana"],["Warren County","Ohio"],["Washington County","Arkansas"],["Williamson County","Tennessee"],["Forsyth County","Georgia"],["Clay County","Missouri"],["Jefferson County","Texas"],["Yakima County","Washington"],["St. Clair County","Illinois"],["Cumberland County","Pennsylvania"],["McLennan County","Texas"],["Harford County","Maryland"],["Kalamazoo County","Michigan"],["Weber County","Utah"],["Marin County","California"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["Madison County","Illinois"],["Cherokee County","Georgia"],["Webb County","Texas"],["Washington County","Minnesota"],["New London County","Connecticut"],["New London County","Connecticut"],["Brown County","Wisconsin"],["Buncombe County","North Carolina"],["Santa Cruz County","California"],["Santa Cruz County","California"],["Santa Cruz County","California"],["Erie County","Pennsylvania"],["Frederick County","Maryland"],["St. Joseph County","Indiana"],["St. Johns County","Florida"],["St. Johns County","Florida"],["Atlantic County","New Jersey"],["Kitsap County","Washington"],["Alachua County","Florida"],["Merced County","California"],["York County","South Carolina"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["Benton County","Arkansas"],["Ingham County","Michigan"],["Winnebago County","Illinois"],["Dauphin County","Pennsylvania"],["Leon County","Florida"],["Lexington County","South Carolina"],["Thurston County","Washington"],["Chatham County","Georgia"],["Cleveland County","Oklahoma"],["Dutchess County","New York"],["Ottawa County","Michigan"],["Clayton County","Georgia"],["Greene County","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["Gloucester County","New Jersey"],["Cumberland County","Maine"],["McHenry County","Illinois"],["Lubbock County","Texas"],["Northampton County","Pennsylvania"],["Lorain County","Ohio"],["Rockingham County","New Hampshire"],["Albany County","New York"],["Escambia County","Florida"],["Fayette County","Kentucky"],["Lancaster County","Nebraska"],["Durham County","North Carolina"],["Luzerne County","Pennsylvania"],["Spartanburg County","South Carolina"],["Weld County","Colorado"],["St. Lucie County","Florida"],["St. Lucie County","Florida"],["Boulder County","Colorado"],["Howard County","Maryland"],["Henrico County","Virginia"],["Cumberland County","North Carolina"],["Rockland County","New York"],["Rutherford County","Tennessee"],["Somerset County","New Jersey"],["Marion County","Oregon"],["Hamilton County","Indiana"],["Galveston County","Texas"],["Horry County","South Carolina"],["Nueces County","Texas"],["Westmoreland County","Pennsylvania"],["Douglas County","Colorado"],["Larimer County","Colorado"],["Davis County","Utah"],["Anoka County","Minnesota"],["Chesterfield County","Virginia"],["Hamilton County","Tennessee"],["Bell County","Texas"],["Brazoria County","Texas"],["Washtenaw County","Michigan"],["Lehigh County","Pennsylvania"],["Stark County","Ohio"],["Collier County","Florida"],["Marion County","Florida"],["Forsyth County","North Carolina"],["Lane County","Oregon"],["Lake County","Florida"],["Orleans Parish","Louisiana"],["Allen County","Indiana"],["Mercer County","New Jersey"],["Madison County","Alabama"],["Osceola County","Florida"],["Butler County","Ohio"],["Pulaski County","Arkansas"],["Manatee County","Florida"],["Orange County","New York"],["Placer County","California"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["Genesee County","Michigan"],["Waukesha County","Wisconsin"],["Charleston County","South Carolina"],["Mobile County","Alabama"],["Richland County","South Carolina"],["Loudoun County","Virginia"],["Cameron County","Texas"],["Clackamas County","Oregon"],["Hillsborough County","New Hampshire"],["Pinal County","Arizona"],["Berks County","Pennsylvania"],["Lucas County","Ohio"],["Sarasota County","Florida"],["Monterey County","California"],["Dakota County","Minnesota"],["Jefferson Parish","Louisiana"],["Jefferson Parish","Louisiana"],["Santa Barbara County","California"],["Santa Barbara County","California"],["Santa Barbara County","California"],["Solano County","California"],["York County","Pennsylvania"],["East Baton Rouge Parish","Louisiana"],["East Baton Rouge Parish","Louisiana"],["East Baton Rouge Parish","Louisiana"],["Burlington County","New Jersey"],["Hampden County","Massachusetts"],["Seminole County","Florida"],["Tulare County","California"],["Onondaga County","New York"],["Knox County","Tennessee"],["Prince William County","Virginia"],["Washoe County","Nevada"],["Sonoma County","California"],["Polk County","Iowa"],["Ada County","Idaho"],["Richmond County","New York"],["Lake County","Indiana"],["Clark County","Washington"],["Morris County","New Jersey"],["Kane County","Illinois"],["Adams County","Colorado"],["Camden County","New Jersey"],["Sedgwick County","Kansas"],["Passaic County","New Jersey"],["Greenville County","South Carolina"],["Plymouth County","Massachusetts"],["Chester County","Pennsylvania"],["Montgomery County","Ohio"],["Spokane County","Washington"],["Summit County","Ohio"],["Guilford County","North Carolina"],["Ramsey County","Minnesota"],["Stanislaus County","California"],["Lancaster County","Pennsylvania"],["Volusia County","Florida"],["Dane County","Wisconsin"],["Pasco County","Florida"],["New Castle County","Delaware"],["Union County","New Jersey"],["Delaware County","Pennsylvania"],["Bristol County","Massachusetts"],["Jefferson County","Colorado"],["Douglas County","Nebraska"],["Baltimore city","Maryland"],["Baltimore city","Maryland"],["Anne Arundel County","Maryland"],["Washington County","Oregon"],["Brevard County","Florida"],["Williamson County","Texas"],["Johnson County","Kansas"],["Montgomery County","Texas"],["Ocean County","New Jersey"],["Monmouth County","New Jersey"],["Bucks County","Pennsylvania"],["Arapahoe County","Colorado"],["Kent County","Michigan"],["Providence County","Rhode Island"],["Tulsa County","Oklahoma"],["Jefferson County","Alabama"],["Bernalillo County","New Mexico"],["Will County","Illinois"],["Lake County","Illinois"],["Denver County","Colorado"],["Davidson County","Tennessee"],["Jackson County","Missouri"],["Hudson County","New Jersey"],["Polk County","Florida"],["Norfolk County","Massachusetts"],["El Paso County","Colorado"],["Monroe County","New York"],["Lee County","Florida"],["DeKalb County","Georgia"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["Cobb County","Georgia"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["Jefferson County","Kentucky"],["Suffolk County","Massachusetts"],["Essex County","Massachusetts"],["Multnomah County","Oregon"],["Fort Bend County","Texas"],["Snohomish County","Washington"],["Hamilton County","Ohio"],["Ventura County","California"],["Baltimore County","Maryland"],["Baltimore County","Maryland"],["Montgomery County","Pennsylvania"],["Worcester County","Massachusetts"],["Middlesex County","New Jersey"],["Essex County","New Jersey"],["New Haven County","Connecticut"],["New Haven County","Connecticut"],["El Paso County","Texas"],["Hidalgo County","Texas"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["Macomb County","Michigan"],["Hartford County","Connecticut"],["Denton County","Texas"],["Kern County","California"],["Pierce County","Washington"],["Shelby County","Tennessee"],["DuPage County","Illinois"],["Milwaukee County","Wisconsin"],["Erie County","New York"],["Bergen County","New Jersey"],["Gwinnett County","Georgia"],["Fairfield County","Connecticut"],["Pinellas County","Florida"],["Prince George's County","Maryland"],["Marion County","Indiana"],["Duval County","Florida"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["Westchester County","New York"],["Fresno County","California"],["Honolulu County","Hawaii"],["Pima County","Arizona"],["Montgomery County","Maryland"],["Collin County","Texas"],["Fulton County","Georgia"],["Mecklenburg County","North Carolina"],["Wake County","North Carolina"],["Contra Costa County","California"],["Salt Lake County","Utah"],["Allegheny County","Pennsylvania"],["Cuyahoga County","Ohio"],["Oakland County","Michigan"],["Hennepin County","Minnesota"],["Travis County","Texas"],["Franklin County","Ohio"],["Nassau County","New York"],["Orange County","Florida"],["Hillsborough County","Florida"],["Bronx County","New York"],["Palm Beach County","Florida"],["Suffolk County","New York"],["Sacramento County","California"],["Philadelphia County","Pennsylvania"],["Middlesex County","Massachusetts"],["Alameda County","California"],["Wayne County","Michigan"],["Santa Clara County","California"],["Santa Clara County","California"],["Santa Clara County","California"],["Broward County","Florida"],["Bexar County","Texas"],["Tarrant County","Texas"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["Clark County","Nevada"],["King County","Washington"],["Queens County","New York"],["Riverside County","California"],["Dallas County","Texas"],["Miami-Dade County","Florida"],["Kings County","New York"],["Orange County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["Maricopa County","Arizona"],["Harris County","Texas"],["Cook County","Illinois"],["Los Angeles County","California"]],"hovertemplate":"2020 Income=%{x}\u003cbr\u003eTotalChristianAdherents=%{y}\u003cbr\u003eCOUNAM=%{customdata[0]}\u003cbr\u003eSTATNAM=%{customdata[1]}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","marker":{"color":"#636efa","symbol":"circle"},"mode":"markers","name":"","showlegend":false,"x":[108092.0,82906.0,49464.0,67559.0,70770.0,53465.0,37382.0,80793.0,61589.0,53831.0,69601.0,43803.0,60627.0,64167.0,54134.0,100751.0,65273.0,46681.0,54793.0,47951.0,49520.0,55032.0,54839.0,66673.0,70785.0,54192.0,46771.0,55626.0,52878.0,85559.0,64799.0,56973.0,49489.0,44334.0,86835.0,40468.0,52455.0,50445.0,55787.0,110024.0,66775.0,41756.0,74088.0,74359.0,74960.0,67156.0,60193.0,86809.0,46341.0,30808.0,60295.0,67793.0,56988.0,59974.0,40860.0,72083.0,45612.0,48292.0,45123.0,52433.0,92149.0,39867.0,60126.0,70968.0,38125.0,73604.0,84840.0,57145.0,57534.0,46115.0,40552.0,53849.0,65243.0,44296.0,51277.0,45294.0,70930.0,46042.0,86708.0,63420.0,51147.0,44973.0,61888.0,48559.0,62187.0,71235.0,50699.0,60539.0,54142.0,58003.0,35882.0,47986.0,26513.0,60901.0,47392.0,41246.0,57388.0,63667.0,53345.0,52433.0,54033.0,44347.0,84155.0,69116.0,60209.0,84431.0,58822.0,65571.0,38891.0,63376.0,60325.0,80242.0,44320.0,39618.0,80610.0,55960.0,64058.0,58101.0,56492.0,67896.0,39242.0,61718.0,68886.0,39904.0,66804.0,40966.0,58152.0,28178.0,54595.0,57053.0,51491.0,51374.0,52357.0,76020.0,40883.0,48926.0,46180.0,63327.0,42525.0,75761.0,46967.0,70349.0,51603.0,42496.0,66530.0,57674.0,49511.0,55686.0,48668.0,47506.0,60930.0,48720.0,64608.0,47701.0,54151.0,59476.0,54034.0,101691.0,37338.0,56100.0,38826.0,61317.0,46885.0,39165.0,73168.0,45061.0,38951.0,60193.0,63885.0,60719.0,55310.0,52705.0,57665.0,49798.0,64616.0,71448.0,68909.0,48419.0,96425.0,61150.0,59564.0,84296.0,42827.0,39836.0,66928.0,36475.0,45192.0,44595.0,46749.0,55270.0,49756.0,64478.0,35459.0,55649.0,51203.0,48131.0,66746.0,67518.0,41423.0,44010.0,40912.0,70584.0,55752.0,55079.0,73331.0,51338.0,47751.0,68446.0,55689.0,39514.0,51456.0,44958.0,57498.0,36420.0,53329.0,50670.0,55927.0,37613.0,41878.0,49344.0,53559.0,33421.0,52390.0,92697.0,47267.0,41397.0,54313.0,35657.0,48975.0,56985.0,66122.0,43291.0,65478.0,66380.0,68280.0,37088.0,33390.0,57302.0,58030.0,54643.0,74148.0,58493.0,66323.0,56940.0,52466.0,37774.0,40959.0,67492.0,59236.0,49755.0,40425.0,67879.0,57562.0,78373.0,68007.0,44208.0,53750.0,47083.0,48929.0,61578.0,69736.0,42234.0,56520.0,49767.0,37076.0,46091.0,50216.0,61148.0,74712.0,39623.0,48913.0,50511.0,38025.0,50337.0,51744.0,48952.0,41805.0,43704.0,43855.0,40815.0,50652.0,47126.0,64596.0,54969.0,41784.0,45086.0,72084.0,53174.0,49644.0,48158.0,47379.0,39855.0,47761.0,41358.0,47410.0,42539.0,40456.0,46119.0,37860.0,44567.0,75140.0,42970.0,46030.0,45270.0,47095.0,55337.0,57768.0,46679.0,67230.0,42626.0,58689.0,58018.0,42745.0,53926.0,43404.0,55990.0,45041.0,59967.0,57554.0,66926.0,42112.0,37555.0,42804.0,56116.0,40325.0,43785.0,82164.0,50834.0,45957.0,51993.0,50025.0,40681.0,69987.0,38302.0,49495.0,30574.0,53109.0,40267.0,40368.0,66980.0,62646.0,81718.0,50099.0,50407.0,43920.0,41450.0,48248.0,61335.0,53775.0,48640.0,56357.0,33404.0,48451.0,52862.0,60975.0,32097.0,43486.0,55152.0,49975.0,58070.0,55324.0,59520.0,50715.0,30401.0,66495.0,51290.0,32999.0,58470.0,40934.0,58274.0,45981.0,42099.0,48088.0,43148.0,43391.0,68478.0,46289.0,69152.0,47460.0,55446.0,44613.0,31475.0,52766.0,52888.0,47037.0,45373.0,45769.0,55991.0,43793.0,22614.0,49553.0,49337.0,50026.0,44544.0,47693.0,46327.0,53891.0,38223.0,43446.0,57219.0,37480.0,54319.0,50456.0,45045.0,48483.0,54216.0,34050.0,35671.0,47474.0,52619.0,38866.0,41939.0,45159.0,45689.0,45716.0,39111.0,69293.0,40569.0,59321.0,71730.0,40000.0,44640.0,44864.0,69397.0,47084.0,35317.0,40796.0,49668.0,45421.0,51656.0,43720.0,44373.0,57343.0,35395.0,49649.0,51083.0,46414.0,39180.0,53107.0,51156.0,58946.0,49700.0,41567.0,36863.0,30571.0,35688.0,44009.0,61068.0,50134.0,56610.0,50012.0,48868.0,41018.0,47843.0,48520.0,54205.0,47076.0,39376.0,44491.0,49854.0,72475.0,53796.0,48420.0,50811.0,50279.0,37561.0,60225.0,28022.0,49928.0,42858.0,54393.0,26406.0,52791.0,47704.0,39213.0,32615.0,39979.0,49886.0,40074.0,47797.0,41368.0,43886.0,70666.0,43440.0,53149.0,41122.0,35535.0,47688.0,50684.0,36308.0,33080.0,64887.0,58704.0,54852.0,70931.0,44558.0,26929.0,78962.0,48091.0,32152.0,47478.0,33347.0,54776.0,43964.0,44664.0,55045.0,34664.0,44128.0,41165.0,48941.0,22265.0,44506.0,53544.0,35876.0,46521.0,37668.0,42243.0,57667.0,37978.0,49359.0,49789.0,33658.0,50622.0,49727.0,43494.0,39004.0,38670.0,45294.0,46337.0,52443.0,38871.0,51288.0,55098.0,45093.0,47894.0,44472.0,36626.0,43642.0,39209.0,59453.0,34487.0,35174.0,31550.0,44783.0,48098.0,53467.0,45803.0,45981.0,42099.0,48088.0,43148.0,49970.0,31331.0,47476.0,47104.0,66012.0,41146.0,39293.0,40125.0,45316.0,36085.0,54134.0,100751.0,47226.0,41281.0,38448.0,43592.0,61289.0,47157.0,44577.0,37402.0,64596.0,29153.0,37531.0,36842.0,40890.0,36373.0,32289.0,35352.0,44416.0,56408.0,51262.0,49873.0,62172.0,57129.0,35211.0,52429.0,33084.0,56280.0,52394.0,41801.0,36388.0,38856.0,48475.0,48135.0,58284.0,42606.0,44055.0,34862.0,50623.0,42794.0,37701.0,51331.0,61846.0,37372.0,58110.0,34228.0,33059.0,52855.0,35668.0,50405.0,64233.0,45033.0,45365.0,44635.0,40403.0,43752.0,55270.0,35372.0,38665.0,38876.0,53072.0,47119.0,62970.0,39603.0,32954.0,44913.0,40793.0,47254.0,28791.0,50930.0,42857.0,38423.0,39924.0,44001.0,41008.0,41905.0,46552.0,62117.0,59467.0,35442.0,38425.0,33860.0,47537.0,34183.0,71571.0,44388.0,65146.0,53517.0,40996.0,44096.0,40207.0,34072.0,45167.0,41143.0,42569.0,52106.0,42505.0,44504.0,42725.0,31063.0,52019.0,40004.0,58150.0,34116.0,38680.0,78750.0,50464.0,48923.0,32007.0,42499.0,52324.0,46046.0,44636.0,68755.0,44085.0,56510.0,47651.0,60059.0,37746.0,49093.0,49253.0,48624.0,42518.0,60894.0,42995.0,38255.0,50758.0,43210.0,34644.0,42687.0,45412.0,50063.0,39014.0,37537.0,61995.0,39470.0,55108.0,40805.0,46207.0,55672.0,44415.0,38785.0,42831.0,51626.0,41580.0,42183.0,65804.0,37682.0,38384.0,71666.0,45029.0,54394.0,38396.0,38448.0,45067.0,33922.0,52260.0,37981.0,58081.0,33315.0,41763.0,47035.0,41776.0,49148.0,40759.0,57918.0,41184.0,54218.0,40147.0,40629.0,48951.0,37876.0,47919.0,47599.0,58823.0,41656.0,43993.0,46209.0,35391.0,44391.0,48848.0,43821.0,41626.0,58366.0,45269.0,37733.0,34412.0,42209.0,43668.0,44531.0,52318.0,30495.0,47590.0,36000.0,78838.0,59163.0,44611.0,39867.0,35071.0,38166.0,43164.0,55842.0,61913.0,57415.0,42750.0,49334.0,47869.0,35964.0,57727.0,55313.0,43900.0,42379.0,50400.0,36944.0,39507.0,50960.0,41046.0,37176.0,34627.0,49480.0,46612.0,52327.0,61302.0,40613.0,50818.0,41553.0,48975.0,56985.0,64049.0,39309.0,52667.0,45302.0,57383.0,44015.0,45077.0,42485.0,44257.0,65486.0,47929.0,38351.0,39468.0,44612.0,42169.0,36647.0,41670.0,34573.0,62687.0,40588.0,40202.0,37448.0,40575.0,49424.0,36300.0,32706.0,56394.0,35328.0,36308.0,33080.0,45389.0,43057.0,39731.0,46440.0,65421.0,44694.0,36454.0,45738.0,45617.0,58700.0,35650.0,54103.0,43730.0,39367.0,49649.0,51083.0,38333.0,44956.0,35575.0,48432.0,37100.0,56131.0,33906.0,35393.0,49636.0,46460.0,38786.0,40790.0,49012.0,54212.0,49230.0,54698.0,52680.0,43862.0,46345.0,42231.0,59113.0,47934.0,43084.0,41576.0,56584.0,36381.0,39487.0,44245.0,44325.0,41074.0,56429.0,38254.0,38061.0,42690.0,56122.0,41837.0,47452.0,32534.0,36073.0,54262.0,37856.0,39449.0,30798.0,37353.0,37331.0,43427.0,39597.0,49571.0,48882.0,40983.0,41023.0,44606.0,48844.0,59493.0,60155.0,50117.0,42785.0,54358.0,35823.0,34072.0,39207.0,37942.0,44595.0,40714.0,39213.0,38831.0,43918.0,44912.0,27953.0,40318.0,44133.0,48258.0,49065.0,29050.0,44503.0,37847.0,39322.0,39434.0,48306.0,39246.0,40285.0,40531.0,35935.0,34858.0,34438.0,37287.0,36069.0,39276.0,55374.0,29553.0,47067.0,35150.0,40580.0,42610.0,44900.0,41680.0,46806.0,41056.0,44159.0,50438.0,36250.0,47446.0,35589.0,49689.0,34696.0,41787.0,39935.0,60401.0,46818.0,46030.0,39742.0,49062.0,43275.0,43079.0,37234.0,38277.0,49669.0,50707.0,40693.0,41810.0,41537.0,46684.0,37461.0,36046.0,31376.0,56320.0,32854.0,47991.0,43908.0,33095.0,45593.0,42602.0,31505.0,45733.0,48866.0,34940.0,30828.0,65990.0,43365.0,53927.0,41027.0,40077.0,45732.0,51376.0,49292.0,34888.0,29864.0,45891.0,44112.0,47749.0,36793.0,59311.0,31555.0,36853.0,47741.0,48637.0,42819.0,43551.0,37679.0,41100.0,30660.0,44375.0,45637.0,37129.0,53543.0,34422.0,36666.0,41652.0,40776.0,54017.0,34477.0,47883.0,45649.0,40092.0,37326.0,40289.0,35069.0,36756.0,93597.0,46463.0,35778.0,48423.0,45170.0,45369.0,39617.0,39966.0,43042.0,61390.0,39992.0,46583.0,32504.0,69066.0,61885.0,39407.0,42034.0,47687.0,45595.0,48510.0,43856.0,46466.0,65969.0,62728.0,55169.0,46611.0,48877.0,47834.0,57271.0,35062.0,69063.0,41204.0,36817.0,43786.0,40391.0,51038.0,53591.0,40560.0,40269.0,30342.0,40410.0,48159.0,44632.0,39063.0,49508.0,39416.0,41073.0,37928.0,38553.0,61983.0,40086.0,44504.0,45473.0,35269.0,51626.0,41580.0,42183.0,41383.0,53534.0,35067.0,48954.0,40262.0,59845.0,42418.0,45044.0,38272.0,44082.0,52478.0,43639.0,51458.0,40070.0,46069.0,62867.0,40434.0,48695.0,37003.0,40447.0,48566.0,44986.0,46769.0,52030.0,45317.0,38486.0,55998.0,49205.0,46897.0,35851.0,45472.0,41663.0,35628.0,36672.0,37685.0,43760.0,55792.0,36560.0,43573.0,49141.0,37490.0,45525.0,33472.0,46646.0,41929.0,24472.0,43531.0,36305.0,42968.0,39109.0,49990.0,32988.0,37930.0,34586.0,37748.0,49141.0,38222.0,41948.0,41472.0,40636.0,53601.0,46835.0,42227.0,45108.0,35138.0,44377.0,45180.0,52050.0,37488.0,52843.0,46218.0,40166.0,39083.0,47826.0,50675.0,44785.0,58006.0,44533.0,41032.0,48831.0,42060.0,48082.0,33019.0,42845.0,45626.0,114448.0,33515.0,33807.0,40176.0,45807.0,48011.0,48765.0,45591.0,31173.0,56132.0,45003.0,40919.0,39816.0,33075.0,40809.0,54208.0,41577.0,36350.0,35810.0,45369.0,38361.0,43833.0,57215.0,48887.0,47555.0,53475.0,35045.0,36499.0,45547.0,37085.0,50786.0,47428.0,38354.0,42835.0,172065.0,54055.0,41835.0,55117.0,51953.0,36703.0,39401.0,36305.0,54055.0,49333.0,52002.0,62621.0,39149.0,54083.0,55545.0,81257.0,40161.0,51156.0,58946.0,49700.0,39778.0,36314.0,54030.0,39490.0,47331.0,39382.0,41403.0,40973.0,35469.0,43066.0,37897.0,52454.0,41984.0,32305.0,39236.0,46857.0,47008.0,60469.0,37707.0,36178.0,47547.0,37256.0,39401.0,50114.0,35350.0,46165.0,39134.0,39418.0,48096.0,44011.0,37987.0,38930.0,55521.0,37936.0,37003.0,57206.0,48757.0,42715.0,35114.0,47469.0,48592.0,39931.0,39482.0,41539.0,45594.0,54952.0,39063.0,39283.0,45095.0,37567.0,64295.0,40525.0,45763.0,46760.0,41009.0,59712.0,56709.0,46978.0,39534.0,39850.0,30972.0,39331.0,42200.0,51511.0,39659.0,43897.0,63055.0,33975.0,37044.0,43790.0,54915.0,47248.0,41664.0,76281.0,40900.0,56194.0,48820.0,51067.0,47949.0,35788.0,45853.0,34772.0,55045.0,34664.0,44128.0,34551.0,40521.0,53640.0,40588.0,41488.0,38764.0,34977.0,50846.0,35654.0,41848.0,39879.0,40089.0,54884.0,38727.0,37497.0,38064.0,54643.0,39647.0,36698.0,49103.0,58322.0,40546.0,43693.0,47024.0,34673.0,55051.0,43696.0,39941.0,54004.0,42760.0,35619.0,54221.0,44574.0,53448.0,59787.0,41968.0,32989.0,45584.0,39309.0,52667.0,45302.0,57383.0,44015.0,45077.0,42485.0,44257.0,65486.0,50337.0,36843.0,46078.0,46931.0,59998.0,34708.0,39621.0,43193.0,38155.0,42289.0,35078.0,33884.0,39134.0,42177.0,45726.0,45115.0,46174.0,55645.0,52538.0,50957.0,37202.0,38419.0,84852.0,40598.0,43788.0,45833.0,47422.0,43993.0,41962.0,53594.0,54473.0,39412.0,38257.0,39032.0,44294.0,55187.0,60651.0,52442.0,40642.0,44865.0,46049.0,44679.0,34236.0,51882.0,44103.0,35622.0,48388.0,45629.0,39905.0,45822.0,49719.0,38166.0,56195.0,34832.0,36842.0,44409.0,56054.0,50518.0,31846.0,50690.0,55911.0,41240.0,41644.0,39967.0,47920.0,39552.0,43592.0,46852.0,35490.0,38993.0,35773.0,42448.0,58227.0,46496.0,44768.0,55601.0,38849.0,40851.0,51048.0,41465.0,34114.0,37561.0,42488.0,56086.0,35765.0,34244.0,50170.0,45220.0,42190.0,36506.0,38344.0,51002.0,49113.0,42032.0,45398.0,43080.0,41561.0,35084.0,34875.0,45319.0,40609.0,57608.0,49729.0,51209.0,34938.0,73012.0,43866.0,37295.0,48618.0,37841.0,44893.0,58654.0,39267.0,43455.0,36100.0,51544.0,38126.0,41541.0,37954.0,51070.0,41393.0,31015.0,42881.0,88570.0,39122.0,54842.0,39853.0,41234.0,33567.0,41686.0,45725.0,31987.0,53954.0,300665.0,41564.0,43984.0,38021.0,43942.0,48659.0,35942.0,51960.0,47940.0,42735.0,44375.0,52142.0,34880.0,51198.0,38037.0,39386.0,38717.0,33906.0,41945.0,53207.0,42052.0,36012.0,38304.0,57014.0,41572.0,38779.0,59611.0,48508.0,36979.0,48274.0,41526.0,124919.0,37259.0,38062.0,37810.0,41138.0,62179.0,39296.0,34497.0,43306.0,40259.0,43781.0,48304.0,39461.0,37945.0,32523.0,41837.0,48779.0,34742.0,47244.0,56814.0,45100.0,43576.0,41095.0,99944.0,46970.0,41269.0,45843.0,45407.0,91880.0,38085.0,41639.0,40405.0,33447.0,39971.0,52852.0,35645.0,43321.0,45759.0,36415.0,35383.0,55526.0,37111.0,43594.0,43567.0,54014.0,35518.0,33893.0,42947.0,32291.0,56879.0,43140.0,42362.0,35778.0,37629.0,38848.0,32653.0,50775.0,49956.0,55725.0,45511.0,41084.0,47109.0,45006.0,56546.0,31868.0,41954.0,57548.0,37054.0,41239.0,46985.0,35830.0,56786.0,57739.0,50727.0,40720.0,33719.0,46103.0,39067.0,58198.0,65795.0,52115.0,45817.0,35506.0,39021.0,47943.0,40988.0,47496.0,40730.0,51199.0,57664.0,35782.0,38181.0,42975.0,34500.0,48163.0,49639.0,42804.0,44274.0,51156.0,58946.0,49700.0,77886.0,33969.0,39309.0,51885.0,47361.0,34123.0,41809.0,54791.0,46579.0,41474.0,39384.0,49496.0,43204.0,32047.0,51626.0,41580.0,42183.0,39050.0,40795.0,44340.0,36030.0,48349.0,37583.0,49630.0,49897.0,45981.0,42099.0,48088.0,43148.0,40156.0,39936.0,44581.0,48966.0,37311.0,41477.0,38025.0,42303.0,40722.0,42358.0,48798.0,41448.0,42550.0,33274.0,43654.0,43346.0,40853.0,52882.0,39862.0,45983.0,42808.0,44057.0,39068.0,34908.0,38660.0,39597.0,39530.0,35469.0,37466.0,55496.0,42307.0,40731.0,36560.0,47443.0,49761.0,36828.0,37516.0,43615.0,39236.0,42845.0,44923.0,38790.0,40162.0,54860.0,36538.0,38895.0,49002.0,43075.0,42853.0,44783.0,49494.0,45784.0,50940.0,44636.0,46017.0,45625.0,40155.0,45903.0,47071.0,37566.0,44453.0,40137.0,52909.0,37100.0,37647.0,43676.0,39569.0,43041.0,40077.0,61527.0,48615.0,40203.0,48892.0,40931.0,42902.0,50831.0,65788.0,39779.0,35791.0,43565.0,56360.0,34963.0,54911.0,47803.0,48753.0,42533.0,41327.0,60942.0,40340.0,42645.0,42176.0,37099.0,45808.0,46904.0,43945.0,45884.0,38429.0,39625.0,47241.0,40302.0,48796.0,59264.0,36600.0,46262.0,41886.0,50253.0,36874.0,41018.0,32726.0,77833.0,44065.0,46121.0,43419.0,41738.0,38578.0,53411.0,42775.0,52791.0,42403.0,49251.0,40998.0,38423.0,51614.0,40393.0,39168.0,35024.0,45603.0,38886.0,36497.0,44176.0,46958.0,54778.0,45806.0,38523.0,38488.0,39342.0,49325.0,38968.0,40191.0,38061.0,39648.0,40290.0,45219.0,50858.0,56431.0,43919.0,46945.0,45937.0,48333.0,40936.0,50457.0,34928.0,36917.0,46904.0,46904.0,41550.0,38738.0,52304.0,46708.0,56482.0,47856.0,48419.0,50924.0,52773.0,42441.0,41703.0,46428.0,55106.0,43302.0,61656.0,41631.0,41023.0,41790.0,42545.0,44205.0,30593.0,46998.0,39536.0,47458.0,43724.0,62269.0,46791.0,37902.0,40697.0,49743.0,54189.0,39580.0,44324.0,50871.0,43068.0,50774.0,48261.0,54439.0,52901.0,41204.0,38451.0,41969.0,47556.0,52912.0,55121.0,52995.0,41748.0,36250.0,68334.0,48420.0,41303.0,45594.0,61159.0,49834.0,51352.0,54689.0,44003.0,43030.0,42489.0,46660.0,53199.0,33216.0,43343.0,61115.0,42562.0,50312.0,54447.0,45671.0,39189.0,47271.0,37172.0,44186.0,37094.0,39132.0,49372.0,46736.0,36443.0,55580.0,47632.0,49319.0,42020.0,47287.0,39403.0,43031.0,45097.0,54540.0,39701.0,39250.0,42481.0,47866.0,36380.0,52260.0,39605.0,45929.0,46296.0,53243.0,43631.0,64544.0,45731.0,43653.0,46570.0,43926.0,46450.0,56709.0,46978.0,44916.0,42030.0,44063.0,50938.0,41757.0,45983.0,55683.0,39927.0,55761.0,38572.0,51196.0,50087.0,45851.0,44180.0,78636.0,37926.0,46650.0,42903.0,46546.0,42160.0,45513.0,52255.0,42919.0,44562.0,38571.0,37046.0,44870.0,48461.0,43177.0,44267.0,61042.0,51951.0,45785.0,39269.0,56414.0,45041.0,35930.0,46564.0,38817.0,57943.0,52246.0,46026.0,37860.0,44567.0,53868.0,49649.0,43056.0,38047.0,55797.0,42065.0,50523.0,37889.0,42300.0,49046.0,38958.0,39333.0,47116.0,47866.0,37468.0,35817.0,48601.0,42720.0,40832.0,46804.0,38338.0,33208.0,50841.0,45331.0,34165.0,44297.0,39018.0,57576.0,38206.0,40281.0,47604.0,47359.0,40368.0,45902.0,42956.0,55815.0,43832.0,37870.0,50951.0,46611.0,41057.0,61728.0,38857.0,44657.0,43893.0,49704.0,49323.0,49420.0,44621.0,41453.0,49656.0,48622.0,41064.0,49755.0,54196.0,41458.0,71183.0,47230.0,64094.0,47523.0,42878.0,47492.0,46649.0,40525.0,51054.0,54708.0,164349.0,56802.0,39309.0,52667.0,45302.0,57383.0,44015.0,45077.0,42485.0,44257.0,65486.0,53785.0,45726.0,39534.0,37613.0,45861.0,48155.0,53010.0,49978.0,46029.0,42717.0,45580.0,36460.0,41033.0,45851.0,40265.0,40113.0,35765.0,59146.0,35602.0,40196.0,52333.0,50498.0,48371.0,35858.0,40852.0,37672.0,57951.0,42616.0,45376.0,53706.0,39309.0,52667.0,45302.0,57383.0,44015.0,45077.0,42485.0,44257.0,65486.0,40517.0,37644.0,47773.0,40828.0,49301.0,43617.0,38200.0,52517.0,49287.0,49487.0,102177.0,43232.0,45619.0,44929.0,50834.0,40063.0,46457.0,41963.0,40139.0,47302.0,42234.0,49644.0,45251.0,51941.0,45039.0,44893.0,40186.0,41199.0,46127.0,49838.0,46721.0,38532.0,48304.0,47164.0,54090.0,42193.0,44574.0,39371.0,38993.0,39728.0,47490.0,39512.0,50775.0,37542.0,37726.0,53101.0,36900.0,40802.0,40728.0,46433.0,43457.0,45865.0,47070.0,38398.0,46143.0,50590.0,44029.0,42694.0,41777.0,47396.0,57543.0,54519.0,48163.0,46223.0,48069.0,53982.0,38429.0,48711.0,47274.0,37783.0,43960.0,45263.0,45877.0,56574.0,42826.0,43176.0,53506.0,44263.0,41045.0,46290.0,50857.0,36610.0,41433.0,48999.0,42757.0,42019.0,48363.0,49889.0,40249.0,44157.0,44507.0,40426.0,42307.0,38348.0,42201.0,56988.0,50741.0,40264.0,39309.0,52667.0,45302.0,57383.0,44015.0,45077.0,42485.0,44257.0,65486.0,85351.0,45579.0,45482.0,40071.0,54757.0,51867.0,71124.0,52041.0,43169.0,41767.0,61104.0,46823.0,66049.0,45282.0,41161.0,49063.0,40554.0,42564.0,46659.0,43319.0,39746.0,51945.0,46478.0,79886.0,49683.0,45866.0,50306.0,40145.0,39309.0,52667.0,45302.0,57383.0,44015.0,45077.0,42485.0,44257.0,65486.0,49259.0,36752.0,49255.0,47551.0,47534.0,37583.0,42480.0,54580.0,54563.0,44253.0,63280.0,59037.0,59249.0,39309.0,52667.0,45302.0,57383.0,44015.0,45077.0,42485.0,44257.0,65486.0,51440.0,38905.0,49675.0,58308.0,41794.0,24804.0,43011.0,51766.0,44992.0,40593.0,41683.0,47903.0,46477.0,50554.0,45039.0,50285.0,43815.0,40193.0,43123.0,51212.0,46622.0,47157.0,41046.0,39770.0,44774.0,57182.0,44460.0,44714.0,55551.0,49653.0,61017.0,47896.0,88073.0,45888.0,38930.0,40812.0,45524.0,36399.0,51383.0,37193.0,53893.0,37851.0,47528.0,48133.0,40052.0,36491.0,44005.0,49979.0,38340.0,43949.0,41826.0,56828.0,62220.0,42791.0,35612.0,43257.0,39154.0,43885.0,48133.0,56124.0,50514.0,53568.0,46686.0,45315.0,54776.0,42210.0,39793.0,45151.0,43591.0,45422.0,40816.0,38133.0,35834.0,43975.0,42250.0,44878.0,41342.0,46708.0,64276.0,45479.0,52985.0,38448.0,47905.0,45161.0,54826.0,49920.0,42894.0,44992.0,42701.0,41290.0,45483.0,64301.0,58990.0,57713.0,49329.0,45508.0,44882.0,59037.0,49305.0,38205.0,43161.0,49569.0,37353.0,48455.0,62252.0,44544.0,46608.0,43632.0,44833.0,37783.0,51911.0,68625.0,61644.0,59893.0,45968.0,67536.0,134758.0,51317.0,63024.0,141882.0,43774.0,43262.0,38322.0,40942.0,42111.0,47526.0,59495.0,44578.0,51979.0,50770.0,42593.0,43088.0,74385.0,43026.0,37957.0,46496.0,42856.0,40180.0,46383.0,49947.0,47670.0,51390.0,58485.0,55652.0,44883.0,30393.0,52777.0,41195.0,44162.0,42192.0,48945.0,50119.0,42004.0,43560.0,45287.0,37785.0,42422.0,37681.0,58150.0,34116.0,38680.0,78750.0,50464.0,48029.0,46791.0,48729.0,40962.0,38360.0,38420.0,50073.0,39308.0,67763.0,37808.0,57425.0,38876.0,38879.0,51037.0,52001.0,44642.0,45121.0,44016.0,41803.0,50815.0,45981.0,42099.0,48088.0,43148.0,44622.0,48273.0,41388.0,43406.0,41256.0,39953.0,57499.0,42131.0,39424.0,50335.0,77646.0,53728.0,60460.0,43044.0,34596.0,45104.0,47587.0,45640.0,43216.0,41853.0,40914.0,47479.0,31984.0,74288.0,44162.0,54966.0,53025.0,37372.0,43624.0,45170.0,73540.0,45706.0,44276.0,49588.0,45549.0,43723.0,55745.0,73458.0,46525.0,53374.0,43766.0,47450.0,39662.0,49227.0,70275.0,31270.0,57496.0,40817.0,44580.0,41674.0,46708.0,50927.0,52041.0,40128.0,48315.0,50941.0,44619.0,57951.0,51423.0,50096.0,55304.0,48550.0,44256.0,63738.0,44746.0,52076.0,56726.0,49015.0,40096.0,46103.0,35955.0,49295.0,45680.0,41494.0,46142.0,46924.0,37831.0,48860.0,45327.0,55840.0,46371.0,39309.0,52667.0,45302.0,57383.0,44015.0,45077.0,42485.0,44257.0,65486.0,94837.0,35066.0,44250.0,47155.0,56589.0,41874.0,43810.0,45727.0,49058.0,38634.0,48300.0,50449.0,52711.0,43656.0,47175.0,49776.0,76435.0,40963.0,48169.0,42940.0,46164.0,51873.0,59211.0,42524.0,45753.0,41095.0,42181.0,44636.0,47955.0,48910.0,45626.0,47464.0,43529.0,66135.0,41380.0,43432.0,69092.0,51420.0,53497.0,86875.0,52477.0,40350.0,45991.0,40444.0,67104.0,45485.0,54457.0,46002.0,59624.0,42199.0,38989.0,51262.0,47560.0,46125.0,46612.0,49990.0,55639.0,50088.0,68836.0,72092.0,51515.0,46685.0,42484.0,52264.0,39579.0,45827.0,43214.0,41147.0,75547.0,44998.0,62748.0,44838.0,40944.0,46767.0,45301.0,52804.0,44325.0,40777.0,49536.0,70783.0,57370.0,44183.0,45130.0,47111.0,55842.0,49475.0,47663.0,38713.0,42263.0,46952.0,66471.0,42967.0,46351.0,39607.0,47831.0,42951.0,52796.0,53258.0,47030.0,51474.0,52419.0,55522.0,49320.0,42588.0,51690.0,50472.0,49914.0,46199.0,42200.0,55245.0,38620.0,60173.0,75745.0,47325.0,47418.0,50987.0,68067.0,51424.0,42651.0,43229.0,51885.0,43677.0,69053.0,47613.0,60280.0,45377.0,59268.0,48757.0,65092.0,45553.0,48025.0,49999.0,45865.0,46163.0,42319.0,41680.0,44985.0,58637.0,38876.0,62459.0,48046.0,54916.0,48378.0,50431.0,39591.0,37167.0,50260.0,48916.0,44189.0,45759.0,57586.0,54964.0,41402.0,50672.0,48676.0,64278.0,44781.0,68059.0,55966.0,49943.0,53817.0,48762.0,45564.0,39050.0,40795.0,47706.0,40826.0,50853.0,47277.0,42823.0,44624.0,50123.0,59981.0,50722.0,42685.0,46835.0,55802.0,44634.0,45266.0,47621.0,37715.0,48586.0,46421.0,93251.0,61119.0,47084.0,57890.0,59621.0,73351.0,49889.0,42202.0,57102.0,49252.0,51825.0,41165.0,53667.0,51204.0,47932.0,43024.0,43882.0,46250.0,39664.0,43593.0,41280.0,48265.0,48865.0,53533.0,44342.0,50271.0,53840.0,61808.0,46728.0,54405.0,81905.0,48509.0,53164.0,56703.0,45942.0,46399.0,49851.0,41475.0,52362.0,41641.0,67079.0,40654.0,46322.0,52890.0,47174.0,53350.0,41866.0,55070.0,61523.0,72271.0,47801.0,59931.0,65678.0,47264.0,41185.0,56435.0,64297.0,41602.0,44000.0,53645.0,48590.0,49195.0,49721.0,63104.0,48548.0,51296.0,55580.0,44394.0,59185.0,48414.0,43114.0,53155.0,46648.0,52013.0,54121.0,97665.0,51542.0,87110.0,43423.0,43602.0,49920.0,42894.0,48940.0,53673.0,66119.0,43292.0,52360.0,48833.0,63522.0,61338.0,45424.0,47909.0,70759.0,55689.0,52923.0,48111.0,59941.0,55350.0,43256.0,52557.0,63772.0,48872.0,43299.0,47964.0,43984.0,61264.0,52288.0,36191.0,106959.0,48920.0,62462.0,54939.0,51986.0,44223.0,51855.0,49507.0,65131.0,56244.0,41326.0,56697.0,53266.0,50069.0,43376.0,51540.0,50511.0,45565.0,48150.0,50628.0,45360.0,51353.0,52939.0,46052.0,58285.0,51246.0,60353.0,50869.0,61838.0,70947.0,47190.0,42526.0,56778.0,48422.0,65026.0,50522.0,45686.0,54913.0,55048.0,74197.0,49860.0,63279.0,62417.0,42700.0,54958.0,52360.0,64774.0,52951.0,64080.0,47398.0,50553.0,43161.0,50009.0,43736.0,42177.0,46781.0,50158.0,41139.0,50724.0,44073.0,49336.0,60894.0,41786.0,60909.0,51308.0,53709.0,57737.0,50213.0,40229.0,80033.0,51659.0,44945.0,60305.0,46741.0,47815.0,45830.0,59313.0,51850.0,54128.0,49313.0,41905.0,46606.0,53867.0,39137.0,44309.0,44808.0,47491.0,46116.0,79606.0,45077.0,55321.0,39271.0,51230.0,49571.0,55040.0,55450.0,43706.0,69305.0,46954.0,56403.0,54770.0,58390.0,97751.0,42920.0,52159.0,54100.0,66255.0,44883.0,99108.0,69446.0,52111.0,45227.0,45996.0,50312.0,60871.0,45756.0,62146.0,54818.0,46020.0,144658.0,39309.0,52667.0,45302.0,57383.0,44015.0,45077.0,42485.0,44257.0,65486.0,51122.0,57355.0,37015.0,71110.0,60506.0,61119.0,56965.0,52847.0,68801.0,124637.0,78299.0,50179.0,65495.0,50076.0,76091.0,45416.0,53533.0,62192.0,47655.0,44163.0,51878.0,59893.0,45968.0,67536.0,134758.0,51317.0,63024.0,141882.0,83178.0,46267.0,46497.0,54891.0,49155.0,52224.0,54831.0,51366.0,47444.0,63835.0,53553.0,31757.0,47751.0,58150.0,34116.0,38680.0,78750.0,50464.0,58451.0,68583.0,59795.0,48140.0,60074.0,50943.0,81679.0,68825.0,47483.0,55601.0,53413.0,53973.0,48544.0,47726.0,51920.0,76091.0,45416.0,81673.0,81308.0,69268.0,42554.0,64228.0,45965.0,103317.0,49115.0,80436.0,56203.0,44013.0,48777.0,56226.0,83745.0,59762.0,50348.0,55673.0,58219.0,56191.0,46569.0,53110.0,64606.0,58875.0,48985.0,110993.0,40896.0,51667.0,50701.0,45699.0,55577.0,50107.0,72811.0,56265.0,39272.0,51827.0,55665.0,53842.0,55350.0,74046.0,58150.0,34116.0,38680.0,78750.0,50464.0,45384.0,76931.0,68698.0,42416.0,48969.0,85393.0,33704.0,64848.0,66256.0,41546.0,54418.0,50236.0,74102.0,60216.0,63327.0,54778.0,45806.0,68801.0,124637.0,78299.0,57029.0,54395.0,55045.0,34664.0,44128.0,65369.0,57736.0,52928.0,45523.0,57781.0,55991.0,35765.0,65110.0,71866.0,57284.0,58150.0,59317.0,47778.0,57827.0,100797.0,58284.0,48594.0,56814.0,53098.0,53539.0,52076.0,74093.0,92175.0,51333.0,49083.0,56369.0,49900.0,57421.0,48532.0,57816.0,47861.0,65500.0,46646.0,58624.0,70682.0,70945.0,60325.0,68983.0,63908.0,63845.0,54125.0,72194.0,67693.0,51212.0,57774.0,79088.0,68909.0,56954.0,86588.0,78810.0,69132.0,59254.0,51528.0,61416.0,58074.0,50063.0,57742.0,81516.0,86823.0,73177.0,49572.0,64653.0,40807.0,95831.0,54504.0,57124.0,58139.0,55996.0,59893.0,45968.0,67536.0,134758.0,51317.0,63024.0,141882.0,62551.0,59893.0,45968.0,67536.0,134758.0,51317.0,63024.0,141882.0,56306.0,87433.0,71952.0,62954.0,63655.0,62805.0,63022.0,68273.0,63845.0,54125.0,86337.0,61287.0,64841.0,67857.0,60506.0,61119.0,40186.0,31310.0,59893.0,45968.0,67536.0,134758.0,51317.0,63024.0,141882.0,50883.0,66436.0,64582.0,44490.0,55533.0,53335.0,78904.0,50651.0,55097.0,88461.0,45934.0,115859.0,60721.0,50197.0,59825.0,49908.0,58150.0,34116.0,38680.0,78750.0,50464.0,111340.0,48095.0,60273.0,49601.0,85373.0,72105.0,92999.0,68546.0,65717.0,86359.0,57292.0,66014.0,57048.0,76404.0,77672.0,72771.0,54352.0,91828.0,48829.0,53144.0,41240.0,92202.0,78701.0,57243.0,54887.0,90955.0,87561.0,46416.0,68801.0,124637.0,78299.0,56080.0,47970.0,53863.0,59893.0,45968.0,67536.0,134758.0,51317.0,63024.0,141882.0,52562.0,99372.0,51882.0,48265.0,66044.0,56235.0,55031.0,75572.0,59893.0,45968.0,67536.0,134758.0,51317.0,63024.0,141882.0,56024.0,59099.0,66952.0,67383.0],"xaxis":"x","y":[null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,3651.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,2952.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,4363.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,8906.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,6062.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,6823.0,null,null,null,null,null,null,null,null,null,null,null,null,3222.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,13686.0,null,null,null,3356.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,14175.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,8515.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,18508.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,17522.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,17483.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,20514.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,11036.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,16864.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,25264.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,20191.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,19624.0,12629.0,null,null,25704.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,37304.0,null,null,null,null,null,null,null,null,null,29565.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,17899.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,26119.0,null,null,null,null,null,null,null,null,null,36564.0,null,42177.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,29681.0,null,null,null,null,null,null,null,null,null,null,null,null,48476.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,31789.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,77734.0,null,null,null,null,null,null,null,null,45985.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,44089.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,63071.0,null,null,null,null,null,null,null,null,40854.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,54525.0,null,null,null,null,null,null,null,49439.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,86431.0,null,null,null,null,null,null,null,null,null,null,null,null,null,68083.0,null,null,null,null,null,null,87705.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,175241.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,183935.0,null,null,null,null,null,null,null,null,null,null,null,null,null,224180.0,null,null,null,null,null,null,null,null,null,null,200318.0,null,null,null,null,124287.0,143268.0,null,null,null,218878.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,303505.0,null,null,null,null,null,null,null,null,null,266225.0,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,337546.0,null,null,null,null,null,null,null,null,329136.0,null,null,331400.0,331400.0,null,null,227040.0,227040.0,227040.0,227040.0,227040.0,227040.0,227040.0,null,328390.0,null,null,null,541101.0,null,null,null,null,null,440401.0,394788.0,null,null,609659.0,null,null,null,null,null,null,null,null,null,400437.0,null,null,493661.0,410469.0,null,null,null,null,null,null,null,null,null,null,756324.0,null,null,null,null,null,719967.0,null,null,null,null,null,null,null,1080375.0,null,null,null,null,null,null,null,null,677387.0,null,null,null,1239303.0,null,1351115.0,1099890.0,1099890.0,1099890.0,1099890.0,1099890.0,1099890.0,1099890.0,null,null,2251893.0,4374608.0],"yaxis":"y","type":"scattergl"},{"hovertemplate":"\u003cb\u003eOLS trendline\u003c\u002fb\u003e\u003cbr\u003eTotalChristianAdherents = 8.67691 * 2020 Income + -138292\u003cbr\u003eR\u003csup\u003e2\u003c\u002fsup\u003e=0.110527\u003cbr\u003e\u003cbr\u003e2020 Income=%{x}\u003cbr\u003eTotalChristianAdherents=%{y} \u003cb\u003e(trend)\u003c\u002fb\u003e\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","line":{"color":"red"},"marker":{"color":"#636efa","symbol":"circle"},"mode":"lines","name":"","showlegend":false,"x":[30972.0,31555.0,32305.0,33095.0,35668.0,37488.0,37561.0,37672.0,38817.0,38895.0,39283.0,39384.0,39607.0,39746.0,39953.0,40096.0,40807.0,40851.0,41095.0,41139.0,42554.0,43041.0,43632.0,43723.0,44157.0,44180.0,44189.0,44619.0,44945.0,45104.0,45161.0,45968.0,45968.0,46646.0,46685.0,47909.0,48455.0,48940.0,49320.0,49900.0,49908.0,50069.0,51317.0,51317.0,51353.0,51528.0,51941.0,52711.0,53144.0,53335.0,53863.0,54128.0,56235.0,56726.0,57736.0,58284.0,59893.0,59893.0,60325.0,60506.0,60721.0,61119.0,61287.0,62252.0,63024.0,63024.0,65500.0,65717.0,66436.0,66952.0,67383.0,67536.0,67536.0,68546.0,71952.0,75572.0,85373.0,90955.0,99372.0,115859.0,134758.0,134758.0,141882.0,141882.0],"xaxis":"x","y":[130448.939911558,135507.5755458842,142015.25432074646,148870.00929693464,171195.68594722863,186987.65310756094,187621.06717498088,188584.2036336605,198519.2598966168,199196.05848920246,202562.69764206454,203439.06505041267,205374.01487280504,206580.1046724128,208376.22401427478,209617.0214340152,215786.3009125846,216168.08473404316,218285.24956213165,218667.03338359023,230944.85400549695,235170.50675664085,240298.55763123225,241088.1559892489,244853.93277363584,245053.50158939825,245131.59373469662,248862.66289895092,251691.33393975772,253070.96184002853,253565.54542691802,260567.80778866977,260567.80778866977,266450.74940114527,266789.14869743807,277409.6804580132,282147.2706061129,286355.5695471905,289652.7934597873,294685.3983790141,294754.8136192793,296151.7953296164,306980.5728109871,306980.5728109871,307292.9413921805,308811.3997729817,312394.9615516725,319076.17842719774,322833.2783065515,324490.5671678831,329071.9730253861,331371.35285917076,349653.591764017,353913.95213529345,362677.6262187746,367432.5701769406,381393.7103752784,381393.7103752784,385142.13334959897,386712.65316059906,388578.1877427262,392031.59594591975,393489.31599148887,401862.5293484783,408561.10003406985,408561.10003406985,430045.1168961483,431928.0052883418,438166.7000071764,442643.98300428153,446383.72907356906,447711.29554364097,447711.29554364097,456474.96962712205,486028.50817002973,517438.90439003136,602481.2506199308,650915.7345149721,723949.2441789925,867005.3774605304,1030990.2056820252,1030990.2056820252,1092804.477138183,1092804.477138183],"yaxis":"y","type":"scattergl"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"2020 Income"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"TotalChristianAdherents"}},"legend":{"tracegroupgap":0},"margin":{"t":60}},                        {"responsive": true}                    )         };                            </script>        </div>
</body>
</html>


This one was a hail mary, but I noticed the outliers could possibly be dealt with by having the y be on a per capita basis.


```python
# prompt: Same graph as previous but make the x the log of the 2020 income

# Assuming IncomeAndReligionByCounty is your DataFrame
IncomeAndReligionByCounty['Log TotalChristianAdherents'] = np.log(IncomeAndReligionByCounty['TotalChristianAdherents'])
IncomeAndReligionByCounty['Log 2020 Income'] = np.log(IncomeAndReligionByCounty['2020 Income'])

# Create the scatter plot
fig = px.scatter(IncomeAndReligionByCounty, x = 'Log 2020 Income', y = 'Log TotalChristianAdherents', hover_data=['COUNAM', 'STATNAM'], trendline='ols', trendline_color_override='red')

fig.update_layout(
    title='Log of 2020 Income vs. Log of Total Christian Adherents',
    xaxis_title='Log of 2020 Income',
    yaxis_title='Log of Total Christian Adherents'
)

fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
        <script charset="utf-8" src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>                <div id="c214e7c9-bfa5-46fa-a090-3ba4f67c2cf9" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("c214e7c9-bfa5-46fa-a090-3ba4f67c2cf9")) {                    Plotly.newPlot(                        "c214e7c9-bfa5-46fa-a090-3ba4f67c2cf9",                        [{"customdata":[["Loving County","Texas"],["King County","Texas"],["Kenedy County","Texas"],["McPherson County","Nebraska"],["Blaine County","Nebraska"],["Arthur County","Nebraska"],["Petroleum County","Montana"],["McMullen County","Texas"],["Loup County","Nebraska"],["Grant County","Nebraska"],["Borden County","Texas"],["Harding County","New Mexico"],["Thomas County","Nebraska"],["Banner County","Nebraska"],["San Juan County","Colorado"],["San Juan County","Colorado"],["Slope County","North Dakota"],["Hooker County","Nebraska"],["Logan County","Nebraska"],["Esmeralda County","Nevada"],["Kent County","Texas"],["Terrell County","Texas"],["Treasure County","Montana"],["Keya Paha County","Nebraska"],["Wheeler County","Nebraska"],["Hinsdale County","Colorado"],["Clark County","Idaho"],["Golden Valley County","Montana"],["Roberts County","Texas"],["Hayes County","Nebraska"],["Mineral County","Colorado"],["Jones County","South Dakota"],["Daggett County","Utah"],["Wibaux County","Montana"],["Billings County","North Dakota"],["Motley County","Texas"],["Camas County","Idaho"],["Prairie County","Montana"],["Foard County","Texas"],["Glasscock County","Texas"],["Sioux County","Nebraska"],["Garfield County","Montana"],["Alpine County","California"],["Stonewall County","Texas"],["Rock County","Nebraska"],["Hyde County","South Dakota"],["Sheridan County","North Dakota"],["Greeley County","Kansas"],["Harding County","South Dakota"],["Issaquena County","Mississippi"],["Sterling County","Texas"],["Campbell County","South Dakota"],["Jackson County","Colorado"],["Cottle County","Texas"],["Carter County","Montana"],["Edwards County","Texas"],["Briscoe County","Texas"],["Piute County","Utah"],["Throckmorton County","Texas"],["Kiowa County","Colorado"],["Sully County","South Dakota"],["Wheeler County","Oregon"],["Wallace County","Kansas"],["Irion County","Texas"],["Taliaferro County","Georgia"],["Lane County","Kansas"],["Dundy County","Nebraska"],["Daniels County","Montana"],["Jerauld County","South Dakota"],["Comanche County","Kansas"],["Powder River County","Montana"],["De Baca County","New Mexico"],["Hodgeman County","Kansas"],["McCone County","Montana"],["Golden Valley County","North Dakota"],["Cheyenne County","Colorado"],["Oldham County","Texas"],["Dickens County","Texas"],["Steele County","North Dakota"],["Boyd County","Nebraska"],["Garfield County","Nebraska"],["Deuel County","Nebraska"],["Armstrong County","Texas"],["Eureka County","Nevada"],["Sherman County","Oregon"],["Haakon County","South Dakota"],["Garden County","Nebraska"],["Logan County","North Dakota"],["Oliver County","North Dakota"],["Gosper County","Nebraska"],["Mellette County","South Dakota"],["Meagher County","Montana"],["Buffalo County","South Dakota"],["Liberty County","Montana"],["Menard County","Texas"],["Worth County","Missouri"],["Clark County","Kansas"],["Gilliam County","Oregon"],["Jeff Davis County","Texas"],["Judith Basin County","Montana"],["Keweenaw County","Michigan"],["Wheatland County","Montana"],["Stanton County","Kansas"],["Faulk County","South Dakota"],["Wichita County","Kansas"],["Towner County","North Dakota"],["Greeley County","Nebraska"],["Culberson County","Texas"],["Robertson County","Kentucky"],["Divide County","North Dakota"],["Adams County","North Dakota"],["Burke County","North Dakota"],["Highland County","Virginia"],["Quitman County","Georgia"],["Renville County","North Dakota"],["Garfield County","Washington"],["Cimarron County","Oklahoma"],["Miner County","South Dakota"],["Grant County","North Dakota"],["Griggs County","North Dakota"],["Dolores County","Colorado"],["Sanborn County","South Dakota"],["Eddy County","North Dakota"],["Webster County","Georgia"],["Kidder County","North Dakota"],["Sedgwick County","Colorado"],["McPherson County","South Dakota"],["Ziebach County","South Dakota"],["Graham County","Kansas"],["Sheridan County","Kansas"],["Schleicher County","Texas"],["Kiowa County","Kansas"],["Niobrara County","Wyoming"],["Potter County","South Dakota"],["Elk County","Kansas"],["Wayne County","Utah"],["Harmon County","Oklahoma"],["Hettinger County","North Dakota"],["Rich County","Utah"],["Hamilton County","Kansas"],["Frontier County","Nebraska"],["McIntosh County","North Dakota"],["Pawnee County","Nebraska"],["Cochran County","Texas"],["Rawlins County","Kansas"],["Chase County","Kansas"],["Butte County","Idaho"],["Cheyenne County","Kansas"],["Hitchcock County","Nebraska"],["Collingsworth County","Texas"],["Ness County","Kansas"],["Morton County","Kansas"],["Gove County","Kansas"],["Aurora County","South Dakota"],["Real County","Texas"],["Logan County","Kansas"],["Decatur County","Kansas"],["Sherman County","Texas"],["Jackson County","South Dakota"],["Trego County","Kansas"],["Hall County","Texas"],["Douglas County","South Dakota"],["Perkins County","South Dakota"],["Clay County","Georgia"],["Perkins County","Nebraska"],["Baker County","Georgia"],["Glascock County","Georgia"],["Franklin County","Nebraska"],["Brown County","Nebraska"],["Edwards County","Kansas"],["Jewell County","Kansas"],["Lincoln County","Kansas"],["Rush County","Kansas"],["Sherman County","Nebraska"],["Stanley County","South Dakota"],["Bowman County","North Dakota"],["Nelson County","North Dakota"],["Fallon County","Montana"],["Lipscomb County","Texas"],["Harlan County","Nebraska"],["Crockett County","Texas"],["Shackelford County","Texas"],["Woodson County","Kansas"],["Kinney County","Texas"],["Hand County","South Dakota"],["Hudspeth County","Texas"],["Sierra County","California"],["Tyrrell County","North Carolina"],["Donley County","Texas"],["Harper County","Oklahoma"],["Coke County","Texas"],["Emmons County","North Dakota"],["Concho County","Texas"],["Upton County","Texas"],["Granite County","Montana"],["Knox County","Texas"],["Traverse County","Minnesota"],["Sutton County","Texas"],["Chautauqua County","Kansas"],["Nance County","Nebraska"],["Bennett County","South Dakota"],["Hemphill County","Texas"],["Reagan County","Texas"],["Webster County","Nebraska"],["Foster County","North Dakota"],["Kimball County","Nebraska"],["Roger Mills County","Oklahoma"],["Hanson County","South Dakota"],["Baylor County","Texas"],["Costilla County","Colorado"],["Osborne County","Kansas"],["Baca County","Colorado"],["Lewis County","Idaho"],["Mercer County","Missouri"],["Sheridan County","Montana"],["Hardeman County","Texas"],["Smith County","Kansas"],["Catron County","New Mexico"],["Hardin County","Illinois"],["Fisher County","Texas"],["Sweet Grass County","Montana"],["Echols County","Georgia"],["Adams County","Iowa"],["Cavalier County","North Dakota"],["Lyman County","South Dakota"],["Knox County","Missouri"],["Ellis County","Oklahoma"],["Pope County","Illinois"],["Lake of the Woods County","Minnesota"],["Lake of the Woods County","Minnesota"],["Haskell County","Kansas"],["Sharkey County","Mississippi"],["Clark County","South Dakota"],["Sargent County","North Dakota"],["Chase County","Nebraska"],["Sioux County","North Dakota"],["Corson County","South Dakota"],["Red Lake County","Minnesota"],["Columbia County","Washington"],["Mason County","Texas"],["Wells County","North Dakota"],["Kearny County","Kansas"],["Edmunds County","South Dakota"],["Pierce County","North Dakota"],["Gregory County","South Dakota"],["Schuyler County","Missouri"],["Owsley County","Kentucky"],["Meade County","Kansas"],["Valley County","Nebraska"],["Stafford County","Kansas"],["Union County","New Mexico"],["LaMoure County","North Dakota"],["Nuckolls County","Nebraska"],["Dunn County","North Dakota"],["Storey County","Nevada"],["Tensas Parish","Louisiana"],["Grant County","Oklahoma"],["Hidalgo County","New Mexico"],["Mora County","New Mexico"],["Kittson County","Minnesota"],["Bath County","Virginia"],["Phillips County","Montana"],["Holt County","Missouri"],["Barber County","Kansas"],["Menominee County","Wisconsin"],["Custer County","Idaho"],["Kimble County","Texas"],["Deuel County","South Dakota"],["Marshall County","South Dakota"],["Adams County","Idaho"],["Wahkiakum County","Washington"],["Calhoun County","Illinois"],["Guadalupe County","New Mexico"],["Mills County","Texas"],["Dewey County","Oklahoma"],["Lincoln County","Nevada"],["Hickman County","Kentucky"],["Phillips County","Colorado"],["Mineral County","Montana"],["Schley County","Georgia"],["Cameron County","Pennsylvania"],["Mineral County","Nevada"],["Morrill County","Nebraska"],["Florence County","Wisconsin"],["Oneida County","Idaho"],["Hyde County","North Carolina"],["Hot Springs County","Wyoming"],["Furnas County","Nebraska"],["Ringgold County","Iowa"],["Republic County","Kansas"],["Crane County","Texas"],["Putnam County","Missouri"],["Custer County","Colorado"],["Scotland County","Missouri"],["Musselshell County","Montana"],["Calhoun County","Arkansas"],["Washington County","Colorado"],["Carlisle County","Kentucky"],["Jim Hogg County","Texas"],["Jim Hogg County","Texas"],["Ouray County","Colorado"],["Craig County","Virginia"],["Rooks County","Kansas"],["Gallatin County","Illinois"],["Scott County","Illinois"],["Toole County","Montana"],["Phillips County","Kansas"],["Wheeler County","Texas"],["Dickey County","North Dakota"],["Pickett County","Tennessee"],["Thayer County","Nebraska"],["Beaver County","Oklahoma"],["Garfield County","Utah"],["Hamilton County","New York"],["Lincoln County","Idaho"],["Sheridan County","Nebraska"],["Crosby County","Texas"],["Scott County","Kansas"],["Big Stone County","Minnesota"],["Kingsbury County","South Dakota"],["Pulaski County","Illinois"],["Wirt County","West Virginia"],["Carter County","Missouri"],["Polk County","Nebraska"],["Warren County","Georgia"],["Delta County","Texas"],["Martin County","Texas"],["Dewey County","South Dakota"],["Alexander County","Illinois"],["Brule County","South Dakota"],["Stevens County","Kansas"],["Coal County","Oklahoma"],["Hansford County","Texas"],["Johnson County","Nebraska"],["Atchison County","Missouri"],["Stewart County","Georgia"],["Walworth County","South Dakota"],["Jefferson County","Oklahoma"],["Luce County","Michigan"],["McHenry County","North Dakota"],["Boone County","Nebraska"],["Hartley County","Texas"],["Morris County","Kansas"],["Stark County","Illinois"],["Floyd County","Texas"],["Mahnomen County","Minnesota"],["Haskell County","Texas"],["Day County","South Dakota"],["Cherry County","Nebraska"],["Norton County","Kansas"],["Harper County","Kansas"],["Greer County","Oklahoma"],["Cotton County","Oklahoma"],["Washington County","Kansas"],["Fillmore County","Nebraska"],["Calhoun County","Georgia"],["Lynn County","Texas"],["Cook County","Minnesota"],["Dixon County","Nebraska"],["Cameron Parish","Louisiana"],["Tripp County","South Dakota"],["Putnam County","Illinois"],["Lincoln County","Minnesota"],["Bent County","Colorado"],["Gray County","Kansas"],["Audubon County","Iowa"],["Lincoln County","Colorado"],["McCook County","South Dakota"],["Alfalfa County","Oklahoma"],["Ransom County","North Dakota"],["San Saba County","Texas"],["San Saba County","Texas"],["San Saba County","Texas"],["San Saba County","Texas"],["Talbot County","Georgia"],["Lander County","Nevada"],["Ottawa County","Kansas"],["Mitchell County","Kansas"],["Carson County","Texas"],["Gilpin County","Colorado"],["Ontonagon County","Michigan"],["Garza County","Texas"],["Sullivan County","Pennsylvania"],["Stanton County","Nebraska"],["Cumberland County","Kentucky"],["Chouteau County","Montana"],["Taylor County","Iowa"],["Pondera County","Montana"],["Essex County","Vermont"],["Crowley County","Colorado"],["Sherman County","Kansas"],["Ohio County","Indiana"],["Benson County","North Dakota"],["Sullivan County","Missouri"],["Miller County","Georgia"],["Greenwood County","Kansas"],["Grant County","Minnesota"],["Reynolds County","Missouri"],["Shelby County","Missouri"],["Clay County","Nebraska"],["Menifee County","Kentucky"],["Presidio County","Texas"],["Iron County","Wisconsin"],["Pendleton County","West Virginia"],["Gentry County","Missouri"],["Hamlin County","South Dakota"],["Van Buren County","Tennessee"],["Quitman County","Mississippi"],["Osceola County","Iowa"],["Teton County","Montana"],["Calhoun County","West Virginia"],["Brown County","Illinois"],["Edwards County","Illinois"],["Pawnee County","Kansas"],["Woodruff County","Arkansas"],["Bland County","Virginia"],["Antelope County","Nebraska"],["Lafayette County","Arkansas"],["Moody County","South Dakota"],["Spink County","South Dakota"],["Saguache County","Colorado"],["Bear Lake County","Idaho"],["Ellsworth County","Kansas"],["Bottineau County","North Dakota"],["Henderson County","Illinois"],["Treutlen County","Georgia"],["Randolph County","Georgia"],["Norman County","Minnesota"],["Moore County","Tennessee"],["Howard County","Nebraska"],["Dallas County","Arkansas"],["Wayne County","Iowa"],["Wilkin County","Minnesota"],["Fulton County","Kentucky"],["Rio Blanco County","Colorado"],["Rio Blanco County","Colorado"],["Surry County","Virginia"],["Wolfe County","Kentucky"],["Fremont County","Iowa"],["King and Queen County","Virginia"],["King and Queen County","Virginia"],["King and Queen County","Virginia"],["Clark County","Missouri"],["Pershing County","Nevada"],["Hancock County","Tennessee"],["Childress County","Texas"],["La Salle County","Texas"],["Kearney County","Nebraska"],["Russell County","Kansas"],["Lac qui Parle County","Minnesota"],["Burt County","Nebraska"],["Refugio County","Texas"],["Clinch County","Georgia"],["Tucker County","West Virginia"],["Thurston County","Nebraska"],["Charles City County","Virginia"],["Broadwater County","Montana"],["Monroe County","Arkansas"],["Huerfano County","Colorado"],["Weston County","Wyoming"],["Pembina County","North Dakota"],["Wabaunsee County","Kansas"],["Schuyler County","Illinois"],["Bailey County","Texas"],["Powell County","Montana"],["Tillman County","Oklahoma"],["Swisher County","Texas"],["Forest County","Pennsylvania"],["Fall River County","South Dakota"],["Bon Homme County","South Dakota"],["Ida County","Iowa"],["Lake County","Tennessee"],["Goliad County","Texas"],["Caribou County","Idaho"],["Shannon County","Missouri"],["Blaine County","Montana"],["Beaver County","Utah"],["Nemaha County","Nebraska"],["Brooks County","Texas"],["Pocahontas County","Iowa"],["Kit Carson County","Colorado"],["Union County","Indiana"],["Dallam County","Texas"],["Ferry County","Washington"],["Crook County","Wyoming"],["Van Buren County","Iowa"],["Newton County","Arkansas"],["Grant County","Oregon"],["Jefferson County","Nebraska"],["Jefferson County","Mississippi"],["Jefferson County","Mississippi"],["Grand Isle County","Vermont"],["Pierce County","Nebraska"],["Pepin County","Wisconsin"],["Rappahannock County","Virginia"],["Grant County","Kansas"],["Elliott County","Kentucky"],["Castro County","Texas"],["Wallowa County","Oregon"],["Lee County","Kentucky"],["Chariton County","Missouri"],["Gilmer County","West Virginia"],["Hutchinson County","South Dakota"],["Lake County","Colorado"],["Worth County","Iowa"],["East Carroll Parish","Louisiana"],["East Carroll Parish","Louisiana"],["East Carroll Parish","Louisiana"],["Conejos County","Colorado"],["Kingman County","Kansas"],["Wheeler County","Georgia"],["Harney County","Oregon"],["Adair County","Iowa"],["Marion County","Georgia"],["Doniphan County","Kansas"],["Nicholas County","Kentucky"],["Cleveland County","Arkansas"],["Grant County","South Dakota"],["Dade County","Missouri"],["Monroe County","Iowa"],["Valley County","Montana"],["Clay County","Tennessee"],["Boise County","Idaho"],["Red River Parish","Louisiana"],["McCulloch County","Texas"],["Decatur County","Iowa"],["Benton County","Mississippi"],["Pleasants County","West Virginia"],["Kane County","Utah"],["Merrick County","Nebraska"],["Franklin County","Mississippi"],["Coleman County","Texas"],["Washakie County","Wyoming"],["Lincoln County","Georgia"],["Yoakum County","Texas"],["Ballard County","Kentucky"],["Greene County","Alabama"],["Major County","Oklahoma"],["Humphreys County","Mississippi"],["Winkler County","Texas"],["Doddridge County","West Virginia"],["Taylor County","Georgia"],["Searcy County","Arkansas"],["Anderson County","Kansas"],["Pocahontas County","West Virginia"],["Richardson County","Nebraska"],["Power County","Idaho"],["San Augustine County","Texas"],["San Augustine County","Texas"],["San Augustine County","Texas"],["San Augustine County","Texas"],["Thomas County","Kansas"],["Liberty County","Florida"],["Lemhi County","Idaho"],["Hamilton County","Illinois"],["Traill County","North Dakota"],["Twiggs County","Georgia"],["Graham County","North Carolina"],["Allendale County","South Carolina"],["Schoolcraft County","Michigan"],["Clay County","West Virginia"],["San Miguel County","Colorado"],["San Miguel County","Colorado"],["Clay County","Kansas"],["Harrison County","Missouri"],["Baraga County","Michigan"],["Lake County","Oregon"],["Murray County","Minnesota"],["Franklin city","Virginia"],["Dawes County","Nebraska"],["Oscoda County","Michigan"],["Hamilton County","Texas"],["Lafayette County","Florida"],["Choctaw County","Mississippi"],["Hickory County","Missouri"],["Prairie County","Arkansas"],["Houston County","Tennessee"],["Atkinson County","Georgia"],["Nevada County","Arkansas"],["Tyler County","West Virginia"],["Custer County","South Dakota"],["Rosebud County","Montana"],["Keith County","Nebraska"],["Mercer County","North Dakota"],["Coffey County","Kansas"],["Perry County","Tennessee"],["Butler County","Nebraska"],["Webster County","West Virginia"],["Cedar County","Nebraska"],["Knox County","Nebraska"],["Bracken County","Kentucky"],["Daviess County","Missouri"],["Maries County","Missouri"],["Warren County","Indiana"],["Ritchie County","West Virginia"],["Johnson County","Wyoming"],["Jack County","Texas"],["Trimble County","Kentucky"],["Montgomery County","Arkansas"],["Carroll County","Missouri"],["Kiowa County","Oklahoma"],["Perry County","Alabama"],["Clearwater County","Minnesota"],["Mathews County","Virginia"],["Ozark County","Missouri"],["Archer County","Texas"],["Wilkinson County","Mississippi"],["Lee County","Arkansas"],["Platte County","Wyoming"],["Montgomery County","Georgia"],["Dimmit County","Texas"],["Madison County","Montana"],["Wilson County","Kansas"],["Woods County","Oklahoma"],["Lucas County","Iowa"],["Oregon County","Missouri"],["Monroe County","Missouri"],["Turner County","South Dakota"],["Jenkins County","Georgia"],["Lyon County","Kentucky"],["Gallatin County","Kentucky"],["Modoc County","California"],["Benton County","Indiana"],["Sublette County","Wyoming"],["Clearwater County","Idaho"],["Hancock County","Georgia"],["Blaine County","Oklahoma"],["Quay County","New Mexico"],["Monona County","Iowa"],["Wilcox County","Georgia"],["Greene County","Iowa"],["Caldwell County","Missouri"],["Alger County","Michigan"],["Wilkinson County","Georgia"],["Livingston County","Kentucky"],["Catahoula Parish","Louisiana"],["Richmond County","Virginia"],["Dawson County","Montana"],["Stillwater County","Montana"],["Phelps County","Nebraska"],["Kemper County","Mississippi"],["Crittenden County","Kentucky"],["Mitchell County","Texas"],["Palo Alto County","Iowa"],["Turner County","Georgia"],["Cuming County","Nebraska"],["Cloud County","Kansas"],["Marshall County","Minnesota"],["White Pine County","Nevada"],["Hancock County","Kentucky"],["Stephens County","Texas"],["Davis County","Iowa"],["Claiborne County","Mississippi"],["Seminole County","Georgia"],["McLean County","Kentucky"],["Montmorency County","Michigan"],["Pratt County","Kansas"],["Jones County","North Carolina"],["Forest County","Wisconsin"],["Terrell County","Georgia"],["Johnson County","Georgia"],["Somervell County","Texas"],["Clinton County","Kentucky"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["Jasper County","Illinois"],["Todd County","South Dakota"],["Nowata County","Oklahoma"],["Beaverhead County","Montana"],["Charles Mix County","South Dakota"],["Emmet County","Iowa"],["Clear Creek County","Colorado"],["Deer Lodge County","Montana"],["Pipestone County","Minnesota"],["Rice County","Kansas"],["Hamilton County","Nebraska"],["Latimer County","Oklahoma"],["Cheyenne County","Nebraska"],["Howard County","Iowa"],["Brown County","Kansas"],["McCormick County","South Carolina"],["Yellow Medicine County","Minnesota"],["Benewah County","Idaho"],["Iron County","Missouri"],["Brewster County","Texas"],["Greenlee County","Arizona"],["Chattahoochee County","Georgia"],["Wilkes County","Georgia"],["Linn County","Kansas"],["Humboldt County","Iowa"],["Caldwell Parish","Louisiana"],["Irwin County","Georgia"],["Grand County","Utah"],["Zavala County","Texas"],["Stevens County","Minnesota"],["Cumberland County","Virginia"],["Wayne County","Nebraska"],["Rock County","Minnesota"],["Marion County","Texas"],["Switzerland County","Indiana"],["Clarke County","Iowa"],["West Carroll Parish","Louisiana"],["West Carroll Parish","Louisiana"],["West Carroll Parish","Louisiana"],["McLean County","North Dakota"],["Tunica County","Mississippi"],["Grundy County","Missouri"],["Mountrail County","North Dakota"],["Martin County","Indiana"],["Sac County","Iowa"],["Montgomery County","Mississippi"],["Emery County","Utah"],["Duval County","Texas"],["Scott County","Arkansas"],["Swift County","Minnesota"],["Pulaski County","Georgia"],["Parmer County","Texas"],["Lanier County","Georgia"],["Sabine County","Texas"],["Runnels County","Texas"],["Webster County","Mississippi"],["Calhoun County","Iowa"],["Yuma County","Colorado"],["Jackson County","Minnesota"],["Carroll County","Mississippi"],["Ochiltree County","Texas"],["Madison Parish","Louisiana"],["Perry County","Arkansas"],["Franklin County","Iowa"],["Lewis County","Missouri"],["Keokuk County","Iowa"],["Marshall County","Kansas"],["Holt County","Nebraska"],["Love County","Oklahoma"],["Howard County","Missouri"],["Alcona County","Michigan"],["Pike County","Arkansas"],["Chicot County","Arkansas"],["Clay County","Texas"],["Butte County","South Dakota"],["Johnston County","Oklahoma"],["Nemaha County","Kansas"],["Roberts County","South Dakota"],["Noxubee County","Mississippi"],["Metcalfe County","Kentucky"],["Lowndes County","Alabama"],["Montgomery County","Iowa"],["Ralls County","Missouri"],["Camden County","North Carolina"],["Bullock County","Alabama"],["Franklin County","Texas"],["Coosa County","Alabama"],["Cumberland County","Illinois"],["Carbon County","Montana"],["Gates County","North Carolina"],["Washington County","Idaho"],["Leslie County","Kentucky"],["Crawford County","Indiana"],["Bradley County","Arkansas"],["Custer County","Nebraska"],["Walsh County","North Dakota"],["Mitchell County","Iowa"],["Bollinger County","Missouri"],["Colfax County","Nebraska"],["Essex County","Virginia"],["Wilcox County","Alabama"],["Guthrie County","Iowa"],["Middlesex County","Virginia"],["Winnebago County","Iowa"],["Ripley County","Missouri"],["Red Willow County","Nebraska"],["Evans County","Georgia"],["Roosevelt County","Montana"],["Hancock County","Iowa"],["Carroll County","Kentucky"],["Pushmataha County","Oklahoma"],["Sussex County","Virginia"],["Mackinac County","Michigan"],["Louisa County","Iowa"],["Box Butte County","Nebraska"],["Barnes County","North Dakota"],["Early County","Georgia"],["Lincoln County","Washington"],["Alleghany County","North Carolina"],["Lake County","Minnesota"],["Lake County","Minnesota"],["Lancaster County","Virginia"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["Noble County","Oklahoma"],["Washita County","Oklahoma"],["Wayne County","Missouri"],["McIntosh County","Georgia"],["Grant County","West Virginia"],["Candler County","Georgia"],["Washington County","North Carolina"],["DeKalb County","Missouri"],["Lake County","South Dakota"],["Clay County","North Carolina"],["Green County","Kentucky"],["Bacon County","Georgia"],["Dooly County","Georgia"],["Watonwan County","Minnesota"],["Owen County","Kentucky"],["Martin County","Kentucky"],["Pope County","Minnesota"],["Okfuskee County","Oklahoma"],["Jefferson Davis County","Mississippi"],["Jefferson Davis County","Mississippi"],["Montgomery County","Missouri"],["Live Oak County","Texas"],["Monroe County","Kentucky"],["Wabash County","Illinois"],["Blanco County","Texas"],["Desha County","Arkansas"],["Heard County","Georgia"],["Decatur County","Tennessee"],["Fergus County","Montana"],["Richland County","Montana"],["Perry County","Mississippi"],["Cottonwood County","Minnesota"],["Big Horn County","Wyoming"],["Charlotte County","Virginia"],["Rio Grande County","Colorado"],["Rio Grande County","Colorado"],["Haskell County","Oklahoma"],["Sierra County","New Mexico"],["Douglas County","Missouri"],["Red River County","Texas"],["Conecuh County","Alabama"],["Ramsey County","North Dakota"],["Trousdale County","Tennessee"],["Jackson County","Tennessee"],["Teton County","Idaho"],["Iron County","Michigan"],["Magoffin County","Kentucky"],["Barton County","Missouri"],["Ward County","Texas"],["Cherokee County","Iowa"],["Marshall County","Illinois"],["Valley County","Idaho"],["Shelby County","Iowa"],["Juab County","Utah"],["Marion County","Kansas"],["Terry County","Texas"],["Northumberland County","Virginia"],["Custer County","Montana"],["Linn County","Missouri"],["Owyhee County","Idaho"],["Lyon County","Iowa"],["Lunenburg County","Virginia"],["Summers County","West Virginia"],["Morris County","Texas"],["Greene County","Illinois"],["Prowers County","Colorado"],["Chickasaw County","Iowa"],["Lawrence County","Mississippi"],["Little River County","Arkansas"],["Washington County","Kentucky"],["Skamania County","Washington"],["Boundary County","Idaho"],["Koochiching County","Minnesota"],["Fulton County","Arkansas"],["Macon County","Georgia"],["Jefferson County","Montana"],["Lake County","Michigan"],["Blackford County","Indiana"],["Glades County","Florida"],["Edmonson County","Kentucky"],["Crawford County","Georgia"],["Union County","Iowa"],["Rains County","Texas"],["Morrow County","Oregon"],["Rolette County","North Dakota"],["Newton County","Texas"],["Todd County","Kentucky"],["Pike County","Indiana"],["Pamlico County","North Carolina"],["Northampton County","Virginia"],["Morgan County","Utah"],["Menard County","Illinois"],["Appanoose County","Iowa"],["Grundy County","Iowa"],["Sumter County","Alabama"],["Stone County","Arkansas"],["Butler County","Kentucky"],["Monroe County","West Virginia"],["Colfax County","New Mexico"],["Sanders County","Montana"],["Braxton County","West Virginia"],["Franklin County","Florida"],["Dawson County","Texas"],["Camp County","Texas"],["Telfair County","Georgia"],["Yalobusha County","Mississippi"],["Towns County","Georgia"],["Goshen County","Wyoming"],["Pulaski County","Indiana"],["Charlton County","Georgia"],["Allen County","Kansas"],["Mississippi County","Missouri"],["Lewis County","Tennessee"],["Bleckley County","Georgia"],["Chippewa County","Minnesota"],["Madison County","Missouri"],["Caldwell County","Kentucky"],["Choctaw County","Alabama"],["Tallahatchie County","Mississippi"],["Amite County","Mississippi"],["Bath County","Kentucky"],["Meigs County","Tennessee"],["Howard County","Arkansas"],["Vinton County","Ohio"],["Wilbarger County","Texas"],["Lincoln County","Arkansas"],["Wright County","Iowa"],["Jackson County","Kentucky"],["Millard County","Utah"],["Bienville Parish","Louisiana"],["Presque Isle County","Michigan"],["Crawford County","Michigan"],["Perquimans County","North Carolina"],["Webster County","Kentucky"],["Cass County","Illinois"],["Lamb County","Texas"],["Lewis County","Kentucky"],["Mason County","Illinois"],["Big Horn County","Montana"],["Cass County","Iowa"],["Powell County","Kentucky"],["Shoshone County","Idaho"],["Crenshaw County","Alabama"],["Mono County","California"],["Jackson County","Kansas"],["Amelia County","Virginia"],["Calhoun County","Mississippi"],["Osage County","Missouri"],["Clay County","Illinois"],["Moffat County","Colorado"],["Johnson County","Illinois"],["Bamberg County","South Carolina"],["Buffalo County","Wisconsin"],["Archuleta County","Colorado"],["Hughes County","Oklahoma"],["Monroe County","Ohio"],["Fremont County","Idaho"],["Pend Oreille County","Washington"],["Madison County","Texas"],["Grundy County","Tennessee"],["Greene County","Mississippi"],["Ford County","Illinois"],["Izard County","Arkansas"],["Comanche County","Texas"],["Trinity County","Texas"],["Calhoun County","Florida"],["Stewart County","Tennessee"],["Union County","Kentucky"],["Oglala Lakota County","South Dakota"],["Chowan County","North Carolina"],["Callahan County","Texas"],["Breathitt County","Kentucky"],["Morgan County","Kentucky"],["Converse County","Wyoming"],["Winn Parish","Louisiana"],["Washington County","Illinois"],["Glacier County","Montana"],["Morgan County","Ohio"],["Newton County","Indiana"],["Madison County","Virginia"],["White County","Illinois"],["Walthall County","Mississippi"],["Zapata County","Texas"],["Murray County","Oklahoma"],["Crockett County","Tennessee"],["Faribault County","Minnesota"],["Lamar County","Alabama"],["Pennington County","Minnesota"],["Hamilton County","Florida"],["Roane County","West Virginia"],["Price County","Wisconsin"],["Allamakee County","Iowa"],["Trigg County","Kentucky"],["Wadena County","Minnesota"],["Screven County","Georgia"],["Craig County","Oklahoma"],["Noble County","Ohio"],["Swain County","North Carolina"],["Calhoun County","South Carolina"],["Dickenson County","Virginia"],["York County","Nebraska"],["Atoka County","Oklahoma"],["Estill County","Kentucky"],["Massac County","Illinois"],["Claiborne Parish","Louisiana"],["O'Brien County","Iowa"],["Cedar County","Missouri"],["Rusk County","Wisconsin"],["Gulf County","Florida"],["Franklin County","Idaho"],["Choctaw County","Oklahoma"],["Smith County","Mississippi"],["Clay County","Alabama"],["Knott County","Kentucky"],["Nantucket County","Massachusetts"],["Saline County","Nebraska"],["Hardy County","West Virginia"],["Butler County","Iowa"],["Bourbon County","Kansas"],["Gogebic County","Michigan"],["Dent County","Missouri"],["Wetzel County","West Virginia"],["Harrison County","Ohio"],["Mills County","Iowa"],["Cannon County","Tennessee"],["Jefferson County","Florida"],["San Juan County","Utah"],["Moultrie County","Illinois"],["Carbon County","Wyoming"],["Clay County","Arkansas"],["Las Animas County","Colorado"],["Fulton County","Pennsylvania"],["Livingston County","Missouri"],["Harrison County","Iowa"],["Jasper County","Georgia"],["Pendleton County","Kentucky"],["McKenzie County","North Dakota"],["Karnes County","Texas"],["Renville County","Minnesota"],["Nolan County","Texas"],["Pike County","Illinois"],["Reeves County","Texas"],["Nelson County","Virginia"],["Jeff Davis County","Georgia"],["Clarke County","Virginia"],["Hale County","Alabama"],["LaSalle Parish","Louisiana"],["Gasconade County","Missouri"],["Oglethorpe County","Georgia"],["Kossuth County","Iowa"],["Sibley County","Minnesota"],["Larue County","Kentucky"],["Mitchell County","North Carolina"],["Bledsoe County","Tennessee"],["Clay County","South Dakota"],["Jackson County","Texas"],["Arenac County","Michigan"],["Jackson Parish","Louisiana"],["Hamilton County","Iowa"],["Torrance County","New Mexico"],["Missaukee County","Michigan"],["Cleburne County","Alabama"],["Fleming County","Kentucky"],["Kingfisher County","Oklahoma"],["Pecos County","Texas"],["Macon County","Missouri"],["Page County","Iowa"],["Lawrence County","Illinois"],["West Feliciana Parish","Louisiana"],["West Feliciana Parish","Louisiana"],["West Feliciana Parish","Louisiana"],["Marshall County","Oklahoma"],["Roseau County","Minnesota"],["Grayson County","Virginia"],["Tipton County","Indiana"],["Washington County","Alabama"],["Redwood County","Minnesota"],["Vermillion County","Indiana"],["Clark County","Illinois"],["Barbour County","West Virginia"],["Moniteau County","Missouri"],["Brown County","Indiana"],["Floyd County","Virginia"],["De Witt County","Illinois"],["Pawnee County","Oklahoma"],["Marquette County","Wisconsin"],["Gooding County","Idaho"],["Clarke County","Mississippi"],["Floyd County","Iowa"],["Nottoway County","Virginia"],["Pemiscot County","Missouri"],["Jefferson County","Iowa"],["Henry County","Kentucky"],["Aitkin County","Minnesota"],["Mercer County","Illinois"],["Carroll County","Illinois"],["Jefferson County","Georgia"],["Grand County","Colorado"],["Leon County","Texas"],["Osage County","Kansas"],["Van Buren County","Arkansas"],["Richland County","Illinois"],["Sequatchie County","Tennessee"],["Sevier County","Arkansas"],["Brunswick County","Virginia"],["Benton County","Tennessee"],["Neosho County","Kansas"],["Otoe County","Nebraska"],["Casey County","Kentucky"],["Ashland County","Wisconsin"],["Kanabec County","Minnesota"],["Rockcastle County","Kentucky"],["Bates County","Missouri"],["Trinity County","California"],["Crawford County","Wisconsin"],["Appomattox County","Virginia"],["Union County","Florida"],["Parke County","Indiana"],["Long County","Georgia"],["Wayne County","Illinois"],["Lawrence County","Arkansas"],["Bayfield County","Wisconsin"],["Wayne County","Tennessee"],["Dade County","Georgia"],["Lawrence County","Kentucky"],["Brooks County","Georgia"],["Hill County","Montana"],["Fayette County","Alabama"],["Atchison County","Kansas"],["Jasper County","Mississippi"],["Alamosa County","Colorado"],["Clay County","Iowa"],["Potter County","Pennsylvania"],["New Madrid County","Missouri"],["Fountain County","Indiana"],["Madison County","Arkansas"],["Crawford County","Iowa"],["Burnett County","Wisconsin"],["Richland County","North Dakota"],["Lee County","South Carolina"],["Madison County","Iowa"],["La Paz County","Arizona"],["Phillips County","Arkansas"],["Socorro County","New Mexico"],["Lafayette County","Wisconsin"],["Washburn County","Wisconsin"],["Baker County","Oregon"],["Piatt County","Illinois"],["Taylor County","West Virginia"],["Bond County","Illinois"],["Rush County","Indiana"],["Jackson County","Arkansas"],["Robertson County","Texas"],["Dixie County","Florida"],["Giles County","Virginia"],["Piscataquis County","Maine"],["Union County","South Dakota"],["Buckingham County","Virginia"],["Marion County","Arkansas"],["Cross County","Arkansas"],["Warren County","Illinois"],["Edgar County","Illinois"],["Hardin County","Iowa"],["Rabun County","Georgia"],["McCreary County","Kentucky"],["Gunnison County","Colorado"],["Scurry County","Texas"],["Garrard County","Kentucky"],["Falls County","Texas"],["Holmes County","Mississippi"],["Lewis County","West Virginia"],["Clayton County","Iowa"],["Morgan County","West Virginia"],["Dallas County","Missouri"],["Franklin County","Arkansas"],["Cooper County","Missouri"],["Chickasaw County","Mississippi"],["Mason County","Kentucky"],["Mariposa County","California"],["Tama County","Iowa"],["Henry County","Alabama"],["Park County","Montana"],["Ben Hill County","Georgia"],["Cook County","Georgia"],["Union County","Illinois"],["Sharp County","Arkansas"],["Humboldt County","Nevada"],["Richland County","Wisconsin"],["Chester County","Tennessee"],["Drew County","Arkansas"],["Pitkin County","Colorado"],["Park County","Colorado"],["Northampton County","North Carolina"],["Lee County","Texas"],["Delaware County","Iowa"],["Polk County","Tennessee"],["Pike County","Missouri"],["Patrick County","Virginia"],["Seward County","Nebraska"],["Hancock County","Illinois"],["Burleson County","Texas"],["Dickinson County","Iowa"],["Winston County","Mississippi"],["Eastland County","Texas"],["Hughes County","South Dakota"],["San Juan County","Washington"],["Avery County","North Carolina"],["King William County","Virginia"],["King William County","Virginia"],["King William County","Virginia"],["Gilchrist County","Florida"],["Haywood County","Tennessee"],["Young County","Texas"],["Attala County","Mississippi"],["Schuyler County","New York"],["Unicoi County","Tennessee"],["Bertie County","North Carolina"],["Kalkaska County","Michigan"],["Johnson County","Tennessee"],["Grant County","Arkansas"],["Madison County","Florida"],["Benzie County","Michigan"],["Russell County","Kentucky"],["Brantley County","Georgia"],["Banks County","Georgia"],["Sawyer County","Wisconsin"],["Andrew County","Missouri"],["Montour County","Pennsylvania"],["Berrien County","Georgia"],["Wright County","Missouri"],["Bosque County","Texas"],["Stone County","Mississippi"],["Covington County","Mississippi"],["Jefferson County","Kansas"],["Frio County","Texas"],["Dickinson County","Kansas"],["Appling County","Georgia"],["Yancey County","North Carolina"],["Westmoreland County","Virginia"],["Ste. Genevieve County","Missouri"],["Fentress County","Tennessee"],["Lamar County","Georgia"],["Cedar County","Iowa"],["Hampton County","South Carolina"],["Randolph County","Arkansas"],["Deaf Smith County","Texas"],["Andrews County","Texas"],["Clay County","Mississippi"],["Warren County","North Carolina"],["Poweshiek County","Iowa"],["Crawford County","Illinois"],["Concordia Parish","Louisiana"],["Otero County","Colorado"],["Harrison County","Kentucky"],["Paulding County","Ohio"],["Houston County","Minnesota"],["Tishomingo County","Mississippi"],["Saluda County","South Carolina"],["Pike County","Georgia"],["Adair County","Kentucky"],["Greene County","Georgia"],["McIntosh County","Oklahoma"],["Perry County","Missouri"],["Waseca County","Minnesota"],["Humphreys County","Tennessee"],["Inyo County","California"],["Green Lake County","Wisconsin"],["Green Lake County","Wisconsin"],["Butler County","Alabama"],["Ashley County","Arkansas"],["McDowell County","West Virginia"],["Pickens County","Alabama"],["Gem County","Idaho"],["Beadle County","South Dakota"],["Perry County","Indiana"],["Roosevelt County","New Mexico"],["Kent County","Maryland"],["Polk County","Arkansas"],["Hart County","Kentucky"],["Marengo County","Alabama"],["Polk County","North Carolina"],["Cherokee County","Kansas"],["Benton County","Missouri"],["Los Alamos County","New Mexico"],["Freestone County","Texas"],["Chaffee County","Colorado"],["Jackson County","Iowa"],["Spencer County","Kentucky"],["Langlade County","Wisconsin"],["Adair County","Oklahoma"],["Fayette County","Iowa"],["Macon County","Alabama"],["East Feliciana Parish","Louisiana"],["East Feliciana Parish","Louisiana"],["East Feliciana Parish","Louisiana"],["Wayne County","Kentucky"],["Marion County","Kentucky"],["Lincoln County","Wyoming"],["Simpson County","Kentucky"],["Duchesne County","Utah"],["Elbert County","Georgia"],["Holmes County","Florida"],["Gonzales County","Texas"],["Jones County","Texas"],["Lincoln County","Montana"],["Vernon County","Missouri"],["Pierce County","Georgia"],["Douglas County","Illinois"],["Monroe County","Alabama"],["Franklin Parish","Louisiana"],["Wayne County","Mississippi"],["Plumas County","California"],["Tyler County","Texas"],["Union County","Tennessee"],["Spencer County","Indiana"],["DeWitt County","Texas"],["Orange County","Indiana"],["Smith County","Tennessee"],["Taylor County","Wisconsin"],["Dodge County","Georgia"],["Davison County","South Dakota"],["Montague County","Texas"],["Washington County","Georgia"],["Martin County","Minnesota"],["Richland Parish","Louisiana"],["Hempstead County","Arkansas"],["Winneshiek County","Iowa"],["DeKalb County","Tennessee"],["Morgan County","Georgia"],["Calhoun County","Texas"],["Crisp County","Georgia"],["Willacy County","Texas"],["Labette County","Kansas"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["Bourbon County","Kentucky"],["Yell County","Arkansas"],["Lincoln County","New Mexico"],["Carroll County","Indiana"],["Lavaca County","Texas"],["Clay County","Kentucky"],["Buchanan County","Virginia"],["Carbon County","Utah"],["Breckinridge County","Kentucky"],["Uinta County","Wyoming"],["Greene County","North Carolina"],["Lincoln County","West Virginia"],["Woodward County","Oklahoma"],["Jay County","Indiana"],["Fulton County","Indiana"],["Henry County","Iowa"],["Greene County","Virginia"],["Colorado County","Texas"],["Kewaunee County","Wisconsin"],["Buchanan County","Iowa"],["Allen County","Kentucky"],["Barnwell County","South Carolina"],["Dukes County","Massachusetts"],["Meriwether County","Georgia"],["Adams County","Washington"],["Hutchinson County","Texas"],["Jones County","Iowa"],["Adams County","Wisconsin"],["Conway County","Arkansas"],["Pointe Coupee Parish","Louisiana"],["Carroll County","Iowa"],["Ogemaw County","Michigan"],["Worth County","Georgia"],["Sullivan County","Indiana"],["Buena Vista County","Iowa"],["Bandera County","Texas"],["Washington County","Nebraska"],["Dodge County","Minnesota"],["Perry County","Illinois"],["Fairfield County","South Carolina"],["Shelby County","Illinois"],["Morgan County","Missouri"],["Morgan County","Tennessee"],["Assumption Parish","Louisiana"],["Union Parish","Louisiana"],["Logan County","Arkansas"],["Jackson County","Wisconsin"],["Clinton County","Missouri"],["Madison County","North Carolina"],["Gray County","Texas"],["Fillmore County","Minnesota"],["Nodaway County","Missouri"],["Llano County","Texas"],["Leake County","Mississippi"],["Newton County","Mississippi"],["Owen County","Indiana"],["Hubbard County","Minnesota"],["Moore County","Texas"],["Wyoming County","West Virginia"],["Texas County","Oklahoma"],["Wabasha County","Minnesota"],["Coahoma County","Mississippi"],["Clark County","Arkansas"],["Fayette County","Illinois"],["Jersey County","Illinois"],["Sevier County","Utah"],["Logan County","Colorado"],["Hockley County","Texas"],["Letcher County","Kentucky"],["Hertford County","North Carolina"],["Scott County","Virginia"],["Dakota County","Nebraska"],["Stutsman County","North Dakota"],["Gaines County","Texas"],["Minidoka County","Idaho"],["Lampasas County","Texas"],["Grenada County","Mississippi"],["McDuffie County","Georgia"],["Gage County","Nebraska"],["Mitchell County","Georgia"],["Taylor County","Florida"],["Boone County","West Virginia"],["Tippah County","Mississippi"],["Colusa County","California"],["Prince Edward County","Virginia"],["Scott County","Tennessee"],["Wyandot County","Ohio"],["Henry County","Missouri"],["Seward County","Kansas"],["Randolph County","Alabama"],["Martin County","North Carolina"],["Jo Daviess County","Illinois"],["Putnam County","Georgia"],["Anson County","North Carolina"],["Houston County","Texas"],["Limestone County","Texas"],["Sabine Parish","Louisiana"],["Grant Parish","Louisiana"],["Lee County","Virginia"],["Mahaska County","Iowa"],["Meigs County","Ohio"],["Saunders County","Nebraska"],["Asotin County","Washington"],["Nobles County","Minnesota"],["Bibb County","Alabama"],["Leelanau County","Michigan"],["Sumner County","Kansas"],["Beckham County","Oklahoma"],["Panola County","Texas"],["Overton County","Tennessee"],["Brooke County","West Virginia"],["Washington County","Iowa"],["Mercer County","Kentucky"],["Ouachita County","Arkansas"],["Johnson County","Kentucky"],["Klickitat County","Washington"],["Caswell County","North Carolina"],["Allen Parish","Louisiana"],["Emanuel County","Georgia"],["Franklin County","Indiana"],["Columbia County","Arkansas"],["Tattnall County","Georgia"],["Osceola County","Michigan"],["New Kent County","Virginia"],["Poinsett County","Arkansas"],["Vilas County","Wisconsin"],["Crawford County","Missouri"],["Clarke County","Alabama"],["St. Francis County","Arkansas"],["Hampshire County","West Virginia"],["Ray County","Missouri"],["McDonald County","Missouri"],["Yankton County","South Dakota"],["Teton County","Wyoming"],["Saline County","Missouri"],["Pacific County","Washington"],["Starke County","Indiana"],["Fayette County","Indiana"],["Meeker County","Minnesota"],["Franklin County","Georgia"],["Antrim County","Michigan"],["Curry County","Oregon"],["Roscommon County","Michigan"],["Menominee County","Michigan"],["Juniata County","Pennsylvania"],["Washington County","Missouri"],["Plaquemines Parish","Louisiana"],["Grainger County","Tennessee"],["Winston County","Alabama"],["Seminole County","Oklahoma"],["Mingo County","West Virginia"],["Page County","Virginia"],["Iowa County","Wisconsin"],["Saline County","Illinois"],["Ohio County","Kentucky"],["Upshur County","West Virginia"],["Aransas County","Texas"],["Anderson County","Kentucky"],["Itawamba County","Mississippi"],["Hood River County","Oregon"],["Shelby County","Texas"],["Bell County","Kentucky"],["Dawson County","Nebraska"],["Jerome County","Idaho"],["Blaine County","Idaho"],["Lincoln County","Kentucky"],["Abbeville County","South Carolina"],["George County","Mississippi"],["Scott County","Indiana"],["Fayette County","Texas"],["Marion County","Mississippi"],["Texas County","Missouri"],["Randolph County","Indiana"],["Jefferson County","Oregon"],["Waushara County","Wisconsin"],["Uvalde County","Texas"],["Burke County","Georgia"],["Nicholas County","West Virginia"],["Somerset County","Maryland"],["Union County","Georgia"],["Cassia County","Idaho"],["Rowan County","Kentucky"],["White County","Indiana"],["Teller County","Colorado"],["Cleburne County","Arkansas"],["Randolph County","Missouri"],["Miller County","Missouri"],["Goochland County","Virginia"],["Crook County","Oregon"],["Milam County","Texas"],["Yates County","New York"],["Jackson County","Oklahoma"],["Routt County","Colorado"],["Hickman County","Tennessee"],["Grant County","Kentucky"],["Audrain County","Missouri"],["Chattooga County","Georgia"],["Cherokee County","Alabama"],["Bremer County","Iowa"],["Prentiss County","Mississippi"],["Manistee County","Michigan"],["Otsego County","Michigan"],["Lauderdale County","Tennessee"],["Macon County","Tennessee"],["Posey County","Indiana"],["Barbour County","Alabama"],["Iosco County","Michigan"],["Todd County","Minnesota"],["Lyon County","Minnesota"],["Adair County","Missouri"],["Washington County","Florida"],["Fannin County","Georgia"],["Hardee County","Florida"],["Pottawatomie County","Kansas"],["Payette County","Idaho"],["Gladwin County","Michigan"],["Luna County","New Mexico"],["Butts County","Georgia"],["Mason County","West Virginia"],["Hardeman County","Tennessee"],["Barton County","Kansas"],["Churchill County","Nevada"],["Benton County","Iowa"],["Cheboygan County","Michigan"],["Morehouse Parish","Louisiana"],["Garvin County","Oklahoma"],["Edgefield County","South Carolina"],["Plymouth County","Iowa"],["Johnson County","Arkansas"],["Montgomery County","North Carolina"],["Lawrence County","South Dakota"],["Russell County","Virginia"],["Hart County","Georgia"],["Montezuma County","Colorado"],["McNairy County","Tennessee"],["Brown County","Minnesota"],["Lamoille County","Vermont"],["Dickinson County","Michigan"],["Simpson County","Mississippi"],["Sunflower County","Mississippi"],["Franklin County","Kansas"],["Taylor County","Kentucky"],["Charlevoix County","Michigan"],["Elbert County","Colorado"],["Wyoming County","Pennsylvania"],["Union County","Oregon"],["Grady County","Georgia"],["Grayson County","Kentucky"],["Mille Lacs County","Minnesota"],["Clay County","Indiana"],["Decatur County","Indiana"],["Ashe County","North Carolina"],["Lewis County","New York"],["Cass County","Nebraska"],["Carter County","Kentucky"],["Geneva County","Alabama"],["Oceana County","Michigan"],["Marlboro County","South Carolina"],["Wasco County","Oregon"],["Boone County","Iowa"],["Juneau County","Wisconsin"],["Carroll County","Ohio"],["King George County","Virginia"],["King George County","Virginia"],["King George County","Virginia"],["Gillespie County","Texas"],["Yazoo County","Mississippi"],["Stephens County","Georgia"],["Dawson County","Georgia"],["De Soto Parish","Louisiana"],["Harlan County","Kentucky"],["Hardin County","Tennessee"],["Woodford County","Kentucky"],["Mineral County","West Virginia"],["Caddo County","Oklahoma"],["Toombs County","Georgia"],["Iroquois County","Illinois"],["Pike County","Ohio"],["Cibola County","New Mexico"],["West Baton Rouge Parish","Louisiana"],["West Baton Rouge Parish","Louisiana"],["West Baton Rouge Parish","Louisiana"],["San Miguel County","New Mexico"],["San Miguel County","New Mexico"],["McDonough County","Illinois"],["Union County","South Carolina"],["Fluvanna County","Virginia"],["White County","Tennessee"],["Tillamook County","Oregon"],["Orleans County","Vermont"],["San Jacinto County","Texas"],["San Jacinto County","Texas"],["San Jacinto County","Texas"],["San Jacinto County","Texas"],["Logan County","Kentucky"],["Adams County","Ohio"],["Jennings County","Indiana"],["Henry County","Ohio"],["Upson County","Georgia"],["Del Norte County","California"],["Union County","Mississippi"],["Jackson County","West Virginia"],["Henderson County","Tennessee"],["Randolph County","West Virginia"],["Monroe County","Georgia"],["Peach County","Georgia"],["Logan County","Illinois"],["Scott County","Mississippi"],["White County","Georgia"],["Hocking County","Ohio"],["Tate County","Mississippi"],["Currituck County","North Carolina"],["Montgomery County","Kentucky"],["Wells County","Indiana"],["Washington County","Indiana"],["Grant County","New Mexico"],["Baker County","Florida"],["Carroll County","Arkansas"],["Dunklin County","Missouri"],["Montgomery County","Illinois"],["Wythe County","Virginia"],["Dillon County","South Carolina"],["Bradford County","Florida"],["Codington County","South Dakota"],["Leflore County","Mississippi"],["Jones County","Georgia"],["Copiah County","Mississippi"],["Palo Pinto County","Texas"],["Lincoln County","Wisconsin"],["Sanpete County","Utah"],["Carroll County","Tennessee"],["Cass County","Texas"],["Perry County","Kentucky"],["Custer County","Oklahoma"],["Marion County","Missouri"],["Elmore County","Idaho"],["Stoddard County","Missouri"],["Le Sueur County","Minnesota"],["Cherokee County","North Carolina"],["Jasper County","South Carolina"],["Garrett County","Maryland"],["Marion County","Tennessee"],["Pine County","Minnesota"],["Alpena County","Michigan"],["Glenn County","California"],["Van Wert County","Ohio"],["Ellis County","Kansas"],["Fayette County","Ohio"],["Ripley County","Indiana"],["Mason County","Michigan"],["Neshoba County","Mississippi"],["Hancock County","West Virginia"],["Morgan County","Colorado"],["Marion County","South Carolina"],["Gallia County","Ohio"],["Grimes County","Texas"],["Orange County","Vermont"],["Marion County","Alabama"],["Decatur County","Georgia"],["Franklin County","Maine"],["Adams County","Mississippi"],["Bladen County","North Carolina"],["Sumter County","Georgia"],["Park County","Wyoming"],["Schoharie County","New York"],["Smyth County","Virginia"],["Meade County","South Dakota"],["Haralson County","Georgia"],["Meade County","Kentucky"],["Cass County","Minnesota"],["Door County","Wisconsin"],["Madison County","Georgia"],["Wayne County","Georgia"],["Randolph County","Illinois"],["Austin County","Texas"],["Knox County","Kentucky"],["McPherson County","Kansas"],["Caledonia County","Vermont"],["Iberville Parish","Louisiana"],["Ottawa County","Oklahoma"],["Mecklenburg County","Virginia"],["Powhatan County","Virginia"],["Giles County","Tennessee"],["Marshall County","West Virginia"],["Boyle County","Kentucky"],["Hardin County","Ohio"],["Vernon County","Wisconsin"],["Trempealeau County","Wisconsin"],["Obion County","Tennessee"],["Greene County","Indiana"],["McCurtain County","Oklahoma"],["Clare County","Michigan"],["Caroline County","Virginia"],["Jefferson County","Idaho"],["Freeborn County","Minnesota"],["Sheridan County","Wyoming"],["Muhlenberg County","Kentucky"],["Wabash County","Indiana"],["Bolivar County","Mississippi"],["Elk County","Pennsylvania"],["Williamsburg County","South Carolina"],["Kleberg County","Texas"],["Bee County","Texas"],["Summit County","Colorado"],["Stone County","Missouri"],["Washington County","Maine"],["Lake County","Montana"],["Clarendon County","South Carolina"],["Pontotoc County","Mississippi"],["Polk County","Minnesota"],["Delta County","Colorado"],["Adams County","Nebraska"],["Titus County","Texas"],["Coos County","New Hampshire"],["Amherst County","Virginia"],["Gilmer County","Georgia"],["Huron County","Michigan"],["Montgomery County","Kansas"],["Polk County","Missouri"],["Malheur County","Oregon"],["Marshall County","Kentucky"],["Claiborne County","Tennessee"],["Franklin County","Alabama"],["Lyon County","Kansas"],["Henry County","Tennessee"],["Jefferson Davis Parish","Louisiana"],["Jefferson Davis Parish","Louisiana"],["Chester County","South Carolina"],["Evangeline Parish","Louisiana"],["Hale County","Texas"],["Dorchester County","Maryland"],["Logan County","West Virginia"],["Jackson County","Ohio"],["Lassen County","California"],["Rhea County","Tennessee"],["Weakley County","Tennessee"],["Morgan County","Illinois"],["Jasper County","Indiana"],["Jefferson County","Washington"],["Greenbrier County","West Virginia"],["Jasper County","Texas"],["Lafayette County","Missouri"],["Transylvania County","North Carolina"],["Pike County","Alabama"],["Gibson County","Indiana"],["Hot Spring County","Arkansas"],["Lawrence County","Alabama"],["Jefferson County","Indiana"],["Lee County","Georgia"],["Clinton County","Indiana"],["Panola County","Mississippi"],["Pickens County","Georgia"],["Bureau County","Illinois"],["Morton County","North Dakota"],["Caroline County","Maryland"],["Daviess County","Indiana"],["Accomack County","Virginia"],["Marion County","Iowa"],["Lincoln County","Oklahoma"],["Lumpkin County","Georgia"],["Lee County","Iowa"],["Botetourt County","Virginia"],["Fulton County","Illinois"],["Stark County","North Dakota"],["Wexford County","Michigan"],["Marshall County","Mississippi"],["Wakulla County","Florida"],["Pulaski County","Virginia"],["Seneca County","New York"],["DeSoto County","Florida"],["Morrison County","Minnesota"],["Halifax County","Virginia"],["Harvey County","Kansas"],["Christian County","Illinois"],["Emmet County","Michigan"],["Lee County","Illinois"],["Scotland County","North Carolina"],["Monroe County","Mississippi"],["Whitley County","Indiana"],["Miami County","Kansas"],["Preston County","West Virginia"],["Ford County","Kansas"],["Platte County","Nebraska"],["Marshall County","Tennessee"],["Brookings County","South Dakota"],["Steuben County","Indiana"],["Putnam County","Ohio"],["Nicollet County","Minnesota"],["Taos County","New Mexico"],["Barry County","Missouri"],["Cowley County","Kansas"],["Clark County","Wisconsin"],["Harris County","Georgia"],["Effingham County","Illinois"],["Lincoln County","Nebraska"],["Alcorn County","Mississippi"],["Chambers County","Alabama"],["Wasatch County","Utah"],["Howard County","Texas"],["Lincoln County","Mississippi"],["Morrow County","Ohio"],["Monroe County","Illinois"],["Silver Bow County","Montana"],["Becker County","Minnesota"],["Lincoln County","Maine"],["Lincoln County","Tennessee"],["Perry County","Ohio"],["Wapello County","Iowa"],["Warren County","Missouri"],["Madison County","Nebraska"],["Uintah County","Utah"],["Fannin County","Texas"],["Washington County","Texas"],["Adams County","Indiana"],["Livingston County","Illinois"],["Sioux County","Iowa"],["Hill County","Texas"],["Floyd County","Kentucky"],["Greene County","Pennsylvania"],["Miami County","Indiana"],["Greenup County","Kentucky"],["Cocke County","Tennessee"],["Laclede County","Missouri"],["Scotts Bluff County","Nebraska"],["Carlton County","Minnesota"],["Ware County","Georgia"],["Orange County","Virginia"],["Matagorda County","Texas"],["Knox County","Indiana"],["Alexander County","North Carolina"],["Beauregard Parish","Louisiana"],["Coshocton County","Ohio"],["Graves County","Kentucky"],["Huntington County","Indiana"],["Sagadahoc County","Maine"],["Okmulgee County","Oklahoma"],["Whitley County","Kentucky"],["Putnam County","Indiana"],["Geary County","Kansas"],["Escambia County","Alabama"],["McLeod County","Minnesota"],["Chippewa County","Michigan"],["Hopkins County","Texas"],["Dyer County","Tennessee"],["Clinton County","Illinois"],["Delta County","Michigan"],["Dare County","North Carolina"],["Webster Parish","Louisiana"],["Clark County","Kentucky"],["Webster County","Iowa"],["Macon County","North Carolina"],["Albany County","Wyoming"],["Green County","Wisconsin"],["Green County","Wisconsin"],["Williams County","Ohio"],["Calloway County","Kentucky"],["Jefferson County","Illinois"],["Dodge County","Nebraska"],["Yadkin County","North Carolina"],["Clarion County","Pennsylvania"],["Bennington County","Vermont"],["Houghton County","Michigan"],["Addison County","Vermont"],["Boone County","Arkansas"],["Essex County","New York"],["Steele County","Minnesota"],["Clinton County","Pennsylvania"],["Natchitoches Parish","Louisiana"],["Talbot County","Maryland"],["Covington County","Alabama"],["Louisa County","Virginia"],["Newberry County","South Carolina"],["Marion County","Illinois"],["Franklin County","Illinois"],["Jasper County","Iowa"],["Oneida County","Wisconsin"],["Cass County","Indiana"],["Montgomery County","Indiana"],["Independence County","Arkansas"],["Lawrence County","Missouri"],["Scott County","Missouri"],["Pontotoc County","Oklahoma"],["Brown County","Texas"],["Defiance County","Ohio"],["Brown County","South Dakota"],["Susquehanna County","Pennsylvania"],["Guernsey County","Ohio"],["Dallas County","Alabama"],["Woodford County","Illinois"],["Finney County","Kansas"],["Graham County","Arizona"],["Warren County","Pennsylvania"],["Colleton County","South Carolina"],["Isle of Wight County","Virginia"],["Gloucester County","Virginia"],["Champaign County","Ohio"],["Jim Wells County","Texas"],["Jim Wells County","Texas"],["Des Moines County","Iowa"],["Oconto County","Wisconsin"],["Crawford County","Kansas"],["Wayne County","West Virginia"],["Douglas County","Minnesota"],["Mayes County","Oklahoma"],["Union County","Arkansas"],["Webster County","Missouri"],["Person County","North Carolina"],["Fremont County","Wyoming"],["Campbell County","Tennessee"],["Sequoyah County","Oklahoma"],["Latah County","Idaho"],["Waldo County","Maine"],["Hendry County","Florida"],["Okeechobee County","Florida"],["Harrison County","Indiana"],["Avoyelles Parish","Louisiana"],["Mecosta County","Michigan"],["Snyder County","Pennsylvania"],["Howell County","Missouri"],["Murray County","Georgia"],["Mower County","Minnesota"],["Marshall County","Iowa"],["Pike County","Mississippi"],["Orleans County","New York"],["Rio Arriba County","New Mexico"],["Ottawa County","Ohio"],["Delaware County","Oklahoma"],["Tazewell County","Virginia"],["McKean County","Pennsylvania"],["Amador County","California"],["Fayette County","West Virginia"],["Wyoming County","New York"],["Pasquotank County","North Carolina"],["Knox County","Maine"],["Sanilac County","Michigan"],["Mississippi County","Arkansas"],["Warren County","Virginia"],["Shawano County","Wisconsin"],["Upshur County","Texas"],["Williams County","North Dakota"],["Warren County","Tennessee"],["Preble County","Ohio"],["Tioga County","Pennsylvania"],["Clatsop County","Oregon"],["Cheatham County","Tennessee"],["Isanti County","Minnesota"],["Tallapoosa County","Alabama"],["Tift County","Georgia"],["Benton County","Minnesota"],["Wharton County","Texas"],["Baxter County","Arkansas"],["McClain County","Oklahoma"],["Cooke County","Texas"],["Gratiot County","Michigan"],["Oconee County","Georgia"],["Marinette County","Wisconsin"],["Fayette County","Tennessee"],["Clinton County","Ohio"],["Crawford County","Ohio"],["Nez Perce County","Idaho"],["Okanogan County","Washington"],["Butler County","Missouri"],["Pierce County","Wisconsin"],["Sweetwater County","Wyoming"],["Summit County","Utah"],["Ohio County","West Virginia"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["Mercer County","Ohio"],["Erath County","Texas"],["Vance County","North Carolina"],["Miller County","Arkansas"],["Montrose County","Colorado"],["Union County","Pennsylvania"],["Davie County","North Carolina"],["Fulton County","Ohio"],["Camden County","Missouri"],["Franklin County","Tennessee"],["Stephens County","Oklahoma"],["Polk County","Georgia"],["Levy County","Florida"],["Douglas County","Washington"],["Richmond County","North Carolina"],["Pettis County","Missouri"],["Prince George County","Virginia"],["Sullivan County","New Hampshire"],["Coffee County","Georgia"],["Jackson County","North Carolina"],["Cerro Gordo County","Iowa"],["Muscatine County","Iowa"],["DeKalb County","Indiana"],["Chesterfield County","South Carolina"],["Highland County","Ohio"],["Suwannee County","Florida"],["Dubois County","Indiana"],["Brown County","Ohio"],["Kay County","Oklahoma"],["Kandiyohi County","Minnesota"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["Pittsburg County","Oklahoma"],["Baldwin County","Georgia"],["Madison County","Ohio"],["Gadsden County","Florida"],["Siskiyou County","California"],["Huntingdon County","Pennsylvania"],["Lawrence County","Tennessee"],["Ravalli County","Montana"],["Shenandoah County","Virginia"],["Holmes County","Ohio"],["Kendall County","Texas"],["Callaway County","Missouri"],["Douglas County","Wisconsin"],["Delaware County","New York"],["Kittitas County","Washington"],["Barren County","Kentucky"],["Jefferson County","Pennsylvania"],["Stokes County","North Carolina"],["McDowell County","North Carolina"],["Stephenson County","Illinois"],["Phelps County","Missouri"],["Beaufort County","North Carolina"],["Warren County","Mississippi"],["Bryan County","Georgia"],["Henderson County","Kentucky"],["Wood County","Texas"],["Branch County","Michigan"],["Washington County","Mississippi"],["Macoupin County","Illinois"],["Polk County","Wisconsin"],["Lawrence County","Indiana"],["Chilton County","Alabama"],["Itasca County","Minnesota"],["Shelby County","Indiana"],["Calaveras County","California"],["Hopkins County","Kentucky"],["Dunn County","Wisconsin"],["Washington Parish","Louisiana"],["Greene County","Arkansas"],["Hillsdale County","Michigan"],["Thomas County","Georgia"],["Osage County","Oklahoma"],["Perry County","Pennsylvania"],["Caldwell County","Texas"],["Colquitt County","Georgia"],["Windham County","Vermont"],["Habersham County","Georgia"],["Hancock County","Mississippi"],["Bryan County","Oklahoma"],["Marshall County","Indiana"],["Mifflin County","Pennsylvania"],["Logan County","Ohio"],["Beltrami County","Minnesota"],["Monroe County","Tennessee"],["Monroe County","Wisconsin"],["Auglaize County","Ohio"],["Jackson County","Indiana"],["Stevens County","Washington"],["Allegany County","New York"],["Clinton County","Iowa"],["Chambers County","Texas"],["Barron County","Wisconsin"],["Nelson County","Kentucky"],["Cortland County","New York"],["Coles County","Illinois"],["Campbell County","Wyoming"],["Cherokee County","Oklahoma"],["Bonner County","Idaho"],["Chenango County","New York"],["Jackson County","Florida"],["Noble County","Indiana"],["Franklin County","New York"],["Bedford County","Pennsylvania"],["Goodhue County","Minnesota"],["Val Verde County","Texas"],["Santa Cruz County","Arizona"],["Greene County","New York"],["Whitman County","Washington"],["Bingham County","Idaho"],["Carter County","Oklahoma"],["Shelby County","Kentucky"],["Le Flore County","Oklahoma"],["Crittenden County","Arkansas"],["Shelby County","Ohio"],["Boyd County","Kentucky"],["Lincoln Parish","Louisiana"],["Curry County","New Mexico"],["Tioga County","New York"],["Halifax County","North Carolina"],["Duplin County","North Carolina"],["Vernon Parish","Louisiana"],["Edgecombe County","North Carolina"],["Henry County","Indiana"],["Fremont County","Colorado"],["Atascosa County","Texas"],["Burnet County","Texas"],["Henry County","Illinois"],["Dale County","Alabama"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["Douglas County","Nevada"],["Montgomery County","New York"],["Logan County","Oklahoma"],["Laurens County","Georgia"],["Winona County","Minnesota"],["Wilson County","Texas"],["Queen Anne's County","Maryland"],["Franklin County","Vermont"],["Knox County","Illinois"],["Newaygo County","Michigan"],["Buffalo County","Nebraska"],["Lamar County","Texas"],["Carroll County","New Hampshire"],["Polk County","Texas"],["Bedford County","Tennessee"],["Lincoln County","Oregon"],["Cherokee County","Texas"],["Gibson County","Tennessee"],["Venango County","Pennsylvania"],["Somerset County","Maine"],["Columbus County","North Carolina"],["Dearborn County","Indiana"],["Medina County","Texas"],["Bristol County","Rhode Island"],["Wayne County","Pennsylvania"],["Franklin County","Kentucky"],["Cass County","Michigan"],["Nye County","Nevada"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["Ogle County","Illinois"],["Oktibbeha County","Mississippi"],["Waupaca County","Wisconsin"],["Darke County","Ohio"],["Grant County","Wisconsin"],["Hoke County","North Carolina"],["Rusk County","Texas"],["Warren County","Iowa"],["Calumet County","Wisconsin"],["Ashland County","Ohio"],["Washington County","Oklahoma"],["Worcester County","Maryland"],["Grundy County","Illinois"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["Culpeper County","Virginia"],["Jackson County","Alabama"],["Columbia County","Oregon"],["Kerr County","Texas"],["Navarro County","Texas"],["Madison County","Idaho"],["Jackson County","Illinois"],["Jessamine County","Kentucky"],["Gila County","Arizona"],["McMinn County","Tennessee"],["Tuscola County","Michigan"],["Fulton County","New York"],["Roane County","Tennessee"],["Boone County","Illinois"],["Coffee County","Alabama"],["Elko County","Nevada"],["Pulaski County","Missouri"],["Johnson County","Missouri"],["Watauga County","North Carolina"],["Saline County","Kansas"],["Dickson County","Tennessee"],["Franklin County","Virginia"],["Jefferson County","Tennessee"],["Camden County","Georgia"],["Grady County","Oklahoma"],["Loudon County","Tennessee"],["Seneca County","Ohio"],["Lenoir County","North Carolina"],["Hancock County","Maine"],["Tuolumne County","California"],["La Plata County","Colorado"],["Whiteside County","Illinois"],["Eagle County","Colorado"],["Lafayette County","Mississippi"],["Taney County","Missouri"],["Pearl River County","Mississippi"],["Marion County","West Virginia"],["Cherokee County","South Carolina"],["Hardin County","Texas"],["Carter County","Tennessee"],["Chisago County","Minnesota"],["Hawkins County","Tennessee"],["Waller County","Texas"],["Scott County","Kentucky"],["Colbert County","Alabama"],["Iron County","Utah"],["Vermilion Parish","Louisiana"],["Putnam County","West Virginia"],["Gordon County","Georgia"],["Acadia Parish","Louisiana"],["Box Elder County","Utah"],["Jefferson County","West Virginia"],["Windsor County","Vermont"],["Oxford County","Maine"],["Maverick County","Texas"],["Coffee County","Tennessee"],["Anderson County","Texas"],["Lawrence County","Ohio"],["Genesee County","New York"],["Columbia County","Wisconsin"],["Otsego County","New York"],["Pike County","Pennsylvania"],["Pickaway County","Ohio"],["Huron County","Ohio"],["Carson City","Nevada"],["Newton County","Missouri"],["Pike County","Kentucky"],["Autauga County","Alabama"],["Lowndes County","Mississippi"],["Sandusky County","Ohio"],["Sampson County","North Carolina"],["Blount County","Alabama"],["Russell County","Alabama"],["Lyon County","Nevada"],["Van Zandt County","Texas"],["Lincoln County","Missouri"],["Mercer County","West Virginia"],["Washington County","Ohio"],["Washington County","Vermont"],["Bradford County","Pennsylvania"],["Otter Tail County","Minnesota"],["Crawford County","Arkansas"],["Herkimer County","New York"],["Pender County","North Carolina"],["Rutland County","Vermont"],["St. Joseph County","Michigan"],["St. Joseph County","Michigan"],["Tipton County","Tennessee"],["Granville County","North Carolina"],["Cumberland County","Tennessee"],["Washington County","New York"],["Columbia County","New York"],["Hood County","Texas"],["Garfield County","Colorado"],["Livingston County","New York"],["Reno County","Kansas"],["Haywood County","North Carolina"],["Eddy County","New Mexico"],["Barry County","Michigan"],["Athens County","Ohio"],["Stanly County","North Carolina"],["Walla Walla County","Washington"],["Laurel County","Kentucky"],["Knox County","Ohio"],["Union County","Ohio"],["Garfield County","Oklahoma"],["Hall County","Nebraska"],["Darlington County","South Carolina"],["Lee County","North Carolina"],["Pope County","Arkansas"],["Georgetown County","South Carolina"],["Belknap County","New Hampshire"],["Warrick County","Indiana"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["Lamar County","Mississippi"],["Isabella County","Michigan"],["Rutherford County","North Carolina"],["Hamblen County","Tennessee"],["Nacogdoches County","Texas"],["Columbia County","Pennsylvania"],["Carbon County","Pennsylvania"],["Effingham County","Georgia"],["Salem County","New Jersey"],["Coos County","Oregon"],["Pulaski County","Kentucky"],["Chaves County","New Mexico"],["Lincoln County","South Dakota"],["Jefferson County","Ohio"],["Liberty County","Georgia"],["Clay County","Minnesota"],["Walker County","Alabama"],["Marion County","Ohio"],["Kershaw County","South Carolina"],["Armstrong County","Pennsylvania"],["Mason County","Washington"],["Adams County","Illinois"],["Warren County","New York"],["Sauk County","Wisconsin"],["Tehama County","California"],["Starr County","Texas"],["Harrison County","West Virginia"],["Wilkes County","North Carolina"],["Marquette County","Michigan"],["Apache County","Arizona"],["Crow Wing County","Minnesota"],["Chippewa County","Wisconsin"],["Muskogee County","Oklahoma"],["Belmont County","Ohio"],["Wayne County","Indiana"],["Montcalm County","Michigan"],["Grant County","Indiana"],["Ionia County","Michigan"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["Rice County","Minnesota"],["Aroostook County","Maine"],["Williamson County","Illinois"],["Jones County","Mississippi"],["Jefferson County","Arkansas"],["Spalding County","Georgia"],["Butler County","Kansas"],["Laurens County","South Carolina"],["Oldham County","Kentucky"],["Walker County","Georgia"],["Carteret County","North Carolina"],["Otero County","New Mexico"],["Catoosa County","Georgia"],["McCracken County","Kentucky"],["Madison County","New York"],["Shiawassee County","Michigan"],["Allegany County","Maryland"],["Lake County","California"],["Franklin County","North Carolina"],["Wise County","Texas"],["San Patricio County","Texas"],["San Patricio County","Texas"],["San Patricio County","Texas"],["San Patricio County","Texas"],["Harrison County","Texas"],["Blue Earth County","Minnesota"],["Greenwood County","South Carolina"],["Klamath County","Oregon"],["Troup County","Georgia"],["Columbia County","Florida"],["Ward County","North Dakota"],["Iberia Parish","Louisiana"],["Greene County","Tennessee"],["Portage County","Wisconsin"],["Boone County","Indiana"],["Lewis and Clark County","Montana"],["Franklin County","Massachusetts"],["Surry County","North Carolina"],["DeKalb County","Alabama"],["Creek County","Oklahoma"],["Morgan County","Indiana"],["Riley County","Kansas"],["Pottawatomie County","Oklahoma"],["Tooele County","Utah"],["Christian County","Kentucky"],["Robertson County","Tennessee"],["McKinley County","New Mexico"],["Fauquier County","Virginia"],["Lauderdale County","Mississippi"],["Grand Forks County","North Dakota"],["Kauai County","Hawaii"],["Putnam County","Florida"],["Scioto County","Ohio"],["Lonoke County","Arkansas"],["Broomfield County","Colorado"],["Somerset County","Pennsylvania"],["Vermilion County","Illinois"],["Wood County","Wisconsin"],["Lea County","New Mexico"],["Raleigh County","West Virginia"],["Hancock County","Ohio"],["Walton County","Florida"],["Van Buren County","Michigan"],["Erie County","Ohio"],["Grays Harbor County","Washington"],["Jackson County","Georgia"],["Valencia County","New Mexico"],["Cayuga County","New York"],["Chatham County","North Carolina"],["Walker County","Texas"],["Cheshire County","New Hampshire"],["White County","Arkansas"],["Cattaraugus County","New York"],["Ross County","Ohio"],["Anderson County","Tennessee"],["Clallam County","Washington"],["Cole County","Missouri"],["Forrest County","Mississippi"],["Oconee County","South Carolina"],["Sullivan County","New York"],["Wilson County","North Carolina"],["Chelan County","Washington"],["Clinton County","Michigan"],["Bedford County","Virginia"],["Hancock County","Indiana"],["Clinton County","New York"],["Putnam County","Tennessee"],["Natrona County","Wyoming"],["Umatilla County","Oregon"],["Kosciusko County","Indiana"],["Floyd County","Indiana"],["Clearfield County","Pennsylvania"],["Caldwell County","North Carolina"],["Wagoner County","Oklahoma"],["Bulloch County","Georgia"],["Manitowoc County","Wisconsin"],["Yuba County","California"],["Payne County","Oklahoma"],["Cape Girardeau County","Missouri"],["Leavenworth County","Kansas"],["Talladega County","Alabama"],["Lewis County","Washington"],["Henderson County","Texas"],["Bartholomew County","Indiana"],["Bullitt County","Kentucky"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["Monroe County","Florida"],["Coryell County","Texas"],["Indiana County","Pennsylvania"],["Lee County","Mississippi"],["Midland County","Michigan"],["Barrow County","Georgia"],["Howard County","Indiana"],["Crawford County","Pennsylvania"],["Chemung County","New York"],["Orangeburg County","South Carolina"],["Wood County","West Virginia"],["Cascade County","Montana"],["Glynn County","Georgia"],["Buchanan County","Missouri"],["Orange County","Texas"],["Jefferson County","Wisconsin"],["Newport County","Rhode Island"],["Dougherty County","Georgia"],["Lawrence County","Pennsylvania"],["Angelina County","Texas"],["Muskingum County","Ohio"],["Lincoln County","North Carolina"],["Island County","Washington"],["Bannock County","Idaho"],["Polk County","Oregon"],["Burke County","North Carolina"],["Cullman County","Alabama"],["Elmore County","Alabama"],["Josephine County","Oregon"],["Lapeer County","Michigan"],["Christian County","Missouri"],["Dodge County","Wisconsin"],["Twin Falls County","Idaho"],["Nassau County","Florida"],["Rockingham County","North Carolina"],["St. Clair County","Alabama"],["Grafton County","New Hampshire"],["Wayne County","New York"],["Victoria County","Texas"],["Ozaukee County","Wisconsin"],["Mendocino County","California"],["Liberty County","Texas"],["Northumberland County","Pennsylvania"],["Madison County","Kentucky"],["Calvert County","Maryland"],["Bowie County","Texas"],["Campbell County","Kentucky"],["Tuscarawas County","Ohio"],["St. Croix County","Wisconsin"],["Lauderdale County","Alabama"],["Rockdale County","Georgia"],["Steuben County","New York"],["Pottawattamie County","Iowa"],["Cabell County","West Virginia"],["Nash County","North Carolina"],["Benton County","Oregon"],["Grand Traverse County","Michigan"],["Rogers County","Oklahoma"],["Cape May County","New Jersey"],["Geauga County","Ohio"],["Lancaster County","South Carolina"],["Walton County","Georgia"],["Franklin County","Washington"],["Sherburne County","Minnesota"],["Bastrop County","Texas"],["Lafourche Parish","Louisiana"],["Ashtabula County","Ohio"],["Marshall County","Alabama"],["Putnam County","New York"],["Sevier County","Tennessee"],["Burleigh County","North Dakota"],["Story County","Iowa"],["Floyd County","Georgia"],["Madison County","Tennessee"],["Grant County","Washington"],["Dubuque County","Iowa"],["Lenawee County","Michigan"],["Cleveland County","North Carolina"],["Sutter County","California"],["Dallas County","Iowa"],["Moore County","North Carolina"],["Hunt County","Texas"],["Garland County","Arkansas"],["DeKalb County","Illinois"],["Laramie County","Wyoming"],["Craven County","North Carolina"],["Maury County","Tennessee"],["Highlands County","Florida"],["Columbiana County","Ohio"],["Allen County","Ohio"],["Nevada County","California"],["Whitfield County","Georgia"],["Daviess County","Kentucky"],["Etowah County","Alabama"],["Limestone County","Alabama"],["Wicomico County","Maryland"],["Cecil County","Maryland"],["Adams County","Pennsylvania"],["Bay County","Michigan"],["Macon County","Illinois"],["Fond du Lac County","Wisconsin"],["Flathead County","Montana"],["Franklin County","Missouri"],["Sumter County","South Carolina"],["Eau Claire County","Wisconsin"],["Tompkins County","New York"],["Monongalia County","West Virginia"],["Woodbury County","Iowa"],["Vigo County","Indiana"],["Walworth County","Wisconsin"],["Navajo County","Arizona"],["Platte County","Missouri"],["Carver County","Minnesota"],["Houston County","Alabama"],["Kankakee County","Illinois"],["Yamhill County","Oregon"],["Rockwall County","Texas"],["Cass County","Missouri"],["St. Lawrence County","New York"],["Bradley County","Tennessee"],["Miami County","Ohio"],["Bartow County","Georgia"],["Madison County","Mississippi"],["Eaton County","Michigan"],["Pennington County","South Dakota"],["Terrebonne Parish","Louisiana"],["Warren County","New Jersey"],["LaSalle County","Illinois"],["Hanover County","Virginia"],["Mercer County","Pennsylvania"],["Hardin County","Kentucky"],["Cowlitz County","Washington"],["Androscoggin County","Maine"],["Douglas County","Oregon"],["Craighead County","Arkansas"],["Delaware County","Indiana"],["LaPorte County","Indiana"],["Ontario County","New York"],["Newton County","Georgia"],["St. Mary's County","Maryland"],["Lycoming County","Pennsylvania"],["Flagler County","Florida"],["Henderson County","North Carolina"],["Windham County","Connecticut"],["Calhoun County","Alabama"],["Robeson County","North Carolina"],["Jefferson County","New York"],["Wayne County","Ohio"],["Wayne County","North Carolina"],["Oswego County","New York"],["Missoula County","Montana"],["Sheboygan County","Wisconsin"],["Lowndes County","Georgia"],["Potter County","Texas"],["Douglas County","Kansas"],["Gallatin County","Montana"],["Carroll County","Georgia"],["Fayette County","Georgia"],["Tom Green County","Texas"],["Allegan County","Michigan"],["La Crosse County","Wisconsin"],["Clark County","Indiana"],["Comanche County","Oklahoma"],["San Juan County","New Mexico"],["San Juan County","New Mexico"],["Berkeley County","West Virginia"],["Jasper County","Missouri"],["Blair County","Pennsylvania"],["Saline County","Arkansas"],["Morgan County","Alabama"],["Faulkner County","Arkansas"],["Kennebec County","Maine"],["Bonneville County","Idaho"],["Gregg County","Texas"],["Richland County","Ohio"],["Cochise County","Arizona"],["Ascension Parish","Louisiana"],["Chautauqua County","New York"],["Sebastian County","Arkansas"],["Linn County","Oregon"],["Clarke County","Georgia"],["Bossier Parish","Louisiana"],["Fayette County","Pennsylvania"],["Hunterdon County","New Jersey"],["Berkshire County","Massachusetts"],["Wichita County","Texas"],["Skagit County","Washington"],["Sumter County","Florida"],["Washington County","Rhode Island"],["Rapides Parish","Louisiana"],["Madison County","Indiana"],["Strafford County","New Hampshire"],["Black Hawk County","Iowa"],["Tazewell County","Illinois"],["Pickens County","South Carolina"],["Kendall County","Illinois"],["Wood County","Ohio"],["Washington County","Tennessee"],["Cache County","Utah"],["Tangipahoa Parish","Louisiana"],["Cambria County","Pennsylvania"],["Harnett County","North Carolina"],["Calhoun County","Michigan"],["Warren County","Kentucky"],["Blount County","Tennessee"],["Grayson County","Texas"],["Boone County","Kentucky"],["Clark County","Ohio"],["Humboldt County","California"],["Brunswick County","North Carolina"],["Washington County","Wisconsin"],["Florence County","South Carolina"],["Marathon County","Wisconsin"],["Napa County","California"],["Monroe County","Indiana"],["Randall County","Texas"],["Wright County","Minnesota"],["Livingston Parish","Louisiana"],["Schuylkill County","Pennsylvania"],["Taylor County","Texas"],["Jackson County","Mississippi"],["Lebanon County","Pennsylvania"],["Randolph County","North Carolina"],["Sussex County","New Jersey"],["Douglas County","Georgia"],["Rock Island County","Illinois"],["Coconino County","Arizona"],["Kaufman County","Texas"],["Coweta County","Georgia"],["Rowan County","North Carolina"],["Wilson County","Tennessee"],["Parker County","Texas"],["Orange County","North Carolina"],["Sandoval County","New Mexico"],["Tolland County","Connecticut"],["Scott County","Minnesota"],["Penobscot County","Maine"],["Kings County","California"],["Johnson County","Iowa"],["Merrimack County","New Hampshire"],["Citrus County","Florida"],["Cumberland County","New Jersey"],["Berrien County","Michigan"],["Canadian County","Oklahoma"],["Washington County","Maryland"],["Monroe County","Michigan"],["Santa Fe County","New Mexico"],["Mesa County","Colorado"],["Franklin County","Pennsylvania"],["Columbia County","Georgia"],["Madera County","California"],["Stafford County","Virginia"],["Rankin County","Mississippi"],["Bibb County","Georgia"],["Schenectady County","New York"],["Sullivan County","Tennessee"],["Centre County","Pennsylvania"],["Stearns County","Minnesota"],["Martin County","Florida"],["Fairfield County","Ohio"],["Indian River County","Florida"],["Jackson County","Michigan"],["Ouachita Parish","Louisiana"],["St. Clair County","Michigan"],["St. Clair County","Michigan"],["Catawba County","North Carolina"],["Rensselaer County","New York"],["Comal County","Texas"],["Dorchester County","South Carolina"],["Johnson County","Indiana"],["Portage County","Ohio"],["Hampshire County","Massachusetts"],["Olmsted County","Minnesota"],["Houston County","Georgia"],["Rock County","Wisconsin"],["Middlesex County","Connecticut"],["Yellowstone County","Montana"],["Maui County","Hawaii"],["Ector County","Texas"],["Charles County","Maryland"],["Greene County","Ohio"],["Pueblo County","Colorado"],["Beaver County","Pennsylvania"],["Chittenden County","Vermont"],["Monroe County","Pennsylvania"],["Paulding County","Georgia"],["Aiken County","South Carolina"],["Davidson County","North Carolina"],["Kenton County","Kentucky"],["Kenosha County","Wisconsin"],["Wyandotte County","Kansas"],["Midland County","Texas"],["Pitt County","North Carolina"],["Kent County","Rhode Island"],["McLean County","Illinois"],["Kootenai County","Idaho"],["Alamance County","North Carolina"],["Winnebago County","Wisconsin"],["Guadalupe County","Texas"],["Carroll County","Maryland"],["Porter County","Indiana"],["Lee County","Alabama"],["Scott County","Iowa"],["Hendricks County","Indiana"],["Bay County","Florida"],["Muskegon County","Michigan"],["Licking County","Ohio"],["Shawnee County","Kansas"],["Imperial County","California"],["Johnson County","Texas"],["Vanderburgh County","Indiana"],["Washington County","Utah"],["Kanawha County","West Virginia"],["Peoria County","Illinois"],["Kent County","Delaware"],["Ulster County","New York"],["Shasta County","California"],["Medina County","Ohio"],["Boone County","Missouri"],["Cass County","North Dakota"],["Litchfield County","Connecticut"],["DeSoto County","Mississippi"],["Tippecanoe County","Indiana"],["Iredell County","North Carolina"],["Charlotte County","Florida"],["Beaufort County","South Carolina"],["Santa Rosa County","Florida"],["Saginaw County","Michigan"],["Sarpy County","Nebraska"],["Outagamie County","Wisconsin"],["El Dorado County","California"],["Ellis County","Texas"],["Butler County","Pennsylvania"],["Livingston County","Michigan"],["Hernando County","Florida"],["Sumner County","Tennessee"],["Sangamon County","Illinois"],["Minnehaha County","South Dakota"],["Racine County","Wisconsin"],["Deschutes County","Oregon"],["Broome County","New York"],["St. Louis County","Minnesota"],["Trumbull County","Ohio"],["Hall County","Georgia"],["Anderson County","South Carolina"],["Yuma County","Arizona"],["Onslow County","North Carolina"],["Champaign County","Illinois"],["Richmond County","Georgia"],["Benton County","Washington"],["Muscogee County","Georgia"],["Elkhart County","Indiana"],["Clermont County","Ohio"],["Harrison County","Mississippi"],["Washington County","Pennsylvania"],["Butte County","California"],["Okaloosa County","Florida"],["York County","Maine"],["Niagara County","New York"],["Mohave County","Arizona"],["Delaware County","Ohio"],["Lackawanna County","Pennsylvania"],["Johnston County","North Carolina"],["Yolo County","California"],["Calcasieu Parish","Louisiana"],["Clay County","Florida"],["Montgomery County","Tennessee"],["Shelby County","Alabama"],["Jackson County","Oregon"],["New Hanover County","North Carolina"],["Cabarrus County","North Carolina"],["Richmond city","Virginia"],["Jefferson County","Missouri"],["Whatcom County","Washington"],["Tuscaloosa County","Alabama"],["Hinds County","Mississippi"],["Gaston County","North Carolina"],["Mahoning County","Ohio"],["Montgomery County","Alabama"],["Barnstable County","Massachusetts"],["Berkeley County","South Carolina"],["Linn County","Iowa"],["Canyon County","Idaho"],["Baldwin County","Alabama"],["Oneida County","New York"],["Lake County","Ohio"],["Smith County","Texas"],["Brazos County","Texas"],["Saratoga County","New York"],["Yavapai County","Arizona"],["Sussex County","Delaware"],["Caddo Parish","Louisiana"],["Union County","North Carolina"],["Arlington County","Virginia"],["Henry County","Georgia"],["Hays County","Texas"],["Lafayette Parish","Louisiana"],["Warren County","Ohio"],["Washington County","Arkansas"],["Williamson County","Tennessee"],["Forsyth County","Georgia"],["Clay County","Missouri"],["Jefferson County","Texas"],["Yakima County","Washington"],["St. Clair County","Illinois"],["Cumberland County","Pennsylvania"],["McLennan County","Texas"],["Harford County","Maryland"],["Kalamazoo County","Michigan"],["Weber County","Utah"],["Marin County","California"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["Madison County","Illinois"],["Cherokee County","Georgia"],["Webb County","Texas"],["Washington County","Minnesota"],["New London County","Connecticut"],["New London County","Connecticut"],["Brown County","Wisconsin"],["Buncombe County","North Carolina"],["Santa Cruz County","California"],["Santa Cruz County","California"],["Santa Cruz County","California"],["Erie County","Pennsylvania"],["Frederick County","Maryland"],["St. Joseph County","Indiana"],["St. Johns County","Florida"],["St. Johns County","Florida"],["Atlantic County","New Jersey"],["Kitsap County","Washington"],["Alachua County","Florida"],["Merced County","California"],["York County","South Carolina"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["Benton County","Arkansas"],["Ingham County","Michigan"],["Winnebago County","Illinois"],["Dauphin County","Pennsylvania"],["Leon County","Florida"],["Lexington County","South Carolina"],["Thurston County","Washington"],["Chatham County","Georgia"],["Cleveland County","Oklahoma"],["Dutchess County","New York"],["Ottawa County","Michigan"],["Clayton County","Georgia"],["Greene County","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["Gloucester County","New Jersey"],["Cumberland County","Maine"],["McHenry County","Illinois"],["Lubbock County","Texas"],["Northampton County","Pennsylvania"],["Lorain County","Ohio"],["Rockingham County","New Hampshire"],["Albany County","New York"],["Escambia County","Florida"],["Fayette County","Kentucky"],["Lancaster County","Nebraska"],["Durham County","North Carolina"],["Luzerne County","Pennsylvania"],["Spartanburg County","South Carolina"],["Weld County","Colorado"],["St. Lucie County","Florida"],["St. Lucie County","Florida"],["Boulder County","Colorado"],["Howard County","Maryland"],["Henrico County","Virginia"],["Cumberland County","North Carolina"],["Rockland County","New York"],["Rutherford County","Tennessee"],["Somerset County","New Jersey"],["Marion County","Oregon"],["Hamilton County","Indiana"],["Galveston County","Texas"],["Horry County","South Carolina"],["Nueces County","Texas"],["Westmoreland County","Pennsylvania"],["Douglas County","Colorado"],["Larimer County","Colorado"],["Davis County","Utah"],["Anoka County","Minnesota"],["Chesterfield County","Virginia"],["Hamilton County","Tennessee"],["Bell County","Texas"],["Brazoria County","Texas"],["Washtenaw County","Michigan"],["Lehigh County","Pennsylvania"],["Stark County","Ohio"],["Collier County","Florida"],["Marion County","Florida"],["Forsyth County","North Carolina"],["Lane County","Oregon"],["Lake County","Florida"],["Orleans Parish","Louisiana"],["Allen County","Indiana"],["Mercer County","New Jersey"],["Madison County","Alabama"],["Osceola County","Florida"],["Butler County","Ohio"],["Pulaski County","Arkansas"],["Manatee County","Florida"],["Orange County","New York"],["Placer County","California"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["Genesee County","Michigan"],["Waukesha County","Wisconsin"],["Charleston County","South Carolina"],["Mobile County","Alabama"],["Richland County","South Carolina"],["Loudoun County","Virginia"],["Cameron County","Texas"],["Clackamas County","Oregon"],["Hillsborough County","New Hampshire"],["Pinal County","Arizona"],["Berks County","Pennsylvania"],["Lucas County","Ohio"],["Sarasota County","Florida"],["Monterey County","California"],["Dakota County","Minnesota"],["Jefferson Parish","Louisiana"],["Jefferson Parish","Louisiana"],["Santa Barbara County","California"],["Santa Barbara County","California"],["Santa Barbara County","California"],["Solano County","California"],["York County","Pennsylvania"],["East Baton Rouge Parish","Louisiana"],["East Baton Rouge Parish","Louisiana"],["East Baton Rouge Parish","Louisiana"],["Burlington County","New Jersey"],["Hampden County","Massachusetts"],["Seminole County","Florida"],["Tulare County","California"],["Onondaga County","New York"],["Knox County","Tennessee"],["Prince William County","Virginia"],["Washoe County","Nevada"],["Sonoma County","California"],["Polk County","Iowa"],["Ada County","Idaho"],["Richmond County","New York"],["Lake County","Indiana"],["Clark County","Washington"],["Morris County","New Jersey"],["Kane County","Illinois"],["Adams County","Colorado"],["Camden County","New Jersey"],["Sedgwick County","Kansas"],["Passaic County","New Jersey"],["Greenville County","South Carolina"],["Plymouth County","Massachusetts"],["Chester County","Pennsylvania"],["Montgomery County","Ohio"],["Spokane County","Washington"],["Summit County","Ohio"],["Guilford County","North Carolina"],["Ramsey County","Minnesota"],["Stanislaus County","California"],["Lancaster County","Pennsylvania"],["Volusia County","Florida"],["Dane County","Wisconsin"],["Pasco County","Florida"],["New Castle County","Delaware"],["Union County","New Jersey"],["Delaware County","Pennsylvania"],["Bristol County","Massachusetts"],["Jefferson County","Colorado"],["Douglas County","Nebraska"],["Baltimore city","Maryland"],["Baltimore city","Maryland"],["Anne Arundel County","Maryland"],["Washington County","Oregon"],["Brevard County","Florida"],["Williamson County","Texas"],["Johnson County","Kansas"],["Montgomery County","Texas"],["Ocean County","New Jersey"],["Monmouth County","New Jersey"],["Bucks County","Pennsylvania"],["Arapahoe County","Colorado"],["Kent County","Michigan"],["Providence County","Rhode Island"],["Tulsa County","Oklahoma"],["Jefferson County","Alabama"],["Bernalillo County","New Mexico"],["Will County","Illinois"],["Lake County","Illinois"],["Denver County","Colorado"],["Davidson County","Tennessee"],["Jackson County","Missouri"],["Hudson County","New Jersey"],["Polk County","Florida"],["Norfolk County","Massachusetts"],["El Paso County","Colorado"],["Monroe County","New York"],["Lee County","Florida"],["DeKalb County","Georgia"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["Cobb County","Georgia"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["Jefferson County","Kentucky"],["Suffolk County","Massachusetts"],["Essex County","Massachusetts"],["Multnomah County","Oregon"],["Fort Bend County","Texas"],["Snohomish County","Washington"],["Hamilton County","Ohio"],["Ventura County","California"],["Baltimore County","Maryland"],["Baltimore County","Maryland"],["Montgomery County","Pennsylvania"],["Worcester County","Massachusetts"],["Middlesex County","New Jersey"],["Essex County","New Jersey"],["New Haven County","Connecticut"],["New Haven County","Connecticut"],["El Paso County","Texas"],["Hidalgo County","Texas"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["Macomb County","Michigan"],["Hartford County","Connecticut"],["Denton County","Texas"],["Kern County","California"],["Pierce County","Washington"],["Shelby County","Tennessee"],["DuPage County","Illinois"],["Milwaukee County","Wisconsin"],["Erie County","New York"],["Bergen County","New Jersey"],["Gwinnett County","Georgia"],["Fairfield County","Connecticut"],["Pinellas County","Florida"],["Prince George's County","Maryland"],["Marion County","Indiana"],["Duval County","Florida"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["Westchester County","New York"],["Fresno County","California"],["Honolulu County","Hawaii"],["Pima County","Arizona"],["Montgomery County","Maryland"],["Collin County","Texas"],["Fulton County","Georgia"],["Mecklenburg County","North Carolina"],["Wake County","North Carolina"],["Contra Costa County","California"],["Salt Lake County","Utah"],["Allegheny County","Pennsylvania"],["Cuyahoga County","Ohio"],["Oakland County","Michigan"],["Hennepin County","Minnesota"],["Travis County","Texas"],["Franklin County","Ohio"],["Nassau County","New York"],["Orange County","Florida"],["Hillsborough County","Florida"],["Bronx County","New York"],["Palm Beach County","Florida"],["Suffolk County","New York"],["Sacramento County","California"],["Philadelphia County","Pennsylvania"],["Middlesex County","Massachusetts"],["Alameda County","California"],["Wayne County","Michigan"],["Santa Clara County","California"],["Santa Clara County","California"],["Santa Clara County","California"],["Broward County","Florida"],["Bexar County","Texas"],["Tarrant County","Texas"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["Clark County","Nevada"],["King County","Washington"],["Queens County","New York"],["Riverside County","California"],["Dallas County","Texas"],["Miami-Dade County","Florida"],["Kings County","New York"],["Orange County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["Maricopa County","Arizona"],["Harris County","Texas"],["Cook County","Illinois"],["Los Angeles County","California"]],"hovertemplate":"Log 2020 Income=%{x}\u003cbr\u003eLog TotalChristianAdherents=%{y}\u003cbr\u003eCOUNAM=%{customdata[0]}\u003cbr\u003eSTATNAM=%{customdata[1]}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","marker":{"color":"#636efa","symbol":"circle"},"mode":"markers","name":"","showlegend":false,"x":[11.590737995338337,11.3254627148614,10.809000411238404,11.120756569154405,11.167190461069831,10.886782513190758,10.528944584126123,11.299645607092907,11.028238562147264,10.893604788384124,11.150534214035387,10.687457587169673,11.012495617386358,11.069244338833569,10.899217733236709,11.520407405317984,11.086333753496243,10.751092508621763,10.911317727550735,10.777934935151473,10.810131907358478,10.91567011320585,10.912156898644932,11.10755535234985,11.167402392828597,10.900288575057553,10.75301863171864,10.926405996835037,10.875742652327716,11.356961475423505,11.079045450122525,10.950332750382355,10.809505701639543,10.699507156016702,11.371765045181215,10.60826681732578,10.867710938165587,10.82863891284248,10.929296146316139,11.608453802794545,11.109084037978162,10.639598432528189,11.213008854850106,11.216659993654583,11.224709916912303,11.114773550156288,11.00531134546621,11.371465581909298,10.743782377382361,10.335529675494746,11.007004460537694,11.124214223760614,10.950595998337121,11.001666413954883,10.617906868371612,11.185573511837868,10.72792611877725,10.785021194452279,10.717147373323323,10.867291443078967,11.43116211116714,10.593304192999618,11.004197639286383,11.169984350200423,10.548625513909712,11.206454651066265,11.348522408678619,10.953347176331699,10.960131356381735,10.738893555669819,10.610340380152186,10.893939112309972,11.085874039736575,10.698649658502804,10.84499758754313,10.72092985236768,11.169448754196132,10.737309302378842,11.370301430714814,11.057534548092338,10.842459118633341,10.713817588680424,11.033081578812967,10.790534832440615,11.037901253667622,11.173739549651332,10.83366146551888,11.011043064434661,10.899365503749372,10.96825001232884,10.48799105597933,10.778664580680367,10.18539045772387,11.017004873924424,10.766208717067526,10.627309417363993,10.95759050121828,11.061421653949045,10.884535531625561,10.867291443078967,10.897350250005168,10.699800341706831,11.340415615560266,11.143541531433012,11.005577121783782,11.343689911724637,10.982271213570051,11.090888804018297,10.568518140370246,11.056840519861698,11.007501890493232,11.292802347549516,10.699191321421166,10.587038839422627,11.297377990277647,10.932392428779417,11.067544201945207,10.969938154395841,10.941854314188955,11.125732401649513,10.577502880780047,11.030330901545064,11.140208243321867,10.594231848479764,11.109518237971509,10.620497733360601,10.97081555116447,10.246296810613222,10.907697582448167,10.951735939359013,10.849162314098441,10.846887486888901,10.865840922736847,11.23875174254324,10.618469607703592,10.79806423150353,10.740302082908487,11.05606705747418,10.657847417264062,11.23533892735046,10.757200506425557,11.161223847800425,10.851335089314501,10.657165232836105,11.105408252735932,10.962561744356746,10.809950146091303,10.927484047823448,10.79277700890734,10.768611297835038,11.017480943242541,10.793844902383778,11.076093521112565,10.77270764101727,10.899531719479302,10.993328148817113,10.897368757042468,11.529694082545465,10.527766853797273,10.934891091510787,10.56684540428532,11.023812408109887,10.755453073853726,10.575538769801339,11.200513445897837,10.715772406372029,10.570059724910275,11.00531134546621,11.064839871025423,11.014011942895687,10.920709002988724,10.872465606689289,10.96240568266004,10.815730101563714,11.076217337122133,11.176725191363722,11.140542072564054,10.787647577655898,11.47652078307643,11.021085141115318,10.994806643710096,11.342089693279364,10.664924023794766,10.59252630505153,11.11137269368198,10.504382373390987,10.718675359005099,10.705377024100308,10.752548144113725,10.919985544827309,10.814886338329856,11.074079359329735,10.476132378440926,10.926819387090307,10.843553403061053,10.781681739143439,11.108649649373282,11.120149507978052,10.631591561105106,10.692172159805137,10.619178697530968,11.16455876890194,10.928668563118356,10.916523797267468,11.202738717978361,10.846186497686585,10.773755288097965,11.133800392193905,10.927537919877333,10.584410318473351,10.848482352538639,10.713483999592366,10.959505443571818,10.502873353281599,10.884235552246894,10.833089298469956,10.931802547900372,10.535105014302918,10.642515908352262,10.806571456923,10.888539128981071,10.416939723904,10.866471012402265,11.437091388570725,10.763567656573366,10.630963693419664,10.902518887949263,10.481700760003815,10.799065242812741,10.950543354289836,11.099256799511375,10.675700040192325,11.089469487341145,11.103151085273966,11.131372176908377,10.521048746139478,10.4160117329377,10.956090806107662,10.968715397184654,10.908576397569082,11.21381837484898,10.976662367940685,11.102292024009255,10.949753360832029,10.867920619736298,10.539376314255792,10.620326845352862,11.119764351318228,10.989284744157393,10.814866240049263,10.607203684445308,11.12548198735986,10.960617906749297,11.269234759268315,11.127365920036635,10.696661047163198,10.89209894598991,10.759667280669499,10.79812554671483,11.02805994287377,11.152471962691411,10.650980862836187,10.942349836798464,10.815107392760385,10.520725138995724,10.738372982159593,10.824088979997368,11.021052434120925,11.221396000789554,10.587165036719648,10.797798488802224,10.82994641332591,10.545999117127494,10.826495672157808,10.854063762376834,10.798595505142377,10.640771228584159,10.685194910075554,10.688644016385481,10.616804939885457,10.832733995570498,10.760580144684319,11.075907768348957,10.914524668948285,10.640268770116135,10.716327056014078,11.185587384638161,10.881324834061799,10.812632816249412,10.782242550881179,10.765934371538163,10.593003146862024,10.773964685870737,10.630021152113708,10.766588455896164,10.658176581190668,10.60797024275982,10.73898029158071,10.541650424763313,10.704748953825517,11.227108319127959,10.66825747676904,10.737048636811288,10.720399840430005,10.759922117256918,10.921197041535379,10.964190268131018,10.7510496637203,11.115874855463082,10.660219674721183,10.980007594729422,10.968508586209147,10.663007508460334,10.89536801535987,10.678306881740099,10.932928382342938,10.715328465053778,11.001549689898756,10.960478916513138,11.111342810376286,10.648088014684989,10.533561804120112,10.664386835146892,10.935176255838662,10.60472690299341,10.687046571956325,11.316472528909063,10.836320701029594,10.735461455680806,10.858864373117484,10.820278159451934,10.61351643196459,11.156064789498748,10.553257393126504,10.809626933353908,10.32790525356098,10.880101684393388,10.603287553926174,10.605792670880838,11.112149346348195,11.045255111518165,11.311029574819049,10.821756326793912,10.827885333304181,10.690125076183412,10.63224316056344,10.784109655130823,11.024105921466852,10.89256395413593,10.792201516640048,10.939461735355295,10.41643093227312,10.788308256940795,10.875440023235184,11.01821922308412,10.376517846806717,10.680194326195004,10.917848288756646,10.8192781593686,10.969404458366096,10.920962089744599,10.994067669506974,10.833977003810096,10.322230781590136,11.104882035847263,10.845251080383314,10.404232536959167,10.976269081169717,10.619716292539394,10.972911303739563,10.735983546667017,10.647779266419246,10.780787944718998,10.67239134549532,10.678007325311796,11.134267804781656,10.74265963085397,11.144062259306612,10.767642529989754,10.923164853116095,10.705780575356794,10.356948858912547,10.873622322882394,10.875931749013414,10.75868980502856,10.72267249346074,10.731362285036713,10.932946242515648,10.687229266240786,10.026324462495191,10.810798082829503,10.80642958564055,10.820298149257134,10.704232743694092,10.772539915583412,10.743480223454219,10.894718767073803,10.551192707649491,10.679274066616875,10.954641290044536,10.531562736352358,10.902629352637497,10.828856948343487,10.71541726908554,10.788968500016754,10.900731346815949,10.435585311577658,10.482093312723077,10.767937471740897,10.870832550232782,10.567875111424648,10.643971460585572,10.717944874528614,10.72961284769053,10.730203625017488,10.574159036330888,11.146099169975122,10.61075950714147,10.990718653830616,11.18066434912048,10.596634733096073,10.706385597055192,10.711390970394262,11.147598917894847,10.759688519532371,10.47211971339814,10.616339316370409,10.813116141536733,10.723729832149901,10.852361634306304,10.685560942290476,10.70038645533948,10.956806057566476,10.47432584620829,10.812733528283578,10.841207039823576,10.745356416842704,10.575921691498532,10.880064025283644,10.84263506655321,10.984377049549666,10.81376021208472,10.635061862214055,10.514963616951515,10.327807126158824,10.4825697768081,10.692149437438374,11.019743276376833,10.822454699613692,10.943940927030706,10.82001825561489,10.79687806452395,10.621766273733678,10.775680095688484,10.789731363057987,10.900528434095392,10.759518595997553,10.580911772630838,10.7030422005086,10.816854012893037,11.190996953789856,10.89295439394344,10.78766823049205,10.835868145559232,10.825342773882696,10.533721557035943,11.005842827483072,10.240745194931177,10.81833724661388,10.665647604383027,10.903990748093918,10.181346536039147,10.874096000619872,10.772770530802942,10.576763603453662,10.392527584230196,10.59610959523532,10.817495681252732,10.59848302395369,10.774718155003685,10.630262914076058,10.689350641595816,11.165719830979276,10.679135954607817,10.880854568917648,10.624298537078547,10.478273405260996,10.772435072899762,10.8333655579188,10.499793381646517,10.406684149137627,11.080402574461411,10.980263146595064,10.912393928119744,11.169462852503631,10.704546990290469,10.200959051807608,11.276722003067231,10.780850328399447,10.378229936129037,10.768021724837249,10.414723092275086,10.9110074208009,10.69112639618879,10.706923086990196,10.915906311504504,10.453456963419745,10.694849780593028,10.625343659732527,10.798370769971397,10.010771217755803,10.703379290526062,10.888259024780478,10.487823827237893,10.747659102532259,10.536566206629955,10.651193938585422,10.962440365141921,10.544762323685362,10.80687539905476,10.815549355080247,10.424006048273018,10.832141543393682,10.814303324130014,10.680378276528932,10.57141948395501,10.562819384601342,10.72092985236768,10.743696057004223,10.867482144479293,10.56800375029692,10.845212085667093,10.916868696841577,10.716482302801335,10.776745514592863,10.702615056633306,10.508513649700895,10.683775268411074,10.576661591263116,10.992941363419327,10.448337720413921,10.468062452296309,10.35932886796936,10.70958388210257,10.780995875187799,10.886819920140972,10.732104870140509,10.735983546667017,10.647779266419246,10.780787944718998,10.67239134549532,10.819178104338251,10.35236330172604,10.767979599176396,10.760113202088547,11.097591822663459,10.624881996034176,10.578801664944281,10.599754860432316,10.72141544999338,10.493632545506374,10.899217733236709,11.520407405317984,10.762699867370506,10.62815762466823,10.55706195797625,10.682628926262934,11.023355660471326,10.761237739396348,10.704973309924457,10.529479457908666,11.075907768348957,10.280313102435128,10.532922537124472,10.514393777712163,10.618640813358688,10.501582020144314,10.382481893932408,10.473110246810576,10.701355043866476,10.940366271398876,10.844705015934142,10.817235053137502,11.03766001660279,10.953067147626927,10.469113812768233,10.867215152334905,10.406805060811797,10.938094511228325,10.866547359936277,10.640675541671662,10.501994328941953,10.56761778402558,10.788803480110852,10.781764842212066,10.973082892133744,10.65975036741015,10.69319413230083,10.459152689774811,10.832161297455611,10.664153184826896,10.537441898283253,10.846050137149113,11.032402703134284,10.528677039912846,10.97009304506915,10.440799301537945,10.406049122883656,10.875307594202763,10.48200920725477,10.827845655488042,11.070272376307287,10.715150833328286,10.722496161603729,10.706273583613463,10.606659318618037,10.686292605026608,10.919985544827309,10.473675825695626,10.562690077043136,10.568132372623362,10.879404761186834,10.760431595689404,11.050413701482789,10.58666015194887,10.402867928617377,10.712482564117947,10.616265777045221,10.763292585423422,10.267818117285737,10.83820741987865,10.665624271244136,10.556411517605202,10.594732925806477,10.691967639914864,10.621522448603852,10.643160430533007,10.748325246336506,11.036774982471208,10.993176815825393,10.475652836535291,10.556463568406796,10.429989655687127,10.769263634169105,10.439483723444063,11.178445242969808,10.700724441620455,11.084386183891462,10.887754639419377,10.621229779951454,10.694124354373331,10.60179638880159,10.43623121160305,10.718122010680352,10.624809082278963,10.658881567825121,10.861035384258484,10.65737699505146,10.70333435175513,10.66253950798379,10.343772679288913,10.859364315442246,10.596734728096406,10.97078115794681,10.437521761439,10.56307794956723,11.274033556687879,10.829015489762766,10.798002912532443,10.37370990785957,10.657235825223923,10.865210435808118,10.737396175804315,10.706295987305591,11.138304740157045,10.693874867521128,10.942172892623889,10.771658895221004,11.003082691382058,10.538634788798085,10.80147173742764,10.804725558450654,10.791872515156575,10.657682794661007,11.016889926676873,10.668839108844997,10.552029549665953,10.83482451994885,10.67382722892598,10.452879829450936,10.6616497032138,10.723531666284424,10.821037491276446,10.571675835054878,10.533082392189554,11.034809015613943,10.583296168656894,10.917050175164489,10.616559901903344,10.740886580744084,10.927232606524687,10.701332529203802,10.565788852924973,10.66501741845733,10.851780700535777,10.635374561412004,10.649772575258925,11.094435905739312,10.536937805837946,10.555395985079477,11.179771716072842,10.715062005631752,10.904009132643543,10.555708566483428,10.55706195797625,10.715905550345243,10.431819050431784,10.863986539074604,10.54484131366684,10.96959386698131,10.413763024996637,10.639766059056678,10.758647284406052,10.64007729093891,10.802591432987462,10.615431953178978,10.96678349607667,10.625805110395854,10.900768235614668,10.600302996782498,10.612237376323481,10.79857507675918,10.54207294510339,10.777267364458066,10.770567031595471,10.982288213867557,10.637200694842734,10.691785809335006,10.740929863292568,10.474212829509952,10.700792025170644,10.79646871497466,10.68786843351892,10.636480251018197,10.974488807496055,10.720377750501907,10.53829032212183,10.446160619741239,10.650388747427439,10.68437084740016,10.703940854834315,10.865095759100743,10.325318014730557,10.770377934115157,10.491274217438248,11.2751503931113,10.988051625478178,10.705735744369607,10.593304192999618,10.465129857127469,10.54970034590686,10.672762093483625,10.930281553413765,11.033485452777471,10.95806087221029,10.663124474364906,10.80636877750035,10.776223392258185,10.490273717104664,10.96348028065585,10.920763241257452,10.689669599063263,10.654408235508033,10.82774645405946,10.517158531594276,10.58423315037833,10.838796290246044,10.622448667989053,10.523418670764814,10.452389003554346,10.809323826506423,10.749613297693154,10.865267769230652,11.02356774781948,10.611843491382025,10.836005901514934,10.634724999843208,10.799065242812741,10.950543354289836,11.0674036944005,10.579208779272696,10.87174435243489,10.721106460606913,10.95750337119409,10.692285763895006,10.716127417580799,10.656906351437641,10.697768830015422,11.08959165831958,10.777476028176377,10.554535882074735,10.583245495977057,10.705758160114428,10.649440632919003,10.509086848575649,10.6375367244165,10.450828309595938,11.045909368600698,10.611227735398973,10.601672024613341,10.530708582979907,10.610907392382792,10.808191415158364,10.499573020252942,10.395313826292336,10.940118048848356,10.472431129636767,10.499793381646517,10.406684149137627,10.723025063923394,10.670280098263682,10.589887018388692,10.745916435811829,11.088598586820854,10.707594543404332,10.503806470784879,10.73068474121633,10.728035733044752,10.980195005816189,10.481504425842441,10.898644916162183,10.685789644406967,10.580683180882003,10.812733528283578,10.841207039823576,10.554066422987296,10.713439512638157,10.479398422958052,10.7879160312615,10.521372248595526,10.93544352356233,10.431347268857898,10.474269339455718,10.81247165589451,10.7463470063244,10.565814635756187,10.616192232311604,10.799820445069336,10.900657565135907,10.804258472752247,10.90958242467033,10.871991155857218,10.68880362056745,10.743868690309933,10.650909827496076,10.987206145364233,10.777580343710097,10.670906977470661,10.635278356688278,10.943481538715826,10.501801939324901,10.583726782795289,10.69749764970145,10.699304130942409,10.623130596900038,10.940738489735812,10.55200340895048,10.546945414808707,10.661719979752007,10.935283171500128,10.641536394447272,10.767473952780994,10.390040975326398,10.493299942049775,10.901579445098683,10.541544766778113,10.582763977410282,10.335205031788359,10.528168508620523,10.527579359655915,10.678836646467854,10.586508636797065,10.811161264303168,10.797164509538696,10.620912625555597,10.621888164008205,10.705623658107903,10.796386824952913,10.99361393755394,11.004679843467624,10.82211555087377,10.663942852852156,10.9033470758296,10.486345424201494,10.43623121160305,10.576610581265145,10.54381395691249,10.705377024100308,10.614327292626992,10.576763603453662,10.566974175677647,10.690079537805937,10.712460298601664,10.238279807349246,10.604553298340369,10.694963080918322,10.784316896132124,10.800901228640594,10.276773762280058,10.703311881612331,10.541306995486556,10.579539437667437,10.582383667326214,10.785311055528036,10.577604807189267,10.603734470211297,10.609822392399646,10.489467029902544,10.459037945081628,10.446915884846131,10.526400019413622,10.49318904964302,10.578368924289181,10.921865448493632,10.293940540523788,10.759327397501066,10.46737989723881,10.611030613379805,10.659844246493957,10.712193073730345,10.637776676427249,10.753766678816367,10.622692267415363,10.69555203576704,10.828500138222152,10.49819466028282,10.76734750122231,10.479791880329213,10.813538859620264,10.454379685515201,10.64034056535614,10.59500841135149,11.008760940077243,10.754023023344816,10.737048636811288,10.590163841965762,10.800840083390032,10.67533038004441,10.670790918373239,10.524977601331843,10.552604472589852,10.813136275021739,10.83381924711004,10.61381136646669,10.640890824350612,10.634339875274723,10.751156772532244,10.531055670783255,10.49255117955275,10.353798548436128,10.938804990831924,10.399828782101146,10.778768772309705,10.689851814807207,10.407137492553023,10.72750947494687,10.659656479512229,10.357901542376156,10.730575416949513,10.796837137108716,10.461387583688047,10.336178646897883,11.097258494377467,10.677407943118556,10.895386559118505,10.621985665531742,10.598557882657921,10.73055355066186,10.846926416329294,10.805517075058013,10.459898209522603,10.30440902059442,10.734024298391375,10.694487133263578,10.773713403281205,10.513062888672096,10.990550065253778,10.35948733401834,10.514692305429964,10.773545846468581,10.792139837106326,10.664737208297877,10.681687944129537,10.536858189059995,10.623763400484325,10.330714152425806,10.700431526777717,10.728474070001383,10.522153614408765,10.88824034837718,10.446451173829926,10.50960517412297,10.637104665649787,10.615848952019878,10.89705409081744,10.448047714031748,10.776515814350669,10.728736979978141,10.598932092144757,10.527445413743076,10.603833757822766,10.465072828327909,10.512056756620776,11.44675361066998,10.746411575914298,10.48508845835116,10.78773018644139,10.71818842864865,10.722584331418851,10.58701359805202,10.595784371641235,10.66993166215753,11.025002234421542,10.596434713093407,10.748990946688572,10.389118437667562,11.142817848143117,11.033033102974123,10.581698744480091,10.646234093587358,10.77241410304393,10.727553340367766,10.789525241239263,10.688666818542567,10.746476141335233,11.09694021369669,11.046563197910757,10.918156480309198,10.749591843760111,10.79706221716655,10.77549196269881,10.955549666384403,10.46487320191382,11.142774410487005,10.626290618003583,10.513714974009698,10.68706941056728,10.606362266854584,10.840325732297943,10.889136422512594,10.610537638265065,10.603337221155746,10.320288170308038,10.606832558072519,10.782263315647524,10.706206369525365,10.572931006396837,10.809889551659912,10.5819271042238,10.623106250301866,10.543444904581953,10.55978919697525,11.034615432880917,10.598782425153532,10.70333435175513,10.72487402221026,10.470759670120469,10.851780700535777,10.635374561412004,10.649772575258925,10.630625447463311,10.88807224504927,10.46501579627588,10.798636360656856,10.603163375058774,10.999513165307471,10.655328079435291,10.715395068816916,10.552473837310304,10.693806814848333,10.868149313135678,10.683706524927356,10.848521219942494,10.59838320363019,10.737895551594969,11.048776662726263,10.607426294174273,10.7933316343953,10.51875426942055,10.607747754099643,10.790678976585008,10.714106609236245,10.752975869264068,10.85957575428435,10.721437517010912,10.558049817780505,10.933071254793802,10.803750523333086,10.755708986503604,10.487126739641525,10.724852030896827,10.637368723744101,10.48088712455176,10.509768800074411,10.53701741627757,10.686475437095863,10.929385768915433,10.506710025568086,10.682192971457658,10.802448995888462,10.531829509729958,10.72601690459581,10.418464547424595,10.750342457690289,10.643732990607813,10.10528488583074,10.681228606945007,10.499710751814348,10.668210931585294,10.574107898514463,10.819578264407616,10.403899137953246,10.543497634682945,10.451204254885868,10.538687773141223,10.802448995888462,10.551166545048927,10.644186034954295,10.632773779711947,10.612409652211436,10.889323003601277,10.754386065643232,10.650815105859214,10.71681489335218,10.467038444924999,10.700476596184611,10.718409790021994,10.859960074043116,10.531776160747578,10.875080532194938,10.741124611581021,10.600776145596624,10.573442868819397,10.775324703655977,10.8331879713202,10.709628540909296,10.968301732454014,10.70398576635862,10.622107529069105,10.796120636059609,10.646852449256691,10.780663165681714,10.404838432339576,10.66534423110322,10.72823300845282,11.647875850348164,10.419748378792058,10.42842316062046,10.601025081397367,10.73219219685162,10.779185430302025,10.794768121406115,10.727465607601715,10.347307614520757,10.935461338871026,10.714484433197,10.619349781839288,10.59202412053839,10.406532988983157,10.61665792430154,10.900583778011725,10.635302408736912,10.500949482961666,10.485982462992478,10.722584331418851,10.554796597479278,10.688142237340195,10.954571380751815,10.797266791448184,10.769642214916486,10.886969533950607,10.464388228934425,10.505040141934996,10.726500038828679,10.520967854170658,10.835376005033337,10.766968050577962,10.554614103833462,10.665110804398145,12.055627591383479,10.897757325726872,10.641488588729699,10.917213477500983,10.858094742694488,10.510613774571024,10.5815464756746,10.499710751814348,10.897757325726872,10.806348507298559,10.8590374583624,11.044855964091758,10.575130158308562,10.898275182551036,10.924948782015823,11.305372250327109,10.600651654454007,10.84263506655321,10.984377049549666,10.81376021208472,10.591069274623191,10.499958620830613,10.897294726838112,10.583802754280695,10.764920750925564,10.581064138105116,10.63110862095615,10.620668592170619,10.476414354531222,10.670489101666554,10.542627232264719,10.867691874024281,10.645043872303761,10.382977295992266,10.577349971684207,10.754855689525833,10.758073078973604,11.00988611600467,10.537601032592947,10.49620647826158,10.769473974500535,10.525568284662214,10.5815464756746,10.822055689154324,10.473053671324719,10.739977214206728,10.574746933338044,10.58197784375244,10.780954292552702,10.692194881655606,10.54499927491401,10.569520440604501,10.924516606545858,10.543655808305187,10.51875426942055,10.954414066971678,10.794604055861562,10.66230542558572,10.466355190329153,10.767832145387093,10.79121418728553,10.594908243570373,10.583600150825614,10.634388023957865,10.72753140789784,10.914215355893717,10.572931006396837,10.578547134297418,10.716526654599809,10.533881284434855,11.07123714670454,10.609674346603876,10.731231183345313,10.752783415586006,10.62154683379229,10.997288284207016,10.945688207278275,10.757434685999781,10.584916340141875,10.592877684218362,10.340838849506614,10.579768290986172,10.650175500024103,10.849550656077264,10.588073187434166,10.689601259598334,11.051762640389974,10.433380239019344,10.51986167429016,10.687160759795445,10.913541814222446,10.763165603983705,10.63739272556824,11.24217916922465,10.618885342030893,10.936565268616524,10.79589534394695,10.840893775014358,10.777893225036763,10.485367920667487,10.733195906296567,10.456567744198955,10.915906311504504,10.453456963419745,10.694849780593028,10.450191772337018,10.609575637228874,10.890050337395614,10.611227735398973,10.633159507778446,10.565247259854441,10.462445981601402,10.8365567356491,10.481616621511806,10.641799285050446,10.593605148535708,10.59885726144917,10.912977146041065,10.56429231017482,10.532016208758332,10.54702423254274,10.908576397569082,10.587770562157601,10.510477536644899,10.801675411712429,10.973734659647342,10.61019241102814,10.684943185186642,10.758413388658699,10.453716565076885,10.916015307290108,10.685011843713486,10.595158644212706,10.896813396877137,10.663358365138981,10.480634482333901,10.900823566261407,10.704906008379862,10.886464497605314,10.99854352500146,10.644662702106656,10.403929451547379,10.72731205673769,10.579208779272696,10.87174435243489,10.721106460606913,10.95750337119409,10.692285763895006,10.716127417580799,10.656906351437641,10.697768830015422,11.08959165831958,10.826495672157808,10.514420920278495,10.738090891650067,10.756433716893001,11.002066507315336,10.45472548691338,10.587114559711914,10.673433724065745,10.549412089723733,10.652282283934888,10.465329432318082,10.430698205551442,10.574746933338044,10.649630327748017,10.730422342894173,10.716970064428601,10.74017214809227,10.926747505407526,10.869291996279744,10.83873741881143,10.524117802256896,10.556307407873451,11.348663841392241,10.611474083292713,10.687115086224448,10.732759634666934,10.766841535026922,10.691785809335006,10.644519725816647,10.889192400494602,10.90546044504981,10.581825617442366,10.552081829046976,10.572137101495674,10.698604506679791,10.918482697282624,11.012891402282436,10.867463075975694,10.612557293639888,10.711413259732158,10.737461325921066,10.707258871553977,10.4410330010015,10.856727188188485,10.694283086332076,10.48071870349873,10.78700712807974,10.728298758274772,10.59425690831011,10.732519604116439,10.814142432791654,10.54970034590686,10.936583063952368,10.458291783474328,10.514393777712163,10.701197430581601,10.934070790806766,10.830084987398923,10.368667064416371,10.833483931466395,10.931516419748775,10.627163938130897,10.636912579594643,10.595809392596285,10.777288232789331,10.585371540817363,10.682628926262934,10.754748976189765,10.477006245640542,10.571137421822545,10.484948697900347,10.65603507637752,10.972104443668837,10.747121566370009,10.709248877465209,10.925956465688445,10.567437615438774,10.617686579792686,10.840521645548183,10.632604976885304,10.437463136200819,10.533721557035943,10.656976962102235,10.934641505999714,10.484725040542484,10.441266645862376,10.823172517478298,10.719294745831961,10.649938505118385,10.50523190962273,10.554353340839468,10.839620126623823,10.801879044522451,10.646186511925322,10.723223330195648,10.670814131270324,10.634917506521377,10.465500465071273,10.459525519123666,10.721481649585172,10.611744995900427,10.961416725928702,10.814343542920238,10.843670576829885,10.461330341065175,11.198379090182675,10.68889481152137,10.526614548389263,10.79174911168878,10.541148449877937,10.71203715957191,10.979411052949546,10.57813975045983,10.67948119887156,10.494048144320972,10.850191090818479,10.548651743073922,10.634436170322823,10.544130179113925,10.84095251964169,10.630867063391808,10.342226237407218,10.666184116368278,11.391548478803628,10.574440247586304,10.91221160274137,10.592952963693447,10.627018437730513,10.42129872047583,10.637920620001616,10.730400473259067,10.373084849239977,10.89588711066259,12.613751967124037,10.634989686972537,10.691581210405026,10.545893917642873,10.690625861516315,10.792592065365966,10.489661807091968,10.858229470784536,10.777705507988376,10.662773535600119,10.700431526777717,10.86172604501804,10.459668878022915,10.84345574776464,10.546314649196058,10.581165702192141,10.564034059049991,10.431347268857898,10.644114515280394,10.881945245621354,10.646662226695721,10.491607495228367,10.553309608357699,10.951052130693586,10.635182142708313,10.565634141976286,10.995595399782035,10.789484011776683,10.518105462931352,10.784648392426545,10.634075016069918,11.735420806241695,10.525648805362787,10.546971688076972,10.54032889688498,10.624687547538109,11.037772601141834,10.578878011506815,10.448627642716774,10.676046472520236,10.603088860335872,10.68695521229612,10.78526965194662,10.583068121374101,10.543893021838013,10.389702810329402,10.641536394447272,10.795055171354777,10.455704608661868,10.763080940731738,10.947538053211556,10.71663752549077,10.68226181906351,10.6236417385826,11.512365308111665,10.757264379021041,10.627866891777025,10.732977794273367,10.723421557166176,11.428238656803035,10.547575782806888,10.636792507070695,10.606708818667547,10.41771737543568,10.595909470156478,10.875250833534107,10.48136416355173,10.676392784874349,10.731143772668043,10.502736056652015,10.473986757787737,10.9246066585059,10.52166870060616,10.682674805188459,10.682055262024345,10.896998551203797,10.47779488921454,10.430963782371098,10.667722076311636,10.382543832613134,10.948681483450565,10.672205919943147,10.654007012953944,10.48508845835116,10.535530308692785,10.56741187441917,10.393692014097626,10.835159386448586,10.818897896982977,10.92818415825407,10.725709333961985,10.623374030285696,10.760219344553063,10.714551093197692,10.942809745178671,10.369357650500257,10.644329058958736,10.960374661156923,10.520131587109958,10.627139689534282,10.757583680817165,10.486540810299,10.947045095455094,10.96368813405067,10.834213592206538,10.614474651224404,10.425816755685535,10.738633302789303,10.573033399843746,10.971606268867896,11.094299126584241,10.861208094173422,10.73241048027168,10.477456975266742,10.57185524173185,10.777768084253218,10.621034619919609,10.76840077595051,10.614720200642457,10.843475279586862,10.96238834096801,10.485200252649769,10.550093288660157,10.66837383025105,10.448714603019452,10.782346370401418,10.81253209407131,10.664386835146892,10.698152876286422,10.84263506655321,10.984377049549666,10.81376021208472,11.26300149812105,10.43320362298215,10.579208779272696,10.85678501003938,10.765554384199836,10.437726922711134,10.640866906341545,10.911281225871654,10.74890507476649,10.632822003857786,10.581114921438036,10.809647137210824,10.673688362538364,10.374958854223562,10.851780700535777,10.635374561412004,10.649772575258925,10.572598155267832,10.6163148038629,10.699642483170303,10.492107203742139,10.786200818144286,10.534307099477882,10.812350768581487,10.817716159691836,10.735983546667017,10.647779266419246,10.780787944718998,10.67239134549532,10.600527147811418,10.5950334517291,10.705063038271945,10.798881458697299,10.527043468321851,10.632894335716385,10.545999117127494,10.652613284505339,10.614523765931814,10.653912584247546,10.79544460739483,10.632194908494624,10.65843513400152,10.412531590219688,10.684050195099022,10.676969705748347,10.617735537004092,10.875818295292955,10.593178768122684,10.736027041947786,10.66448027999114,10.693239529068588,10.573058996567367,10.460471308283202,10.562560752762321,10.586508636797065,10.58481515629073,10.476414354531222,10.531189134021004,10.924066225065138,10.652707835976868,10.614744752268392,10.506710025568086,10.767284269446213,10.814986823674152,10.514013704407736,10.53252278762883,10.683156406867319,10.577349971684207,10.66534423110322,10.712705192018595,10.565917760434013,10.600676553922405,10.912539764491594,10.506108093896515,10.568620986640875,10.79961639258633,10.67069806139613,10.665530933243835,10.70958388210257,10.809606729088786,10.731689964088938,10.838403748533448,10.706295987305591,10.73676617241622,10.728211090884793,10.600502244622563,10.734285753389923,10.759412379123841,10.533854664973365,10.702187730228152,10.60005388114173,10.87632873570067,10.521372248595526,10.536008548778417,10.684554031133956,10.585801262389678,10.6699084287665,10.598557882657921,11.027231381841842,10.791687404243758,10.601696898688338,10.797369062897154,10.619643001144993,10.666673723876048,10.836261683668637,11.09419272986116,10.59109441383156,10.485451744135313,10.682009354665388,10.939514966012617,10.462045638444781,10.913468971726102,10.774843678016403,10.794522012994118,10.658035524203411,10.62927131837234,11.017677871167557,10.605098811508203,10.66066531275321,10.64960661786218,10.521345294054358,10.732214027337896,10.75585823864405,10.690694130998745,10.733871751401159,10.556567661882832,10.587215511179581,10.76301743858852,10.60415637449492,10.795403621268628,10.989757318005852,10.507803519389457,10.742076168746246,10.642706921198457,10.824825525631796,10.515261974630336,10.621766273733678,10.39592514798884,11.262320784758563,10.693421095533761,10.739023656715148,10.678652412305714,10.639167263814777,10.560437444784185,10.885771996244106,10.663709098760394,10.874096000619872,10.654974393434033,10.804684950962628,10.621278564008833,10.556411517605202,10.851548232499086,10.60641178160999,10.575615365871998,10.463788819762645,10.727728782812129,10.568389567655771,10.504985344411832,10.695936934169936,10.757008864157203,10.911043932475511,10.732170365888766,10.559010744499384,10.55810178337929,10.580047929491675,10.806186330890815,10.570496075486378,10.601398368945096,10.546945414808707,10.587795784428868,10.603858578185394,10.719272631478638,10.836792714569413,10.940773931876523,10.690102307253893,10.756731982692648,10.735026171542216,10.785869836159096,10.619765150484927,10.828876767395542,10.461044078789724,10.51642742854388,10.75585823864405,10.75585823864405,10.634652800283595,10.564576309402185,10.864828128963993,10.751670735195605,10.941677282305049,10.775951780869729,10.787647577655898,10.838089604181535,10.873754975267016,10.655870155127044,10.638328347645203,10.745658004488513,10.917013882134562,10.675954102300329,11.029325827457829,10.63660036103912,10.621888164008205,10.640412355441962,10.658317618283657,10.696593183839905,10.328526503601397,10.757860326595294,10.584966928228392,10.767600388351703,10.685652429413727,11.039218988640071,10.753446155719935,10.542759160126755,10.613909658640255,10.814625029169482,10.900233214800668,10.586079219156558,10.699281570056216,10.837048295575237,10.670535540935608,10.835139691522983,10.784379060058418,10.904836087750256,10.876177521259402,10.626290618003583,10.557139982397933,10.644686529501012,10.769663242978435,10.876385435221573,10.917286047758095,10.877952848461355,10.639406824939943,10.49819466028282,11.132162725502406,10.78766823049205,10.628690415536205,10.72753140789784,11.021232309353408,10.816452760981706,10.846459162991614,10.909417871295242,10.692013092394305,10.669652825832646,10.657000497882507,10.75064254557542,10.881794878160589,10.41078696652556,10.67690049281473,11.020512614211363,10.658717115392617,10.82599889622334,10.90498303042451,10.729218802151282,10.576151374154673,10.763652278630156,10.52331106867723,10.696163275810974,10.521210510449233,10.574695825577319,10.807138740863818,10.752270024627522,10.503504675098267,10.925578703296495,10.771260083255557,10.806064681322521,10.645900974398991,10.763990695266562,10.58159723451934,10.66967606516289,10.716571004431286,10.90668965639958,10.589131655274922,10.577706723210554,10.65681219612839,10.77616071925456,10.501774452072114,10.863986539074604,10.58671065189838,10.734852004820683,10.742810843253675,10.882621619531593,10.683523185864164,11.075102440753938,10.730531683896064,10.684027287428389,10.748711835976422,10.690261678874698,10.746131744241984,10.945688207278275,10.757434685999781,10.71254935769243,10.646138927999163,10.693375707007972,10.838364485885963,10.63962238089551,10.736027041947786,10.927430172867208,10.594808065754666,10.928829979276463,10.560281903630274,10.843416682975683,10.821516772364003,10.733152287697589,10.696027476974109,11.272584888827497,10.543392171700354,10.75042820627549,10.666697032541045,10.74819634990461,10.649227183215244,10.725753278416203,10.863890859028604,10.667069897311976,10.70463675689735,10.560255977752359,10.519915662682669,10.71152469897003,10.788514629733339,10.673063225045645,10.697994757448491,11.019317430821303,10.858056245620261,10.731711805541833,10.578190682516476,10.940472633633293,10.715328465053778,10.489327880107565,10.748582989368131,10.566613573984062,10.967215047683993,10.863718611872649,10.736961733187352,10.541650424763313,10.704748953825517,10.894291888569933,10.812733528283578,10.670256872966688,10.546577516554702,10.929475383483236,10.646971319984914,10.830183957124165,10.542416111476454,10.65254236503437,10.800513912228825,10.570239421736542,10.579819140167512,10.760367925078675,10.77616071925456,10.531242514329021,10.486177920013498,10.791399385808587,10.662422473634077,10.617221366704461,10.753723948338848,10.554196850398105,10.410546089732875,10.83645839466148,10.721746404137187,10.438957007214878,10.698672233649825,10.571778357097207,10.96086109318764,10.550747850323598,10.603635172740818,10.77067207030233,10.7655121544701,10.605792670880838,10.734263968084111,10.667931614978107,10.929797929448833,10.688119423218252,10.54191452089584,10.83861966554364,10.749591843760111,10.622716624094574,11.030492915705455,10.567643519745475,10.706766348932756,10.689510133046271,10.813840691743529,10.806145782678987,10.8081104795426,10.705959879210065,10.632315534301455,10.812874508093488,10.791831382359332,10.622887104240139,10.814866240049263,10.900362383966321,10.632436145559456,11.17300930484645,10.762784562890163,11.068106034783508,10.76896908335696,10.666114152865877,10.768316554785683,10.750406769818508,10.609674346603876,10.840639175077612,10.909765230001442,12.009747494498253,10.947326815356947,10.579208779272696,10.87174435243489,10.721106460606913,10.95750337119409,10.692285763895006,10.716127417580799,10.656906351437641,10.697768830015422,11.08959165831958,10.892749896866105,10.730422342894173,10.584916340141875,10.535105014302918,10.733370361669143,10.782180253994964,10.878235853981852,10.819338187581879,10.737026911613315,10.662352246449105,10.727224302799675,10.503971048232653,10.622131899994592,10.733152287697589,10.603237884229646,10.599455750282775,10.484725040542484,10.98776424243687,10.480157095037379,10.601522767168849,10.8653824262153,10.829689010518798,10.786655739574796,10.487321973155373,10.61771105869799,10.536672391923391,10.967353104874404,10.659985048596836,10.722738609891799,10.891280006098993,10.579208779272696,10.87174435243489,10.721106460606913,10.95750337119409,10.692285763895006,10.716127417580799,10.656906351437641,10.697768830015422,11.08959165831958,10.609476918109369,10.535928857978679,10.774215905333193,10.61712339952339,10.805699643800724,10.683202261599535,10.550590794594667,10.868892205688535,10.805415633574446,10.809465287801839,11.534461882500754,10.674336240759926,10.728079575387694,10.712838744972538,10.836320701029594,10.598208494084364,10.746282432565001,10.644543556617958,10.600103709234817,10.764307856884209,10.650980862836187,10.812632816249412,10.719980048331397,10.857863738015615,10.715284060080414,10.71203715957191,10.601273955244498,10.626169263198392,10.739153740836397,10.816533024245254,10.751949021382632,10.559244343877515,10.78526965194662,10.761386168696564,10.898404604865473,10.650009609487778,10.704906008379862,10.580784783666008,10.571137421822545,10.589811507747948,10.768274441543168,10.58435970222046,10.835159386448586,10.533215585226419,10.53810479090567,10.879951039444416,10.515966830028619,10.616486378798674,10.614671095582173,10.745765692323122,10.679527222435633,10.733457577943756,10.759391134395187,10.5557606538861,10.73950054911992,10.831509207285983,10.692603786704465,10.661813674121044,10.640101227841237,10.76629311593663,10.960287773389798,10.906304543749371,10.782346370401418,10.741232788688686,10.78039275767599,10.896405936645174,10.556567661882832,10.793660156255225,10.763715740473742,10.539614544996624,10.691035408517557,10.720245200685072,10.733719181136808,10.943304794693733,10.664900673766162,10.673040064298478,10.88754907612852,10.697904392600355,10.622424304782367,10.742681234025316,10.836773051786144,10.508076706114283,10.631832943746039,10.799555168721248,10.663288203650593,10.645877175924472,10.786490337544109,10.817555816557183,10.602840437817578,10.695506743860696,10.70340175915424,10.607228421306944,10.652707835976868,10.554457654196888,10.650199196425806,10.950595998337121,10.834489541275977,10.603213048456196,10.579208779272696,10.87174435243489,10.721106460606913,10.95750337119409,10.692285763895006,10.716127417580799,10.656906351437641,10.697768830015422,11.08959165831958,11.354527444615577,10.727202363111877,10.725071922271374,10.598408159645215,10.910660493387415,10.856438028772885,11.17218011157584,10.859787148429518,10.672877924046807,10.639861833030173,11.020332609465298,10.754129814173721,11.09815216979044,10.720664881512924,10.625246485085315,10.800860465555639,10.61038969832841,10.658764104561621,10.75062111371267,10.676346616822633,10.59026448608823,10.857940745504632,10.746734361340112,11.28835589737794,10.8134181012576,10.733479380823917,10.82587963326826,10.600253178618784,10.579208779272696,10.87174435243489,10.721106460606913,10.95750337119409,10.692285763895006,10.716127417580799,10.656906351437641,10.697768830015422,11.08959165831958,10.804847371021863,10.51194792492888,10.804766164289779,10.769558098246614,10.769200523441311,10.534307099477882,10.65678865591582,10.90742279426233,10.907111276342949,10.697678444748158,11.055324602441535,10.9859196449752,10.989504181217818,10.579208779272696,10.87174435243489,10.721106460606913,10.95750337119409,10.692285763895006,10.716127417580799,10.656906351437641,10.697768830015422,11.08959165831958,10.8481713589115,10.56887805605103,10.813257067420018,10.973494584193903,10.640508067540043,10.118760209469768,10.669211175914377,10.854488842085678,10.714239975170337,10.611350916931753,10.6378486508044,10.776933411917968,10.746712845552901,10.830797350892716,10.715284060080414,10.82546210087858,10.687731503489951,10.601448130091603,10.67181177644663,10.84372915856607,10.749827811712468,10.761237739396348,10.622448667989053,10.590868138201737,10.709382892787827,10.95399444252939,10.702345187518187,10.708041930670204,10.925056796705926,10.81281409060865,11.018907792853605,10.776787272605189,11.385921295032222,10.733958923959293,10.569520440604501,10.616731434795195,10.725994938401781,10.502296580719984,10.847062657437341,10.523875850511647,10.894755878333363,10.54141267859585,10.769074290035578,10.781723291541018,10.597933888827693,10.504820933823419,10.692058542807912,10.81935819618558,10.554249016599636,10.690785149725912,10.641273434714453,10.947784440991967,11.038431770451629,10.664083079084039,10.480437938693562,10.674914348974756,10.575257867336488,10.689327855026217,10.781723291541018,10.935318807513887,10.830005804565719,10.888707153849147,10.751199612844985,10.721393382488882,10.9110074208009,10.650412438776545,10.59144629640695,10.7177677069941,10.68260598601082,10.723751848155539,10.616829440381593,10.54883532796278,10.486652442359842,10.691376569605758,10.65135963278532,10.711702975923748,10.629634211359182,10.751670735195605,11.070941590161643,10.725005959935844,10.877764133608936,10.55706195797625,10.776975162084973,10.71798916150825,10.911919812973826,10.81817700304331,10.666487234994907,10.714239975170337,10.661977618146238,10.628375618880137,10.725093908749692,11.071330462204312,10.98512321699712,10.96323773041211,10.806267422382335,10.725643413659608,10.711792102483521,10.9859196449752,10.80578077476643,10.550721676081666,10.672692588705143,10.8111209173191,10.528168508620523,10.78839081116865,11.0389459423249,10.704232743694092,10.749527479199216,10.68354610508537,10.710699754384043,10.539614544996624,10.857285992746686,11.136412178811831,11.029131180255268,11.000314915838985,10.735700781219071,11.12041606802228,11.811235856211189,10.8457773602789,11.051270885210688,11.862751005207715,10.68679531280403,10.675029930523447,10.553779422789644,10.619911710000567,10.648064268202436,10.769032208692334,10.993647554389254,10.704995742766139,10.858595069841899,10.83506090794144,10.659445199506749,10.67099981505138,11.217009587591344,10.66955986311063,10.544209219042303,10.747121566370009,10.665600937560797,10.601124638368926,10.744688291770704,10.818717722212963,10.772057548198871,10.847198879986275,10.976525590084808,10.926873294961768,10.711814382882341,10.321967597721788,10.873830768729865,10.62607216874969,10.695619969780495,10.649985908593068,10.79845249769553,10.822155456696034,10.645520130825885,10.681894577046897,10.720775294568275,10.53966747745482,10.655422374579162,10.53691126761627,10.97078115794681,10.437521761439,10.56307794956723,11.274033556687879,10.829015489762766,10.779560274121492,10.753446155719935,10.794029614387506,10.620400086646335,10.554770528997375,10.556333436322548,10.821237219646527,10.579183339482318,11.123771602253786,10.540275999426688,10.958235027557299,10.568132372623362,10.568209538078998,10.840306138861743,10.859018228147887,10.706430398918958,10.71710304904691,10.692308483164355,10.640723386272409,10.835946865571866,10.735983546667017,10.647779266419246,10.780787944718998,10.67239134549532,10.705982289931356,10.78462767712726,10.630746262724841,10.67835295938093,10.627551835730795,10.595459042242352,10.959522835329864,10.648539090746434,10.582130046893191,10.826455939163523,11.259915314049724,10.891689559877268,11.00973726833345,10.669978127320283,10.451493347426403,10.716726213353894,10.770314893674692,10.728539803976012,10.673966076032396,10.641918757936217,10.619227581748708,10.76804278700223,10.372991056740181,11.215704710259702,10.695619969780495,10.914470091243263,10.878518779432882,10.528677039912846,10.683362736605897,10.71818842864865,11.205584754855263,10.729984859292829,10.698198048505514,10.811504147958038,10.726543948550297,10.68562955841758,10.928542999201673,11.20446909330197,10.747745081510452,10.885079014992419,10.686612539214305,10.767431804038074,10.588148829445775,10.80419753244326,11.160171395774732,10.350414450451886,10.959470659148279,10.616853940277469,10.70504060693986,10.637632712130145,10.751670735195605,10.83814851376516,10.859787148429518,10.599829623992592,10.78549735043341,10.838423379279122,10.705915056260707,10.967353104874404,10.847840822175167,10.821696443566188,10.9206005176251,10.790349473719472,10.697746234464486,11.06253621000807,10.708757334233022,10.860459469017288,10.94598793840407,10.799881652695827,10.599031857695795,10.738633302789303,10.490023435536594,10.805577935009142,10.729415844329893,10.633304117453084,10.739478877125554,10.756284550625612,10.540884151324754,10.79671434481173,10.721658160407951,10.930245737436254,10.744429542820429,10.579208779272696,10.87174435243489,10.721106460606913,10.95750337119409,10.692285763895006,10.716127417580799,10.656906351437641,10.697768830015422,11.08959165831958,11.459914907456342,10.464987279030074,10.697610650436076,10.761195326977985,10.943569899013834,10.642420388245206,10.687617380807945,10.730444212051008,10.800758550573029,10.561887996766238,10.785186839640664,10.828718203979754,10.872579441401411,10.684096008866067,10.761619370236751,10.815288219137418,11.244195985435134,10.620424499218812,10.782470939599769,10.667559071432771,10.739955552540295,10.8565537025729,10.988862614422217,10.657823901408495,10.731012642324293,10.6236417385826,10.649725161670181,10.706295987305591,10.778018350162052,10.797737153533403,10.72823300845282,10.767726807938478,10.681182661619935,11.099453386460148,10.630552951299533,10.678951775585286,11.143194228813176,10.84778248081988,10.887380856545494,11.372225582867094,10.868130257349865,10.605346673698095,10.736201004154935,10.607673580211289,11.113998933701646,10.725137880256161,10.905166678408571,10.73644015278695,10.99581345656153,10.650151803060869,10.571034834045788,10.844705015934142,10.769747350804717,10.739110381342828,10.749613297693154,10.819578264407616,10.926639673194344,10.821536737425147,11.139482142884802,11.185698360112696,10.849628306379168,10.751178192918026,10.656882813441431,10.864063076520587,10.586053953551886,10.732628716054485,10.673919795805615,10.62490629943787,11.232510258110352,10.714373323320329,11.046881983976132,10.710811273158345,10.61996055839957,10.75293310498079,10.721084386282662,10.87434222440065,10.699304130942409,10.615873475949103,10.8104549569494,11.16737413785572,10.957276797595917,10.696095378697706,10.717302492821046,10.760261798384528,10.930281553413765,10.809222770470766,10.77191069453828,10.563930739922945,10.651667277765442,10.75688108223817,11.104521041303386,10.668187658180978,10.743998145734295,10.586761149297775,10.775429243836092,10.667815210028436,10.874190709248845,10.882903307029347,10.758540974939093,10.848832104801021,10.867024400007148,10.924534617586627,10.80608495727828,10.659327802434497,10.853019618190086,10.829174006050646,10.818056803511944,10.740713431813928,10.650175500024103,10.919533117547275,10.561525555982506,11.00497902570508,11.235127714592425,10.764793976077524,10.76675718243303,10.839325977252653,11.12824779319225,10.84786026853724,10.660805999303808,10.674266845309926,10.85678501003938,10.684576926741435,11.142629604671352,10.770861112175668,11.006755652740432,10.72276064773077,10.989824810328626,10.794604055861562,11.083556932780505,10.726631762209768,10.779476987636757,10.81975828421028,10.733457577943756,10.739933890404625,10.652991436763397,10.637776676427249,10.714084379851219,10.979121175633827,10.568132372623362,11.042265620462347,10.77991416431514,10.913560024017496,10.786800443913076,10.828361344340758,10.586357098684939,10.523176549783848,10.824964811097583,10.797859820309261,10.696231168314535,10.731143772668043,10.961034761585639,10.914433704451666,10.631084467825298,10.83312876877842,10.79294137445669,11.070972705490613,10.70953922130135,11.12813025502894,10.932499642474284,10.818637634116012,10.8933446813672,10.794706599981259,10.726873210019802,10.572598155267832,10.6163148038629,10.772812455129538,10.61707441233353,10.836694396786596,10.76377919829018,10.664830620408827,10.70602710986727,10.822235263563458,11.001783124388094,10.834115020510335,10.661602849444407,10.754386065643232,10.929564990020989,10.706251179419397,10.720311477789672,10.771029119400374,10.53781317228773,10.791090702546029,10.745507222034997,11.443050061309151,11.02057806245001,10.759688519532371,10.96629993707305,10.995763139986401,11.203011416743363,10.817555816557183,10.650222892266003,10.952594421300399,10.804705254912761,10.85562793730398,10.625343659732527,10.890553566459324,10.843572932976,10.777538618802406,10.669513378508645,10.689259492201895,10.741816742940571,10.588199254274972,10.682651865988806,10.628133400155445,10.784461939282716,10.796816672772936,10.888053565157241,10.699687588152155,10.825183649068833,10.89377196431861,11.031788084906063,10.752098835720146,10.904211340385112,11.313315318038732,10.789504626720456,10.881136754541224,10.945582398369066,10.735135010341178,10.745033186257967,10.816793835369323,10.632846115058646,10.865936416391367,10.636840537810377,11.113626308252979,10.612852511118907,10.743372289207658,10.875969564060025,10.76159817234382,10.8846292567299,10.642229320654465,10.916360382256528,11.027166367619959,11.188178221181435,10.774801838762809,11.000949179446842,11.092519292992764,10.763504185331106,10.62582939137535,10.940844812389727,11.07126825283867,10.635903522016774,10.691944912900398,10.890143547070847,10.79117302739995,10.803547271299866,10.814182658053124,11.052539437962308,10.790308278226252,10.84536805540928,10.925578703296495,10.700859604153607,10.988423410387995,10.787544307076562,10.67160304933338,10.880967452722706,10.750385332901992,10.859248966318772,10.89897755957152,11.489298534339072,10.850152288265265,11.374926966812938,10.678744533629564,10.68285829984469,10.81817700304331,10.666487234994907,10.798350336996663,10.890665360757932,11.099211427803652,10.675723139415037,10.865898220023837,10.796161592809286,11.059141581571435,11.024154831985069,10.723795878712753,10.777058657190121,11.167035015895737,10.927537919877333,10.876593305964516,10.781266120176918,11.001116024081504,10.921431938136783,10.67489123106184,10.869653573903932,11.063069501527256,10.796959914329603,10.675884819035673,10.778206008499323,10.691581210405026,11.022947673717075,10.864522178219675,10.49656574811856,11.580200862442666,10.797941589801109,11.04231365081754,10.913978757809058,10.858729730545223,10.697000294715387,10.856206641023835,10.809869352700158,11.084155905330146,10.937454647710707,10.62924712082355,10.945476578263147,10.883053507923325,10.821157333085402,10.677661571738447,10.850113484206355,10.82994641332591,10.726895156930228,10.782076417226271,10.832260061912338,10.722385938401633,10.846478636240239,10.876895586294035,10.737526471793554,10.973100049353933,10.844392845174202,11.00796593531503,10.83700897967195,11.032273341211786,11.169688398396127,10.761937284720434,10.657870932566647,10.946904205736288,10.787709534884778,11.082542468899101,10.830164163962701,10.729547184215814,10.913505393637527,10.915960810882316,11.214478997071259,10.816974357077548,11.05530879953538,11.041592953151035,10.661954199216716,10.914324536132202,10.865898220023837,11.078659567256338,10.877122236592484,11.06788758174224,10.766335312700145,10.830777569868651,10.672692588705143,10.819958268212227,10.685926840574835,10.649630327748017,10.753232416566384,10.822933302103584,10.624711855667964,10.83415445035479,10.693602629038537,10.80640931667133,11.016889926676873,10.640316634182197,11.01713622603035,10.84560196441974,10.891335864219382,10.963653494818272,10.824029236297822,10.602343407563055,11.290194328601283,10.852419709126046,10.7131947990075,11.007170298017343,10.752377002814772,10.775094676783644,10.73269417750317,10.99058378524299,10.856110213657674,10.89910689102049,10.80594301695381,10.643160430533007,10.749484567190283,10.894273324500688,10.574823590081959,10.698943095669854,10.710141973889668,10.768295498386117,10.738915240352844,11.284844745876201,10.716127417580799,10.920907862260288,10.578241611979182,10.844080576933248,10.811161264303168,10.915815472607225,10.923236992778513,10.685240671430098,11.146272332647454,10.756923678025453,10.940277627560896,10.910897877777767,10.974899921277583,11.490178707974312,10.667093196744634,10.862052024637613,10.898589464834572,11.101266212698736,10.711814382882341,11.503965443598718,11.148304751131443,10.861131337893761,10.71944953261348,10.736309715168556,10.82599889622334,11.016512149807108,10.731078209645563,11.037241734449294,10.911773886155865,10.736831363589356,11.882127614785785,10.579208779272696,10.87174435243489,10.721106460606913,10.95750337119409,10.692285763895006,10.716127417580799,10.656906351437641,10.697768830015422,11.08959165831958,10.841970211916781,10.957015302715368,10.519078514877199,11.171983252877563,11.01049781265528,11.02057806245001,10.950192323132216,10.875156225259598,11.138973558699526,11.733160791495264,11.268290110505259,10.823351891463572,11.089729082831749,10.821297130379554,11.239685271415658,10.723619744850563,10.888053565157241,11.037981653092004,10.771742835371727,10.695642613426124,10.856650087186134,11.000314915838985,10.735700781219071,11.12041606802228,11.811235856211189,10.8457773602789,11.051270885210688,11.862751005207715,11.328738168766431,10.74218424297173,10.74714307336516,10.913104679632676,10.802733849801024,10.863297438323778,10.912011006422551,10.846731753970541,10.767305347149167,11.064056908254452,10.888427096715661,10.365868452461307,10.773755288097965,10.97078115794681,10.437521761439,10.56307794956723,11.274033556687879,10.829015489762766,10.975944075393727,11.13579996959208,10.998677324402907,10.781868711337063,11.003332414606783,10.838462639614411,11.310552209864484,11.139322330010808,10.768127031226284,10.925956465688445,10.885809441013075,10.896239200504729,10.790225882148258,10.773231601753162,10.857459351377972,11.239685271415658,10.723619744850563,11.310478748872237,11.305999691678853,11.145738318072041,10.658529136633662,11.070194531669575,10.735635516297855,11.545557210783578,10.80191976610897,11.295217116145958,10.936725415239998,10.692240323807754,10.795014169263665,10.93713456235188,11.33553174641257,10.998125286448827,10.826714175411395,10.927250568714278,10.971967040924001,10.936511880708872,10.748690362694553,10.880120513416445,11.076062564714649,10.98317183131872,10.799269407778743,11.61722241524285,10.618787537737207,10.852574558825365,10.83370091325064,10.72983169480481,10.925524725589275,10.82191599787183,11.195622321671587,10.937827951184097,10.57826707573789,10.855666527972762,10.927106862162807,10.8938091107312,10.921431938136783,11.212441800681239,10.97078115794681,10.437521761439,10.56307794956723,11.274033556687879,10.829015489762766,10.722914899006403,11.2506641951986,11.137475365705162,10.655280928528807,10.798942723822146,11.35501940920405,10.425371803658852,11.07980134886809,11.10128130578535,10.634556526094629,10.904450260467481,10.824487180138018,11.213197801473246,11.005693376714367,11.05606705747418,10.911043932475511,10.732170365888766,11.138973558699526,11.733160791495264,11.268290110505259,10.951315189365955,10.904027516855184,10.915906311504504,10.453456963419745,10.694849780593028,11.08780341895267,10.963636174752109,10.876687778383364,10.725972971725227,10.964415280897114,10.932946242515648,10.484725040542484,11.083833426230909,11.182558552867995,10.955776631598594,10.97078115794681,10.990651221810495,10.7743205614855,10.96521107361782,11.520863872271748,10.973082892133744,10.791255345477046,10.947538053211556,10.879894541737267,10.888165639275709,10.860459469017288,11.213076339885324,11.431444223102345,10.84608909920008,10.801268021651186,10.939674640985677,10.81777628173961,10.958165369058063,10.789978653171763,10.965020832962818,10.77605625551905,11.089805421623343,10.750342457690289,10.978899448033802,11.165946222581114,11.169660207941414,11.007501890493232,11.14161537641205,11.065199828147462,11.064213549858781,10.89905146530479,11.18711221893464,11.122738056213281,10.84372915856607,10.964294126468339,11.27831643554674,11.140542072564054,10.949999203458866,11.368916516819747,11.274795171347694,11.143772999520383,10.989588567267166,10.849880628226726,11.025425666507735,10.969473338377144,10.821037491276446,10.963740090649603,11.308554598979303,11.371626842506773,11.200636442925564,10.811181437184764,11.07678978683568,10.616608914303491,11.470341502428932,10.906029372453505,10.952979622572824,10.970591974102547,10.933035538594716,11.000314915838985,10.735700781219071,11.12041606802228,11.811235856211189,10.8457773602789,11.051270885210688,11.862751005207715,11.043737502977494,11.000314915838985,10.735700781219071,11.12041606802228,11.811235856211189,10.8457773602789,11.051270885210688,11.862751005207715,10.938556380385453,11.378628064751071,11.18375450901049,11.050159579947797,11.061233155495746,11.047789967121354,11.05123915076453,11.13126965261369,11.064213549858781,10.89905146530479,11.366013522154168,11.023323027655763,11.07969339830934,11.125157828696091,11.01049781265528,11.02057806245001,10.601273955244498,10.351692814320451,11.000314915838985,10.735700781219071,11.12041606802228,11.811235856211189,10.8457773602789,11.051270885210688,11.862751005207715,10.83728415853995,11.10399435721889,11.07569101317308,10.703019723800088,10.924732717627794,10.884348055059583,11.275987202633829,10.832714252818556,10.916850547197763,11.390317055902848,10.73496086257636,11.66012921350686,11.014044880972106,10.823710542937889,10.999178912776575,10.817936589530913,10.97078115794681,10.437521761439,10.56307794956723,11.274033556687879,10.829015489762766,11.6203438617375,10.780933500586716,11.006639521246269,10.811766273800105,11.354785170537204,11.185878668996171,11.44034401938941,11.135260331719744,11.093112922904789,11.366268305126779,10.955916276899755,11.09762211972616,10.95164829770814,11.243790329805025,11.26025011104998,11.19507280317333,10.903236690400366,11.427672540995461,10.796079677632406,10.880760489345077,10.627163938130897,11.431737101283387,11.273411140805074,10.95506064319845,10.913031805286236,11.418120157696316,11.380090972311647,10.745399506361185,11.138973558699526,11.733160791495264,11.268290110505259,10.934534521708471,10.77833109449611,10.894199064777272,11.000314915838985,10.735700781219071,11.12041606802228,11.811235856211189,10.8457773602789,11.051270885210688,11.862751005207715,10.869748704184923,11.506625662821701,10.856727188188485,10.784461939282716,11.098076465551722,10.937294617838122,10.91565194179493,11.232841123193209,11.000314915838985,10.735700781219071,11.12041606802228,11.811235856211189,10.8457773602789,11.051270885210688,11.862751005207715,10.933535449335354,10.986969282777263,11.11173122371271,11.118148039566904],"xaxis":"x","y":[null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,8.202756381655638,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,7.990238185720363,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,8.38091517312361,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.094480485881647,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,8.709795057617749,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,8.828054536815424,null,null,null,null,null,null,null,null,null,null,null,null,8.07775756373692,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.524128691512443,null,null,null,8.118505067587098,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.559235128595953,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.049584593096789,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.825958350026891,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.77121251322631,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.76898425919765,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.928862858867356,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.308917935337176,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.73293645134109,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,10.137135736495424,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.912992239550373,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.884508585938326,9.44375103564617,null,null,10.154401900795694,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,10.526855838488157,null,null,null,null,null,null,null,null,null,10.29434650825493,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,9.7925001243465,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,10.17041829781828,null,null,null,null,null,null,null,null,null,10.50681942877371,null,10.649630327748017,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,10.298262389436102,null,null,null,null,null,null,null,null,null,null,null,null,10.788824109088377,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,10.366875596977243,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,11.26104802108292,null,null,null,null,null,null,null,null,10.736070535336799,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,10.693965597214751,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,11.052016354930764,null,null,null,null,null,null,null,null,10.617760014711022,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,10.90641459106983,null,null,null,null,null,null,null,10.808494865389797,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,11.367101686736445,null,null,null,null,null,null,null,null,null,null,null,null,null,11.128482828081323,null,null,null,null,null,null,11.38173418927788,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,12.073917448371265,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,12.122337713310237,null,null,null,null,null,null,null,null,null,null,null,null,null,12.320204579575087,null,null,null,null,null,null,null,null,null,null,12.20766138281847,null,null,null,null,11.730348686349531,11.872472281133389,null,null,null,12.296269775947676,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,12.623153363810568,null,null,null,null,null,null,null,null,null,12.492097094883585,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,12.729457076303522,null,null,null,null,null,null,null,null,12.704226318192255,null,null,12.7110813839746,12.7110813839746,null,null,12.33288149239387,12.33288149239387,12.33288149239387,12.33288149239387,12.33288149239387,12.33288149239387,12.33288149239387,null,12.701957205426865,null,null,null,13.201361231716348,null,null,null,null,null,12.995440954491118,12.886104190942744,null,null,13.320655063448132,null,null,null,null,null,null,null,null,null,12.900311729746292,null,null,13.109604325785357,12.92505568736163,null,null,null,null,null,null,null,null,null,null,13.536225134779738,null,null,null,null,null,13.486960656608526,null,null,null,null,null,null,null,13.89281876105494,null,null,null,null,null,null,null,null,13.425998028157153,null,null,null,14.03005968277141,null,14.116440735451407,13.910720732768265,13.910720732768265,13.910720732768265,13.910720732768265,13.910720732768265,13.910720732768265,13.910720732768265,null,null,14.627281753791433,15.291327473759532],"yaxis":"y","type":"scattergl"},{"hovertemplate":"\u003cb\u003eOLS trendline\u003c\u002fb\u003e\u003cbr\u003eLog TotalChristianAdherents = 3.67163 * Log 2020 Income + -28.4449\u003cbr\u003eR\u003csup\u003e2\u003c\u002fsup\u003e=0.457605\u003cbr\u003e\u003cbr\u003eLog 2020 Income=%{x}\u003cbr\u003eLog TotalChristianAdherents=%{y} \u003cb\u003e(trend)\u003c\u002fb\u003e\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","line":{"color":"red"},"marker":{"color":"#636efa","symbol":"circle"},"mode":"lines","name":"","showlegend":false,"x":[10.340838849506614,10.35948733401834,10.382977295992266,10.407137492553023,10.48200920725477,10.531776160747578,10.533721557035943,10.536672391923391,10.566613573984062,10.568620986640875,10.578547134297418,10.581114921438036,10.586761149297775,10.59026448608823,10.595459042242352,10.599031857695795,10.616608914303491,10.617686579792686,10.6236417385826,10.624711855667964,10.658529136633662,10.6699084287665,10.68354610508537,10.68562955841758,10.695506743860696,10.696027476974109,10.696231168314535,10.705915056260707,10.7131947990075,10.716726213353894,10.71798916150825,10.735700781219071,10.735700781219071,10.750342457690289,10.751178192918026,10.777058657190121,10.78839081116865,10.798350336996663,10.80608495727828,10.81777628173961,10.817936589530913,10.821157333085402,10.8457773602789,10.8457773602789,10.846478636240239,10.849880628226726,10.857863738015615,10.872579441401411,10.880760489345077,10.884348055059583,10.894199064777272,10.89910689102049,10.937294617838122,10.94598793840407,10.963636174752109,10.973082892133744,11.000314915838985,11.000314915838985,11.007501890493232,11.01049781265528,11.014044880972106,11.02057806245001,11.023323027655763,11.0389459423249,11.051270885210688,11.051270885210688,11.089805421623343,11.093112922904789,11.10399435721889,11.11173122371271,11.118148039566904,11.12041606802228,11.12041606802228,11.135260331719744,11.18375450901049,11.232841123193209,11.354785170537204,11.418120157696316,11.506625662821701,11.66012921350686,11.811235856211189,11.811235856211189,11.862751005207715,11.862751005207715],"xaxis":"x","y":[9.522761685735325,9.591231944624816,9.677478297600459,9.76618550124995,10.041086428770654,10.223812064607245,10.230954832022107,10.241789193846884,10.35172201363514,10.359092481955159,10.395537582863568,10.404965536656853,10.425696373152562,10.438559315278972,10.457631782238153,10.470749824023684,10.535286200461535,10.53924298499247,10.561108100295385,10.56503716991125,10.689201574863525,10.730982078680043,10.781054524385596,10.788704185619508,10.824969515596557,10.826881452787234,10.827629331190103,10.863184945069307,10.889913437146419,10.902879469554662,10.90751654271942,10.972546984533054,10.972546984533054,11.026305743210209,11.029374250325098,11.12439763347328,11.166005063621164,11.202572716688728,11.230971348907943,11.273897518706079,11.274486108945979,11.286311474425624,11.376707004139853,11.376707004139853,11.379281827128587,11.39177266904705,11.421083661779178,11.475114219593834,11.505151967183345,11.518324166409549,11.554493388914949,11.57251309090448,11.712724138078876,11.744642759100628,11.809440480917296,11.844125293206986,11.944111096986923,11.944111096986923,11.970498979331957,11.981498884762303,11.994522392693952,12.018509791073846,12.028588276441518,12.085949774708666,12.131202354330206,12.131202354330206,12.272686756599043,12.284830663996743,12.324783220147197,12.35319009961733,12.376750246958345,12.38507759899656,12.38507759899656,12.439580182182354,12.617632659939595,12.797860344338616,13.245593267967124,13.478135647741759,13.803094753414399,14.366702367173062,14.921509431488772,14.921509431488772,15.11065378723012,15.11065378723012],"yaxis":"y","type":"scattergl"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Log of 2020 Income"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Log of Total Christian Adherents"}},"legend":{"tracegroupgap":0},"margin":{"t":60},"title":{"text":"Log of 2020 Income vs. Log of Total Christian Adherents"}},                        {"responsive": true}                    )              };                            </script>        </div>
</body>
</html>



```python
fig = px.scatter(merged_df_edu_cleaned, x=np.log(merged_df_edu_cleaned['GDP/Cap for 2010'] + 1), y='Educational index ',
                 color='chrstgenpct',
                 hover_data=['name'],
                 #size=1/ merged_df_edu_cleaned['pop'],
                 trendline='ols', trendline_color_override='red')

fig.update_layout(
    title='Log of GDP per Capita vs. Educational Index (2010)',
    xaxis_title='Log GDP per Capita',
    yaxis_title='Educational Index'
)
fig.update_xaxes(range=[5, 12])

fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
        <script charset="utf-8" src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>                <div id="1cd520fb-6057-4075-b74d-0622a9a0ffa3" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("1cd520fb-6057-4075-b74d-0622a9a0ffa3")) {                    Plotly.newPlot(                        "1cd520fb-6057-4075-b74d-0622a9a0ffa3",                        [{"customdata":[["USA"],["CAN"],["BHM"],["CUB"],["HAI"],["DOM"],["JAM"],["TRI"],["BAR"],["DMA"],["GRN"],["SLU"],["SVG"],["AAB"],["SKN"],["MEX"],["BLZ"],["GUA"],["HON"],["SAL"],["NIC"],["COS"],["PAN"],["COL"],["VEN"],["GUY"],["SUR"],["ECU"],["PER"],["BRA"],["BOL"],["PAR"],["CHL"],["ARG"],["URU"],["UKG"],["IRE"],["NTH"],["BEL"],["LUX"],["FRN"],["MNC"],["LIE"],["SWZ"],["SPN"],["AND"],["POR"],["GMY"],["POL"],["AUS"],["HUN"],["CZR"],["SLO"],["ITA"],["SNM"],["MLT"],["ALB"],["MNG"],["MAC"],["CRO"],["YUG"],["BOS"],["KOS"],["SLV"],["GRC"],["CYP"],["BUL"],["MLD"],["ROM"],["RUS"],["EST"],["LAT"],["LIT"],["UKR"],["BLR"],["ARM"],["GRG"],["AZE"],["FIN"],["SWD"],["NOR"],["DEN"],["ICE"],["CAP"],["STP"],["GNB"],["EQG"],["GAM"],["MLI"],["SEN"],["BEN"],["MAA"],["NIR"],["CDI"],["GUI"],["BFO"],["LBR"],["SIE"],["GHA"],["TOG"],["CAO"],["NIG"],["GAB"],["CEN"],["CHA"],["CON"],["DRC"],["UGA"],["KEN"],["TAZ"],["BUI"],["RWA"],["SOM"],["DJI"],["ETH"],["ERI"],["ANG"],["MZM"],["ZAM"],["ZIM"],["MAW"],["SAF"],["NAM"],["LES"],["BOT"],["SWA"],["MAG"],["COM"],["MAS"],["SEY"],["MOR"],["ALG"],["TUN"],["LIB"],["SUD"],["IRN"],["TUR"],["IRQ"],["EGY"],["SYR"],["LEB"],["JOR"],["ISR"],["SAU"],["YEM"],["KUW"],["BAH"],["QAT"],["UAE"],["OMA"],["AFG"],["TKM"],["TAJ"],["KYR"],["UZB"],["KZK"],["CHN"],["MON"],["TAW"],["PRK"],["ROK"],["JPN"],["IND"],["BHU"],["PAK"],["BNG"],["MYA"],["SRI"],["MAD"],["NEP"],["THI"],["CAM"],["LAO"],["DRV"],["MAL"],["SIN"],["BRU"],["PHI"],["INS"],["ETM"],["AUL"],["PNG"],["NEW"],["VAN"],["SOL"],["KIR"],["TUV"],["FIJ"],["TON"],["NAU"],["MSI"],["PAL"],["FSM"],["WSM"]],"hovertemplate":"x=%{x}\u003cbr\u003eEducational index =%{y}\u003cbr\u003ename=%{customdata[0]}\u003cbr\u003echrstgenpct=%{marker.color}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","marker":{"color":[0.7454,0.7661,0.966,0.6589,0.82,0.87,0.6881,0.5588,0.6434,0.92,0.87,0.9218,0.899,0.914,0.8979,0.9686,0.7365,0.95,0.89,0.861,0.9005,0.8822,0.9793,0.9701,0.95,0.5575,0.48,0.903,0.938,0.8823,0.9426,0.951,0.9128,0.8515,0.8183,0.6263,0.9299,0.5794,0.692,0.9106,0.7019,0.802,0.8678,0.8056,0.8056,0.907,0.8573,0.7078,0.9046,0.73,0.6736,0.2138,0.7548,0.7939,0.8631,0.9727,0.2144,0.7593,0.6374,0.9137,0.9122,0.52,0.0369,0.67,0.9438,0.7453,0.8227,0.8213,0.9751,0.7423,0.2837,0.7902,0.8296,0.852,0.5684,0.951,0.798,0.0241,0.794,0.7606,0.8401,0.8172,0.9155,0.9478,0.9441,0.1088,0.892,0.0435,0.03,0.0349,0.4,0.0026,0.039,0.375,0.08,0.2935,0.85,0.1905,0.7034,0.48,0.4952,0.42,0.7472,0.492,0.34,0.8063,0.9302,0.833,0.8063,0.4777,0.889,0.8945,0.0005,0.0139,0.6156,0.575,0.8912,0.4734,0.87,0.8188,0.7228,0.8094,0.87,0.9418,0.692,0.7843,0.5858,0.0013,0.3252,0.9365,0.01,0.008,0.0035,0.03,0.0715,0.0016,0.0042,0.0189,0.1212,0.0752,0.407,0.03,0.02,0.03,0.0,0.0,0.098,0.1445,0.0714,0.0334,0.0003,0.09,0.0202,0.1007,0.05,0.29,0.058,0.0194,0.0541,0.0166,0.2859,0.0196,0.0234,0.0122,0.017,0.002,0.0776,0.0726,0.0045,0.0142,0.006,0.0037,0.015,0.091,0.0826,0.1821,0.03,0.9174,0.106,0.98,0.6145,0.96,0.5407,0.85,0.9,0.96,0.9699,0.64,0.9421,0.9699,0.9341,0.8606,0.8651,0.9538],"coloraxis":"coloraxis","symbol":"circle"},"mode":"markers","name":"","orientation":"v","showlegend":false,"x":[10.792441297156916,10.76978239226268,0.0,8.571024456629198,0.0,8.614422988335823,8.484006781175223,0.0,0.0,8.879528115759323,0.0,0.0,0.0,0.0,0.0,9.192600351651647,8.594165731714519,0.0,0.0,0.0,7.311037466186321,0.0,9.002769719587798,8.76307748493126,9.524706850126247,8.43182537162787,8.987260242947832,8.422350232843476,8.526787942884786,9.328149353112442,7.561672203006716,0.0,9.454508792980567,9.248306878937314,0.0,0.0,0.0,0.0,10.69616206171446,11.616266865995831,0.0,0.0,11.859827601479275,8.303141801009161,0.0,10.783920845519637,0.0,0.0,9.433903849957591,10.861841572736775,9.489372990147483,0.0,0.0,10.492291616242218,0.0,9.989661317282824,8.317607385975874,7.886565560895402,10.833235075922067,0.0,0.0,0.0,0.0,8.012451487937502,10.193079630741071,10.345156884654784,0.0,0.0,0.0,9.275752595797039,9.593153831839416,0.0,0.0,8.03249485626628,8.705443613000469,8.053260530085385,0.0,8.673262104832178,10.747343134629526,0.0,11.386956361372793,0.0,0.0,0.0,6.9510842978853695,6.398361908960739,0.0,0.0,6.535717015388946,7.160539156570414,6.918190140733011,0.0,0.0,0.0,0.0,0.0,6.210640970560055,0.0,7.138838584375519,0.0,0.0,0.0,9.036058095169816,0.0,0.0,0.0,0.0,6.716277133638263,6.998180477286562,0.0,0.0,6.388755795651335,5.413820502430541,7.113810332557267,5.81841535458076,6.226482241277933,0.0,0.0,0.0,0.0,0.0,0.0,8.602713802654932,0.0,0.0,0.0,0.0,7.233501108967359,0.0,0.0,0.0,0.0,8.35279294264527,0.0,0.0,8.773318643539497,9.270842825763095,8.396476761990561,7.828345568168514,7.919109867174478,0.0,8.2727497063205,10.350337866689182,9.795899250611775,7.130949297261716,0.0,0.0,11.198520286488366,0.0,0.0,6.334165952028958,8.363547835094181,0.0,0.0,7.463563402068518,0.0,8.423206403127715,0.0,0.0,0.0,0.0,10.713732116746254,7.209069857837933,0.0,6.920273774796863,0.0,0.0,0.0,0.0,0.0,0.0,0.0,7.028941248785702,0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0,7.539155004564972,0.0,0.0,0.0,7.332957494264105,8.02098247447819,0.0,8.136550648134108,0.0,0.0,0.0,7.923352318967936,8.159201731122018],"xaxis":"x","y":[0.891,0.872,null,0.826,null,0.609,0.647,null,null,0.68,null,null,null,null,null,0.64,0.694,null,null,null,0.496,null,0.669,0.647,0.681,0.559,0.574,0.669,0.674,0.614,0.653,null,0.748,0.826,null,null,null,null,0.881,0.813,null,null,0.805,0.473,null,0.693,null,null,0.848,0.901,0.826,null,null,0.778,null,null,0.715,0.736,null,null,null,null,null,0.549,0.818,0.77,null,null,null,0.81,0.903,null,null,0.802,0.808,0.716,null,0.701,0.887,null,0.905,null,null,null,0.458,0.36,null,null,0.266,0.3,0.382,null,null,null,null,null,0.415,null,0.54,null,null,null,0.585,null,null,null,null,0.497,0.49,null,null,0.432,0.235,0.241,0.294,0.355,null,null,null,null,null,null,0.533,null,null,null,null,0.442,null,null,null,null,0.612,null,null,0.698,0.624,0.516,0.557,0.544,null,0.641,0.834,0.667,0.309,null,null,0.634,null,null,0.318,0.644,null,null,0.687,null,0.587,null,null,null,null,0.843,0.461,null,0.321,null,null,null,null,null,null,null,0.445,null,null,null,null,null,null,null,null,0.36,null,null,null,0.593,0.641,null,0.772,null,null,null,0.608,0.721],"yaxis":"y","type":"scatter"},{"hovertemplate":"\u003cb\u003eOLS trendline\u003c\u002fb\u003e\u003cbr\u003eEducational index  = 0.101121 * x + -0.238413\u003cbr\u003eR\u003csup\u003e2\u003c\u002fsup\u003e=0.675879\u003cbr\u003e\u003cbr\u003ex=%{x}\u003cbr\u003eEducational index =%{y} \u003cb\u003e(trend)\u003c\u002fb\u003e\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","line":{"color":"red"},"marker":{"symbol":"circle"},"mode":"lines","name":"","showlegend":false,"x":[5.413820502430541,5.81841535458076,6.210640970560055,6.226482241277933,6.334165952028958,6.388755795651335,6.398361908960739,6.535717015388946,6.716277133638263,6.918190140733011,6.920273774796863,6.9510842978853695,6.998180477286562,7.028941248785702,7.113810332557267,7.130949297261716,7.138838584375519,7.160539156570414,7.209069857837933,7.233501108967359,7.311037466186321,7.332957494264105,7.463563402068518,7.539155004564972,7.561672203006716,7.828345568168514,7.886565560895402,7.919109867174478,7.923352318967936,8.012451487937502,8.02098247447819,8.03249485626628,8.053260530085385,8.136550648134108,8.159201731122018,8.2727497063205,8.303141801009161,8.317607385975874,8.35279294264527,8.363547835094181,8.396476761990561,8.422350232843476,8.423206403127715,8.43182537162787,8.484006781175223,8.526787942884786,8.571024456629198,8.594165731714519,8.602713802654932,8.614422988335823,8.673262104832178,8.705443613000469,8.76307748493126,8.773318643539497,8.879528115759323,8.987260242947832,9.002769719587798,9.036058095169816,9.192600351651647,9.248306878937314,9.270842825763095,9.275752595797039,9.328149353112442,9.433903849957591,9.454508792980567,9.489372990147483,9.524706850126247,9.593153831839416,9.795899250611775,10.193079630741071,10.345156884654784,10.350337866689182,10.492291616242218,10.69616206171446,10.713732116746254,10.747343134629526,10.76978239226268,10.783920845519637,10.792441297156916,10.861841572736775,11.198520286488366,11.386956361372793,11.616266865995831,11.859827601479275],"xaxis":"x","y":[0.30904041440068175,0.34995364709354293,0.3896160842436419,0.3912179770793681,0.4021071139326262,0.4076273200423173,0.4085987044952162,0.4224882569721802,0.44074676444879535,0.4611645077766705,0.4613752079495671,0.4644908138298931,0.4692532494776662,0.4723638244033427,0.4809459122730291,0.4826790298531003,0.4834768062898306,0.485671200398059,0.4905786970287094,0.493049221448691,0.500889813112666,0.5031063989258919,0.5163134624084504,0.5239573975849054,0.5262343701527531,0.5532007771247381,0.559088069306418,0.5623789979194423,0.5628080009492425,0.5718178413202193,0.572680507356586,0.5738446565108376,0.5759445123060113,0.5843669328154004,0.5866574439875138,0.5981395839762201,0.6012128777549531,0.6026756592031999,0.6062336749806926,0.6073212256873083,0.6106510477087155,0.6132674115303299,0.6133539887417739,0.6142255516446266,0.6195022133216261,0.6238283079681403,0.6283015699751273,0.630641650100575,0.6315060437368302,0.6326900939931799,0.6386399928904697,0.6418942348193997,0.6477222575951802,0.6487578587723987,0.6594979184346069,0.6703919512299721,0.6719602925554812,0.6753264625621346,0.6911562481653601,0.6967893749865177,0.69906824341882,0.6995647266607585,0.7048631646240783,0.7155572165002885,0.7176408189585055,0.7211663383855551,0.7247393508140755,0.7316608113197449,0.7521627293534556,0.7923261996173718,0.8077044775257447,0.8082283861282005,0.8225829602317067,0.8431986426371425,0.8449753527117314,0.8483741487873466,0.8506432398648065,0.8520729412684325,0.8529345419997112,0.8599524009978117,0.8939978528498231,0.9130527887653535,0.9362410077570189,0.9608702312696769],"yaxis":"y","type":"scatter"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Log GDP per Capita"},"range":[5,12]},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Educational Index"}},"coloraxis":{"colorbar":{"title":{"text":"chrstgenpct"}},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"legend":{"tracegroupgap":0},"margin":{"t":60},"title":{"text":"Log of GDP per Capita vs. Educational Index (2010)"}},                        {"responsive": true}                    )             };                            </script>        </div>
</body>
</html>



```python
# prompt: get the r squared value

import statsmodels.formula.api as sm

# Assuming IncomeAndReligionByCounty is your DataFrame

# Fit a linear regression model
model = sm.ols('np.log(TotalChristianAdherents) ~ np.log(Q("2020 Income"))', data=IncomeAndReligionByCounty).fit()

# Print the R-squared value
print(f"R-squared: {model.rsquared}")
```

    R-squared: 0.45760539726848226


# Something interesting

Though still not the best R^2 value ever, I found the line fits to a good degree to my liking. The colors were hard to get a hang of, I kinda just had to pick a religion and roll with it.


```python
# prompt: make a column of the log of the chrstadherentspercapita

# Assuming IncomeAndReligionByCounty is your DataFrame
IncomeAndReligionByCounty['Log ChrstAdherentsPerCapita'] = np.log(IncomeAndReligionByCounty['ChrstAdherentsPerCapita'] + 1)
```


```python
# prompt: make a graph with income for 2020 on the x and the aherants per capita on the y

# Assuming IncomeAndReligionByCounty is your DataFrame

# Create the scatter plot
fig = px.scatter(IncomeAndReligionByCounty, x=np.log(IncomeAndReligionByCounty['2020 Income']+ 1), y='Log ChrstAdherentsPerCapita',
                 hover_data=['COUNAM', 'STATNAM'], trendline="ols", trendline_color_override='red')

fig.update_layout(
    title='Log of 2020 Income vs. Christian Adherents per Capita',
    xaxis_title='Log of 2020 Income',
    yaxis_title='Christian Adherents per Capita'
)


fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
        <script charset="utf-8" src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>                <div id="60caa76f-2837-49fe-acd9-084e1e3c8bca" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("60caa76f-2837-49fe-acd9-084e1e3c8bca")) {                    Plotly.newPlot(                        "60caa76f-2837-49fe-acd9-084e1e3c8bca",                        [{"customdata":[["Loving County","Texas"],["King County","Texas"],["Kenedy County","Texas"],["McPherson County","Nebraska"],["Blaine County","Nebraska"],["Arthur County","Nebraska"],["Petroleum County","Montana"],["McMullen County","Texas"],["Loup County","Nebraska"],["Grant County","Nebraska"],["Borden County","Texas"],["Harding County","New Mexico"],["Thomas County","Nebraska"],["Banner County","Nebraska"],["San Juan County","Colorado"],["San Juan County","Colorado"],["Slope County","North Dakota"],["Hooker County","Nebraska"],["Logan County","Nebraska"],["Esmeralda County","Nevada"],["Kent County","Texas"],["Terrell County","Texas"],["Treasure County","Montana"],["Keya Paha County","Nebraska"],["Wheeler County","Nebraska"],["Hinsdale County","Colorado"],["Clark County","Idaho"],["Golden Valley County","Montana"],["Roberts County","Texas"],["Hayes County","Nebraska"],["Mineral County","Colorado"],["Jones County","South Dakota"],["Daggett County","Utah"],["Wibaux County","Montana"],["Billings County","North Dakota"],["Motley County","Texas"],["Camas County","Idaho"],["Prairie County","Montana"],["Foard County","Texas"],["Glasscock County","Texas"],["Sioux County","Nebraska"],["Garfield County","Montana"],["Alpine County","California"],["Stonewall County","Texas"],["Rock County","Nebraska"],["Hyde County","South Dakota"],["Sheridan County","North Dakota"],["Greeley County","Kansas"],["Harding County","South Dakota"],["Issaquena County","Mississippi"],["Sterling County","Texas"],["Campbell County","South Dakota"],["Jackson County","Colorado"],["Cottle County","Texas"],["Carter County","Montana"],["Edwards County","Texas"],["Briscoe County","Texas"],["Piute County","Utah"],["Throckmorton County","Texas"],["Kiowa County","Colorado"],["Sully County","South Dakota"],["Wheeler County","Oregon"],["Wallace County","Kansas"],["Irion County","Texas"],["Taliaferro County","Georgia"],["Lane County","Kansas"],["Dundy County","Nebraska"],["Daniels County","Montana"],["Jerauld County","South Dakota"],["Comanche County","Kansas"],["Powder River County","Montana"],["De Baca County","New Mexico"],["Hodgeman County","Kansas"],["McCone County","Montana"],["Golden Valley County","North Dakota"],["Cheyenne County","Colorado"],["Oldham County","Texas"],["Dickens County","Texas"],["Steele County","North Dakota"],["Boyd County","Nebraska"],["Garfield County","Nebraska"],["Deuel County","Nebraska"],["Armstrong County","Texas"],["Eureka County","Nevada"],["Sherman County","Oregon"],["Haakon County","South Dakota"],["Garden County","Nebraska"],["Logan County","North Dakota"],["Oliver County","North Dakota"],["Gosper County","Nebraska"],["Mellette County","South Dakota"],["Meagher County","Montana"],["Buffalo County","South Dakota"],["Liberty County","Montana"],["Menard County","Texas"],["Worth County","Missouri"],["Clark County","Kansas"],["Gilliam County","Oregon"],["Jeff Davis County","Texas"],["Judith Basin County","Montana"],["Keweenaw County","Michigan"],["Wheatland County","Montana"],["Stanton County","Kansas"],["Faulk County","South Dakota"],["Wichita County","Kansas"],["Towner County","North Dakota"],["Greeley County","Nebraska"],["Culberson County","Texas"],["Robertson County","Kentucky"],["Divide County","North Dakota"],["Adams County","North Dakota"],["Burke County","North Dakota"],["Highland County","Virginia"],["Quitman County","Georgia"],["Renville County","North Dakota"],["Garfield County","Washington"],["Cimarron County","Oklahoma"],["Miner County","South Dakota"],["Grant County","North Dakota"],["Griggs County","North Dakota"],["Dolores County","Colorado"],["Sanborn County","South Dakota"],["Eddy County","North Dakota"],["Webster County","Georgia"],["Kidder County","North Dakota"],["Sedgwick County","Colorado"],["McPherson County","South Dakota"],["Ziebach County","South Dakota"],["Graham County","Kansas"],["Sheridan County","Kansas"],["Schleicher County","Texas"],["Kiowa County","Kansas"],["Niobrara County","Wyoming"],["Potter County","South Dakota"],["Elk County","Kansas"],["Wayne County","Utah"],["Harmon County","Oklahoma"],["Hettinger County","North Dakota"],["Rich County","Utah"],["Hamilton County","Kansas"],["Frontier County","Nebraska"],["McIntosh County","North Dakota"],["Pawnee County","Nebraska"],["Cochran County","Texas"],["Rawlins County","Kansas"],["Chase County","Kansas"],["Butte County","Idaho"],["Cheyenne County","Kansas"],["Hitchcock County","Nebraska"],["Collingsworth County","Texas"],["Ness County","Kansas"],["Morton County","Kansas"],["Gove County","Kansas"],["Aurora County","South Dakota"],["Real County","Texas"],["Logan County","Kansas"],["Decatur County","Kansas"],["Sherman County","Texas"],["Jackson County","South Dakota"],["Trego County","Kansas"],["Hall County","Texas"],["Douglas County","South Dakota"],["Perkins County","South Dakota"],["Clay County","Georgia"],["Perkins County","Nebraska"],["Baker County","Georgia"],["Glascock County","Georgia"],["Franklin County","Nebraska"],["Brown County","Nebraska"],["Edwards County","Kansas"],["Jewell County","Kansas"],["Lincoln County","Kansas"],["Rush County","Kansas"],["Sherman County","Nebraska"],["Stanley County","South Dakota"],["Bowman County","North Dakota"],["Nelson County","North Dakota"],["Fallon County","Montana"],["Lipscomb County","Texas"],["Harlan County","Nebraska"],["Crockett County","Texas"],["Shackelford County","Texas"],["Woodson County","Kansas"],["Kinney County","Texas"],["Hand County","South Dakota"],["Hudspeth County","Texas"],["Sierra County","California"],["Tyrrell County","North Carolina"],["Donley County","Texas"],["Harper County","Oklahoma"],["Coke County","Texas"],["Emmons County","North Dakota"],["Concho County","Texas"],["Upton County","Texas"],["Granite County","Montana"],["Knox County","Texas"],["Traverse County","Minnesota"],["Sutton County","Texas"],["Chautauqua County","Kansas"],["Nance County","Nebraska"],["Bennett County","South Dakota"],["Hemphill County","Texas"],["Reagan County","Texas"],["Webster County","Nebraska"],["Foster County","North Dakota"],["Kimball County","Nebraska"],["Roger Mills County","Oklahoma"],["Hanson County","South Dakota"],["Baylor County","Texas"],["Costilla County","Colorado"],["Osborne County","Kansas"],["Baca County","Colorado"],["Lewis County","Idaho"],["Mercer County","Missouri"],["Sheridan County","Montana"],["Hardeman County","Texas"],["Smith County","Kansas"],["Catron County","New Mexico"],["Hardin County","Illinois"],["Fisher County","Texas"],["Sweet Grass County","Montana"],["Echols County","Georgia"],["Adams County","Iowa"],["Cavalier County","North Dakota"],["Lyman County","South Dakota"],["Knox County","Missouri"],["Ellis County","Oklahoma"],["Pope County","Illinois"],["Lake of the Woods County","Minnesota"],["Lake of the Woods County","Minnesota"],["Haskell County","Kansas"],["Sharkey County","Mississippi"],["Clark County","South Dakota"],["Sargent County","North Dakota"],["Chase County","Nebraska"],["Sioux County","North Dakota"],["Corson County","South Dakota"],["Red Lake County","Minnesota"],["Columbia County","Washington"],["Mason County","Texas"],["Wells County","North Dakota"],["Kearny County","Kansas"],["Edmunds County","South Dakota"],["Pierce County","North Dakota"],["Gregory County","South Dakota"],["Schuyler County","Missouri"],["Owsley County","Kentucky"],["Meade County","Kansas"],["Valley County","Nebraska"],["Stafford County","Kansas"],["Union County","New Mexico"],["LaMoure County","North Dakota"],["Nuckolls County","Nebraska"],["Dunn County","North Dakota"],["Storey County","Nevada"],["Tensas Parish","Louisiana"],["Grant County","Oklahoma"],["Hidalgo County","New Mexico"],["Mora County","New Mexico"],["Kittson County","Minnesota"],["Bath County","Virginia"],["Phillips County","Montana"],["Holt County","Missouri"],["Barber County","Kansas"],["Menominee County","Wisconsin"],["Custer County","Idaho"],["Kimble County","Texas"],["Deuel County","South Dakota"],["Marshall County","South Dakota"],["Adams County","Idaho"],["Wahkiakum County","Washington"],["Calhoun County","Illinois"],["Guadalupe County","New Mexico"],["Mills County","Texas"],["Dewey County","Oklahoma"],["Lincoln County","Nevada"],["Hickman County","Kentucky"],["Phillips County","Colorado"],["Mineral County","Montana"],["Schley County","Georgia"],["Cameron County","Pennsylvania"],["Mineral County","Nevada"],["Morrill County","Nebraska"],["Florence County","Wisconsin"],["Oneida County","Idaho"],["Hyde County","North Carolina"],["Hot Springs County","Wyoming"],["Furnas County","Nebraska"],["Ringgold County","Iowa"],["Republic County","Kansas"],["Crane County","Texas"],["Putnam County","Missouri"],["Custer County","Colorado"],["Scotland County","Missouri"],["Musselshell County","Montana"],["Calhoun County","Arkansas"],["Washington County","Colorado"],["Carlisle County","Kentucky"],["Jim Hogg County","Texas"],["Jim Hogg County","Texas"],["Ouray County","Colorado"],["Craig County","Virginia"],["Rooks County","Kansas"],["Gallatin County","Illinois"],["Scott County","Illinois"],["Toole County","Montana"],["Phillips County","Kansas"],["Wheeler County","Texas"],["Dickey County","North Dakota"],["Pickett County","Tennessee"],["Thayer County","Nebraska"],["Beaver County","Oklahoma"],["Garfield County","Utah"],["Hamilton County","New York"],["Lincoln County","Idaho"],["Sheridan County","Nebraska"],["Crosby County","Texas"],["Scott County","Kansas"],["Big Stone County","Minnesota"],["Kingsbury County","South Dakota"],["Pulaski County","Illinois"],["Wirt County","West Virginia"],["Carter County","Missouri"],["Polk County","Nebraska"],["Warren County","Georgia"],["Delta County","Texas"],["Martin County","Texas"],["Dewey County","South Dakota"],["Alexander County","Illinois"],["Brule County","South Dakota"],["Stevens County","Kansas"],["Coal County","Oklahoma"],["Hansford County","Texas"],["Johnson County","Nebraska"],["Atchison County","Missouri"],["Stewart County","Georgia"],["Walworth County","South Dakota"],["Jefferson County","Oklahoma"],["Luce County","Michigan"],["McHenry County","North Dakota"],["Boone County","Nebraska"],["Hartley County","Texas"],["Morris County","Kansas"],["Stark County","Illinois"],["Floyd County","Texas"],["Mahnomen County","Minnesota"],["Haskell County","Texas"],["Day County","South Dakota"],["Cherry County","Nebraska"],["Norton County","Kansas"],["Harper County","Kansas"],["Greer County","Oklahoma"],["Cotton County","Oklahoma"],["Washington County","Kansas"],["Fillmore County","Nebraska"],["Calhoun County","Georgia"],["Lynn County","Texas"],["Cook County","Minnesota"],["Dixon County","Nebraska"],["Cameron Parish","Louisiana"],["Tripp County","South Dakota"],["Putnam County","Illinois"],["Lincoln County","Minnesota"],["Bent County","Colorado"],["Gray County","Kansas"],["Audubon County","Iowa"],["Lincoln County","Colorado"],["McCook County","South Dakota"],["Alfalfa County","Oklahoma"],["Ransom County","North Dakota"],["San Saba County","Texas"],["San Saba County","Texas"],["San Saba County","Texas"],["San Saba County","Texas"],["Talbot County","Georgia"],["Lander County","Nevada"],["Ottawa County","Kansas"],["Mitchell County","Kansas"],["Carson County","Texas"],["Gilpin County","Colorado"],["Ontonagon County","Michigan"],["Garza County","Texas"],["Sullivan County","Pennsylvania"],["Stanton County","Nebraska"],["Cumberland County","Kentucky"],["Chouteau County","Montana"],["Taylor County","Iowa"],["Pondera County","Montana"],["Essex County","Vermont"],["Crowley County","Colorado"],["Sherman County","Kansas"],["Ohio County","Indiana"],["Benson County","North Dakota"],["Sullivan County","Missouri"],["Miller County","Georgia"],["Greenwood County","Kansas"],["Grant County","Minnesota"],["Reynolds County","Missouri"],["Shelby County","Missouri"],["Clay County","Nebraska"],["Menifee County","Kentucky"],["Presidio County","Texas"],["Iron County","Wisconsin"],["Pendleton County","West Virginia"],["Gentry County","Missouri"],["Hamlin County","South Dakota"],["Van Buren County","Tennessee"],["Quitman County","Mississippi"],["Osceola County","Iowa"],["Teton County","Montana"],["Calhoun County","West Virginia"],["Brown County","Illinois"],["Edwards County","Illinois"],["Pawnee County","Kansas"],["Woodruff County","Arkansas"],["Bland County","Virginia"],["Antelope County","Nebraska"],["Lafayette County","Arkansas"],["Moody County","South Dakota"],["Spink County","South Dakota"],["Saguache County","Colorado"],["Bear Lake County","Idaho"],["Ellsworth County","Kansas"],["Bottineau County","North Dakota"],["Henderson County","Illinois"],["Treutlen County","Georgia"],["Randolph County","Georgia"],["Norman County","Minnesota"],["Moore County","Tennessee"],["Howard County","Nebraska"],["Dallas County","Arkansas"],["Wayne County","Iowa"],["Wilkin County","Minnesota"],["Fulton County","Kentucky"],["Rio Blanco County","Colorado"],["Rio Blanco County","Colorado"],["Surry County","Virginia"],["Wolfe County","Kentucky"],["Fremont County","Iowa"],["King and Queen County","Virginia"],["King and Queen County","Virginia"],["King and Queen County","Virginia"],["Clark County","Missouri"],["Pershing County","Nevada"],["Hancock County","Tennessee"],["Childress County","Texas"],["La Salle County","Texas"],["Kearney County","Nebraska"],["Russell County","Kansas"],["Lac qui Parle County","Minnesota"],["Burt County","Nebraska"],["Refugio County","Texas"],["Clinch County","Georgia"],["Tucker County","West Virginia"],["Thurston County","Nebraska"],["Charles City County","Virginia"],["Broadwater County","Montana"],["Monroe County","Arkansas"],["Huerfano County","Colorado"],["Weston County","Wyoming"],["Pembina County","North Dakota"],["Wabaunsee County","Kansas"],["Schuyler County","Illinois"],["Bailey County","Texas"],["Powell County","Montana"],["Tillman County","Oklahoma"],["Swisher County","Texas"],["Forest County","Pennsylvania"],["Fall River County","South Dakota"],["Bon Homme County","South Dakota"],["Ida County","Iowa"],["Lake County","Tennessee"],["Goliad County","Texas"],["Caribou County","Idaho"],["Shannon County","Missouri"],["Blaine County","Montana"],["Beaver County","Utah"],["Nemaha County","Nebraska"],["Brooks County","Texas"],["Pocahontas County","Iowa"],["Kit Carson County","Colorado"],["Union County","Indiana"],["Dallam County","Texas"],["Ferry County","Washington"],["Crook County","Wyoming"],["Van Buren County","Iowa"],["Newton County","Arkansas"],["Grant County","Oregon"],["Jefferson County","Nebraska"],["Jefferson County","Mississippi"],["Jefferson County","Mississippi"],["Grand Isle County","Vermont"],["Pierce County","Nebraska"],["Pepin County","Wisconsin"],["Rappahannock County","Virginia"],["Grant County","Kansas"],["Elliott County","Kentucky"],["Castro County","Texas"],["Wallowa County","Oregon"],["Lee County","Kentucky"],["Chariton County","Missouri"],["Gilmer County","West Virginia"],["Hutchinson County","South Dakota"],["Lake County","Colorado"],["Worth County","Iowa"],["East Carroll Parish","Louisiana"],["East Carroll Parish","Louisiana"],["East Carroll Parish","Louisiana"],["Conejos County","Colorado"],["Kingman County","Kansas"],["Wheeler County","Georgia"],["Harney County","Oregon"],["Adair County","Iowa"],["Marion County","Georgia"],["Doniphan County","Kansas"],["Nicholas County","Kentucky"],["Cleveland County","Arkansas"],["Grant County","South Dakota"],["Dade County","Missouri"],["Monroe County","Iowa"],["Valley County","Montana"],["Clay County","Tennessee"],["Boise County","Idaho"],["Red River Parish","Louisiana"],["McCulloch County","Texas"],["Decatur County","Iowa"],["Benton County","Mississippi"],["Pleasants County","West Virginia"],["Kane County","Utah"],["Merrick County","Nebraska"],["Franklin County","Mississippi"],["Coleman County","Texas"],["Washakie County","Wyoming"],["Lincoln County","Georgia"],["Yoakum County","Texas"],["Ballard County","Kentucky"],["Greene County","Alabama"],["Major County","Oklahoma"],["Humphreys County","Mississippi"],["Winkler County","Texas"],["Doddridge County","West Virginia"],["Taylor County","Georgia"],["Searcy County","Arkansas"],["Anderson County","Kansas"],["Pocahontas County","West Virginia"],["Richardson County","Nebraska"],["Power County","Idaho"],["San Augustine County","Texas"],["San Augustine County","Texas"],["San Augustine County","Texas"],["San Augustine County","Texas"],["Thomas County","Kansas"],["Liberty County","Florida"],["Lemhi County","Idaho"],["Hamilton County","Illinois"],["Traill County","North Dakota"],["Twiggs County","Georgia"],["Graham County","North Carolina"],["Allendale County","South Carolina"],["Schoolcraft County","Michigan"],["Clay County","West Virginia"],["San Miguel County","Colorado"],["San Miguel County","Colorado"],["Clay County","Kansas"],["Harrison County","Missouri"],["Baraga County","Michigan"],["Lake County","Oregon"],["Murray County","Minnesota"],["Franklin city","Virginia"],["Dawes County","Nebraska"],["Oscoda County","Michigan"],["Hamilton County","Texas"],["Lafayette County","Florida"],["Choctaw County","Mississippi"],["Hickory County","Missouri"],["Prairie County","Arkansas"],["Houston County","Tennessee"],["Atkinson County","Georgia"],["Nevada County","Arkansas"],["Tyler County","West Virginia"],["Custer County","South Dakota"],["Rosebud County","Montana"],["Keith County","Nebraska"],["Mercer County","North Dakota"],["Coffey County","Kansas"],["Perry County","Tennessee"],["Butler County","Nebraska"],["Webster County","West Virginia"],["Cedar County","Nebraska"],["Knox County","Nebraska"],["Bracken County","Kentucky"],["Daviess County","Missouri"],["Maries County","Missouri"],["Warren County","Indiana"],["Ritchie County","West Virginia"],["Johnson County","Wyoming"],["Jack County","Texas"],["Trimble County","Kentucky"],["Montgomery County","Arkansas"],["Carroll County","Missouri"],["Kiowa County","Oklahoma"],["Perry County","Alabama"],["Clearwater County","Minnesota"],["Mathews County","Virginia"],["Ozark County","Missouri"],["Archer County","Texas"],["Wilkinson County","Mississippi"],["Lee County","Arkansas"],["Platte County","Wyoming"],["Montgomery County","Georgia"],["Dimmit County","Texas"],["Madison County","Montana"],["Wilson County","Kansas"],["Woods County","Oklahoma"],["Lucas County","Iowa"],["Oregon County","Missouri"],["Monroe County","Missouri"],["Turner County","South Dakota"],["Jenkins County","Georgia"],["Lyon County","Kentucky"],["Gallatin County","Kentucky"],["Modoc County","California"],["Benton County","Indiana"],["Sublette County","Wyoming"],["Clearwater County","Idaho"],["Hancock County","Georgia"],["Blaine County","Oklahoma"],["Quay County","New Mexico"],["Monona County","Iowa"],["Wilcox County","Georgia"],["Greene County","Iowa"],["Caldwell County","Missouri"],["Alger County","Michigan"],["Wilkinson County","Georgia"],["Livingston County","Kentucky"],["Catahoula Parish","Louisiana"],["Richmond County","Virginia"],["Dawson County","Montana"],["Stillwater County","Montana"],["Phelps County","Nebraska"],["Kemper County","Mississippi"],["Crittenden County","Kentucky"],["Mitchell County","Texas"],["Palo Alto County","Iowa"],["Turner County","Georgia"],["Cuming County","Nebraska"],["Cloud County","Kansas"],["Marshall County","Minnesota"],["White Pine County","Nevada"],["Hancock County","Kentucky"],["Stephens County","Texas"],["Davis County","Iowa"],["Claiborne County","Mississippi"],["Seminole County","Georgia"],["McLean County","Kentucky"],["Montmorency County","Michigan"],["Pratt County","Kansas"],["Jones County","North Carolina"],["Forest County","Wisconsin"],["Terrell County","Georgia"],["Johnson County","Georgia"],["Somervell County","Texas"],["Clinton County","Kentucky"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["St. Clair County","Missouri"],["Jasper County","Illinois"],["Todd County","South Dakota"],["Nowata County","Oklahoma"],["Beaverhead County","Montana"],["Charles Mix County","South Dakota"],["Emmet County","Iowa"],["Clear Creek County","Colorado"],["Deer Lodge County","Montana"],["Pipestone County","Minnesota"],["Rice County","Kansas"],["Hamilton County","Nebraska"],["Latimer County","Oklahoma"],["Cheyenne County","Nebraska"],["Howard County","Iowa"],["Brown County","Kansas"],["McCormick County","South Carolina"],["Yellow Medicine County","Minnesota"],["Benewah County","Idaho"],["Iron County","Missouri"],["Brewster County","Texas"],["Greenlee County","Arizona"],["Chattahoochee County","Georgia"],["Wilkes County","Georgia"],["Linn County","Kansas"],["Humboldt County","Iowa"],["Caldwell Parish","Louisiana"],["Irwin County","Georgia"],["Grand County","Utah"],["Zavala County","Texas"],["Stevens County","Minnesota"],["Cumberland County","Virginia"],["Wayne County","Nebraska"],["Rock County","Minnesota"],["Marion County","Texas"],["Switzerland County","Indiana"],["Clarke County","Iowa"],["West Carroll Parish","Louisiana"],["West Carroll Parish","Louisiana"],["West Carroll Parish","Louisiana"],["McLean County","North Dakota"],["Tunica County","Mississippi"],["Grundy County","Missouri"],["Mountrail County","North Dakota"],["Martin County","Indiana"],["Sac County","Iowa"],["Montgomery County","Mississippi"],["Emery County","Utah"],["Duval County","Texas"],["Scott County","Arkansas"],["Swift County","Minnesota"],["Pulaski County","Georgia"],["Parmer County","Texas"],["Lanier County","Georgia"],["Sabine County","Texas"],["Runnels County","Texas"],["Webster County","Mississippi"],["Calhoun County","Iowa"],["Yuma County","Colorado"],["Jackson County","Minnesota"],["Carroll County","Mississippi"],["Ochiltree County","Texas"],["Madison Parish","Louisiana"],["Perry County","Arkansas"],["Franklin County","Iowa"],["Lewis County","Missouri"],["Keokuk County","Iowa"],["Marshall County","Kansas"],["Holt County","Nebraska"],["Love County","Oklahoma"],["Howard County","Missouri"],["Alcona County","Michigan"],["Pike County","Arkansas"],["Chicot County","Arkansas"],["Clay County","Texas"],["Butte County","South Dakota"],["Johnston County","Oklahoma"],["Nemaha County","Kansas"],["Roberts County","South Dakota"],["Noxubee County","Mississippi"],["Metcalfe County","Kentucky"],["Lowndes County","Alabama"],["Montgomery County","Iowa"],["Ralls County","Missouri"],["Camden County","North Carolina"],["Bullock County","Alabama"],["Franklin County","Texas"],["Coosa County","Alabama"],["Cumberland County","Illinois"],["Carbon County","Montana"],["Gates County","North Carolina"],["Washington County","Idaho"],["Leslie County","Kentucky"],["Crawford County","Indiana"],["Bradley County","Arkansas"],["Custer County","Nebraska"],["Walsh County","North Dakota"],["Mitchell County","Iowa"],["Bollinger County","Missouri"],["Colfax County","Nebraska"],["Essex County","Virginia"],["Wilcox County","Alabama"],["Guthrie County","Iowa"],["Middlesex County","Virginia"],["Winnebago County","Iowa"],["Ripley County","Missouri"],["Red Willow County","Nebraska"],["Evans County","Georgia"],["Roosevelt County","Montana"],["Hancock County","Iowa"],["Carroll County","Kentucky"],["Pushmataha County","Oklahoma"],["Sussex County","Virginia"],["Mackinac County","Michigan"],["Louisa County","Iowa"],["Box Butte County","Nebraska"],["Barnes County","North Dakota"],["Early County","Georgia"],["Lincoln County","Washington"],["Alleghany County","North Carolina"],["Lake County","Minnesota"],["Lake County","Minnesota"],["Lancaster County","Virginia"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["St. Helena Parish","Louisiana"],["Noble County","Oklahoma"],["Washita County","Oklahoma"],["Wayne County","Missouri"],["McIntosh County","Georgia"],["Grant County","West Virginia"],["Candler County","Georgia"],["Washington County","North Carolina"],["DeKalb County","Missouri"],["Lake County","South Dakota"],["Clay County","North Carolina"],["Green County","Kentucky"],["Bacon County","Georgia"],["Dooly County","Georgia"],["Watonwan County","Minnesota"],["Owen County","Kentucky"],["Martin County","Kentucky"],["Pope County","Minnesota"],["Okfuskee County","Oklahoma"],["Jefferson Davis County","Mississippi"],["Jefferson Davis County","Mississippi"],["Montgomery County","Missouri"],["Live Oak County","Texas"],["Monroe County","Kentucky"],["Wabash County","Illinois"],["Blanco County","Texas"],["Desha County","Arkansas"],["Heard County","Georgia"],["Decatur County","Tennessee"],["Fergus County","Montana"],["Richland County","Montana"],["Perry County","Mississippi"],["Cottonwood County","Minnesota"],["Big Horn County","Wyoming"],["Charlotte County","Virginia"],["Rio Grande County","Colorado"],["Rio Grande County","Colorado"],["Haskell County","Oklahoma"],["Sierra County","New Mexico"],["Douglas County","Missouri"],["Red River County","Texas"],["Conecuh County","Alabama"],["Ramsey County","North Dakota"],["Trousdale County","Tennessee"],["Jackson County","Tennessee"],["Teton County","Idaho"],["Iron County","Michigan"],["Magoffin County","Kentucky"],["Barton County","Missouri"],["Ward County","Texas"],["Cherokee County","Iowa"],["Marshall County","Illinois"],["Valley County","Idaho"],["Shelby County","Iowa"],["Juab County","Utah"],["Marion County","Kansas"],["Terry County","Texas"],["Northumberland County","Virginia"],["Custer County","Montana"],["Linn County","Missouri"],["Owyhee County","Idaho"],["Lyon County","Iowa"],["Lunenburg County","Virginia"],["Summers County","West Virginia"],["Morris County","Texas"],["Greene County","Illinois"],["Prowers County","Colorado"],["Chickasaw County","Iowa"],["Lawrence County","Mississippi"],["Little River County","Arkansas"],["Washington County","Kentucky"],["Skamania County","Washington"],["Boundary County","Idaho"],["Koochiching County","Minnesota"],["Fulton County","Arkansas"],["Macon County","Georgia"],["Jefferson County","Montana"],["Lake County","Michigan"],["Blackford County","Indiana"],["Glades County","Florida"],["Edmonson County","Kentucky"],["Crawford County","Georgia"],["Union County","Iowa"],["Rains County","Texas"],["Morrow County","Oregon"],["Rolette County","North Dakota"],["Newton County","Texas"],["Todd County","Kentucky"],["Pike County","Indiana"],["Pamlico County","North Carolina"],["Northampton County","Virginia"],["Morgan County","Utah"],["Menard County","Illinois"],["Appanoose County","Iowa"],["Grundy County","Iowa"],["Sumter County","Alabama"],["Stone County","Arkansas"],["Butler County","Kentucky"],["Monroe County","West Virginia"],["Colfax County","New Mexico"],["Sanders County","Montana"],["Braxton County","West Virginia"],["Franklin County","Florida"],["Dawson County","Texas"],["Camp County","Texas"],["Telfair County","Georgia"],["Yalobusha County","Mississippi"],["Towns County","Georgia"],["Goshen County","Wyoming"],["Pulaski County","Indiana"],["Charlton County","Georgia"],["Allen County","Kansas"],["Mississippi County","Missouri"],["Lewis County","Tennessee"],["Bleckley County","Georgia"],["Chippewa County","Minnesota"],["Madison County","Missouri"],["Caldwell County","Kentucky"],["Choctaw County","Alabama"],["Tallahatchie County","Mississippi"],["Amite County","Mississippi"],["Bath County","Kentucky"],["Meigs County","Tennessee"],["Howard County","Arkansas"],["Vinton County","Ohio"],["Wilbarger County","Texas"],["Lincoln County","Arkansas"],["Wright County","Iowa"],["Jackson County","Kentucky"],["Millard County","Utah"],["Bienville Parish","Louisiana"],["Presque Isle County","Michigan"],["Crawford County","Michigan"],["Perquimans County","North Carolina"],["Webster County","Kentucky"],["Cass County","Illinois"],["Lamb County","Texas"],["Lewis County","Kentucky"],["Mason County","Illinois"],["Big Horn County","Montana"],["Cass County","Iowa"],["Powell County","Kentucky"],["Shoshone County","Idaho"],["Crenshaw County","Alabama"],["Mono County","California"],["Jackson County","Kansas"],["Amelia County","Virginia"],["Calhoun County","Mississippi"],["Osage County","Missouri"],["Clay County","Illinois"],["Moffat County","Colorado"],["Johnson County","Illinois"],["Bamberg County","South Carolina"],["Buffalo County","Wisconsin"],["Archuleta County","Colorado"],["Hughes County","Oklahoma"],["Monroe County","Ohio"],["Fremont County","Idaho"],["Pend Oreille County","Washington"],["Madison County","Texas"],["Grundy County","Tennessee"],["Greene County","Mississippi"],["Ford County","Illinois"],["Izard County","Arkansas"],["Comanche County","Texas"],["Trinity County","Texas"],["Calhoun County","Florida"],["Stewart County","Tennessee"],["Union County","Kentucky"],["Oglala Lakota County","South Dakota"],["Chowan County","North Carolina"],["Callahan County","Texas"],["Breathitt County","Kentucky"],["Morgan County","Kentucky"],["Converse County","Wyoming"],["Winn Parish","Louisiana"],["Washington County","Illinois"],["Glacier County","Montana"],["Morgan County","Ohio"],["Newton County","Indiana"],["Madison County","Virginia"],["White County","Illinois"],["Walthall County","Mississippi"],["Zapata County","Texas"],["Murray County","Oklahoma"],["Crockett County","Tennessee"],["Faribault County","Minnesota"],["Lamar County","Alabama"],["Pennington County","Minnesota"],["Hamilton County","Florida"],["Roane County","West Virginia"],["Price County","Wisconsin"],["Allamakee County","Iowa"],["Trigg County","Kentucky"],["Wadena County","Minnesota"],["Screven County","Georgia"],["Craig County","Oklahoma"],["Noble County","Ohio"],["Swain County","North Carolina"],["Calhoun County","South Carolina"],["Dickenson County","Virginia"],["York County","Nebraska"],["Atoka County","Oklahoma"],["Estill County","Kentucky"],["Massac County","Illinois"],["Claiborne Parish","Louisiana"],["O'Brien County","Iowa"],["Cedar County","Missouri"],["Rusk County","Wisconsin"],["Gulf County","Florida"],["Franklin County","Idaho"],["Choctaw County","Oklahoma"],["Smith County","Mississippi"],["Clay County","Alabama"],["Knott County","Kentucky"],["Nantucket County","Massachusetts"],["Saline County","Nebraska"],["Hardy County","West Virginia"],["Butler County","Iowa"],["Bourbon County","Kansas"],["Gogebic County","Michigan"],["Dent County","Missouri"],["Wetzel County","West Virginia"],["Harrison County","Ohio"],["Mills County","Iowa"],["Cannon County","Tennessee"],["Jefferson County","Florida"],["San Juan County","Utah"],["Moultrie County","Illinois"],["Carbon County","Wyoming"],["Clay County","Arkansas"],["Las Animas County","Colorado"],["Fulton County","Pennsylvania"],["Livingston County","Missouri"],["Harrison County","Iowa"],["Jasper County","Georgia"],["Pendleton County","Kentucky"],["McKenzie County","North Dakota"],["Karnes County","Texas"],["Renville County","Minnesota"],["Nolan County","Texas"],["Pike County","Illinois"],["Reeves County","Texas"],["Nelson County","Virginia"],["Jeff Davis County","Georgia"],["Clarke County","Virginia"],["Hale County","Alabama"],["LaSalle Parish","Louisiana"],["Gasconade County","Missouri"],["Oglethorpe County","Georgia"],["Kossuth County","Iowa"],["Sibley County","Minnesota"],["Larue County","Kentucky"],["Mitchell County","North Carolina"],["Bledsoe County","Tennessee"],["Clay County","South Dakota"],["Jackson County","Texas"],["Arenac County","Michigan"],["Jackson Parish","Louisiana"],["Hamilton County","Iowa"],["Torrance County","New Mexico"],["Missaukee County","Michigan"],["Cleburne County","Alabama"],["Fleming County","Kentucky"],["Kingfisher County","Oklahoma"],["Pecos County","Texas"],["Macon County","Missouri"],["Page County","Iowa"],["Lawrence County","Illinois"],["West Feliciana Parish","Louisiana"],["West Feliciana Parish","Louisiana"],["West Feliciana Parish","Louisiana"],["Marshall County","Oklahoma"],["Roseau County","Minnesota"],["Grayson County","Virginia"],["Tipton County","Indiana"],["Washington County","Alabama"],["Redwood County","Minnesota"],["Vermillion County","Indiana"],["Clark County","Illinois"],["Barbour County","West Virginia"],["Moniteau County","Missouri"],["Brown County","Indiana"],["Floyd County","Virginia"],["De Witt County","Illinois"],["Pawnee County","Oklahoma"],["Marquette County","Wisconsin"],["Gooding County","Idaho"],["Clarke County","Mississippi"],["Floyd County","Iowa"],["Nottoway County","Virginia"],["Pemiscot County","Missouri"],["Jefferson County","Iowa"],["Henry County","Kentucky"],["Aitkin County","Minnesota"],["Mercer County","Illinois"],["Carroll County","Illinois"],["Jefferson County","Georgia"],["Grand County","Colorado"],["Leon County","Texas"],["Osage County","Kansas"],["Van Buren County","Arkansas"],["Richland County","Illinois"],["Sequatchie County","Tennessee"],["Sevier County","Arkansas"],["Brunswick County","Virginia"],["Benton County","Tennessee"],["Neosho County","Kansas"],["Otoe County","Nebraska"],["Casey County","Kentucky"],["Ashland County","Wisconsin"],["Kanabec County","Minnesota"],["Rockcastle County","Kentucky"],["Bates County","Missouri"],["Trinity County","California"],["Crawford County","Wisconsin"],["Appomattox County","Virginia"],["Union County","Florida"],["Parke County","Indiana"],["Long County","Georgia"],["Wayne County","Illinois"],["Lawrence County","Arkansas"],["Bayfield County","Wisconsin"],["Wayne County","Tennessee"],["Dade County","Georgia"],["Lawrence County","Kentucky"],["Brooks County","Georgia"],["Hill County","Montana"],["Fayette County","Alabama"],["Atchison County","Kansas"],["Jasper County","Mississippi"],["Alamosa County","Colorado"],["Clay County","Iowa"],["Potter County","Pennsylvania"],["New Madrid County","Missouri"],["Fountain County","Indiana"],["Madison County","Arkansas"],["Crawford County","Iowa"],["Burnett County","Wisconsin"],["Richland County","North Dakota"],["Lee County","South Carolina"],["Madison County","Iowa"],["La Paz County","Arizona"],["Phillips County","Arkansas"],["Socorro County","New Mexico"],["Lafayette County","Wisconsin"],["Washburn County","Wisconsin"],["Baker County","Oregon"],["Piatt County","Illinois"],["Taylor County","West Virginia"],["Bond County","Illinois"],["Rush County","Indiana"],["Jackson County","Arkansas"],["Robertson County","Texas"],["Dixie County","Florida"],["Giles County","Virginia"],["Piscataquis County","Maine"],["Union County","South Dakota"],["Buckingham County","Virginia"],["Marion County","Arkansas"],["Cross County","Arkansas"],["Warren County","Illinois"],["Edgar County","Illinois"],["Hardin County","Iowa"],["Rabun County","Georgia"],["McCreary County","Kentucky"],["Gunnison County","Colorado"],["Scurry County","Texas"],["Garrard County","Kentucky"],["Falls County","Texas"],["Holmes County","Mississippi"],["Lewis County","West Virginia"],["Clayton County","Iowa"],["Morgan County","West Virginia"],["Dallas County","Missouri"],["Franklin County","Arkansas"],["Cooper County","Missouri"],["Chickasaw County","Mississippi"],["Mason County","Kentucky"],["Mariposa County","California"],["Tama County","Iowa"],["Henry County","Alabama"],["Park County","Montana"],["Ben Hill County","Georgia"],["Cook County","Georgia"],["Union County","Illinois"],["Sharp County","Arkansas"],["Humboldt County","Nevada"],["Richland County","Wisconsin"],["Chester County","Tennessee"],["Drew County","Arkansas"],["Pitkin County","Colorado"],["Park County","Colorado"],["Northampton County","North Carolina"],["Lee County","Texas"],["Delaware County","Iowa"],["Polk County","Tennessee"],["Pike County","Missouri"],["Patrick County","Virginia"],["Seward County","Nebraska"],["Hancock County","Illinois"],["Burleson County","Texas"],["Dickinson County","Iowa"],["Winston County","Mississippi"],["Eastland County","Texas"],["Hughes County","South Dakota"],["San Juan County","Washington"],["Avery County","North Carolina"],["King William County","Virginia"],["King William County","Virginia"],["King William County","Virginia"],["Gilchrist County","Florida"],["Haywood County","Tennessee"],["Young County","Texas"],["Attala County","Mississippi"],["Schuyler County","New York"],["Unicoi County","Tennessee"],["Bertie County","North Carolina"],["Kalkaska County","Michigan"],["Johnson County","Tennessee"],["Grant County","Arkansas"],["Madison County","Florida"],["Benzie County","Michigan"],["Russell County","Kentucky"],["Brantley County","Georgia"],["Banks County","Georgia"],["Sawyer County","Wisconsin"],["Andrew County","Missouri"],["Montour County","Pennsylvania"],["Berrien County","Georgia"],["Wright County","Missouri"],["Bosque County","Texas"],["Stone County","Mississippi"],["Covington County","Mississippi"],["Jefferson County","Kansas"],["Frio County","Texas"],["Dickinson County","Kansas"],["Appling County","Georgia"],["Yancey County","North Carolina"],["Westmoreland County","Virginia"],["Ste. Genevieve County","Missouri"],["Fentress County","Tennessee"],["Lamar County","Georgia"],["Cedar County","Iowa"],["Hampton County","South Carolina"],["Randolph County","Arkansas"],["Deaf Smith County","Texas"],["Andrews County","Texas"],["Clay County","Mississippi"],["Warren County","North Carolina"],["Poweshiek County","Iowa"],["Crawford County","Illinois"],["Concordia Parish","Louisiana"],["Otero County","Colorado"],["Harrison County","Kentucky"],["Paulding County","Ohio"],["Houston County","Minnesota"],["Tishomingo County","Mississippi"],["Saluda County","South Carolina"],["Pike County","Georgia"],["Adair County","Kentucky"],["Greene County","Georgia"],["McIntosh County","Oklahoma"],["Perry County","Missouri"],["Waseca County","Minnesota"],["Humphreys County","Tennessee"],["Inyo County","California"],["Green Lake County","Wisconsin"],["Green Lake County","Wisconsin"],["Butler County","Alabama"],["Ashley County","Arkansas"],["McDowell County","West Virginia"],["Pickens County","Alabama"],["Gem County","Idaho"],["Beadle County","South Dakota"],["Perry County","Indiana"],["Roosevelt County","New Mexico"],["Kent County","Maryland"],["Polk County","Arkansas"],["Hart County","Kentucky"],["Marengo County","Alabama"],["Polk County","North Carolina"],["Cherokee County","Kansas"],["Benton County","Missouri"],["Los Alamos County","New Mexico"],["Freestone County","Texas"],["Chaffee County","Colorado"],["Jackson County","Iowa"],["Spencer County","Kentucky"],["Langlade County","Wisconsin"],["Adair County","Oklahoma"],["Fayette County","Iowa"],["Macon County","Alabama"],["East Feliciana Parish","Louisiana"],["East Feliciana Parish","Louisiana"],["East Feliciana Parish","Louisiana"],["Wayne County","Kentucky"],["Marion County","Kentucky"],["Lincoln County","Wyoming"],["Simpson County","Kentucky"],["Duchesne County","Utah"],["Elbert County","Georgia"],["Holmes County","Florida"],["Gonzales County","Texas"],["Jones County","Texas"],["Lincoln County","Montana"],["Vernon County","Missouri"],["Pierce County","Georgia"],["Douglas County","Illinois"],["Monroe County","Alabama"],["Franklin Parish","Louisiana"],["Wayne County","Mississippi"],["Plumas County","California"],["Tyler County","Texas"],["Union County","Tennessee"],["Spencer County","Indiana"],["DeWitt County","Texas"],["Orange County","Indiana"],["Smith County","Tennessee"],["Taylor County","Wisconsin"],["Dodge County","Georgia"],["Davison County","South Dakota"],["Montague County","Texas"],["Washington County","Georgia"],["Martin County","Minnesota"],["Richland Parish","Louisiana"],["Hempstead County","Arkansas"],["Winneshiek County","Iowa"],["DeKalb County","Tennessee"],["Morgan County","Georgia"],["Calhoun County","Texas"],["Crisp County","Georgia"],["Willacy County","Texas"],["Labette County","Kansas"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["St. James Parish","Louisiana"],["Bourbon County","Kentucky"],["Yell County","Arkansas"],["Lincoln County","New Mexico"],["Carroll County","Indiana"],["Lavaca County","Texas"],["Clay County","Kentucky"],["Buchanan County","Virginia"],["Carbon County","Utah"],["Breckinridge County","Kentucky"],["Uinta County","Wyoming"],["Greene County","North Carolina"],["Lincoln County","West Virginia"],["Woodward County","Oklahoma"],["Jay County","Indiana"],["Fulton County","Indiana"],["Henry County","Iowa"],["Greene County","Virginia"],["Colorado County","Texas"],["Kewaunee County","Wisconsin"],["Buchanan County","Iowa"],["Allen County","Kentucky"],["Barnwell County","South Carolina"],["Dukes County","Massachusetts"],["Meriwether County","Georgia"],["Adams County","Washington"],["Hutchinson County","Texas"],["Jones County","Iowa"],["Adams County","Wisconsin"],["Conway County","Arkansas"],["Pointe Coupee Parish","Louisiana"],["Carroll County","Iowa"],["Ogemaw County","Michigan"],["Worth County","Georgia"],["Sullivan County","Indiana"],["Buena Vista County","Iowa"],["Bandera County","Texas"],["Washington County","Nebraska"],["Dodge County","Minnesota"],["Perry County","Illinois"],["Fairfield County","South Carolina"],["Shelby County","Illinois"],["Morgan County","Missouri"],["Morgan County","Tennessee"],["Assumption Parish","Louisiana"],["Union Parish","Louisiana"],["Logan County","Arkansas"],["Jackson County","Wisconsin"],["Clinton County","Missouri"],["Madison County","North Carolina"],["Gray County","Texas"],["Fillmore County","Minnesota"],["Nodaway County","Missouri"],["Llano County","Texas"],["Leake County","Mississippi"],["Newton County","Mississippi"],["Owen County","Indiana"],["Hubbard County","Minnesota"],["Moore County","Texas"],["Wyoming County","West Virginia"],["Texas County","Oklahoma"],["Wabasha County","Minnesota"],["Coahoma County","Mississippi"],["Clark County","Arkansas"],["Fayette County","Illinois"],["Jersey County","Illinois"],["Sevier County","Utah"],["Logan County","Colorado"],["Hockley County","Texas"],["Letcher County","Kentucky"],["Hertford County","North Carolina"],["Scott County","Virginia"],["Dakota County","Nebraska"],["Stutsman County","North Dakota"],["Gaines County","Texas"],["Minidoka County","Idaho"],["Lampasas County","Texas"],["Grenada County","Mississippi"],["McDuffie County","Georgia"],["Gage County","Nebraska"],["Mitchell County","Georgia"],["Taylor County","Florida"],["Boone County","West Virginia"],["Tippah County","Mississippi"],["Colusa County","California"],["Prince Edward County","Virginia"],["Scott County","Tennessee"],["Wyandot County","Ohio"],["Henry County","Missouri"],["Seward County","Kansas"],["Randolph County","Alabama"],["Martin County","North Carolina"],["Jo Daviess County","Illinois"],["Putnam County","Georgia"],["Anson County","North Carolina"],["Houston County","Texas"],["Limestone County","Texas"],["Sabine Parish","Louisiana"],["Grant Parish","Louisiana"],["Lee County","Virginia"],["Mahaska County","Iowa"],["Meigs County","Ohio"],["Saunders County","Nebraska"],["Asotin County","Washington"],["Nobles County","Minnesota"],["Bibb County","Alabama"],["Leelanau County","Michigan"],["Sumner County","Kansas"],["Beckham County","Oklahoma"],["Panola County","Texas"],["Overton County","Tennessee"],["Brooke County","West Virginia"],["Washington County","Iowa"],["Mercer County","Kentucky"],["Ouachita County","Arkansas"],["Johnson County","Kentucky"],["Klickitat County","Washington"],["Caswell County","North Carolina"],["Allen Parish","Louisiana"],["Emanuel County","Georgia"],["Franklin County","Indiana"],["Columbia County","Arkansas"],["Tattnall County","Georgia"],["Osceola County","Michigan"],["New Kent County","Virginia"],["Poinsett County","Arkansas"],["Vilas County","Wisconsin"],["Crawford County","Missouri"],["Clarke County","Alabama"],["St. Francis County","Arkansas"],["Hampshire County","West Virginia"],["Ray County","Missouri"],["McDonald County","Missouri"],["Yankton County","South Dakota"],["Teton County","Wyoming"],["Saline County","Missouri"],["Pacific County","Washington"],["Starke County","Indiana"],["Fayette County","Indiana"],["Meeker County","Minnesota"],["Franklin County","Georgia"],["Antrim County","Michigan"],["Curry County","Oregon"],["Roscommon County","Michigan"],["Menominee County","Michigan"],["Juniata County","Pennsylvania"],["Washington County","Missouri"],["Plaquemines Parish","Louisiana"],["Grainger County","Tennessee"],["Winston County","Alabama"],["Seminole County","Oklahoma"],["Mingo County","West Virginia"],["Page County","Virginia"],["Iowa County","Wisconsin"],["Saline County","Illinois"],["Ohio County","Kentucky"],["Upshur County","West Virginia"],["Aransas County","Texas"],["Anderson County","Kentucky"],["Itawamba County","Mississippi"],["Hood River County","Oregon"],["Shelby County","Texas"],["Bell County","Kentucky"],["Dawson County","Nebraska"],["Jerome County","Idaho"],["Blaine County","Idaho"],["Lincoln County","Kentucky"],["Abbeville County","South Carolina"],["George County","Mississippi"],["Scott County","Indiana"],["Fayette County","Texas"],["Marion County","Mississippi"],["Texas County","Missouri"],["Randolph County","Indiana"],["Jefferson County","Oregon"],["Waushara County","Wisconsin"],["Uvalde County","Texas"],["Burke County","Georgia"],["Nicholas County","West Virginia"],["Somerset County","Maryland"],["Union County","Georgia"],["Cassia County","Idaho"],["Rowan County","Kentucky"],["White County","Indiana"],["Teller County","Colorado"],["Cleburne County","Arkansas"],["Randolph County","Missouri"],["Miller County","Missouri"],["Goochland County","Virginia"],["Crook County","Oregon"],["Milam County","Texas"],["Yates County","New York"],["Jackson County","Oklahoma"],["Routt County","Colorado"],["Hickman County","Tennessee"],["Grant County","Kentucky"],["Audrain County","Missouri"],["Chattooga County","Georgia"],["Cherokee County","Alabama"],["Bremer County","Iowa"],["Prentiss County","Mississippi"],["Manistee County","Michigan"],["Otsego County","Michigan"],["Lauderdale County","Tennessee"],["Macon County","Tennessee"],["Posey County","Indiana"],["Barbour County","Alabama"],["Iosco County","Michigan"],["Todd County","Minnesota"],["Lyon County","Minnesota"],["Adair County","Missouri"],["Washington County","Florida"],["Fannin County","Georgia"],["Hardee County","Florida"],["Pottawatomie County","Kansas"],["Payette County","Idaho"],["Gladwin County","Michigan"],["Luna County","New Mexico"],["Butts County","Georgia"],["Mason County","West Virginia"],["Hardeman County","Tennessee"],["Barton County","Kansas"],["Churchill County","Nevada"],["Benton County","Iowa"],["Cheboygan County","Michigan"],["Morehouse Parish","Louisiana"],["Garvin County","Oklahoma"],["Edgefield County","South Carolina"],["Plymouth County","Iowa"],["Johnson County","Arkansas"],["Montgomery County","North Carolina"],["Lawrence County","South Dakota"],["Russell County","Virginia"],["Hart County","Georgia"],["Montezuma County","Colorado"],["McNairy County","Tennessee"],["Brown County","Minnesota"],["Lamoille County","Vermont"],["Dickinson County","Michigan"],["Simpson County","Mississippi"],["Sunflower County","Mississippi"],["Franklin County","Kansas"],["Taylor County","Kentucky"],["Charlevoix County","Michigan"],["Elbert County","Colorado"],["Wyoming County","Pennsylvania"],["Union County","Oregon"],["Grady County","Georgia"],["Grayson County","Kentucky"],["Mille Lacs County","Minnesota"],["Clay County","Indiana"],["Decatur County","Indiana"],["Ashe County","North Carolina"],["Lewis County","New York"],["Cass County","Nebraska"],["Carter County","Kentucky"],["Geneva County","Alabama"],["Oceana County","Michigan"],["Marlboro County","South Carolina"],["Wasco County","Oregon"],["Boone County","Iowa"],["Juneau County","Wisconsin"],["Carroll County","Ohio"],["King George County","Virginia"],["King George County","Virginia"],["King George County","Virginia"],["Gillespie County","Texas"],["Yazoo County","Mississippi"],["Stephens County","Georgia"],["Dawson County","Georgia"],["De Soto Parish","Louisiana"],["Harlan County","Kentucky"],["Hardin County","Tennessee"],["Woodford County","Kentucky"],["Mineral County","West Virginia"],["Caddo County","Oklahoma"],["Toombs County","Georgia"],["Iroquois County","Illinois"],["Pike County","Ohio"],["Cibola County","New Mexico"],["West Baton Rouge Parish","Louisiana"],["West Baton Rouge Parish","Louisiana"],["West Baton Rouge Parish","Louisiana"],["San Miguel County","New Mexico"],["San Miguel County","New Mexico"],["McDonough County","Illinois"],["Union County","South Carolina"],["Fluvanna County","Virginia"],["White County","Tennessee"],["Tillamook County","Oregon"],["Orleans County","Vermont"],["San Jacinto County","Texas"],["San Jacinto County","Texas"],["San Jacinto County","Texas"],["San Jacinto County","Texas"],["Logan County","Kentucky"],["Adams County","Ohio"],["Jennings County","Indiana"],["Henry County","Ohio"],["Upson County","Georgia"],["Del Norte County","California"],["Union County","Mississippi"],["Jackson County","West Virginia"],["Henderson County","Tennessee"],["Randolph County","West Virginia"],["Monroe County","Georgia"],["Peach County","Georgia"],["Logan County","Illinois"],["Scott County","Mississippi"],["White County","Georgia"],["Hocking County","Ohio"],["Tate County","Mississippi"],["Currituck County","North Carolina"],["Montgomery County","Kentucky"],["Wells County","Indiana"],["Washington County","Indiana"],["Grant County","New Mexico"],["Baker County","Florida"],["Carroll County","Arkansas"],["Dunklin County","Missouri"],["Montgomery County","Illinois"],["Wythe County","Virginia"],["Dillon County","South Carolina"],["Bradford County","Florida"],["Codington County","South Dakota"],["Leflore County","Mississippi"],["Jones County","Georgia"],["Copiah County","Mississippi"],["Palo Pinto County","Texas"],["Lincoln County","Wisconsin"],["Sanpete County","Utah"],["Carroll County","Tennessee"],["Cass County","Texas"],["Perry County","Kentucky"],["Custer County","Oklahoma"],["Marion County","Missouri"],["Elmore County","Idaho"],["Stoddard County","Missouri"],["Le Sueur County","Minnesota"],["Cherokee County","North Carolina"],["Jasper County","South Carolina"],["Garrett County","Maryland"],["Marion County","Tennessee"],["Pine County","Minnesota"],["Alpena County","Michigan"],["Glenn County","California"],["Van Wert County","Ohio"],["Ellis County","Kansas"],["Fayette County","Ohio"],["Ripley County","Indiana"],["Mason County","Michigan"],["Neshoba County","Mississippi"],["Hancock County","West Virginia"],["Morgan County","Colorado"],["Marion County","South Carolina"],["Gallia County","Ohio"],["Grimes County","Texas"],["Orange County","Vermont"],["Marion County","Alabama"],["Decatur County","Georgia"],["Franklin County","Maine"],["Adams County","Mississippi"],["Bladen County","North Carolina"],["Sumter County","Georgia"],["Park County","Wyoming"],["Schoharie County","New York"],["Smyth County","Virginia"],["Meade County","South Dakota"],["Haralson County","Georgia"],["Meade County","Kentucky"],["Cass County","Minnesota"],["Door County","Wisconsin"],["Madison County","Georgia"],["Wayne County","Georgia"],["Randolph County","Illinois"],["Austin County","Texas"],["Knox County","Kentucky"],["McPherson County","Kansas"],["Caledonia County","Vermont"],["Iberville Parish","Louisiana"],["Ottawa County","Oklahoma"],["Mecklenburg County","Virginia"],["Powhatan County","Virginia"],["Giles County","Tennessee"],["Marshall County","West Virginia"],["Boyle County","Kentucky"],["Hardin County","Ohio"],["Vernon County","Wisconsin"],["Trempealeau County","Wisconsin"],["Obion County","Tennessee"],["Greene County","Indiana"],["McCurtain County","Oklahoma"],["Clare County","Michigan"],["Caroline County","Virginia"],["Jefferson County","Idaho"],["Freeborn County","Minnesota"],["Sheridan County","Wyoming"],["Muhlenberg County","Kentucky"],["Wabash County","Indiana"],["Bolivar County","Mississippi"],["Elk County","Pennsylvania"],["Williamsburg County","South Carolina"],["Kleberg County","Texas"],["Bee County","Texas"],["Summit County","Colorado"],["Stone County","Missouri"],["Washington County","Maine"],["Lake County","Montana"],["Clarendon County","South Carolina"],["Pontotoc County","Mississippi"],["Polk County","Minnesota"],["Delta County","Colorado"],["Adams County","Nebraska"],["Titus County","Texas"],["Coos County","New Hampshire"],["Amherst County","Virginia"],["Gilmer County","Georgia"],["Huron County","Michigan"],["Montgomery County","Kansas"],["Polk County","Missouri"],["Malheur County","Oregon"],["Marshall County","Kentucky"],["Claiborne County","Tennessee"],["Franklin County","Alabama"],["Lyon County","Kansas"],["Henry County","Tennessee"],["Jefferson Davis Parish","Louisiana"],["Jefferson Davis Parish","Louisiana"],["Chester County","South Carolina"],["Evangeline Parish","Louisiana"],["Hale County","Texas"],["Dorchester County","Maryland"],["Logan County","West Virginia"],["Jackson County","Ohio"],["Lassen County","California"],["Rhea County","Tennessee"],["Weakley County","Tennessee"],["Morgan County","Illinois"],["Jasper County","Indiana"],["Jefferson County","Washington"],["Greenbrier County","West Virginia"],["Jasper County","Texas"],["Lafayette County","Missouri"],["Transylvania County","North Carolina"],["Pike County","Alabama"],["Gibson County","Indiana"],["Hot Spring County","Arkansas"],["Lawrence County","Alabama"],["Jefferson County","Indiana"],["Lee County","Georgia"],["Clinton County","Indiana"],["Panola County","Mississippi"],["Pickens County","Georgia"],["Bureau County","Illinois"],["Morton County","North Dakota"],["Caroline County","Maryland"],["Daviess County","Indiana"],["Accomack County","Virginia"],["Marion County","Iowa"],["Lincoln County","Oklahoma"],["Lumpkin County","Georgia"],["Lee County","Iowa"],["Botetourt County","Virginia"],["Fulton County","Illinois"],["Stark County","North Dakota"],["Wexford County","Michigan"],["Marshall County","Mississippi"],["Wakulla County","Florida"],["Pulaski County","Virginia"],["Seneca County","New York"],["DeSoto County","Florida"],["Morrison County","Minnesota"],["Halifax County","Virginia"],["Harvey County","Kansas"],["Christian County","Illinois"],["Emmet County","Michigan"],["Lee County","Illinois"],["Scotland County","North Carolina"],["Monroe County","Mississippi"],["Whitley County","Indiana"],["Miami County","Kansas"],["Preston County","West Virginia"],["Ford County","Kansas"],["Platte County","Nebraska"],["Marshall County","Tennessee"],["Brookings County","South Dakota"],["Steuben County","Indiana"],["Putnam County","Ohio"],["Nicollet County","Minnesota"],["Taos County","New Mexico"],["Barry County","Missouri"],["Cowley County","Kansas"],["Clark County","Wisconsin"],["Harris County","Georgia"],["Effingham County","Illinois"],["Lincoln County","Nebraska"],["Alcorn County","Mississippi"],["Chambers County","Alabama"],["Wasatch County","Utah"],["Howard County","Texas"],["Lincoln County","Mississippi"],["Morrow County","Ohio"],["Monroe County","Illinois"],["Silver Bow County","Montana"],["Becker County","Minnesota"],["Lincoln County","Maine"],["Lincoln County","Tennessee"],["Perry County","Ohio"],["Wapello County","Iowa"],["Warren County","Missouri"],["Madison County","Nebraska"],["Uintah County","Utah"],["Fannin County","Texas"],["Washington County","Texas"],["Adams County","Indiana"],["Livingston County","Illinois"],["Sioux County","Iowa"],["Hill County","Texas"],["Floyd County","Kentucky"],["Greene County","Pennsylvania"],["Miami County","Indiana"],["Greenup County","Kentucky"],["Cocke County","Tennessee"],["Laclede County","Missouri"],["Scotts Bluff County","Nebraska"],["Carlton County","Minnesota"],["Ware County","Georgia"],["Orange County","Virginia"],["Matagorda County","Texas"],["Knox County","Indiana"],["Alexander County","North Carolina"],["Beauregard Parish","Louisiana"],["Coshocton County","Ohio"],["Graves County","Kentucky"],["Huntington County","Indiana"],["Sagadahoc County","Maine"],["Okmulgee County","Oklahoma"],["Whitley County","Kentucky"],["Putnam County","Indiana"],["Geary County","Kansas"],["Escambia County","Alabama"],["McLeod County","Minnesota"],["Chippewa County","Michigan"],["Hopkins County","Texas"],["Dyer County","Tennessee"],["Clinton County","Illinois"],["Delta County","Michigan"],["Dare County","North Carolina"],["Webster Parish","Louisiana"],["Clark County","Kentucky"],["Webster County","Iowa"],["Macon County","North Carolina"],["Albany County","Wyoming"],["Green County","Wisconsin"],["Green County","Wisconsin"],["Williams County","Ohio"],["Calloway County","Kentucky"],["Jefferson County","Illinois"],["Dodge County","Nebraska"],["Yadkin County","North Carolina"],["Clarion County","Pennsylvania"],["Bennington County","Vermont"],["Houghton County","Michigan"],["Addison County","Vermont"],["Boone County","Arkansas"],["Essex County","New York"],["Steele County","Minnesota"],["Clinton County","Pennsylvania"],["Natchitoches Parish","Louisiana"],["Talbot County","Maryland"],["Covington County","Alabama"],["Louisa County","Virginia"],["Newberry County","South Carolina"],["Marion County","Illinois"],["Franklin County","Illinois"],["Jasper County","Iowa"],["Oneida County","Wisconsin"],["Cass County","Indiana"],["Montgomery County","Indiana"],["Independence County","Arkansas"],["Lawrence County","Missouri"],["Scott County","Missouri"],["Pontotoc County","Oklahoma"],["Brown County","Texas"],["Defiance County","Ohio"],["Brown County","South Dakota"],["Susquehanna County","Pennsylvania"],["Guernsey County","Ohio"],["Dallas County","Alabama"],["Woodford County","Illinois"],["Finney County","Kansas"],["Graham County","Arizona"],["Warren County","Pennsylvania"],["Colleton County","South Carolina"],["Isle of Wight County","Virginia"],["Gloucester County","Virginia"],["Champaign County","Ohio"],["Jim Wells County","Texas"],["Jim Wells County","Texas"],["Des Moines County","Iowa"],["Oconto County","Wisconsin"],["Crawford County","Kansas"],["Wayne County","West Virginia"],["Douglas County","Minnesota"],["Mayes County","Oklahoma"],["Union County","Arkansas"],["Webster County","Missouri"],["Person County","North Carolina"],["Fremont County","Wyoming"],["Campbell County","Tennessee"],["Sequoyah County","Oklahoma"],["Latah County","Idaho"],["Waldo County","Maine"],["Hendry County","Florida"],["Okeechobee County","Florida"],["Harrison County","Indiana"],["Avoyelles Parish","Louisiana"],["Mecosta County","Michigan"],["Snyder County","Pennsylvania"],["Howell County","Missouri"],["Murray County","Georgia"],["Mower County","Minnesota"],["Marshall County","Iowa"],["Pike County","Mississippi"],["Orleans County","New York"],["Rio Arriba County","New Mexico"],["Ottawa County","Ohio"],["Delaware County","Oklahoma"],["Tazewell County","Virginia"],["McKean County","Pennsylvania"],["Amador County","California"],["Fayette County","West Virginia"],["Wyoming County","New York"],["Pasquotank County","North Carolina"],["Knox County","Maine"],["Sanilac County","Michigan"],["Mississippi County","Arkansas"],["Warren County","Virginia"],["Shawano County","Wisconsin"],["Upshur County","Texas"],["Williams County","North Dakota"],["Warren County","Tennessee"],["Preble County","Ohio"],["Tioga County","Pennsylvania"],["Clatsop County","Oregon"],["Cheatham County","Tennessee"],["Isanti County","Minnesota"],["Tallapoosa County","Alabama"],["Tift County","Georgia"],["Benton County","Minnesota"],["Wharton County","Texas"],["Baxter County","Arkansas"],["McClain County","Oklahoma"],["Cooke County","Texas"],["Gratiot County","Michigan"],["Oconee County","Georgia"],["Marinette County","Wisconsin"],["Fayette County","Tennessee"],["Clinton County","Ohio"],["Crawford County","Ohio"],["Nez Perce County","Idaho"],["Okanogan County","Washington"],["Butler County","Missouri"],["Pierce County","Wisconsin"],["Sweetwater County","Wyoming"],["Summit County","Utah"],["Ohio County","West Virginia"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["St. John the Baptist Parish","Louisiana"],["Mercer County","Ohio"],["Erath County","Texas"],["Vance County","North Carolina"],["Miller County","Arkansas"],["Montrose County","Colorado"],["Union County","Pennsylvania"],["Davie County","North Carolina"],["Fulton County","Ohio"],["Camden County","Missouri"],["Franklin County","Tennessee"],["Stephens County","Oklahoma"],["Polk County","Georgia"],["Levy County","Florida"],["Douglas County","Washington"],["Richmond County","North Carolina"],["Pettis County","Missouri"],["Prince George County","Virginia"],["Sullivan County","New Hampshire"],["Coffee County","Georgia"],["Jackson County","North Carolina"],["Cerro Gordo County","Iowa"],["Muscatine County","Iowa"],["DeKalb County","Indiana"],["Chesterfield County","South Carolina"],["Highland County","Ohio"],["Suwannee County","Florida"],["Dubois County","Indiana"],["Brown County","Ohio"],["Kay County","Oklahoma"],["Kandiyohi County","Minnesota"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["St. Bernard Parish","Louisiana"],["Pittsburg County","Oklahoma"],["Baldwin County","Georgia"],["Madison County","Ohio"],["Gadsden County","Florida"],["Siskiyou County","California"],["Huntingdon County","Pennsylvania"],["Lawrence County","Tennessee"],["Ravalli County","Montana"],["Shenandoah County","Virginia"],["Holmes County","Ohio"],["Kendall County","Texas"],["Callaway County","Missouri"],["Douglas County","Wisconsin"],["Delaware County","New York"],["Kittitas County","Washington"],["Barren County","Kentucky"],["Jefferson County","Pennsylvania"],["Stokes County","North Carolina"],["McDowell County","North Carolina"],["Stephenson County","Illinois"],["Phelps County","Missouri"],["Beaufort County","North Carolina"],["Warren County","Mississippi"],["Bryan County","Georgia"],["Henderson County","Kentucky"],["Wood County","Texas"],["Branch County","Michigan"],["Washington County","Mississippi"],["Macoupin County","Illinois"],["Polk County","Wisconsin"],["Lawrence County","Indiana"],["Chilton County","Alabama"],["Itasca County","Minnesota"],["Shelby County","Indiana"],["Calaveras County","California"],["Hopkins County","Kentucky"],["Dunn County","Wisconsin"],["Washington Parish","Louisiana"],["Greene County","Arkansas"],["Hillsdale County","Michigan"],["Thomas County","Georgia"],["Osage County","Oklahoma"],["Perry County","Pennsylvania"],["Caldwell County","Texas"],["Colquitt County","Georgia"],["Windham County","Vermont"],["Habersham County","Georgia"],["Hancock County","Mississippi"],["Bryan County","Oklahoma"],["Marshall County","Indiana"],["Mifflin County","Pennsylvania"],["Logan County","Ohio"],["Beltrami County","Minnesota"],["Monroe County","Tennessee"],["Monroe County","Wisconsin"],["Auglaize County","Ohio"],["Jackson County","Indiana"],["Stevens County","Washington"],["Allegany County","New York"],["Clinton County","Iowa"],["Chambers County","Texas"],["Barron County","Wisconsin"],["Nelson County","Kentucky"],["Cortland County","New York"],["Coles County","Illinois"],["Campbell County","Wyoming"],["Cherokee County","Oklahoma"],["Bonner County","Idaho"],["Chenango County","New York"],["Jackson County","Florida"],["Noble County","Indiana"],["Franklin County","New York"],["Bedford County","Pennsylvania"],["Goodhue County","Minnesota"],["Val Verde County","Texas"],["Santa Cruz County","Arizona"],["Greene County","New York"],["Whitman County","Washington"],["Bingham County","Idaho"],["Carter County","Oklahoma"],["Shelby County","Kentucky"],["Le Flore County","Oklahoma"],["Crittenden County","Arkansas"],["Shelby County","Ohio"],["Boyd County","Kentucky"],["Lincoln Parish","Louisiana"],["Curry County","New Mexico"],["Tioga County","New York"],["Halifax County","North Carolina"],["Duplin County","North Carolina"],["Vernon Parish","Louisiana"],["Edgecombe County","North Carolina"],["Henry County","Indiana"],["Fremont County","Colorado"],["Atascosa County","Texas"],["Burnet County","Texas"],["Henry County","Illinois"],["Dale County","Alabama"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["St. Mary Parish","Louisiana"],["Douglas County","Nevada"],["Montgomery County","New York"],["Logan County","Oklahoma"],["Laurens County","Georgia"],["Winona County","Minnesota"],["Wilson County","Texas"],["Queen Anne's County","Maryland"],["Franklin County","Vermont"],["Knox County","Illinois"],["Newaygo County","Michigan"],["Buffalo County","Nebraska"],["Lamar County","Texas"],["Carroll County","New Hampshire"],["Polk County","Texas"],["Bedford County","Tennessee"],["Lincoln County","Oregon"],["Cherokee County","Texas"],["Gibson County","Tennessee"],["Venango County","Pennsylvania"],["Somerset County","Maine"],["Columbus County","North Carolina"],["Dearborn County","Indiana"],["Medina County","Texas"],["Bristol County","Rhode Island"],["Wayne County","Pennsylvania"],["Franklin County","Kentucky"],["Cass County","Michigan"],["Nye County","Nevada"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["St. Martin Parish","Louisiana"],["Ogle County","Illinois"],["Oktibbeha County","Mississippi"],["Waupaca County","Wisconsin"],["Darke County","Ohio"],["Grant County","Wisconsin"],["Hoke County","North Carolina"],["Rusk County","Texas"],["Warren County","Iowa"],["Calumet County","Wisconsin"],["Ashland County","Ohio"],["Washington County","Oklahoma"],["Worcester County","Maryland"],["Grundy County","Illinois"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["St. Charles Parish","Louisiana"],["Culpeper County","Virginia"],["Jackson County","Alabama"],["Columbia County","Oregon"],["Kerr County","Texas"],["Navarro County","Texas"],["Madison County","Idaho"],["Jackson County","Illinois"],["Jessamine County","Kentucky"],["Gila County","Arizona"],["McMinn County","Tennessee"],["Tuscola County","Michigan"],["Fulton County","New York"],["Roane County","Tennessee"],["Boone County","Illinois"],["Coffee County","Alabama"],["Elko County","Nevada"],["Pulaski County","Missouri"],["Johnson County","Missouri"],["Watauga County","North Carolina"],["Saline County","Kansas"],["Dickson County","Tennessee"],["Franklin County","Virginia"],["Jefferson County","Tennessee"],["Camden County","Georgia"],["Grady County","Oklahoma"],["Loudon County","Tennessee"],["Seneca County","Ohio"],["Lenoir County","North Carolina"],["Hancock County","Maine"],["Tuolumne County","California"],["La Plata County","Colorado"],["Whiteside County","Illinois"],["Eagle County","Colorado"],["Lafayette County","Mississippi"],["Taney County","Missouri"],["Pearl River County","Mississippi"],["Marion County","West Virginia"],["Cherokee County","South Carolina"],["Hardin County","Texas"],["Carter County","Tennessee"],["Chisago County","Minnesota"],["Hawkins County","Tennessee"],["Waller County","Texas"],["Scott County","Kentucky"],["Colbert County","Alabama"],["Iron County","Utah"],["Vermilion Parish","Louisiana"],["Putnam County","West Virginia"],["Gordon County","Georgia"],["Acadia Parish","Louisiana"],["Box Elder County","Utah"],["Jefferson County","West Virginia"],["Windsor County","Vermont"],["Oxford County","Maine"],["Maverick County","Texas"],["Coffee County","Tennessee"],["Anderson County","Texas"],["Lawrence County","Ohio"],["Genesee County","New York"],["Columbia County","Wisconsin"],["Otsego County","New York"],["Pike County","Pennsylvania"],["Pickaway County","Ohio"],["Huron County","Ohio"],["Carson City","Nevada"],["Newton County","Missouri"],["Pike County","Kentucky"],["Autauga County","Alabama"],["Lowndes County","Mississippi"],["Sandusky County","Ohio"],["Sampson County","North Carolina"],["Blount County","Alabama"],["Russell County","Alabama"],["Lyon County","Nevada"],["Van Zandt County","Texas"],["Lincoln County","Missouri"],["Mercer County","West Virginia"],["Washington County","Ohio"],["Washington County","Vermont"],["Bradford County","Pennsylvania"],["Otter Tail County","Minnesota"],["Crawford County","Arkansas"],["Herkimer County","New York"],["Pender County","North Carolina"],["Rutland County","Vermont"],["St. Joseph County","Michigan"],["St. Joseph County","Michigan"],["Tipton County","Tennessee"],["Granville County","North Carolina"],["Cumberland County","Tennessee"],["Washington County","New York"],["Columbia County","New York"],["Hood County","Texas"],["Garfield County","Colorado"],["Livingston County","New York"],["Reno County","Kansas"],["Haywood County","North Carolina"],["Eddy County","New Mexico"],["Barry County","Michigan"],["Athens County","Ohio"],["Stanly County","North Carolina"],["Walla Walla County","Washington"],["Laurel County","Kentucky"],["Knox County","Ohio"],["Union County","Ohio"],["Garfield County","Oklahoma"],["Hall County","Nebraska"],["Darlington County","South Carolina"],["Lee County","North Carolina"],["Pope County","Arkansas"],["Georgetown County","South Carolina"],["Belknap County","New Hampshire"],["Warrick County","Indiana"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["San Benito County","California"],["Lamar County","Mississippi"],["Isabella County","Michigan"],["Rutherford County","North Carolina"],["Hamblen County","Tennessee"],["Nacogdoches County","Texas"],["Columbia County","Pennsylvania"],["Carbon County","Pennsylvania"],["Effingham County","Georgia"],["Salem County","New Jersey"],["Coos County","Oregon"],["Pulaski County","Kentucky"],["Chaves County","New Mexico"],["Lincoln County","South Dakota"],["Jefferson County","Ohio"],["Liberty County","Georgia"],["Clay County","Minnesota"],["Walker County","Alabama"],["Marion County","Ohio"],["Kershaw County","South Carolina"],["Armstrong County","Pennsylvania"],["Mason County","Washington"],["Adams County","Illinois"],["Warren County","New York"],["Sauk County","Wisconsin"],["Tehama County","California"],["Starr County","Texas"],["Harrison County","West Virginia"],["Wilkes County","North Carolina"],["Marquette County","Michigan"],["Apache County","Arizona"],["Crow Wing County","Minnesota"],["Chippewa County","Wisconsin"],["Muskogee County","Oklahoma"],["Belmont County","Ohio"],["Wayne County","Indiana"],["Montcalm County","Michigan"],["Grant County","Indiana"],["Ionia County","Michigan"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["St. Francois County","Missouri"],["Rice County","Minnesota"],["Aroostook County","Maine"],["Williamson County","Illinois"],["Jones County","Mississippi"],["Jefferson County","Arkansas"],["Spalding County","Georgia"],["Butler County","Kansas"],["Laurens County","South Carolina"],["Oldham County","Kentucky"],["Walker County","Georgia"],["Carteret County","North Carolina"],["Otero County","New Mexico"],["Catoosa County","Georgia"],["McCracken County","Kentucky"],["Madison County","New York"],["Shiawassee County","Michigan"],["Allegany County","Maryland"],["Lake County","California"],["Franklin County","North Carolina"],["Wise County","Texas"],["San Patricio County","Texas"],["San Patricio County","Texas"],["San Patricio County","Texas"],["San Patricio County","Texas"],["Harrison County","Texas"],["Blue Earth County","Minnesota"],["Greenwood County","South Carolina"],["Klamath County","Oregon"],["Troup County","Georgia"],["Columbia County","Florida"],["Ward County","North Dakota"],["Iberia Parish","Louisiana"],["Greene County","Tennessee"],["Portage County","Wisconsin"],["Boone County","Indiana"],["Lewis and Clark County","Montana"],["Franklin County","Massachusetts"],["Surry County","North Carolina"],["DeKalb County","Alabama"],["Creek County","Oklahoma"],["Morgan County","Indiana"],["Riley County","Kansas"],["Pottawatomie County","Oklahoma"],["Tooele County","Utah"],["Christian County","Kentucky"],["Robertson County","Tennessee"],["McKinley County","New Mexico"],["Fauquier County","Virginia"],["Lauderdale County","Mississippi"],["Grand Forks County","North Dakota"],["Kauai County","Hawaii"],["Putnam County","Florida"],["Scioto County","Ohio"],["Lonoke County","Arkansas"],["Broomfield County","Colorado"],["Somerset County","Pennsylvania"],["Vermilion County","Illinois"],["Wood County","Wisconsin"],["Lea County","New Mexico"],["Raleigh County","West Virginia"],["Hancock County","Ohio"],["Walton County","Florida"],["Van Buren County","Michigan"],["Erie County","Ohio"],["Grays Harbor County","Washington"],["Jackson County","Georgia"],["Valencia County","New Mexico"],["Cayuga County","New York"],["Chatham County","North Carolina"],["Walker County","Texas"],["Cheshire County","New Hampshire"],["White County","Arkansas"],["Cattaraugus County","New York"],["Ross County","Ohio"],["Anderson County","Tennessee"],["Clallam County","Washington"],["Cole County","Missouri"],["Forrest County","Mississippi"],["Oconee County","South Carolina"],["Sullivan County","New York"],["Wilson County","North Carolina"],["Chelan County","Washington"],["Clinton County","Michigan"],["Bedford County","Virginia"],["Hancock County","Indiana"],["Clinton County","New York"],["Putnam County","Tennessee"],["Natrona County","Wyoming"],["Umatilla County","Oregon"],["Kosciusko County","Indiana"],["Floyd County","Indiana"],["Clearfield County","Pennsylvania"],["Caldwell County","North Carolina"],["Wagoner County","Oklahoma"],["Bulloch County","Georgia"],["Manitowoc County","Wisconsin"],["Yuba County","California"],["Payne County","Oklahoma"],["Cape Girardeau County","Missouri"],["Leavenworth County","Kansas"],["Talladega County","Alabama"],["Lewis County","Washington"],["Henderson County","Texas"],["Bartholomew County","Indiana"],["Bullitt County","Kentucky"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["St. Landry Parish","Louisiana"],["Monroe County","Florida"],["Coryell County","Texas"],["Indiana County","Pennsylvania"],["Lee County","Mississippi"],["Midland County","Michigan"],["Barrow County","Georgia"],["Howard County","Indiana"],["Crawford County","Pennsylvania"],["Chemung County","New York"],["Orangeburg County","South Carolina"],["Wood County","West Virginia"],["Cascade County","Montana"],["Glynn County","Georgia"],["Buchanan County","Missouri"],["Orange County","Texas"],["Jefferson County","Wisconsin"],["Newport County","Rhode Island"],["Dougherty County","Georgia"],["Lawrence County","Pennsylvania"],["Angelina County","Texas"],["Muskingum County","Ohio"],["Lincoln County","North Carolina"],["Island County","Washington"],["Bannock County","Idaho"],["Polk County","Oregon"],["Burke County","North Carolina"],["Cullman County","Alabama"],["Elmore County","Alabama"],["Josephine County","Oregon"],["Lapeer County","Michigan"],["Christian County","Missouri"],["Dodge County","Wisconsin"],["Twin Falls County","Idaho"],["Nassau County","Florida"],["Rockingham County","North Carolina"],["St. Clair County","Alabama"],["Grafton County","New Hampshire"],["Wayne County","New York"],["Victoria County","Texas"],["Ozaukee County","Wisconsin"],["Mendocino County","California"],["Liberty County","Texas"],["Northumberland County","Pennsylvania"],["Madison County","Kentucky"],["Calvert County","Maryland"],["Bowie County","Texas"],["Campbell County","Kentucky"],["Tuscarawas County","Ohio"],["St. Croix County","Wisconsin"],["Lauderdale County","Alabama"],["Rockdale County","Georgia"],["Steuben County","New York"],["Pottawattamie County","Iowa"],["Cabell County","West Virginia"],["Nash County","North Carolina"],["Benton County","Oregon"],["Grand Traverse County","Michigan"],["Rogers County","Oklahoma"],["Cape May County","New Jersey"],["Geauga County","Ohio"],["Lancaster County","South Carolina"],["Walton County","Georgia"],["Franklin County","Washington"],["Sherburne County","Minnesota"],["Bastrop County","Texas"],["Lafourche Parish","Louisiana"],["Ashtabula County","Ohio"],["Marshall County","Alabama"],["Putnam County","New York"],["Sevier County","Tennessee"],["Burleigh County","North Dakota"],["Story County","Iowa"],["Floyd County","Georgia"],["Madison County","Tennessee"],["Grant County","Washington"],["Dubuque County","Iowa"],["Lenawee County","Michigan"],["Cleveland County","North Carolina"],["Sutter County","California"],["Dallas County","Iowa"],["Moore County","North Carolina"],["Hunt County","Texas"],["Garland County","Arkansas"],["DeKalb County","Illinois"],["Laramie County","Wyoming"],["Craven County","North Carolina"],["Maury County","Tennessee"],["Highlands County","Florida"],["Columbiana County","Ohio"],["Allen County","Ohio"],["Nevada County","California"],["Whitfield County","Georgia"],["Daviess County","Kentucky"],["Etowah County","Alabama"],["Limestone County","Alabama"],["Wicomico County","Maryland"],["Cecil County","Maryland"],["Adams County","Pennsylvania"],["Bay County","Michigan"],["Macon County","Illinois"],["Fond du Lac County","Wisconsin"],["Flathead County","Montana"],["Franklin County","Missouri"],["Sumter County","South Carolina"],["Eau Claire County","Wisconsin"],["Tompkins County","New York"],["Monongalia County","West Virginia"],["Woodbury County","Iowa"],["Vigo County","Indiana"],["Walworth County","Wisconsin"],["Navajo County","Arizona"],["Platte County","Missouri"],["Carver County","Minnesota"],["Houston County","Alabama"],["Kankakee County","Illinois"],["Yamhill County","Oregon"],["Rockwall County","Texas"],["Cass County","Missouri"],["St. Lawrence County","New York"],["Bradley County","Tennessee"],["Miami County","Ohio"],["Bartow County","Georgia"],["Madison County","Mississippi"],["Eaton County","Michigan"],["Pennington County","South Dakota"],["Terrebonne Parish","Louisiana"],["Warren County","New Jersey"],["LaSalle County","Illinois"],["Hanover County","Virginia"],["Mercer County","Pennsylvania"],["Hardin County","Kentucky"],["Cowlitz County","Washington"],["Androscoggin County","Maine"],["Douglas County","Oregon"],["Craighead County","Arkansas"],["Delaware County","Indiana"],["LaPorte County","Indiana"],["Ontario County","New York"],["Newton County","Georgia"],["St. Mary's County","Maryland"],["Lycoming County","Pennsylvania"],["Flagler County","Florida"],["Henderson County","North Carolina"],["Windham County","Connecticut"],["Calhoun County","Alabama"],["Robeson County","North Carolina"],["Jefferson County","New York"],["Wayne County","Ohio"],["Wayne County","North Carolina"],["Oswego County","New York"],["Missoula County","Montana"],["Sheboygan County","Wisconsin"],["Lowndes County","Georgia"],["Potter County","Texas"],["Douglas County","Kansas"],["Gallatin County","Montana"],["Carroll County","Georgia"],["Fayette County","Georgia"],["Tom Green County","Texas"],["Allegan County","Michigan"],["La Crosse County","Wisconsin"],["Clark County","Indiana"],["Comanche County","Oklahoma"],["San Juan County","New Mexico"],["San Juan County","New Mexico"],["Berkeley County","West Virginia"],["Jasper County","Missouri"],["Blair County","Pennsylvania"],["Saline County","Arkansas"],["Morgan County","Alabama"],["Faulkner County","Arkansas"],["Kennebec County","Maine"],["Bonneville County","Idaho"],["Gregg County","Texas"],["Richland County","Ohio"],["Cochise County","Arizona"],["Ascension Parish","Louisiana"],["Chautauqua County","New York"],["Sebastian County","Arkansas"],["Linn County","Oregon"],["Clarke County","Georgia"],["Bossier Parish","Louisiana"],["Fayette County","Pennsylvania"],["Hunterdon County","New Jersey"],["Berkshire County","Massachusetts"],["Wichita County","Texas"],["Skagit County","Washington"],["Sumter County","Florida"],["Washington County","Rhode Island"],["Rapides Parish","Louisiana"],["Madison County","Indiana"],["Strafford County","New Hampshire"],["Black Hawk County","Iowa"],["Tazewell County","Illinois"],["Pickens County","South Carolina"],["Kendall County","Illinois"],["Wood County","Ohio"],["Washington County","Tennessee"],["Cache County","Utah"],["Tangipahoa Parish","Louisiana"],["Cambria County","Pennsylvania"],["Harnett County","North Carolina"],["Calhoun County","Michigan"],["Warren County","Kentucky"],["Blount County","Tennessee"],["Grayson County","Texas"],["Boone County","Kentucky"],["Clark County","Ohio"],["Humboldt County","California"],["Brunswick County","North Carolina"],["Washington County","Wisconsin"],["Florence County","South Carolina"],["Marathon County","Wisconsin"],["Napa County","California"],["Monroe County","Indiana"],["Randall County","Texas"],["Wright County","Minnesota"],["Livingston Parish","Louisiana"],["Schuylkill County","Pennsylvania"],["Taylor County","Texas"],["Jackson County","Mississippi"],["Lebanon County","Pennsylvania"],["Randolph County","North Carolina"],["Sussex County","New Jersey"],["Douglas County","Georgia"],["Rock Island County","Illinois"],["Coconino County","Arizona"],["Kaufman County","Texas"],["Coweta County","Georgia"],["Rowan County","North Carolina"],["Wilson County","Tennessee"],["Parker County","Texas"],["Orange County","North Carolina"],["Sandoval County","New Mexico"],["Tolland County","Connecticut"],["Scott County","Minnesota"],["Penobscot County","Maine"],["Kings County","California"],["Johnson County","Iowa"],["Merrimack County","New Hampshire"],["Citrus County","Florida"],["Cumberland County","New Jersey"],["Berrien County","Michigan"],["Canadian County","Oklahoma"],["Washington County","Maryland"],["Monroe County","Michigan"],["Santa Fe County","New Mexico"],["Mesa County","Colorado"],["Franklin County","Pennsylvania"],["Columbia County","Georgia"],["Madera County","California"],["Stafford County","Virginia"],["Rankin County","Mississippi"],["Bibb County","Georgia"],["Schenectady County","New York"],["Sullivan County","Tennessee"],["Centre County","Pennsylvania"],["Stearns County","Minnesota"],["Martin County","Florida"],["Fairfield County","Ohio"],["Indian River County","Florida"],["Jackson County","Michigan"],["Ouachita Parish","Louisiana"],["St. Clair County","Michigan"],["St. Clair County","Michigan"],["Catawba County","North Carolina"],["Rensselaer County","New York"],["Comal County","Texas"],["Dorchester County","South Carolina"],["Johnson County","Indiana"],["Portage County","Ohio"],["Hampshire County","Massachusetts"],["Olmsted County","Minnesota"],["Houston County","Georgia"],["Rock County","Wisconsin"],["Middlesex County","Connecticut"],["Yellowstone County","Montana"],["Maui County","Hawaii"],["Ector County","Texas"],["Charles County","Maryland"],["Greene County","Ohio"],["Pueblo County","Colorado"],["Beaver County","Pennsylvania"],["Chittenden County","Vermont"],["Monroe County","Pennsylvania"],["Paulding County","Georgia"],["Aiken County","South Carolina"],["Davidson County","North Carolina"],["Kenton County","Kentucky"],["Kenosha County","Wisconsin"],["Wyandotte County","Kansas"],["Midland County","Texas"],["Pitt County","North Carolina"],["Kent County","Rhode Island"],["McLean County","Illinois"],["Kootenai County","Idaho"],["Alamance County","North Carolina"],["Winnebago County","Wisconsin"],["Guadalupe County","Texas"],["Carroll County","Maryland"],["Porter County","Indiana"],["Lee County","Alabama"],["Scott County","Iowa"],["Hendricks County","Indiana"],["Bay County","Florida"],["Muskegon County","Michigan"],["Licking County","Ohio"],["Shawnee County","Kansas"],["Imperial County","California"],["Johnson County","Texas"],["Vanderburgh County","Indiana"],["Washington County","Utah"],["Kanawha County","West Virginia"],["Peoria County","Illinois"],["Kent County","Delaware"],["Ulster County","New York"],["Shasta County","California"],["Medina County","Ohio"],["Boone County","Missouri"],["Cass County","North Dakota"],["Litchfield County","Connecticut"],["DeSoto County","Mississippi"],["Tippecanoe County","Indiana"],["Iredell County","North Carolina"],["Charlotte County","Florida"],["Beaufort County","South Carolina"],["Santa Rosa County","Florida"],["Saginaw County","Michigan"],["Sarpy County","Nebraska"],["Outagamie County","Wisconsin"],["El Dorado County","California"],["Ellis County","Texas"],["Butler County","Pennsylvania"],["Livingston County","Michigan"],["Hernando County","Florida"],["Sumner County","Tennessee"],["Sangamon County","Illinois"],["Minnehaha County","South Dakota"],["Racine County","Wisconsin"],["Deschutes County","Oregon"],["Broome County","New York"],["St. Louis County","Minnesota"],["Trumbull County","Ohio"],["Hall County","Georgia"],["Anderson County","South Carolina"],["Yuma County","Arizona"],["Onslow County","North Carolina"],["Champaign County","Illinois"],["Richmond County","Georgia"],["Benton County","Washington"],["Muscogee County","Georgia"],["Elkhart County","Indiana"],["Clermont County","Ohio"],["Harrison County","Mississippi"],["Washington County","Pennsylvania"],["Butte County","California"],["Okaloosa County","Florida"],["York County","Maine"],["Niagara County","New York"],["Mohave County","Arizona"],["Delaware County","Ohio"],["Lackawanna County","Pennsylvania"],["Johnston County","North Carolina"],["Yolo County","California"],["Calcasieu Parish","Louisiana"],["Clay County","Florida"],["Montgomery County","Tennessee"],["Shelby County","Alabama"],["Jackson County","Oregon"],["New Hanover County","North Carolina"],["Cabarrus County","North Carolina"],["Richmond city","Virginia"],["Jefferson County","Missouri"],["Whatcom County","Washington"],["Tuscaloosa County","Alabama"],["Hinds County","Mississippi"],["Gaston County","North Carolina"],["Mahoning County","Ohio"],["Montgomery County","Alabama"],["Barnstable County","Massachusetts"],["Berkeley County","South Carolina"],["Linn County","Iowa"],["Canyon County","Idaho"],["Baldwin County","Alabama"],["Oneida County","New York"],["Lake County","Ohio"],["Smith County","Texas"],["Brazos County","Texas"],["Saratoga County","New York"],["Yavapai County","Arizona"],["Sussex County","Delaware"],["Caddo Parish","Louisiana"],["Union County","North Carolina"],["Arlington County","Virginia"],["Henry County","Georgia"],["Hays County","Texas"],["Lafayette Parish","Louisiana"],["Warren County","Ohio"],["Washington County","Arkansas"],["Williamson County","Tennessee"],["Forsyth County","Georgia"],["Clay County","Missouri"],["Jefferson County","Texas"],["Yakima County","Washington"],["St. Clair County","Illinois"],["Cumberland County","Pennsylvania"],["McLennan County","Texas"],["Harford County","Maryland"],["Kalamazoo County","Michigan"],["Weber County","Utah"],["Marin County","California"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["St. Tammany Parish","Louisiana"],["Madison County","Illinois"],["Cherokee County","Georgia"],["Webb County","Texas"],["Washington County","Minnesota"],["New London County","Connecticut"],["New London County","Connecticut"],["Brown County","Wisconsin"],["Buncombe County","North Carolina"],["Santa Cruz County","California"],["Santa Cruz County","California"],["Santa Cruz County","California"],["Erie County","Pennsylvania"],["Frederick County","Maryland"],["St. Joseph County","Indiana"],["St. Johns County","Florida"],["St. Johns County","Florida"],["Atlantic County","New Jersey"],["Kitsap County","Washington"],["Alachua County","Florida"],["Merced County","California"],["York County","South Carolina"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["San Luis Obispo County","California"],["Benton County","Arkansas"],["Ingham County","Michigan"],["Winnebago County","Illinois"],["Dauphin County","Pennsylvania"],["Leon County","Florida"],["Lexington County","South Carolina"],["Thurston County","Washington"],["Chatham County","Georgia"],["Cleveland County","Oklahoma"],["Dutchess County","New York"],["Ottawa County","Michigan"],["Clayton County","Georgia"],["Greene County","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["St. Louis city","Missouri"],["Gloucester County","New Jersey"],["Cumberland County","Maine"],["McHenry County","Illinois"],["Lubbock County","Texas"],["Northampton County","Pennsylvania"],["Lorain County","Ohio"],["Rockingham County","New Hampshire"],["Albany County","New York"],["Escambia County","Florida"],["Fayette County","Kentucky"],["Lancaster County","Nebraska"],["Durham County","North Carolina"],["Luzerne County","Pennsylvania"],["Spartanburg County","South Carolina"],["Weld County","Colorado"],["St. Lucie County","Florida"],["St. Lucie County","Florida"],["Boulder County","Colorado"],["Howard County","Maryland"],["Henrico County","Virginia"],["Cumberland County","North Carolina"],["Rockland County","New York"],["Rutherford County","Tennessee"],["Somerset County","New Jersey"],["Marion County","Oregon"],["Hamilton County","Indiana"],["Galveston County","Texas"],["Horry County","South Carolina"],["Nueces County","Texas"],["Westmoreland County","Pennsylvania"],["Douglas County","Colorado"],["Larimer County","Colorado"],["Davis County","Utah"],["Anoka County","Minnesota"],["Chesterfield County","Virginia"],["Hamilton County","Tennessee"],["Bell County","Texas"],["Brazoria County","Texas"],["Washtenaw County","Michigan"],["Lehigh County","Pennsylvania"],["Stark County","Ohio"],["Collier County","Florida"],["Marion County","Florida"],["Forsyth County","North Carolina"],["Lane County","Oregon"],["Lake County","Florida"],["Orleans Parish","Louisiana"],["Allen County","Indiana"],["Mercer County","New Jersey"],["Madison County","Alabama"],["Osceola County","Florida"],["Butler County","Ohio"],["Pulaski County","Arkansas"],["Manatee County","Florida"],["Orange County","New York"],["Placer County","California"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["St. Charles County","Missouri"],["Genesee County","Michigan"],["Waukesha County","Wisconsin"],["Charleston County","South Carolina"],["Mobile County","Alabama"],["Richland County","South Carolina"],["Loudoun County","Virginia"],["Cameron County","Texas"],["Clackamas County","Oregon"],["Hillsborough County","New Hampshire"],["Pinal County","Arizona"],["Berks County","Pennsylvania"],["Lucas County","Ohio"],["Sarasota County","Florida"],["Monterey County","California"],["Dakota County","Minnesota"],["Jefferson Parish","Louisiana"],["Jefferson Parish","Louisiana"],["Santa Barbara County","California"],["Santa Barbara County","California"],["Santa Barbara County","California"],["Solano County","California"],["York County","Pennsylvania"],["East Baton Rouge Parish","Louisiana"],["East Baton Rouge Parish","Louisiana"],["East Baton Rouge Parish","Louisiana"],["Burlington County","New Jersey"],["Hampden County","Massachusetts"],["Seminole County","Florida"],["Tulare County","California"],["Onondaga County","New York"],["Knox County","Tennessee"],["Prince William County","Virginia"],["Washoe County","Nevada"],["Sonoma County","California"],["Polk County","Iowa"],["Ada County","Idaho"],["Richmond County","New York"],["Lake County","Indiana"],["Clark County","Washington"],["Morris County","New Jersey"],["Kane County","Illinois"],["Adams County","Colorado"],["Camden County","New Jersey"],["Sedgwick County","Kansas"],["Passaic County","New Jersey"],["Greenville County","South Carolina"],["Plymouth County","Massachusetts"],["Chester County","Pennsylvania"],["Montgomery County","Ohio"],["Spokane County","Washington"],["Summit County","Ohio"],["Guilford County","North Carolina"],["Ramsey County","Minnesota"],["Stanislaus County","California"],["Lancaster County","Pennsylvania"],["Volusia County","Florida"],["Dane County","Wisconsin"],["Pasco County","Florida"],["New Castle County","Delaware"],["Union County","New Jersey"],["Delaware County","Pennsylvania"],["Bristol County","Massachusetts"],["Jefferson County","Colorado"],["Douglas County","Nebraska"],["Baltimore city","Maryland"],["Baltimore city","Maryland"],["Anne Arundel County","Maryland"],["Washington County","Oregon"],["Brevard County","Florida"],["Williamson County","Texas"],["Johnson County","Kansas"],["Montgomery County","Texas"],["Ocean County","New Jersey"],["Monmouth County","New Jersey"],["Bucks County","Pennsylvania"],["Arapahoe County","Colorado"],["Kent County","Michigan"],["Providence County","Rhode Island"],["Tulsa County","Oklahoma"],["Jefferson County","Alabama"],["Bernalillo County","New Mexico"],["Will County","Illinois"],["Lake County","Illinois"],["Denver County","Colorado"],["Davidson County","Tennessee"],["Jackson County","Missouri"],["Hudson County","New Jersey"],["Polk County","Florida"],["Norfolk County","Massachusetts"],["El Paso County","Colorado"],["Monroe County","New York"],["Lee County","Florida"],["DeKalb County","Georgia"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["San Mateo County","California"],["Cobb County","Georgia"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["San Joaquin County","California"],["Jefferson County","Kentucky"],["Suffolk County","Massachusetts"],["Essex County","Massachusetts"],["Multnomah County","Oregon"],["Fort Bend County","Texas"],["Snohomish County","Washington"],["Hamilton County","Ohio"],["Ventura County","California"],["Baltimore County","Maryland"],["Baltimore County","Maryland"],["Montgomery County","Pennsylvania"],["Worcester County","Massachusetts"],["Middlesex County","New Jersey"],["Essex County","New Jersey"],["New Haven County","Connecticut"],["New Haven County","Connecticut"],["El Paso County","Texas"],["Hidalgo County","Texas"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["San Francisco County","California"],["Macomb County","Michigan"],["Hartford County","Connecticut"],["Denton County","Texas"],["Kern County","California"],["Pierce County","Washington"],["Shelby County","Tennessee"],["DuPage County","Illinois"],["Milwaukee County","Wisconsin"],["Erie County","New York"],["Bergen County","New Jersey"],["Gwinnett County","Georgia"],["Fairfield County","Connecticut"],["Pinellas County","Florida"],["Prince George's County","Maryland"],["Marion County","Indiana"],["Duval County","Florida"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["St. Louis County","Missouri"],["Westchester County","New York"],["Fresno County","California"],["Honolulu County","Hawaii"],["Pima County","Arizona"],["Montgomery County","Maryland"],["Collin County","Texas"],["Fulton County","Georgia"],["Mecklenburg County","North Carolina"],["Wake County","North Carolina"],["Contra Costa County","California"],["Salt Lake County","Utah"],["Allegheny County","Pennsylvania"],["Cuyahoga County","Ohio"],["Oakland County","Michigan"],["Hennepin County","Minnesota"],["Travis County","Texas"],["Franklin County","Ohio"],["Nassau County","New York"],["Orange County","Florida"],["Hillsborough County","Florida"],["Bronx County","New York"],["Palm Beach County","Florida"],["Suffolk County","New York"],["Sacramento County","California"],["Philadelphia County","Pennsylvania"],["Middlesex County","Massachusetts"],["Alameda County","California"],["Wayne County","Michigan"],["Santa Clara County","California"],["Santa Clara County","California"],["Santa Clara County","California"],["Broward County","Florida"],["Bexar County","Texas"],["Tarrant County","Texas"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["San Bernardino County","California"],["Clark County","Nevada"],["King County","Washington"],["Queens County","New York"],["Riverside County","California"],["Dallas County","Texas"],["Miami-Dade County","Florida"],["Kings County","New York"],["Orange County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["San Diego County","California"],["Maricopa County","Arizona"],["Harris County","Texas"],["Cook County","Illinois"],["Los Angeles County","California"]],"hovertemplate":"x=%{x}\u003cbr\u003eLog ChrstAdherentsPerCapita=%{y}\u003cbr\u003eCOUNAM=%{customdata[0]}\u003cbr\u003eSTATNAM=%{customdata[1]}\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","marker":{"color":"#636efa","symbol":"circle"},"mode":"markers","name":"","showlegend":false,"x":[11.590747246673999,11.32547477664184,10.809020627757324,11.120771370921736,11.167204591251192,10.886801216840775,10.528971334610977,11.299657984326226,11.02825479868109,10.893623364868153,11.150548581541834,10.68748041639565,11.012512111551548,11.06925992304676,10.899236205744998,11.520417330728524,11.086349073649137,10.751113930384133,10.911335977890648,10.777955789556444,10.810152101015651,10.915688284286576,10.91217513367625,11.107570350812507,11.167416520015664,10.900307027795478,10.75304001226021,10.926423973878354,10.875761563605456,11.356973163196342,11.079060882340366,10.950350302402153,10.809525907945932,10.699529711814108,11.371776561208646,10.608291527903145,10.867730001943455,10.82865873621622,10.929314071478585,11.608462891679292,11.109099013530573,10.63962238089551,11.213022352221492,11.21667344183538,11.22472325727156,11.114788440747668,11.005327958555663,11.371477101385853,10.743803956312695,10.335562134069491,11.007021045523306,11.124228974437301,10.950613545737037,11.001683087707896,10.617931341885154,11.185587384638161,10.727948042591994,10.785041901601423,10.71716953472481,10.8673105148556,11.43117296309797,10.593329276087347,11.00421427088809,11.169998440958999,10.548651743073922,11.206468237192114,11.348534195502129,10.95336467552236,10.960148737257558,10.738915240352844,10.610365039544332,10.893957682584535,11.085889366933921,10.698672233649825,10.84501708927391,10.720951930103388,11.169462852503631,10.73733102144275,11.370312963609512,11.057550315864589,10.842478669931058,10.713839823996778,11.033097736903727,10.79055542573338,11.03791733406963,11.173753587595897,10.833681189579275,11.01105958257571,10.899383973528197,10.968267252667786,10.488018924717574,10.778685419874725,10.185428174358796,11.017021293881239,10.766229817452608,10.627333661845343,10.957607926312159,11.061437360549744,10.884554277349194,10.8673105148556,10.897368757042468,10.699822890892243,11.34042749832491,11.143555999758231,11.005593730458493,11.34370175564545,10.982288213867557,11.090904054546346,10.568543852929547,11.05685629858094,11.007518467231098,11.2928148097734,10.699213884343516,10.587064080156123,11.297390395609458,10.932410298526829,11.067559812676024,10.969955365655448,10.94187201565375,11.125747129949204,10.577528363356336,11.03034710414234,11.140222759954298,10.59425690831011,11.109533207022995,10.620522143549415,10.970832747329727,10.246332298662626,10.907715898976086,10.9517534667675,10.849181734779526,10.846906951798536,10.865860022197287,11.238764896889764,10.618494067448967,10.798084670325027,10.740323737069875,11.056082848402292,10.657870932566647,11.235352126666735,10.757221797744021,11.161238062542536,10.851354467845027,10.657188764185747,11.105423283436139,10.962579083041954,10.809970343419197,10.927502005497212,10.792797556078508,10.768632347586125,11.017497355384243,10.793865427624695,11.076108998952167,10.772728604718623,10.899550186188444,10.993344962180375,10.897387263737267,11.529703916209046,10.527793635805121,10.934908916663861,10.566871159890386,11.023828716667804,10.755474402409464,10.575564302476781,11.20052711298135,10.715794598265331,10.570085397862536,11.005327958555663,11.064855524029626,11.01402841206951,10.9207270827385,10.872484580041217,10.96242302405134,10.815750182489847,11.076232813045465,11.176739187458812,11.140556584351254,10.78766823049205,11.476531153777126,11.021101494211369,10.994823432233462,11.342101556168096,10.66494737327816,10.592551407658437,11.111387634999954,10.504409789053556,10.718697486570514,10.705399447887462,10.752569534716834,10.920003637661642,10.814906436206515,11.074094868375386,10.476160579628198,10.926837356703691,10.843572932976,10.781702515558052,11.108664631432267,11.120164318733623,10.631615701991318,10.692194881655606,10.619203139938547,11.1645729363183,10.928686499533763,10.916541952842591,11.202752354682916,10.846205976245562,10.773776229848485,11.133815002144742,10.927555876583714,10.584435625639076,10.8485017864294,10.713506242327334,10.959522835329864,10.502900810345617,10.884254303594648,10.833109033818927,10.931820428191822,10.535131600502023,10.642539786953455,10.806591722606107,10.888557799805108,10.416969644763327,10.86649009983224,11.437102176348173,10.763588812758906,10.630987849467736,10.902537299578048,10.481728804594715,10.799085661185194,10.950560902613532,11.099271922956497,10.675723139415037,11.089484759529727,11.10316614993904,11.131386822378166,10.521075708675037,10.416041681575788,10.956108257353245,10.968732629502142,10.908594698007377,11.21383186129847,10.976679463857327,11.102307101621264,10.949770923024142,10.867939679517301,10.53940278714094,10.62035125971339,11.119779167779317,10.98930162564094,10.814886338329856,10.607228421306944,11.125496719348163,10.960635279170578,11.26924751868317,11.127380624297194,10.696683667247571,10.892117550468008,10.759688519532371,10.798145984283169,11.028076182307988,11.1524863023844,10.651004540161598,10.942367529494035,10.815127486194855,10.520752110257845,10.738394678133906,10.82410889377073,11.02106878775184,11.221409385430679,10.587190274268073,10.797818933055856,10.829966210797773,10.546025415269531,10.826515538062948,10.854083088102273,10.798615933108263,10.640795148881727,10.685217791014589,10.688666818542567,10.616829440381593,10.832753737932673,10.76060136416805,11.075923249063857,10.914542860854706,10.640292702435536,10.716349235602204,11.185601257246004,10.881343640068438,10.812652959467695,10.782263315647524,10.765955477712776,10.593028237501962,10.773985623236607,10.630045330940309,10.766609548270218,10.658200088754228,10.607994960666709,10.739001974382996,10.541676837515393,10.704771391700652,11.22712162753022,10.668280748548518,10.737070361537285,10.720421929870149,10.759943350708097,10.921215112463774,10.964207578602988,10.751071086400492,11.115889729664524,10.660243134306185,10.98002463355238,10.968525822090808,10.663030902735755,10.895386559118505,10.678329920825908,10.932946242515648,10.715350666801058,11.001566365598094,10.960496291349163,11.11135775214076,10.64811176060366,10.533588431378439,10.664410197176586,10.93519407590941,10.60475170119802,10.68706941056728,11.31648469961539,10.83634037270926,10.735483214914881,10.858883606290863,10.820298149257134,10.613541013162433,11.15607907776451,10.553283501082905,10.809647137210824,10.327937960555372,10.880120513416445,10.603312387849314,10.605817442670727,11.112164276066547,11.04527107410187,11.311041811950178,10.821776287072955,10.827905171621891,10.69014784459452,10.63226728572478,10.784130381163758,11.024122225238731,10.892582549964887,10.792222075639238,10.93947947922257,10.416460868359577,10.788328896136694,10.87545894023684,11.018235623113641,10.376549001881102,10.68021732183733,10.917866420301001,10.819298169173406,10.969421678813655,10.92098016491925,10.994084470441106,10.83399672164784,10.322263674703965,11.104897074458899,10.845270577171219,10.404262840448617,10.97628618381122,10.61974072181055,10.972928463903958,10.736005294543881,10.647803019670473,10.780808739711565,10.672414521272,10.678030371300068,11.134282407905264,10.742681234025316,11.144076720099788,10.76766360014283,10.923182888519593,10.705802990096727,10.356980629654874,10.873641274300434,10.875950656715467,10.758711064661833,10.722694532756806,10.731384133647687,10.932964102369375,10.687252100679688,10.026368681911944,10.810818263038772,10.80644985419895,10.82031813866275,10.704255193154744,10.772560882801168,10.743501808905625,10.894737322875738,10.551218869565592,10.67929708343066,10.954658766604101,10.531589416892908,10.902647762232577,10.828876767395542,10.715439468861323,10.788989125590403,10.900749791385406,10.435614679722034,10.482121346307313,10.767958535680487,10.870851554594283,10.567900840522974,10.643995304455911,10.717967018263598,10.729634734557317,10.73022549895797,10.574184604258482,11.146113601343142,10.610784156200493,10.990735511125187,11.180678290191572,10.596659732783579,10.706407998237976,10.711413259732158,11.147613327635833,10.759709757944163,10.47214802797307,10.616363828277068,10.813136275021739,10.723751848155539,10.852380992954295,10.685583814855978,10.700408991312528,10.956823496334602,10.474354098387241,10.812753669473318,10.841226615616153,10.745377961834032,10.575947214398955,10.880082855015793,10.842654614411254,10.984394014085305,10.813780332606648,10.635085919470326,10.514990744055563,10.327839836362775,10.482597797038709,10.692172159805137,11.019759651431075,10.822474645958026,10.943958591598234,10.820038250616141,10.79689852760344,10.621790652977191,10.775700997169356,10.78975197290331,10.900546882407832,10.759539838018519,10.580937168488774,10.70306467671192,10.816874071262893,11.191010751555998,10.892972982513328,10.78768888290167,10.83588782614335,10.825362662704183,10.533748180040883,11.005859431745387,10.240780880540958,10.818357275254836,10.665670936977497,10.904009132643543,10.181384405503108,10.874114943063258,10.772791493185947,10.576789104875367,10.392558244499089,10.596134608054392,10.817515726756024,10.598507977477754,10.774739076600005,10.630287087057917,10.689373427646196,11.165733981956047,10.679158974600682,10.880873383770094,10.624322854666243,10.478301546134208,10.77245604231587,10.8333852878165,10.499820923406714,10.406714378426788,11.08041798575018,10.980280181064312,10.912412158829376,11.16947695061237,10.704569432697642,10.200996185805645,11.276734667306584,10.7808711220948,10.378261037909617,10.76804278700223,10.414753079530504,10.911025676804842,10.691149141813103,10.706945476135939,10.915924478293796,10.453485811376591,10.694872441685067,10.625367951918946,10.798391202528636,10.010816130288653,10.70340175915424,10.888277700834976,10.487851700636917,10.747680597969852,10.536592754010393,10.651217610866365,10.962457705931794,10.544788654372462,10.80689565857927,10.815569439636228,10.424035758450241,10.832161297455611,10.814323433727319,10.680401267941642,10.571445122022414,10.562845244106652,10.720951930103388,10.74371763779732,10.867501212619292,10.568029476085739,10.845231583215277,10.916886846155988,10.716504478946458,10.776766393816992,10.702637542439142,10.508540952336965,10.683798181855538,10.576687095286378,10.992958183286955,10.448366716426971,10.46809088198259,10.359360563188138,10.709606211755235,10.781016665856948,10.886838623091364,10.73212670253323,10.736005294543881,10.647803019670473,10.780808739711565,10.672414521272,10.819198116145218,10.352395218487128,10.768000662228644,10.760134431482768,11.097606971309549,10.62490629943787,10.578827114446108,10.599779782240146,10.721437517010912,10.493660257468244,10.899236205744998,11.520417330728524,10.762721041922928,10.628181848594203,10.55708796679324,10.682651865988806,11.023371976479778,10.761258944930994,10.704995742766139,10.529506194089404,11.075923249063857,10.280347403633957,10.53294918140994,10.514420920278495,10.618665268916827,10.501609512686963,10.382512863752321,10.473138533353255,10.701377558022253,10.940383999223585,10.844724523371353,10.817255103865845,11.037676100884426,10.953084651718509,10.469142212580797,10.867234225566579,10.40683528644616,10.938112279371822,10.866566445909042,10.640699464258175,10.502021810151676,10.567643519745475,10.788824109088377,10.781785616900187,10.973100049353933,10.659773838007359,10.693216830942317,10.459181373890983,10.832181051127325,10.66417655231571,10.537468422426857,10.846069618364352,11.032418872198015,10.5287037975555,10.970110253663124,10.440828516957847,10.406079371375014,10.875326513709721,10.48203724319685,10.827865494592903,11.070287944507681,10.715173039019605,10.722518204786326,10.706295987305591,10.606684068949075,10.686315460863419,10.920003637661642,10.473704096244782,10.562715939892447,10.568158095103524,10.879423603336724,10.760452818325469,11.050429581934747,10.586685402242406,10.40289827348682,10.712504829138487,10.616290290754515,10.763313747429157,10.267852849758867,10.838227054478743,10.665647604383027,10.55643754334466,10.594757973083214,10.691990366412826,10.62154683379229,10.643184293749053,10.74834672745997,11.036791080994169,10.993193631733241,10.475681051249266,10.556489592791646,10.430019188623737,10.769284670193297,10.439512977323862,11.178459215011753,10.700746969978026,11.084401533910267,10.887773324896092,10.621254172277629,10.694147031910097,10.601821259783373,10.436260560784943,10.71814415049327,10.624833387454752,10.658905058822198,10.861054575722122,10.657400521418637,10.703356821393031,10.662562913210179,10.343804871411503,10.859383539002643,10.596759725284224,10.970798354703502,10.437551072769297,10.563103802387129,11.274046255019954,10.82903530567296,10.798023352607254,10.373741150537072,10.657259354912508,10.8652295473142,10.737417892981517,10.706318390495808,11.138319284448048,10.693897550716283,10.942190588450329,10.771679880919251,11.003099341537322,10.538661281320572,10.801492106722966,10.804745861576322,10.791893080920747,10.657706313835016,11.01690634852121,10.668862367092954,10.552055689698106,10.83484422108265,10.673850371449209,10.452908694061481,10.661673129275295,10.723553686653267,10.821057465908664,10.571701466550861,10.533109032216196,11.034825145816942,10.583321504033949,10.917068321185521,10.616584408403694,10.740908222252498,10.927250568714278,10.701355043866476,10.565814635756187,10.665040765760134,10.85180007043302,10.635398611146856,10.649796281210305,11.094451102268424,10.536964343355363,10.555422037261998,11.179785669593665,10.715084213295617,10.904027516855184,10.555734610523901,10.55708796679324,10.715927739284057,10.431848529391178,10.864005673985291,10.544867642274191,10.969611084167505,10.41379304105523,10.63979000341,10.758668544943307,10.640101227841237,10.802611779488373,10.615456487336662,10.966800761717183,10.62582939137535,10.900786679503748,10.60032790493369,10.612261988981773,10.798595505142377,10.542099346698048,10.777288232789331,10.770588040219511,10.982305213876058,10.637224700700166,10.691808539965669,10.740951503864313,10.474241084882006,10.700814552005737,10.79648918643233,10.687891253367626,10.636504274176522,10.974505940611799,10.720399840430005,10.538316823771558,10.446189678949377,10.650412438776545,10.684393747202078,10.703963310848598,10.865114872798575,10.325350806453928,10.77039894671221,10.491301994830229,11.275163077269422,10.98806852779126,10.705758160114428,10.593329276087347,10.465158370307687,10.549726546894638,10.672785260669624,10.93029946092149,11.033501604343769,10.958078289109908,10.663147865904188,10.806389047291267,10.776244282386555,10.490301522301456,10.963497603422296,10.920781320026649,10.689692377847104,10.65443183182229,10.827766295132466,10.517185599222747,10.584258462028018,10.838815913287421,10.622473030602189,10.523445569477712,10.452417882335665,10.809344036488135,10.749634751165935,10.865286879641049,11.023584060367908,10.611868113736662,10.83602557938815,10.634749065204732,10.799085661185194,10.950560902613532,11.06741930732488,10.579234218415905,10.871763339476235,10.7211285344439,10.95752079780627,10.692308483164355,10.716149601597216,10.656929888879828,10.697791425055811,11.089606928642473,10.777496892153676,10.554561956674165,10.58327083263794,10.705780575356794,10.649464346740606,10.509114135566579,10.637560722208704,10.450857233482733,11.045925320744267,10.611252372919454,10.601696898688338,10.53073528631916,10.610932037796898,10.808211648038817,10.499600568082863,10.395344401254501,10.940135781074018,10.472459435395576,10.499820923406714,10.406714378426788,10.72304709545051,10.670303323021274,10.589912187335246,10.74593796874106,11.088613872315685,10.707616917521953,10.503833902240531,10.73070660463555,10.728057654456492,10.980212041446208,10.481532475939918,10.898663399254776,10.685812511742123,10.580708582545814,10.812753669473318,10.841226615616153,10.554092509830399,10.713461756362648,10.479426532190532,10.787936678554125,10.521399202410167,10.935461338871026,10.431376761728,10.47429759323113,10.81249180235931,10.746368529984284,10.565840417922663,10.616216747823795,10.799840848027767,10.900676011066274,10.804278785363332,10.909600706707314,10.872010138213119,10.688826419085547,10.743890267377827,10.650933506503453,10.987223061973808,10.777601205511097,10.670930187673868,10.635302408736912,10.943499211400042,10.501829425822162,10.58375210726506,10.697520250869932,10.69932669131962,10.623154942905469,10.940756210963185,10.552029549665953,10.546971688076972,10.661743404167277,10.935300989665748,10.641560296449066,10.767495026486278,10.390071711929085,10.493327663230145,10.90159787403211,10.54157118232102,10.582789326274021,10.335237500902117,10.528195279873552,10.527606146685637,10.678859673351743,10.586533890916645,10.811181437184764,10.79718496675754,10.620937025619039,10.621912540280341,10.705646076365333,10.796407298087043,10.993630746112858,11.004696467051504,10.822135503983962,10.663966225256358,10.903365472216551,10.486373338838536,10.436260560784943,10.576636086589383,10.543840312582256,10.705399447887462,10.614351853901232,10.576789104875367,10.566999927966382,10.690102307253893,10.712482564117947,10.238315581044851,10.604578100850384,10.694985739443027,10.784337617870264,10.800921609559978,10.276808185095502,10.70333435175513,10.541333417310984,10.579564868400478,10.58240902583209,10.785331756675916,10.577630287168375,10.603759293038369,10.609847064568209,10.489494857538169,10.459066632489291,10.446944922115469,10.526426838052577,10.493216773897585,10.578394384806286,10.921883507347436,10.293974377463579,10.75934864358382,10.467408346336265,10.611055255757304,10.659867714887898,10.712215345197256,10.637800668461894,10.753788043370438,10.622716624094574,10.695574680950976,10.828519964347038,10.498222246109226,10.767368577592539,10.479819978504239,10.813558984596366,10.454408506866061,10.640364495957398,10.5950334517291,11.008777495957478,10.75404438242296,10.737070361537285,10.59018900394601,10.800860465555639,10.675353487807463,10.670814131270324,10.525004458144746,10.552630597598018,10.813156408101396,10.833838968058616,10.613835940415848,10.640914741787618,10.63436394990608,10.751178192918026,10.531082364855838,10.492578921497184,10.353830419422378,10.938822746356111,10.399859219331969,10.778789609332929,10.689874589440821,10.407167708141248,10.72753140789784,10.659679952313123,10.357933282865915,10.73059728275904,10.796857601025716,10.461416203770762,10.336211084415119,11.097273648073832,10.677431002924163,10.895405102533275,10.622010039427302,10.598582834314088,10.730575416949513,10.846945880481194,10.80553736211994,10.459926872262475,10.304442505166406,10.734046088919033,10.694509802574999,10.773734345908876,10.513090067385729,10.990566925390514,10.35951902421498,10.514719439894806,10.77356679260559,10.79216039737361,10.664760562143673,10.681710905451192,10.5368847286903,10.623787731088578,10.330746767679962,10.700454061735071,10.72849598180637,10.522180547171125,10.888259024780478,10.446480224596142,10.509632446974212,10.637128673812564,10.615873475949103,10.897072603336532,10.448076718454924,10.77653669837126,10.728758886023115,10.598957034465641,10.527472204361002,10.603858578185394,10.465101343134224,10.512083962693172,11.446764294716028,10.746433098184468,10.485116408097518,10.787750837571522,10.718210566991154,10.72260637265801,10.587038839422627,10.595809392596285,10.669954895008782,11.025018523586803,10.596459717781787,10.749012413516956,10.389149202638569,11.142832326942536,11.033049261848173,10.581724120360319,10.646257883569398,10.772435072899762,10.727575272356669,10.789545855333118,10.688689620179726,10.746497662215868,11.096955372216916,11.046579139627841,10.918174606266476,10.749613297693154,10.797082676478094,10.775512868112267,10.955567127076021,10.46490172241293,11.142788889915359,10.626314887197484,10.513742135006508,10.687092248656647,10.606387024538751,10.840345325350247,10.889155082188104,10.610562292793487,10.6033620538455,10.320321127381453,10.606857304116247,10.782284079982702,10.706228774723371,10.572956605741496,10.809909750211677,10.581952474309931,10.623130596900038,10.543471269980007,10.559815134957537,11.034631566206722,10.598807371207691,10.703356821393031,10.724896013040084,10.470788023230098,10.85180007043302,10.635398611146856,10.649796281210305,10.630649611683351,10.88809092459237,10.465044312708477,10.798656787788172,10.603188212065916,10.9995298750016,10.655351654054858,10.71541726908554,10.552499965731496,10.693829499587176,10.868168368558376,10.683729439947006,10.848540653077935,10.598408159645215,10.737917257929963,11.04879256919622,10.607451025529922,10.79335217017376,10.518781293891209,10.60777247750653,10.790699566909616,10.714128838127134,10.752997250719933,10.859594973780608,10.721459583541503,10.55807580091745,10.933089112414988,10.803770846264467,10.755730309601852,10.487154632477253,10.72487402221026,10.63739272556824,10.4809151919697,10.509796068463533,10.537043951682437,10.686498288754322,10.929403692471466,10.506737377491612,10.682215921186279,10.802469345287646,10.531856183153893,10.726038870307335,10.41849442269534,10.750363895525926,10.643756840164809,10.105325748023002,10.681251578815953,10.499738295850376,10.668234204447975,10.57413346774956,10.819598268208338,10.403929451547379,10.543523998690803,10.451233167901064,10.538714264260078,10.802469345287646,10.551192707649491,10.644209873708961,10.632797892075562,10.612434260629977,10.889341659795601,10.754407416968615,10.650838787109585,10.716837062123032,10.467066903737985,10.700499130126362,10.71843192346452,10.85997928615443,10.531802835594531,10.875099455998244,10.741146247938758,10.60080104196549,10.573468455064233,10.77534561256631,10.833207704721945,10.709650869564777,10.968318971901319,10.704008221364402,10.622131899994592,10.79614111464413,10.646876224532782,10.780683963269196,10.40486871747412,10.665367570777166,10.728254925540478,11.647884587902611,10.419778215733176,10.428452739855837,10.601049971569482,10.732214027337896,10.779206258645235,10.794788627706676,10.727487541514835,10.347339693048996,10.935479153862342,10.714506653690963,10.619374220065563,10.592049235754445,10.406563222842058,10.616682428399852,10.900602225303203,10.63532646020706,10.500976992899632,10.486010387763148,10.72260637265801,10.554822665281634,10.688165050941665,10.954588858533185,10.79728724657475,10.769663242978435,10.886988234103013,10.464416763268364,10.505067539570582,10.726521993930495,10.520994818887328,10.83539569530536,10.766989134947066,10.554640176393397,10.665134149520766,12.055633403123775,10.89777582523201,10.641512491874158,10.917231620558995,10.858113990675855,10.510641019929098,10.581571855419028,10.499738295850376,10.89777582523201,10.80636877750035,10.859056688207119,11.044871933048107,10.575155701418948,10.89829367247865,10.924966785274414,11.305384556883427,10.600676553922405,10.842654614411254,10.984394014085305,10.813780332606648,10.59109441383156,10.499986158040269,10.897313234903,10.583828076826626,10.76494187850445,10.581089530093944,10.63113277350364,10.620692998189144,10.476442547767668,10.670512321570657,10.54265361922956,10.867710938165587,10.645067690617664,10.383008250473704,10.577375458157261,10.754877030826584,10.75809435172215,11.00990265326726,10.53762755251604,10.496234118987427,10.769495006100515,10.525595125616142,10.581571855419028,10.822075643458966,10.473081959467745,10.739998875403943,10.574772486238938,10.582003212551355,10.78097508408639,10.692217602989803,10.545025599362843,10.56954612740534,10.924534617586627,10.54368216814334,10.518781293891209,10.954431547502736,10.794624565526743,10.662328836291437,10.46638366859312,10.767853211545363,10.791234766593037,10.594933286456316,10.583625478502434,10.634412097430104,10.727553340367766,10.914233553427952,10.572956605741496,10.578572590277664,10.716548829761411,10.53390790318777,11.071252699892554,10.609699022425275,10.731253034820835,10.752804801157161,10.621571218386105,10.997305031119303,10.945705841008074,10.757455972332892,10.584941634505027,10.592902778006396,10.340871136212566,10.579793715900047,10.650199196425806,10.84957006921802,10.588098402073786,10.6896240399389,11.051778499434786,10.433409671993108,10.519888668850758,10.687183595798688,10.913560024017496,10.763186768676764,10.637416726816307,11.242192278563087,10.61890979160975,10.936583063952368,10.795915827145608,10.840913356940241,10.777914080311584,10.485395862604143,10.733217714882608,10.456596502556854,10.915924478293796,10.453485811376591,10.694872441685067,10.450220714640537,10.609600315486096,10.890068980025717,10.611252372919454,10.633183610843151,10.565273056653059,10.462474571409137,10.836576402686164,10.481644668462405,10.64182318076953,10.593630224075774,10.598882205636553,10.912995366121416,10.56431813161953,10.532042877202896,10.547050503740312,10.908594698007377,10.587795784428868,10.510504785715026,10.801695776859518,10.97375180568875,10.61021707406934,10.684966071886038,10.758434654169232,10.453745405545833,10.916033472099423,10.685034728841586,10.59518368082876,10.896831913852575,10.6633817512079,10.480662556843653,10.900842009130011,10.704928442731342,10.886483207204273,10.998560250905705,10.644686529501012,10.403959764222627,10.727333994019004,10.579234218415905,10.871763339476235,10.7211285344439,10.95752079780627,10.692308483164355,10.716149601597216,10.656929888879828,10.697791425055811,11.089606928642473,10.826515538062948,10.514448062108126,10.738112593745406,10.756455024543515,11.002083174398681,10.454754298299642,10.587139798534272,10.673456875697358,10.549438298265098,10.652305930466534,10.465357939808428,10.430727717570214,10.574772486238938,10.64965403707171,10.730444212051008,10.716992229759807,10.74019380506744,10.92676547631263,10.869311029940775,10.838757043008064,10.524144682170881,10.556333436322548,11.348675626548836,10.611498714744615,10.687137923270706,10.732781452769414,10.766862622063668,10.691808539965669,10.644543556617958,10.88921105912562,10.905478802599813,10.581850990103325,10.5521079677126,10.572162721171585,10.698627082846134,10.918500817327924,11.01290788992083,10.867482144479293,10.612581898425521,10.71143554857325,10.737483041683452,10.707281253183137,10.441062209594671,10.856746462510271,10.69430576026952,10.480746775644146,10.78702779414709,10.728320673921449,10.594281967512476,10.732541427456502,10.814162545624647,10.549726546894638,10.936600858971541,10.458320492295115,10.514420920278495,10.701219948286148,10.934088630587693,10.830104782127586,10.368698465041247,10.833503659028759,10.931534305156966,10.627188186139529,10.636936592369441,10.595834412925305,10.777309100685118,10.585396823669269,10.682651865988806,10.754770319768017,10.477034422194833,10.571163067122404,10.484976651553191,10.65605863433599,10.972121617684552,10.74714307336516,10.709271214599578,10.925974450814746,10.567463355795793,10.61771105869799,10.840541234762362,10.63262909331945,10.437492449249524,10.533748180040883,10.657000497882507,10.934659335602204,10.48475300044798,10.441295847632006,10.82319244951007,10.71931685969625,10.649962207136612,10.50525930200491,10.55437942019896,10.83963973350584,10.801899405522992,10.646210303039341,10.723245357355136,10.670837343628586,10.63494156725066,10.465528967686389,10.459554192547706,10.721503715141942,10.611769620680343,10.961434084478222,10.814363651708785,10.843690104456597,10.461358962786202,11.198392786467558,10.688917607960567,10.526641361275539,10.79176967999097,10.541174875891706,10.71205943451149,10.97942810193982,10.578165216812412,10.679504210918369,10.494075844768336,10.850210491530484,10.54867797155018,10.634460242636054,10.544156526450868,10.840972100417284,10.630891221774164,10.342258479350765,10.666207436448033,11.391559769244576,10.574465808325012,10.912229836775195,10.59297805559253,10.627042689267455,10.421328511196023,10.637944608583052,10.730422342894173,10.37311611145178,10.895905644797834,12.613755293079292,10.635013745965189,10.691603945686776,10.545920218551572,10.690648618528321,10.792612616337514,10.489689629308009,10.858248716172861,10.777726367178413,10.662796935349743,10.700454061735071,10.861745223231589,10.459697547336718,10.843475279586862,10.546340939041606,10.58119109160222,10.564059887163895,10.431376761728,10.64413835574004,10.881964039964258,10.646686006494784,10.491635263364433,10.553335714950922,10.951069670091458,10.635206197071174,10.565659928796643,10.995612175068683,10.789504626720456,10.518132504941116,10.784669107296715,10.634099097078431,11.735428811397014,10.52567564415558,10.546997960654972,10.540355344564857,10.624711855667964,11.037788683612744,10.578903459065758,10.448656630324574,10.676069563742107,10.603113699193782,10.686978052993675,10.78529035395161,10.583093462529407,10.543919375424078,10.389733557327729,10.641560296449066,10.795075671769911,10.455733391852487,10.763102107216726,10.94755565435211,10.716659698193956,10.68228476721217,10.623666072147104,11.512375313664748,10.757285668979632,10.627891122746627,10.73299960761659,10.723443579959769,11.428249540505234,10.547602039518763,10.636816522728905,10.606733567773487,10.417747273036401,10.59593448798168,10.87526975411497,10.481392217583796,10.676415868100923,10.731165626053679,10.502763517486002,10.474015019548162,10.924624667924826,10.52169564643158,10.682697743861915,10.68207821491354,10.897017064751084,10.477823043556645,10.430993286553317,10.667745360554026,10.382574800514906,10.948699064477122,10.672229100017557,10.654030618737362,10.485116408097518,10.535556883587484,10.567437615438774,10.39372263868611,10.835179080986306,10.818917914398128,10.928202103359991,10.725731306430482,10.623398370365289,10.760240571694087,10.7145733122105,10.942827429739166,10.369389029448124,10.64435289430417,10.960392037804448,10.520158574385459,10.627163938130897,10.757604963978993,10.486568719482518,10.947062705274329,10.963705453216926,10.834233305379868,10.614499208879641,10.425846412115792,10.738654993116501,10.573058996567367,10.97162345144133,11.094314325192048,10.861227282322822,10.732432305993294,10.477485139124067,10.571880868629844,10.777788942138022,10.621059017006598,10.768421830133452,10.614744752268392,10.843494811027599,10.96240568266004,10.485228199271722,10.550119479354604,10.668397099322965,10.448743588106625,10.78236713301211,10.812552239318544,10.664410197176586,10.698175462651035,10.842654614411254,10.984394014085305,10.813780332606648,11.263014337316546,10.43323306115463,10.579234218415905,10.85680428324673,10.765575498395966,10.437756228028585,10.640890824350612,10.91129947687774,10.748926543438332,10.632846115058646,10.581140312137425,10.809667340659555,10.673711508275499,10.374990057905599,10.85180007043302,10.635398611146856,10.649796281210305,10.57262376313457,10.616339316370409,10.699665035915537,10.49213495800589,10.78622150088144,10.534333706898694,10.81237091748186,10.817736200776059,10.736005294543881,10.647803019670473,10.780808739711565,10.672414521272,10.600552050380118,10.595058491479705,10.705085469100878,10.79890188082263,10.527070269710164,10.63291844517332,10.546025415269531,10.652636923211357,10.614548322380951,10.653936192260108,10.795465099828,10.632219034820066,10.65845863548799,10.412561643263313,10.684073102244907,10.676992775661722,10.617760014711022,10.87583720514026,10.593203854356613,10.736048788878751,10.664503639837902,10.693262226679666,10.573084592635812,10.460499954601437,10.562586618956502,10.586533890916645,10.584840453213362,10.476442547767668,10.531215824531195,10.924084244219499,10.652731472447943,10.614769303291556,10.506737377491612,10.767305347149167,10.815006919531392,10.514040857292054,10.532549442567325,10.68317933449626,10.577375458157261,10.665367570777166,10.712727452082927,10.565943539941884,10.600701452770835,10.912557992542743,10.50613546228876,10.568646696555904,10.799636799708416,10.670721276448772,10.66555426856067,10.709606211755235,10.809626933353908,10.731711805541833,10.838423379279122,10.706318390495808,10.736787903279478,10.72823300845282,10.600527147811418,10.734307538221145,10.759433623401165,10.533881284434855,10.702210225644713,10.600078795498629,10.876347635898178,10.521399202410167,10.536035110967143,10.684576926741435,10.58582653437947,10.66993166215753,10.598582834314088,11.02724763473689,10.79170797381519,10.60172177214463,10.797389515931872,10.619667432206645,10.666697032541045,10.836281356509298,11.094207930086123,10.591119552407964,10.485479683729912,10.682032308608301,10.939532708935408,10.462074239700378,10.913487182847634,10.774864596986772,10.794542524342022,10.658059035083072,10.629295515335622,11.017694280077595,10.60512360049198,10.66068876188618,10.649630327748017,10.521372248595526,10.73223585734761,10.755879558560052,10.690716886457212,10.733893545253114,10.556593683558889,10.587240747454205,10.763038606417654,10.604181186851473,10.795424114541712,10.9897741915136,10.50783084142058,10.742097784525766,10.64273079523902,10.824845424743302,10.51528909364212,10.621790652977191,10.395955704265866,11.262333632696789,10.693443789024133,10.739045338577187,10.678675443432283,10.639191222509986,10.560463365957897,10.885790718803854,10.663732476628567,10.874114943063258,10.654997976392988,10.804705254912761,10.621302955145095,10.55643754334466,10.85156760689969,10.606436538068333,10.575640896591837,10.463817371205208,10.727750710953611,10.568415283521176,10.505012743548761,10.695959570639554,10.757030159556333,10.911062187812915,10.73219219685162,10.559036702680755,10.55812776516606,10.580073347296848,10.806206604380188,10.57052173723882,10.60142324982787,10.546971688076972,10.587821006063988,10.603883397931984,10.719294745831961,10.836812376966062,10.940791652475832,10.690125076183412,10.756753283988832,10.7350479402497,10.785890525742927,10.619789578562562,10.82889658605481,10.461072708705126,10.516454515968546,10.755879558560052,10.755879558560052,10.634676867382668,10.564602123514762,10.864847247777861,10.751692144575056,10.94169498690382,10.775972676672808,10.78766823049205,10.838109241095006,10.873773924171296,10.655893716970995,10.638352326447942,10.745679542983188,10.917032028814173,10.675977195655216,11.02934204634797,10.636624381312231,10.621912540280341,10.640436284325322,10.658341122532052,10.696615805459388,10.32855919028321,10.757881603870102,10.584992221312,10.767621459392718,10.685675299886803,11.039235047866498,10.753467527122861,10.542785543610696,10.613934230174134,10.814645132298535,10.90025166856016,10.586104484122892,10.699304130942409,10.837067952947244,10.670558759761432,10.835159386448586,10.784399780508467,10.904854456765403,10.876196424315083,10.626314887197484,10.557165989185707,10.644710356327636,10.769684270598214,10.87640433434749,10.917304189499522,10.877971717988014,10.639430777896337,10.498222246109226,11.1321773593989,10.78768888290167,10.628714626559486,10.727553340367766,11.021248660042998,10.816472827401556,10.846478636240239,10.909436156340819,10.692035817859326,10.66967606516289,10.657024033108858,10.750663976978858,10.881813675329736,10.41081707204541,10.676923564324877,11.020528976672605,10.658740610253117,10.826018771999738,10.905001396740687,10.729240697644094,10.576176891193677,10.763673433025511,10.523337970284603,10.696185907157652,10.521237468623626,10.574721379784181,10.807158995053905,10.752291421180539,10.50353211483375,10.925596695218122,10.771281077324733,10.80608495727828,10.645924772307156,10.764011842504205,10.58162261297557,10.66969930395308,10.716593178609457,10.906707991398342,10.589156843240115,10.57773220059301,10.65683573578683,10.776181610692205,10.501801939324901,10.864005673985291,10.586735900916826,10.734873777319839,10.742832443158637,10.88264040116691,10.68354610508537,11.07511793394081,10.73055355066186,10.684050195099022,10.7487333087972,10.690284444175827,10.746153272535546,10.945705841008074,10.757455972332892,10.712571621225875,10.64616272024527,10.693398401528382,10.8383841174024,10.63964632868932,10.736048788878751,10.927448131508458,10.594833111149445,10.928847912796902,10.560307828836057,10.843436215560919,10.821536737425147,10.733174097234901,10.696050111394271,11.272597605568452,10.543418538488748,10.750449642272962,10.666720340662762,10.748217833797062,10.649250902099034,10.725775249919163,10.863909995770191,10.667093196744634,10.70465919729006,10.560281903630274,10.519942655785933,10.711546985327436,10.788535264670351,10.673086385256404,10.698017347384676,11.019333812850217,10.858075494342627,10.731733646517688,10.578216147572055,10.940490359572546,10.715350666801058,10.489355711615616,10.748604464955758,10.566639335560673,10.967232305875163,10.863737751910739,10.736983459801367,10.541676837515393,10.704771391700652,10.894310452294558,10.812753669473318,10.670280098263682,10.546603799490509,10.929493305433144,10.646995092435022,10.830203749893865,10.542442504012646,10.652566005416872,10.800534301043522,10.57026509007593,10.5798445637886,10.760389149066027,10.776181610692205,10.53126920341452,10.486205839326685,10.791419961305229,10.662445881599808,10.617245857000183,10.753745313805846,10.554222933839034,10.41057620250521,10.836478063632697,10.72176846385284,10.438986276507002,10.69869480828722,10.571803985965566,10.960878461384734,10.550774023880454,10.603659998032827,10.770693076719791,10.765533269557887,10.605817442670727,10.734285753389923,10.667954894342117,10.929815845619073,10.688142237340195,10.541940926673426,10.838639292051202,10.749613297693154,10.622740980180552,11.030509115677916,10.567669254803059,10.706788741587966,10.689532915462804,10.813860810646245,10.80616605699042,10.808130714060667,10.705982289931356,10.63233965771685,10.812894646443958,10.791851948969441,10.622911456174293,10.814886338329856,10.900380835342334,10.632460266065506,11.173023353045823,10.762805735649291,11.068121636746236,10.768990125578178,10.666137474577225,10.768337610741888,10.75042820627549,10.609699022425275,10.840658761989639,10.909783508696709,12.009753579092365,10.947344420215888,10.579234218415905,10.871763339476235,10.7211285344439,10.95752079780627,10.692308483164355,10.716149601597216,10.656929888879828,10.697791425055811,11.089606928642473,10.892768489237657,10.730444212051008,10.584941634505027,10.535131600502023,10.733392166450933,10.782201020054917,10.878254718169137,10.81935819618558,10.737048636811288,10.66237565605875,10.727246242006135,10.503998475174141,10.622156270326151,10.733174097234901,10.603262719386294,10.599480679545993,10.48475300044798,10.987781149608049,10.480185182952555,10.601547644956717,10.8654015344347,10.82970881308719,10.786676412905166,10.487349860546091,10.617735537004092,10.536698936485076,10.96737036068314,10.660008513686648,10.72276064773077,10.89129862581914,10.579234218415905,10.871763339476235,10.7211285344439,10.95752079780627,10.692308483164355,10.716149601597216,10.656929888879828,10.697791425055811,11.089606928642473,10.609501598802897,10.535955422284223,10.774236837439904,10.617147892218444,10.805719927159243,10.683225188177172,10.5506169722625,10.868911246960494,10.805435922694407,10.80948549492485,11.534471669391213,10.67435937150647,10.728101495838379,10.712861002064205,10.83634037270926,10.59823345445977,10.746303957614778,10.644567386851376,10.60012862235033,10.764328997415893,10.651004540161598,10.812652959467695,10.720002147046358,10.857882990443828,10.715306262813572,10.71205943451149,10.60129883922295,10.626193535337618,10.739175419878183,10.816553089054588,10.751970424805041,10.559270295995857,10.78529035395161,10.761407371083953,10.898423092400252,10.650033309820769,10.704928442731342,10.580810182749103,10.571163067122404,10.589836678595073,10.768295498386117,10.584385010667155,10.835179080986306,10.533242221705077,10.538131297472674,10.879969871304157,10.515993929932415,10.616510887100864,10.61469564841373,10.745787228498514,10.679550233423381,10.733479380823917,10.759412379123841,10.555786696570062,10.739522220644622,10.831528973842945,10.6926264987498,10.661837096341706,10.640125164170602,10.766314214540959,10.960305151547193,10.90632288581047,10.78236713301211,10.741254422706016,10.780413560888006,10.89642446116701,10.556593683558889,10.79368068528841,10.763736893526659,10.539641011575952,10.691058156211511,10.72026729354135,10.733740978314072,10.943322470501737,10.664924023794766,10.673063225045645,10.88756776544664,10.697926984577945,10.622448667989053,10.742702836729976,10.836792714569413,10.50810402068251,10.631857078805835,10.799575577092764,10.663311591360353,10.645900974398991,10.786511014294137,10.817575860855083,10.60286528284671,10.695529390070288,10.70342422727759,10.607253157556682,10.652731472447943,10.55448373083613,10.650222892266003,10.950613545737037,10.834509249010278,10.603237884229646,10.579234218415905,10.871763339476235,10.7211285344439,10.95752079780627,10.692308483164355,10.716149601597216,10.656929888879828,10.697791425055811,11.089606928642473,11.354539160871298,10.727224302799675,10.725093908749692,10.598433115037453,10.910678755725908,10.856457308668775,11.172194171428632,10.859806363863356,10.672901088549523,10.639885775090388,11.020348974872102,10.754151170971056,11.09816730995047,10.720686965099299,10.625270779632405,10.80088084730582,10.610414356504446,10.658787598318158,10.75064254557542,10.676369701114927,10.590289645536233,10.857959996450335,10.746755876664402,11.288368415137512,10.813438228664085,10.733501183228723,10.82589951141522,10.600278088010873,10.579234218415905,10.871763339476235,10.7211285344439,10.95752079780627,10.692308483164355,10.716149601597216,10.656929888879828,10.697791425055811,11.089606928642473,10.804867671674529,10.511975133962281,10.804786466591047,10.769579128077432,10.769221560793131,10.534333706898694,10.65681219612839,10.90744111582406,10.907129603613011,10.697701041830877,11.055340405097962,10.985936583361818,10.989521058997378,10.579234218415905,10.871763339476235,10.7211285344439,10.95752079780627,10.692308483164355,10.716149601597216,10.656929888879828,10.697791425055811,11.089606928642473,10.84819079884696,10.568903759357763,10.813277198067922,10.973511734352114,10.640531994133257,10.11880052473515,10.669234425510417,10.85450815959797,10.714262201096881,10.611375551417572,10.637872641112319,10.776954287219356,10.746734361340112,10.8308171315255,10.715306262813572,10.825481987326961,10.687754326463557,10.601473009736322,10.67183496565901,10.843748685048862,10.749849260583721,10.761258944930994,10.622473030602189,10.59089328246696,10.709405226928913,10.954011930397183,10.702367679393,10.708064294780282,10.925074798020022,10.812834230175852,11.01892418159454,10.77680815095747,11.385932649185289,10.733980715911525,10.56954612740534,10.616755937092288,10.72601690459581,10.502324053624832,10.847082118937628,10.523902736929974,10.894774433446688,10.541439097628123,10.769095330043152,10.78174406709235,10.597958856058204,10.504848337465365,10.692081267240086,10.819378204388943,10.554275098679943,10.690807903113322,10.641297343002263,10.947802037796388,11.038447842325047,10.664106448211086,10.480466018721645,10.674937466353247,10.575283407185038,10.689350641595816,10.78174406709235,10.935336625044556,10.830025600861832,10.888725821536315,10.75122103231314,10.72141544999338,10.911025676804842,10.650436129564383,10.591471426139194,10.71778985465254,10.682628926262934,10.723773863676481,10.616853940277469,10.54886155162439,10.48668034842802,10.691399309540497,10.651383301144275,10.71172525830841,10.629658399543255,10.751692144575056,11.07095714794715,10.725027947864472,10.877783006696857,10.55708796679324,10.776996036514841,10.718011304262587,10.911938052328884,10.818197034893952,10.666510548007066,10.714262201096881,10.662001036527325,10.628399837526073,10.725115894744613,11.071346013941053,10.985140168879203,10.963255057380671,10.806287694227784,10.72566538757657,10.711814382882341,10.985936583361818,10.805801056479424,10.550747850323598,10.67271575750141,10.811141091014619,10.528195279873552,10.788411448660783,11.038962005936805,10.704255193154744,10.749548934513161,10.683569023781297,10.710722059133841,10.539641011575952,10.857305256301004,11.13642675065466,11.029147402302653,11.00033161214159,10.735722535246286,11.12043087483045,11.811243276893372,10.845796846808836,11.05128675205612,11.862758053293279,10.686818157154052,10.67505304523018,10.553805517120653,10.619936134498339,10.648088014684989,10.76905324958531,10.993664362383136,10.705018175104598,10.858614308195481,10.835080604418726,10.65946867726744,10.671023023099933,11.217023031071593,10.66958310460134,10.544235564296866,10.74714307336516,10.665624271244136,10.601149526063207,10.744709851161437,10.818737743235035,10.772078525532862,10.847218338835674,10.976542688339931,10.926891263606484,10.711836662784757,10.32200049949355,10.873849716198011,10.626096443245693,10.695642613426124,10.650009609487778,10.798472928582948,10.822175409010004,10.645543937798948,10.681917533624532,10.720797375716495,10.539693942633264,10.655445946975886,10.536937805837946,10.970798354703502,10.437551072769297,10.563103802387129,11.274046255019954,10.82903530567296,10.77958109465887,10.753467527122861,10.794050135837551,10.620424499218812,10.554796597479278,10.556359464094182,10.821257190289682,10.579208779272696,11.123786359460837,10.540302448505601,10.958252441423962,10.568158095103524,10.568235258574376,10.840325732297943,10.8590374583624,10.70645279909816,10.717125211430696,10.692331201917552,10.640747307714394,10.835966544606807,10.736005294543881,10.647803019670473,10.780808739711565,10.672414521272,10.706004700150416,10.784648392426545,10.630770424025688,10.67837599740519,10.627576074335622,10.595484071338678,10.959540226785442,10.648562825956432,10.58215541183124,10.826475805858005,11.259928192930293,10.891708171973269,11.009753808057733,10.670001359092055,10.45152225208439,10.716748384090739,10.770335907596417,10.72856171434071,10.673989215342615,10.641942650800615,10.619252022961483,10.768063848723605,10.373022321884237,11.215718171293377,10.695642613426124,10.914488284142575,10.878537638283815,10.5287037975555,10.683385659504728,10.718210566991154,11.205598352804692,10.730006738019052,10.698220633849886,10.811524313923938,10.726565902688105,10.685652429413727,10.928560937869367,11.204482706430472,10.74776657509999,10.885097750530926,10.686635387740004,10.767452878631598,10.588174042178206,10.804217846292227,11.160185625484944,10.350446429473651,10.959488051511292,10.616878439573116,10.705063038271945,10.637656707618994,10.751692144575056,10.838168149521874,10.859806363863356,10.599854543937271,10.78551804772517,10.838443009639438,10.705937467986523,10.96737036068314,10.84786026853724,10.821716405040542,10.920618599336354,10.790370070829697,10.697768830015422,11.06255189911277,10.708779682349634,10.86047867153666,10.94600556684933,10.799902054405491,10.59905679752845,10.738654993116501,10.49005124769329,10.80559822083645,10.729437735508842,10.633328217032549,10.73950054911992,10.75630586145471,10.540910584323711,10.79673481124167,10.721680222070297,10.930263645585358,10.744451107790292,10.579234218415905,10.871763339476235,10.7211285344439,10.95752079780627,10.692308483164355,10.716149601597216,10.656929888879828,10.697791425055811,11.089606928642473,11.459925451808523,10.46501579627588,10.697633249050782,10.761216533412018,10.94358757013657,10.642444269127367,10.687640206386288,10.730466080729594,10.8007789344005,10.561913880367685,10.785207543360087,10.828738025781755,10.872598412593655,10.684118914962527,10.76164056768034,10.815308308938832,11.244209068361261,10.620448911195329,10.782491699624266,10.667582359470872,10.739977214206728,10.85657298023876,10.988879503033383,10.657847417264062,10.73103449857573,10.623666072147104,10.64974886874556,10.706318390495808,10.778039202827545,10.797757599041015,10.728254925540478,10.767747876315898,10.681205634546343,11.099468506932512,10.63057711727143,10.678974799818294,11.143208702164118,10.847801928316501,10.887399549007759,11.372237093592211,10.868149313135678,10.605371456538457,10.736222747303128,10.607698305452052,11.114013835831907,10.72515986528436,10.905185041352151,10.736461890735974,10.995830228190643,10.650175500024103,10.571060481976643,10.844724523371353,10.769768376656003,10.739132061324618,10.749634751165935,10.819598268208338,10.926657646037379,10.821556702087694,11.139496670061519,11.185712231181116,10.84964771801256,10.751199612844985,10.656906351437641,10.864082209966808,10.586079219156558,10.732650537013516,10.673942936186739,10.62493060225092,11.232523494815737,10.714395546283317,11.046897920612066,10.71083357542091,10.619984981704288,10.752954487351028,10.721106460606913,10.874361162180575,10.69932669131962,10.61589799927692,10.810475144084139,11.167388265441952,10.95729422815692,10.696118011581023,10.717324650785175,10.760283024624407,10.93029946092149,10.8092429824949,10.771931674953063,10.563956570705491,10.651690938844151,10.756902380358612,11.104536085344817,10.668210931585294,10.744019720009131,10.586786397041259,10.77545015056074,10.667838492102405,10.87420964989832,10.882922083374908,10.75856223773664,10.84885153189599,10.867043476877397,10.924552628303003,10.806105232822933,10.659351282951539,10.853038964104712,10.829193818819975,10.818076837770526,10.74073507706983,10.650199196425806,10.919551218569078,10.561551448966803,11.004995644316264,11.235140916696839,10.764815106334996,10.766778271248578,10.839345589902813,11.128262484491326,10.847879714521158,10.66082944513807,10.674289977661678,10.85680428324673,10.684599821824717,11.142644086196546,10.770882114622454,11.006772241852998,10.722782685084084,10.989841682697591,10.794624565526743,11.08357229553351,10.726653714419808,10.77949780990826,10.819778284410283,10.733479380823917,10.739955552540295,10.65301506653218,10.637800668461894,10.714106609236245,10.97913822956689,10.568158095103524,11.042281630837069,10.779934977485716,10.913578233480955,10.786821114252175,10.82838117321755,10.586382356631722,10.52320345501019,10.824984707437652,10.797880263309066,10.696253798124786,10.731165626053679,10.961052126766715,10.914451898012965,10.63110862095615,10.833148503348454,10.792961918250924,11.070988262792044,10.709561551951284,11.128144948054898,10.932517510305933,10.81865765674158,10.893363262683687,10.794727107543425,10.726895156930228,10.57262376313457,10.616339316370409,10.772833416633738,10.617098906228428,10.836714061116485,10.763800350000826,10.664853972073217,10.70604951908194,10.822255214285176,11.001799796195236,10.834134735626902,10.661626276603513,10.754407416968615,10.92958291036506,10.706273583613463,10.720333569181761,10.77105011831893,10.537839686585567,10.791111284394898,10.745528763777509,11.443060784997243,11.020594423840402,10.759709757944163,10.966317211064466,10.995779912459419,11.203025049729737,10.817575860855083,10.65024658754472,10.952611933668509,10.804725558450654,10.855647232824525,10.625367951918946,10.890572199710363,10.843592462509537,10.777559481473872,10.66953662107974,10.689282280329282,10.74183836432845,10.588224465736102,10.682674805188459,10.62815762466823,10.784482658015559,10.796837137108716,10.88807224504927,10.699710139880182,10.825203541055348,10.893790537697386,11.03180426391057,10.752120235936289,10.904229720879732,11.313327527231033,10.789525241239263,10.881155564085187,10.945600033964753,10.735156776679537,10.745054738214346,10.816813894946268,10.632870225678168,10.865955514028034,10.63686455231514,11.113641215937145,10.612877108641937,10.743393876988973,10.875988471047103,10.761619370236751,10.884648000696686,10.64225320609987,10.91637854079876,11.0271826215717,11.188192057894385,10.77482275860842,11.000965865163035,11.092534518675446,10.763525342859484,10.625853671765293,10.940862531733048,11.071283805542897,10.63592755903378,10.691967639914864,10.890162187963373,10.791193607554506,10.803567598362301,10.814202770077097,11.052555284692732,10.790328876184995,10.845387549916703,10.925596695218122,10.700882129466427,10.988440306418273,10.787564962045632,10.671626243386426,10.880986265451398,10.750406769818508,10.859268192096696,10.898996036516913,11.489308773369231,10.850171689730077,11.374938446485308,10.678767562634595,10.682881234309459,10.818197034893952,10.666510548007066,10.798370769971397,10.890683991926014,11.09922655193496,10.675746238104187,10.865917318389972,10.796182070555096,11.059157324024897,11.024171134959547,10.723817893264371,10.777079529877168,11.16704914827372,10.927555876583714,10.8766122011623,10.78128690522831,11.001132707014031,10.921450004820915,10.674914348974756,10.869672600684126,11.063085182267388,10.796980375734279,10.675907913990581,10.778226857252047,10.691603945686776,11.022963996383547,10.864541302883799,10.496593378915847,11.580210211775825,10.797962031129387,11.042329660423304,10.913996959649264,10.858748966308355,10.697022907127343,10.85622592538133,10.809889551659912,11.08417125888411,10.937472427226925,10.62927131837234,10.945494215725116,10.8830722814489,10.82117730532399,10.677684625696235,10.85013288642403,10.829966210797773,10.726917103358996,10.782097185442595,10.832279813633209,10.722407984014007,10.846498109109664,10.876914475781092,10.73754818614131,10.973117206279754,10.844412358701955,11.007982504362394,10.837028637816811,11.032289512367296,11.169702493325477,10.76195847542619,10.657894447316275,10.946921818036719,10.78773018644139,11.082557847244853,10.830183957124165,10.729569072519801,10.913523604095793,10.915978976681567,11.214492474614303,10.816994413033667,11.055324602441535,11.041608974298951,10.661977618146238,10.914342731679753,10.865917318389972,11.078675005430311,10.87714112179876,11.06790318711361,10.76635641041421,10.830797350892716,10.67271575750141,10.81997826441295,10.685949704772932,10.64965403707171,10.753253792537654,10.822953238903926,10.624736163206949,10.834174164694016,10.693625318409701,10.80642958564055,11.01690634852121,10.64034056535614,11.01715264383053,10.845621454367802,10.891354482899505,10.963670814584455,10.82404915126093,10.602368264943834,11.290206823369099,10.852439066649831,10.713217048175938,11.007186880252794,10.75239839707897,10.77511559050409,10.732715997033832,10.990600644811217,10.856129499874779,10.899125365576408,10.805963295376555,10.643184293749053,10.74950602342493,10.894291888569933,10.574849141024151,10.698965664193535,10.710164291083952,10.768316554785683,10.738936924565653,11.284857307664499,10.716149601597216,10.92092593841513,10.57826707573789,10.84410009655535,10.811181437184764,10.915833641046829,10.923255026881002,10.685263551322105,11.146286761516736,10.756944975238714,10.94029535695712,10.91091613578162,10.974917047351175,11.490188937996358,10.667116495634444,10.862071196600535,10.898607948952096,11.10128130578535,10.711836662784757,11.503975533550639,11.148319150705216,10.861150527516015,10.719471643055135,10.73633145595318,10.826018771999738,11.01652857785636,10.731100064464005,11.03725782546005,10.911792128172705,10.736853093036018,11.882134527618422,10.579234218415905,10.871763339476235,10.7211285344439,10.95752079780627,10.692308483164355,10.716149601597216,10.656929888879828,10.697791425055811,11.089606928642473,10.841989772775502,10.957032737834929,10.519105530586836,11.171997315498414,11.010514339805257,11.020594423840402,10.950209877616949,10.875175147630571,11.13898809326636,11.73316881476274,11.268302881978894,10.823371819920414,11.089744351056284,10.8213170998263,11.239698413488032,10.72364176327999,10.88807224504927,11.037997732201221,10.771763819308523,10.695665256559028,10.856669362994031,11.00033161214159,10.735722535246286,11.12043087483045,11.811243276893372,10.845796846808836,11.05128675205612,11.862758053293279,11.328750191103934,10.742205856415293,10.74716457989777,10.913122897389524,10.802754193404487,10.863316586424766,10.91202924411439,10.84675122191171,10.767326424407859,11.064072573519077,10.88844576963153,10.365899941086042,10.773776229848485,10.970798354703502,10.437551072769297,10.563103802387129,11.274046255019954,10.82903530567296,10.975961183594542,11.135814550358592,10.998694048069405,10.78188948386747,11.00334906060467,10.838482269204055,11.310564452838547,11.139336859509323,10.768148091173424,10.925974450814746,10.885828162871782,10.896257728115502,10.790246481804246,10.77325255447335,10.857478611593109,11.239698413488032,10.72364176327999,11.31049099274571,11.306011990515998,11.145752754648552,10.658552635911061,11.070210101081909,10.735657271744875,11.54556688968599,10.801940126280403,11.295229548312948,10.93674320772623,10.692263044109481,10.795034670519367,10.937152347559921,11.335543687352681,10.998142019349894,10.826734036976289,10.927268530581234,10.971984217299614,10.93652967699479,10.748711835976422,10.880139342084975,11.076078043033393,10.983188816312477,10.799289821982947,11.617231424779444,10.618811989707426,10.852593913351907,10.83372063653299,10.729853576882297,10.925542718482083,10.821935954964083,11.195636055765789,10.93784572406446,10.578292538848208,10.855685822748702,10.927124826611164,10.89382768342006,10.921450004820915,11.212455305708485,10.970798354703502,10.437551072769297,10.563103802387129,11.274046255019954,10.82903530567296,10.722936932960728,11.250677193775257,11.137489922063743,10.65530450425995,10.798963144696364,11.355031119697239,10.42540147328754,11.079816769425236,11.101296398644163,10.634580595510828,10.904468636571197,10.82450708598337,11.21321129629461,11.005709983458367,11.056082848402292,10.911062187812915,10.73219219685162,11.13898809326636,11.73316881476274,11.268302881978894,10.951332724150584,10.90404590072885,10.915924478293796,10.453485811376591,10.694872441685067,11.087818716606776,10.963653494818272,10.876706671796175,10.725994938401781,10.96443258747448,10.932964102369375,10.48475300044798,11.083848784736833,11.182572467557037,10.955794088327726,10.970798354703502,10.990668080241818,10.774341491401676,10.965228366428333,11.520873793152724,10.973100049353933,10.79127592393757,10.94755565435211,10.879913374660985,10.888184317074343,10.86047867153666,11.213089836345878,11.431455071972165,10.846108579656313,10.801288395096439,10.93969238107562,10.817796321618971,10.958182784137781,10.78999925792116,10.965038129063412,10.776077149139185,11.089820688682373,10.750363895525926,10.97891650574858,11.16596037035461,11.169674303268108,11.007518467231098,11.14162987263216,11.065215475518313,11.064229212669787,10.899069940884694,11.18712607040532,11.122752828680358,10.843748685048862,10.964311435142582,11.278329079610037,11.140556584351254,10.950016761334012,11.368928065697483,11.274807860012277,11.14378746449706,10.98960544362255,10.849900034962806,11.025441948777157,10.96949055763861,10.821057465908664,10.963757408916045,11.308566866434358,11.371638360125852,11.20065010832818,10.811201609659424,11.07680525390243,10.616633419602762,11.470351937411166,10.906047719562459,10.952997128196506,10.970609174112868,10.933053396853715,11.00033161214159,10.735722535246286,11.12043087483045,11.811243276893372,10.845796846808836,11.05128675205612,11.862758053293279,11.04375348980435,11.00033161214159,10.735722535246286,11.12043087483045,11.811243276893372,10.845796846808836,11.05128675205612,11.862758053293279,10.93857414032436,11.37863950201482,11.183768407068236,11.050175464435801,11.06124886505737,11.047805889293775,11.051255018113492,11.131284299585063,11.064229212669787,10.899069940884694,11.366025104606752,11.023339344196657,11.07970882053122,11.125172565460634,11.010514339805257,11.020594423840402,10.60129883922295,10.351724752488161,11.00033161214159,10.735722535246286,11.12043087483045,11.811243276893372,10.845796846808836,11.05128675205612,11.862758053293279,10.8373038112761,11.104009409185805,11.075706497243841,10.7030422005086,10.924750724776633,10.884366804297896,11.275999876182233,10.832733995570498,10.916868696841577,11.39032836025559,10.734982632705567,11.660137844650615,11.014061349603482,10.823730464248712,10.999195628056848,10.817956626198013,10.970798354703502,10.437551072769297,10.563103802387129,11.274046255019954,10.82903530567296,11.62035284319528,10.780954292552702,11.00665611228545,10.81178643448073,11.354796883773746,11.185892537563756,11.440354772135393,11.135274920356654,11.093128139551801,11.366279884628744,10.95593373119133,11.097637267913301,10.95166582665281,11.243803418039358,11.260262985619487,11.195086544816695,10.903255088818101,11.427683430860808,10.796100157055706,10.880779305967682,10.627188186139529,11.43174794697629,11.273423847043201,10.955078112430767,10.913050024370726,11.418131152083681,11.380102392856065,10.74542105042418,11.13898809326636,11.73316881476274,11.268302881978894,10.934552353218534,10.778351940641137,10.894217630225118,11.00033161214159,10.735722535246286,11.12043087483045,11.811243276893372,10.845796846808836,11.05128675205612,11.862758053293279,10.869767729155198,11.506635725967943,10.856746462510271,10.784482658015559,11.098091606857963,10.937312400199797,10.91567011320585,11.232854355519782,11.00033161214159,10.735722535246286,11.12043087483045,11.811243276893372,10.845796846808836,11.05128675205612,11.862758053293279,10.933553298669128,10.98698620339419,11.111746159674773,11.1181628799952],"xaxis":"x","y":[null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.35349917481061044,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.19580970461317432,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.2712125730539786,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.4309674009191006,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.28996845286206285,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.3087578477975381,null,null,null,null,null,null,null,null,null,null,null,null,0.1558013197314934,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.49021904913037906,null,null,null,0.14313141159323414,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.42161224792699054,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.25909133331877054,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.48559615156164626,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.38326483332794675,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.3735481585751765,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.3865325075286756,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.22048455864220598,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.2972685318715497,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.4048393732609937,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.2892173615743744,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.27222141853357057,0.1832794100025662,null,null,0.3426077807844686,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.4286759029258108,null,null,null,null,null,null,null,null,null,0.34503035315034314,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.21508067406609313,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.28632618309672475,null,null,null,null,null,null,null,null,null,0.3745257001702607,null,0.42064954140848254,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.30103645056253775,null,null,null,null,null,null,null,null,null,null,null,null,0.44055459030737465,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.2842989913495525,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.5604827530322594,null,null,null,null,null,null,null,null,0.364144920225235,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.3190060078410184,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.3312418636330353,null,null,null,null,null,null,null,null,0.22281237672290563,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.27093308892096474,null,null,null,null,null,null,null,0.24179179095478923,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.34948385543149757,null,null,null,null,null,null,null,null,null,null,null,null,null,0.2739891508365777,null,null,null,null,null,null,0.3282871202411785,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.42103167783270173,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.3327930368245113,null,null,null,null,null,null,null,null,null,null,null,null,null,0.36048050312624247,null,null,null,null,null,null,null,null,null,null,0.3148611310009249,null,null,null,null,0.19995401865440293,0.22711542839367602,null,null,null,0.32055849596253555,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.377984516271668,null,null,null,null,null,null,null,null,null,0.3127528569788758,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,null,0.3484088892709691,null,null,null,null,null,null,null,null,0.3233719039270432,null,null,0.3243956662121731,0.3243956662121731,null,null,0.23093834895134355,0.23093834895134355,0.23093834895134355,0.23093834895134355,0.23093834895134355,0.23093834895134355,0.23093834895134355,null,0.31121406940527363,null,null,null,0.4586830651166333,null,null,null,null,null,0.37842803696310934,0.3447382592430194,null,null,0.4777074115177726,null,null,null,null,null,null,null,null,null,0.31993457263664227,null,null,0.3664151406402852,0.31000846943377086,null,null,null,null,null,null,null,null,null,null,0.41746916806282264,null,null,null,null,null,0.3654453676460506,null,null,null,null,null,null,null,0.41334782897377914,null,null,null,null,null,null,null,null,0.261172092441251,null,null,null,0.3775462566451183,null,0.35343271977244983,0.2877605867193643,0.2877605867193643,0.2877605867193643,0.2877605867193643,0.2877605867193643,0.2877605867193643,0.2877605867193643,null,null,0.3554729801391049,0.3624523952228396],"yaxis":"y","type":"scattergl"},{"hovertemplate":"\u003cb\u003eOLS trendline\u003c\u002fb\u003e\u003cbr\u003eLog ChrstAdherentsPerCapita = -0.0353037 * x + 0.705798\u003cbr\u003eR\u003csup\u003e2\u003c\u002fsup\u003e=0.021335\u003cbr\u003e\u003cbr\u003ex=%{x}\u003cbr\u003eLog ChrstAdherentsPerCapita=%{y} \u003cb\u003e(trend)\u003c\u002fb\u003e\u003cextra\u003e\u003c\u002fextra\u003e","legendgroup":"","line":{"color":"red"},"marker":{"color":"#636efa","symbol":"circle"},"mode":"lines","name":"","showlegend":false,"x":[10.340871136212566,10.35951902421498,10.383008250473704,10.407167708141248,10.48203724319685,10.531802835594531,10.533748180040883,10.536698936485076,10.566639335560673,10.568646696555904,10.578572590277664,10.581140312137425,10.586786397041259,10.590289645536233,10.595484071338678,10.59905679752845,10.616633419602762,10.61771105869799,10.623666072147104,10.624736163206949,10.658552635911061,10.66993166215753,10.683569023781297,10.685652429413727,10.695529390070288,10.696050111394271,10.696253798124786,10.705937467986523,10.713217048175938,10.716748384090739,10.718011304262587,10.735722535246286,10.735722535246286,10.750363895525926,10.751199612844985,10.777079529877168,10.788411448660783,10.798370769971397,10.806105232822933,10.817796321618971,10.817956626198013,10.82117730532399,10.845796846808836,10.845796846808836,10.846498109109664,10.849900034962806,10.857882990443828,10.872598412593655,10.880779305967682,10.884366804297896,10.894217630225118,10.899125365576408,10.937312400199797,10.94600556684933,10.963653494818272,10.973100049353933,11.00033161214159,11.00033161214159,11.007518467231098,11.010514339805257,11.014061349603482,11.020594423840402,11.023339344196657,11.038962005936805,11.05128675205612,11.05128675205612,11.089820688682373,11.093128139551801,11.104009409185805,11.111746159674773,11.1181628799952,11.12043087483045,11.12043087483045,11.135274920356654,11.183768407068236,11.232854355519782,11.354796883773746,11.418131152083681,11.506635725967943,11.660137844650615,11.811243276893372,11.811243276893372,11.862758053293279,11.862758053293279],"xaxis":"x","y":[0.3407275235282337,0.34006918431961447,0.3392399280186198,0.3383870100774857,0.3357438394164537,0.33398693049940564,0.33391825266719555,0.3338140800841102,0.33275707359465573,0.3326862063495907,0.33233578570051897,0.332245135650664,0.3320458080342119,0.33192213044447744,0.33173874805974995,0.33161261765119737,0.3309920980800211,0.33095405344627826,0.3307438195130361,0.3307060413527749,0.32951219517161834,0.3291104735861504,0.32862902443448877,0.3285554725333239,0.32820677940188936,0.32818839601904737,0.3281812051263867,0.327839335872749,0.32758233984937307,0.3274576706701493,0.3274130849311972,0.32678781316916333,0.32678781316916333,0.3262709191628094,0.32624141525982653,0.3253277587591069,0.3249277002407816,0.3245760994745627,0.3243030444158817,0.3238903058717161,0.32388464652896953,0.3237709446799056,0.3229017840835098,0.3229017840835098,0.32287702693845927,0.3227569264115981,0.32247509864680574,0.32195558998333884,0.3216667742810482,0.3215401223614673,0.32119235188234746,0.3210190907276868,0.3196709475947904,0.3193640467569203,0.3187410098247306,0.31840751161644126,0.31744613703650126,0.31744613703650126,0.31719241455106617,0.317086649202232,0.3169614266771275,0.31673078506653723,0.3166338792563551,0.31608234168999894,0.3156472327057766,0.3156472327057766,0.3142868426530143,0.3141700774414448,0.31378592849982234,0.3135127926791046,0.3132862587908094,0.31320619021013163,0.31320619021013163,0.3126821406671934,0.3109701417716212,0.3092372267919876,0.30493220589432113,0.30269627268449917,0.29957173487503785,0.2941525440625536,0.28881796511892854,0.28881796511892854,0.28699930355666914,0.28699930355666914],"yaxis":"y","type":"scattergl"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Log of 2020 Income"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Christian Adherents per Capita"}},"legend":{"tracegroupgap":0},"margin":{"t":60},"title":{"text":"Log of 2020 Income vs. Christian Adherents per Capita"}},                        {"responsive": true}                    )             };                            </script>        </div>
</body>
</html>



```python
# prompt: get rsquared

# Assuming IncomeAndReligionByCounty is your DataFrame

# Fit a linear regression model
model = sm.ols('np.log(TotalChristianAdherents) ~ np.log(Q("2020 Income"))', data=IncomeAndReligionByCounty).fit()

# Print the R-squared value
print(f"R-squared: {model.rsquared}")
```

    R-squared: 0.45760539726848226


# This graph makes me uncomfortable

I found a similar fit of the R^2 but the line just feels off. The fit should theoretically be better becuase the y represents adherence of Christianity per capita, but it just feels cursed.


```python
# prompt: create a graph with the same dataset, but use totrate_2020 on the y and 2020 Income on the x

# Assuming IncomeAndReligionByCounty is your DataFrame

# Create the scatter plot
fig = px.scatter(IncomeAndReligionByCounty, x=np.log(IncomeAndReligionByCounty['2020 Income']), y='TOTRATE_2020',
                 hover_data=['COUNAM', 'STATNAM'], trendline='ols', trendline_color_override='red')

fig.update_layout(
    title='2020 Income vs. Total Rate of Religious Adherence',
    xaxis_title='2020 Income',
    yaxis_title='Total Rate of Religious Adherence'
)

fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
</body>
</html>



```python
# prompt: show r squared for last graph

# Assuming 'IncomeAndReligionByCounty' is your DataFrame

# Fit a linear regression model
model = sm.ols('TOTRATE_2020 ~ np.log(Q("2020 Income"))', data=IncomeAndReligionByCounty).fit()

# Print the R-squared value
print(f"R-squared: {model.rsquared}")
```

    R-squared: 0.0014682412084271457


# Bigger amount of Counties shown, but less correlation :(

The reason for the spike in dots is that im not using a combined list of columns, which discards the counties with any NaN values for the columns its adding. But with just the total religious percentage, it has the preset values in the set already.


```python
fig = px.scatter(IncomeAndReligionByCounty, x='Log 2020 Income', y='EVANRATE_2020',
                 hover_data=['COUNAM'],
                 trendline='ols', trendline_color_override='red')

fig.update_layout(
    title='Log of 2020 Income vs. Total Christian Adherents per Capita',
    xaxis_title='Log of 2020 Income',
    yaxis_title='Total Evangelical Christian Adherents per Capita'
)

fig.show()

fig = px.scatter(IncomeAndReligionByCounty, x='Log 2020 Income', y='CATHRATE_2020',
                 hover_data=['COUNAM'],
                 trendline='ols', trendline_color_override='red')
fig.update_layout(
    title='Log of 2020 Income vs. Total Christian Adherents per Capita',
    xaxis_title='Log of 2020 Income',
    yaxis_title='Total Chatholic Adherents per Capita'
)

fig.show()
```


<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
</body>
</html>



<html>
<head><meta charset="utf-8" /></head>
<body>
    <div>            <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_SVG"></script><script type="text/javascript">if (window.MathJax && window.MathJax.Hub && window.MathJax.Hub.Config) {window.MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}</script>                <script type="text/javascript">window.PlotlyConfig = {MathJaxConfig: 'local'};</script>
</body>
</html>



```python
# prompt: find rsquared for last graphs

# Assuming IncomeAndReligionByCounty is your DataFrame

# Fit a linear regression model for 'Log 2020 Income' vs. 'EVANRATE_2020'
model_evanrate = sm.ols('EVANRATE_2020 ~ Q("Log 2020 Income")', data=IncomeAndReligionByCounty).fit()
r_squared_evanrate = model_evanrate.rsquared
print(f"R-squared for Log 2020 Income vs. EVANRATE_2020: {r_squared_evanrate}")


# Fit a linear regression model for 'Log 2020 Income' vs. 'CATHRATE_2020'
model_cathrate = sm.ols('CATHRATE_2020 ~ Q("Log 2020 Income")', data=IncomeAndReligionByCounty).fit()
r_squared_cathrate = model_cathrate.rsquared
print(f"R-squared for Log 2020 Income vs. CATHRATE_2020: {r_squared_cathrate}")
```

    R-squared for Log 2020 Income vs. EVANRATE_2020: 0.09995276973203426
    R-squared for Log 2020 Income vs. CATHRATE_2020: 0.11328044032942619


# Last thing I really looked at

There is an obvious trend between the graphs which is, as the percent of evangelicals goes down, the percent of the catholics goes up. This makes sense because they are the largest religious groups in the US and they are very related becasue of their proximity of beliefs and population.

# Conclusion:


I'm deeply sorry in my performance here, I'm very dissappointed in myself. I want to try this again with more time spent on getting data. Actually using the resources I can like asking professors for possible avenues, which I lacked the hindsight to do, would have been a huge help. I'd also like to try to do this on a Physics focus possibly.

In terms of my "argument", I could not find an intellectually rigorous answer to my question. I found a decent correlation in the education to income comparison, but that one is sort of given. It's an obvious assumption to have that correlation. That's what I mean by not being "intellecually rigorous". It was too obvious. Everything else that I did was just looking at interesting possibilities of correlations and not finding any. My argument was that there should be a correlation between religious affiliation (however general) to GDP (in some form), or at the very least to income (in this case the median). However, because of many factors, I was unable to prove this. This inability to prove the solution of correlation has led me to not be so conviced now.