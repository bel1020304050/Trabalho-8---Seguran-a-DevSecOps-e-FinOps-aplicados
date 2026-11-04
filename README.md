 Trabalho 8 — Segurança, DevSecOps, Zero Trust e FinOps

Disciplina: Cloud Computing e DevOps Avançado  
Curso: CST em Sistemas para Internet — 6º Período  
Estudo de caso: Sistema Web de Biblioteca  
Aluno(a): Isabely Novais Dalava  
Professor: Diogo Ranghetti 
Data: 04/11/2026

 1. Introdução

Este trabalho apresenta uma proposta de segurança e otimização financeira para um Sistema Web de Biblioteca executado em ambiente de nuvem.

O sistema permite que usuários consultem o catálogo, realizem empréstimos e acompanhem suas informações, enquanto funcionários administram livros, usuários e operações de empréstimo.

O cenário considera uma aplicação executada em containers no Kubernetes, com banco de dados, armazenamento de arquivos, pipeline de integração e entrega contínuas e serviços de monitoramento.

Como existem dados pessoais e registros de operações, é necessário controlar os acessos, proteger as informações, registrar atividades e prevenir vulnerabilidades durante o desenvolvimento e a publicação.

Além da segurança, o estudo considera os custos de computação, banco de dados, armazenamento, tráfego e observabilidade. O objetivo é reduzir desperdícios sem comprometer a disponibilidade, a proteção dos dados e a recuperação do sistema.

 2. Objetivo

Definir controles práticos de IAM, gerenciamento de segredos, proteção de containers e dados, segurança no pipeline, auditoria e Zero Trust.

Também apresentar uma estimativa acadêmica dos custos mensais e propor ações de otimização justificadas.

 3. Descrição do sistema e premissas

- Usuários finais: consultam o catálogo, acompanham empréstimos e atualizam dados permitidos.
- Bibliotecários: cadastram livros, realizam empréstimos e devoluções.
- Administradores: gerenciam usuários, perfis e configurações autorizadas.
- Aplicação: serviço web executado em containers no Kubernetes.
- Banco de dados: armazena cadastro, catálogo e movimentações.
- Pipeline CI/CD: testa, verifica e publica imagens da aplicação.
- Observabilidade: centraliza logs, métricas e alertas.
- Ambientes: desenvolvimento/teste e produção, com permissões separadas.

As quantidades e os custos apresentados são hipóteses didáticas para dimensionar uma biblioteca de pequeno porte. Não representam medição real nem preço oficial de um provedor.

 4. Entregáveis

1. Diagrama de contexto.
2. Matriz IAM e menor privilégio.
3. Política de gerenciamento de segredos.
4. Controles de segurança do pipeline.
5. Checklist de containers e dados.
6. Plano de auditoria.
7. Aplicação de Zero Trust.
8. Estimativa de custos.
9. Cinco ações de otimização.

 5. Principais riscos identificados

O risco mais importante é o uso de uma credencial administrativa compartilhada. Essa prática dificulta identificar quem realizou uma ação e aumenta o impacto de um vazamento.

Também são relevantes a exposição de dados pessoais, vulnerabilidades em dependências e imagens de containers, permissões excessivas no pipeline e crescimento descontrolado dos logs.

 6. Conclusão

A segurança da Biblioteca depende de controles combinados: identidade individual, menor privilégio, proteção de segredos, verificações automatizadas, containers seguros, auditoria e avaliação contínua do contexto de acesso.

O modelo Zero Trust evita confiança automática, enquanto FinOps permite acompanhar os gastos e eliminar desperdícios com responsabilidade.

As otimizações propostas preservam os requisitos de segurança, disponibilidade e recuperação.

 7. Referência principal

RANGHETTI, D. Aula 13 — Segurança, DevSecOps, Zero Trust e FinOps. Material da disciplina Cloud Computing e DevOps Avançado, slides 38 a 42.

Disponível em: https://github.com/dpRanghetti/UniALFA/blob/master/Cloud%20Computing%20e%20DevOps%20Avan%C3%A7ado/aula_13_seguranca_devsecops_zero_trust_finops.md
