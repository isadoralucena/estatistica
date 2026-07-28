# Estatística aplicada com Python e Quarto

Relatório reprodutível de regressão linear múltipla desenvolvido em Python.
O texto, as análises, as tabelas e os gráficos são executados pelo Quarto e
publicados em PDF com o formato do
[ModeloUFCG](https://github.com/jerfsonbruno/ModeloUFCG).

O exemplo atual analisa a base `iris` disponibilizada pelo scikit-learn. A
base `college.csv` está preservada em `data/raw/`, mas ainda não é utilizada
pelo relatório.

Documento gerado: [relatorio/relatorio.pdf](relatorio/relatorio.pdf).

Planejamento da equipe:
[PLANO_TRABALHO.md](PLANO_TRABALHO.md).

## Estrutura do projeto

```text
.
├── data/
│   ├── raw/
│   │   └── college.csv             # dado original, somente leitura
│   └── README.md                   # catálogo e dicionário dos dados
├── relatorio/
│   ├── _extensions/
│   │   └── modeloufcg/             # extensão Quarto do ModeloUFCG
│   ├── _quarto.yml                 # configuração do relatório
│   ├── modeloUFCG.bib              # referências bibliográficas
│   ├── orientacoes.tex             # checklist anexado ao relatório
│   ├── relatorio.qmd               # texto e código Python
│   └── relatorio.pdf               # documento final
├── .editorconfig                   # padrões básicos de edição
├── .gitignore                      # arquivos locais e gerados
└── requirements.txt                # dependências Python
```

O diretório `relatorio/` é um projeto Quarto autocontido. Seus arquivos devem
permanecer juntos porque o template usa caminhos relativos entre a fonte, a
extensão, a bibliografia e os recursos visuais.

Os diretórios `.venv/`, `.quarto/` e `*_files/` são locais e podem ser
recriados a qualquer momento. O PDF final, por outro lado, fica em
`relatorio/relatorio.pdf` e pode ser versionado com o trabalho.

## Pré-requisitos

- Python 3;
- Quarto 1.3 ou mais recente;
- uma distribuição LaTeX com XeLaTeX.

Se o LaTeX ainda não estiver instalado:

```bash
quarto install tinytex
```

A extensão `modeloufcg` já está incluída no repositório. Não é necessário
executar `quarto add`.

## Configuração do ambiente

Execute os comandos na raiz do projeto.

### Windows (PowerShell)

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### Linux ou macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Confirme a instalação:

```bash
python --version
python -m jupyter --version
quarto --version
```

## Renderização

Com o ambiente virtual ativado, gere o relatório completo:

```bash
quarto render relatorio/relatorio.qmd
```

O arquivo final será criado em `relatorio/relatorio.pdf`.

Para visualizar as alterações durante a edição:

```bash
quarto preview relatorio/relatorio.qmd
```

## Fluxo de trabalho

1. Edite os metadados e o conteúdo de `relatorio/relatorio.qmd`.
2. Mantenha dados originais em `data/raw/` sem alterações manuais.
3. Registre novas fontes em `relatorio/modeloUFCG.bib` e cite-as no relatório.
4. Atualize `relatorio/orientacoes.tex` apenas quando o checklist mudar.
5. Renderize novamente e revise `relatorio/relatorio.pdf` antes da entrega.

Consulte [data/README.md](data/README.md) para o catálogo e o dicionário das
bases disponíveis.
