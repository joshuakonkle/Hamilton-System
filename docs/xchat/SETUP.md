# DK XChat v0 setup

Two lanes. Do not merge them onto one token.

- Lane A (public): your posting handle, hand-typed `@grok` summon. Summon is **lens only** — no `@AmSysConsult` in the tweet. Close lives in the HTML.
- Lane B (private): project Chat bot, encrypted Chat, Grok consult prompt.

Live Lane B: `@AmSysConsult` (id `2096714716408098818`), Automated by `@7SwanSwimming`, display **Digital Knowledge | American System**, `dm_permission=everyone`.

Public summon snippets: `docs/xchat/reply-snippets.md` (lens URL or mini-prompt; no bot handle)
Private prompt: `docs/xchat/system-prompt.md` (no handle — close is the word consult inside Chat)
Hosted lens: https://source.digitalknowledge.net/docs/public/ask-grok.html

Runtime after 6 Sep smoke: Jenny. Do not Rotate / Revoke / Delete the bot from this desk.

---

## 0. What you will hold when this works

| Item | Where it comes from |
|---|---|
| App Bearer Token | Developer Console app |
| Bot handle + numeric user id | Console card / create response |
| Bot token `xcbot_…` | Shown once |
| Chat key blob + signing version | Chat XDK export after Juicebox or register |
| xAI key `xai-…` | console.x.ai API Keys |

Default project cap is **1 bot**. This project is at 1/1.

---

## 1–6. Already done on 6 Sep

Console create (not the curl 201 path). Keys via console Register + Juicebox PIN, then `export_keys` blob on Joshua Windows PC (`CHAT_SIGNING_KEY_VERSION=1788731061388`). Skeleton cloned at `C:\Users\joshu\Documents\xchat-agent-skeleton`. Use `.venv\Scripts\python.exe`.

Create-again curl is retired. Repeating `POST /2/bots` on this handle **revokes the token**.

---

## 7. Verify before any public CTA of the bot handle

Lane A `@grok` + HTML lens is in use (CEO smoke 7 Sep, low-engagement posts). That is not a public blast of `@AmSysConsult`.

Still do not Evangelist-blast the handle until Joshua greens productize:

1. Profile `https://x.com/AmSysConsult` shows Automated by @7SwanSwimming.
2. A **second account that does not follow the bot** sends an **encrypted** Chat (not the Unencrypted read-only stub).
3. Process decrypts, replies in the brief voice, ends with consult close + `STATUS:` line **in the sender's thread**.
4. Owner can pick up a thread when the sender says `consult`.

Owner→own-bot compose on web is broken (Unencrypted / read-only). Do not treat that pane as a fail of the bot.

Promo (limited time): Chat up to 500 msgs/day on pay-per-use. https://docs.x.com/xchat/introduction

---

## Do not do in v0

- Rebuild listen/firehose
- API-post summons that contain URLs ($0.20 class on PPU)
- Use `@AmSysConsult` for public thought-leadership replies
- Put `@AmSysConsult` in the Lane A `@grok` summon (HTML already closes)
- Create bot / Rotate token / Register chat keys again without Jenny
