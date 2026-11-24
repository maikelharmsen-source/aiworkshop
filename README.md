# AI Workshop - OpenEdge ABL Project

Workshop starter copied from the tracked files of ProjectGengar's Step-16 branch. Local untracked additions and source repository history are not included.

## Requirements and setup

- Windows with OpenEdge 12.8 and a configured `DLC` environment variable.
- Apache Ant and the OpenEdge PCT library at `${DLC}/pct/PCT.jar` for the database setup target.
- An ABL development environment with `src` on PROPATH and the OpenEdge business logic libraries available.

Run `ant db` from the repository root to create the local Sports2000 sample database. Connect it as logical database `sp2k` and define the `sports` alias as specified in [openedge-project.json](openedge-project.json).

Database binaries, compiled r-code, local configuration, scripts, and large library reference documents are intentionally excluded. [dump/sports2000-schema.txt](dump/sports2000-schema.txt) is an informational summary, not a loadable schema. Export the full schema from your local Sports2000 database to `dump/sports2000.df` before using schema-based editor features or the included database rule.

## Contents

- [src/CustomerWin.w](src/CustomerWin.w): customer lookup and update window.
- [src/ItemWin.w](src/ItemWin.w): original item window with direct database access, retained as a workshop starting point.
- [src/business](src/business): customer entity, dataset, and singleton entity factory.
- [doc/business-entity-pattern.md](doc/business-entity-pattern.md): condensed architecture guide.
- [.windsurf](.windsurf): original rules and workflows.
- [.github/ISSUE_TEMPLATE](.github/ISSUE_TEMPLATE): bug and feature request templates.

The original Step-16 application sources are preserved as workshop exercises, not refactored or runtime-tested by this export. Item entity classes from later local work are not part of this snapshot.
