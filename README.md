# desafio-prompt-n8n
# Planejamento de Automação no N8N — Registro de Leads CloudDb

---

## 📌 Passo 1: Defina a automação desejada

* **Objetivo:** Criar uma automação no N8N para registrar automaticamente os leads recebidos por formulário no site da CloudDb.
* **Público / Responsável:** Equipe comercial da CloudDb.
* **Resultado esperado:** Salvar os dados em uma planilha e enviar uma notificação para Luiza (time de vendas).

---

## ⚙️ Passo 2: Adicione contexto e regras

### 🛠️ Ferramentas envolvidas
* **Google Forms**
* **Google Sheets**
* **Gmail**

### 🔄 Fluxo desejado
1. Receber uma nova resposta do formulário.
2. Registrar os dados na planilha.
3. Enviar um e-mail de confirmação/notificação.

### ⚠️ Regras importantes
* **Validação:** Ignorar registros sem e-mail válido.
* **Classificação:** Classificar os clientes em:
  * Novo
  * Esporádico / Exploratório
  * Antigo / Recorrente

---

## 🚀 Passo 3: Monte o prompt final

> **Prompt:**
> 
> Atue como um especialista em N8N.
> 
> Crie uma automação para registrar leads recebidos por formulário.
> 
> * **Público:** Equipe comercial, liderada pela Graciele.
> * **Ferramentas envolvidas:** Google Forms, Google Sheets e Gmail (a CloudDb possui conta no Google Workspace/G Suite).
> * **Campos coletados no formulário:**
>   * Nome do contato
>   * Data de preenchimento
>   * Dores da empresa (*pré-análise do trabalho requisitado*)
>   * Checkbox/opções de classificação do cliente (*Novo, Esporádico, Recorrente*)
> * **Fluxo de execução:**
>   1. Receber os dados do formulário dos clientes.
>   2. Salvar os dados na planilha do Google Sheets.
>   3. Enviar e-mails de confirmação e notificação interna.
> * **Regras de negócio:**
>   * Ignorar registros sem e-mail válido.
>   * Padronizar/validar a classificação dos clientes (*Novo, Esporádico, Recorrente*).
> 
> Explique quais nós do N8N devem ser utilizados e a lógica detalhada de funcionamento do workflow.

---

## 📊 Arquitetura do Workflow (Diagrama)

```text
[Google Forms Trigger / Webhook]
               │
               ▼
   [Filter / If Node] ──── (E-mail inválido/vazio) ──► [Stop and End]
               │
         (E-mail Válido)
               │
               ▼
     [Code / Edit Fields] ──► (Tratamento de dados & Classificação do cliente)
               │
               ▼
     [Google Sheets Node] ──► (Append row: Registra na planilha da CloudDb)
               │
               ▼
       [Gmail Node] ──► (Notifica a Luiza / Equipe Comercial)
               │
               ▼
 [Gmail Node (Opcional)] ──► (Confirmação automática de recebimento ao cliente)
