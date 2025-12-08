```python
#install relevant packages
!pip install statsbombpy
!pip install mplsoccer
!pip install highlight_text
```

    Collecting statsbombpy
      Downloading statsbombpy-1.16.0-py3-none-any.whl.metadata (63 kB)
    [?25l     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m0.0/63.7 kB[0m [31m?[0m eta [36m-:--:--[0m[2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m63.7/63.7 kB[0m [31m2.4 MB/s[0m eta [36m0:00:00[0m
    [?25hRequirement already satisfied: pandas in /usr/local/lib/python3.12/dist-packages (from statsbombpy) (2.2.2)
    Requirement already satisfied: requests in /usr/local/lib/python3.12/dist-packages (from statsbombpy) (2.32.4)
    Collecting requests-cache (from statsbombpy)
      Downloading requests_cache-1.2.1-py3-none-any.whl.metadata (9.9 kB)
    Requirement already satisfied: inflect in /usr/local/lib/python3.12/dist-packages (from statsbombpy) (7.5.0)
    Requirement already satisfied: joblib in /usr/local/lib/python3.12/dist-packages (from statsbombpy) (1.5.2)
    Requirement already satisfied: more_itertools>=8.5.0 in /usr/local/lib/python3.12/dist-packages (from inflect->statsbombpy) (10.8.0)
    Requirement already satisfied: typeguard>=4.0.1 in /usr/local/lib/python3.12/dist-packages (from inflect->statsbombpy) (4.4.4)
    Requirement already satisfied: numpy>=1.26.0 in /usr/local/lib/python3.12/dist-packages (from pandas->statsbombpy) (2.0.2)
    Requirement already satisfied: python-dateutil>=2.8.2 in /usr/local/lib/python3.12/dist-packages (from pandas->statsbombpy) (2.9.0.post0)
    Requirement already satisfied: pytz>=2020.1 in /usr/local/lib/python3.12/dist-packages (from pandas->statsbombpy) (2025.2)
    Requirement already satisfied: tzdata>=2022.7 in /usr/local/lib/python3.12/dist-packages (from pandas->statsbombpy) (2025.2)
    Requirement already satisfied: charset_normalizer<4,>=2 in /usr/local/lib/python3.12/dist-packages (from requests->statsbombpy) (3.4.4)
    Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.12/dist-packages (from requests->statsbombpy) (3.11)
    Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/local/lib/python3.12/dist-packages (from requests->statsbombpy) (2.5.0)
    Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.12/dist-packages (from requests->statsbombpy) (2025.11.12)
    Requirement already satisfied: attrs>=21.2 in /usr/local/lib/python3.12/dist-packages (from requests-cache->statsbombpy) (25.4.0)
    Collecting cattrs>=22.2 (from requests-cache->statsbombpy)
      Downloading cattrs-25.3.0-py3-none-any.whl.metadata (8.4 kB)
    Requirement already satisfied: platformdirs>=2.5 in /usr/local/lib/python3.12/dist-packages (from requests-cache->statsbombpy) (4.5.0)
    Collecting url-normalize>=1.4 (from requests-cache->statsbombpy)
      Downloading url_normalize-2.2.1-py3-none-any.whl.metadata (5.6 kB)
    Requirement already satisfied: typing-extensions>=4.14.0 in /usr/local/lib/python3.12/dist-packages (from cattrs>=22.2->requests-cache->statsbombpy) (4.15.0)
    Requirement already satisfied: six>=1.5 in /usr/local/lib/python3.12/dist-packages (from python-dateutil>=2.8.2->pandas->statsbombpy) (1.17.0)
    Downloading statsbombpy-1.16.0-py3-none-any.whl (16 kB)
    Downloading requests_cache-1.2.1-py3-none-any.whl (61 kB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m61.4/61.4 kB[0m [31m5.8 MB/s[0m eta [36m0:00:00[0m
    [?25hDownloading cattrs-25.3.0-py3-none-any.whl (70 kB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m70.7/70.7 kB[0m [31m5.6 MB/s[0m eta [36m0:00:00[0m
    [?25hDownloading url_normalize-2.2.1-py3-none-any.whl (14 kB)
    Installing collected packages: url-normalize, cattrs, requests-cache, statsbombpy
    Successfully installed cattrs-25.3.0 requests-cache-1.2.1 statsbombpy-1.16.0 url-normalize-2.2.1
    Collecting mplsoccer
      Downloading mplsoccer-1.6.1-py3-none-any.whl.metadata (4.8 kB)
    Requirement already satisfied: matplotlib>=3.6 in /usr/local/lib/python3.12/dist-packages (from mplsoccer) (3.10.0)
    Requirement already satisfied: numpy in /usr/local/lib/python3.12/dist-packages (from mplsoccer) (2.0.2)
    Requirement already satisfied: pandas in /usr/local/lib/python3.12/dist-packages (from mplsoccer) (2.2.2)
    Requirement already satisfied: pillow in /usr/local/lib/python3.12/dist-packages (from mplsoccer) (11.3.0)
    Requirement already satisfied: requests in /usr/local/lib/python3.12/dist-packages (from mplsoccer) (2.32.4)
    Requirement already satisfied: scipy in /usr/local/lib/python3.12/dist-packages (from mplsoccer) (1.16.3)
    Requirement already satisfied: seaborn in /usr/local/lib/python3.12/dist-packages (from mplsoccer) (0.13.2)
    Requirement already satisfied: contourpy>=1.0.1 in /usr/local/lib/python3.12/dist-packages (from matplotlib>=3.6->mplsoccer) (1.3.3)
    Requirement already satisfied: cycler>=0.10 in /usr/local/lib/python3.12/dist-packages (from matplotlib>=3.6->mplsoccer) (0.12.1)
    Requirement already satisfied: fonttools>=4.22.0 in /usr/local/lib/python3.12/dist-packages (from matplotlib>=3.6->mplsoccer) (4.60.1)
    Requirement already satisfied: kiwisolver>=1.3.1 in /usr/local/lib/python3.12/dist-packages (from matplotlib>=3.6->mplsoccer) (1.4.9)
    Requirement already satisfied: packaging>=20.0 in /usr/local/lib/python3.12/dist-packages (from matplotlib>=3.6->mplsoccer) (25.0)
    Requirement already satisfied: pyparsing>=2.3.1 in /usr/local/lib/python3.12/dist-packages (from matplotlib>=3.6->mplsoccer) (3.2.5)
    Requirement already satisfied: python-dateutil>=2.7 in /usr/local/lib/python3.12/dist-packages (from matplotlib>=3.6->mplsoccer) (2.9.0.post0)
    Requirement already satisfied: pytz>=2020.1 in /usr/local/lib/python3.12/dist-packages (from pandas->mplsoccer) (2025.2)
    Requirement already satisfied: tzdata>=2022.7 in /usr/local/lib/python3.12/dist-packages (from pandas->mplsoccer) (2025.2)
    Requirement already satisfied: charset_normalizer<4,>=2 in /usr/local/lib/python3.12/dist-packages (from requests->mplsoccer) (3.4.4)
    Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.12/dist-packages (from requests->mplsoccer) (3.11)
    Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/local/lib/python3.12/dist-packages (from requests->mplsoccer) (2.5.0)
    Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.12/dist-packages (from requests->mplsoccer) (2025.11.12)
    Requirement already satisfied: six>=1.5 in /usr/local/lib/python3.12/dist-packages (from python-dateutil>=2.7->matplotlib>=3.6->mplsoccer) (1.17.0)
    Downloading mplsoccer-1.6.1-py3-none-any.whl (88 kB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m88.5/88.5 kB[0m [31m3.4 MB/s[0m eta [36m0:00:00[0m
    [?25hInstalling collected packages: mplsoccer
    Successfully installed mplsoccer-1.6.1
    Collecting highlight_text
      Downloading highlight_text-0.2-py3-none-any.whl.metadata (13 kB)
    Downloading highlight_text-0.2-py3-none-any.whl (11 kB)
    Installing collected packages: highlight_text
    Successfully installed highlight_text-0.2



```python
#import packages
from statsbombpy import sb
import pandas as pd
import numpy as np
from mplsoccer import VerticalPitch,Pitch
from highlight_text import ax_text, fig_text
from matplotlib.colors import LinearSegmentedColormap
import matplotlib.pyplot as plt
import matplotlib.patheffects as path_effects
from matplotlib.lines import Line2D
from matplotlib.offsetbox import OffsetImage, AnnotationBbox
import seaborn as sns
```


```python
#call statsbombpy API to get all free competitions
free_comps = sb.competitions()

#print a list of free competitions
free_comps
```





  <div id="df-389be43e-4981-4e95-8cc1-c7211fa0f7d5" class="colab-df-container">
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
      <th>competition_id</th>
      <th>season_id</th>
      <th>country_name</th>
      <th>competition_name</th>
      <th>competition_gender</th>
      <th>competition_youth</th>
      <th>competition_international</th>
      <th>season_name</th>
      <th>match_updated</th>
      <th>match_updated_360</th>
      <th>match_available_360</th>
      <th>match_available</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9</td>
      <td>281</td>
      <td>Germany</td>
      <td>1. Bundesliga</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>2023/2024</td>
      <td>2024-09-28T20:46:38.893391</td>
      <td>2025-07-06T04:26:07.636270</td>
      <td>2025-07-06T04:26:07.636270</td>
      <td>2024-09-28T20:46:38.893391</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>27</td>
      <td>Germany</td>
      <td>1. Bundesliga</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>2015/2016</td>
      <td>2024-05-19T11:11:14.192381</td>
      <td>None</td>
      <td>None</td>
      <td>2024-05-19T11:11:14.192381</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1267</td>
      <td>107</td>
      <td>Africa</td>
      <td>African Cup of Nations</td>
      <td>male</td>
      <td>False</td>
      <td>True</td>
      <td>2023</td>
      <td>2024-09-28T01:57:35.846538</td>
      <td>None</td>
      <td>None</td>
      <td>2024-09-28T01:57:35.846538</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16</td>
      <td>4</td>
      <td>Europe</td>
      <td>Champions League</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>2018/2019</td>
      <td>2025-05-08T15:10:50.835274</td>
      <td>2021-06-13T16:17:31.694</td>
      <td>None</td>
      <td>2025-05-08T15:10:50.835274</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16</td>
      <td>1</td>
      <td>Europe</td>
      <td>Champions League</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>2017/2018</td>
      <td>2024-02-13T02:35:28.134882</td>
      <td>2021-06-13T16:17:31.694</td>
      <td>None</td>
      <td>2024-02-13T02:35:28.134882</td>
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
      <th>70</th>
      <td>35</td>
      <td>75</td>
      <td>Europe</td>
      <td>UEFA Europa League</td>
      <td>male</td>
      <td>False</td>
      <td>False</td>
      <td>1988/1989</td>
      <td>2024-02-12T14:45:05.702250</td>
      <td>2021-06-13T16:17:31.694</td>
      <td>None</td>
      <td>2024-02-12T14:45:05.702250</td>
    </tr>
    <tr>
      <th>71</th>
      <td>53</td>
      <td>315</td>
      <td>Europe</td>
      <td>UEFA Women's Euro</td>
      <td>female</td>
      <td>False</td>
      <td>True</td>
      <td>2025</td>
      <td>2025-07-28T14:19:20.467348</td>
      <td>2025-07-29T16:03:07.355174</td>
      <td>2025-07-29T16:03:07.355174</td>
      <td>2025-07-28T14:19:20.467348</td>
    </tr>
    <tr>
      <th>72</th>
      <td>53</td>
      <td>106</td>
      <td>Europe</td>
      <td>UEFA Women's Euro</td>
      <td>female</td>
      <td>False</td>
      <td>True</td>
      <td>2022</td>
      <td>2024-02-13T13:27:17.178263</td>
      <td>2024-02-13T13:30:52.820588</td>
      <td>2024-02-13T13:30:52.820588</td>
      <td>2024-02-13T13:27:17.178263</td>
    </tr>
    <tr>
      <th>73</th>
      <td>72</td>
      <td>107</td>
      <td>International</td>
      <td>Women's World Cup</td>
      <td>female</td>
      <td>False</td>
      <td>True</td>
      <td>2023</td>
      <td>2025-07-14T10:07:06.620906</td>
      <td>2025-07-14T10:10:27.224586</td>
      <td>2025-07-14T10:10:27.224586</td>
      <td>2025-07-14T10:07:06.620906</td>
    </tr>
    <tr>
      <th>74</th>
      <td>72</td>
      <td>30</td>
      <td>International</td>
      <td>Women's World Cup</td>
      <td>female</td>
      <td>False</td>
      <td>True</td>
      <td>2019</td>
      <td>2024-08-08T15:57:56.748740</td>
      <td>2021-06-13T16:17:31.694</td>
      <td>None</td>
      <td>2024-08-08T15:57:56.748740</td>
    </tr>
  </tbody>
</table>
<p>75 rows × 12 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-389be43e-4981-4e95-8cc1-c7211fa0f7d5')"
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
        document.querySelector('#df-389be43e-4981-4e95-8cc1-c7211fa0f7d5 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-389be43e-4981-4e95-8cc1-c7211fa0f7d5');
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


    <div id="df-a367421a-655b-48c2-9a94-203b8a17fca2">
      <button class="colab-df-quickchart" onclick="quickchart('df-a367421a-655b-48c2-9a94-203b8a17fca2')"
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
            document.querySelector('#df-a367421a-655b-48c2-9a94-203b8a17fca2 button');
          quickchartButtonEl.style.display =
            google.colab.kernel.accessAllowed ? 'block' : 'none';
        })();
      </script>
    </div>

  <div id="id_9c2bea7a-6808-4140-a78c-475d4e8689f2">
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
    <button class="colab-df-generate" onclick="generateWithVariable('free_comps')"
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
        document.querySelector('#id_9c2bea7a-6808-4140-a78c-475d4e8689f2 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('free_comps');
      }
      })();
    </script>
  </div>

    </div>
  </div>





```python
#call the statsbombpy API to get a list of matches for a given competition
#Euro 2024 competition id, season id
#competition_id=55, season_id=282
euro_2024_matches = sb.matches(competition_id=55, season_id=282)

row_count = len(euro_2024_matches)

row_count
```




    51




```python
#create a variable for the team you want to look into
team="England"

#filter for only matches that the focus team played in
matches_df = euro_2024_matches[(euro_2024_matches['home_team'] == team)|(euro_2024_matches['away_team'] == team)]

#sort by match date to get the most recent match
matches_df=matches_df.sort_values(by='match_date', ascending=False)
```


```python
#create a variable containing the first match id in the data frame
latest_match_id = matches_df.match_id.iloc[0]

#latest_match_id=3943043
```


```python
#call the statsbombpy events API to bring in the event data for the match
events_df = sb.events(match_id=latest_match_id)


events_df.head()
```





  <div id="df-bc41c96c-3587-4405-adee-cba4aa0158bb" class="colab-df-container">
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
      <th>50_50</th>
      <th>ball_receipt_outcome</th>
      <th>ball_recovery_recovery_failure</th>
      <th>block_deflection</th>
      <th>block_offensive</th>
      <th>block_save_block</th>
      <th>carry_end_location</th>
      <th>clearance_aerial_won</th>
      <th>clearance_body_part</th>
      <th>clearance_head</th>
      <th>...</th>
      <th>substitution_outcome</th>
      <th>substitution_outcome_id</th>
      <th>substitution_replacement</th>
      <th>substitution_replacement_id</th>
      <th>tactics</th>
      <th>team</th>
      <th>team_id</th>
      <th>timestamp</th>
      <th>type</th>
      <th>under_pressure</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>{'formation': 4231, 'lineup': [{'player': {'id...</td>
      <td>Spain</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>{'formation': 4231, 'lineup': [{'player': {'id...</td>
      <td>England</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>England</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Spain</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
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
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>England</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 92 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-bc41c96c-3587-4405-adee-cba4aa0158bb')"
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
        document.querySelector('#df-bc41c96c-3587-4405-adee-cba4aa0158bb button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-bc41c96c-3587-4405-adee-cba4aa0158bb');
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


    <div id="df-b7d34fda-2d20-4707-960c-b3d9cb0a5a08">
      <button class="colab-df-quickchart" onclick="quickchart('df-b7d34fda-2d20-4707-960c-b3d9cb0a5a08')"
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
            document.querySelector('#df-b7d34fda-2d20-4707-960c-b3d9cb0a5a08 button');
          quickchartButtonEl.style.display =
            google.colab.kernel.accessAllowed ? 'block' : 'none';
        })();
      </script>
    </div>

    </div>
  </div>





```python
#print a list of columns available in the event data
events_df.columns
```




    Index(['50_50', 'ball_receipt_outcome', 'ball_recovery_recovery_failure',
           'block_deflection', 'block_offensive', 'block_save_block',
           'carry_end_location', 'clearance_aerial_won', 'clearance_body_part',
           'clearance_head', 'clearance_left_foot', 'clearance_right_foot',
           'counterpress', 'dribble_nutmeg', 'dribble_outcome', 'dribble_overrun',
           'duel_outcome', 'duel_type', 'duration', 'foul_committed_advantage',
           'foul_committed_card', 'foul_committed_offensive', 'foul_won_advantage',
           'foul_won_defensive', 'goalkeeper_body_part', 'goalkeeper_end_location',
           'goalkeeper_outcome', 'goalkeeper_position', 'goalkeeper_technique',
           'goalkeeper_type', 'id', 'index', 'injury_stoppage_in_chain',
           'interception_outcome', 'location', 'match_id', 'minute', 'off_camera',
           'out', 'pass_aerial_won', 'pass_angle', 'pass_assisted_shot_id',
           'pass_body_part', 'pass_cross', 'pass_cut_back', 'pass_end_location',
           'pass_goal_assist', 'pass_height', 'pass_inswinging', 'pass_length',
           'pass_no_touch', 'pass_outcome', 'pass_outswinging', 'pass_recipient',
           'pass_recipient_id', 'pass_shot_assist', 'pass_switch',
           'pass_technique', 'pass_through_ball', 'pass_type', 'period',
           'play_pattern', 'player', 'player_id', 'position', 'possession',
           'possession_team', 'possession_team_id', 'related_events', 'second',
           'shot_aerial_won', 'shot_body_part', 'shot_deflected',
           'shot_end_location', 'shot_first_time', 'shot_freeze_frame',
           'shot_key_pass_id', 'shot_one_on_one', 'shot_outcome',
           'shot_statsbomb_xg', 'shot_technique', 'shot_type',
           'substitution_outcome', 'substitution_outcome_id',
           'substitution_replacement', 'substitution_replacement_id', 'tactics',
           'team', 'team_id', 'timestamp', 'type', 'under_pressure'],
          dtype='object')




```python
#separate start and end locations from coordinates
events_df[['x', 'y']] = events_df['location'].apply(pd.Series)
events_df[['pass_end_x', 'pass_end_y']] = events_df['pass_end_location'].apply(pd.Series)
events_df[['carry_end_x', 'carry_end_y']] = events_df['carry_end_location'].apply(pd.Series)
```


```python
print(events_df['pass_outcome'].unique())
print(events_df['duel_outcome'].unique())
print(events_df['duel_type'].unique())
print(events_df['dribble_outcome'].unique())
print(events_df['position'].unique())
print(events_df['possession'].unique())

```

    [nan 'Out' 'Incomplete' 'Unknown' 'Pass Offside']
    [nan 'Won' 'Success In Play' 'Lost Out' 'Lost In Play' 'Success Out']
    [nan 'Tackle' 'Aerial Lost']
    [nan 'Incomplete' 'Complete']
    [nan 'Right Defensive Midfield' 'Goalkeeper' 'Right Center Back'
     'Right Back' 'Center Forward' 'Center Attacking Midfield' 'Left Wing'
     'Left Center Back' 'Left Back' 'Left Defensive Midfield' 'Right Wing'
     'Right Center Midfield' 'Center Defensive Midfield' 'Left Center Forward'
     'Right Center Forward']
    [  1  79   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  46  47  48  49  50  51  52  53  54
      56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  72  73  74
      75  77  78  80  81  82  83  84  85  86  87  88  89  90  91  92  93  94
      95  96  97  98  99 100 101 102 103 104 105 106 107 108 109 110 111 112
     113 114 115 117 119 120 121 122 123 124 125 126 127 128 129 130 132 133
     134 135 136 137 138 139 140 141 142 143 144 145 146 147  71 131 118  45
      76 116  55]



```python
events_df.head()
```





  <div id="df-a085f10e-97f1-4adf-9100-d9e024e96077" class="colab-df-container">
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
      <th>50_50</th>
      <th>ball_receipt_outcome</th>
      <th>ball_recovery_recovery_failure</th>
      <th>block_deflection</th>
      <th>block_offensive</th>
      <th>block_save_block</th>
      <th>carry_end_location</th>
      <th>clearance_aerial_won</th>
      <th>clearance_body_part</th>
      <th>clearance_head</th>
      <th>...</th>
      <th>team_id</th>
      <th>timestamp</th>
      <th>type</th>
      <th>under_pressure</th>
      <th>x</th>
      <th>y</th>
      <th>pass_end_x</th>
      <th>pass_end_y</th>
      <th>carry_end_x</th>
      <th>carry_end_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
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
      <td>...</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
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
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
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
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
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
      <td>...</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
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
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
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
<p>5 rows × 98 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-a085f10e-97f1-4adf-9100-d9e024e96077')"
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
        document.querySelector('#df-a085f10e-97f1-4adf-9100-d9e024e96077 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-a085f10e-97f1-4adf-9100-d9e024e96077');
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


    <div id="df-26dbfc85-ee44-4a9c-aab8-20fc2a29a7ad">
      <button class="colab-df-quickchart" onclick="quickchart('df-26dbfc85-ee44-4a9c-aab8-20fc2a29a7ad')"
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
            document.querySelector('#df-26dbfc85-ee44-4a9c-aab8-20fc2a29a7ad button');
          quickchartButtonEl.style.display =
            google.colab.kernel.accessAllowed ? 'block' : 'none';
        })();
      </script>
    </div>

    </div>
  </div>





```python
#separate the period
sel_period = 1

df = events_df[events_df['period'] == sel_period].copy()

#sort the DataFrame by timestamp in descending order
fp = df.sort_values(by='timestamp', ascending=True)

fp.head()
```





  <div id="df-e02b71d9-7502-4b30-90f0-30053997de27" class="colab-df-container">
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
      <th>50_50</th>
      <th>ball_receipt_outcome</th>
      <th>ball_recovery_recovery_failure</th>
      <th>block_deflection</th>
      <th>block_offensive</th>
      <th>block_save_block</th>
      <th>carry_end_location</th>
      <th>clearance_aerial_won</th>
      <th>clearance_body_part</th>
      <th>clearance_head</th>
      <th>...</th>
      <th>team_id</th>
      <th>timestamp</th>
      <th>type</th>
      <th>under_pressure</th>
      <th>x</th>
      <th>y</th>
      <th>pass_end_x</th>
      <th>pass_end_y</th>
      <th>carry_end_x</th>
      <th>carry_end_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
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
      <td>...</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
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
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Starting XI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
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
      <td>...</td>
      <td>768</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
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
      <td>...</td>
      <td>772</td>
      <td>00:00:00.000</td>
      <td>Half Start</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
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
      <td>...</td>
      <td>768</td>
      <td>00:00:00.340</td>
      <td>Pass</td>
      <td>NaN</td>
      <td>60.0</td>
      <td>40.0</td>
      <td>25.4</td>
      <td>38.8</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 98 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-e02b71d9-7502-4b30-90f0-30053997de27')"
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
        document.querySelector('#df-e02b71d9-7502-4b30-90f0-30053997de27 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-e02b71d9-7502-4b30-90f0-30053997de27');
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


    <div id="df-fd70942f-fedd-4a36-8ced-dd0b3cdc3e3c">
      <button class="colab-df-quickchart" onclick="quickchart('df-fd70942f-fedd-4a36-8ced-dd0b3cdc3e3c')"
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
            document.querySelector('#df-fd70942f-fedd-4a36-8ced-dd0b3cdc3e3c button');
          quickchartButtonEl.style.display =
            google.colab.kernel.accessAllowed ? 'block' : 'none';
        })();
      </script>
    </div>

    </div>
  </div>





```python
# 페널티 제외
df1 = fp[fp['shot_type'] != 'Penalty'].copy()

# --- 선수별 xG 합계 ---
p_xg = df1.groupby('player')['shot_statsbomb_xg'].sum().round(2)

# --- 선수별 슈팅 횟수 (결측이 아닌 shot_outcome만 카운트) ---
p_shots = df1[df1['shot_outcome'].notna()].groupby('player').size()

# --- 두 결과를 하나로 합치기 ---
p_stats = pd.concat([p_xg, p_shots], axis=1)
p_stats.columns = ['xG_sum', 'Shots']
p_stats = p_stats.sort_values('xG_sum', ascending=False)

# --- 팀별 xG ---
t_xg = df1.groupby('team')['shot_statsbomb_xg'].sum().round(2)

# --- 출력 ---
print(f'Player & Team xG in {sel_period} Period')
print('-----------------------------------------------')
print(p_stats.head(12))
print('-----------------------------------------------')
print(t_xg)

```

    Player & Team xG in 1 Period
    -----------------------------------------------
                                  xG_sum  Shots
    player                                     
    Phil Foden                      0.18    1.0
    Robin Aime Robert Le Normand    0.12    1.0
    Álvaro Borja Morata Martín      0.08    1.0
    Nicholas Williams Arthuer       0.07    1.0
    Declan Rice                     0.05    1.0
    Fabián Ruiz Peña                0.05    1.0
    Harry Kane                      0.05    1.0
    Daniel Olmo Carvajal            0.03    1.0
    Aymeric Laporte                 0.00    NaN
    Bukayo Saka                     0.00    NaN
    Daniel Carvajal Ramos           0.00    NaN
    John Stones                     0.00    NaN
    -----------------------------------------------
    team
    England    0.28
    Spain      0.34
    Name: shot_statsbomb_xg, dtype: float64



```python
TEAM_NAME = 'England'
TEAM_COLOR = 'white' #darked or white

# --- 데이터 전처리 ---
df = fp.copy()

# 좌표와 id만 숫자로, outcome들은 문자열 그대로 두기
num_cols = ['x','y','pass_end_x','pass_end_y','player_id','pass_recipient_id','period']
for c in num_cols:
    if c in df.columns:
        df[c] = pd.to_numeric(df[c], errors='coerce')

# 성공 패스만, StatsBomb에서는 pass_outcome이 NaN이면 성공
team_passes = (
    df[(df['team'] == TEAM_NAME)
       & (df['type'] == 'Pass')
       & (df['pass_outcome'].isna())]            # <- 핵심 수정
    .dropna(subset=['x','y','pass_end_x','pass_end_y','player_id','pass_recipient_id'])
)

# 슛, 골 표기, shot_outcome으로 골 판단
team_shots = df[(df['team'] == TEAM_NAME) & (df['type'] == 'Shot')].copy()
team_shots['sx'] = team_shots['x']
team_shots['sy'] = team_shots['y']

id_to_name = (df[['player_id','player']].dropna()
              .drop_duplicates('player_id')
              .set_index('player_id')['player'].to_dict())

def make_network(team_df, min_edge_count=1):
    # 엣지, 패스 송수신 쌍과 횟수
    edges = (team_df
             .dropna(subset=['player_id','pass_recipient_id'])
             .groupby(['player_id','pass_recipient_id']).size()
             .reset_index(name='count'))
    edges = edges[edges['count'] >= min_edge_count].copy()

    # 노드, 평균 위치
    out_pos = (team_df.groupby('player_id')[['x','y']]
               .mean().rename(columns={'x':'x_out','y':'y_out'}))
    in_pos  = (team_df.groupby('pass_recipient_id')[['pass_end_x','pass_end_y']]
               .mean().rename(columns={'pass_end_x':'x_in','pass_end_y':'y_in'}))

    node_ids = pd.Index(out_pos.index).union(pd.Index(in_pos.index))
    nodes = (pd.DataFrame(index=node_ids)
             .join(out_pos, how='left')
             .join(in_pos, how='left'))
    nodes['x'] = nodes[['x_out','x_in']].mean(axis=1, skipna=True)
    nodes['y'] = nodes[['y_out','y_in']].mean(axis=1, skipna=True)

    sent = team_df.groupby('player_id').size().rename('sent')
    recv = team_df.groupby('pass_recipient_id').size().rename('received')
    nodes = nodes.join(sent, how='left').join(recv, how='left')
    nodes[['sent','received']] = nodes[['sent','received']].fillna(0)
    nodes['count'] = nodes['sent'] + nodes['received']

    nodes['name'] = nodes.index.map(lambda pid: id_to_name.get(pid, str(int(pid)) if pd.notna(pid) else 'NA'))
    nodes = nodes.dropna(subset=['x','y'])
    return nodes, edges

# 피치는 하나만 필요하니 ncols=1
pitch = Pitch(pitch_type='statsbomb', pitch_color='grass', line_color='white')
fig, ax = pitch.draw(ncols=1, nrows=1, figsize=(7, 6.5))
fig.subplots_adjust(top=0.85)

period = 1
half_passes = team_passes[team_passes['period'] == period]
nodes, edges = make_network(half_passes, min_edge_count=1)

# 패스 라인
if not edges.empty and not nodes.empty:
    edges = edges.merge(nodes[['x','y']], left_on='player_id', right_index=True)
    edges = edges.merge(nodes[['x','y']], left_on='pass_recipient_id', right_index=True, suffixes=('_sx','_rx'))
    maxc = edges['count'].max()
    lw_scale = (4.0/maxc) if maxc and maxc > 0 else 1.5
    for _, r in edges.iterrows():
        pitch.lines(r['x_sx'], r['y_sx'], r['x_rx'], r['y_rx'],
                    ax=ax, lw=max(0.8, r['count']*lw_scale),
                    alpha=0.75, color=TEAM_COLOR, zorder=3)

# 노드
if not nodes.empty:
    maxn = nodes['count'].max()
    size_scale = (350/maxn) if maxn and maxn > 0 else 120
    pitch.scatter(nodes['x'], nodes['y'],
                  s=np.clip(nodes['count']*size_scale, 80, 800),
                  ax=ax, color=TEAM_COLOR, edgecolors='black', linewidth=0.8, zorder=4)
    for _, r in nodes.iterrows():
        ax.text(r['x'], r['y'], r['name'], fontsize=8, ha='center', va='center',
                color='black',
                bbox=dict(facecolor='white', alpha=0.7, boxstyle='round,pad=0.2'),
                zorder=5)

# 슛, 골 표기, shot_outcome으로 구분
hs = team_shots[team_shots['period'] == period]
if not hs.empty:
    g = hs[hs['shot_outcome'] == 'Goal']
    if not g.empty:
        pitch.scatter(g['sx'], g['sy'], s=90, ax=ax, color='blue',
                      edgecolors='black', linewidth=0.8, marker='o', zorder=6)
    m = hs[hs['shot_outcome'] != 'Goal']
    if not m.empty:
        pitch.scatter(m['sx'], m['sy'], s=90, ax=ax, color='red',
                      edgecolors='black', linewidth=0.8, marker='o', zorder=6)

# 범례와 제목
pass_proxy = Line2D([0],[0], color=TEAM_COLOR, lw=3, label='Pass success')
goal_proxy = Line2D([0],[0], marker='o', color='blue', lw=0, markersize=8,
                    markerfacecolor='blue', markeredgecolor='black', label='Goal')
miss_proxy = Line2D([0],[0], marker='o', color='red', lw=0, markersize=8,
                    markerfacecolor='red', markeredgecolor='black', label='Miss')
ax.legend(handles=[pass_proxy, goal_proxy, miss_proxy], loc='upper right', frameon=True, fontsize=8)
ax.set_title(f"{TEAM_NAME} Passing Map, Period {period}", fontsize=12, pad=8)

plt.show()

```


    
![png](Euro_2024_Final_files/Euro_2024_Final_13_0.png)
    



```python
Team = 'England'

passes_in_period = fp[fp['type'] == 'Pass'].copy()
successful_passes_count = passes_in_period['pass_outcome'].isna().sum()
total_passes_count = len(passes_in_period)

if total_passes_count > 0:
    tsr = ((successful_passes_count / total_passes_count) * 100).round(2)
else:
    tsr = None # Handle cases with no passes, e.g., set to None or np.nan

print('---------------------------------------------------------------------')
print(f'{Team} Pass Success Rate Per Team:', tsr, '%')
print('---------------------------------------------------------------------')

# Calculate pass success rate per player
player_passes_df = fp[(fp['type'] == 'Pass') & (fp['team'] == Team )].copy()

# Group by player and calculate successful passes and total passes
pass_stats_per_player = player_passes_df.groupby('player').agg(
    successful_passes=('pass_outcome', lambda x: x.isna().sum()),
    total_passes=('type', 'count')
)

# Calculate success rate per player
pass_stats_per_player['success_rate'] = ((pass_stats_per_player['successful_passes'] / pass_stats_per_player['total_passes']) * 100).round(2)

print(f'{Team} Pass Success Rate Per Player:')
print(pass_stats_per_player.sort_values(by='success_rate', ascending=False).head(20))
```

    ---------------------------------------------------------------------
    England Pass Success Rate Per Team: 82.64 %
    ---------------------------------------------------------------------
    England Pass Success Rate Per Player:
                     successful_passes  total_passes  success_rate
    player                                                        
    Marc Guehi                       8             8        100.00
    Bukayo Saka                      8             9         88.89
    John Stones                     15            18         83.33
    Luke Shaw                        9            11         81.82
    Kyle Walker                     16            20         80.00
    Phil Foden                       8            10         80.00
    Kobbie Mainoo                    9            12         75.00
    Jordan Pickford                 13            19         68.42
    Jude Bellingham                 10            15         66.67
    Declan Rice                     11            18         61.11
    Harry Kane                       5            10         50.00



```python
TEAM_NAME = 'England'
DOT_COLOR = 'white'  # 팀 톤

# 데이터: 실패 패스(Outcome=0)의 종료 지점만 사용
df = fp.copy()
for c in ['pass_end_x','pass_end_y']:
    if c in df.columns:
        df[c] = pd.to_numeric(df[c], errors='coerce')

fail = df[(df['team']==TEAM_NAME) & (df['type']=='Pass') & (df['pass_outcome'].notna())]
fail = fail.dropna(subset=['pass_end_x','pass_end_y'])

# 그리기
pitch = Pitch(pitch_type='statsbomb', pitch_color='grass', line_color='white')
fig, ax = pitch.draw(ncols=1, nrows=1, figsize=(13, 6.5))
fig.subplots_adjust(top=0.83, wspace=0.18)

period = 1
dat = fail[fail['period'] == period]
if not dat.empty:
        # 원형 점: 투명도 누적 → 밀집도 직관적
        ax.scatter(dat['pass_end_x'], dat['pass_end_y'],
                   s=75, facecolor=DOT_COLOR, edgecolor='black',
                   linewidths=0.3, alpha=0.28, zorder=4)
    # 간단한 범례(원형 샘플)
dot_proxy = plt.Line2D([0],[0], marker='o', linestyle='',
                           markersize=8, markerfacecolor=DOT_COLOR,
                           markeredgecolor='black', label='Failed pass end')
ax.legend(handles=[dot_proxy], loc='upper right', fontsize=8, frameon=True)
ax.set_title(f"{TEAM_NAME} Failed Pass Endpoints (Period {period})", fontsize=11, pad=6)

plt.show()
```


    
![png](Euro_2024_Final_files/Euro_2024_Final_15_0.png)
    



```python
#선수별 경합 성공률
df = fp.copy()

duel_won_cd = df[df['duel_outcome'].isin(['Won', 'Success In Play', 'Success Out']) | df['clearance_aerial_won'].isin([True])]
duel_won = duel_won_cd.groupby('player').size()
duel_lost_cd = df[df['duel_outcome'].isin(['Lost In Play', 'Lost Out']) | df['duel_type'].isin(['Aerial Lost'])]
duel_lost = duel_lost_cd.groupby('player').size()


# Combine duel_won and duel_lost into a single DataFrame indexed by player
duel_stat = pd.concat([duel_won.rename('Duel Won'), duel_lost.rename('Duel Lost')], axis=1).fillna(0)

duel_stat['Duel Success Rate'] = (duel_stat['Duel Won'] / (duel_stat['Duel Won'] + duel_stat['Duel Lost']) * 100).fillna(0).round(2)
duel_stat = duel_stat.sort_values(by='Duel Success Rate', ascending=False)

# To include team information and filter by team:
# First, get a player-to-team mapping from the original events dataframe
player_team_map = df[['player', 'team']].drop_duplicates(subset=['player']).set_index('player')['team']
# Merge this map with the duel_stat DataFrame
duel_stat = duel_stat.merge(player_team_map, left_index=True, right_index=True, how='left')


print(f'{sel_period} Period Duel Success Rate Per Player:')
print('-------------------------------------------------')
#print(duel_stat.head(30)) # Print top 30 overall

eng_duel_stat = duel_stat[duel_stat['team'] == 'England']
spa_duel_stat = duel_stat[duel_stat['team'] == 'Spain']

print('\nEngland Duel Stats:')
print('-------------------------------------------------')
print(eng_duel_stat)

print('\nSpain Duel Stats:')
print('-------------------------------------------------')
print(spa_duel_stat)
```

    1 Period Duel Success Rate Per Player:
    -------------------------------------------------
    
    England Duel Stats:
    -------------------------------------------------
                     Duel Won  Duel Lost  Duel Success Rate     team
    player                                                          
    Kyle Walker           2.0        0.0             100.00  England
    Marc Guehi            1.0        0.0             100.00  England
    John Stones           2.0        1.0              66.67  England
    Jude Bellingham       3.0        4.0              42.86  England
    Luke Shaw             1.0        2.0              33.33  England
    Bukayo Saka           0.0        2.0               0.00  England
    Harry Kane            0.0        4.0               0.00  England
    Kobbie Mainoo         0.0        2.0               0.00  England
    Phil Foden            0.0        1.0               0.00  England
    
    Spain Duel Stats:
    -------------------------------------------------
                                  Duel Won  Duel Lost  Duel Success Rate   team
    player                                                                     
    Daniel Carvajal Ramos              4.0        1.0              80.00  Spain
    Robin Aime Robert Le Normand       1.0        1.0              50.00  Spain
    Fabián Ruiz Peña                   1.0        1.0              50.00  Spain
    Aymeric Laporte                    1.0        2.0              33.33  Spain
    Daniel Olmo Carvajal               1.0        2.0              33.33  Spain
    Álvaro Borja Morata Martín         1.0        3.0              25.00  Spain
    Rodrigo Hernández Cascante         0.0        1.0               0.00  Spain



```python
#duel_won = df[df['duel_outcome'].isin(['Won', 'Success In Play', 'Success Out'])].groupby('team').size()
#duel_lost_cd = df[df['duel_outcome'].isin(['Lost In Play', 'Lost Out']) | df['duel_type'].isin(['Aerial Lost'])]
#duel_lost = duel_lost_cd.groupby('team').size()
#duel_won = df[df['duel_type'].isin(['Tackle'])].groupby('team').size()
#duel_lost = df[df['duel_type'].isin(['Aerial Lost'])].groupby('team').size()
duel_won_cd = df[df['duel_outcome'].isin(['Won', 'Success In Play', 'Success Out']) | df['clearance_aerial_won'].isin([True])]
duel_won = duel_won_cd.groupby('team').size()
duel_lost_cd = df[df['duel_outcome'].isin(['Lost In Play', 'Lost Out']) | df['duel_type'].isin(['Aerial Lost'])]
duel_lost = duel_lost_cd.groupby('team').size()


duel_stat = pd.concat([duel_won, duel_lost], axis=1).fillna(0)
duel_stat.columns = ['Duel Won', 'Duel Lost']

duel_stat['Duel Success Rate'] = (duel_stat['Duel Won'] / (duel_stat['Duel Won'] + duel_stat['Duel Lost']) * 100).fillna(0).round(2)
duel_stat = duel_stat.sort_values(by='Duel Success Rate', ascending=False)

print(f'{sel_period} Period Duel Success Rate Per Team')
print('-------------------------------------------------')
print(duel_stat.head(30))
```

    1 Period Duel Success Rate Per Team
    -------------------------------------------------
             Duel Won  Duel Lost  Duel Success Rate
    team                                           
    Spain           9         11               45.0
    England         9         16               36.0



```python
df = fp.copy()
dribble_suc = df[df['dribble_outcome'] == 'Complete'].groupby('player').size()
dribble_fail = df[df['dribble_outcome'] == 'Incomplete'].groupby('player').size()
dribble_success_rate = (dribble_suc / (dribble_suc + dribble_fail) * 100).fillna(0).round(2)

dribble_stat = pd.concat([dribble_suc.rename('Dribble Success'), dribble_fail.rename('Dribble Fail'), dribble_success_rate.rename('Dribble Success Rate')], axis=1).fillna(0)

player_index = df[['player', 'team']].drop_duplicates(subset=['player']).set_index('player')['team']
dribble_stat = dribble_stat.merge(player_index, left_index=True, right_index=True, how='left')

dribble_stat  = dribble_stat.sort_values(by='Dribble Success Rate', ascending=False)

eng_dribble_stat = dribble_stat[dribble_stat['team'] == 'England']
spa_dribble_stat = dribble_stat[dribble_stat['team'] == 'Spain']

print(f'{sel_period} Period Dribble Success Rate by Player')
print('-------------------------------------------------------')
print(eng_dribble_stat.head(20))
print('-------------------------------------------------------')
print(spa_dribble_stat.head(20))
```

    1 Period Dribble Success Rate by Player
    -------------------------------------------------------
                     Dribble Success  Dribble Fail  Dribble Success Rate     team
    player                                                                       
    Declan Rice                  1.0           1.0                  50.0  England
    Luke Shaw                    1.0           1.0                  50.0  England
    Jude Bellingham              1.0           0.0                   0.0  England
    Kobbie Mainoo                0.0           1.0                   0.0  England
    Phil Foden                   0.0           1.0                   0.0  England
    -------------------------------------------------------
                                 Dribble Success  Dribble Fail  \
    player                                                       
    Nicholas Williams Arthuer                1.0           1.0   
    Fabián Ruiz Peña                         1.0           0.0   
    Lamine Yamal Nasraoui Ebana              0.0           1.0   
    Álvaro Borja Morata Martín               0.0           1.0   
    
                                 Dribble Success Rate   team  
    player                                                    
    Nicholas Williams Arthuer                    50.0  Spain  
    Fabián Ruiz Peña                              0.0  Spain  
    Lamine Yamal Nasraoui Ebana                   0.0  Spain  
    Álvaro Borja Morata Martín                    0.0  Spain  



```python
eng_player = 'Declan Rice'
spa_player = 'Martín Zubimendi Ibáñez'

eng_duel_one = eng_duel_stat.reindex([eng_player]).fillna(0)
spa_duel_one = spa_duel_stat.reindex([spa_player]).fillna(0)

eng_dribble_one = eng_dribble_stat.reindex([eng_player]).fillna(0)
spa_dribble_one = spa_dribble_stat.reindex([spa_player]).fillna(0)

eng_stat = eng_duel_one.merge(eng_dribble_one, left_index=True, right_index=True, how='left')
spa_stat = spa_duel_one.merge(spa_dribble_one, left_index=True, right_index=True, how='left')

print('First Period Player Stats Comparison')
print('---------------------------------------------------------------------------')
print(f'{eng_player} Stats:')
print(eng_stat)
print('---------------------------------------------------------------------------')
print(f'{spa_player} Stats:')
print(spa_stat)
print('---------------------------------------------------------------------------')
```

    First Period Player Stats Comparison
    ---------------------------------------------------------------------------
    Declan Rice Stats:
                 Duel Won  Duel Lost  Duel Success Rate  team_x  Dribble Success  \
    player                                                                         
    Declan Rice       0.0        0.0                0.0       0              1.0   
    
                 Dribble Fail  Dribble Success Rate   team_y  
    player                                                    
    Declan Rice           1.0                  50.0  England  
    ---------------------------------------------------------------------------
    Martín Zubimendi Ibáñez Stats:
                             Duel Won  Duel Lost  Duel Success Rate  team_x  \
    player                                                                    
    Martín Zubimendi Ibáñez       0.0        0.0                0.0       0   
    
                             Dribble Success  Dribble Fail  Dribble Success Rate  \
    player                                                                         
    Martín Zubimendi Ibáñez              0.0           0.0                   0.0   
    
                             team_y  
    player                           
    Martín Zubimendi Ibáñez       0  
    ---------------------------------------------------------------------------


    /tmp/ipython-input-1330070284.py:4: FutureWarning: Downcasting object dtype arrays on .fillna, .ffill, .bfill is deprecated and will change in a future version. Call result.infer_objects(copy=False) instead. To opt-in to the future behavior, set `pd.set_option('future.no_silent_downcasting', True)`
      eng_duel_one = eng_duel_stat.reindex([eng_player]).fillna(0)
    /tmp/ipython-input-1330070284.py:5: FutureWarning: Downcasting object dtype arrays on .fillna, .ffill, .bfill is deprecated and will change in a future version. Call result.infer_objects(copy=False) instead. To opt-in to the future behavior, set `pd.set_option('future.no_silent_downcasting', True)`
      spa_duel_one = spa_duel_stat.reindex([spa_player]).fillna(0)
    /tmp/ipython-input-1330070284.py:8: FutureWarning: Downcasting object dtype arrays on .fillna, .ffill, .bfill is deprecated and will change in a future version. Call result.infer_objects(copy=False) instead. To opt-in to the future behavior, set `pd.set_option('future.no_silent_downcasting', True)`
      spa_dribble_one = spa_dribble_stat.reindex([spa_player]).fillna(0)



```python
from google.colab import drive
drive.mount('/content/drive')
```

    Drive already mounted at /content/drive; to attempt to forcibly remount, call drive.mount("/content/drive", force_remount=True).



```python
!jupyter nbconvert --to markdown "/content/drive/MyDrive/Euro_2024_Final.ipynb"
```

    [NbConvertApp] WARNING | pattern '/content/drive/MyDrive/Euro_2024_Final.ipynb' matched no files
    This application is used to convert notebook files (*.ipynb)
            to various other formats.
    
            WARNING: THE COMMANDLINE INTERFACE MAY CHANGE IN FUTURE RELEASES.
    
    Options
    =======
    The options below are convenience aliases to configurable class-options,
    as listed in the "Equivalent to" description-line of the aliases.
    To see all configurable class-options for some <cmd>, use:
        <cmd> --help-all
    
    --debug
        set log level to logging.DEBUG (maximize logging output)
        Equivalent to: [--Application.log_level=10]
    --show-config
        Show the application's configuration (human-readable format)
        Equivalent to: [--Application.show_config=True]
    --show-config-json
        Show the application's configuration (json format)
        Equivalent to: [--Application.show_config_json=True]
    --generate-config
        generate default config file
        Equivalent to: [--JupyterApp.generate_config=True]
    -y
        Answer yes to any questions instead of prompting.
        Equivalent to: [--JupyterApp.answer_yes=True]
    --execute
        Execute the notebook prior to export.
        Equivalent to: [--ExecutePreprocessor.enabled=True]
    --allow-errors
        Continue notebook execution even if one of the cells throws an error and include the error message in the cell output (the default behaviour is to abort conversion). This flag is only relevant if '--execute' was specified, too.
        Equivalent to: [--ExecutePreprocessor.allow_errors=True]
    --stdin
        read a single notebook file from stdin. Write the resulting notebook with default basename 'notebook.*'
        Equivalent to: [--NbConvertApp.from_stdin=True]
    --stdout
        Write notebook output to stdout instead of files.
        Equivalent to: [--NbConvertApp.writer_class=StdoutWriter]
    --inplace
        Run nbconvert in place, overwriting the existing notebook (only
                relevant when converting to notebook format)
        Equivalent to: [--NbConvertApp.use_output_suffix=False --NbConvertApp.export_format=notebook --FilesWriter.build_directory=]
    --clear-output
        Clear output of current file and save in place,
                overwriting the existing notebook.
        Equivalent to: [--NbConvertApp.use_output_suffix=False --NbConvertApp.export_format=notebook --FilesWriter.build_directory= --ClearOutputPreprocessor.enabled=True]
    --coalesce-streams
        Coalesce consecutive stdout and stderr outputs into one stream (within each cell).
        Equivalent to: [--NbConvertApp.use_output_suffix=False --NbConvertApp.export_format=notebook --FilesWriter.build_directory= --CoalesceStreamsPreprocessor.enabled=True]
    --no-prompt
        Exclude input and output prompts from converted document.
        Equivalent to: [--TemplateExporter.exclude_input_prompt=True --TemplateExporter.exclude_output_prompt=True]
    --no-input
        Exclude input cells and output prompts from converted document.
                This mode is ideal for generating code-free reports.
        Equivalent to: [--TemplateExporter.exclude_output_prompt=True --TemplateExporter.exclude_input=True --TemplateExporter.exclude_input_prompt=True]
    --allow-chromium-download
        Whether to allow downloading chromium if no suitable version is found on the system.
        Equivalent to: [--WebPDFExporter.allow_chromium_download=True]
    --disable-chromium-sandbox
        Disable chromium security sandbox when converting to PDF..
        Equivalent to: [--WebPDFExporter.disable_sandbox=True]
    --show-input
        Shows code input. This flag is only useful for dejavu users.
        Equivalent to: [--TemplateExporter.exclude_input=False]
    --embed-images
        Embed the images as base64 dataurls in the output. This flag is only useful for the HTML/WebPDF/Slides exports.
        Equivalent to: [--HTMLExporter.embed_images=True]
    --sanitize-html
        Whether the HTML in Markdown cells and cell outputs should be sanitized..
        Equivalent to: [--HTMLExporter.sanitize_html=True]
    --log-level=<Enum>
        Set the log level by value or name.
        Choices: any of [0, 10, 20, 30, 40, 50, 'DEBUG', 'INFO', 'WARN', 'ERROR', 'CRITICAL']
        Default: 30
        Equivalent to: [--Application.log_level]
    --config=<Unicode>
        Full path of a config file.
        Default: ''
        Equivalent to: [--JupyterApp.config_file]
    --to=<Unicode>
        The export format to be used, either one of the built-in formats
                ['asciidoc', 'custom', 'html', 'latex', 'markdown', 'notebook', 'pdf', 'python', 'qtpdf', 'qtpng', 'rst', 'script', 'slides', 'webpdf']
                or a dotted object name that represents the import path for an
                ``Exporter`` class
        Default: ''
        Equivalent to: [--NbConvertApp.export_format]
    --template=<Unicode>
        Name of the template to use
        Default: ''
        Equivalent to: [--TemplateExporter.template_name]
    --template-file=<Unicode>
        Name of the template file to use
        Default: None
        Equivalent to: [--TemplateExporter.template_file]
    --theme=<Unicode>
        Template specific theme(e.g. the name of a JupyterLab CSS theme distributed
        as prebuilt extension for the lab template)
        Default: 'light'
        Equivalent to: [--HTMLExporter.theme]
    --sanitize_html=<Bool>
        Whether the HTML in Markdown cells and cell outputs should be sanitized.This
        should be set to True by nbviewer or similar tools.
        Default: False
        Equivalent to: [--HTMLExporter.sanitize_html]
    --writer=<DottedObjectName>
        Writer class used to write the
                                            results of the conversion
        Default: 'FilesWriter'
        Equivalent to: [--NbConvertApp.writer_class]
    --post=<DottedOrNone>
        PostProcessor class used to write the
                                            results of the conversion
        Default: ''
        Equivalent to: [--NbConvertApp.postprocessor_class]
    --output=<Unicode>
        Overwrite base name use for output files.
                    Supports pattern replacements '{notebook_name}'.
        Default: '{notebook_name}'
        Equivalent to: [--NbConvertApp.output_base]
    --output-dir=<Unicode>
        Directory to write output(s) to. Defaults
                                      to output to the directory of each notebook. To recover
                                      previous default behaviour (outputting to the current
                                      working directory) use . as the flag value.
        Default: ''
        Equivalent to: [--FilesWriter.build_directory]
    --reveal-prefix=<Unicode>
        The URL prefix for reveal.js (version 3.x).
                This defaults to the reveal CDN, but can be any url pointing to a copy
                of reveal.js.
                For speaker notes to work, this must be a relative path to a local
                copy of reveal.js: e.g., "reveal.js".
                If a relative path is given, it must be a subdirectory of the
                current directory (from which the server is run).
                See the usage documentation
                (https://nbconvert.readthedocs.io/en/latest/usage.html#reveal-js-html-slideshow)
                for more details.
        Default: ''
        Equivalent to: [--SlidesExporter.reveal_url_prefix]
    --nbformat=<Enum>
        The nbformat version to write.
                Use this to downgrade notebooks.
        Choices: any of [1, 2, 3, 4]
        Default: 4
        Equivalent to: [--NotebookExporter.nbformat_version]
    
    Examples
    --------
    
        The simplest way to use nbconvert is
    
                > jupyter nbconvert mynotebook.ipynb --to html
    
                Options include ['asciidoc', 'custom', 'html', 'latex', 'markdown', 'notebook', 'pdf', 'python', 'qtpdf', 'qtpng', 'rst', 'script', 'slides', 'webpdf'].
    
                > jupyter nbconvert --to latex mynotebook.ipynb
    
                Both HTML and LaTeX support multiple output templates. LaTeX includes
                'base', 'article' and 'report'.  HTML includes 'basic', 'lab' and
                'classic'. You can specify the flavor of the format used.
    
                > jupyter nbconvert --to html --template lab mynotebook.ipynb
    
                You can also pipe the output to stdout, rather than a file
    
                > jupyter nbconvert mynotebook.ipynb --stdout
    
                PDF is generated via latex
    
                > jupyter nbconvert mynotebook.ipynb --to pdf
    
                You can get (and serve) a Reveal.js-powered slideshow
    
                > jupyter nbconvert myslides.ipynb --to slides --post serve
    
                Multiple notebooks can be given at the command line in a couple of
                different ways:
    
                > jupyter nbconvert notebook*.ipynb
                > jupyter nbconvert notebook1.ipynb notebook2.ipynb
    
                or you can specify the notebooks list in a config file, containing::
    
                    c.NbConvertApp.notebooks = ["my_notebook.ipynb"]
    
                > jupyter nbconvert --config mycfg.py
    
    To see all available configurables, use `--help-all`.
    

