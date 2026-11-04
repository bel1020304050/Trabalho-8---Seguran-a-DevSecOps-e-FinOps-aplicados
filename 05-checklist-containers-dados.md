
 05 — Checklist de Segurança de Containers e Dados

 1. Segurança de Containers

| Verificação | Aplicação proposta | Status |
|---|---|---|
| Imagem-base confiável e mínima | Utilizar imagem oficial e mantida | A implementar/verificar |
| Atualização de dependências | Atualizar e testar periodicamente | A implementar/verificar |
| Scan de vulnerabilidades | Executar no pipeline antes da publicação | A implementar/verificar |
| Usuário não privilegiado | Executar processo sem root | A implementar/verificar |
| Sistema de arquivos | Preferir somente leitura quando possível | A implementar/verificar |
| Capabilities | Remover permissões desnecessárias | A implementar/verificar |
| Segredos | Injetar em tempo de execução por cofre | A implementar/verificar |
| Imagem rastreável | Registrar versão, origem e assinatura | A implementar/verificar |
| Rede | Restringir comunicação entre serviços | A implementar/verificar |
| Runtime | Monitorar comportamento e eventos suspeitos | A implementar/verificar |

 2. Proteção de Dados

| Verificação | Aplicação proposta | Status |
|---|---|---|
| Classificação | Identificar dados pessoais e operacionais | A implementar/verificar |
| Minimização | Coletar apenas dados necessários | A implementar/verificar |
| Criptografia em trânsito | HTTPS/TLS entre cliente e aplicação e conexões protegidas | A implementar/verificar |
| Criptografia em repouso | Proteger banco, discos e backups | A implementar/verificar |
| Controle de acesso | Restringir dados por perfil e propriedade | A implementar/verificar |
| Backup | Definir frequência e retenção | A implementar/verificar |
| Restauração | Testar recuperação periodicamente | A implementar/verificar |
| Logs | Não registrar senhas, tokens ou dados desnecessários | A implementar/verificar |
| Retenção | Definir prazo para logs e dados | A implementar/verificar |
| Descarte | Excluir dados conforme política aplicável | A implementar/verificar |

 3. Cuidados Específicos da Biblioteca

- Um leitor deve visualizar somente seus próprios dados e empréstimos.
- Bibliotecários podem realizar operações necessárias ao atendimento, sem administrar infraestrutura.
- O banco de dados não deve ficar exposto diretamente à internet.
- Backups devem ser protegidos e testados. Backup sem teste de restauração não comprova capacidade de recuperação.
- Logs de auditoria devem ser preservados contra alteração por usuários comuns.
- Dados pessoais devem ser tratados conforme a legislação aplicável, incluindo a LGPD.

 4. Critérios de Aprovação

A imagem só deve ser publicada quando passar pelas verificações obrigatórias do pipeline.

O ambiente de produção deve ser liberado somente após confirmação dos controles de acesso, proteção dos dados, backup e monitoramento.

 5. Observação

O status "A implementar/verificar" indica controles propostos neste projeto acadêmico. Não significa que o sistema já possui essas configurações implementadas.

 6. Conclusão

A segurança dos containers e dos dados é fundamental para proteger as informações da Biblioteca, evitar vulnerabilidades e garantir a continuidade do serviço.
