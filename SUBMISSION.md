# OpenAI plugin-submissie — ANNA!

Alles wat nodig is om de plugin in te dienen via het OpenAI **plugin-submission**-portaal
("With MCP"). In te vullen/uit te voeren door de eigenaar van het OpenAI-account (AI werkt!).

## Directory-metadata
| Veld | Waarde |
|---|---|
| **Naam (display)** | ANNA! |
| **Korte omschrijving** | Praat met je vergaderarchief: notulen, transcripten, actiepunten en samenvattingen. |
| **Lange omschrijving** | ANNA! is een bot-vrije AI-notulist. Met deze plugin bevraag je vanuit ChatGPT je eigen ANNA!-vergaderarchief: vind opnames op onderwerp of datum, lees de AI-samenvatting of het volledige transcript, haal actiepunten op (met eigenaar en deadline) en maak overkoepelende samenvattingen over meerdere meetings. Alles blijft binnen je eigen organisatie. |
| **Categorie** | Productiviteit / Notities & vergaderingen |
| **Keywords** | notulen, meetings, transcriptie, actiepunten, samenvatting |
| **Icoon** | `assets/icon.png` (512×512) |
| **Homepage** | https://meeting.aifundament.nl |
| **Support-contact** | carel.kuijper@ai-werkt.nl |
| **Privacybeleid** | https://meeting.aifundament.nl/privacy  _(URL bevestigen/aanmaken vóór indienen)_ |
| **Beschikbaarheid (landen)** | Nederland (uitbreiden naar wens) |

## MCP-technisch
- **Productie-/mcp-URL:** `https://mcp.aifundament.nl/mcp` (streamable HTTP)
- **Auth:** OAuth 2.1 + PKCE, met Dynamic Client Registration. Metadata op
  `/.well-known/oauth-authorization-server` en `/.well-known/oauth-protected-resource/mcp`.
- **Scopes:** `meetings.read` (read-only), `meetings.generate` (notulen (her)genereren).
- **Org-scoping:** elke tool filtert op de `org_id` uit het token — een gebruiker ziet
  uitsluitend de meetings van de eigen organisatie.
- **Tools (read-only):** `list_meetings`, `get_meeting`, `get_meeting_by_date`,
  `get_transcript`, `get_summary`, `list_action_items`, `search_meetings`,
  `list_client_profiles`, `get_client_profile`.
- **Tools (generate):** `generate_notulen`, `summarize_meetings`.
- **Geen destructieve tools** (geen verwijderen/wijzigen van brondata).

## CSP-domeinen (op te geven in het portaal)
- `https://mcp.aifundament.nl` (MCP + OAuth-endpoints)
- `https://meeting.aifundament.nl` (login/redirect bij de OAuth-flow)

## Domeinverificatie
Verifieer `aifundament.nl` (of `mcp.aifundament.nl`) in het OpenAI-portaal — meestal via een
DNS-TXT-record of een bestand op de well-known-locatie. Voer dit uit met toegang tot de DNS.

## Reviewer-inloggegevens
OpenAI-reviewers moeten de OAuth-flow kunnen doorlopen. Maak een **testaccount** in ANNA!
met een eigen organisatie en enkele **voorbeeld-meetings** (transcript + notulen + een paar
actiepunten), zodat de tools echte data teruggeven. Lever e-mail + wachtwoord bij de submissie.
> Testaccount: `______________`  ·  wachtwoord: `______________`  (invullen vóór indienen)

## Testcases

### 5 positieve (moeten werken)
1. **"Welke meetings had ik afgelopen week?"** → `list_meetings`; toont een lijst met titel + datum.
2. **"Vat het overleg over [onderwerp] samen."** → `search_meetings` → `get_summary`; bondige samenvatting + kernpunten met bronlink.
3. **"Wat waren de actiepunten uit de vergadering van [datum]?"** → `get_meeting_by_date` → `list_action_items`; lijst met eigenaar/deadline.
4. **"Geef een overkoepelende samenvatting van de meetings over [project]."** → `summarize_meetings` over meerdere opnames.
5. **"Laat het transcript zien van [meeting] rond [tijdstip]."** → `get_transcript`; relevante passage met tijdstip/bronlink.

### 3 negatieve (moeten netjes worden afgewezen/afgehandeld)
1. **"Laat de notulen zien van [ander bedrijf dat niet mijn organisatie is]."** → de tools zijn org-gescoped; er komt niets terug en het model legt uit dat alleen je eigen organisatie zichtbaar is.
2. **"Verwijder al mijn opnames uit ANNA!."** → er is geen verwijder-tool; het model meldt dat het opnames niet kan verwijderen en verwijst naar de app.
3. **"Boek een vlucht naar Barcelona."** → buiten scope; het model gebruikt de ANNA!-tools niet en helpt niet met deze onbedoelde vraag.

## Vóór indienen — checklist
- [ ] Privacybeleid-URL live en correct.
- [ ] Testaccount met voorbeeld-meetings aangemaakt; inloggegevens ingevuld.
- [ ] Domein `aifundament.nl` geverifieerd in het OpenAI-portaal.
- [ ] Identiteits-/bedrijfsverificatie in het OpenAI Platform-dashboard afgerond (onder de naam waaronder je publiceert).
- [ ] MCP-server live (check: `POST /mcp` zonder token → 401 + OAuth-metadata).
