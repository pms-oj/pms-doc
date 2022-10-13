### note that for some notations
- [x]: enumeration of arbitrary elements which are following rule x
- {x}: indefinite variable x
- *: optional; not required
Directory structure of PMS task v1

  ../{task UUID}

  - task.toml

  - checker
      - checker.toml
      - {checker file}
  - tests
      - [{standard input}.in]
      - [{standard output}.out]
  - subtasks
      - [{name of subtask}.toml]
  - statements
      - [{IETF language tag}]
          - statement.toml
          - [statement.{tex, pdf, md}]
  - graders
      - grader.toml
      - {manager file}
      - * [{language UUID}]
          - stub.toml
          - Makefile
          - [{stub file}]
  - attachments
      - [{attachment file}]