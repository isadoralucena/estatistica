# Plano de trabalho — análise da base College

## Objetivo proposto

Investigar quais características institucionais estão associadas à taxa de
graduação das faculdades.

- Variável resposta recomendada: `Grad.Rate`.
- Preditor qualitativo: `Private`.
- Preditores quantitativos: as outras 16 variáveis numéricas.
- Unidade de análise: instituição de ensino superior.

Antes de iniciar a modelagem, o grupo deve confirmar com o professor se
`Grad.Rate` pode ser usada como resposta. Caso outra resposta seja exigida, a
divisão de responsabilidades continua válida.

## Diagnóstico inicial da base

- 777 instituições e 18 variáveis;
- 565 instituições privadas e 212 públicas;
- nenhum valor ausente;
- nenhuma linha duplicada;
- uma observação com `Grad.Rate = 118`, acima do limite esperado de 100;
- possíveis grupos de variáveis correlacionadas, como `Apps`, `Accept`,
  `Enroll` e `F.Undergrad`.

O valor 118 deve ser documentado e analisado. Ele não deve ser corrigido,
limitado ou removido sem justificativa e análise de sensibilidade.

## Divisão da equipe

### Isadora — problema, dados e análise descritiva

Responsável por estabelecer uma base confiável para as demais etapas.

1. Formular a pergunta de pesquisa e o objetivo do relatório.
2. Adaptar a introdução e a metodologia do exemplo `iris` para a base College.
3. Carregar `data/raw/college.csv` sem modificar o arquivo original.
4. Confirmar dimensões, tipos, categorias, duplicatas e valores ausentes.
5. Validar faixas e unidades das variáveis.
6. Investigar e documentar a observação com `Grad.Rate = 118`.
7. Produzir a tabela descritiva e as análises univariadas.
8. Escrever as seções:
   - Introdução;
   - Descrição da base de dados;
   - Qualidade dos dados;
   - Análise exploratória univariada.

Entregáveis:

- código único de leitura e preparação dos dados;
- dicionário de variáveis revisado;
- tabela de estatísticas descritivas;
- histogramas ou box-plots das variáveis principais;
- decisão documentada sobre como tratar o valor 118.

### Jennifer — relações entre variáveis e seleção do modelo

Responsável pela construção e comparação dos modelos candidatos.

1. Comparar `Grad.Rate` entre instituições públicas e privadas.
2. Produzir gráficos bivariados entre a resposta e os principais preditores.
3. Calcular e interpretar a matriz de correlação.
4. Ajustar o modelo inicial com todos os preditores.
5. Codificar e interpretar a variável dummy `Private`.
6. Calcular o VIF e identificar multicolinearidade.
7. Avaliar transformações para variáveis muito assimétricas, se necessário.
8. Comparar modelos com AIC, BIC, teste F e seleção retroativa.
9. Propor o modelo final, justificando cada exclusão.
10. Escrever as seções:
    - Análise bivariada;
    - Correlação e multicolinearidade;
    - Modelo inicial;
    - Seleção do modelo final.

Entregáveis:

- matriz de correlação e gráficos bivariados;
- tabela de VIF;
- tabela comparativa dos modelos;
- fórmula e justificativa do modelo selecionado.

Jennifer deve prestar atenção especial à redundância entre `Apps`, `Accept`,
`Enroll` e `F.Undergrad`, evitando selecionar variáveis apenas pelo p-valor.

### Oscar — diagnóstico, inferência e conclusão

Responsável por verificar se o modelo escolhido é confiável e interpretar seus
resultados.

1. Verificar linearidade, normalidade e homocedasticidade dos resíduos.
2. Calcular resíduos estudentizados, alavancagem e distância de Cook.
3. Identificar observações atípicas e influentes.
4. Fazer análise de sensibilidade com e sem observações justificadamente
   problemáticas, incluindo o caso `Grad.Rate = 118`.
5. Interpretar coeficientes brutos e padronizados.
6. Definir dois ou três perfis plausíveis de instituições para previsão.
7. Calcular e interpretar:
   - intervalo de confiança para a resposta média;
   - intervalo de predição para uma nova instituição.
8. Escrever as seções:
   - Diagnóstico do modelo;
   - Pontos atípicos, de alavanca e influentes;
   - Interpretação;
   - Previsões;
   - Conclusão.

Entregáveis:

- painel de diagnóstico dos resíduos;
- tabela de observações influentes;
- comparação da análise de sensibilidade;
- tabela de previsões;
- conclusão ligada à pergunta de pesquisa.

## Ordem de execução

### Etapa 1 — decisões conjuntas

Responsáveis: Isadora, Jennifer e Oscar.

1. Confirmar `Grad.Rate` como resposta.
2. Definir a pergunta de pesquisa.
3. Acordar as regras para dados problemáticos.
4. Definir nomes, unidades e arredondamentos usados nas tabelas.

### Etapa 2 — preparação e exploração

Responsável principal: Isadora.

Jennifer pode preparar os gráficos bivariados em paralelo. Oscar pode preparar
funções de diagnóstico usando um modelo provisório.

### Etapa 3 — construção e seleção

Responsável principal: Jennifer.

O modelo final só deve ser fechado depois da revisão de Isadora sobre os dados
e de uma verificação preliminar de Oscar sobre os resíduos.

### Etapa 4 — diagnóstico e previsão

Responsável principal: Oscar.

Se os pressupostos falharem, Jennifer revisa a especificação do modelo e
Isadora confirma se a causa pode estar na preparação dos dados.

### Etapa 5 — integração e revisão

- Isadora: padronização do texto, metadados, tabelas e referências.
- Jennifer: auditoria das fórmulas, critérios de seleção e resultados.
- Oscar: auditoria das interpretações, diagnósticos e previsões.
- Todos: leitura do PDF final e aprovação da conclusão.

## Estratégia para evitar conflitos

Cada pessoa deve trabalhar em uma seção própria antes da integração:

```text
relatorio/secoes/
├── 01_dados_isadora.qmd
├── 02_modelagem_jennifer.qmd
└── 03_diagnosticos_oscar.qmd
```

Na integração, o conteúdo aprovado é incluído em `relatorio/relatorio.qmd`.
Se o grupo preferir trabalhar diretamente no arquivo principal, as alterações
devem ser integradas na ordem Isadora → Jennifer → Oscar.

Sugestão de branches:

- `isadora/dados-contexto`;
- `jennifer/modelagem`;
- `oscar/diagnosticos-previsao`.

## Critérios de conclusão

O trabalho estará pronto quando:

- todas as tabelas e figuras forem produzidas por código;
- o dado original permanecer inalterado;
- a escolha da resposta e do modelo estiver justificada;
- multicolinearidade e pressupostos forem avaliados;
- pontos influentes tiverem análise de sensibilidade;
- intervalos de confiança e predição tiverem interpretação prática;
- `quarto render relatorio/relatorio.qmd` executar sem erros;
- `relatorio/relatorio.pdf` estiver atualizado e revisado pelos três.
