# DK XChat v0 setup

Two lanes. Do not merge them onto one token.

## Lane A: public summon (hand-posted)
Account: your personal posting handle.
Method: X app or web. Not the X API for v0.
Reply under a live post:

```
@grok Use the American System (American School / Hamiltonian) as the lens on this post. Productive capacity, sovereignty, and domestic skill over labor arbitrage. Short brief: producer, constraint, next move. Then remind people they can DM @botTiedAcct for a private consult.
```

Optional longer summon if the mini-prompt is thin:

```
@grok Follow https://source.digitalknowledge.net/public/ask-grok.html
Then DM @botTiedAcct for a private working session.
```

Cost: hand-posted replies do not spend X Developer API credits. Premium is unrelated.

## Lane B: private consult (X Chat bot)
1. Create a project bot in the X Developer Console. Open DMs (`dm_permission=everyone`).
2. Fork or clone https://github.com/xdevplatform/xchat-agent-skeleton
3. Put `docs/xchat/system-prompt.md` into `GROK_SYSTEM_PROMPT`.
4. Fill `.env`: X bot token, Chat keys, `XAI_API_KEY`.
5. Run the process. Test a DM from an account that does **not** follow the bot.
6. Human picks up threads tagged `STATUS: consult-requested` or `qualified`.

X Chat promo (limited time): up to 500 msgs/day on pay-per-use. xAI token usage is a separate bill.

## Do not do in v0
- Rebuild listen/firehose
- API-post summons that contain URLs ($0.20 class on PPU)
- Use the Chat bot handle for public thought-leadership replies
