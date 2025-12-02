# pw-harness

This is new version of harness for parsewave based on [Harbor](https://github.com/laude-institute/harbor)

Mostly it's the same, just different file names.

Top 5 problems after migration we noticed:
1. custom docker-compose.yaml file
2. UpperCase task name - docker fails to create container
3. exec /opt/pytest-venv/bin/pytest - it doesn't return exit code
4. Existing /tests directory collapses with /tests in harbor
5. 'RUN pipx ensurepath' things setup via PATH stop working

Migrate tasks:
```
uv run harbor tasks migrate -i contributor_tasks -o harbor_tasks
```

Run nop:
```
uv run harbor run -a nop -p contributor_tasks/task
```

Run oracle:
```
uv run harbor run -a oracle -p contributor_tasks/task
```

Run oss 5 attempts:
```
uv run harbor run -a terminus-2 -p contributor_tasks/task -m openrouter/openai/gpt-oss-120b -k 5
```
