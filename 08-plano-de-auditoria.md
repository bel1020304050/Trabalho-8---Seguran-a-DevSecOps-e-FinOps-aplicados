# 08 — Plano de Auditoria e Compliance

## 1. Objetivo

Definir quais ações do Sistema de Biblioteca devem ser registradas, como esses registros serão protegidos e quem será responsável por analisá-los.

A auditoria permite descobrir quem fez cada ação, investigar incidentes e comprovar que os controles de segurança estão funcionando.

## 2. Informações registradas em cada evento

Todo registro de auditoria deve responder às seguintes perguntas:

| Pergunta | Informação registrada | Exemplo |
|---|---|---|
| Quem? | Identidade individual do usuário ou serviço | `maria.bibliotecaria` ou `pipeline-ci` |
| O quê? | Ação realizada | Alteração de perfil de usuário |
| Quando? | Data e hora com fuso horário | 04/11/2026 14:32:10 (UTC-3) |
| Onde? | Recurso afetado e endereço de origem | Tabela de usuários, IP 10.0.2.15 |
| Resultado? | Sucesso ou falha | Negado por falta de permissão |

Os registros não devem conter senhas, tokens ou dados pessoais desnecessários.

## 3. Eventos auditados

| Evento | Origem | Prioridade | Gera alerta? |
|---|---|---|---|
| Login com falha repetida | Aplicação | Alta | Sim, após 5 tentativas |
| Login de administrador | Aplicação / provedor de nuvem | Alta | Sim |
| Criação de conta administrativa | IAM | Crítica | Sim, imediato |
| Alteração de perfis e permissões | IAM / aplicação | Crítica | Sim, imediato |
| Elevação temporária de privilégio | IAM | Alta | Sim |
| Acesso ou alteração de segredo no cofre | Cofre de segredos | Crítica | Sim |
| Exclusão de livros, usuários ou empréstimos | Aplicação | Alta | Sim, quando em grande quantidade |
| Exportação de dados pessoais | Aplicação | Alta | Sim |
| Publicação de imagem e deploy | Pipeline CI/CD | Média | Não, apenas registro |
| Exceção aprovada no gate de segurança | Pipeline CI/CD | Alta | Sim |
| Exclusão de recurso de nuvem (banco, bucket, cluster) | Provedor de nuvem | Crítica | Sim, imediato |
| Tentativa de acesso de um leitor a dados de outro leitor | Aplicação | Alta | Sim |
| Alteração ou exclusão de logs de auditoria | Observabilidade | Crítica | Sim, imediato |

## 4. Proteção dos registros

- **Integridade:** os logs de auditoria ficam em um armazenamento separado e imutável. Nenhum usuário comum consegue alterar ou apagar registros.
- **Acesso controlado:** somente o auditor e a equipe de segurança podem consultar, com MFA e permissão de leitura.
- **Retenção:** logs de auditoria são guardados por 1 ano. Logs técnicos de depuração ficam apenas 7 dias.
- **Sincronização de horário:** todos os serviços usam a mesma fonte de horário, para que os eventos possam ser comparados.
- **Separação:** quem administra o sistema não é quem audita as ações administrativas.

Os prazos de retenção são hipóteses acadêmicas e devem ser ajustados conforme as exigências legais e contratuais.

## 5. Rotina de revisão

| Frequência | Atividade | Responsável |
|---|---|---|
| Diária | Analisar alertas críticos | Operação / Segurança |
| Semanal | Verificar tentativas de acesso negadas | Segurança |
| Mensal | Revisar usuários, papéis e contas de serviço | Responsável técnico |
| Mensal | Conferir exceções aprovadas no pipeline e seus prazos | Responsável técnico |
| Semestral | Testar se os logs estão completos e íntegros | Auditor |

## 6. Compliance

O sistema armazena dados pessoais dos leitores, como nome, e-mail e histórico de empréstimos. Por isso, deve seguir a LGPD (Lei Geral de Proteção de Dados).

Estar em conformidade não significa que o sistema está totalmente seguro. Significa que existem controles, responsáveis e evidências de que as regras estão sendo cumpridas.

| Requisito | Controle aplicado | Evidência |
|---|---|---|
| Acesso apenas por pessoas autorizadas | Matriz IAM e menor privilégio | Lista de permissões revisada |
| Rastreabilidade das ações | Logs de auditoria | Registros com quem, o quê e quando |
| Proteção de dados pessoais | Criptografia e controle de acesso | Configuração do banco e checklist de dados |
| Proteção de credenciais | Cofre de segredos | Registros de acesso e rotação |
| Publicação segura | Gates no pipeline | Histórico de execução do pipeline |
| Tratamento de desvios | Exceções com responsável e prazo | Registro das exceções aprovadas |

Sempre que possível, as evidências devem ser geradas automaticamente pelo pipeline e pelos serviços de nuvem, evitando depender de prints ou controles manuais.

## 7. Uso da auditoria em incidentes

Quando ocorrer um incidente, os logs de auditoria são usados para:

1. Detectar a ação suspeita por meio dos alertas.
2. Identificar a conta envolvida e conter o acesso.
3. Preservar os registros como evidência antes de qualquer correção.
4. Descobrir o que foi alterado e desde quando.
5. Apoiar a recuperação e a comunicação do incidente.
6. Registrar as lições aprendidas.

## 8. Evidência principal

A evidência de auditoria mais importante é o registro de **alteração de permissões e criação de contas administrativas**.

Esse registro resolve diretamente o maior risco identificado no trabalho: o uso de credencial administrativa compartilhada. Com contas individuais e auditoria, é possível saber exatamente quem realizou cada ação.

## 9. Conclusão

O plano de auditoria garante que as ações importantes da Biblioteca fiquem registradas de forma segura. Isso permite investigar incidentes, comprovar o cumprimento da LGPD e manter o controle sobre quem acessa e altera o sistema.
