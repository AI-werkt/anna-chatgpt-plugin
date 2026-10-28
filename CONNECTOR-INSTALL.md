# ANNA! in ChatGPT — als custom MCP-server (web, mobiel én desktop)

Deze route voegt ANNA! toe als **custom MCP-server**. ChatGPT maakt daar een **plugin**
van (vroeger heette dit "connector"; die menu's bestaan niet meer). Anders dan de
GitHub-plugin — die alleen in de **ChatGPT-desktop-app** werkt — werkt deze route op
**web, mobiel en desktop**. Je voegt de ANNA-MCP-server één keer toe en publiceert 'm voor
de hele werkruimte; iedere gebruiker logt daarna met z'n eigen ANNA-account in en ziet
**uitsluitend de meetings van de eigen organisatie** (OAuth 2.1, org-gescoped).

- **Nodig:** ChatGPT **Business** of Enterprise/Edu, en een **workspace-admin/owner**
  (op Business mogen alleen admins en owners plugins met MCP's maken: permissie
  *Create plugins with MCPs*).
- **MCP-URL:** `https://mcp.aifundament.nl/mcp`
- **Authenticatie:** OAuth — **Client ID en Secret leeg laten** (de server registreert zich
  automatisch via Dynamic Client Registration).

---

## A. Eenmalig instellen (admin/owner, in de browser)

**1. De MCP-server toevoegen**
Ga naar **Plugins** ([chatgpt.com/plugins](https://chatgpt.com/plugins)) → **+** →
**Add custom MCP server**:
- **Name:** `ANNA!`
- **Connection → Server URL:** `https://mcp.aifundament.nl/mcp`
- **Authentication:** **OAuth**
- **Client ID / Secret:** leeg laten
- Lees de waarschuwing, kies **I understand and want to continue** en daarna
  **Create as a plugin**.

Een aparte "developer mode" aanzetten is niet meer nodig.

**2. Inloggen (OAuth)**
Er opent een venster om in te loggen met je **ANNA-account**. Keur de toegang goed
(scopes `meetings.read` voor lezen en `meetings.generate` voor notulen (her)genereren).
Na het toevoegen is de plugin eerst **alleen voor jou** zichtbaar.

**3. Publiceren naar de werkruimte**
Workspace settings → **Apps** → tab **Drafts** → zoek **ANNA!** → **Publish**.
Kies desgewenst voor welke rollen 'ie beschikbaar is. Daarna kunnen collega's 'm zelf
installeren.

---

## B. Voor elke gebruiker (web / mobiel / desktop)

1. Installeer **ANNA!** één keer via **Plugins** en log in met je ANNA-account.
2. Open een nieuwe chat (web, mobiele app of desktop-app), typ **`@`** en kies **ANNA!**.
3. Vraag bijvoorbeeld:
   - *"Welke meetings had ik vorige week?"*
   - *"Wat waren de actiepunten uit de vergadering van [datum]?"*
   - *"Vat het overleg over [onderwerp] samen."*

Je ziet altijd alleen de opnames van je **eigen organisatie**.

---

## Wat ANNA! kan (tools)

- **Lezen** (`meetings.read`): opnames vinden op onderwerp/datum, een opname openen,
  samenvatting en volledig transcript lezen, actiepunten ophalen (met eigenaar/deadline),
  klantprofielen bekijken.
- **Genereren** (`meetings.generate`): notulen (her)genereren en overkoepelende
  samenvattingen over meerdere meetings maken.
- **Geen verwijder-/wijzig-tools** op brondata.

## Problemen oplossen

- **Geen "Connectors" in Settings:** klopt, die heten nu **Plugins**. Volg stap A1 hierboven.
- **Geen "+ → Add custom MCP server" bij Plugins:** het account is geen admin/owner van de
  Business-werkruimte, of zit niet op Business/Enterprise/Edu. Laat een beheerder de
  plugin toevoegen en publiceren; Free wordt niet ondersteund.
- **Gepubliceerde plugin niet zichtbaar bij collega's:** geef het even tijd / herlaad;
  controleer of 'ie echt is **gepubliceerd** (niet in Drafts) en voor de juiste rol beschikbaar is.
- **OAuth-venster loopt vast:** opnieuw proberen; de koppeling gebruikt standaard OAuth 2.1
  met PKCE en automatische client-registratie, dus er zijn geen handmatige sleutels nodig.

---

> Alternatief (alleen desktop): installeren als GitHub-plugin — zie **README.md**.
> Alternatief (alle plannen, incl. Plus/Free): publieke ChatGPT-directory — zie **SUBMISSION.md**.
