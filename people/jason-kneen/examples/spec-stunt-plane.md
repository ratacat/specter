<!-- source: https://github.com/jasonkneen/tiny-world-builder/blob/main/docs/superpowers/specs/2026-06-01-stunt-plane-combat-design.md -->
# Stunt-plane combat: guns, targeting, missiles

A design spec beside numbered `plans/012-*.md`. Goal, non-goals, principles, then three systems.

## Goal

Bring ships-combat *feel* (wing guns, targeting HUD, guided missiles) to tinyworld flight. Do not port the ships economy.

## Out of scope

Ammo economy, weapon heat, flares/countermeasures, alien weapon, AI dogfight, score banners, gamepad/touch.

## Invariants

Combat lives in scene-space. Flight physics untouched. Own module, hooked like multiplayer (`tick` / `onEnter` / `onExit`). One load-bearing abstraction: the **target adapter** (`id`, `kind`, `getWorldPos`, `radius`, `isAlive`, `label`, `speedKts`, `applyDamage`).

## Architecture

System 1 guns. System 2 targeting HUD. System 3 missiles. Damage model for world objects.
