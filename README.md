# livraria-api_openapi_swagger
Continuação da livraria em node.js
# API Livros e Autores — OpenAPI 3.0 + Swagger UI

API REST em Node.js/Express com autenticação JWT, senhas com BCrypt e controle de acesso por perfil (RBAC).

## Requisitos
- Node.js 18 ou superior
- npm

## Instalação e execução
```bash
npm install
npm start
```

Servidor local: `http://localhost:3000`

- **Swagger UI:** `http://localhost:3000/docs`
- **Especificação OpenAPI JSON:** `http://localhost:3000/docs/api.json`

## Como testar rotas protegidas no Swagger
1. Abra `/docs`.
2. Execute `POST /api/v1/auth/login` com as credenciais de uma conta.
3. Copie somente o valor do campo `token` retornado.
4. Clique em **Authorize** e cole o token no campo Bearer. O Swagger adiciona o prefixo `Bearer` automaticamente.
5. Teste as rotas protegidas. Comentários aceitam `USER` ou `ADMIN`; criar livros/autores exige `ADMIN`.

A base de dados local `database.txt` é criada automaticamente quando a API inicia. O repositório inclui contas de demonstração pré-cadastradas; consulte `repositories/LivrariaRepository.js` para os dados iniciais e ajuste-os para seu ambiente antes de publicar em produção.

## Rotas documentadas
- `GET /api/v1/livros` — público
- `GET /api/v1/livros/{id}` — público
- `POST /api/v1/auth/register` — público
- `POST /api/v1/auth/login` — público
- `POST /api/v1/livros/{id}/comentarios` — USER ou ADMIN
- `POST /api/v1/autores` — ADMIN
- `POST /api/v1/livros` — ADMIN

## Segurança
Defina `JWT_SECRET` como variável de ambiente forte antes de publicar a API. Não utilize o segredo padrão em produção. Os códigos `400`, `401`, `403`, `404`, `409`, `422` e `500` são documentados conforme a rota; a aplicação atual retorna `400` para várias falhas de validação e não possui middleware dedicado para produzir `422`.
