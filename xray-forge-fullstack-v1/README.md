# PACKAGE NOTES

This package standardizes the skill into a Claude-friendly full-directory structure.

Structure:
- SKILL.md → root router skill
- agents/*.md → specialist execution specs
- docs/*.md → reusable support material

Purpose:
Allow Claude to load only the relevant specialist instructions instead of carrying a monolithic prompt on every invocation.
