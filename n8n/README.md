# RetailGuard n8n demo

RetailGuard extends the repository's retail support theme with an account-safety assistant. The workflow uses n8n's Chat Trigger, AI Agent, local Ollama chat model, Simple Memory, and a Code Tool for explainable risk triage. The Code Tool performs keyword-based guidance only; it does not access customer accounts, verify charges, or perform an actual escalation.

## Run locally

1. Install [n8n](https://docs.n8n.io/hosting/installation/npm/) or [Docker](https://docs.n8n.io/hosting/installation/docker/) and [Ollama](https://docs.ollama.com/quickstart). Run `ollama pull qwen3:4b-instruct` and start Ollama.
2. Start n8n (`n8n start`) and open `http://localhost:5678`. For Docker, use `docker run -d --name retailguard-n8n -p 5678:5678 -v retailguard-n8n:/home/node/.n8n n8nio/n8n:2.47.3`; create the volume first with `docker volume create retailguard-n8n`.
3. Import `n8n/retail-guard-agent.json` from the workflow editor.
4. In **Ollama Chat Model**, create/select an Ollama credential with base URL `http://127.0.0.1:11434` when n8n runs on the same host, or `http://host.docker.internal:11434` when n8n runs in Docker Desktop. Confirm the selected model exists in Ollama.
5. Save the workflow and use **Open chat** or the Chat Trigger's test URL. Leave it unpublished for a local demo.

No API keys are stored in this repository. n8n credentials stay in the local n8n instance.

## Example tests

1. `Someone used my card without my permission. What should I do?` Expected: security concern, verified bank and retailer contact, no request for card details.
2. `My order has not arrived and the refund is overdue.` Expected: staff review and practical delivery/refund steps, no invented order status.
3. `The shoes fit well. Can you help me choose a size for another pair?` Expected: routine shopping guidance without claiming access to inventory.

For the later case-study report, capture the full n8n canvas, each node setting, the system prompt, the three chat runs, and the execution log. Hide credential values and personal data in screenshots.
