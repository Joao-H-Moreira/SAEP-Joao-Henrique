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

