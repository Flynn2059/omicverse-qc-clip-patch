# Issue Update Draft

Post this as a comment on:

```text
https://github.com/omicverse/omicverse/issues/808
```

```markdown
Update: I have implemented this feature myself using Codex.

The requested `ov.pl.qc` display-only clipping support is now working locally on the latest OmicVerse `master` / `2.2.4rc1`. The implementation adds:

- `umi_clip_at` for UMI/count metrics: `nUMIs` and `total_counts`
- `gene_clip_at` for gene-count metrics: `detected_genes` and `n_genes_by_counts`
- display-only upper clipping for both histogram and violin QC plots
- support for grouped plots via `batch_key`
- validation for invalid clip values
- labels indicating when a panel is clipped
- focused tests confirming that `adata.obs` is not modified

Example:

```python
ov.pl.qc(adata, umi_clip_at=50000, gene_clip_at=8000)
```

I added this because this request has been open for about 15 days and I needed the feature for actual QC visualization work. To be direct: I am disappointed with the speed of response here, especially for a relatively small but practical plotting improvement. I appreciate the OmicVerse project, but this kind of usability issue should not require users to implement and test the feature themselves after waiting this long.

Local validation passed:

```bash
conda run -n omicverse python -m pytest /Users/flynn/Downloads/omicverse/tests/pl/test_qc.py
```

Result:

```text
16 passed
```

I have published a small public repository with the patch summary and usage notes so the change is easy to review or reproduce:

https://github.com/Flynn2059/omicverse-qc-clip-patch
```
