
 02 — Matriz IAM com Menor Privilégio

 1. Objetivo

IAM (Identity and Access Management) é responsável por controlar quem pode acessar cada recurso e quais ações pode executar.

O princípio do menor privilégio determina que cada identidade receba somente as permissões necessárias para realizar suas atividades.

 2. Matriz de acesso

| Identidade | Recurso | Ação permitida | Condição |
|---|---|---|---|
| Leitor | Aplicação | Consultar catálogo e seus empréstimos | Conta autenticada; acesso limitado aos próprios dados |
| Bibliotecário | Aplicação | Cadastrar e alterar livros, registrar empréstimos e devoluções | Perfil de bibliotecário |
| Administrador | Gestão de usuários | Criar, bloquear e atribuir perfis | MFA e acesso privilegiado aprovado e registrado |
| Desenvolvedor | Repositório de código | Ler, criar branch e abrir pull request | Conta individual e MFA |
| Pipeline CI | Registro de imagens | Publicar imagem aprovada | Identidade de serviço e permissão limitada |
| Aplicação | Banco de dados | Ler e gravar somente tabelas necessárias | Credencial própria e conexão privada |
| Observabilidade | Logs e métricas | Consultar e gerar alertas | Papel de leitura |
| Auditor | Trilhas de auditoria | Consultar e exportar evidências | MFA e acesso somente leitura |
| Operador | Kubernetes de produção | Consultar estado e executar ações autorizadas | Acesso temporário, aprovado e registrado |

 3. Regras de menor privilégio

- Cada pessoa utiliza sua própria conta. É proibido compartilhar credenciais administrativas.
- A conta de desenvolvimento não recebe permissão de administração em produção.
- O pipeline não recebe acesso total à conta ou ao cluster.
- A aplicação utiliza identidade própria, diferente da identidade do pipeline.
- O auditor possui acesso de leitura e não pode modificar ou apagar evidências.
- Acesso administrativo exige MFA, justificativa, prazo definido e registro.
- As permissões devem ser revisadas periodicamente e removidas quando deixarem de ser necessárias.

 4. Autenticação e autorização

**Autenticação** confirma a identidade de uma pessoa ou serviço, por exemplo, utilizando senha e autenticação multifator (MFA).

**Autorização** define quais recursos e operações essa identidade pode acessar depois de autenticada.

Estar autenticado não significa ter acesso irrestrito ao sistema.

 5. Permissão mais crítica

A permissão mais crítica é a administração do ambiente de produção e do banco de dados.

Se uma conta com esse nível de acesso for comprometida, um invasor poderá alterar ou excluir dados, criar acessos e interromper o sistema.

**Controle proposto:** conta individual, MFA obrigatório, elevação temporária de privilégio, aprovação, registro de sessão e revisão das ações realizadas.

 6. Revisão de acessos

A cada mês, o responsável técnico deve conferir usuários ativos, papéis, contas de serviço e permissões não utilizadas.

Em desligamentos ou mudanças de função, o acesso deve ser revogado ou ajustado imediatamente.

 7. Conclusão

A utilização de IAM com o princípio do menor privilégio reduz os riscos de acessos indevidos e limita os danos que podem ocorrer caso uma conta seja comprometida.
