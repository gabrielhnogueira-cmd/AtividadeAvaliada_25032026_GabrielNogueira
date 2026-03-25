# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: Gabriel Henrique Lopes Nogueira
RA: 25000243
Data: 25/03/2026

---

# 1. Definição do MVP
Meu MVP cobre o ciclo essencial de operação de balcão e gestão básica de suprimentos. 

**Dentro do MVP:** Processo de venda como a identificação de cliente, consulta de estoque e venda de controlados. Atualização automática de estoque, registro de compras e controle básico de contas a pagar e receber.
**Fora do MVP:** Relatórios avançados de BI, gestão de programas de fidelidade, transferências entre unidades e integração com APIs de convênios externos.
**Motivação:** Foquei nos dados de estoque e vendas que é o maior problema atual da rede.

---

# 2. Regras de Negócio

**RN01 — Validação de Receita:** Medicamentos controlados exigem obrigatoriamente a liberação digital do Farmacêutico.
**RN02 — Bloqueio de Estoque Negativo:** O sistema impede a venda de itens sem saldo disponível.
**RN03 — Registro Financeiro Automático:** Vendas a prazo geram automaticamente um título no Contas a Receber.
**RN04 — Atualização de Custo:** Toda entrada de mercadoria via fornecedor deve atualizar o preço de custo médio do produto.
**RN05 — Alerta de Reposição:** O sistema deve notificar o gerente quando o estoque atingir o limite mínimo.
