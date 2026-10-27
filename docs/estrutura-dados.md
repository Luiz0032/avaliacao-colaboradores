# Estrutura de dados (SharePoint)

O app usa 9 listas do SharePoint, apontadas por variáveis de ambiente. As listas de cadastro (colaboradores, cargos e departamentos) podem ficar em um site diferente das listas de avaliação — por isso existem duas variáveis de site.

| Variável de ambiente | Tipo | Aponta para |
|---|---|---|
| `lf_SiteAppAvaliacao` | Site | Site das listas de avaliação |
| `lf_SiteBase` | Site | Site das listas de cadastro |
| `lf_BaseAvaliacoes2` | Lista | BaseAvaliacoes |
| `lf_BaseAvaliacoesItens` | Lista | BaseAvaliacoesItens |
| `lf_AvaliacoesColaboradores` | Lista | AvaliacoesColaboradores |
| `lf_AvaliacoesColaboradoresRespostas` | Lista | AvaliacoesColaboradoresRespostas |
| `lf_MetasAvaliacaoColaboradores` | Lista | MetasAvaliacaoColaboradores |
| `lf_StatusAvaliacoes` | Lista | StatusAvaliacoes |
| `lf_BaseColaboradores` | Lista | BaseColaboradores *(site base)* |
| `lf_BaseCargos` | Lista | BaseCargos *(site base)* |
| `lf_BaseDptos` | Lista | BaseDptos *(site base)* |

## Listas de cadastro

**BaseColaboradores**
| Coluna | Tipo |
|---|---|
| NomeColaborador | Texto |
| EmailColaborador | Texto |
| CodColaborador | Texto |
| FotoUser | Imagem |
| CodCargo | Texto |
| CodDpto | Texto |
| CodGestor | Texto |
| Status | Escolha |

**BaseCargos** — `CodCargo` (Texto), `NomeCargo` (Texto)

**BaseDptos** — `CodDpto` (Texto), `NomeDpto` (Texto)

## Listas de avaliação

**BaseAvaliacoes** — o ciclo de avaliação
| Coluna | Tipo |
|---|---|
| NomeAvaliacao | Texto |
| DescricaoAvaliacao | Texto (várias linhas) |
| PeriodoAvaliacao | Texto |
| DataAberturaDefinicaoMetas | Data |
| DataLimiteDefinicaoMetas | Data |
| DataAberturaAvaliacao | Data |
| DataLimiteAvaliacao | Data |
| Status | Escolha |

**BaseAvaliacoesItens** — competências avaliadas no ciclo
| Coluna | Tipo |
|---|---|
| IdBaseAvaliacao | Número |
| TituloItem | Texto |
| DescricaoItem | Texto (várias linhas) |
| OrdemItem | Número |
| Categoria | Escolha |

**AvaliacoesColaboradores** — uma linha por colaborador no ciclo
| Coluna | Tipo |
|---|---|
| IdBaseAvaliacao | Número |
| CodColaborador | Número |
| CodGestor | Número |
| Cargo | Número |
| Dpto | Número |
| Status | Número (10 a 50) |
| TerminoDefinicaoMetas | Data |
| TerminoAvaliacaoColab | Data |
| TerminoAvaliacaoGestor | Data |
| TerminoAvaliacaoCalibracao | Data |
| JaFezPrimeiroAcesso | Sim/Não |
| AvaliacaoColabConcluida | Sim/Não |
| AvaliacaoGestorConcluida | Sim/Não |

**AvaliacoesColaboradoresRespostas** — notas por competência
| Coluna | Tipo |
|---|---|
| IdBaseAvaliacao | Número |
| IdAvaliacao | Número |
| IdItem | Número |
| CategoriaPergunta | Texto |
| RespostaColab | Número |
| RespostaGestor | Número |
| RespostaCalibrada | Número |
| ComentarioColab | Texto (várias linhas) |
| ComentarioGestor | Texto (várias linhas) |

**MetasAvaliacaoColaboradores** — metas individuais com peso
| Coluna | Tipo |
|---|---|
| IdBaseAvaliacao | Número |
| IdAvaliacao | Número |
| CodColab | Número |
| TituloMeta | Texto |
| DescricaoMeta | Texto (várias linhas) |
| Peso | Número |
| Resposta | Número |
| ComentarioColab | Texto (várias linhas) |
| ComentarioGestor | Texto (várias linhas) |

**StatusAvaliacoes** — `Ordem` (Número), `NomeStatus` (Texto)

Valores usados pelo app:

| Ordem | Etapa |
|---|---|
| 10 | Convidado, ainda sem metas |
| 20 | Definindo metas (ou metas reabertas) |
| 30 | Metas definidas |
| 40 | Em avaliação (autoavaliação e gestor) |
| 50 | Concluída (após calibração) |

## Escala de notas

| Nota | Significado |
|---|---|
| 1 | Abaixo do esperado |
| 2 | Cumpre o esperado |
| 3 | Excede o esperado |
