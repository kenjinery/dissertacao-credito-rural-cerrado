# Crédito rural no Cerrado — notebooks da dissertação

Repositório dos notebooks de apoio à pesquisa sobre observância dos impedimentos socioambientais no crédito rural no bioma Cerrado, no período de **2021 a 2025**. O trabalho combina análise documental, estatística descritiva e análise espacial vetorial de glebas do SICOR e bases territoriais oficiais.

**Autor:** Mario Kenji Fernandes Nery  
**Orientador:** Prof. Dr. Remis Balaniuk  
**Programa:** Mestrado em Governança, Tecnologia e Inovação — Universidade Católica de Brasília, 2026.

Este guia relaciona os **43 notebooks** disponíveis — **42 na raiz e 1 em `notebooks/quilombolas/`** — aos procedimentos e resultados da dissertação. O acervo contém preparação de bases, cruzamentos, relatórios V2, complementos, auditorias e versões anteriores. Não representa uma sequência de 43 arquivos que devam ser executados integralmente.

## Referência documental e alcance da conferência

A correspondência foi revista em **30/10/2026**, tomando como referência a última versão disponibilizada para consulta: **`Dissertacao - Mario - Kenji 20261029 v17(3).docx`**, de 29/10/2026. Foram consultados o texto metodológico, as seções de resultados pertinentes e a síntese da Tabela 29, além do código, das células de documentação e das saídas salvas dos notebooks no commit [`1b28906`](https://github.com/kenjinery/dissertacao-credito-rural-cerrado/tree/1b28906a629f803161ee684962daf8ec023ceab8).

**A conferência é documental e estática:** não houve reexecução dos cruzamentos nem recálculo das bases externas. Correspondência de método e de totais salvos é evidência de compatibilidade, mas não comprova, sozinha, que cada cópia seja exatamente a que gerou todas as tabelas e figuras finais. Arquivos sem saídas não podem ser classificados como “não utilizados” apenas por essa ausência.

Os nomes originais foram preservados. Em particular, os notebooks que citam **5.2.1** no nome ou no texto sobre gráficos financeiros correspondem, na versão consultada, à **seção 5.4**. A seção **5.2.1** atual trata da distinção entre unidades da base.

## Correspondência com as sete etapas da pesquisa

| Etapa da seção 4.3 | Procedimento e notebooks relacionados | Apresentação na dissertação |
| --- | --- | --- |
| 1. Análise normativa e institucional | Trabalho documental e bibliográfico; os notebooks não substituem essa análise. | Capítulos 2–3 e seção 5.1 |
| 2. Obtenção e preparação do SICOR | Base01, Base02, leitores, auditoria geométrica e mapas do Cerrado. | Seção 5.2 |
| 3. Enriquecimento e identificação das glebas | Base04, Base05, conferência da base e auditoria de repetições. | Seção 5.3 |
| 4. Caracterização estatística e financeira | Correção de UF/finalidade/financeiro V2 e gráficos. | Seção 5.4 |
| 5. Cruzamento com bases territoriais | Sete notebooks de interseção, relatórios V2 e complementos cartográficos. | Subseções 5.5.1–5.5.7 |
| 6. Qualificação temporal e normativa | Análise temporal dos embargos e leitura dos atributos revisados; qualificação jurídica depende de exame documental. | Seção 5.5, especialmente 5.5.5 |
| 7. Síntese e discussão | Correção UC/ZA, documentação do produto e comparação dos resultados; discussão elaborada no texto da dissertação. | Seção 5.6 e capítulo 6 |

## Unidades de análise e regras de interpretação

| Campo ou medida | Significado e regra |
| --- | --- |
| Registro territorial | Linha da base; não equivale a operação, produtor ou imóvel distinto. |
| `REF_BACEN` | Referência administrativa de uma operação. |
| `REF_BACEN + NU_ORDEM` | Chave da ordem/destinação. Na base territorial, conferir o campo correspondente `NU_ORDEM_GLEBA`; número de ordem isolado não é chave global. |
| `ID_GLEBA` | Identificador sequencial atribuído na pesquisa a cada registro territorial. |
| `id_gleba2` / `ID_GLEBA2` | Identificador derivado do SHA-256 do texto WKT exato de `GT_GEOMETRIA`, com atribuição do menor `ID_GLEBA` do grupo. Não há normalização geométrica; WKT diferentes podem representar a mesma área. |
| `ANO_BASE` | Ano do arquivo de origem; não confundir automaticamente com o ano de emissão da operação. |
| `DT_EMISSAO` | Data da operação usada na caracterização por emissão e na comparação temporal dos embargos. |
| Interseção única por ID | Resultado geométrico por `id_gleba2 × feição territorial`, posteriormente expandido aos vínculos administrativos. |
| Linhas expandidas | Preservam as combinações entre registros administrativos e feições intersectadas. São a unidade principal dos resultados territoriais V2. |
| Área acumulada | Soma das áreas nas linhas consideradas; pode repetir a mesma superfície. |
| União geométrica | Superfície das interseções sem repetir trechos sobrepostos, calculada no recorte indicado. |
| Valor financeiro da seção 5.4 | `VL_PARC_CREDITO` considerado uma vez por ordem; não equivale ao total desembolsado. |
| Valor financeiro das interseções | Soma dos valores presentes nas linhas expandidas; pode repetir ordens e operações. Não mede crédito irregular. |

O cálculo espacial por geometria distinta reduz processamento; ele **não autoriza eliminar os vínculos administrativos** na apresentação das linhas expandidas. O recorte municipal pode dividir uma ocorrência em várias partes: `base_partes_municipais_sem_deduplicacao.csv` não deve substituir a base de registros nas contagens gerais.

As rotinas de interseção usam `EPSG:4326` para as geometrias de origem e `EPSG:5880` para cálculo de áreas, convertidas de m² para hectares. Reparo geométrico, auditoria da geometria original e ajuste exclusivo de desenho são procedimentos distintos.

## Inventário dos 43 notebooks

As tabelas abaixo indicam a função observada de cada arquivo e sua relação com o texto. “Histórico” designa uma abordagem anterior ou alternativa identificada no código; não significa comprovação de que o arquivo jamais tenha sido usado.

### Preparação e conferência das bases

| Notebook | Seção de referência | Função e estado observado |
| --- | --- | --- |
| [Base01.ipynb](Base01.ipynb) | 5.2.2 | Seleciona os arquivos anuais de glebas e gera recortes do Cerrado e resumo. O parâmetro salvo é `within`; conferir a divergência com a descrição de inclusão parcial na dissertação. |
| [Base02.ipynb](Base02.ipynb) | 5.2.1 e 5.3.1 | Consolida os cinco CSVs anuais, valida contagens e cria `ID_GLEBA` sequencial. Saída salva de 480.679 linhas; a tabela de 377.465 na introdução está desatualizada. |
| [Base04.ipynb](Base04.ipynb) | 5.2.1 e 5.3 | Enriquece os registros territoriais por referência e ordem, incorpora tabelas de domínio e preserva 480.679 linhas nas saídas salvas. |
| [Base05_criar_ID_GLEBA2.ipynb](Base05_criar_ID_GLEBA2.ipynb) | 5.3.1 | Calcula SHA-256 do WKT exato e atribui o menor `ID_GLEBA` ao grupo. Saídas salvas: 395.575 `ID_GLEBA2`, sem eliminação de linhas. |
| [notebook_ler_sicor_cerrado_2021_2025.ipynb](notebook_ler_sicor_cerrado_2021_2025.ipynb) | 5.2 — apoio | Inspeciona o CSV consolidado: colunas, identificadores, ausências e distribuição anual. |
| [Cópia de notebook_ler_sicor_cerrado_2021_2025 - enriquecido.ipynb](C%C3%B3pia%20de%20notebook_ler_sicor_cerrado_2021_2025%20-%20enriquecido.ipynb) | 5.3 — apoio | Variante de leitura apontada para a base enriquecida; serve à inspeção, não substitui o enriquecimento. |
| [notebook_verificar_base04_enriquecido.ipynb](notebook_verificar_base04_enriquecido.ipynb) | 5.3 — apoio | Confere quantidade de registros e colunas do arquivo produzido pelo Base04. |

### Auditorias, mapas de localização e caracterização financeira

| Notebook | Seção de referência | Função e estado observado |
| --- | --- | --- |
| [Auditoria_Geometrias_Invalidas_por_Ano (1).ipynb](Auditoria_Geometrias_Invalidas_por_Ano%20%281%29.ipynb) | 5.2.3 | Auditoria configurada dos WKT nos arquivos anuais do Cerrado e da entrada nacional; diagnósticos separados, sem reparação nem deduplicação. |
| [Auditoria_Geometrias_Invalidas_por_Ano.ipynb](Auditoria_Geometrias_Invalidas_por_Ano.ipynb) | 5.2.3 — alternativa | Modelo genérico de auditoria de arquivos vetoriais, com caminhos a preencher; sem saídas salvas. |
| [Auditoria_Repeticoes_ID_GLEBA2.ipynb](Auditoria_Repeticoes_ID_GLEBA2.ipynb) | 5.3.1 | Audita a relação entre IDs e WKT, repetições por ano, referência e ordem. Contém resultados compatíveis com os totais da dissertação e também um erro salvo de montagem do Drive. |
| [Mapas_Cerrado_Dissertacao.ipynb](Mapas_Cerrado_Dissertacao.ipynb) | 5.2.2; Figuras 6–7 | Produz mapas do Brasil/Cerrado e Cerrado/UFs, com Biomas IBGE 2019 e malha estadual 2024 na configuração padrão. |
| [SICOR_Cerrado_Correcao_UF_Finalidade_Financeiro_v2.ipynb](SICOR_Cerrado_Correcao_UF_Finalidade_Financeiro_v2.ipynb) | 5.4.1–5.4.6; Figuras 8–13 | Corrige UF administrativa, finalidade e instrumento; integra liberações, desclassificações e saldos. Consolida valores por ordem. Corte configurado: 16/09/2026. |
| [SICOR_Cerrado_Graficos_Secao_5_2_1.ipynb](SICOR_Cerrado_Graficos_Secao_5_2_1.ipynb) | 5.4 — complemento | Gera gráficos e tabelas da Base04, com valores por ordem. O nome conserva a antiga seção 5.2.1; para a integração financeira, consultar o notebook de correção V2. |

### Cruzamentos espaciais por id_gleba2

| Notebook | Seção de referência | Função e estado observado |
| --- | --- | --- |
| [intersecao_sicor_terras_indigenas_por_id_gleba2.ipynb](intersecao_sicor_terras_indigenas_por_id_gleba2.ipynb) | 5.3.2 e 5.5.1 | SICOR × `tis_poligonais.shp`; interseção única por geometria/feição e expansão para os vínculos administrativos. |
| [intersecao_sicor_quilombolas_por_id_gleba2.ipynb](intersecao_sicor_quilombolas_por_id_gleba2.ipynb) | 5.3.2 e 5.5.2 | SICOR × áreas quilombolas; gera CSV único, CSV expandido e resumo por identificador. |
| [intersecao_sicor_cnfp_por_id_gleba2.ipynb](intersecao_sicor_cnfp_por_id_gleba2.ipynb) | 5.3.2 e 5.5.3 | SICOR × `CNFP_2025.shp`; preserva atributos da camada com prefixo `FP_`. |
| [intersecao_sicor_assentamentos_por_id_gleba2.ipynb](intersecao_sicor_assentamentos_por_id_gleba2.ipynb) | 5.3.2 e 5.5.4 | SICOR × assentamentos; gera interseções e expansão. A camada é de contextualização territorial, não impedimento automático. |
| [intersecao_sicor_embargos_ibama_por_id_gleba2.ipynb](intersecao_sicor_embargos_ibama_por_id_gleba2.ipynb) | 5.3.2 e 5.5.5 | SICOR × embargos federais do Ibama; preserva atributos `EMB_` e descarta contatos sem área positiva. |
| [intersecao_sicor_unidades_conservacao_por_id_gleba2.ipynb](intersecao_sicor_unidades_conservacao_por_id_gleba2.ipynb) | 5.3.2 e 5.5.6 | SICOR × `ucs.shp`; o resultado requer a separação posterior entre limites de UC e zonas de amortecimento. |
| [intersecao_sicor_cerrado_2021_2025_sicar_suspensos_por_id_gleba2.ipynb](intersecao_sicor_cerrado_2021_2025_sicar_suspensos_por_id_gleba2.ipynb) | 5.5.7 — requer conferência | Cruza arquivos estaduais do SICAR. O filtro salvo exige `SUSPENSO`, enquanto a dissertação e as saídas V2 usam `SU`; ver a pendência de compatibilidade abaixo. |

### Relatórios com preservação das linhas expandidas

| Notebook | Seção de referência | Função e estado observado |
| --- | --- | --- |
| [notebook_unificado_terras_indigenas_sem_deduplicacao_versao_2.ipynb](notebook_unificado_terras_indigenas_sem_deduplicacao_versao_2.ipynb) | 5.5.1 | Relatório V2 de terras indígenas, com base completa, registros espaciais, partes municipais, tabelas, gráficos e Word. Saídas registram 660 linhas. |
| [notebook_unificado_assentamentos_sem_deduplicacao_versao_2.ipynb](notebook_unificado_assentamentos_sem_deduplicacao_versao_2.ipynb) | 5.5.4 | Relatório V2 de assentamentos; preserva linhas e exporta bases analíticas e relatório. Saídas registram 33.044 linhas. |
| [notebook_unificado_sicar_suspensos_sem_deduplicacao_versao_2.ipynb](notebook_unificado_sicar_suspensos_sem_deduplicacao_versao_2.ipynb) | 5.5.7 | Relatório V2 do SICAR suspenso; saídas registram 530 linhas e atributos com status `SU`. Aplicar também a revisão dos campos auxiliares. |
| [notebook_unificado_unidades_conservacao_sem_deduplicacao_versao_2.ipynb](notebook_unificado_unidades_conservacao_sem_deduplicacao_versao_2.ipynb) | 5.5.6 — antes da separação UC/ZA | Relatório V2 de conservação; saídas registram 18.617 linhas combinadas. Complementar obrigatoriamente com a correção UC/ZA para comparar com a síntese final. |

### Tabelas, mapas de detalhe e qualificação temporal

| Notebook | Seção de referência | Função e estado observado |
| --- | --- | --- |
| [Terras_Indigenas_5_5_1_Tabelas_e_Mapas.ipynb](Terras_Indigenas_5_5_1_Tabelas_e_Mapas.ipynb) | 5.5.1 | Complemento V2 de terras indígenas: tabela integral, mapas geral/estadual e detalhes. Saídas registram 660 linhas, 554 glebas e 43 unidades. |
| [Territorios_Quilombolas_5_5_2_Tabelas_e_Mapas.ipynb](Territorios_Quilombolas_5_5_2_Tabelas_e_Mapas.ipynb) | 5.5.2 | Complemento V2 de quilombolas: tabelas e mapas de detalhe. Saídas registram 368 linhas, 300 glebas e 43 unidades. |
| [Florestas_Publicas_5_5_3_Tabelas_e_Mapas.ipynb](Florestas_Publicas_5_5_3_Tabelas_e_Mapas.ipynb) | 5.5.3 | Complemento V2 de florestas públicas, com leitura em blocos/cache e tabelas por unidade. Saídas: 33.984 linhas, 25.284 glebas e 1.766 unidades. |
| [Assentamentos_5_5_4_Tabelas_e_Mapas.ipynb](Assentamentos_5_5_4_Tabelas_e_Mapas.ipynb) | 5.5.4 | Complemento V2 de assentamentos; distingue assentamento de categoria de produtor. Saídas: 33.044 linhas, 24.615 glebas e 1.568 unidades. |
| [analise_temporal_embargos_sicor_cerrado_2021_2025.ipynb](analise_temporal_embargos_sicor_cerrado_2021_2025.ipynb) | 5.5.5 e 5.6.1 | Compara emissão e imposição do embargo, mantendo 931 linhas. Saídas: 400 com embargo anterior ou na mesma data e 531 posteriores; a dissertação informa zero coincidências. |
| [Embargos_5_5_5_Tabelas_Mapas_e_Analise_Temporal.ipynb](Embargos_5_5_5_Tabelas_Mapas_e_Analise_Temporal.ipynb) | 5.5.5 | Vincula a base espacial à análise temporal e produz tabelas por polígono, gráficos e mapas. Saídas: 931 linhas, 626 glebas e 388 polígonos. |
| [Unidades_Conservacao_5_5_6_Tabelas_e_Mapas.ipynb](Unidades_Conservacao_5_5_6_Tabelas_e_Mapas.ipynb) | 5.5.6 — versão anterior do complemento | Tabelas e mapas de conservação com UC/ZA ainda agregados. Guarda erro de geometria vazia ou não poligonal para `territorio=607`. |
| [Unidades_Conservacao_5_5_6_Tabelas_e_Mapas (1).ipynb](Unidades_Conservacao_5_5_6_Tabelas_e_Mapas%20%281%29.ipynb) | 5.5.6 — complemento com ajuste cartográfico | Variante que aceita componentes poligonais de `GeometryCollection` para desenho e contém saídas dos mapas. Ainda agrega 18.617 linhas; não substitui a correção UC/ZA. |
| [Corrigir_Resultados_UC_ZA_Cerrado.ipynb](Corrigir_Resultados_UC_ZA_Cerrado.ipynb) | 5.5.6 e 5.6; Tabelas 26–29, conforme o produto | Separa `UC_LIMITE=uc` e `UC_LIMITE=za`, recalcula uniões e gera tabelas/mapas. Saídas registram conclusão, com 18.493 linhas de UC e 124 de ZA. |

### Organização e documentação do produto

| Notebook | Seção de referência | Função e estado observado |
| --- | --- | --- |
| [Organizar_Produto_Dissertacao_Cerrado.ipynb](Organizar_Produto_Dissertacao_Cerrado.ipynb) | Produto de apoio; 5.6 | Organiza CSVs leves, inventário, dicionário, verificações e ZIP a partir de resultados existentes. Mantém as visões de 931 e 37 linhas de embargos; contém erro salvo de caminho. |
| [Revisar_Dicionario_Produto_Cerrado.ipynb](Revisar_Dicionario_Produto_Cerrado.ipynb) | Documentação dos atributos | Primeira revisão do dicionário e dos campos auxiliares; registra 149 definições ainda pendentes no pacote de referência. |
| [Revisar_Dicionario_Produto_Cerrado (1).ipynb](Revisar_Dicionario_Produto_Cerrado%20%281%29.ipynb) | Documentação dos atributos; 5.5–5.6 | Segunda revisão: trata as 149 pendências, mantém 37 parcialmente esclarecidas ou não confirmadas e cria vistas de apoio, inclusive UC/ZA. Não recalcula as uniões geométricas. |

### Versões anteriores e alternativas de relatório

| Notebook | Seção de referência | Função e estado observado |
| --- | --- | --- |
| [notebook_unificado_terras_indigenas_id_gleba2.ipynb](notebook_unificado_terras_indigenas_id_gleba2.ipynb) | Histórico de 5.5.1 | Relatório deduplicado por `id_gleba2 × TI`; guarda erro de obtenção de malha pelo `geobr`. |
| [notebook_unificado_terras_indigenas_id_gleba2 (1).ipynb](notebook_unificado_terras_indigenas_id_gleba2%20%281%29.ipynb) | Histórico de 5.5.1 | Variante com saídas do relatório deduplicado. Sua unidade principal difere das linhas expandidas adotadas na versão final. |
| [notebook_unificado_terras_indigenas_id_gleba2 (2).ipynb](notebook_unificado_terras_indigenas_id_gleba2%20%282%29.ipynb) | Histórico de 5.5.1 | Outra variante deduplicada; guarda `KeyError: index_right`. O sufixo `(2)` não comprova que seja a versão final. |
| [notebook_unificado_assentamentos_id_gleba2.ipynb](notebook_unificado_assentamentos_id_gleba2.ipynb) | Histórico de 5.5.4 | Relatório que deduplica ocorrências por geometria/assentamento; não usar suas contagens como equivalentes às da V2. |
| [notebook_unificado_sicar_suspensos_id_gleba2.ipynb](notebook_unificado_sicar_suspensos_id_gleba2.ipynb) | Histórico de 5.5.7 | Relatório que deduplica ocorrências por geometria/cadastro; distinto da V2 sem deduplicação. |
| [notebook_unificado_unidades_conservacao_id_gleba2.ipynb](notebook_unificado_unidades_conservacao_id_gleba2.ipynb) | Histórico de 5.5.6 | Relatório deduplicado por geometria/unidade, com saídas parciais; não corresponde à síntese final UC/ZA. |
| [notebooks/quilombolas/Relatorio_Unificado_SICOR_Quilombolas_id_gleba2.ipynb](notebooks/quilombolas/Relatorio_Unificado_SICOR_Quilombolas_id_gleba2.ipynb) | Histórico de 5.5.2 | Cópia recuperada do anexo `Texto colado(4).txt`. Aponta para CSV único, registra 303 linhas e erro de identificação do período; não substitui os 368 registros expandidos da dissertação. |

## Totais de referência da dissertação

Estes números são referências do **texto consultado**, não resultados de uma nova execução deste repositório. As saídas salvas de Base02, Base04, Base05, auditoria de repetições e correção financeira apresentam contagens compatíveis com os principais totais da base.

| Indicador | Total | Referência |
| --- | ---: | --- |
| Registros territoriais preservados | 480.679 | Tabela 11 |
| Operações com vínculo territorial | 334.166 | Tabela 11 |
| Ordens na consolidação administrativa | 401.294 | Tabela 11 |
| Ordens com vínculo territorial | 374.949 | Tabela 11 |
| Ordens sem correspondência territorial na integração | 26.345 | Tabela 11 |
| Representações WKT distintas | 395.575 | Tabela 11 e seção 5.3.1 |
| Valor nominal consolidado uma vez por ordem territorial | R$ 130.187.076.962,47 | Seção 5.4 |

As ordens sem correspondência territorial não participam dos cruzamentos espaciais. Os indicadores acima não devem ser somados.

### Síntese territorial da Tabela 29

| Camada ou recorte | Registros | Glebas distintas | Unidades da camada | União geométrica (ha) | Valor somado nas linhas (R$) |
| --- | ---: | ---: | ---: | ---: | ---: |
| Terras indígenas | 660 | 554 | 43 | 23.590,12 | 464.826.507,95 |
| Territórios quilombolas | 368 | 300 | 43 | 9.367,44 | 184.451.603,64 |
| Florestas públicas | 33.984 | 25.284 | 1.766 | 232.002,78 | 12.321.219.185,59 |
| Assentamentos | 33.044 | 24.615 | 1.568 | 291.757,19 | 5.892.958.982,97 |
| Embargos ambientais federais | 931 | 626 | 388 | 11.122,34 | 1.392.013.462,24 |
| Unidades de conservação — limites | 18.493 | 14.577 | 206 | 787.963,48 | 21.505.054.244,05 |
| Zonas de amortecimento | 124 | 100 | 2 | 4.844,63 | 101.158.586,29 |
| CAR/SICAR — status SU | 530 | 377 | 214 | 7.775,62 | 162.165.249,15 |

**Não somar as camadas como conjuntos independentes.** Uma gleba, operação ou superfície pode aparecer em mais de uma camada. A dissertação informa que UC e ZA compartilham 56 glebas, 64 referências BACEN e 2.489,12 ha; uma unidade tem ocorrências nos dois recortes. As somas financeiras acima não equivalem a valores de contratos distintos, desembolsos ou dano apurado.

Nos embargos, a seção 5.6.1 distingue **400 linhas com embargo anterior à emissão** e **531 posteriores**, sem coincidências de data. Das 400 anteriores, **37 linhas** correspondem a operações emitidas a partir de 02/01/2024, abrangendo **31 referências BACEN**, 34 glebas e 25 polígonos de embargo. Esse subconjunto é uma seleção para apuração, não 37 operações comprovadamente irregulares.

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

As datas de obtenção e edições das fontes devem acompanhar os arquivos usados; a Tabela 8 da dissertação documenta as referências adotadas na pesquisa. Baixar uma versão atual de uma camada pode modificar os resultados de uma reprodução histórica.

Os CSVs e vetores de entrada, os pacotes completos de resultados e o Word da dissertação **não estão incluídos neste inventário do repositório**. Os arquivos `.ipynb` contêm algumas saídas incorporadas. Caminhos e IDs do Drive presentes no código não concedem acesso aos dados.

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

## Divergências e lacunas identificadas

Esta seção registra diferenças observáveis entre o acervo e o texto de referência. A revisão do README não modificou o código nem os resultados dos notebooks.

| Ponto | Evidência observada | Consequência para reprodução |
| --- | --- | --- |
| Seleção territorial no Base01 | `CRITERIO_ESPACIAL = "within"`; o texto das seções 4.3 e 5.2.2 descreve glebas total ou parcialmente inseridas. O arquivo não tem saídas salvas. | Confirmar o predicado efetivamente utilizado na geração dos arquivos anuais. Não afirmar que a configuração salva reproduz a inclusão parcial nem trocar o parâmetro silenciosamente. |
| Filtro do SICAR | O notebook de interseção compara `ind_status` normalizado com `SUSPENSO`. Não há conversão de `SU` para esse texto. A dissertação e saídas salvas do relatório V2 apresentam `SU`. | Conferir os valores reais da camada e recuperar/documentar a configuração que gerou as interseções. Uma camada codificada apenas como `SU` não passa pelo filtro atual. |
| Relatórios V2 ausentes | Há relatórios unificados V2 de TI, assentamentos, SICAR e UC. Não foram encontrados os equivalentes V2 de quilombolas, florestas públicas e embargos, embora os complementos usem produtos dessas versões. | O acervo permite consultar os complementos e os cruzamentos, mas ainda não contém todos os geradores intermediários de relatórios mencionados nas dependências. O relatório antigo de quilombolas não supre essa falta. |
| UC e ZA agregadas nas rotinas anteriores | O unificado V2 e os dois complementos de conservação trabalham com 18.617 linhas combinadas. O complemento com `(1)` ajusta o desenho de coleções geométricas, mas não separa os recortes. | Para a síntese final, consultar `Corrigir_Resultados_UC_ZA_Cerrado.ipynb`: 18.493 UC e 124 ZA. Não apresentar 18.617 como total de linhas apenas no interior das UCs. |
| Texto antigo no Base02 | A introdução ainda apresenta 377.465 linhas; o código calcula os totais a partir dos arquivos e as saídas registram 480.679. | Usar a validação dos arquivos efetivos e documentar a desatualização da introdução. |
| Relatórios deduplicados | Os relatórios antigos reduzem ocorrências por geometria/unidade; a dissertação final preserva linhas expandidas. | Não substituir tabelas V2 por resultados deduplicados nem misturar os denominadores. |
| Campos auxiliares e dicionário | A segunda revisão trata seis alertas e mantém 37 definições parcialmente esclarecidas ou ainda pendentes no pacote específico. | Consultar o dicionário revisado e as vistas de apoio; nomes de campos auxiliares não asseguram seu significado. Por exemplo, tipo de imóvel CAR, porte do produtor e UF cadastral são dimensões distintas. |
| Rastreabilidade da execução | Há saídas parciais, contadores ausentes e erros guardados junto de resultados posteriores. Não há registro único que vincule todas as figuras finais a uma execução integral do acervo. | Preservar logs, versões e hashes dos insumos/produtos para comprovar a reprodução; não inferir “última execução” apenas pelo nome ou pela data de alteração do notebook. |

### Erros preservados nas cópias

Foram identificados outputs de erro em **6 notebooks**. São registros históricos das células, não diagnósticos de uma nova execução. Em particular, a auditoria de repetições também contém resultados posteriores compatíveis com a dissertação.

| Notebook | Erro salvo |
| --- | --- |
| `Auditoria_Repeticoes_ID_GLEBA2.ipynb` | `ValueError: mount failed`. |
| `Organizar_Produto_Dissertacao_Cerrado.ipynb` | Pasta de entrada não encontrada; verificar `RAIZ`. |
| `Unidades_Conservacao_5_5_6_Tabelas_e_Mapas.ipynb` | Geometria vazia ou não poligonal em `territorio=607`. |
| `notebook_unificado_terras_indigenas_id_gleba2.ipynb` | Erro de obtenção de arquivo pelo `geobr`. |
| `notebook_unificado_terras_indigenas_id_gleba2 (2).ipynb` | `KeyError: index_right`. |
| `notebooks/quilombolas/Relatorio_Unificado_SICOR_Quilombolas_id_gleba2.ipynb` | Coluna do período não identificada. |

**41 arquivos contêm alguma saída salva**; isso pode significar apenas instalação ou montagem do Drive. **Base01** e o modelo genérico **Auditoria_Geometrias_Invalidas_por_Ano** não contêm saídas. Nenhuma dessas classificações certifica execução integral ou uso na versão final.

## Alcance dos achados

As interseções são evidências territoriais para triagem. Não comprovam, isoladamente, irregularidade, domínio do imóvel, identidade do beneficiário ou vigência histórica de uma restrição. A interpretação deve considerar a norma aplicável à data da operação, os atributos e a edição da camada, os atos administrativos e as exceções pertinentes.

Assentamentos são uma camada de contextualização; a presença da gleba neles não é impedimento automático. Categorias de UC, sobretudo APAs, precisam de análise própria. A anterioridade de um embargo não demonstra sua vigência na contratação, e o status SU da base do CAR não informa, por si só, quando a suspensão começou.

O universo é o subconjunto do SICOR com informações territoriais públicas disponíveis e vínculos utilizáveis. Ele não representa uma amostra aleatória de todo o crédito rural do Cerrado. A abordagem documentada é vetorial e descritiva; não deve ser apresentada como classificação automática de desmatamento, modelagem causal ou certificação jurídica de operações.

## Referência e atribuição

Para citar os procedimentos, identificar a dissertação de **Mario Kenji Fernandes Nery**, Universidade Católica de Brasília, **2026**, a versão consultada e o commit dos notebooks utilizado. O título da capa da versão de referência é:

> Em que medida as concessões de crédito rural no bioma Cerrado têm observado os impedimentos socioambientais e climáticos previstos na legislação, e em quais situações essas regras vêm sendo violadas, à luz de evidências produzidas por geoprocessamento e análise espacial.

As bases devem ser atribuídas aos respectivos órgãos produtores. A dissertação reconhece o Projeto Panoptes e o material GeoCreditoRural como referências metodológicas para organização dos dados e procedimentos vetoriais.
