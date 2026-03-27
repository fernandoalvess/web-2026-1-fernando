# Descrição do Projeto — SIFU
**Sistema Integrado Funcional e Unificado | UFERSA**

> **Processo escolhido:** Empréstimo ou Renovação de Material Informacional
> **Portfólio EP:** https://ep.ufersa.edu.br/wp-content/uploads/portfolioep/ensino/emprestimoourenovacaodematerial/index.html#normal

---

## 1. Descrição do Problema a ser Solucionado

O projeto visa modernizar e otimizar o processo de **Empréstimo ou Renovação de Material Informacional** no âmbito da UFERSA. O novo módulo dentro do SIFU automatizará o controle de circulação do acervo, permitindo renovações online simplificadas e agilizando o check-out presencial com **validação automática de pendências do usuário**, substituindo verificações manuais por integrações de sistema.

---

## 2. Perfis de Usuário

| Perfil | Descrição |
|---|---|
| **Discente / Docente / Técnico-Administrativo** | Usuários finais que acessam o portal para consultar o acervo, realizar renovações e gerenciar seus empréstimos. |
| **Servidor do SISBI (Biblioteca)** | Possui privilégios de administrador para registrar saídas de materiais, inserir tombos, desmagnetizar itens e conferir status de usuários no balcão. |

---

## 3. Informações a serem Armazenadas

- **Dados do Usuário** *(via Amazon Cognito)*: Credenciais de acesso, perfil e tipo de vínculo institucional.
- **Transações de Empréstimo** *(Amazon DynamoDB)*: Histórico de empréstimos, datas de devolução, status do material (`emprestado` | `devolvido` | `atrasado`) e matrícula/SIAPE vinculado.
- **Arquivos e Objetos** *(Amazon S3)*: Imagens de capa de materiais informacionais, manuais em PDF do SISBI e comprovantes digitais de renovação.

---

## 4. Estimativa de Preço da Infraestrutura (AWS)

A arquitetura é totalmente **Serverless** (gerenciada), o que elimina custos fixos de servidores. A maioria dos serviços se enquadra no **Free Tier** para o volume de uso esperado.

| Serviço AWS | Finalidade |
|---|---|
| **AWS Amplify** | Hospedagem e CI/CD do frontend |
| **Amazon Cognito** | Autenticação e autorização dos usuários |
| **Amazon API Gateway** | Roteamento das chamadas REST |
| **AWS Lambda** (3 funções) | C.R.U.D, Objetos (S3) e Agente IA |
| **Amazon DynamoDB** | Banco de dados NoSQL on-demand |
| **Amazon S3** | Armazenamento de objetos (Standard) |
| **Amazon Route 53** | Gerenciamento de DNS |

**URL pública da estimativa:** https://calculator.aws/#/estimate?id=218fa24340fda60abdd559238b59d4fcf05c0306

---

## 5. Arquitetura do Sistema

A solução é dividida entre um **frontend** em React e um **backend Serverless** na AWS, comunicando-se via API REST.

### Frontend — AWS Amplify (SPA)

Hospedado via AWS Amplify, construído com:

- **Core:** React + TypeScript
- **Estilização e UI:** Tailwind CSS, Framer Motion (animações) e React Icons
- **Formulários:** React Hook Form com validação via Zod
- **Roteamento e Requisições:** React Router DOM + Axios
- **Qualidade de Código:** ESLint + Prettier

### Backend — AWS Serverless

```
Usuário → Amplify (SPA)
             │
             ▼
         Route 53 (DNS)
             │
       ┌─────┴──────┐
       ▼            ▼
   Cognito       API Gateway
   (Auth)            │
                ┌────┼────┐
                ▼    ▼    ▼
           Lambda  Lambda  Lambda
           (CRUD) (OBJ.)  (Agente IA)
              │      │
           DynamoDB  S3
```

| Componente | Responsabilidade |
|---|---|
| **Route 53** | Direciona o domínio para o frontend (Amplify) e para a API (API Gateway) |
| **Cognito** | Autenticação e autorização, emite tokens JWT para usuários logados |
| **API Gateway** | Recebe requisições do frontend e distribui para as Lambdas correspondentes |
| **Lambda — C.R.U.D** | Regras de negócio: criar empréstimo, consultar acervo, atualizar renovação, persistir no DynamoDB |
| **Lambda — OBJ.** | Gerencia uploads/downloads de arquivos estáticos (capas, PDFs) no S3 |
| **Lambda — Agente IA** | Orquestra as chamadas ao LLM e executa ferramentas internas do sistema |

---

## 6. Conta do GitHub

- **Nome do repositório:** `web-2026-1-fernando`
- **Nome do usuário:** `fernandoalvess`
- **URL:** `https://github.com/fernandoalvess/web-2026-1-fernando`

---

## 7. Inserção de IA Generativa

A IA será implementada por meio de uma **função Lambda dedicada (Agente IA)**, que atua como um **orquestrador cognitivo** para o acervo da biblioteca.

### 7.1 Busca Semântica (LLM + Vetores)

O usuário poderá fazer perguntas em linguagem natural sobre o acervo, como:

> *"Quais livros de Engenharia de Software abordam metodologias ágeis e estão disponíveis?"*

O agente transforma a pergunta em embeddings/vetores e realiza uma **busca semântica** no acervo, retornando os materiais mais relevantes — indo além de uma simples busca por palavras-chave.

### 7.2 Chamadas de Ferramentas — Tool Use

O Agente não será apenas um chat: ele terá acesso a **ferramentas internas do sistema**. Exemplos:

> *"Renove todos os meus livros que vencem amanhã."*

Neste caso, a IA irá:
1. Interpretar a intenção do usuário;
2. Extrair os dados relevantes (livros com vencimento no dia seguinte);
3. Invocar a **ferramenta de renovação** do próprio sistema;
4. Executar a ação real em nome do usuário e confirmar o resultado.

Isso transforma o assistente em um agente que **age**, não apenas responde.
