# Rateio de Custos — Ability

Site de rateio de custos por centro de custo, integrado ao Firebase Firestore.

## Como subir na Vercel

### Opção 1 — Pelo site da Vercel (mais fácil)
1. Acesse https://vercel.com e faça login
2. Clique em **Add New → Project**
3. Escolha **"Deploy from a folder"** ou suba via GitHub
4. Arraste a pasta `rateio-vercel` ou conecte o repositório
5. Clique em **Deploy** — pronto!

### Opção 2 — Via GitHub (recomendado para atualizações fáceis)
1. Crie um repositório no GitHub (pode ser privado)
2. Faça upload desta pasta para o repositório
3. Na Vercel, importe o repositório
4. Toda vez que atualizar o GitHub, a Vercel atualiza automaticamente

### Opção 3 — Via CLI
```bash
npm i -g vercel
cd rateio-vercel
vercel --prod
```

## Firebase — configurar regras do Firestore

No console do Firebase (https://console.firebase.google.com):
1. Acesse **Firestore Database → Regras**
2. Cole as regras abaixo e publique:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /rateios/{rateioId} {
      allow read, write: if true; // sem login por enquanto
    }
    match /configs/{configId} {
      allow read, write: if true;
    }
  }
}
```

> Quando quiser adicionar login, troque `if true` por `if request.auth != null`

## Estrutura do projeto

```
rateio-vercel/
├── index.html     → site completo (HTML + CSS + JS)
├── vercel.json    → configuração da Vercel
└── README.md      → este arquivo
```

## Funcionalidades

- 📂 **Upload** — carrega planilha .xlsx de colaboradores e calcula rateio
- 🎛️ **Gerenciar Rateio** — seleciona centros, ajusta %, verificações automáticas
- ⚖️ **Rateio Proporcional** — distribui múltiplos itens de custo proporcionalmente
- 🔍 **Buscar Colaborador** — encontra qualquer colaborador e mostra seu centro de custo
- ✏️ **Entrada Manual** — sem planilha, digita centros e quantidades direto
- 📅 **Histórico** — salva rateios no Firebase, reabrir e exportar depois
- 📥 **Modelo Ability** — exporta no formato exato do RATEIO_MAST.xlsx
