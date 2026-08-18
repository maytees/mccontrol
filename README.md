# Shared Controls — downloads

One Minecraft character, several brains. One player is the **Body**; everyone else
sees the world **through the Body's eyes** (first-person view with the Body's items
in their hands, hotbar, hearts) while their own mouse/keyboard drives one slice of
the Body's controls — camera, clicks, movement, inventory. The Body can keep some
controls for themself (e.g. walk their own body while others aim and click). All in
Minecraft, all configured from an in-game menu (`/sc`): no config files, no web
pages, no IPs, no port forwarding.

**For Minecraft 26.2** (Fabric on the clients, Paper on the server).

## Downloads (this repo)

| file | who installs it | where |
|---|---|---|
| [`sharedcontrols-0.7.1.jar`](sharedcontrols-0.7.1.jar) | **every player** (Body + controllers) | Minecraft `mods/` folder |
| [`sharedcontrols-relay-0.2.3.jar`](sharedcontrols-relay-0.2.3.jar) | **the server** | Paper `plugins/` folder |

## Install

### Every player (all of you, same steps)

1. Install [Fabric Loader](https://fabricmc.net/use/installer/) for Minecraft **26.2**.
2. Put in your `mods/` folder (Windows: `%appdata%\.minecraft\mods`, Mac: `~/Library/Application Support/minecraft/mods`):
   - `sharedcontrols-0.7.1.jar` (from this repo)
   - [Fabric API](https://modrinth.com/mod/fabric-api) 0.157.0+26.2
3. Launch with the Fabric profile.

### Server (once)

Drop `sharedcontrols-relay-0.2.3.jar` into the server's `plugins/` folder (remove any
older sharedcontrols-relay jar) and restart.
Must be a Paper (or Paper-fork) server on Minecraft 26.2. The console should log
`[SharedControlsRelay] Shared Controls relay ready`. The plugin only relays messages —
it never touches gameplay, and players without the mod are unaffected.

## How to play — it's all in the `/sc` menu

Everyone joins the server, then types **`/sc`**:

- **The Body's menu**: claim Body, edit roles (name + six capability toggles per
  row), one-click assign each role to any connected player (including yourself —
  the Body keeps those controls), load the built-in 2/3/4/7-player presets or save
  your own, and Start/Stop the session.
- **A controller's menu**: the current Body's player head and a **Join** button.
  That's their whole job.

Chat commands still work if you prefer (`/sc join`, `/sc assign <role> <name>`,
`/sc swap <a> <b>`, `/sc start`, `/sc stop`, `/sc table`, `/sc say <msg>`).

On **Start**: every controller is snapped into a view **through the Body's eyes**
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
