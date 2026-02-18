# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This repository is a collection of reusable Claude Code **hooks** and **skills/commands** (skicmd). It serves as a personal library of automation tools that can be referenced across projects.

## Repository Structure

- `skicmd/` — Skills/commands, organized by category in subdirectories
  - `repos/` — Repository initialization and scaffolding commands

## Skills/Commands Convention

Each skill is a single Markdown file under `skicmd/<category>/`. The file format:

- Filename becomes the command name (e.g., `iniGit.md` → `/iniGit`)
- Contains a heading with the command name, a description, and an `## Instructions` section with the steps Claude should execute
- Instructions should be self-contained and executable without external context