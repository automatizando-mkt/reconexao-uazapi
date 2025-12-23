# 📱 Interface de Reconexão WhatsApp (UAZAPI / Evolution v2)

Uma interface **standalone** (arquivo único) para facilitar a reconexão de instâncias do WhatsApp. Desenvolvida para que gestores de tráfego e automação possam enviar um link seguro para seus clientes escanearem o QR Code, sem precisar acessar painéis administrativos complexos.

![Status do Projeto](https://img.shields.io/badge/Status-Funcional-brightgreen)
![Tech](https://img.shields.io/badge/Tech-HTML%20%7C%20JS-blue)

## ✨ Funcionalidades

* 🚀 **Single File:** Apenas um arquivo HTML. Não requer NodeJS, PHP ou servidores complexos.
* 🔒 **Links Seguros:** As credenciais (Token/URL) são codificadas em Base64 na URL, dificultando a leitura visual.
* 🔄 **Auto-Refresh Inteligente:** O QR Code atualiza a cada 30s e o status é verificado a cada 3s.
* 📱 **Responsivo:** Funciona perfeitamente em Celulares e Desktop.
* ✅ **Feedback Visual:** Avisa automaticamente quando o WhatsApp conecta.
* 🛠️ **Compatibilidade:** Otimizado para **UAZAPI (uazapiGO)** e forks da Evolution API v2 que usam `POST /instance/connect`.

## ⚙️ Como Usar

### 1. Gerar o Link (Modo Admin)
1.  Abra o arquivo `index.html` no seu navegador.
2.  Preencha os dados da sua API:
    * **URL:** `https://sua-api.com`
    * **Nome:** Nome visual para o cliente (ex: "Clínica Saúde")
    * **Token:** O token específico da instância (Bearer Token).
3.  Clique em **"Gerar Link"**.
4.  Copie o link gerado e envie para seu cliente.

### 2. Para o Cliente
1.  O cliente abre o link.
2.  Um QR Code aparece na tela.
3.  Ele escaneia com o WhatsApp.
4.  Assim que conectar, a tela fica verde confirmando o sucesso.

## 🚀 Como Hospedar (Grátis)

Você pode hospedar este arquivo em qualquer lugar que suporte HTML estático:

* **Vercel / Netlify / GitHub Pages** (Recomendado - Grátis e com HTTPS)
* Hospedagem cPanel / Hostgator (Gerenciador de Arquivos)
* WordPress (Via FTP na raiz)

## ⚠️ Requisito Importante: CORS

Se você hospedar este arquivo em um domínio diferente da sua API (ex: o site está na Vercel e a API na sua VPS), você **PRECISA** liberar o CORS na sua API.

No arquivo `.env` da sua UAZAPI/Evolution:

```bash
# Permitir qualquer origem (Mais fácil)
CORS_ORIGIN=*

# OU permitir apenas seu domínio (Mais seguro)
CORS_ORIGIN=[https://seu-site-de-reconexao.vercel.app](https://seu-site-de-reconexao.vercel.app),[https://outro-dominio.com](https://outro-dominio.com)
Sem isso, o navegador bloqueará a conexão e o QR Code não aparecerá.


🛠️ Detalhes Técnicos (Para Devs)
O script utiliza a seguinte lógica para compatibilidade com UAZAPI v2:

Endpoint: POST /instance/connect (Payload vazio {})

Auth: Header token (Em vez de apikey)

Polling: Verifica status em GET /instance/status

Desenvolvido por Gabriel Moraes Contribuições são bem-vindas!