# Plano de trabalho — análise da base College

## Objetivo proposto

Investigar quais características institucionais ajudam a explicar e prever o
número de candidaturas recebidas pelas universidades.

- Variável resposta definida: `Apps`.
- Preditor qualitativo: `Private`.
- Preditores quantitativos: as outras 16 variáveis numéricas.
- Unidade de análise: instituição de ensino superior.

O grupo deve definir se o objetivo principal é explicativo ou preditivo.
`Accept` e `Enroll` ocorrem depois do recebimento das candidaturas e são muito
próximas de `Apps`; por isso, podem entrar no modelo inicial exigido pelo
trabalho, mas sua permanência no modelo final precisa de justificativa.

## Diagnóstico inicial da base

- 777 instituições e 18 variáveis;
- 565 instituições privadas e 212 públicas;
- nenhum valor ausente;
- nenhuma linha duplicada;
- `Apps` varia de 81 a 48.094 candidaturas;
- média de `Apps` igual a 3.001,6 e mediana igual a 1.558, indicando forte
  assimetria à direita;
- correlação elevada de `Apps` com `Accept` (0,94), `Enroll` (0,85) e
  `F.Undergrad` (0,81);
- todas as linhas respeitam `Enroll <= Accept <= Apps`;
- uma observação tem `Grad.Rate = 118`, acima do limite esperado de 100,
  embora `Grad.Rate` agora seja uma variável explicativa.

Os valores extremos de `Apps` e o valor 118 de `Grad.Rate` devem ser
documentados e analisados. Nenhum deles deve ser corrigido, limitado ou
removido sem justificativa e análise de sensibilidade.

## Divisão da equipe

### Isadora — dados, análise exploratória e modelo inicial

Responsável por estabelecer a base da análise e entregar o primeiro modelo
completo para a equipe.

1. Formular a pergunta de pesquisa e o objetivo do relatório.
2. Adaptar a introdução e a metodologia para a base College.
3. Carregar `../data/raw/college.csv` a partir de `relatorio.qmd`, sem
   modificar o arquivo original.
4. Confirmar dimensões, tipos, categorias, duplicatas e valores ausentes.
5. Validar faixas, unidades e as relações `Enroll <= Accept <= Apps`.
6. Investigar a assimetria e os valores extremos de `Apps`, além do caso
   `Grad.Rate = 118`.
7. Produzir estatísticas descritivas, histogramas e box-plots.
8. Comparar `Apps` entre instituições públicas e privadas.
9. Produzir gráficos bivariados entre `Apps` e os principais preditores.
10. Ajustar o modelo inicial com todos os preditores, incluindo a codificação
    dummy de `Private`.
11. Escrever as seções:
    - Introdução;
    - Descrição e qualidade dos dados;
    - Análise exploratória univariada e bivariada;
    - Modelo inicial.
12. Integrar as três partes aprovadas no relatório e gerar o PDF final.

Entregáveis:

- código de leitura e preparação dos dados;
- dicionário de variáveis revisado;
- tabela de estatísticas descritivas;
- histogramas, box-plots e gráficos bivariados;
- tabela do modelo inicial completo;
- base de análise validada para Jennifer e Oscar;
- `relatorio.qmd` integrado e PDF final.

### Jennifer — multicolinearidade, seleção e validação

Responsável por comparar os modelos candidatos e justificar o modelo final.

1. Calcular e interpretar a matriz de correlação.
2. Calcular o VIF e investigar a redundância entre `Accept`, `Enroll` e
   `F.Undergrad`.
3. Avaliar um modelo explicativo sem `Accept` e `Enroll`.
4. Comparar a resposta original com uma modelagem de `log(Apps)`, caso os
   resíduos confirmem a necessidade de transformação.
5. Comparar modelos com AIC, BIC, teste F e seleção retroativa, sem comparar
   AIC diretamente entre modelos com `Apps` e `log(Apps)`.
6. Aplicar validação cruzada K-Fold aos modelos candidatos:
   - usar `K = 10`;
   - embaralhar os dados com semente fixa (`random_state = 42`);
   - usar exatamente as mesmas divisões para todos os modelos;
   - calcular média e desvio-padrão de RMSE, MAE e R²;
   - avaliar as previsões na escala original de `Apps`.
7. Propor o modelo final combinando adequação estatística, parcimônia e
   desempenho na validação cruzada.
8. Interpretar os coeficientes brutos e padronizados do modelo selecionado,
   incluindo a variável dummy `Private`.
9. Escrever as seções:
   - Correlação e multicolinearidade;
   - Seleção do modelo final;
   - Validação cruzada K-Fold;
   - Interpretação dos coeficientes.

Entregáveis:

- matriz de correlação;
- tabela de VIF;
- tabela comparativa dos modelos;
- comparação entre o modelo completo e o modelo sem `Accept` e `Enroll`;
- tabela K-Fold com média e desvio-padrão de RMSE, MAE e R²;
- fórmula, justificativa e interpretação do modelo selecionado.

Qualquer transformação, seleção de variáveis ou padronização usada na
validação cruzada deve ser estimada dentro de cada fold, evitando vazamento de
informações do conjunto de validação.

### Oscar — diagnóstico, inferência e previsão

Responsável por verificar a confiabilidade do modelo e transformar seus
resultados em inferências e previsões práticas.

1. Verificar linearidade e homocedasticidade dos resíduos.
2. Construir e interpretar o QQ Plot dos resíduos estudentizados.
3. Comparar o QQ Plot com o envelope simulado, quando disponível.
4. Calcular resíduos estudentizados, alavancagem e distância de Cook.
5. Identificar observações atípicas e influentes.
6. Fazer análise de sensibilidade com e sem observações justificadamente
   problemáticas, incluindo valores extremos de `Apps` e `Grad.Rate = 118`.
7. Definir dois ou três perfis plausíveis de instituições para previsão.
8. Calcular e interpretar:
   - intervalo de confiança para o número médio de candidaturas;
   - intervalo de predição para as candidaturas de uma nova instituição.
9. Verificar se os intervalos são plausíveis e não produzem contagens
   negativas; se o modelo usar `log(Apps)`, documentar o retorno à escala
   original.
10. Redigir a conclusão ligada à pergunta de pesquisa.
11. Escrever as seções:
    - Diagnóstico do modelo;
    - QQ Plot e normalidade dos resíduos;
    - Pontos atípicos, de alavanca e influentes;
    - Previsões;
    - Conclusão.

Entregáveis:

- painel de diagnóstico dos resíduos;
- QQ Plot com linha de referência e interpretação;
- tabela de observações influentes;
- análise de sensibilidade;
- tabela de previsões e respectivos intervalos;
- conclusão ligada à pergunta de pesquisa.

## Ordem de execução

### Etapa 1 — decisões conjuntas

Responsáveis: Isadora, Jennifer e Oscar.

1. Registrar `Apps` como variável resposta.
2. Definir se o objetivo é explicativo, preditivo ou ambos.
3. Definir o papel de `Accept` e `Enroll` no modelo final.
4. Acordar as regras para dados problemáticos e valores extremos.
5. Definir nomes, unidades e arredondamentos usados nas tabelas.

### Etapa 2 — preparação e exploração

Responsável principal: Isadora.

Jennifer pode preparar as funções de VIF e K-Fold em paralelo. Oscar pode
preparar as funções de diagnóstico usando um modelo provisório.

### Etapa 3 — seleção e validação

Responsável principal: Jennifer.

O modelo final só deve ser fechado depois da revisão de Isadora sobre os dados
e de uma verificação preliminar de Oscar sobre os resíduos. A escolha deve
considerar tanto os critérios estatísticos quanto a validação cruzada K-Fold.

### Etapa 4 — diagnóstico e previsão

Responsável principal: Oscar.

Se os pressupostos falharem, Jennifer revisa a especificação do modelo e
Isadora confirma se a causa pode estar na preparação dos dados.

### Etapa 5 — integração e revisão

- Isadora: padronização do texto, metadados, tabelas e referências.
- Jennifer: auditoria das fórmulas, critérios de seleção e resultados.
- Oscar: auditoria das interpretações, diagnósticos e previsões.
- Todos: leitura do PDF final e aprovação da conclusão.

## Estratégia de trabalho em uma única branch

Toda a equipe trabalhará apenas na branch `main`. Para reduzir conflitos, cada
pessoa deve editar inicialmente somente o arquivo correspondente à sua seção:

```text
relatorio/secoes/
├── 01_dados_isadora.qmd
├── 02_modelagem_jennifer.qmd
└── 03_diagnosticos_oscar.qmd
```

Regras de colaboração:

1. Antes de começar uma tarefa, executar `git pull` na branch `main`.
2. Não editar o arquivo de seção atribuído a outra pessoa.
3. Fazer commits pequenos e identificados, por exemplo:
   - `dados: adiciona análise descritiva (Isadora)`;
   - `modelo: adiciona validação K-Fold (Jennifer)`;
   - `diagnostico: adiciona QQ Plot (Oscar)`.
4. Avisar o grupo antes de editar arquivos compartilhados, como
   `README.md`, `modeloUFCG.bib` e `orientacoes.tex`.
5. Se outra pessoa tiver enviado alterações, executar `git pull --rebase`
   antes de fazer o próximo `git push`.
6. Isadora será responsável por integrar, na ordem Isadora → Jennifer →
   Oscar, as três seções em `relatorio/relatorio.qmd`.
7. Somente Isadora deve regenerar e enviar `relatorio/relatorio.pdf`, depois
   que as alterações textuais estiverem integradas. Isso evita conflitos no
   PDF, que é um arquivo binário.
8. Jennifer e Oscar revisam o `.qmd` integrado antes da geração do PDF final.

## Critérios de conclusão

O trabalho estará pronto quando:

- todas as tabelas e figuras forem produzidas por código;
- o dado original permanecer inalterado;
- `Apps` estiver documentada como variável resposta;
- o uso ou a exclusão de `Accept` e `Enroll` estiver justificado;
- a escolha da escala de `Apps` e do modelo estiver justificada;
- multicolinearidade e pressupostos forem avaliados;
- o QQ Plot dos resíduos estiver apresentado e interpretado;
- os modelos candidatos forem comparados por validação K-Fold reproduzível;
- pontos influentes tiverem análise de sensibilidade;
- intervalos de confiança e predição tiverem interpretação prática;
- `quarto render relatorio/relatorio.qmd` executar sem erros;
- `relatorio/relatorio.pdf` estiver atualizado e revisado pelos três.
