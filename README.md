Instale o Node.js & npm installed - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)

Siga os passos

```sh

git clone <YOUR_GIT_URL>


cd <YOUR_PROJECT_NAME>


npm i

nmp install vite@v4
npm run dev
```


Esse projeto foi feito com:

- Vite
- TypeScript
- React
- shadcn-ui
- Tailwind CSS


1. **Requisitos Funcionais (RF)**

**RF001 – Cadastro automático de perfil de usuário**

- O sistema deve criar automaticamente um registro na tabela **profiles** sempre que um novo usuário for criado em auth.users.

**RF002 – Visualização do próprio perfil**

- O usuário deve poder visualizar apenas o seu próprio perfil.

**RF003 – Atualização do próprio perfil**

- O usuário deve poder atualizar somente os dados do seu próprio perfil.

**RF004 – Cadastro de categorias**

- Usuários autenticados devem poder criar categorias.

**RF005 – Visualização de categorias**

- Usuários autenticados devem poder visualizar todas as categorias existentes.

**RF006 – Atualização de categorias**

- Usuários autenticados devem poder atualizar categorias.

**RF007 – Exclusão de categorias**

- Usuários autenticados devem poder excluir categorias.

**RF008 – Cadastro de produtos**

- Usuários autenticados devem poder cadastrar produtos, vinculando-os a categorias.

**RF009 – Visualização de produtos**

- Usuários autenticados devem poder visualizar todos os produtos cadastrados.

**RF010 – Atualização de produtos**

- Usuários autenticados devem poder atualizar informações de produtos.

**RF011 – Exclusão de produtos**

- Usuários autenticados devem poder excluir produtos.

**RF012 – Registro de movimentações de estoque**

- O sistema deve permitir que usuários autenticados registrem movimentações (entrada/saída) de estoque.

**RF013 – Associação de movimentações ao responsável**

- Cada movimentação deve registrar automaticamente o usuário responsável.

**RF014 – Atualização automática da quantidade do produto**

- Ao inserir uma movimentação:
    - Se for **entrada**, deve somar.
    - Se for **saída**, deve subtrair sem permitir valor negativo.

**RF015 – Consulta de movimentações**

- Usuários autenticados devem poder visualizar todas as movimentações de estoque.

**RF016 – Atualização automática da coluna updated_at de produtos**

- Sempre que um produto for atualizado, o campo updated_at deve ser atualizado automaticamente.
1. **DER (Diagrama Entidade-Relacionamento) – Descrição Textual**

**Entidade: profiles**

- **id (PK, FK → auth.users.id)**
- full_name
- created_at

**Relacionamento:**

- Um **usuário** possui **um perfil** (1:1)

**Entidade: categories**

- **id (PK)**
- name (único)
- description
- created_at

**Relacionamento:**

- Uma categoria possui vários produtos (1:N)

**Entidade: products**

- **id (PK)**
- name
- description
- category_id (FK → categories.id)
- unit
- current_quantity
- minimum_quantity
- created_at
- updated_at

**Relacionamento:**

- Cada produto pertence a uma categoria (N:1)
- Um produto possui várias movimentações (1:N)

**Entidade: stock_movements**

- **id (PK)**
- product_id (FK → products.id)
- movement_type
- quantity
- responsible_user_id (FK → auth.users.id)
- notes
- created_at

**Relacionamento:**

- Cada movimentação é feita por **um usuário** (N:1)
- Cada movimentação se refere a **um produto** (N:1)
1. **DER em formato de diagrama (ASCII)**

<img width="697" height="649" alt="image" src="https://github.com/user-attachments/assets/ec541807-16ea-4189-bcc2-3ed040ef3ff3" />


1. **DER em formato de lista (para ferramenta CASE)**

**profiles**

- id (PK, FK → auth.users.id)
- full_name
- created_at

**categories**

- id (PK)
- name (UNIQUE)
- description
- created_at

**products**

- id (PK)
- name
- description
- category_id (FK → categories.id)
- unit
- current_quantity
- minimum_quantity
- created_at
- updated_at

**stock_movements**

- id (PK)
- product_id (FK → products.id)
- movement_type (entrada/saida)
- quantity
- responsible_user_id (FK → auth.users.id)
- notes
- created_at

.

🔵RF001 – Cadastro automático de perfil de usuário
CT001 – Criar perfil automaticamente ao criar usuário

Pré-condições: Acesso ao sistema com permissão para criar usuários.
Objetivo: Validar se o perfil é criado automaticamente.
Passos:

Criar um novo usuário via auth.users.

Acessar a tabela profiles.

Pesquisar registro com id igual ao id do novo usuário.
Resultado Esperado:

Um registro deve ser criado em profiles com o mesmo id do usuário, preenchendo full_name como nulo (ou padrão) e created_at automático.

🔵 RF002 – Visualização do próprio perfil
CT002 – Usuário acessa seu próprio perfil

Pré-condições: Usuário autenticado.
Passos:

Realizar login.

Acessar endpoint/tela “Meu perfil”.
Resultado Esperado:

O usuário visualiza somente seu próprio perfil.

CT003 – Usuário tenta acessar perfil de outro usuário

Pré-condições: Dois usuários cadastrados.
Passos:

Logar como Usuário A.

Tentar acessar perfil do Usuário B via API/URL.
Resultado Esperado:

Sistema bloqueia o acesso (403 Forbidden ou equivalente).

🔵 RF003 – Atualização do próprio perfil
CT004 – Atualizar perfil com sucesso

Pré-condições: Usuário autenticado.
Passos:

Logar.

Abrir tela “Meu perfil”.

Alterar campos permitidos (ex.: full_name).

Salvar.
Resultado Esperado:

Sistema atualiza apenas o perfil logado.

CT005 – Impedir atualização de perfil de outro usuário

Passos:

Logar como Usuário A.

Enviar requisição para atualizar perfil de Usuário B.
Resultado Esperado:

Atualização bloqueada.

🔵 RF004 – Cadastro de categorias
CT006 – Criar categoria

Pré-condições: Usuário autenticado.
Passos:

Enviar dados válidos (name, description).

Submeter criação.
Resultado Esperado:

Categoria cadastrada na tabela categories.

🔵 RF005 – Visualização de categorias
CT007 – Listar todas as categorias

Passos:

Usuário autenticado acessa lista de categorias.
Resultado Esperado:

Todas as categorias existentes são exibidas.

🔵 RF006 – Atualização de categorias
CT008 – Atualizar categoria existente

Passos:

Selecionar categoria cadastrada.

Alterar campos.

Salvar.
Resultado Esperado:

Categoria atualizada com sucesso.

🔵 RF007 – Exclusão de categorias
CT009 – Excluir categoria existente

Passos:

Selecionar categoria.

Executar exclusão.
Resultado Esperado:

Categoria removida da tabela categories.

🔵 RF008 – Cadastro de produtos
CT010 – Cadastrar produto vinculado a categoria

Pré-condições: Categoria criada.
Passos:

Enviar campos válidos (name, category_id, unit etc.)

Submeter.
Resultado Esperado:

Produto cadastrado com category_id válido.

current_quantity inicial conforme regra (ex.: 0).

🔵 RF009 – Visualização de produtos
CT011 – Listar todos os produtos

Passos:

Usuário autenticado acessa lista de produtos.
Resultado Esperado:

Todos os produtos cadastrados são exibidos.

🔵 RF010 – Atualização de produtos
CT012 – Atualizar informações do produto

Passos:

Selecionar produto.

Alterar descrição, unit ou minimum_quantity.

Salvar.
Resultado Esperado:

Produto atualizado com sucesso.

Campo updated_at deve alterar (relacionado ao RF016).

🔵 RF011 – Exclusão de produtos
CT013 – Excluir produto

Passos:

Selecionar produto.

Executar exclusão.
Resultado Esperado:

Produto removido da tabela products.

🔵 RF012 – Registro de movimentações de estoque
CT014 – Registrar entrada de estoque

Passos:

Selecionar produto.

Criar movimentação do tipo "entrada" com quantidade X.
Resultado Esperado:

Registro criado em stock_movements.

Quantidade somada ao current_quantity (RF014).

CT015 – Registrar saída de estoque

Passos:

Selecionar produto.

Criar movimentação tipo "saída".
Resultado Esperado:

Registro criado.

Quantidade subtraída do current_quantity sem permitir valor negativo.

CT016 – Impedir saída maior que quantidade atual

Passos:

Tentar criar saída com quantity > current_quantity.
Resultado Esperado:

Sistema nega operação.

🔵 RF013 – Associação de movimentações ao responsável
CT017 – Registrar movimentação com responsável automático

Passos:

Logar.

Criar movimentação de estoque.
Resultado Esperado:

Campo responsible_user_id é preenchido automaticamente com o id do usuário logado.

🔵 RF014 – Atualização automática da quantidade
CT018 – Atualização correta para entrada

Passos:

Verificar quantidade atual.

Criar movimentação de entrada.
Resultado Esperado:

current_quantity = quantidade anterior + quantidade da entrada.

CT019 – Atualização correta para saída

Passos:

Verificar quantidade atual.

Criar movimentação de saída.
Resultado Esperado:

current_quantity = quantidade anterior – quantidade da saída.

🔵 RF015 – Consulta de movimentações
CT020 – Listar todas as movimentações

Passos:

Usuário autenticado acessa lista de movimentações.
Resultado Esperado:

Todas as movimentações são exibidas, incluindo produto, tipo, quantidade e responsável.

🔵 RF016 – Atualização automática do updated_at
CT021 – Alterar produto e validar updated_at

Passos:

Capturar valor atual de updated_at.

Atualizar qualquer campo editável do produto.

Consultar produto novamente.
Resultado Esperado:

updated_at deve ser alterado automaticamente para timestamp atual.
