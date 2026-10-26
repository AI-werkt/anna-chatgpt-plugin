# ANNA! — ChatGPT-plugin (marketplace)

Praat vanuit ChatGPT met je **ANNA!**-vergaderarchief: vind opnames, lees notulen,
transcripten en samenvattingen, haal actiepunten op en maak overkoepelende
overzichten — allemaal binnen je eigen organisatie.

Deze repo is een **Git-backed plugin-marketplace** voor ChatGPT (Business/Enterprise).
Een workspace-admin koppelt deze repo één keer als marketplace en zet de plugin
daarna per rol op "geïnstalleerd". De plugin wijst naar de live ANNA-MCP-server;
die authenticeert met **OAuth 2.1 (PKCE)** en is **per gebruiker op `org_id`
gescoped** — iedereen ziet uitsluitend de meetings van de eigen organisatie.

> ⚠️ **Let op — deze plugin-route werkt alleen in de ChatGPT-desktop-app.**
> ChatGPT markeert elke uit GitHub geïmporteerde plugin met een MCP-server als
> *"Desktop only"*. Wil je ANNA! óók op **web en mobiel**, gebruik dan de
> **connector-route**: zie **[CONNECTOR-INSTALL.md](CONNECTOR-INSTALL.md)**
> (dezelfde MCP-URL, als custom connector workspace-breed gepubliceerd).

## Inhoud
```
.agents/plugins/marketplace.json        # marketplace-manifest (verwijst naar de plugin)
plugins/anna-notulist/
  .codex-plugin/plugin.json             # plugin-manifest (ChatGPT/Codex)
  .claude-plugin/plugin.json            # zelfde manifest (cross-compat)
  .mcp.json                             # → https://mcp.aifundament.nl/mcp (streamable-http, OAuth)
  skills/
    notulen-opzoeken/SKILL.md           # opnames vinden + notulen/transcript/acties lezen
    overzicht-en-acties/SKILL.md        # overkoepelende samenvattingen + actiepunten
  assets/icon.png                       # app-icoon
SUBMISSION.md                           # metadata + testcases (voor de publieke directory, optioneel)
```

## Installeren bij een klant (workspace-admin, Business/Enterprise)

1. ChatGPT → **Admin → Plugins → Add → Import marketplace**.
2. **Source:** `https://github.com/AI-werkt/anna-chatgpt-plugin` (géén branch of map).
3. **Path:** leeg laten (het marketplace-manifest staat in de repo-root onder `.agents/plugins/`).
4. **Branch, tag, or commit:** leeg laten (default branch).
5. **Import marketplace** → GitHub autoriseren wanneer gevraagd.
6. Open bij **Import results** de plugin **ANNA!** en zet de **Installation policy**
   (`Available` of `Installed`) voor de gewenste rollen.
7. Gebruikers verbinden bij het eerste gebruik hun ANNA-account via de **OAuth-flow**
   (de plugin vraagt dit bij installatie/eerste aanroep). Daarna in een chat: typ `@`,
   kies **ANNA!**, en vraag bijv. *"Welke meetings had ik vorige week?"*

> Nieuwe marketplaces synchroniseren dagelijks. Wijzigingen eerder ophalen kan via
> **Admin → Plugins → Marketplaces → Sync now**.

## Zelf eerst testen (onze eigen workspace)

Volg exact dezelfde stappen in de eigen AI werkt!-workspace en loop de testcases uit
`SUBMISSION.md` door (5 positieve + 3 negatieve), zodat de keten — import → OAuth →
tools → org-scoping — bevestigd is vóór uitrol bij klanten.

## Alternatief: publieke directory

Wil je ANNA! óók beschikbaar maken voor klanten op Plus/Free (die geen custom
marketplace kunnen koppelen), dan kan de plugin naar de **publieke ChatGPT-directory**
via het submission-portaal. Zie `SUBMISSION.md` voor de metadata en testcases.

De MCP-server (`mcp.aifundament.nl`) is read-only onder scope `meetings.read`;
`generate_notulen` en `summarize_meetings` vallen onder `meetings.generate`.
