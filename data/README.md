# Catálogo de dados

Os arquivos originais ficam em `data/raw/` e devem ser tratados como somente
leitura. Dados derivados, caso sejam necessários, devem ser reproduzíveis a
partir do código do projeto.

## `raw/college.csv`

Base com 777 instituições de ensino superior dos Estados Unidos e 18
variáveis.

### Variável resposta

`Apps` — número de candidaturas (inscrições) recebidas pela universidade.

| Variável | Descrição |
|---|---|
| `Private` | Instituição privada (`Yes`) ou pública (`No`) |
| **`Apps`** | **Número de candidaturas recebidas (variável resposta)** |
| `Accept` | Número de candidaturas aceitas |
| `Enroll` | Número de novos alunos matriculados |
| `Top10perc` | Percentual de novos alunos no top 10% da turma do ensino médio |
| `Top25perc` | Percentual de novos alunos no top 25% da turma do ensino médio |
| `F.Undergrad` | Número de alunos de graduação em tempo integral |
| `P.Undergrad` | Número de alunos de graduação em tempo parcial |
| `Outstate` | Mensalidade para alunos de fora do estado |
| `Room.Board` | Custo de moradia e alimentação |
| `Books` | Custo estimado com livros |
| `Personal` | Gasto pessoal estimado |
| `PhD` | Percentual do corpo docente com doutorado |
| `Terminal` | Percentual do corpo docente com o grau terminal da área |
| `S.F.Ratio` | Razão aluno/professor |
| `perc.alumni` | Percentual de ex-alunos que fazem doações |
| `Expend` | Gasto institucional por aluno |
| `Grad.Rate` | Taxa de graduação |