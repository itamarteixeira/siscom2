# 🚀 INÍCIO RÁPIDO - 5 MINUTOS

## ⚡ Deploy no Railway (Recomendado)

### 1️⃣ Push para GitHub (1 min)

```bash
# Inicializar git (se ainda não fez)
git init
git add .
git commit -m "Initial commit - Sistema de Comissões"

# Criar repositório no GitHub
# https://github.com/new

# Adicionar remote e push
git remote add origin https://github.com/SEU-USUARIO/SEU-REPO.git
git branch -M main
git push -u origin main
```

### 2️⃣ Railway Deploy (2 min)

```bash
1. Acesse https://railway.app
2. Login com GitHub
3. New Project → Deploy from GitHub repo
4. Selecione seu repositório
5. Aguarde deploy (1-2 min)
```

### 3️⃣ Adicionar PostgreSQL (1 min)

```bash
1. No projeto Railway, clique "+ New"
2. Database → PostgreSQL
3. Aguarde provisionar (30 seg)
4. ✅ Pronto! Conecta automaticamente
```

### 4️⃣ Acessar Sistema (1 min)

```bash
1. Railway mostra URL do deploy
2. Clique na URL
3. ✅ Sistema funcionando!
```

---

## 💻 Rodar Localmente (Desenvolvimento)

### 1️⃣ Instalar PostgreSQL

**Ubuntu/Debian:**
```bash
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib
```

**macOS:**
```bash
brew install postgresql
brew services start postgresql
```

**Windows:**
- Baixar de https://www.postgresql.org/download/windows/

### 2️⃣ Criar Banco

```bash
# Criar banco
createdb commission_db

# Ou via psql
psql postgres
CREATE DATABASE commission_db;
\q
```

### 3️⃣ Configurar Variável

```bash
# Linux/Mac
export DATABASE_URL="postgresql://localhost:5432/commission_db"

# Windows (PowerShell)
$env:DATABASE_URL="postgresql://localhost:5432/commission_db"

# Ou criar arquivo .env
echo 'DATABASE_URL=postgresql://localhost:5432/commission_db' > .env
```

### 4️⃣ Instalar e Rodar

```bash
# Instalar dependências
npm install

# Iniciar servidor
npm start

# Acessar
http://localhost:3000
```

---

## ✅ Testar Sistema

### 1. Importar Nota de Exemplo

```bash
1. Acesse o sistema
2. Clique em "Importar"
3. Selecione "XML"
4. Escolha o arquivo "exemplo-nfe.xml"
5. Veja o preview:
   - Número: 000123
   - Emitente: EMPRESA EXEMPLO LTDA
   - Cliente: CLIENTE EXEMPLO
   - Valor: R$ 5.000,00
   - 2 duplicatas
6. Configure comissão: 5%
7. Clique "Importar"
8. ✅ 2 títulos criados (R$ 125,00 cada)
```

### 2. Usar Filtros

```bash
1. Vá em "Títulos de Comissão"
2. Digite "EMPRESA" na busca
3. Clique "Filtrar"
4. ✅ Mostra apenas títulos da EMPRESA EXEMPLO
```

### 3. Criar Pedido

```bash
1. Selecione os 2 títulos (checkbox)
2. Clique "Criar Pedido com Selecionados"
3. Veja resumo: R$ 250,00
4. Confirme
5. ✅ Pedido criado!
```

---

## 🔧 Verificar Instalação

### Logs do Servidor

Ao iniciar, você deve ver:

```
✅ PostgreSQL conectado com sucesso!
📦 Criando tabelas PostgreSQL...
✅ Tabelas PostgreSQL criadas com sucesso!
🚀 Servidor rodando na porta 3000
```

### Testar Rotas

```bash
# Dashboard
curl http://localhost:3000/api/dashboard

# Deve retornar JSON:
{
  "notasFiscais": { "total": 0, "valor": 0 },
  "titulosComissao": { "total": 0, "valor": 0, "pendentes": 0 },
  "pedidos": { "total": 0, "valor": 0 }
}
```

---

## 🐛 Problemas Comuns

### Erro: "DATABASE_URL não definido"

```bash
# Configurar variável
export DATABASE_URL="postgresql://localhost:5432/commission_db"

# Ou criar .env
echo 'DATABASE_URL=postgresql://localhost:5432/commission_db' > .env
```

### Erro: "Cannot find module 'pg'"

```bash
# Reinstalar dependências
rm -rf node_modules
npm install
```

### Erro: "Porta 3000 já em uso"

```bash
# Alterar porta
PORT=3001 npm start

# Ou matar processo na porta 3000
lsof -ti:3000 | xargs kill
```

### PostgreSQL não conecta

```bash
# Verificar se está rodando
sudo service postgresql status  # Linux
brew services list             # macOS

# Iniciar se necessário
sudo service postgresql start   # Linux
brew services start postgresql  # macOS
```

---

## 📊 Próximos Passos

1. ✅ Importar suas notas fiscais reais
2. ✅ Configurar percentual de comissão
3. ✅ Criar pedidos
4. ✅ Exportar relatórios (futuro)

---

## 💡 Dicas

### Railway (Produção)
- ✅ Deploy automático a cada push
- ✅ PostgreSQL com backup automático
- ✅ SSL/HTTPS gratuito
- ✅ Logs em tempo real
- ✅ Escalável

### Local (Desenvolvimento)
- ✅ Desenvolvimento rápido
- ✅ Debug fácil
- ✅ Sem custo
- ⚠️ Backup manual

---

## 🎯 Está Pronto!

**Sistema funcionando em 5 minutos!** 🚀

Qualquer dúvida:
1. Ver logs do Railway/Console
2. Consultar README.md
3. Abrir issue no GitHub

**Bom uso!** ✨
