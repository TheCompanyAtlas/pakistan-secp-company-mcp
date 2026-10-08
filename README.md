# Pakistan SECP Company Registry MCP

Connect your AI assistant to about 150,000 companies registered with the Securities and Exchange Commission of Pakistan (SECP) through [The Company Atlas](https://thecompanyatlas.com) and the Model Context Protocol.

Use it to confirm that a Pakistani counterparty is a registered company, what kind of company it is, and when and where it was incorporated.

- Search by company name, CUIN, company type, SECP registration office and incorporation date
- Every record has a name and CUIN, and all but one an incorporation date; about 22% also have the date of the last annual return
- Address, status, capital, directors and shareholders are not included

The MCP connection is provided by The Company Atlas. This repository does not run a separate server.

## Connect

```text
https://thecompanyatlas.com/mcp/pakistan
```

Add this URL as a custom MCP connector in Claude, Cursor, or another MCP-compatible client. Sign in with Google when prompted.

- Transport: Streamable HTTP
- Auth: Google OAuth
- Docs: [thecompanyatlas.com/tools/pakistan-secp-companies](https://thecompanyatlas.com/tools/pakistan-secp-companies)

## Tools

### `Pakistan_search_companies`

Search SECP-registered companies. Filters are combined with AND logic; include at least one.

| Parameter | Type | Description |
|---|---|---|
| `q` | string, optional | Company name substring, 3–160 characters |
| `entityType` | enum, optional | `Private Limited`, `Single Member Company`, `Limited Liability Partnership` or `Limited by Guarantee` |
| `registrationOffice` | enum, optional | SECP Company Registration Office: `Islamabad`, `Lahore`, `Karachi`, `Peshawar`, `Multan`, `Faisalabad`, `Gilgit`, `Quetta` or `Sukkur` |
| `incorporatedFrom` / `incorporatedTo` | date, optional | Incorporation date range, `YYYY-MM-DD` |
| `page` / `limit` | integer, optional | Pagination, `limit` up to 50 (default 20) |

Returns `{ data, total, page, limit }`. `id` is `PK` + the 7-digit Corporate Unique Identification Number (CUIN).

### `Pakistan_get_company`

One company by CUIN (e.g. `0070670` or `70670`, with or without the `PK` prefix).

| Parameter | Type | Description |
|---|---|---|
| `cuin` | string | SECP Corporate Unique Identification Number |

## Example prompts

- *"Single member companies registered in Peshawar in 2024."*
- *"Pakistani companies with Textile in the name."*
- *"Look up Pakistani company CUIN 0070670."*
