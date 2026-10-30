# Dissertação — Crédito rural no Cerrado

Repositório dos notebooks da pesquisa sobre observância dos impedimentos socioambientais no crédito rural no Cerrado (2021–2025).

## Notebook incorporado

| Arquivo | Finalidade | Evidência de execução | Última execução no Colab |
| --- | --- | --- | --- |
| [Relatório unificado — Quilombolas](notebooks/quilombolas/Relatorio_Unificado_SICOR_Quilombolas_id_gleba2.ipynb) | Análise SICOR × Territórios Quilombolas por `id_gleba2`, com tabelas, gráficos, mapas e relatório Word | Há saídas salvas; a execução registrada termina com erro na etapa 5 | Não identificável nos metadados fornecidos |

## Origem e preservação

Notebook recuperado do conteúdo JSON integral do anexo `Texto colado(4).txt`, enviado em 30/10/2026. O anexo contém um notebook, com 17 células (15 de código e 2 de texto), e não uma lista de notebooks.

O conteúdo original foi preservado no arquivo `.ipynb`, incluindo código, parâmetros, metadados e saídas. A inclusão no repositório não comprova que esta versão tenha produzido os resultados finais da dissertação. A presença de saídas demonstra execução parcial, mas não permite determinar a data da última execução.

## Uso no Google Colab

1. Abra o arquivo `.ipynb` no Google Colab, usando a opção de abrir um notebook do GitHub, ou baixe-o e faça o upload. O acesso direto depende da autorização do Colab para este repositório privado.
2. Execute a célula de preparação do ambiente e autorize a montagem do seu Google Drive.
3. Na etapa 2, ajuste `ARQUIVO_ENTRADA` para a base CSV disponível no seu Drive.
4. Confira as colunas identificadas na etapa 4 e resolva a pendência de identificação do período indicada abaixo antes de executar as etapas posteriores.
5. Execute as células na ordem.

A entrada configurada no original é `intersecao_quilombolas_unica_por_id_gleba2.csv`, na pasta de resultados por `id_gleba2` do Drive. As bases de entrada não estão incluídas neste repositório.

O notebook instala dependências geoespaciais e de geração de Word, utiliza malhas do `geobr` (ou caminhos locais configurados) e calcula áreas em `EPSG:5880`.

## Produtos previstos

A pasta `relatorio_unificado_quilombolas_id_gleba2`, criada junto ao CSV de entrada, recebe mapas, gráficos e histogramas, tabelas CSV, bases analíticas, inventário de produtos e o arquivo `relatorio_unificado_sicor_quilombolas_2021_2025.docx`.

Esses produtos são previstos pelo código; a cópia anexada não contém evidência de conclusão da geração.

## Estado da cópia recebida

- A etapa 4 registra a leitura de 303 linhas e 32 colunas.
- A etapa 5 contém um `ValueError`: “Não foi possível identificar o período. Acrescente o nome correto da coluna anual aos candidatos de COLUNA_ANO.”
- A instalação registra conflito entre a versão de pandas exigida pelo ambiente Colab e a versão instalada.
- As etapas posteriores não apresentam saídas salvas.

Foi conferida a estrutura JSON básica do notebook para arquivamento. O fluxo não foi reexecutado com as bases da pesquisa e o código não foi corrigido nesta importação.

## Interpretação dos resultados

O notebook distingue glebas, operações, ocorrências espaciais, área acumulada e área física única. Sobreposição espacial exige análise complementar e não comprova, isoladamente, irregularidade na concessão de crédito.
