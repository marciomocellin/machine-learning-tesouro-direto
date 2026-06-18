# Copilot Instructions

## Contexto do projeto

Este repositório contém o trabalho final da disciplina Machine Learning & Analytics. O objetivo é desenvolver um MVP individual em um notebook público no Google Colab, com foco em demonstrar um fluxo completo, coerente e reproduzível de um projeto de Machine Learning.

O tema do MVP é previsão de séries temporais usando a base de dados de taxas dos títulos ofertados pelo Tesouro Direto.

## Objetivo principal

- Desenvolver uma solução tecnicamente justificada, bem documentada e executável do início ao fim sem intervenção manual.
- Priorizar clareza, reprodutibilidade e coerência metodológica em vez de buscar necessariamente o melhor desempenho possível.
- Produzir um notebook que funcione como relatório técnico, combinando código, explicações, gráficos e resultados.

## Dados

- Usar o dataset público do Tesouro Direto: https://www.tesourotransparente.gov.br/ckan/dataset/df56aa42-484a-4a59-8184-7676580c81e3/resource/796d2059-14e9-44e3-80c9-2d9e30b405c1/download/precotaxatesourodireto.csv
- Consultar os metadados quando necessário: https://www.tesourotransparente.gov.br/ckan/dataset/df56aa42-484a-4a59-8184-7676580c81e3/resource/1a8eb2e3-4902-4a38-a1eb-6410f23d90de/download/taxa.pdf
- Carregar os dados diretamente no notebook por URL pública ou biblioteca de acesso público.
- Não exigir upload manual, login, token, chave de API ou configuração local para execução.

## Regras para o notebook

- Deve ser escrito em pt-BR.
- Manter o notebook executável do início ao fim no Colab.
- Explicar no início qual é o problema, qual é o objetivo do modelo, qual variável será prevista e por que o problema pode ser tratado como Machine Learning.
- Tratar explicitamente o problema como previsão de séries temporais.
- Respeitar a ordem temporal na divisão dos dados.
- Evitar vazamento de dados em qualquer etapa que dependa do conjunto de treino.
- Justificar todas as escolhas relevantes: limpeza, transformação, engenharia de atributos, divisão, modelo e métricas.
- Incluir uma análise exploratória suficiente para entender o dataset antes da modelagem.
- Incluir pelo menos um baseline simples e pelo menos duas abordagens candidatas adicionais, ou duas variações justificadas de uma mesma família de modelos.
- Comparar os modelos com métricas apropriadas para séries temporais e discutir limitações e trade-offs.

## Estrutura esperada do conteúdo

1. Apresentação do problema e definição da tarefa.
2. Apresentação dos dados e descrição das variáveis.
3. Análise exploratória inicial.
4. Preparação dos dados.
5. Divisão temporal entre treino, validação e teste, quando aplicável.
6. Modelagem e treinamento.
7. Avaliação dos resultados.
8. Discussão crítica da solução, limitações e possíveis melhorias.

## Boas práticas técnicas

- Preferir código simples, legível e modular.
- Usar nomes descritivos para variáveis e funções.
- Evitar blocos longos sem comentários explicativos quando a lógica não for óbvia.
- Criar pipelines reproduzíveis sempre que fizer sentido.
- Ajustar transformações apenas com os dados de treino quando aplicável.
- Manter as visualizações objetivas e interpretáveis.
- Usar bibliotecas amplamente conhecidas e adequadas ao problema.

## Orientações de escrita

- Escrever em português claro e técnico.
- Explicar decisões como se o notebook fosse avaliado por um professor que precisa reproduzir e entender a solução.
- Destacar hipóteses, limitações e premissas do modelo.
- Não superestimar os resultados; discutir também fragilidades da abordagem.

## Critérios de qualidade

- O notebook deve ser reprodutível.
- A metodologia deve ser compatível com previsão de séries temporais.
- A apresentação deve ser coerente, organizada e tecnicamente defensável.
- O resultado final deve mostrar domínio do fluxo essencial de um projeto de Machine Learning.