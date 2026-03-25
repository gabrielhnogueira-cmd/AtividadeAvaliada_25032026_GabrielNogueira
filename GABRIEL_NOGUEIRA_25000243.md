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

**RN04 — Atualização de Custo:** Toda entrada de mercadoria do fornecedor deve atualizar o preço de custo médio do produto.

**RN05 — Alerta de Reposição:** O sistema deve notificar o gerente quando o estoque atingir o limite mínimo.

---

# 3. Requisitos Funcionais 

**RF01 —** Realizar venda de produtos.

**RF02 —** Consultar estoque em tempo real.
  
**RF03 —** Cadastrar clientes e fornecedores.
  
**RF04 —** Registrar entrada de mercadorias.
  
**RF05 —** Validar receitas médicas para produtos controlados.
  
**RF06 —** Gerar contas a pagar a partir de compras.
  
**RF07 —** Gerar contas a receber a partir de vendas a prazo.
  
**RF08 —** Emitir comprovante de venda detalhado.

---

# 4. Requisitos Não Funcionais 

**RNF01 —** O sistema deve ser acessível via Web.

**RNF02 —** O tempo de processamento de uma venda não deve exceder 5 segundos.

**RNF03 —** Controle de acesso por perfis comoa a atendente, farmacêutico e o gerente.

**RNF04 —** Persistência de dados em banco de dados com backup diário.

---

# 5. Casos de Uso

## **UC01 — Realizar Venda**
**Ator(es):** Atendente.

**Descrição:** Registrar a saída de produtos e o recebimento de valores.

**Pré-condições:** Usuário logado e produto em estoque. 

**Pós-condições:** Estoque baixado e venda registrada.

### Fluxo Principal
1. Iniciar venda; 
2. Identificar Cliente; 
3. Adicionar itens;  
4. Selecionar pagamento;
5. Finalizar.

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** UC02 (Consultar Estoque), UC03 (Identificar Cliente).  
- **Extend:** UC05 (Validar Receita), UC06 (Gerar Contas a Receber).


