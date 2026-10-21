---
name: biolib
description: Find and run bioinformatics apps on BioLib using the pybiolib Python package or the biolib CLI. Use when the user wants to run a BioLib app, find an app for a task, or work with BioLib results and data records.
---

# BioLib

## Setup

1. Run `biolib whoami`. If the `biolib` command is not found, install pybiolib with `pip install pybiolib` and run it again.
2. Read the `BioLib server:` line in the output. `https://biolib.com` is the public BioLib server; any other URL is an organization's Enterprise BioLib server.
3. If not logged in, run `PYTHONUNBUFFERED=1 biolib login` in the background. It prints a sign-in link; forward the link to the user so they can open it and authorize. The command waits until the user has authorized (up to about 5 minutes), then prints `Successfully signed in!`.
4. For an enterprise BioLib instance, set `BIOLIB_BASE_URL` to its URL.

## Find an app

List the available apps with a short description of each:

```python
import biolib
print(biolib.sdk.get_skill_index().list_as_markdown())
```

Or search by keyword:

```python
biolib.search('alignment')
```

## Get the app's instructions before using it

Always fetch the instructions for an app before writing code that calls it. They describe the app's inputs and contain an example:

```python
import biolib
app = biolib.load('<author>/<app>')
print(app.sdk.get_skill().get_markdown())
```

## Run an app

```python
import biolib
app = biolib.load('<author>/<app>')
result = app.cli(args=['--input', 'input.fasta'], check=True, stream_logs=True)
result.save_files('output/')
```

- Arguments that are paths to local files or directories are uploaded automatically.
- `check=True` raises an error if the job fails.
- Use `blocking=False` to start the job without waiting, then fetch it later with `biolib.get_job('<job-id>')`.

From the shell, the same app can be run with `biolib run <author>/<app> <args>`.

## Results and data records

- `biolib.fetch_jobs()` lists recent jobs, and `biolib.get_result('<result-id>')` loads one.
- On a result, `list_output_files()`, `get_output_file('<path>')`, `get_stdout()` and `save_files('<dir>')` read its output.
- `biolib.get_data_record('<uri>')` loads a data record. See `biolib data-record --help` for the CLI commands.
