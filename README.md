<p align="center"><img src="assets/logo.png" width="96" height="96" alt="EnKonto"></p>

# EnKonto MCP server

Create, issue and send invoices, proformas and e-invoices for European companies from your AI assistant, with confirmation before every send.

[EnKonto](https://enkonto.com) is an invoicing app for small companies and freelancers in Europe. Its remote MCP server lets an AI app work with your companies, customers, invoices and proformas after you sign in with your EnKonto account.

- **Server:** `https://app.enkonto.com/mcp` (Streamable HTTP)
- **Sign-in:** OAuth 2.1 with PKCE; you choose read, edit and issue access on the consent screen
- **MCP Registry:** `com.enkonto/enkonto`
- **Guide:** https://enkonto.com/en/guides/ai-apps-mcp

This repository holds only the connection manifests; the server itself is hosted by EnKonto.

## What it can do

- Read companies, customers, invoices and proformas, with totals and payment status.
- Create and edit drafts: items, VAT, customer, bank account, payment QR codes, visible fields.
- Create and update customers and bank accounts.
- Convert proformas to invoices, copy documents, mark invoices as paid.
- Check a document against the e-invoice rules of its country before issuing.
- Issue invoices, send them by e-mail, send them to Poland's KSeF, cancel invoices and delete drafts — each only after a summary that you confirm.

E-invoicing: XRechnung 3.0 and ZUGFeRD (Germany), KSeF FA(3) with status and UPO (Poland), e-SLOG 2.0 and UPN QR (Slovenia), Peppol BIS 3.0 XML (Belgium / EU).

## Install

You need an EnKonto account: sign up at https://enkonto.com.

### Gemini CLI

```bash
gemini extensions install https://github.com/EnKonto/enkonto-mcp
```

On the first call Gemini CLI opens the browser to sign in to EnKonto. Step by step: https://enkonto.com/en/guides/ai-apps-mcp#gemini-cli

### Cursor

[Add to Cursor](https://cursor.com/install-mcp?name=enkonto&config=eyJ1cmwiOiJodHRwczovL2FwcC5lbmtvbnRvLmNvbS9tY3AifQ==), or install the EnKonto plugin from the Cursor Marketplace once it is listed. The plugin adds the server and the `enkonto-invoicing` skill; Cursor opens the EnKonto sign-in page when it connects. Step by step: https://enkonto.com/en/guides/ai-apps-mcp#cursor

### Google Antigravity

Install the plugin from this repository (or from the Antigravity Marketplace once it is listed):

```bash
agy plugin install https://github.com/EnKonto/enkonto-mcp
```

The plugin adds the server and the `enkonto-invoicing` skill; Antigravity opens the EnKonto sign-in page in the browser when the server connects. Step by step: https://enkonto.com/en/guides/ai-apps-mcp#google-antigravity

### Other MCP clients

Add a remote MCP server with the URL `https://app.enkonto.com/mcp`, for example:

```json
{
  "mcpServers": {
    "enkonto": {
      "url": "https://app.enkonto.com/mcp"
    }
  }
}
```

The client opens the EnKonto sign-in page when it connects. Step-by-step instructions for each app: https://enkonto.com/en/guides/ai-apps-mcp

## Security and privacy

- The AI app sees only the companies of the signed-in user, within that user's role in each company.
- Issuing, e-mailing, sending to KSeF, cancelling and deleting run only after you confirm a summary.
- Your profile in EnKonto lists the connected AI apps and their recent changes; you can disconnect an app at any time.

[Privacy Policy](https://enkonto.com/privacy) · [Terms of Service](https://enkonto.com/terms)

## Support

Open an issue in this repository, or see https://enkonto.com/en/guides/ai-apps-mcp.
