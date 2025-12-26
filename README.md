# 💼 Sistema de Gestão de Comissões

Sistema completo para importação de NF-e (XML/PDF), cálculo de comissões e geração de pedidos.

## 🚀 Funcionalidades

### ✅ Importação de Notas Fiscais
- **XML de NF-e** com preview antes de salvar
- **PDF de NF-e** com extração automática e preview
- Detecção automática de duplicatas
- Criação de duplicata padrão (30 dias) se nota não tiver

### 📊 Gestão de Títulos de Comissão
- Cálculo automático por percentual configurável
- Filtros avançados:
  - Busca por texto (nota/emitente/destinatário)
  - Filtro por status (pendente/em pedido)
  - Filtro por pagamento (pendente/pago/atrasado/cancelado)
  - Filtro por período de vencimento
- Seleção múltipla de títulos
- Edição de valores e status

### 📦 Pedidos de Comissão
- Criação de pedidos agrupando múltiplos títulos
- Visualização detalhada de cada pedido
- Controle de status

### 📈 Dashboard
- Visão geral de notas fiscais importadas
- Total de títulos de comissão
- Títulos pendentes
- Pedidos criados

## 🛠️ Tecnologias

### Backend
- **Node.js** + Express
- **PostgreSQL** (banco de dados persistente)
- **Multer** (upload de arquivos)
- **xml2js** (parse de XML)
- **pdf-parse** (extração de PDF)

### Frontend
- **HTML5** + **CSS3** + **JavaScript Vanilla**
- Design responsivo
- Interface moderna e intuitiva

## 📦 Instalação

### 1. Clonar repositório
```bash
git clone <seu-repositorio>
cd commission-system
```

### 2. Instalar dependências
```bash
npm install
```

### 3. Configurar PostgreSQL

#### Opção A: Railway (Recomendado)
1. Criar conta no [Railway](https://railway.app)
2. Criar novo projeto
3. Adicionar PostgreSQL Database
4. Railway cria automaticamente `DATABASE_URL`
5. Fazer deploy (conecta automaticamente)

#### Opção B: Local
```bash
# Instalar PostgreSQL
# Ubuntu/Debian
sudo apt-get install postgresql

# macOS
brew install postgresql

# Criar banco
createdb commission_db

# Configurar variável de ambiente
export DATABASE_URL="postgresql://user:password@localhost:5432/commission_db"
```

### 4. Iniciar servidor
```bash
npm start
```

Servidor rodará em `http://localhost:3000`

## 🚀 Deploy no Railway

### Passo a Passo:

1. **Criar conta no Railway**
   - Acesse https://railway.app
   - Faça login com GitHub

2. **Criar novo projeto**
   - New Project → Deploy from GitHub repo
   - Selecione seu repositório

3. **Adicionar PostgreSQL**
   - + New → Database → PostgreSQL
   - Railway conecta automaticamente

4. **Deploy automático**
   - Railway detecta `package.json`
   - Instala dependências
   - Roda `npm start`
   - ✅ Pronto!

### Variáveis de Ambiente (Railway)

Railway cria automaticamente:
```
DATABASE_URL=postgresql://...
PORT=3000
```

**Não precisa configurar nada!** 🎉

## 📁 Estrutura do Projeto

```
commission-system/
├── server.js              # Servidor Node.js + PostgreSQL
├── package.json           # Dependências
├── public/
│   └── index.html        # Frontend completo
├── uploads/              # Arquivos temporários (gitignored)
├── .gitignore
└── README.md
```

## 🗄️ Banco de Dados

### Tabelas

#### notas_fiscais
- Armazena informações das NF-e importadas
- Campos: número, série, emitente, destinatário, valor, etc.

#### duplicatas
- Duplicatas das notas fiscais
- Referência: `nota_fiscal_id`

#### titulos_comissao
- Títulos de comissão calculados
- Referências: `duplicata_id`, `nota_fiscal_id`

#### pedidos
- Pedidos agrupando múltiplos títulos
- Controle de valor total e quantidade

### Migrations

As tabelas são criadas automaticamente na primeira execução:
```javascript
// server.js executa initDatabase() no startup
// Cria todas as tabelas se não existirem
```

## 🔧 Desenvolvimento

### Logs
```bash
# Ver logs no Railway
Railway Dashboard → Deployments → View Logs

# Logs locais
npm start
# Logs aparecem no console
```

### Debug
```javascript
// server.js tem logs detalhados
console.log('=== INÍCIO EXTRAÇÃO PDF ===');
console.log('Dados extraídos:', resultado);
```

## 📊 Uso

### 1. Importar Nota Fiscal

**XML:**
1. Clique em "Importar"
2. Selecione "XML"
3. Escolha arquivo .xml
4. Veja preview dos dados
5. Configure % comissão
6. Clique "Importar"

**PDF:**
1. Clique em "Importar"
2. Selecione "PDF"
3. Escolha arquivo .pdf
4. Sistema extrai dados automaticamente
5. Veja preview
6. Configure % comissão
7. Clique "Importar"

### 2. Filtrar Títulos

**Filtros disponíveis:**
- 🔍 Busca por texto
- 📊 Status (pendente/em pedido)
- 💳 Pagamento (pendente/pago/atrasado)
- 📅 Vencimento (vencidos/hoje/7 dias/30 dias)

### 3. Criar Pedido

1. Selecione títulos (checkbox)
2. Clique "Criar Pedido com Selecionados"
3. Confirme valores
4. ✅ Pedido criado!

## 🔒 Segurança

- ✅ Upload de arquivos validado
- ✅ SQL injection prevenido (queries parametrizadas)
- ✅ Validação de dados no backend
- ✅ SSL/TLS no PostgreSQL (Railway)

## 🐛 Troubleshooting

### Erro: "PostgreSQL não conectado"
```bash
# Verificar DATABASE_URL
echo $DATABASE_URL

# Verificar se PostgreSQL está rodando
# Railway: Ver logs do serviço PostgreSQL
```

### Erro: "Módulo não encontrado"
```bash
# Reinstalar dependências
rm -rf node_modules package-lock.json
npm install
```

### PDF não extrai dados
- Verifique logs: "=== INÍCIO EXTRAÇÃO PDF ==="
- Confira primeiros 500 caracteres extraídos
- PDF pode estar com OCR ruim ou layout diferente

## 📝 Licença

MIT License - Livre para uso pessoal e comercial

## 🤝 Contribuindo

1. Fork o projeto
2. Crie sua feature branch (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Add: nova feature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abra um Pull Request

## 📧 Suporte

Para suporte e dúvidas:
- Abra uma issue no GitHub
- Veja logs detalhados no Railway
- Consulte documentação do Railway

## 🎯 Roadmap

- [ ] Relatórios em PDF
- [ ] Exportação para Excel
- [ ] API REST documentada
- [ ] Autenticação de usuários
- [ ] Multi-empresa
- [ ] Integração contábil

## ✨ Versão

**v2.0.0** - PostgreSQL Edition (26/12/2025)

### Changelog

**v2.0.0** (26/12/2025)
- ✅ Migração completa para PostgreSQL
- ✅ Preview de PDF antes de salvar
- ✅ Filtros avançados na tela de títulos
- ✅ Coluna destinatário adicionada
- ✅ Duplicata padrão com valor total
- ✅ Logs detalhados de extração
- ✅ Dados persistem para sempre

**v1.0.0**
- Versão inicial com SQLite
- Importação XML/PDF básica
- CRUD de títulos e pedidos

---

**Desenvolvido com ❤️ para facilitar gestão de comissões**

🚀 **Deploy em 5 minutos no Railway!**
