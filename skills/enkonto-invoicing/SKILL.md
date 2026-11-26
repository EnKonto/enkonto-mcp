---
name: enkonto-invoicing
description: Work with EnKonto invoices, proformas, customers and e-invoices through the enkonto MCP server. Use when the user asks to create, check, issue, e-mail, send to KSeF, cancel or look up invoices and proformas in EnKonto.
---

# EnKonto

EnKonto is an invoicing app for small companies and freelancers in Europe. The `enkonto` MCP server works with the companies, customers, invoices and proformas of the signed-in EnKonto user, within that user's role in each company.

## Working with EnKonto

- Every tool takes the `company_id` of one company; `list_companies` returns the companies of the user.
- `get_reference_data` returns the allowed values (countries, currencies, VAT categories, units, languages and others) for a company.
- Drafts can be created and changed freely. A draft gets its number only when it is issued.
- `check_invoice` lists what the e-invoice rules of the document's country would flag. These are warnings: the user decides whether to issue anyway.

## Actions that need the user's confirmation

Issuing, e-mailing, sending to KSeF, cancelling, deleting a draft and changing payment details come in pairs: a `prepare_*` tool returns a summary and a one-time token (valid for 10 minutes) and changes nothing; the matching tool performs the action with that token.

Show the user the full summary and wait for an explicit confirmation before calling the action tool. Don't confirm on the user's behalf, and prepare again if the user changes anything or the token expires.

- `prepare_issue_invoice` / `issue_invoice`
- `prepare_email_invoice` / `email_invoice`
- `prepare_send_invoice_to_ksef` / `send_invoice_to_ksef` (Poland; `refresh_ksef_status` returns the final status)
- `prepare_cancel_invoice` / `cancel_invoice`
- `prepare_delete_invoice_draft` / `delete_invoice_draft`
- `prepare_change_payment_details` / `change_payment_details`
- `prepare_set_invoice_bank_account` / `set_invoice_bank_account`

## Countries and formats

- Germany: XRechnung 3.0 and ZUGFeRD.
- Poland: KSeF FA(3), sent to KSeF with status and UPO.
- Slovenia: e-SLOG 2.0 and UPN QR.
- Belgium / EU: Peppol BIS 3.0 XML.
- Other European countries: PDF invoices.

The user is responsible for the content of their documents; EnKonto is an assistant, not a tax adviser.
