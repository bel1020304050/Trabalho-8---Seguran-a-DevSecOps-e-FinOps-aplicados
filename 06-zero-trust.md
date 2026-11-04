 06 — Aplicação do Modelo Zero Trust

 1. O que é Zero Trust?

Zero Trust é um modelo de segurança baseado no princípio de nunca confiar automaticamente em usuários, dispositivos ou sistemas. Todo acesso precisa ser verificado, autorizado e monitorado.

No Sistema de Biblioteca, esse modelo ajuda a proteger os dados dos leitores, os empréstimos, os cadastros e as funções administrativas.

 2. Princípios aplicados

| Princípio | Aplicação no Sistema de Biblioteca |
|---|---|
| Verificação explícita | Confirmar a identidade do usuário antes de permitir o acesso. |
| Menor privilégio | Conceder somente as permissões necessárias para cada função. |
| Assumir que pode existir uma invasão | Monitorar atividades suspeitas e preparar respostas a incidentes. |
| Avaliação contínua | Revisar acessos e permissões periodicamente. |
| Segmentação | Separar os ambientes de desenvolvimento, testes e produção. |
| Autenticação multifator | Exigir uma segunda etapa de autenticação para contas administrativas. |

 3. Exemplo de aplicação para administradores

Quando um administrador precisar acessar funções importantes do sistema, deverão ser aplicadas as seguintes medidas:

1. Utilizar uma conta individual, sem compartilhar credenciais.
2. Confirmar a identidade por autenticação multifator (MFA).
3. Verificar se o usuário possui autorização para realizar a operação.
4. Conceder permissões administrativas somente quando necessárias.
5. Registrar as ações realizadas em logs de auditoria.
6. Revogar permissões temporárias após o uso.

 4. Exemplo de aplicação para leitores

Um leitor deve consultar somente seus próprios empréstimos e informações pessoais.

Mesmo que tente alterar o identificador de um empréstimo diretamente pela URL, o sistema deverá verificar no servidor se aquele registro realmente pertence ao usuário autenticado.

Essa validação evita que um leitor acesse informações de outras pessoas.

 5. Medidas recomendadas

- Utilizar HTTPS para proteger a comunicação.
- Aplicar autenticação multifator em contas privilegiadas.
- Validar permissões no servidor, e não somente na interface.
- Monitorar tentativas de acesso não autorizado.
- Separar os ambientes de desenvolvimento e produção.
- Revisar periodicamente as permissões dos usuários.

 6. Benefícios esperados

A aplicação do Zero Trust contribui para reduzir acessos indevidos, proteger informações pessoais, limitar danos em caso de comprometimento de uma conta e melhorar o controle sobre as operações do sistema.

 7. Conclusão

O modelo Zero Trust fortalece a segurança do Sistema de Biblioteca ao exigir verificação contínua, controle de permissões e monitoramento dos acessos. Dessa forma, nenhum usuário ou dispositivo recebe confiança automática.
