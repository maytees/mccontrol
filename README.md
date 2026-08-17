# Shared Controls — downloads

One Minecraft character, several brains. One player is the **Body**; everyone else
drives one slice of their controls (movement, camera, clicks, inventory) from their
own Minecraft client, all on the same server. No web pages, no IPs, no port
forwarding — everything rides the Minecraft server connection.

**For Minecraft 26.2** (Fabric on the clients, Paper on the server).

## Downloads (this repo)

| file | who installs it | where |
|---|---|---|
| [`sharedcontrols-0.1.0.jar`](sharedcontrols-0.1.0.jar) | **every player** (Body + controllers) | Minecraft `mods/` folder |
| [`sharedcontrols-relay-0.1.0.jar`](sharedcontrols-relay-0.1.0.jar) | **the server** | Paper `plugins/` folder |

## Install

### Every player (all of you, same steps)

1. Install [Fabric Loader](https://fabricmc.net/use/installer/) for Minecraft **26.2**.
2. Put in your `mods/` folder (Windows: `%appdata%\.minecraft\mods`, Mac: `~/Library/Application Support/minecraft/mods`):
   - `sharedcontrols-0.1.0.jar` (from this repo)
   - [Fabric API](https://modrinth.com/mod/fabric-api) 0.157.0+26.2
3. Launch with the Fabric profile.

### Server (once)

Drop `sharedcontrols-relay-0.1.0.jar` into the server's `plugins/` folder and restart.
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
body>        /sc assign movement <name>
body>        /sc assign camera <name>
body>        /sc assign hands <name>
body>        /sc start                     Body's controls die, controllers take over
```

While running:

- **Movement** holder: your WASD / space / shift / sprint walk the Body (your own character freezes for those keys).
- **Camera** holder: your mouse aims the Body; your own view turns with it.
- **Interact** holder: your mouse buttons mine / attack / place / use as the Body.
- **Inventory** holder: keys 1–9 / Q / F work the Body's hotbar; press **E** for a live
  mirror of the Body's inventory (or open chest) — click slots to move items,
  shift-click to quick-move.
- Anyone: `/sc table` (who holds what), `/sc say <msg>` (chat role).
- Body: `/sc swap <a> <b>` (trade two people's roles mid-game), `/sc unassign <role>`,
  `/sc clear`, `/sc stop` (instantly get your body back).

Rules the mod enforces: one person per role; an unassigned role does nothing; a
controller who disconnects has their roles unassigned and everyone is told; `/sc stop`
always returns the Body to normal instantly; nothing about the world, the server, or
other players is ever modified.
