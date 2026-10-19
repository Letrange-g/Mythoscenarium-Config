# Mythoscenarium-Config

The rules pack that the Mythoscenarium app downloads when a player clicks **Settings > Model rules > Check for updates**.

`rules-pack.json` holds what changes faster than the app does:

- the story and picture models the app offers, with their download files and sizes,
- the settings each story model family runs best with (temperature, min-p, top-k…),
- the picture prompt rules per checkpoint family (Pony score tags, CLIP skip…),
- the default "follow the prompt" value per picture model kind,
- how KoboldCpp runs the story model (context window, KV cache precision, batch size),
- which models to recommend for each size of graphics card,
- the model wizard's pairings (`combos`): a story model plus an anime-family and a realistic picture
  model for each card size and amount of system memory,
- the wizard's looks (`looks`): the art style words new stories start with, and an optional LoRA
  (Hugging Face repo, trigger word, strength) for the SDXL anime models.

## How the app uses it

- The app ships with the same tables built in. A downloaded pack replaces the entries it names (by
  picture model `id`, story model `repo`, rule `match`, look `id`) and adds new ones.
- `recommendations` and `combos` replace the built-in lists whole when the pack has them.
- A pack is only offered when its `version` is newer than the one in use. The player sees the list
  of changes first, installs with one click, and can undo the last install.
- The app only accepts known fields with sane values. Downloads must be Hugging Face repo paths in a
  known ComfyUI folder, and no field can add a command-line flag.
- A player's own `prompt-rules.json` and `text-rules.json` in their data folder still win over the pack.

## Changing it

1. Edit `rules-pack.json` and raise `version` (`YYYY.MM.DD`, or `YYYY.MM.DD.N` for a second one that day).
2. Say what changed in `notes`, in plain words: the player reads them before installing.
3. Merge into `main`. Apps see it on their next check.
