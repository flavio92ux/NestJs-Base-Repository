# NestJS Project Backend

Um projeto backend construído com **NestJS**, utilizando **SQLite3** como banco de dados e **TypeORM** para gerenciamento de dados com validação de dados robusta.

## 🚀 Tecnologias Utilizadas

### Core Framework
- **NestJS** - Framework progressivo para construir aplicações Node.js eficientes e escaláveis
- **TypeScript** - Linguagem tipada que compila para JavaScript

### Banco de Dados
- **SQLite3** - Banco de dados relacional embutido e leve
- **TypeORM** - ORM (Object-Relational Mapping) para TypeScript e JavaScript
- **@nestjs/typeorm** - Integração oficial do TypeORM com NestJS

### Validação e Transformação de Dados
- **class-validator** - Validação declarativa baseada em decoradores para classes
- **class-transformer** - Transformação de objetos com suporte a tipos complexos
- **@nestjs/mapped-types** - Tipos utilitários para reduzir duplicação de código DTOs

## 📋 Estrutura do Projeto

```
src/
├── main.ts                           # Ponto de entrada da aplicação
├── app.module.ts                     # Módulo raiz
├── app.controller.ts                 # Controlador da aplicação
├── app.service.ts                    # Serviço da aplicação
└── developers/                       # Módulo de Developers (gerado com nest g resource)
    ├── developers.module.ts          # Módulo de developers
    ├── developers.controller.ts      # Controlador REST
    ├── developers.service.ts         # Lógica de negócio
    ├── dto/                          # Data Transfer Objects
    │   ├── create-developer.dto.ts   # DTO para criação
    │   └── update-developer.dto.ts   # DTO para atualização
    └── entities/
        └── developer.entity.ts       # Entidade TypeORM
```

## 🔧 Instalação

### Pré-requisitos
- Node.js 18.x ou superior
- npm ou yarn

### Passos de Instalação

1. **Clone o repositório ou extraia o projeto**
```bash
cd /home/flavio/Projetos/nestjs-project-backend
```

2. **Instale as dependências**
```bash
npm install
```

## 🏃 Como Executar

### Desenvolvimento
```bash
npm run start:dev
```
A aplicação será iniciada em modo watch, recarregando automaticamente ao detectar mudanças.

### Produção
```bash
npm run build
npm run start:prod
```

### Debug
```bash
npm run start:debug
```

## 📚 Módulo Developers

O módulo `developers` foi criado utilizando o comando CLI do NestJS:

```bash
nest g resource developers
```

Este comando gerou automaticamente:
- **Controller** - Endpoints REST para operações CRUD
- **Service** - Lógica de negócio
- **Module** - Configuração do módulo
- **Entity** - Modelo de dados com TypeORM
- **DTOs** - Objetos de transferência de dados

### Rotas Disponíveis

| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/developers` | Criar um novo developer |
| GET | `/developers` | Listar todos os developers |
| GET | `/developers/:id` | Obter um developer específico |
| PATCH | `/developers/:id` | Atualizar um developer |
| DELETE | `/developers/:id` | Deletar um developer |

## 🗄️ Banco de Dados

### Configuração SQLite3

O banco de dados é configurado no `app.module.ts` com as seguintes configurações:

```typescript
TypeOrmModule.forRoot({
  type: 'sqlite',
  database: 'db.sqlite',
  entities: [__dirname + '/**/*.entity{.ts,.js}'],
  synchronize: true
})
```

- **type**: Tipo de banco de dados (SQLite)
- **database**: Arquivo de banco de dados (`db.sqlite`)
- **synchronize**: Sincronização automática de esquema (ideal para desenvolvimento)

### Entidade Developer

A entidade `Developer` utiliza **TypeORM** com decoradores para definição de colunas:

```typescript
@Entity('developers')
export class Developer {
  @PrimaryColumn()
  id: string;

  @Column()
  name: string;

  @Column()
  email: string;

  @Column()
  dateOfBirth: string;

  @BeforeInsert()
  generateId() {
    this.id = `dev_${nanoid()}`;
  }
}
```

## ✔️ Validação de Dados

O projeto utiliza **class-validator** e **class-transformer** para validação robusta de dados nos DTOs.

### Exemplo de DTO com Validação

```typescript
import { IsString, IsEmail, IsDateString } from 'class-validator';

export class CreateDeveloperDto {
  @IsString()
  name: string;

  @IsEmail()
  email: string;

  @IsDateString()
  dateOfBirth: string;
}
```

Recursos:
- **Validação automática** em controllers via ValidationPipe
- **Transformação de tipos** com class-transformer
- **Mensagens de erro personalizadas**
- **Regras de validação customizadas**

## 🧪 Testes

```bash
# Testes unitários
npm run test

# Testes com cobertura
npm run test:cov

# Testes em modo watch
npm run test:watch

# Testes e2e
npm run test:e2e
```

## 🎯 Lint e Formatação

```bash
# Executar ESLint com auto-fix
npm run lint

# Formatar código com Prettier
npm run format
```

## 📖 Recursos Adicionais

- [NestJS Documentation](https://docs.nestjs.com)
- [TypeORM Documentation](https://typeorm.io)
- [class-validator](https://github.com/typestack/class-validator)
- [class-transformer](https://github.com/typestack/class-transformer)

## 📝 Licença

UNLICENSED
