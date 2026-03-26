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
- **Extend:** UC04 (Validar Dados).

<img width="786" height="374" alt="image" src="https://github.com/user-attachments/assets/f246751c-6bd7-4376-a179-618cc1026162" />

---

## **UC05 — Validar Receita**
**Ator(es):** Farmacêutico.

**Descrição:** Realizar a conferência técnica e legal da receita médica apresentada pelo cliente para autorizar a venda de medicamentos de uso controlado.

**Pré-condições:** Um item classificado como "Controlado" deve ter sido adicionado ao carrinho;

**Pós-condições:** O item é liberado para finalização da venda;

### Fluxo Principal
1. Detecta a tentativa de venda de um produto controlado e bloqueia a operação;
2. Solicita a intervenção do Farmacêutico; 
3. Farmacêutico analisa a receita física;
4. Farmacêutico insere os dados da receita no sistema;
5. Farmacêutico autoriza a liberação mediante senha;
6. Sistema desbloqueia o item para conclusão da venda.

### Fluxos Alternativos / Exceções
- FA01 — Se a receita não atender aos requisitos legais, o Farmacêutico nega a autorização no sistema. O item é removido da venda e o sistema gera um log de tentativa de venda não autorizada.
- FA02 — Se os dados do paciente na receita não conferem com o cadastro do cliente, o Farmacêutico deve corrigir o cadastro ou recusar a venda.

### Relacionamentos
- **Include:** UC09 (Atualizar Estoque).  
- **Extend:** UC01 (Realizar Venda).

<img width="676" height="299" alt="image" src="https://github.com/user-attachments/assets/cd46bf9a-4595-49fb-b6df-9b6187fd9a6d" />

---

## **UC06 — Gerar Contas a Receber**
**Ator(es):** Sistema, Financeiro.

**Descrição:** Registrar formalmente uma dívida do cliente com a farmácia, gerando um título financeiro com data de vencimento e valor atualizado após uma venda a prazo.

**Pré-condições:** Deve ter sido finalizado com a opção de pagamento "A Prazo";

**Pós-condições:** Um novo título financeiro é gerado no módulo de contas a receber;

### Fluxo Principal
1. Sistema recebe a confirmação da venda com a modalidade "A Prazo";
2. Sistema identifica o cliente vinculado à transação;
3. Sistema calcula a data de vencimento
4. Sistema gera o título financeiro contendo: Valor, Data de Emissão, Vencimento e ID da Venda;
5. Sistema abate o valor total da venda do limite de crédito disponível do cliente;
6. Sistema emite uma "Nota de Débito" para assinatura do cliente no balcão.

### Fluxos Alternativos / Exceções
- FA01 — Se o valor da venda for superior ao limite disponível do cliente, o sistema bloqueia a geração do título e solicita ao atendente que mude a forma de pagamento ou reduza o valor da compra.
- FA02 — Se o sistema detectar títulos já vencidos e não pagos para aquele CPF, a geração de novas contas a receber é bloqueada automaticamente.

### Relacionamentos
- **Include:** UC01 (Realizar Venda).  

<img width="711" height="337" alt="image" src="https://github.com/user-attachments/assets/160ac6c0-6f51-4b64-b4b1-a3c41c64adda" />

---

## **UC07 — Registrar Compra (Entrada)**
**Ator(es):** Gerente.

**Descrição:** Entrada de nota fiscal de fornecedores para reposição.

**Pré-condições:** Pedido recebido.

**Pós-condições:** Estoque e Financeiro atualizados.

### Fluxo Principal
1. Acessar módulo "Entrada de Mercadorias";
2. Importar XML ou chave da Nota Fiscal;
3. Conferir itens, quantidades e preços carregados pelo sistema;
4. Confirmar o registro da compra;
5. Sistema atualiza saldo do estoque;
6. Sistema gera conta a pagar.

### Fluxos Alternativos / Exceções
- FA01 — Caso a entrada contenha itens de bonificação (custo zero), o sistema registra a entrada no estoque sem gerar título no Contas a Pagar.
- FA02 — Se o valor na nota for diferente do pedido de compra original, o sistema exibe um alerta e solicita autorização especial ou permite a recusa parcial da nota.

### Relacionamentos
- **Include:** UC08 (Lançar Contas a Pagar), UC09 (Atualizar Estoque). 
- **Extend:** UC04 (Cadastrar Produto).

<img width="749" height="371" alt="image" src="https://github.com/user-attachments/assets/b3202caa-e456-4920-b84c-ed30ebf27382" />

---

## **UC08 — Lançar Contas a Pagar**
**Ator(es):** Financeiro.

**Descrição:** Registro de obrigações financeiras (Fornecedores, Aluguel, Luz).

**Pré-condições:** Documento fiscal ou fatura em mãos.

**Pós-condições:** Despesa agendada no fluxo de caixa.

### Fluxo Principal
1. O usuário acessa o módulo "Contas a Pagar";
2. Seleciona o tipo de despesa;
3. Insere os dados do título
4. O sistema valida os dados inseridos;
5. O sistema registra a obrigação no financeiro;

### Fluxos Alternativos / Exceções
- FA01 — Se a conta já foi paga, o sistema registra o lançamento e já marca como "Liquidado", atualizando o saldo bancário.
- FA02 — Se o sistema detectar um boleto com o mesmo código de barras já cadastrado, ele exibe um erro e impede o novo lançamento.

### Relacionamentos
- **Include:** UC10 (Emitir Relatórios/Alertas)

<img width="1003" height="329" alt="image" src="https://github.com/user-attachments/assets/6511f28a-aa7f-4d2f-9496-8e2a7cc521aa" />

---

## **UC09 — Atualizar Estoque**
**Ator(es):** Sistema.

**Descrição:** Processo automatizado de incremento ou decremento de saldo.

**Pré-condições:** Ocorre após Venda, Devolução ou Compra.

**Pós-condições:** Saldo físico atualizado.

### Fluxo Principal
1. O sistema recebe a notificação de movimento
2. Identifica o tipo de operação;
3. Gravar o novo saldo no banco de dados;

### Fluxos Alternativos / Exceções
- FA01 — Se uma venda solicitar mais itens do que o disponível, o sistema bloqueia a atualização e emite um erro de "Inconsistência de Inventário".
- FA02 — Se o sistema detectar que o item movimentado pertence a um lote vencido, ele bloqueia a saída e notifica o gerente.

### Relacionamentos
- **Extend:** UC10 (Emitir Relatórios/Alertas)

<img width="728" height="477" alt="image" src="https://github.com/user-attachments/assets/e27aa717-f6b7-4c4e-ab23-81fa97d4564d" />

---

## **UC10 — Emitir Relatórios**
**Ator(es):** Gerente.

**Descrição:** Gerar documentos de conferência (Mais Vendidos, Estoque Baixo).

**Pré-condições:** Dados existentes no período selecionado.

**Pós-condições:** Relatório exibido em tela ou impresso.

### Fluxo Principal
1. Acessar módulo "Relatórios e Indicadores";
2. Selecionar o tipo de relatório
3. Definir filtros de busca
4. Sistema processa os dados do banco;
5. Sistema exibe o relatório formatado;
6. Usuário seleciona imprimir ou salvar arquivo.

### Fluxos Alternativos / Exceções
- FA01 — O sistema monitora a atualização de estoque e exibe um alerta imediato se o saldo atingir o nível crítico.
- FA02 — Se não houver dados no período selecionado, o sistema informa que não há registros.

### Relacionamentos
- **Extend:** UC02 (Consultar Estoque), UC08 (Contas a Pagar), UC09 (Atualizar Estoque).

<img width="449" height="664" alt="image" src="https://github.com/user-attachments/assets/16fdb578-9bf6-48a5-9ad3-425dc9fbfaeb" />

---


















