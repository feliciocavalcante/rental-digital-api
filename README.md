# Rental Digital API

API REST robusta e escalável para sistema de aluguel digital, fornecendo endpoints seguros e eficientes para gerenciamento completo de aluguéis.

## 📋 Descrição

A **Rental Digital API** é uma API REST completa que serve como backend para o sistema de aluguel digital. Fornece funcionalidades de autenticação, gerenciamento de usuários, produtos, reservas e pagamentos, com foco em segurança, performance e escalabilidade.

## 🚀 Tecnologias Utilizadas

- **[Node.js](https://nodejs.org/)** - Runtime JavaScript
- **[Express.js](https://expressjs.com/)** - Framework web rápido e minimalista
- **[TypeScript](https://www.typescriptlang.org/)** - Superset do JavaScript com tipagem estática
- **[Prisma](https://www.prisma.io/)** - ORM moderno para banco de dados
- **[PostgreSQL](https://www.postgresql.org/)** - Banco de dados relacional robusto
- **[JWT](https://jwt.io/)** - Autenticação baseada em tokens
- **[Bcrypt](https://www.npmjs.com/package/bcrypt)** - Hash de senhas
- **[Zod](https://github.com/colinhacks/zod)** - Validação de esquemas TypeScript
- **[Swagger/OpenAPI](https://swagger.io/)** - Documentação da API
- **[Jest](https://jestjs.io/)** - Framework de testes

## 📦 Pré-requisitos

- **Node.js** (versão 18 ou superior)
- **npm** ou **yarn**
- **PostgreSQL** (versão 12 ou superior)
- **Redis** (para cache e sessões)

## 🛠️ Instalação e Configuração

### 1. Clone o Repositório

```bash
git clone https://github.com/feliciocavalcante/rental-digital-api.git
cd rental-digital-api
```

### 2. Instale as Dependências

```bash
npm install
```

### 3. Configuração do Banco de Dados

```bash
# Instalar PostgreSQL (Ubuntu/Debian)
sudo apt update
sudo apt install postgresql postgresql-contrib

# Criar banco de dados
sudo -u postgres createdb rental_digital_db

# Instalar Redis
sudo apt install redis-server
```

### 4. Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto:

```env
# Database
DATABASE_URL="postgresql://username:password@localhost:5432/rental_digital_db"
REDIS_URL="redis://localhost:6379"

# JWT
JWT_SECRET="your-super-secret-jwt-key"
JWT_EXPIRES_IN="7d"

# Server
PORT=3000
NODE_ENV=development

# Email (opcional)
SMTP_HOST="smtp.gmail.com"
SMTP_PORT=587
SMTP_USER="your-email@gmail.com"
SMTP_PASS="your-app-password"

# Payment (exemplo: Stripe)
STRIPE_SECRET_KEY="sk_test_..."
STRIPE_WEBHOOK_SECRET="whsec_..."

# File Upload
CLOUDINARY_CLOUD_NAME="your-cloud-name"
CLOUDINARY_API_KEY="your-api-key"
CLOUDINARY_API_SECRET="your-api-secret"

# Cors
FRONTEND_URL="http://localhost:5173"
```

### 5. Configuração do Prisma

```bash
# Gerar cliente Prisma
npx prisma generate

# Executar migrações
npx prisma migrate dev

# Seed do banco (opcional)
npx prisma db seed
```

### 6. Iniciar o Servidor

```bash
# Desenvolvimento
npm run dev

# Produção
npm run build
npm start
```

## 📝 Scripts Disponíveis

```bash
# Desenvolvimento com hot reload
npm run dev

# Build para produção
npm run build

# Iniciar servidor de produção
npm start

# Executar testes
npm test

# Executar testes com coverage
npm run test:coverage

# Lint do código
npm run lint

# Formatar código
npm run format

# Executar migrações do banco
npm run migrate

# Reset do banco de dados
npm run db:reset

# Visualizar banco de dados
npm run db:studio
```

## 🏗️ Estrutura do Projeto

```
rental-digital-api/
├── src/
│   ├── controllers/          # Controladores da API
│   │   ├── auth.controller.ts
│   │   ├── user.controller.ts
│   │   ├── product.controller.ts
│   │   └── rental.controller.ts
│   ├── middleware/           # Middlewares
│   │   ├── auth.middleware.ts
│   │   ├── validation.middleware.ts
│   │   └── error.middleware.ts
│   ├── routes/              # Definição das rotas
│   │   ├── auth.routes.ts
│   │   ├── user.routes.ts
│   │   ├── product.routes.ts
│   │   └── rental.routes.ts
│   ├── services/            # Lógica de negócios
│   │   ├── auth.service.ts
│   │   ├── user.service.ts
│   │   ├── product.service.ts
│   │   └── rental.service.ts
│   ├── models/              # Modelos de dados
│   ├── validators/          # Esquemas de validação Zod
│   ├── utils/               # Utilitários
│   ├── config/              # Configurações
│   └── app.ts               # Configuração principal do Express
├── prisma/
│   ├── schema.prisma        # Esquema do banco
│   ├── migrations/          # Migrações
│   └── seed.ts              # Dados iniciais
├── tests/                   # Testes
├── docs/                    # Documentação
├── package.json
└── README.md
```

## 🔌 Principais Endpoints

### Autenticação

```http
POST   /api/auth/register     # Registrar usuário
POST   /api/auth/login        # Login
POST   /api/auth/refresh      # Renovar token
POST   /api/auth/logout       # Logout
POST   /api/auth/forgot       # Esqueceu senha
POST   /api/auth/reset        # Resetar senha
```

### Usuários

```http
GET    /api/users             # Listar usuários
GET    /api/users/:id         # Buscar usuário por ID
PUT    /api/users/:id         # Atualizar usuário
DELETE /api/users/:id         # Deletar usuário
GET    /api/users/profile     # Perfil do usuário logado
PUT    /api/users/profile     # Atualizar perfil
```

### Produtos

```http
GET    /api/products          # Listar produtos
GET    /api/products/:id      # Buscar produto por ID
POST   /api/products          # Criar produto
PUT    /api/products/:id      # Atualizar produto
DELETE /api/products/:id      # Deletar produto
GET    /api/products/search   # Buscar produtos
```

### Aluguéis

```http
GET    /api/rentals           # Listar aluguéis
GET    /api/rentals/:id       # Buscar aluguel por ID
POST   /api/rentals           # Criar aluguel
PUT    /api/rentals/:id       # Atualizar aluguel
DELETE /api/rentals/:id       # Cancelar aluguel
GET    /api/rentals/my        # Meus aluguéis
```

### Pagamentos

```http
POST   /api/payments          # Processar pagamento
GET    /api/payments/:id      # Status do pagamento
POST   /api/payments/webhook  # Webhook do gateway
```

## 📚 Documentação da API

A documentação completa da API está disponível via Swagger:

```
http://localhost:3000/api-docs
```

### Exemplo de Uso

```javascript
// Registrar usuário
const response = await fetch('/api/auth/register', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    name: 'João Silva',
    email: 'joao@email.com',
    password: 'minhasenha123',
    phone: '85999999999'
  })
});

// Login
const loginResponse = await fetch('/api/auth/login', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    email: 'joao@email.com',
    password: 'minhasenha123'
  })
});

const { token } = await loginResponse.json();

// Buscar produtos
const products = await fetch('/api/products', {
  headers: {
    'Authorization': `Bearer ${token}`
  }
});
```

## 🔒 Autenticação e Autorização

A API utiliza **JWT (JSON Web Tokens)** para autenticação:

- **Registro/Login**: Retorna token JWT
- **Autorização**: Header `Authorization: Bearer <token>`
- **Refresh Token**: Renovação automática de tokens
- **Roles**: Sistema de permissões (USER, ADMIN)

### Middleware de Autenticação

```typescript
// Rotas protegidas
router.use(authMiddleware);

// Rotas apenas para admin
router.use(adminMiddleware);
```

## 🧪 Testes

```bash
# Executar todos os testes
npm test

# Testes com coverage
npm run test:coverage

# Testes em modo watch
npm run test:watch

# Testes de integração
npm run test:integration
```

### Estrutura de Testes

```
tests/
├── unit/                    # Testes unitários
├── integration/             # Testes de integração
├── fixtures/                # Dados de teste
└── setup.ts                 # Configuração dos testes
```

## 🚀 Deploy

### Deploy com Docker

```dockerfile
# Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]
```

```bash
# Build da imagem
docker build -t rental-digital-api .

# Executar container
docker run -p 3000:3000 rental-digital-api
```

### Deploy com Docker Compose

```yaml
# docker-compose.yml
version: '3.8'

services:
  api:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
    depends_on:
      - postgres
      - redis

  postgres:
    image: postgres:15
    environment:
      POSTGRES_DB: rental_digital_db
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

volumes:
  postgres_data:
```

## 📊 Monitoramento

### Health Check

```http
GET /api/health
```

```json
{
  "status": "OK",
  "timestamp": "2025-08-20T10:30:00Z",
  "services": {
    "database": "connected",
    "redis": "connected"
  }
}
```

### Logs

A API utiliza estrutura de logs para monitoramento:

```typescript
// Logger configurado
import logger from './utils/logger';

logger.info('API started successfully');
logger.error('Database connection failed', error);
```

## 🔧 Configuração de Produção

### Variáveis de Ambiente de Produção

```env
NODE_ENV=production
DATABASE_URL="postgresql://user:pass@prod-db:5432/rental_db"
REDIS_URL="redis://prod-redis:6379"
JWT_SECRET="super-secure-production-secret"
PORT=3000
```

### Otimizações

- **Rate Limiting**: Proteção contra spam
- **CORS**: Configurado para domínios específicos
- **Helmet**: Headers de segurança
- **Compression**: Compressão de resposta
- **Cache**: Redis para cache de consultas

## 🤝 Contribuindo

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-funcionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/nova-funcionalidade`)
5. Abra um Pull Request

### Padrões de Código

```bash
# Verificar padrões antes do commit
npm run lint
npm run format
npm test
```

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👨‍💻 Autor

**Felício Cavalcante**
- GitHub: [@feliciocavalcante](https://github.com/feliciocavalcante)

## 🆘 Suporte

Se você encontrar algum problema ou tiver dúvidas:

1. Verifique as [Issues](https://github.com/feliciocavalcante/rental-digital-api/issues) existentes
2. Crie uma nova issue com detalhes do problema
3. Consulte a [documentação da API](http://localhost:3000/api-docs)

## 📋 Roadmap

- [ ] Implementar notificações em tempo real
- [ ] Adicionar sistema de avaliações
- [ ] Implementar chat entre usuários
- [ ] Adicionar analytics avançados
- [ ] Implementar sistema de cupons
- [ ] Adicionar suporte a múltiplas moedas

---

⭐ **Se este projeto te ajudou, considere deixar uma estrela!**
