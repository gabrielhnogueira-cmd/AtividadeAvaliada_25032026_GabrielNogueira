# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: Gabriel Henrique Lopes Nogueira
RA: 25000243
Data: 25/03/2026

---

# 1. Definição do MVP
Descreva aqui **qual parte do sistema** foi incluída no seu MVP.  
Explique claramente:

- O que está **dentro** do MVP  
- O que está **fora** do MVP  
- Por que você fez essas escolhas  

Exemplo de início:  
> “Meu MVP cobre o processo de venda desde a identificação/cadastro do cliente até a emissão do comprovante, incluindo tratamento de estoque insuficiente.”

---

## 2. Regras de Negócio (RN)

* **RN01 — Validação de Receita:** Medicamentos controlados exigem obrigatoriamente a liberação digital do Farmacêutico.
* **RN02 — Bloqueio de Estoque Negativo:** O sistema impede a venda de itens sem saldo disponível.
* **RN03 — Registro Financeiro Automático:** Vendas a prazo geram automaticamente um título no "Contas a Receber".
* **RN04 — Atualização de Custo:** Toda entrada de mercadoria via fornecedor deve atualizar o preço de custo médio do produto.
* **RN05 — Alerta de Reposição:** O sistema deve notificar o gerente quando o estoque atingir o limite mínimo.
