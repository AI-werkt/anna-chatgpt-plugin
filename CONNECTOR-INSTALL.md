# ANNA! in ChatGPT — als connector (web, mobiel én desktop)

Deze route voegt ANNA! toe als **custom connector** (remote MCP-server). Anders dan de
GitHub-plugin — die alleen in de **ChatGPT-desktop-app** werkt — werkt een connector op
**web, mobiel en desktop**. Je koppelt de ANNA-MCP-server één keer en publiceert 'm voor
de hele werkruimte; iedere gebruiker logt daarna met z'n eigen ANNA-account in en ziet
**uitsluitend de meetings van de eigen organisatie** (OAuth 2.1, org-gescoped).

- **Nodig:** ChatGPT **Business** of Enterprise/Edu, en een **workspace-admin/owner**.
- **MCP-URL:** `https://mcp.aifundament.nl/mcp`
- **Authenticatie:** OAuth — **Client ID en Secret leeg laten** (de server registreert zich
  automatisch via Dynamic Client Registration).

---

## A. Eenmalig instellen (admin/owner)

**1. Developer mode aanzetten**
Settings → **Apps & Connectors** → **Advanced settings** → **Enable developer mode**.
(Hiermee mag je een eigen, nog niet-geverifieerde MCP-connector toevoegen.)

**2. De connector aanmaken**
Settings → **Connectors** → **Create**:
- **Name:** `ANNA!`
- **Server URL / MCP URL:** `https://mcp.aifundament.nl/mcp`
- **Authentication:** **OAuth**
- **Client ID / Secret:** leeg laten
- Aanmaken/opslaan.

**3. Inloggen (OAuth)**
Er opent een venster om in te loggen met je **ANNA-account**. Keur de toegang goed
(scopes `meetings.read` voor lezen en `meetings.generate` voor notulen (her)genereren).
Na het koppelen is de connector eerst **alleen voor jou** zichtbaar.

**4. Publiceren naar de werkruimte**
Settings → **Workspace settings** → **Apps** → tab **Drafts** → zoek **ANNA!** → **Publish**.
Kies desgewenst voor welke rollen 'ie beschikbaar is. Daarna kunnen collega's 'm zelf
koppelen.

---

## B. Voor elke gebruiker (web / mobiel / desktop)

1. Open een nieuwe chat (web, mobiele app of desktop-app).
2. Typ **`@`** en kies **ANNA!** (of koppel 'm één keer via Settings → Connectors → **Connect**
   en log in met je ANNA-account).
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

- **Geen "Connectors"/"Developer mode" in Settings:** het account zit niet op Business/
  Enterprise/Edu, of developer mode staat uit (zie stap 1). Op Pro zijn alleen lezen/zoeken
  mogelijk; Free wordt niet ondersteund.
- **Gepubliceerde connector niet zichtbaar bij collega's:** geef het even tijd / herlaad;
  controleer of 'ie echt is **gepubliceerd** (niet in Drafts) en voor de juiste rol beschikbaar is.
- **OAuth-venster loopt vast:** opnieuw proberen; de koppeling gebruikt standaard OAuth 2.1
  met PKCE en automatische client-registratie, dus er zijn geen handmatige sleutels nodig.

---

> Alternatief (alleen desktop): installeren als GitHub-plugin — zie **README.md**.
> Alternatief (alle plannen, incl. Plus/Free): publieke ChatGPT-directory — zie **SUBMISSION.md**.
