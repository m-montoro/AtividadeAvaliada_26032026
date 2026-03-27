# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: Murilo Montoro Marqui 
RA: 24000317  
Data: 26/03/2026  

---

# 1. Definição do MVP
Descreva aqui **qual parte do sistema** foi incluída no seu MVP.  
Explique claramente: Meu MVP cobre o processo central de funcionamento comercial e regulatório da farmácia indo desde agestão e consulta de estoque até os registros de clientes, pagamentos e a emissão de do comprovante

- O que está **dentro** do MVP:
  Dentro do meu MVP está o cadastro e consulta de cliente e medicamentos, um sistema de ponto de venda, fluxo completo de venda, um controle mais rígido de estoque impedindo a venda de itens zerados no estoque, e o registro obrigatório das receitas médicas para os medicamentos controlados
- O que está **fora** do MVP:
  O que não esta dentro do meu MVP são os modulos de recursos humanos (RH), como a folha de pagamento, está fora também o controle financeiro avançado, gestão de fornecedores e integração com o e-commerce 
- Por que você fez essas escolhas:
  Porque uma farmácia não sobrevive se nao conseguir vender os medicamento de uma forma mais rápida e prática obedecendo todas as leis da Anvisa. Eu foquei no essencial para que a farmácia possa abrir as portas, vender e controlar o que sai das prateleiras de forma eficaz.

---

# 2. Regras de Negócio (mínimo: 5)
Liste e descreva **cada RN** de forma clara.

**RN01 —**  **Venda de Medicamentos Controlados:** O sistema só eve permitir a venda de um medicamento controlado, assim como os famosos tarja preta, a partir do momento em que esta totalemtnte preenchido os dados da receita médica

**RN02 —**  **Bloqueio por Estoque insuficiente:** Fica proibido adicionar ao carrinho de compras uma quantidade de produtos maior do que a disponivel no estoque.

**RN03 —**  **Limite de Desconto por Balconista:** Cada balconista só pode conceder até 10% de desconto no valor total da vende, caso tenha descontos superiores a isso, vai ser necessário uma autenticação do gerente.

**RN04 —**  **Produtos Vencidos:** O sistema não deve permitir a venda de lotes de medicamentos cujo prazo de validade ja tenha vencido.

**RN05 —**  **Desconto para Terceira idade:** Clientes com idade igual ou superior a 60 anos possuem desconto automático de 5% em medicamentos genéricos (não acumulativo)

**RN06 —** **Proibição de Troca de Medicamentos Controlados:** De acordo com as leis da Anvisa o sistema não pode permitir, sob nenhuma hipótese, o fluxo de devolução ou troca de medicamentos controlados após conclusão da venda. 


---

# 3. Requisitos Funcionais (mínimo: 8)
Liste os requisitos funcionais do seu MVP.

**RF01 —**  O sistema deve permitir o cadastro, alteração, consulta e intaivação de clientes.

**RF02 —**  O sistema deve permitir o cadastro, alteração, consulta e inativação de medicamentos

**RF03 —**  O sistema deve permitir que o usuário adiciona e remova itens de um carrinho durante a venda

**RF04 —**  O sistema deve debitar automaticamente do estoque as quantidades de produtos vendidos após o momento da venda.

**RF05 —**  O sistema deve permitir a insercção do CRM do médico, UF e nome do médico para remédios controlados

**RF06 —**  O sistema deve calcular o valor total da venda, abatendo os descontos aplicados

**RF07 —** O sistema deve processar o pagamento repassando os valores para o gateway de pagamento 

**RF08 —** O sistema deve emitir e exibir na tela o cupom fiscal após a finalização da transação

**RF09 —** O sistema deve gerar um relatório de fechamento de caixa no final do turno, para melhor análise do valor total vendido, separando por forma de pagamento

**RF10 —** O sistema deve emitir um alerta visual na tela toda vez que um item for adicionado ao carrinho e o estoque atingir ou ficar abaixo da quantidade minima de segurança definida

---

# 🛡 4. Requisitos Não Funcionais (mínimo: 4)
Liste os RNFs do sistema conforme seu MVP.

**RNF01 —** **Desempanho** A consulta de medicamentos pelo nome ou código de barras deve retornar os resultados na dela em no máx. 2 seg

**RNF02 —**  **Usabilidade** O PDV deve ser acessivel via navegador, sem necessidade de instalação local em cada terminal

**RNF03 —**  **Segurança** Todas as senhas de usuários e dados sensíveis de clientes deve ser armazenatos utilizando criptografia 

**RNF04 —** **Disponibilidade** O sistema deve manter um uptime durante o horário de funcionamento da farmácia

**RNF05 —** **Rastreabilidade** O sistema deve registrar um log oculta e que não seja alterável de todas as vendas canceladas e dos descontos superiores aos permitidos para os balconistas, registrando quem fez, quando fez e quem autorizou

**RNF06 —** **Responsividade** A interface deve ser otimizada e plenamnte funcional nos monitores dos caixas de farmácias


---

# 5. Casos de Uso (mínimo: 10)
### Inserir **diagrama de casos de uso geral**, demonstrando claramente:
<img width="420" height="165" alt="image" src="https://github.com/user-attachments/assets/0ee9dfd7-8e78-4ebe-87a1-73e26c36b0c1" />


---

# 6. Documentação dos Casos de Uso
Para **cada caso de uso**, utilize o template abaixo:
---

## **UC01 — Realizar Venda**
**Ator(es):** Balconista  
**Descrição:** É o fluxo principal do PDV. O balconista pesquisa os produtos, insere no carrinho, verifica a situação e finaliza a transação.  
**Pré-condições:** O balconista deve estar autenticado no sistema (UC10) e deve haver conexão com o banco de dados.  
**Pós-condições:** Os produtos são baixados do estoque e a venda é registrada no histórico do sistema.  

### Fluxo Principal
1. O balconista inicia uma nova venda.  
2. O balconista adiciona os medicamentos desejados, consultando o estoque.  
3. O balconista finaliza a inserção de itens no carrinho.  
4. O sistema processa o pagamento.  
5. O sistema finaliza a transação e emite o comprovante.  

### Fluxos Alternativos / Exceções
- FA01 — **Medicamento Controlado:** Se um item for de venda restrita, o sistema solicita os dados da receita médica.  
- FA02 — **Inserção de Desconto:** O balconista decide inserir um desconto manual antes do pagamento.  
- EX01 — **Pagamento Recusado:** O sistema exibe erro de transação e retorna à tela de cobrança.  

### Relacionamentos
- **Include:** UC02 (Consultar Estoque), UC03 (Processar Pagamento), UC04 (Emitir Comprovante)  
- **Extend:** UC05 (Registrar Receita Médica), UC06 (Aplicar Desconto)  

<img width="313" height="817" alt="image" src="https://github.com/user-attachments/assets/413467fc-7152-407f-82a8-6216ce608838" />

---

## **UC02 — Consultar Estoque**
**Ator(es):** Balconista  
**Descrição:** O sistema ou o usuário checa a quantidade disponível de um item antes de prosseguir com a adição ao carrinho ou para informar ao cliente.  
**Pré-condições:** O usuário deve estar autenticado no sistema.  
**Pós-condições:** Nenhuma alteração no sistema, apenas exibição de dados.  

### Fluxo Principal
1. O balconista informa o código de barras, nome ou princípio ativo do medicamento.  
2. O sistema busca a informação na base de dados.  
3. O sistema retorna as quantidades disponíveis, lotes, validades e preços.  

### Fluxos Alternativos / Exceções
- EX01 — **Produto Não Encontrado:** O sistema exibe a mensagem "Produto não cadastrado" ou "Estoque zerado".  

### Relacionamentos
- **Include:** Nenhum (mas é incluído pelo UC01)  
- **Extend:** Nenhum  

<img width="420" height="290" alt="image" src="https://github.com/user-attachments/assets/1ec3389f-8fa5-4689-8b72-ef3e754ee396" />

---

## **UC03 — Processar Pagamento**
**Ator(es):** Sistema de Pagamento (Gateway) e Balconista  
**Descrição:** Trata a etapa de cobrança do cliente, integrando com as formas de pagamento disponíveis (Cartão, Dinheiro, PIX).  
**Pré-condições:** O carrinho de compras deve ter itens e o valor total deve ser maior que zero.  
**Pós-condições:** O valor é debitado/recebido e a transação de venda é dada como paga.  

### Fluxo Principal
1. O balconista seleciona a forma de pagamento desejada pelo cliente.  
2. O sistema envia o valor para o terminal (maquininha) ou gera o QR Code PIX.  
3. O cliente realiza o pagamento.  
4. O Gateway de pagamento retorna a confirmação de sucesso para o sistema.  

### Fluxos Alternativos / Exceções
- FA01 — **Pagamento em Dinheiro:** O balconista insere o valor recebido e o sistema calcula o troco a ser devolvido (sem passar pelo Gateway externo).  
- EX01 — **Saldo Insuficiente/Cartão Recusado:** A transação é abortada e o sistema solicita uma nova forma de pagamento.  

### Relacionamentos
- **Include:** Nenhum (incluído pelo UC01)  
- **Extend:** Nenhum  

<img width="356" height="550" alt="image" src="https://github.com/user-attachments/assets/804148d8-bddf-48d4-b1c5-186690af3151" />

---

## **UC04 — Emitir Comprovante**
**Ator(es):** Balconista (indiretamente)  
**Descrição:** Gera e imprime o cupom não fiscal ou a nota fiscal para o cliente após a conclusão da venda.  
**Pré-condições:** O pagamento da venda (UC03) deve ter sido aprovado com sucesso.  
**Pós-condições:** O comprovante é gerado e registrado no sistema.  

### Fluxo Principal
1. O sistema compila os dados da venda, incluindo itens, valores e dados do cliente.  
2. O sistema formata os dados para o layout padrão de impressão.  
3. O sistema envia a ordem de impressão para a impressora térmica.  

### Fluxos Alternativos / Exceções
- FA01 — **Envio Digital:** Caso o cliente não queira papel, o sistema envia o comprovante em PDF por E-mail ou WhatsApp.  
- EX01 — **Falha na Impressora:** O sistema salva o PDF em tela e avisa sobre a falha de comunicação com o hardware.  

### Relacionamentos
- **Include:** Nenhum (incluído pelo UC01)  
- **Extend:** Nenhum

  <img width="412" height="312" alt="image" src="https://github.com/user-attachments/assets/3df489bc-666a-4bfa-ad34-fe3f1367b5de" />

---

## **UC05 — Registrar Receita Médica**
**Ator(es):** Balconista  
**Descrição:** Permite a entrada de dados do receituário médico para retenção obrigatória pela Anvisa.  
**Pré-condições:** O balconista deve ter adicionado um item de uso controlado (tarja preta/vermelha) ao carrinho.  
**Pós-condições:** Os dados da receita ficam vinculados àquela venda específica no banco de dados.  

### Fluxo Principal
1. O sistema detecta a adição de um medicamento controlado e trava o avanço da venda.  
2. O sistema abre um formulário solicitando os dados: CRM, UF, Nome do Médico e Data da Prescrição.  
3. O balconista insere os dados lidos na receita física.  
4. O sistema valida o preenchimento e libera o item no carrinho.  

### Fluxos Alternativos / Exceções
- EX01 — **Receita Vencida:** Se a data da prescrição ultrapassar os dias legais permitidos (ex: 30 dias), o sistema bloqueia a venda daquele item e emite um alerta.  

### Relacionamentos
- **Include:** Nenhum  
- **Extend:** UC01 (Realizar Venda)  

<img width="366" height="367" alt="image" src="https://github.com/user-attachments/assets/4f9e8ca7-36b5-4030-b19c-5e7b28ab228c" />

---

## **UC06 — Aplicar Desconto**
**Ator(es):** Balconista  
**Descrição:** Permite reduzir o valor final da compra ou de um item específico para fidelizar o cliente.  
**Pré-condições:** O carrinho de compras deve conter itens e não estar finalizado.  
**Pós-condições:** O valor total da venda é recalculado.  

### Fluxo Principal
1. O balconista aciona a opção "Aplicar Desconto" na tela do PDV.  
2. O balconista insere a porcentagem ou o valor monetário desejado (ex: 5%).  
3. O sistema verifica as regras de negócio de limite de desconto.  
4. O sistema recalcula e atualiza o valor total da compra em tela.  

### Fluxos Alternativos / Exceções
- FA01 — **Desconto Superior ao Limite:** Se o desconto inserido for maior que 10%, o sistema aciona a necessidade de autorização gerencial.  

### Relacionamentos
- **Include:** Nenhum  
- **Extend:** UC01 (Realizar Venda), estendido por UC07 (Autorizar Desconto Especial)  

<img width="419" height="257" alt="image" src="https://github.com/user-attachments/assets/8e725519-b431-45e4-a071-46ade71ab116" />

---

## **UC07 — Autorizar Desconto Especial**
**Ator(es):** Gerente  
**Descrição:** Libera a aplicação de descontos que extrapolam a permissão padrão do balconista (acima de 10%).  
**Pré-condições:** O balconista deve ter tentado aplicar um desconto acima do limite permitido (FA01 do UC06).  
**Pós-condições:** O desconto é aplicado no carrinho ou a operação é recusada.  

### Fluxo Principal
1. O sistema exibe um pop-up solicitando login e senha do gerente na tela do PDV do balconista.  
2. O Gerente digita suas credenciais de acesso.  
3. O sistema valida as credenciais e verifica se o perfil possui privilégios de gerência.  
4. O sistema aprova e aplica o desconto elevado no carrinho.  

### Fluxos Alternativos / Exceções
- EX01 — **Credenciais Inválidas:** O sistema retorna uma mensagem de erro, registra a tentativa falha e aborta a aplicação do desconto.  

### Relacionamentos
- **Include:** Nenhum  
- **Extend:** UC06 (Aplicar Desconto)  

<img width="420" height="346" alt="image" src="https://github.com/user-attachments/assets/194066d2-5117-47f3-b494-eb1d9c91f6b0" />

---

## **UC08 — Gerenciar Clientes**
**Ator(es):** Balconista e Gerente  
**Descrição:** Módulo para manter a base de dados dos consumidores, essencial para aplicação de descontos de fidelidade ou para retenção de receitas.  
**Pré-condições:** O usuário deve estar autenticado no sistema.  
**Pós-condições:** O registro do cliente é inserido, atualizado, inativado ou consultado no banco de dados.  

### Fluxo Principal
1. O usuário acessa o módulo "Clientes" no menu principal.  
2. O usuário escolhe a opção para criar um "Novo" registro.  
3. O usuário preenche os dados obrigatórios: CPF, Nome completo, Data de Nascimento e Telefone.  
4. O usuário confirma a ação e o sistema salva o registro, exibindo mensagem de sucesso.  

### Fluxos Alternativos / Exceções
- FA01 — **Atualizar Cliente:** O usuário busca um cliente existente pelo CPF e altera seu telefone ou endereço.  
- EX01 — **CPF Duplicado:** Durante a criação, o sistema identifica que o CPF já existe e bloqueia a gravação, sugerindo a edição do cadastro atual.  

### Relacionamentos
- **Include:** Nenhum  
- **Extend:** Nenhum  

<img width="378" height="422" alt="image" src="https://github.com/user-attachments/assets/bf48a822-d6e3-45bd-8ad8-bbe775c45f17" />

---

## **UC09 — Gerenciar Medicamentos**
**Ator(es):** Gerente  
**Descrição:** Módulo de controle do portfólio de produtos, onde os remédios são cadastrados, classificados e precificados.  
**Pré-condições:** O usuário deve estar logado com um perfil que tenha privilégios de "Gerente".  
**Pós-condições:** O medicamento é registrado no sistema, ficando disponível para venda e controle de estoque.  

### Fluxo Principal
1. O gerente acessa o módulo "Medicamentos".  
2. O gerente clica em "Adicionar Medicamento".  
3. O gerente insere o código de barras, nome, fabricante, categoria (livre, tarja vermelha, tarja preta), e o preço de venda.  
4. O sistema valida os campos obrigatórios e salva as informações no banco de dados.  

### Fluxos Alternativos / Exceções
- FA01 — **Atualização de Preço:** O gerente busca um medicamento já existente e edita apenas a sua tabela de preço.  
- EX01 — **Código de Barras Duplicado:** O sistema recusa o cadastro alertando que já existe um produto com aquele código de barras.  

### Relacionamentos
- **Include:** Nenhum  
- **Extend:** Nenhum  

<img width="420" height="318" alt="image" src="https://github.com/user-attachments/assets/b7e44c1d-d951-4d5c-ae80-c3fd13f5ac0e" />

---

## **UC10 — Autenticar no Sistema**
**Ator(es):** Balconista, Gerente  
**Descrição:** Controle de acesso da aplicação para garantir segurança e rastreabilidade nas operações da farmácia.  
**Pré-condições:** O funcionário deve ter sido previamente cadastrado no sistema por um administrador.  
**Pós-condições:** Uma sessão segura é iniciada com o nível de permissão correto correspondente ao cargo do usuário.  

### Fluxo Principal
1. O funcionário acessa a tela de login inicial do PDV.  
2. O funcionário digita seu usuário (matrícula) e sua senha secreta.  
3. O sistema compara as credenciais com o banco de dados.  
4. O sistema autentica o usuário e o redireciona para a tela inicial (Dashboard ou PDV) de acordo com seu perfil.  

### Fluxos Alternativos / Exceções
- FA01 — **Recuperação de Senha:** O usuário clica em "Esqueci minha senha" e o sistema envia um link de redefinição para o e-mail cadastrado.  
- EX01 — **Senha Incorreta:** O sistema exibe a mensagem "Usuário ou senha inválidos". Após 3 tentativas falhas consecutivas, a conta é bloqueada temporariamente por segurança.  

### Relacionamentos
- **Include:** Nenhum  
- **Extend:** Nenhum

  <img width="420" height="455" alt="image" src="https://github.com/user-attachments/assets/f9b30010-d9a0-484d-8bd6-5b9d5496804f" />

