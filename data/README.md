# Catálogo de dados

Os arquivos originais ficam em `data/raw/` e devem ser tratados como somente
leitura. Dados derivados, caso sejam necessários, devem ser reproduzíveis a
partir do código do projeto.

## `raw/college.csv`

Base com 777 instituições de ensino superior dos Estados Unidos e 18
variáveis.

> A origem e a licença do arquivo ainda precisam ser registradas antes da
> publicação de resultados baseados nele.

| Variável | Descrição |
|---|---|
| `Private` | Instituição privada (`Yes`) ou pública (`No`) |
| `Apps` | Candidaturas recebidas |
| `Accept` | Candidaturas aceitas |
| `Enroll` | Novos alunos matriculados |
| `Top10perc` | Novos alunos no top 10% da turma do ensino médio |
| `Top25perc` | Novos alunos no top 25% da turma do ensino médio |
| `F.Undergrad` | Alunos de graduação em tempo integral |
| `P.Undergrad` | Alunos de graduação em tempo parcial |
| `Outstate` | Mensalidade para alunos de fora do estado |
| `Room.Board` | Custo de moradia e alimentação |
| `Books` | Custo estimado com livros |
| `Personal` | Gasto pessoal estimado |
| `PhD` | Corpo docente com doutorado |
| `Terminal` | Corpo docente com o grau terminal da área |
| `S.F.Ratio` | Razão aluno/professor |
| `perc.alumni` | Ex-alunos que fazem doações |
| `Expend` | Gasto institucional por aluno |
| `Grad.Rate` | Taxa de graduação |

## Dados usados no relatório

O arquivo `relatorio/relatorio.qmd` usa a base `iris`, carregada diretamente
pelo scikit-learn. Ela contém 150 flores, quatro medidas morfológicas e a
espécie de cada observação; portanto, não há uma cópia local dessa base.
