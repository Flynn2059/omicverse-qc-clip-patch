# OmicVerse QC Plot Clipping

This repository documents a small OmicVerse plotting improvement I implemented using Codex: display-only clipping for high-outlier UMI/count and gene-count QC metrics in `ov.pl.qc`.

The feature was requested upstream in OmicVerse issue #808 and implemented locally against OmicVerse `master` / `2.2.4rc1`.

## What It Adds

`ov.pl.qc` now accepts two optional keyword arguments:

```python
ov.pl.qc(
    adata,
    umi_clip_at=50000,
    gene_clip_at=8000,
)
```

- `umi_clip_at` clips plotted values for `nUMIs` and `total_counts`
- `gene_clip_at` clips plotted values for `detected_genes` and `n_genes_by_counts`
- clipping is display-only and does not modify `adata.obs`
- both histogram and violin QC plots are supported
- grouped plots with `batch_key` are supported
- affected panels are labeled as clipped

## Why This Is Useful

Single-cell QC plots often contain a small number of extreme outliers. These outliers can compress the main distribution and make it difficult to choose practical filtering thresholds. Display-only clipping makes the plot easier to inspect while preserving the underlying QC values.

## Validation

The focused test suite passed locally:

```bash
conda run -n omicverse python -m pytest /Users/flynn/Downloads/omicverse/tests/pl/test_qc.py
```

Result:

```text
16 passed
```

The tests cover:

- figure creation
- preservation of `adata.obs`
- clipping behavior for UMI and gene-count panels
- unchanged mitochondrial percentage panels
- grouped histogram and violin plots
- Scanpy fallback metric names
- invalid clip argument validation

## Patch

See:

```text
patches/omicverse-qc-clipping.patch
```

Apply from the root of an OmicVerse checkout:

```bash
git apply patches/omicverse-qc-clipping.patch
```

If applying from this repository, pass the patch path explicitly from the OmicVerse checkout:

```bash
cd /path/to/omicverse
git apply /path/to/omicverse-qc-clip-patch/patches/omicverse-qc-clipping.patch
```

## Upstream Context

Original upstream issue:

```text
https://github.com/omicverse/omicverse/issues/808
```

This repository is intended to make the implementation easy to inspect, reproduce, and adapt for an upstream pull request.

## License Context

OmicVerse is licensed under GPLv3. The patch in this repository is intended for use with OmicVerse and should be treated as an OmicVerse-derived patch under the upstream project's license terms. The standalone documentation in this repository may be reused under MIT terms; see `LICENSE` for the full notice.
