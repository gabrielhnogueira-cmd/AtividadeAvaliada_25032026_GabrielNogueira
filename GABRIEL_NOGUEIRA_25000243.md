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
- FA01 — Se o item for controlado, o sistema bloqueia a inserção até que o Farmacêutico insira sua senha e valide a receita médica.
- FA02 — Se a opção for "A Prazo", o sistema verifica o limite de crédito do cliente e gera um lançamento automático no contas a receber.

### Relacionamentos
- **Include:** UC02 (Consultar Estoque), UC03 (Identificar Cliente).  
- **Extend:** UC05 (Validar Receita), UC06 (Gerar Contas a Receber).

<img width="786" height="424" alt="image" src="https://github.com/user-attachments/assets/45a28f82-7cb8-48b1-8169-967ff5dc0f53" />

---

## **UC02 — Consultar Estoque**
**Ator(es):** Atendente, Gerente.

**Descrição:** Verificar a disponibilidade física de um item em tempo real.

**Pré-condições:** Produto cadastrado. 

**Pós-condições:** Informação de saldo exibida.

### Fluxo Principal
1. Informar nome ou código; 
2. Sistema busca saldo; 
3. Exibir quantidade.

### Fluxos Alternativos / Exceções
- FA01 — Caso o produto esteja zerado na unidade atual, o usuário pode solicitar a verificação de saldo em outras farmácias da rede.
- FA02 — Se o código ou nome informado não retornar resultados, o sistema exibe a mensagem "Produto não cadastrado" e oferece a opção de novo cadastro

### Relacionamentos 
- **Extend:** UC04 (Cadastrar Produto/Cliente), UC10 (Emitir Relatórios/Alertas).

<img width="445" height="433" alt="image" src="https://github.com/user-attachments/assets/0bb34def-7160-4921-a1fc-91715cc48fdc" />

---

## **UC03 — Identificar Cliente**
**Ator(es):** Atendente.

**Descrição:** Localizar o cadastro de um cliente para vincular à venda ou consulta.

**Pré-condições:** O atendente deve estar autenticado no sistema;. 

**Pós-condições:** O cliente é identificado e vinculado à operação atual;.

### Fluxo Principal
1. Solicitar CPF ou Nome; 
2. Sistema pesquisa na base central; 
3. Exibir dados do cliente.

### Fluxos Alternativos / Exceções
- FA01 — Se o cliente não for encontrado, o sistema sugere o redirecionamento para o cadastro

### Relacionamentos 
- **Extend:** UC04 (Cadastrar Cliente).

<img width="599" height="206" alt="image" src="https://github.com/user-attachments/assets/916240d5-2e1f-4500-a551-a9624a46b3f2" />

---

## **UC04 — Cadastrar Cliente / Produto**
**Ator(es):** Atendente, Gerente.

**Descrição:** Realizar a inclusão de novos registros de clientes ou produtos no sistema centralizado da rede.

**Pré-condições:** Usuário deve ter permissão de acesso ao módulo de cadastros;

**Pós-condições:** Novo registro salvo no banco de dados;

### Fluxo Principal
1. Novo Cadastro;
2. Solicita a categoria; 
3. Preenche os campos obrigatórios;  
4. Valida se o registro já existe;
5. Confirma a gravação dos dados.

### Fluxos Alternativos / Exceções
- FA01 — Se o CPF ou o Código de Barras já constar no sistema, o sistema exibe erro e impede a gravação.
- FA02 — Se campos obrigatórios estiverem vazios, o sistema destaca os campos em vermelho.

### Relacionamentos
- **Include:** UC03 (Identificar Cliente), UC02 (Consultar Estoque).  
- **Extend:** UUC04 (Validar Dados).

<img width="786" height="374" alt="image" src="https://github.com/user-attachments/assets/f246751c-6bd7-4376-a179-618cc1026162" />

---












