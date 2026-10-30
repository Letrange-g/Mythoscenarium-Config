# Training data for the reader (the small lore keeper)

Backup with history of `/mnt/project-files/paracosm/keeper-data/` (see `docs/TRAINING.md` in the app repo).

- `keeper-pairs/<story>-<label>.jsonl`: one exchange a line (task, story, turn, model, the messages sent, the reply),
  from the replay harness since 0.2.450. Rows whose `model` is the teacher (DeepSeek) are the lessons; rows from the
  small models' sweeps are their own answers, kept for comparison only (`build_dataset.py --teacher deepseek`).
- `keeper-answers/raw-<story><label>.json`: the keeper's answers alone (no prompts) from every replay before 0.2.450,
  1,240 of them; their prompts can be rebuilt by replaying the recordings on the same engine version.

Pushed after each replay batch. Never prune; a thousand pairs is about 30 to 40 MB.
