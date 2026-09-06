# DK XChat v0 setup

Two lanes. Do not merge them onto one token.

- Lane A (public): your posting handle, hand-typed `@grok` summon.
- Lane B (private): project Chat bot, open DMs, Grok consult prompt.

Public summon snippets: `docs/xchat/reply-snippets.md`
Private prompt: `docs/xchat/system-prompt.md`
Hosted lens: https://source.digitalknowledge.net/public/ask-grok.html

---

## 0. What you will hold when this works

| Item | Where it comes from |
|---|---|
| App Bearer Token | Developer Console app |
| Bot handle + numeric user id | `POST /2/bots` response |
| Bot token `xcbot_…` | Same response (shown once) |
| Chat key blob + signing version | Chat XDK export after register |
| xAI key `xai-…` | console.x.ai API Keys |

Default project cap is **1 bot**. Check `meta.max_bots` on list.

---

## 1. Developer account and credits

1. Open https://console.x.com and sign in as `@7SwanSwimming` (or the account that will own the app).
2. Accept the Developer Agreement if prompted: https://docs.x.com/x-api/getting-started/getting-access
3. Create or open a Project, then **New App**. Type: **Automated App / Bot**. Guide: https://docs.x.com/fundamentals/developer-apps
4. Billing → Credits. Buy a small pack. Turn **auto-recharge off** or set a low cap. Pricing: https://docs.x.com/x-api/getting-started/pricing
5. Copy the **App Bearer Token**. This is *not* the bot token.

Use case text if asked: private encrypted consult bot for Digital Knowledge / American System operator briefs. Public replies stay on the human handle.

---

## 2. Create the bot-tied account (API, not a password login)

Official bots have **no password and no login**. The only way to act as the bot is its `xcbot_` token. It gets an **Automated by @owner** label pointing at the app owner.
Docs: https://docs.x.com/xchat/bots
Create: https://docs.x.com/x-api/bots/create-a-bot

```bash
curl --request POST \
  --url https://api.x.com/2/bots \
  --header "Authorization: Bearer APP_BEARER_TOKEN" \
  --header "Content-Type: application/json" \
  --data '{
    "handle": "DKconsult",
    "display_name": "DK Consult"
  }'
```

Handle rules: 5–15 chars, letters/digits/underscore. Pick before you run this.

Save from the 201 body:
- `data.id` → `CHAT_BOT_USER_ID`
- `data.username` → the live @handle
- `data.token` → `xcbot_…` (once only)
- `data.scopes` should include `dm.read`, `dm.write`, `tweet.read`, `users.read`, `media.write`

Repeating create on the same handle **revokes the old token** and mints a new one.

List bots:

```bash
curl --url https://api.x.com/2/bots \
  --header "Authorization: Bearer APP_BEARER_TOKEN"
```

---

## 3. Open DMs and lock identity

https://docs.x.com/x-api/bots/update-a-bot (PUT `/2/bots/:id`)

```bash
curl --request PUT \
  --url https://api.x.com/2/bots/BOT_NUMERIC_ID \
  --header "Authorization: Bearer APP_BEARER_TOKEN" \
  --header "Content-Type: application/json" \
  --data '{
    "display_name": "DK Consult",
    "dm_permission": "everyone"
  }'
```

`dm_permission`: `everyone` | `premium` | `no_one`

v0 = `everyone` so a non-follower can request a consult.

If you later need a human-login alt account instead of a project bot, the old automation label path is Settings → Your account → Automation → Managing account. Official project bots already carry Automated by @owner.

---

## 4. Chat encryption keys (bot path)

https://docs.x.com/xchat/getting-started
https://docs.x.com/xchat/handling-private-keys

Bots should use an `export_keys` blob, not a Juicebox PIN.

1. Install Chat XDK: `pip install chatxdk` (Python 3.10+). Announce: https://devcommunity.x.com/t/announcement-x-chat-api-and-xdks-are-now-available/271994
2. `generate_keypairs` → register public keys on the bot user → `export_keys` → store blob in a secret manager.
3. Set `CHAT_PRIVATE_KEYS_B64` and `CHAT_SIGNING_KEY_VERSION` (the registered `public_key_version`).
4. Never commit the blob. Never log it.

The official skeleton expects this blob already minted. There is no first-time key wizard in that repo.

---

## 5. xAI key (separate bill from X Premium and from X API credits)

1. https://console.x.ai → API Keys → Create. Docs: https://docs.x.ai/developers/quickstart
2. Copy `xai-…` once. Put in `XAI_API_KEY`.
3. Set a spend cap on the xAI console too.

---

## 6. Run the skeleton

https://github.com/xdevplatform/xchat-agent-skeleton

```bash
git clone https://github.com/xdevplatform/xchat-agent-skeleton.git
cd xchat-agent-skeleton
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
cp .env.example .env
```

Fill `.env`:

| Variable | Value |
|---|---|
| `X_ACCESS_TOKEN` | Bot `xcbot_…` token (user-context for the bot) |
| `X_BEARER_TOKEN` | App-only Bearer (activity stream / request inbox) |
| `CHAT_BOT_USER_ID` | Numeric bot id |
| `CHAT_PRIVATE_KEYS_B64` | export_keys blob |
| `CHAT_SIGNING_KEY_VERSION` | registered version |
| `XAI_API_KEY` | `xai-…` |
| `GROK_SYSTEM_PROMPT` | paste `docs/xchat/system-prompt.md` |

`GET /2/chat/conversations` is primary inbox only. Non-followers land in Message requests. `X_BEARER_TOKEN` is what discovers those via the activity stream.

```bash
python -m xchat_bot.main
```

Keep it running.

---

## 7. Verify before any public CTA

1. Open `https://x.com/THE_BOT_HANDLE`. Confirm display name and Automated by @owner.
2. From a **second account that does not follow the bot**, send a Chat message.
3. Confirm the process decrypts, replies in the American System brief voice, and ends with the consult close + `STATUS:` line.
4. From the owner account, send “consult” and confirm you can take the thread as a human.
5. Only then swap `@botTiedAcct` in `docs/xchat/reply-snippets.md` and start hand-posted `@grok` summons.

Promo (limited time): Chat up to 500 msgs/day on pay-per-use. https://docs.x.com/xchat/introduction

---

## Do not do in v0

- Rebuild listen/firehose
- API-post summons that contain URLs ($0.20 class on PPU)
- Use the Chat bot handle for public thought-leadership replies
