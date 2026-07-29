# Estatística aplicada

Aplicação de um modelo de regressão linear múltipla (MRLM) ao conjunto de
dados College, com o objetivo de investigar quais características das
universidades ajudam a explicar e prever o número de candidaturas recebidas.

O relatório foi desenvolvido em Python e Quarto, seguindo a formatação do
[ModeloUFCG](https://github.com/jerfsonbruno/ModeloUFCG).

**Relatório final:** [relatorio/relatorio.pdf](relatorio/relatorio.pdf)

## Objetivo

A variável resposta é `Apps`, definida como o número de candidaturas
(inscrições) recebidas por uma universidade. As demais variáveis descrevem
características como natureza pública ou privada, perfil dos estudantes,
tamanho da instituição, mensalidade, gastos, corpo docente e taxa de
graduação.

O estudo busca:

- descrever as características das 777 instituições da base;
- identificar associações entre `Apps` e as variáveis explicativas;
- ajustar e selecionar um modelo de regressão linear múltipla;
- avaliar multicolinearidade e os pressupostos do modelo;
- comparar o desempenho dos modelos por validação cruzada K-Fold;
- produzir previsões e intervalos com interpretação prática.

O dicionário completo está disponível em
[data/README.md](data/README.md).

## Metodologia

A análise contempla:

1. verificação da estrutura, tipos, valores ausentes e duplicatas;
2. análise exploratória univariada e bivariada;
3. matriz de correlação e box-plots;
4. ajuste do modelo inicial com todas as variáveis explicativas;
5. avaliação de multicolinearidade pelo fator de inflação da variância (VIF);
6. seleção de modelos por AIC, BIC, teste F e eliminação retroativa;
7. validação cruzada K-Fold com RMSE, MAE e R²;
8. diagnóstico por resíduos, QQ Plot, alavancagem e distância de Cook;
9. análise de sensibilidade para observações influentes;
10. intervalos de confiança para a resposta média e intervalos de predição.

Como `Accept` e `Enroll` representam etapas posteriores ao recebimento das
candidaturas, sua utilização é discutida separadamente. O modelo completo é
comparado com um modelo explicativo sem essas duas variáveis.

## Orientações do trabalho

Esta seção resume como cada etapa solicitada nas orientações foi contemplada
no relatório. Todas as atividades foram adaptadas ao conjunto de dados
College, usando `Apps` como variável resposta.

| Item | Seção do relatório |
|---|---|
| 1. Problema, características dos dados e objetivo da análise | Introdução |
| 2. Descrição da base: número de observações, variáveis, significados e unidades | Descrição da base de dados |
| 3. Análise exploratória: dados ausentes, valores atípicos e características gerais | Análise exploratória |
| 4. Análises uni e bivariadas: correlação, multicolinearidade e box-plot | Análise exploratória; Modelo inicial (VIF) |
| 5. Modelo inicial com todas as variáveis explicativas | Modelo inicial: todas as variáveis explicativas |
| 6. Seleção do melhor modelo por critério estatístico | Seleção do modelo final; Validação cruzada K-Fold |
| 7. Verificação e resolução de violações dos pressupostos | Diagnóstico do modelo selecionado; QQ Plot; Impacto da remoção |
| 8a. Intervalo de confiança para o valor médio esperado da resposta, com interpretação | Previsões: intervalo de confiança |
| 8b. Previsão pontual e intervalo de predição, com interpretação | Previsões: intervalo de predição |

## Estrutura do projeto

```text
.
├── data/
│   ├── raw/
│   │   └── college.csv             # base de dados original
│   └── README.md                   # dicionário das variáveis
├── relatorio/
│   ├── _extensions/
│   │   └── modeloufcg/             # extensão Quarto do ModeloUFCG
│   ├── _quarto.yml                 # configuração do relatório
│   ├── modeloUFCG.bib              # referências bibliográficas
│   ├── orientacoes.tex             # checklist incluído no PDF
│   ├── relatorio.qmd               # texto, análises e código Python
│   └── relatorio.pdf               # relatório final
├── .editorconfig
├── .gitignore
├── PLANO_TRABALHO.md               # organização e responsabilidades
└── requirements.txt                # dependências Python
```

O diretório `relatorio/` é um projeto Quarto autocontido. A fonte, a
bibliografia, as orientações e a extensão devem permanecer juntas para
preservar os caminhos relativos usados pelo template.

## Reprodução da análise

### Pré-requisitos

- Python 3;
- Quarto 1.3 ou mais recente;
- distribuição LaTeX com XeLaTeX.

Caso o LaTeX ainda não esteja instalado:

```bash
quarto install tinytex
```

A extensão `modeloufcg` já está incluída no repositório.

### Windows

Execute na raiz do projeto:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
quarto render relatorio/relatorio.qmd
```

### Linux ou macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
quarto render relatorio/relatorio.qmd
```

O documento gerado será salvo em `relatorio/relatorio.pdf`.
