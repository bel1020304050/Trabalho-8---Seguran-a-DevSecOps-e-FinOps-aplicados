
 03 — Política de Gerenciamento de Segredos

 1. Objetivo

Definir como senhas, tokens, chaves de API, certificados e credenciais do banco de dados serão criados, armazenados, utilizados, renovados e revogados.

 2. Regras obrigatórias

1. Segredos devem ficar em um cofre de segredos apropriado, nunca diretamente no código-fonte.
2. É proibido publicar senhas, tokens ou chaves em repositórios Git, arquivos de configuração versionados, imagens de containers, mensagens ou logs.
3. A aplicação deve obter o segredo em tempo de execução, usando identidade de serviço com permissão limitada.
4. Cada ambiente deve possuir segredos próprios. Desenvolvimento, teste e produção não devem compartilhar credenciais.
5. O acesso ao cofre deve ser concedido somente às identidades que realmente precisam do segredo.
6. Segredos devem ser transmitidos por canal criptografado e armazenados com proteção em repouso.
7. O uso e a alteração de segredos devem gerar registros de auditoria.
8. Segredos devem ser rotacionados periodicamente conforme o risco e imediatamente em caso de suspeita de exposição.
9. Segredos antigos devem ser revogados após a substituição.
10. Senhas e tokens nunca devem aparecer em logs ou mensagens de erro.

 3. Procedimento para a senha do banco de dados

- Criar uma credencial exclusiva para a aplicação.
- Conceder somente as permissões necessárias ao banco de dados da Biblioteca.
- Armazenar a credencial no cofre de segredos.
- Permitir que a identidade da aplicação consulte apenas esse segredo.
- Carregar a credencial durante a execução, sem gravá-la na imagem do container.
- Registrar o acesso ao segredo sem registrar seu valor.
- Rotacionar a credencial e validar a conexão após a troca.

 4. Resposta a vazamento

Se uma chave ou senha for exposta:

1. Revogar ou desativar imediatamente a credencial comprometida.
2. Gerar um novo segredo e atualizar o cofre.
3. Atualizar os serviços que dependem dele.
4. Investigar os registros para identificar acessos indevidos.
5. Remover o segredo do repositório e do histórico quando aplicável. A remoção do arquivo, sozinha, não torna a credencial segura.
6. Registrar o incidente, seu impacto e as ações corretivas.
7. Revisar o processo que permitiu a exposição.

 5. Responsáveis

| Responsável | Atividade |
|---|---|
| Administrador/Operação | Gerenciar cofre, acessos e rotação |
| Desenvolvedor | Não inserir segredos no código ou logs |
| Pipeline | Usar identidade de serviço e segredo somente quando necessário |
| Segurança | Revisar alertas, acessos e incidentes |

 6. Evidências

As evidências esperadas são:

- Política documentada.
- Lista de identidades autorizadas.
- Registros de acesso ao cofre.
- Comprovantes de rotação e revogação.

Os valores dos segredos nunca devem ser expostos nas evidências.

 7. Conclusão

O gerenciamento adequado de segredos protege as credenciais utilizadas pelo Sistema de Biblioteca, reduzindo o risco de vazamentos e acessos não autorizados.
