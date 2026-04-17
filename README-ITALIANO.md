# PlaceAnywhere — Documentazione (Italiano)

**Versione:** 1.0.0  
**Autore:** MasterCraft  
**API Minecraft:** 1.20+  
**Compatibilità:** Paper / Spigot

---

PlaceAnywhere è un plugin Bukkit/Paper che permette ai giocatori autorizzati di piazzare piante, fiori, decorazioni e altri blocchi "ristretti" su qualsiasi superficie, ignorando le regole di piazzamento vanilla di Minecraft..

---

## Comandi

Tutti i comandi hanno come alias `/pa` e `/pla` oltre al nome completo `/placeanywhere`.

| Comando | Descrizione |
|---|---|
| `/pa` | Attiva/disattiva PlaceAnywhere per te stesso |
| `/pa toggle` | Equivalente a `/pa` (toggle su se stesso) |
| `/pa on` | Attiva PlaceAnywhere per te stesso |
| `/pa off` | Disattiva PlaceAnywhere per te stesso |
| `/pa <giocatore>` | Attiva/disattiva PlaceAnywhere per un altro giocatore |
| `/pa toggle <giocatore>` | Uguale al precedente |
| `/pa on <giocatore>` | Attiva per un altro giocatore |
| `/pa off <giocatore>` | Disattiva per un altro giocatore |
| `/pa info` | Mostra info sul tuo stato, modalità, versione del plugin e statistiche di sessione |
| `/pa list` | Lista di tutti i giocatori con PlaceAnywhere attualmente attivo |
| `/pa reload` | Ricarica la configurazione senza riavviare il server |

---

## Permessi

| Permesso | Descrizione | Default |
|---|---|---|
| `placeanywhere.use` | Accesso al comando `/pa` | op |
| `placeanywhere.toggle` | Attivare/disattivare PlaceAnywhere per se stessi | op |
| `placeanywhere.toggle.others` | Attivare/disattivare PlaceAnywhere per altri giocatori | op |
| `placeanywhere.reload` | Ricaricare la configurazione | op |
| `placeanywhere.notify` | Ricevere notifiche admin quando un giocatore attiva/disattiva la modalità | op |
| `placeanywhere.bypass.permission` | Bypass dei controlli di permesso (sempre attivo) | false |
| `placeanywhere.*` | Tutti i permessi sopra elencati | op |

> Per dare tutti i permessi a un gruppo con LuckPerms: `lp group admin permission set placeanywhere.* true`

---

## Blocchi supportati

Il plugin gestisce le seguenti categorie di blocchi, ognuna attivabile/disattivabile singolarmente nel config:

| Categoria | Esempi |
|---|---|
| `plants` | Erba corta, felci, arbusti secchi, tutte le piantine (sapling) |
| `tall-plants` | Erba alta, felce alta, girasole, lilla, cespuglio di rose, peonia |
| `flowers` | Tarassaco, papavero, orchidea blu, amaranto, fiordaliso, giglio, rosa stregata, ecc. |
| `mushrooms` | Fungo marrone, fungo rosso |
| `fungi` | Fungo cremisi, fungo deformato, germogli del nether |
| `nether-plants` | Verruca del nether, liane piangenti, liane attorcigliate |
| `aquatic` | Alghe, alga marina, cetriolo di mare, tutti i tipi di corallo e ventagli corallini |
| `decorations` | Cornici, dipinti, scale, lanterne, catene, campane, vasi, ninfea, asta di fine, aste di fulmine, leve, uncini per filo trappola, pulsanti |
| `torches` | Torce normali, dell'anima, di redstone (anche varianti a muro) |
| `crops` | Grano, carote, patate, barbabietole, steli di melone/zucca, canna da zucchero, bambù, cespuglio di bacche dolci, cacao, ecc. |
| `vines` | Rampicanti, licheni luminosi, liane di grotta, radici sospese, blossom di spore, dripleaf |
| `other` | Tutto il resto non rientrante nelle categorie precedenti |

### Blacklist (blocchi sempre esclusi)

Per default, i seguenti materiali non possono mai essere piazzati con PlaceAnywhere (indipendentemente dai permessi):

- BEDROCK, BARRIER, COMMAND_BLOCK, CHAIN_COMMAND_BLOCK, REPEATING_COMMAND_BLOCK
- END_PORTAL_FRAME, END_PORTAL, NETHER_PORTAL
- STRUCTURE_VOID, STRUCTURE_BLOCK, JIGSAW

Puoi modificare questa lista nel `config.yml`.

---

## Configurazione (`config.yml`)

```yaml
# ============================================================
#   PlaceAnywhere - Configuration
#   Author: MasterCraft
#   Version: 1.0.0
# ============================================================

settings:
  # Modalità predefinita al primo utilizzo del giocatore
  # TOGGLE = si resetta ad ogni login
  # PERSISTENT = viene salvata tra un login e l'altro
  default-mode: TOGGLE

  # Se true, PlaceAnywhere è abilitato di default per tutti i giocatori
  # con il permesso placeanywhere.toggle al momento del login
  enabled-by-default: false

  # Se true, ogni piazzamento viene registrato nella console del server
  log-placements: false

  # Se true, i giocatori con placeanywhere.notify ricevono messaggi in chat
  # quando un altro giocatore attiva/disattiva la modalità
  notify-admins: true

  # Se true, mostra un feedback visivo quando si fa toggle della modalità
  show-toggle-feedback: true
  # Tipo di feedback: ACTIONBAR | TITLE | CHAT | ALL
  feedback-type: ACTIONBAR

  # Suono riprodotto all'attivazione/disattivazione
  sound-on:  BLOCK_NOTE_BLOCK_PLING
  sound-off: BLOCK_NOTE_BLOCK_BASS
  sound-enabled: true

  # Particella visiva al momento del piazzamento (NONE per disabilitare)
  placement-particle: VILLAGER_HAPPY
  particle-count: 5

placement:
  # Forza il piazzamento del blocco anche se vanilla lo cancella
  force-place: true

  # Se true, bypassa i controlli di WorldGuard/GriefPrevention
  # (richiede quei plugin installati)
  bypass-protection-plugins: false

  # Modalità aggressiva: cancella manualmente l'evento vanilla e imposta
  # il blocco direttamente. Più affidabile ma più invasivo.
  aggressive-mode: true

  # Lista di materiali che PlaceAnywhere non può MAI piazzare
  blacklisted-blocks:
    - BEDROCK
    - BARRIER
    - COMMAND_BLOCK
    - CHAIN_COMMAND_BLOCK
    - REPEATING_COMMAND_BLOCK
    - END_PORTAL_FRAME
    - END_PORTAL
    - NETHER_PORTAL
    - STRUCTURE_VOID
    - STRUCTURE_BLOCK
    - JIGSAW

  # Categorie di blocchi gestite dal plugin
  # Metti false su una categoria per disabilitarla completamente
  categories:
    plants: true
    tall-plants: true
    flowers: true
    mushrooms: true
    fungi: true
    nether-plants: true
    aquatic: true
    decorations: true
    torches: true
    crops: true
    vines: true
    other: true

messages:
  prefix: "&8[&6PlaceAnywhere&8] &r"
  enabled: "&aPlaceAnywhere &2ATTIVATO&r. Puoi piazzare qualsiasi blocco ovunque!"
  disabled: "&cPlaceAnywhere &4DISATTIVATO&r. Ritorno alle regole vanilla."
  no-permission: "&cNon hai il permesso di usare questo comando."
  player-only: "&cQuesto comando può essere usato solo da un giocatore."
  reload: "&aConfigurazione ricaricata con successo!"
  player-not-found: "&cGiocatore non trovato: &e{player}"
  toggled-other-on: "&aPlaceAnywhere attivato per &e{player}&a."
  toggled-other-off: "&cPlaceAnywhere disattivato per &e{player}&c."
  notify-admin: "&7[PA] &e{player} &7ha {action} PlaceAnywhere."
  blacklisted-block: "&cQuesto blocco è nella blacklist e non può essere piazzato ovunque."
  info-header: "&8&m----&r &6PlaceAnywhere Info &8&m----"
  info-status: "  &7Stato: {status}"
  info-mode: "  &7Modalità: &e{mode}"
  info-version: "  &7Versione: &e{version}"
  info-author: "  &7Autore: &eMasterCraft"
  list-header: "&8&m----&r &6Giocatori con PlaceAnywhere attivo &8&m----"
  list-entry: "  &e{player} &7- &fAttivo"
  list-empty: "  &7Nessun giocatore ha PlaceAnywhere attivo."

storage:
  # YAML = salva i dati in un file .yml
  # NONE = nessun salvataggio persistente
  type: YAML
  file: playerdata.yml
```

### Dettaglio opzioni importanti

**`default-mode`**  
- `TOGGLE`: lo stato di PlaceAnywhere si azzera ogni volta che il giocatore esce dal server. Utile per server survival dove non vuoi che resti attivo per sbaglio.  
- `PERSISTENT`: lo stato viene salvato in `playerdata.yml` e ripristinato al login successivo.

**`feedback-type`**  
- `ACTIONBAR`: messaggio sopra la barra dell'inventario (consigliato).  
- `TITLE`: titolo grande a schermo.  
- `CHAT`: messaggio in chat normale.  
- `ALL`: sia chat che actionbar.

**`bypass-protection-plugins`**  
Se abilitato, PlaceAnywhere prova a ignorare i controlli di protezione di plugin come WorldGuard o GriefPrevention. Usare con cautela: potrebbe permettere piazzamenti in zone protette.

**`aggressive-mode`**  
Quando attivo, il plugin intercetta e annulla l'evento vanilla di piazzamento, poi imposta il blocco direttamente via API. Risolve i casi in cui Minecraft non lancia nemmeno l'evento (es. erba corta su legno). Consigliato tenerlo `true`.

---

## Struttura dei file generati

```
plugins/PlaceAnywhere/
├── config.yml       ← Configurazione principale
└── playerdata.yml   ← Dati persistenti dei giocatori (solo in modalità PERSISTENT)
```

---

## Comportamento tecnico

- Il plugin intercetta `BlockCanBuildEvent`, `BlockPlaceEvent` e `PlayerInteractEvent`.
- Per le piante alte (es. girasole, erba alta) piazza automaticamente anche il blocco superiore.
- Per le torce, se il click avviene su una parete laterale, usa la variante "a muro" corretta (es. `WALL_TORCH` invece di `TORCH`).
- Il bambù viene piazzato senza foglie (`Bamboo.Leaves.NONE`) per semplicità.
- I blocchi force-piazzati sono temporaneamente registrati internamente per sopprimere gli eventi di fisica vanilla che li rimuoverebbero immediatamente.
- In modalità Survival, l'oggetto viene consumato correttamente dall'inventario.

---

## Compatibilità

- **Paper 1.20+** (consigliato)
- **Spigot 1.20+** (supportato, ma `BlockCanBuildEvent.getPlayer()` potrebbe restituire `null`)
- Non richiede dipendenze obbligatorie.
- Compatibile opzionalmente con WorldGuard e GriefPrevention (via `bypass-protection-plugins`).
