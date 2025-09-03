# Codex Task List

This document outlines tasks for Codex to extend this First Person Starter into a feature-complete FPS prototype.

## Player
- Implement `CharacterBody3D` movement with jump, sprint, and mouse look.
- Ensure movement works with both keyboard/mouse and controller.

## Weapons
- Design a base weapon class with fire, reload, equip.
- Implement a hitscan rifle as an example.
- Add ammo management.

## UI
- Create a HUD with crosshair, health and ammo display.
- Add pause and settings menus.

## Enemies
- Add basic AI that patrols and chases the player.
- Use a navigation mesh for pathfinding.

## Build & CI
- Provide export presets for Linux and Windows.
- Add a GitHub Actions workflow to run Godot in headless `--check-only` mode.

Refer to the comments in the code and tasks for further details.
