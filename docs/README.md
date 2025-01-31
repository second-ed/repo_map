# repo mapper
This repo provides a tool to generate and update a repo file structure map in a README file. It supports filtering files by extension, ignoring specified directories, and appending or replacing an existing file structure map.

## features

- Scans a directory and generates a file tree structure.
- Allows filtering by file extensions.
- Ignores specified directories.
- Updates the target README file with the generated file tree.
- Can be integrated with pre-commit hooks.

# cli usage:
```bash
python -m repo_mapper <directory> <readme_path> [--allowed-extensions <ext1> <ext2> ...] [--ignore-dirs <dir1> <dir2> ...]
```

# args
`directory`: The root directory to scan for files.

`readme_path`: Path to the README file to update.

`--allowed-extensions`: (Optional) List of file extensions to include in the map (e.g., .py, .yaml). Defaults to all files.

`--ignore-dirs`: (Optional) List of directory names to exclude from the map.


# examples
### generate a repo map including only Python files and YAML files:

```bash
python -m repo_mapper . ./docs/README.md --allowed-extensions .py .yaml
```

### generate a repo map ignoring the tests directory
```bash
python -m repo_mapper . ./README.md --ignore-dirs tests
```

### generate a repo map ignoring files that match patterns listed in the gitignore
```bash
python -m repo_mapper . ./README.md --use-gitignore
```


### pre-commit integration - used for this repo
```yaml
- id: repo_mapper
  name: repo_mapper
  entry: python -m repo_mapper . ./docs/README.md --use-gitignore --allowed-extensions .py .yaml .toml .md --ignore-dirs mock_data
  language: system
```


# generated repo map
```
├── docs
│   └── README.md
├── src
│   └── repo_mapper
│       ├── __init__.py
│       ├── __main__.py
│       ├── io.py
│       └── utils.py
├── tests
│   ├── __init__.py
│   ├── conftest.py
│   └── test_utils.py
├── pyproject.toml
└── ruff.toml
::
```