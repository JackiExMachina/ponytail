---
name: ponytail-debt
description: >
  List every `shortcut:` comment (and older `ponytail:` ones) as a debt ledger. One-shot report,
  changes nothing. Use for "ponytail debt", "what did ponytail defer", "list the
  shortcuts", /ponytail-debt.
---

Every deliberate ponytail shortcut is marked with a `shortcut:` comment naming
its ceiling and upgrade path (older code may say `ponytail:`). This collects them into one ledger so a deferral
can't quietly become permanent.

## Scan

Grep the repo for comment markers, skipping `.git` and everything the
`.gitignore` files ignore (dependencies, build output, caches, in any stack):

`git grep --no-index --exclude-standard -nE '(#|//|/[*]) ?(shortcut|ponytail):'`  (add other comment prefixes if your stack uses them)

If the user names their own marker word (`/ponytail-debt TODO`), grep for that word instead.

Each hit is one ledger row. The comment prefix keeps prose that merely mentions
the convention out of the ledger. Skip hits that are not a deferral, like a note
about a keyboard shortcut.

## Output

Язык: русский.
По одной строке на каждый маркер, сгруппировано по файлам:

`<файл>:<строка>, <что упростили>. предел: <названный лимит>. когда переделать: <триггер для ревизии>.`

Флаг риска загнивания: если в комментарии нет триггера обновления, помечать тегом `без-триггера` (это то, что тихо сгниёт в коде).

Завершать строкой: `<N> маркеров, <M> без триггера.`
Если ничего не найдено: `Технического долга нет. Реестр чист.`

## Boundaries

Только читает и отчитывается, код не меняет. По просьбе может записать реестр в файл (например, `PONYTAIL-DEBT.md`). One-shot.
