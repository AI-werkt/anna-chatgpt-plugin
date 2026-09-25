# ANNA! — ChatGPT-plugin

Praat vanuit ChatGPT met je **ANNA!**-vergaderarchief: vind opnames, lees notulen,
transcripten en samenvattingen, haal actiepunten op en maak overkoepelende
overzichten — allemaal binnen je eigen organisatie.

Dit is een [portable ChatGPT-plugin](https://developers.openai.com/plugins/build/plugins):
een `mcp.json` die naar de live Anna-MCP-server wijst, plus `skills/` die ChatGPT
sturen in hoe die de tools inzet.

## Inhoud
```
plugin.json                 # manifest (naam, versie, auteur)
mcp.json                    # verwijst naar https://mcp.aifundament.nl/mcp (OAuth 2.1)
skills/
  notulen-opzoeken/SKILL.md # opnames vinden + notulen/transcript/acties lezen
  overzicht-en-acties/SKILL.md # overkoepelende samenvattingen + actiepunten
assets/icon.png             # 512×512 app-icoon
```

De MCP-server (`mcp.aifundament.nl`) authenticeert met **OAuth 2.1 (PKCE)** en is
**per gebruiker op `org_id` gescoped** — je ziet alleen de meetings van je eigen
organisatie. Read-only tools vallen onder scope `meetings.read`; `generate_notulen`
en `summarize_meetings` onder `meetings.generate`.

## Zelf testen (Developer mode)
1. ChatGPT → **Settings → Connectors → Advanced → Developer mode** aanzetten.
2. **Add custom connector** → URL `https://mcp.aifundament.nl/mcp`, auth = OAuth →
   inloggen met je ANNA!-account.
3. Nieuwe chat (of **Work**-tab) → typ `@`, kies de connector → vraag bijv.
   *"Welke meetings had ik vorige week?"* of *"Vat het overleg over ISO 27001 samen."*

## Publiceren in de ChatGPT-directory
Indienen via het OpenAI **plugin-submission**-portaal ("With MCP"): productie-`/mcp`-URL,
tool-scan, **domeinverificatie**, CSP-domeinen, **reviewer-inloggegevens** (een testaccount
met wat voorbeeld-meetings), **5 positieve + 3 negatieve testcases**, en
**identiteitsverificatie** (zakelijk) — daarna volgt OpenAI-review.

Zie: <https://developers.openai.com/plugins/build/plugins> en de
[submission-richtlijnen](https://developers.openai.com/apps-sdk/app-submission-guidelines).
