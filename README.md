# Shared Controls — downloads

One Minecraft character, several brains. One player is the **Body**; everyone else
sees the world **through the Body's eyes** (locked spectator view with the Body's
hotbar and health) while their own mouse/keyboard drives one slice of the Body's
controls — camera, clicks, movement, inventory. The Body can keep some controls
for themself (e.g. walk their own body while others aim and click). All on the same
server: no web pages, no IPs, no port forwarding.

**For Minecraft 26.2** (Fabric on the clients, Paper on the server).

## Downloads (this repo)

| file | who installs it | where |
|---|---|---|
| [`sharedcontrols-0.5.0.jar`](sharedcontrols-0.5.0.jar) | **every player** (Body + controllers) | Minecraft `mods/` folder |
| [`sharedcontrols-relay-0.2.1.jar`](sharedcontrols-relay-0.2.1.jar) | **the server** | Paper `plugins/` folder |

## Install

### Every player (all of you, same steps)

1. Install [Fabric Loader](https://fabricmc.net/use/installer/) for Minecraft **26.2**.
2. Put in your `mods/` folder (Windows: `%appdata%\.minecraft\mods`, Mac: `~/Library/Application Support/minecraft/mods`):
   - `sharedcontrols-0.5.0.jar` (from this repo)
   - [Fabric API](https://modrinth.com/mod/fabric-api) 0.157.0+26.2
3. Launch with the Fabric profile.

### Server (once)

Drop `sharedcontrols-relay-0.2.1.jar` into the server's `plugins/` folder (remove any
older sharedcontrols-relay jar) and restart.
Must be a Paper (or Paper-fork) server on Minecraft 26.2. The console should log
`[SharedControlsRelay] Shared Controls relay ready`. The plugin only relays messages —
it never touches gameplay, and players without the mod are unaffected.

## Config (optional)

The Body's client creates `config/sharedcontrols.json` on first launch. Replace it
with one of the presets in [`configs/`](configs/) — the file defines which roles
exist:

- [`3-players.json`](configs/3-players.json) — Body + 2: driver (movement+inventory) and aimer (camera+clicks). This is the built-in default.
- [`4-players.json`](configs/4-players.json) — Body + 3: movement / camera / hands (clicks+inventory).
- [`7-players-chaos.json`](configs/7-players-chaos.json) — Body + 6: every capability its own person, left and right click included.

Rename whichever you pick to `sharedcontrols.json`. `cameraSensitivity` is degrees
per pixel of the camera controller's mouse. Only the Body's config matters.

## How to play

Everyone joins the server, then in chat:

```
body>        /sc body                      claim Body
controllers> /sc join                      each controller — that's the whole setup
body>        /sc assign movement <name>    (you can assign a role to YOURSELF too —
body>        /sc assign camera <name>       the Body keeps those controls)
body>        /sc assign hands <name>
body>        /sc start
```

On `/sc start`: every controller is snapped into a view **through the Body's eyes**
that looks like normal first-person play — the Body's held item in hand, the Body's
hotbar, hearts and crosshair — and everyone's inputs reduce to exactly their role
(F5 flips to third person to watch the Body). When anyone opens the Body's inventory
or a chest, **it opens on everyone's screen** — the inventory holder clicks, the rest
watch. On `/sc stop` every controller instantly pops back to where they were
standing, in their old gamemode, with full control.

While running:

- **Movement** holder: WASD / space / shift / sprint walk the Body.
- **Camera** holder: their mouse aims the Body — and since everyone watches through
  the Body, aiming turns everyone's shared view.
- **Interact** holder: mouse buttons mine / attack / place / use as the Body.
- **Inventory** holder: keys 1–9 / Q / F work the Body's hotbar; **E** opens a live
  mirror of the Body's inventory (or open chest) — click to move items.
- **The Body**: dead controls except chat, `/` commands, Esc — plus any role assigned
  to their own name, which works on their normal keys.
- Body types: `/sc swap <a> <b>` (trade roles mid-game), `/sc table`, `/sc unassign`,
  `/sc reload` (re-read config), `/sc stop`.

Rules the mod enforces: one person per role; an unassigned role does nothing; a
controller who disconnects has their roles unassigned, their spectator view undone,
and everyone is told; `/sc stop` always returns everyone to normal instantly.
