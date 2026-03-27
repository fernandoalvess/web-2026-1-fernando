# SIFU - Sistema Integrado Funcional e Unificado

**Sistema Integrado Funcional e Unificado | UFERSA**

[![GitHub repo](https://img.shields.io/badge/GitHub-fernandoalvess/web--2026--1--fernando-blue)](https://github.com/fernandoalvess/web-2026-1-fernando)
[![UFERSA](https://img.shields.io/badge/Instituição-UFERSA-green)](https://www.ufersa.edu.br/)

## 📋 Descrição do Projeto

O **SIFU** é um sistema moderno para otimizar o processo, uma das funcionalidades é o **Empréstimo ou Renovação de Material Informacional** na Universidade Federal Rural do Semi-Árido (UFERSA). O projeto visa automatizar o controle de circulação do acervo da biblioteca, permitindo renovações online simplificadas e agilizando o check-out presencial com validação automática de pendências do usuário.

### 🎯 Processo Escolhido

- **Empréstimo ou Renovação de Material Informacional**
- [Portfólio EP Completo](https://ep.ufersa.edu.br/wp-content/uploads/portfolioep/ensino/emprestimoourenovacaodematerial/index.html#normal)

## 🚀 Funcionalidades Principais

- **Renovações Online**: Usuários podem renovar materiais diretamente pelo portal, sem necessidade de deslocamento.
- **Check-out Presencial Automatizado**: Validação automática de pendências do usuário no balcão.
- **Consulta de Acervo**: Busca avançada no catálogo da biblioteca.
- **Busca Semântica com IA**: Perguntas em linguagem natural sobre o acervo, utilizando embeddings e vetores para resultados mais relevantes.
- **Gestão de Usuários**: Autenticação via Amazon Cognito para discentes, docentes e técnicos-administrativos.
- **Administração**: Ferramentas para servidores da biblioteca registrarem saídas, inserir tombos e gerenciar status.

## 👥 Perfis de Usuário

| Perfil                                          | Descrição                                                                                                                                            |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Discente / Docente / Técnico-Administrativo** | Usuários finais que acessam o portal para consultar o acervo, realizar renovações e gerenciar seus empréstimos.                                      |
| **Servidor do SISBI (Biblioteca)**              | Possui privilégios de administrador para registrar saídas de materiais, inserir tombos, desmagnetizar itens e conferir status de usuários no balcão. |

## 🏗️ Arquitetura do Sistema

O SIFU é dividido em **frontend** (React) e **backend Serverless** na AWS, comunicando-se via API.

## 🤖 Inserção de IA Generativa

A IA será implementada por meio de uma **função Lambda dedicada (Agente IA)**, que atua como um **orquestrador** para o acervo da biblioteca.

### Busca Semântica

O usuário poderá fazer perguntas em linguagem natural sobre o acervo, como:

> _"Quais livros de Engenharia de Software abordam metodologias ágeis e estão disponíveis?"_

O agente realiza uma **busca semântica** no acervo, retornando os materiais mais relevantes, indo além de uma simples busca por palavras-chave.

## 📁 Estrutura do Projeto

```
web-2026-1-fernando/
├── README.md                 # Este arquivo
├── docs/
│   ├── sifu_descricao_projeto.md  # Descrição detalhada do projeto
│   ├── sifu_descricao_projeto.pdf # PDF da descrição (com links clicáveis)
│   └── calculator_aws.pdf         # Estimativa AWS em PDF
└── [futuras pastas do código]
```

## 🚀 Como Usar

1. **Clone o repositório:**

   ```bash
   git clone https://github.com/fernandoalvess/web-2026-1-fernando.git
   cd web-2026-1-fernando
   ```

2. **Consulte a documentação:**
   - Leia o [arquivo de descrição completa](./docs/sifu_descricao_projeto.md)
   - Visualize os PDFs em `./docs/` para detalhes visuais

3. **Para desenvolvimento futuro:**
   - Instale as dependências do frontend (React/TypeScript)
   - Configure as credenciais AWS para o backend Serverless

## 📞 Contato

- **Autor:** Fernando Alves
- **GitHub:** [@fernandoalvess](https://github.com/fernandoalvess)
- **Instituição:** Universidade Federal Rural do Semi-Árido (UFERSA)
