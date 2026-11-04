# 09 — Cinco Ações de Otimização de Custos

## 1. Objetivo

Propor cinco ações para reduzir os custos do Sistema de Biblioteca, com base na estimativa do arquivo [07 — Estimativa de Custos](07-estimativa-de-custos.md).

A regra principal é otimizar **sem prejudicar a segurança, a disponibilidade (SLO) e a capacidade de recuperação** do sistema. FinOps não significa só cortar gastos, mas gastar melhor.

## 2. Resumo das ações

| Nº | Ação | Serviço afetado | Antes | Depois | Economia |
|---|---|---|---:|---:|---:|
| 1 | Desligar o ambiente de teste fora do horário | Computação (teste) | R$ 150,00 | R$ 55,00 | R$ 95,00 |
| 2 | Reduzir a retenção de logs de depuração | Logs e observabilidade | R$ 180,00 | R$ 110,00 | R$ 70,00 |
| 3 | Rightsizing e autoscaling da produção | Computação (produção) | R$ 300,00 | R$ 250,00 | R$ 50,00 |
| 4 | Mover backups antigos para armazenamento mais barato | Backup | R$ 50,00 | R$ 35,00 | R$ 15,00 |
| 5 | Remover recursos órfãos | Armazenamento | R$ 60,00 | R$ 45,00 | R$ 15,00 |
| | **Total** | | | | **R$ 245,00** |

Os valores são hipóteses acadêmicas, calculados a partir da estimativa mensal de R$ 1.150,00.

## 3. Detalhamento das ações

### Ação 1 — Desligamento programado do ambiente de teste

**Problema:** o ambiente de teste fica ligado 24 horas por dia, mas a equipe só usa em horário de trabalho.

**Ação:** ligar o ambiente automaticamente às 8h e desligar às 20h, de segunda a sexta-feira.

**Cálculo:** 12 horas × 22 dias = 264 horas por mês, contra 730 horas ligado direto. Isso é cerca de 36% do tempo, o que reduz o custo de R$ 150,00 para aproximadamente R$ 55,00.

**Cuidado:** a regra vale **somente para o ambiente de teste**. A produção nunca é desligada automaticamente. Se a equipe precisar trabalhar fora do horário, o ambiente pode ser ligado manualmente.

### Ação 2 — Retenção consciente de logs

**Problema:** os logs crescem rapidamente e ficam guardados sem prazo, o que torna a observabilidade o terceiro maior custo.

**Ação:**

- Logs de depuração: manter por 7 dias.
- Logs da aplicação: manter por 30 dias.
- Logs de auditoria: **manter por 1 ano**, em armazenamento mais barato e imutável.
- Reduzir o nível de log em produção, de `DEBUG` para `INFO`.

**Cuidado:** os logs de auditoria não são reduzidos, pois são evidências exigidas pelo [plano de auditoria](08-plano-de-auditoria.md) e pela LGPD.

### Ação 3 — Rightsizing e autoscaling da produção

**Problema:** as instâncias de produção foram dimensionadas para o pico de uso e ficam com a CPU média baixa no resto do tempo.

**Ação:**

- Analisar CPU e memória durante pelo menos 30 dias antes de reduzir.
- Diminuir o tamanho das máquinas mantendo uma margem de segurança para os picos.
- Usar autoscaling no Kubernetes para aumentar as réplicas só quando a demanda subir.

**Cuidado:** manter **no mínimo 2 réplicas** sempre ativas, para não perder a alta disponibilidade. Se o tempo de resposta piorar, a mudança é revertida.

### Ação 4 — Classe de armazenamento adequada para backups

**Problema:** todos os backups ficam na mesma classe de armazenamento, inclusive os mais antigos, que quase nunca são acessados.

**Ação:** manter os backups dos últimos 7 dias em armazenamento padrão e mover os mais antigos para uma classe de armazenamento frio, que é mais barata.

**Cuidado:** a restauração continua sendo testada periodicamente, conforme o [checklist de dados](05-checklist-containers-dados.md). Backup barato que não restaura não serve.

### Ação 5 — Remoção de recursos órfãos

**Problema:** com o tempo, ficam esquecidos recursos que ninguém usa, como imagens antigas no registro de containers, discos de teste desconectados e snapshots antigos.

**Ação:**

- Exigir as tags `produto`, `ambiente`, `equipe` e `centro-custo` em todos os recursos.
- Revisar mensalmente os recursos sem tag ou sem responsável.
- Manter no registro somente as últimas 10 versões de imagem, além das versões em uso.

**Cuidado:** antes de apagar, confirmar com o responsável que o recurso não é usado. A imagem da versão anterior deve ser mantida para permitir rollback.

## 4. O que não foi reduzido

| Serviço | Motivo |
|---|---|
| Banco de dados | Guarda os dados principais da Biblioteca. Reduzir pode afetar desempenho e backup. |
| Segurança (cofre de segredos) | Custo baixo e protege as credenciais. Cortar aumentaria muito o risco. |
| Tráfego de dados | Depende do uso dos leitores e não tem desperdício claro. |

Essa decisão mostra o equilíbrio entre **custo, risco e confiabilidade**: economizar no lugar errado pode gerar um prejuízo muito maior do que o valor economizado.

## 5. Resultado esperado

| Indicador | Antes | Depois |
|---|---:|---:|
| Custo mensal total | R$ 1.150,00 | R$ 905,00 |
| Redução | — | cerca de 21% |
| Custo por empréstimo (2.000/mês) | R$ 0,58 | R$ 0,45 |

Os alertas de orçamento devem ser recalculados com base no novo valor depois que as ações forem aplicadas e o custo real for confirmado.

## 6. Prioridade

A ação mais importante é a **Ação 1 (desligar o ambiente de teste)**, porque gera a maior economia, é simples de aplicar e não afeta os usuários da Biblioteca.

## 7. Conclusão

As cinco ações reduzem o custo estimado em cerca de 21%, sem diminuir a segurança, a disponibilidade da produção ou a capacidade de recuperação. Os ganhos devem ser acompanhados mês a mês, comparando o custo estimado com o custo real.
