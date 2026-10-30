# Crédito rural no Cerrado — notebooks da dissertação

Repositório dos notebooks de apoio à pesquisa sobre observância dos impedimentos socioambientais no crédito rural no bioma Cerrado, no período de **2021 a 2025**. O trabalho combina análise documental, estatística descritiva e análise espacial vetorial de glebas do SICOR e bases territoriais oficiais.

**Autor:** Mario Kenji Fernandes Nery  
**Orientador:** Prof. Dr. Remis Balaniuk  
**Programa:** Mestrado em Governança, Tecnologia e Inovação — Universidade Católica de Brasília, 2026.

Este guia relaciona os **42 notebooks** disponíveis na raiz aos procedimentos e resultados da dissertação.

## Como utilizar os notebooks

### Ambiente e dados necessários

O ambiente previsto é **Python no Google Colab**, com arquivos no Google Drive. As dependências variam entre notebooks e incluem `pandas`, `numpy`, `geopandas`, `shapely`, `pyogrio`, `pyproj`, `geobr`, `matplotlib`, `seaborn` e bibliotecas de exportação, como `python-docx` e `openpyxl`. Consultar a célula de instalação de cada arquivo: não há um ambiente único com versões fixadas para todo o acervo.

São necessárias as bases externas indicadas nas configurações:

| Fonte | Insumos utilizados |
| --- | --- |
| SICOR / Banco Central | CSVs anuais de glebas de 2021–2025, dados de operações e tabelas de domínio; liberações, saldos e desclassificações para o módulo financeiro. |
| IBGE | Limite do Cerrado, estados e municípios; os mapas de localização usam Biomas 2019 e malha estadual 2024. |
| Funai | `tis_poligonais.shp`. |
| Incra | Camadas de territórios quilombolas e assentamentos; os nomes exatos dos arquivos variam entre texto e configurações. |
| Serviço Florestal Brasileiro | `CNFP_2025.shp`. |
| MMA / CNUC | `ucs.shp`, preservando o atributo que distingue UC de ZA. |
| Ibama | `adm_embargo_ibama_a.shp`, correspondente à base federal. |
| SICAR | Treze arquivos estaduais: AC, BA, DF, GO, MA, MG, MS, MT, PI, PR, RO, SP e TO, com situação e condição cadastral. |

### Sequência de trabalho

1. **Escolher o ponto de partida.** Para inspecionar produtos já gerados, usar os complementos ou as revisões de dicionário, com suas entradas correspondentes. Para reconstruir a base, iniciar pela preparação e resolver as divergências descritas na próxima seção.
2. **Preparar os arquivos de entrada e os caminhos.** A estrutura recorrente é `/content/drive/MyDrive/Colab Notebooks/fluxo/Envio/`, com `Base/` e `Arquivos gerados e relatorios/`. Alguns notebooks usam `/content/drive/MyDrive/Envio/` ou `Produto_dissertacao_Cerrado/`; conferir individualmente.
3. **Preparar e identificar a base:** Base01 → Base02 → Base04 → Base05. Executar as auditorias pertinentes. O salto de Base02 para Base04 reflete os arquivos disponíveis; não há `Base03.ipynb` neste acervo.
4. **Caracterizar as operações:** usar a correção de UF/finalidade/financeiro V2 para a seção 5.4; conferir as chaves por ordem, os formatos de datas, o corte e a cobertura dos arquivos de saldos.
5. **Executar os cruzamentos necessários:** cada notebook de interseção parte da base com `id_gleba2` e da camada correspondente. Usar o resultado **expandido** nas análises V2; o resultado único por geometria não conserva, sozinho, todos os vínculos administrativos.
6. **Gerar relatórios e complementos:** utilizar as versões sem deduplicação disponíveis, seguidas dos notebooks de tabelas/mapas. Para embargos, a análise temporal precede o complemento cartográfico. Para conservação, usar a correção UC/ZA antes de comparar a síntese com a dissertação.
7. **Organizar o produto e documentar as revisões:** o organizador trabalha sobre resultados existentes. As duas revisões de dicionário têm entradas e hashes específicos; a segunda pode ser aplicada diretamente ao pacote compatível indicado nela. Não remover controles de integridade para forçar a execução.
8. **Conferir os resultados:** comparar unidades de contagem, totais, datas, áreas, arquivos exportados e eventuais erros. Registrar versões das bibliotecas, parâmetros e origens. Não alterar valores esperados apenas para fazer uma conferência passar.

Os complementos de florestas públicas e conservação informam entradas de dezenas de GB. Leitura em blocos reduz o uso de memória, mas não elimina tempo de leitura nem a memória necessária às uniões geométricas. Os leitores que carregam o CSV inteiro também podem exigir bastante RAM.

