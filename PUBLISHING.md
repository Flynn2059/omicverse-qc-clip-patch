# Publishing Checklist

This machine does not currently have the GitHub CLI (`gh`) installed or a visible GitHub API token. Use one of the flows below to publish the prepared local repository.

## Repository Settings

- Name: `omicverse-qc-clip-patch`
- Visibility: public
- Description: `Display-only UMI and gene-count clipping for OmicVerse ov.pl.qc plots, implemented with Codex and tested against OmicVerse 2.2.4rc1.`
- Topics: `omicverse`, `single-cell`, `scrna-seq`, `quality-control`, `qc-plot`, `codex`, `bioinformatics`

## Browser Flow

1. Create a new public GitHub repository named `omicverse-qc-clip-patch`.
2. Do not initialize it with a README, license, or `.gitignore`; this local repo already has the initial files.
3. From this local repository, run:

```bash
cd /Users/flynn/omicverse-qc-clip-patch
git remote add origin git@github.com:Flynn2059/omicverse-qc-clip-patch.git
git push -u origin main
```

If you use HTTPS remotes instead of SSH:

```bash
cd /Users/flynn/omicverse-qc-clip-patch
git remote add origin https://github.com/Flynn2059/omicverse-qc-clip-patch.git
git push -u origin main
```

## GitHub CLI Flow

If `gh` is installed and authenticated later:

```bash
cd /Users/flynn/omicverse-qc-clip-patch
gh repo create omicverse-qc-clip-patch \
  --public \
  --description "Display-only UMI and gene-count clipping for OmicVerse ov.pl.qc plots, implemented with Codex and tested against OmicVerse 2.2.4rc1." \
  --source . \
  --remote origin \
  --push
```

Then add repository topics:

```bash
gh repo edit --add-topic omicverse --add-topic single-cell --add-topic scrna-seq --add-topic quality-control --add-topic qc-plot --add-topic codex --add-topic bioinformatics
```

## Issue Update

After publishing, post the prepared issue comment from `ISSUE_UPDATE.md` to:

```text
https://github.com/omicverse/omicverse/issues/808
```
