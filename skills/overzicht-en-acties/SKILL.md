---
name: overzicht-en-acties
description: Maak overkoepelende overzichten en actiepunten-lijsten over meerdere ANNA!-opnames, of genereer notulen opnieuw met een ander sjabloon. Gebruik dit voor vragen als "vat de meetings over project X samen", "welke actiepunten staan er nog open", of "maak er beknoptere notulen van".
---

Je maakt overzichten die meerdere ANNA!-opnames combineren, en helpt met actiepunten. Alles is beperkt tot de organisatie van de ingelogde gebruiker.

## Welke tool wanneer
- **Overkoepelende samenvatting over meerdere meetings** ("vat alles over project Uithoorn samen", "wat is de rode draad van deze week"): `summarize_meetings` — geef de relevante `meeting_id`'s of een zoek-/datumfilter mee. De tool doet een map-reduce over de bestaande samenvattingen.
- **Actiepunten verzamelen** ("welke acties liggen er nog", "actiepunten voor Joost"): `list_action_items` — desgewenst gefilterd per meeting; groepeer daarna zelf per eigenaar of per meeting.
- **Notulen opnieuw genereren** ("maak er kortere/andere notulen van"): `generate_notulen` — herschrijft de notulen van één meeting met een sjabloon. Standaard niet-destructief (een voorstel); alleen definitief opslaan als de gebruiker daar expliciet om vraagt.
- **Klantcontext** ("wie waren de deelnemers", "wat weten we van klant X"): `list_client_profiles` / `get_client_profile`.

## Werkwijze
1. Bepaal welke opnames in scope zijn (via zoeken/datum uit de skill *notulen-opzoeken*), bevestig de selectie kort bij twijfel.
2. Roep de juiste overzichts-tool aan en presenteer het resultaat gestructureerd: korte samenvatting, daarna kernpunten en/of actiepunten als lijst (met eigenaar + deadline waar bekend).
3. Bij actiepunten over meerdere meetings: groepeer logisch (per eigenaar of per project) en ontdubbel.
4. Verzin niets; gebruik alleen wat de tools teruggeven, en verwijs naar de bron-meetings (`meeting_url`).

## Let op
- `generate_notulen` en `summarize_meetings` vallen onder de scope `meetings.generate`; als die niet is toegekend, meld dat vriendelijk en val terug op de al bestaande samenvattingen.
- Wees expliciet over wat je gebruikt hebt ("op basis van 4 meetings van deze week"), zodat de gebruiker de scope kan controleren.
