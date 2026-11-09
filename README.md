# Inbox helper (TypeScript)

An agent with its own email address. When an email arrives it reads it and either answers or hands it to you.

- If your instructions cover the question, it replies.
- If they do not, or it is unsure, it leaves the email for you and tells you why.
- Until you write its instructions in `instructions.md`, it hands every email to you and uses no AI credits.

What it does without asking depends on the agent's level. It starts on "Ask every time", so each reply waits for your approval. Raise the level in the agent's settings once you trust its answers.

## What is in here

- `instructions.md`: what the helper knows. It is empty. Write in it who you are, what you sell or do, and the questions it may answer, in plain words. The helper answers only from this file.
- `src/agent.ts`: the handler.
- `stackshift.yaml`: how StackShift runs it: it wakes on inbox mail, it may use the model `claude-sonnet-5-5`, it may send mail from its own inbox, and it has a monthly AI budget.
- `Dockerfile`: how StackShift builds and runs it. It installs the packages, compiles the TypeScript and starts `node dist/agent.js`. StackShift needs a Dockerfile in the agent's folder, so keep it when you change the agent.

Email that people send it is untrusted. The helper never follows orders written in an email, and StackShift asks you before anything built from an email's words goes out.

## Run it on StackShift

From the dashboard, open Agents and choose New agent. Or from your terminal:

```bash
stackshift agents create --name "Inbox helper" --template inbox-helper --language typescript --platform mail.agent_inbox.send
```

Write your instructions in `instructions.md`, push, and deploy again. Then email the agent's address.
