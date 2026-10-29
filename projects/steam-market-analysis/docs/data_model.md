# Steam Market Analysis — Data Model

## Overview

The processed Steam market data is stored in PostgreSQL under the
`steam_market` schema.

The model preserves one game-level central table and separate bridge tables
for multi-value categorical dimensions.

## Tables

### games

**Grain:** One row per unique Steam AppID  
**Primary Key:** `app_id`

Purpose:

- stores game-level attributes,
- pricing information,
- traction proxies,
- review metrics,
- engagement metrics,
- release information,
- analytical flags.

Important notes:

- Playtest applications were excluded from the main market dataset.
- `estimated_owners` is preserved as a range rather than treated as an exact
  owner count.
- `positive_ratio` is NULL when no review activity exists.
- software-oriented applications are flagged rather than automatically removed.

---

### game_genres

**Grain:** One row per AppID–Genre relationship  
**Primary Key:** (`app_id`, `genre`)  
**Foreign Key:** `app_id → games.app_id`

Purpose:

Represents the many-to-many relationship between games and genres.

---

### game_categories

**Grain:** One row per AppID–Category relationship  
**Primary Key:** (`app_id`, `category`)  
**Foreign Key:** `app_id → games.app_id`

Purpose:

Represents Steam gameplay and feature categories associated with each game.

---

### game_tags

**Grain:** One row per AppID–Tag relationship  
**Primary Key:** (`app_id`, `tag`)  
**Foreign Key:** `app_id → games.app_id`

Purpose:

Represents descriptive tags associated with each game.

## Relationships

games 1 ───< game_genres

games 1 ───< game_categories

games 1 ───< game_tags

At the conceptual level, Games and Genres / Categories / Tags form
many-to-many relationships.

The bridge tables resolve these relationships while preserving the
one-row-per-AppID grain of the `games` table.

## Analytical Considerations

Because one game may belong to multiple Genres, Categories, or Tags:

- counts across groups are not additive,
- joining multiple bridge tables can multiply rows,
- game counts should generally use `COUNT(DISTINCT app_id)` after joins.

The relational model was validated for:

- Primary Key uniqueness,
- Foreign Key integrity,
- duplicate bridge relationships,
- consistency of derived metrics,
- successful JOIN and GROUP BY operations.