# 07 — Estimativa de Custos (FinOps)

## 1. Objetivo

Estimar os custos mensais de infraestrutura do Sistema de Biblioteca em nuvem, considerando os serviços necessários para manter a aplicação disponível, segura e monitorada.

Os valores apresentados são hipotéticos e utilizados apenas para fins acadêmicos. Eles não representam uma cotação oficial de provedores de nuvem.

## 2. Estimativa mensal

| Serviço | Descrição | Custo mensal estimado |
|---|---|---:|
| Computação | Servidores para executar a aplicação | R$ 450,00 |
| Banco de dados | Hospedagem do banco de dados | R$ 300,00 |
| Armazenamento | Arquivos e documentos do sistema | R$ 60,00 |
| Backup | Cópias de segurança | R$ 50,00 |
| Tráfego de dados | Transferência de dados para fora da nuvem | R$ 70,00 |
| Logs e observabilidade | Monitoramento e armazenamento de registros | R$ 180,00 |
| Segurança | Gerenciamento de segredos e recursos de proteção | R$ 40,00 |
| **Total** | | **R$ 1.150,00** |

## 3. Análise dos custos

Os maiores custos estimados estão relacionados à computação e ao banco de dados, pois são essenciais para o funcionamento da aplicação.

Os serviços de monitoramento e segurança também são importantes, pois ajudam a identificar falhas, acompanhar o desempenho e proteger as informações.

Logs e observabilidade aparecem como o terceiro maior gasto (R$ 180,00). Isso acontece porque os logs da Biblioteca crescem rapidamente e, sem uma regra de retenção, ficam armazenados por tempo indeterminado.

Para entender melhor a computação, o valor foi separado por ambiente:

| Ambiente | Uso | Custo mensal estimado |
|---|---|---:|
| Produção | Atende os usuários, ligado 24 horas | R$ 300,00 |
| Desenvolvimento/teste | Usado pela equipe, mas fica ligado o tempo todo | R$ 150,00 |
| **Total de computação** | | **R$ 450,00** |

O ambiente de teste representa um terço do custo de computação, mesmo sendo usado só em horário de trabalho. Esse é um dos principais pontos de desperdício identificados.

### Custo unitário

Considerando, como hipótese, 2.000 empréstimos processados por mês:

**R$ 1.150,00 ÷ 2.000 empréstimos = R$ 0,58 por empréstimo**

Esse indicador ajuda a verificar se o gasto cresce na mesma proporção que o uso do sistema.

## 4. Ações de controle financeiro

Para controlar os gastos, serão adotadas as seguintes medidas:

- Acompanhar mensalmente os custos de cada serviço.
- Criar alertas de orçamento.
- Identificar recursos que não estão sendo utilizados.
- Ajustar a capacidade dos servidores conforme a demanda.
- Revisar o armazenamento e a retenção dos logs.
- Comparar o custo estimado com o custo real.
- Aplicar tags obrigatórias em todos os recursos para saber de onde vem cada gasto.

Tags propostas:

| Tag | Exemplo | Para que serve |
|---|---|---|
| `produto` | `biblioteca` | Separar os custos deste sistema |
| `ambiente` | `producao` ou `teste` | Comparar o gasto de cada ambiente |
| `equipe` | `backend` | Saber quem é responsável pelo recurso |
| `centro-custo` | `si` | Atribuir a despesa ao setor correto |

Recursos sem tags ou sem responsável devem ser investigados, pois podem ser recursos esquecidos.

## 5. Alertas de orçamento

Considerando o orçamento mensal de R$ 1.150,00, serão definidos os seguintes limites:

| Limite atingido | Ação recomendada |
|---|---|
| 70% — R$ 805,00 | Verificar o consumo dos serviços. |
| 85% — R$ 977,50 | Analisar os recursos que estão aumentando os custos. |
| 100% — R$ 1.150,00 | Revisar os gastos e aprovar medidas de redução. |

## 6. Indicadores FinOps

Os principais indicadores acompanhados serão:

- Custo mensal total da infraestrutura.
- Custo por serviço utilizado.
- Variação dos gastos entre os meses.
- Consumo de armazenamento.
- Utilização de CPU e memória.
- Custo dos serviços de monitoramento.

## 7. Conclusão

A prática de FinOps permite acompanhar os gastos da infraestrutura em nuvem e tomar decisões para evitar desperdícios. Com monitoramento, planejamento e otimização dos recursos, o Sistema de Biblioteca poderá manter seus serviços com melhor controle financeiro.
