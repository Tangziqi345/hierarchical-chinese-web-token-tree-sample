# Hierarchical Token Collection Sample

This repository contains an anonymous review sample for a hierarchical Chinese web-token dataset.

The full dataset contains 600K+ token-web-context-category-explanation records. During anonymous review, this repository releases 20 sampled reverse-substring tree collections to show the data format, tree organization, category labels, representative tokens, and generated category explanations. The full dataset is planned for release after acceptance.

## Files

- `open_release_collections.jsonl`: main machine-readable sample file. Each line is one tree collection.
- `open_release_collections_pretty.json`: same content as the JSONL file, formatted as a JSON array for easier inspection.
- `schema.md`: field definitions and interpretation notes.
- `manifest.json`: release-level metadata for this anonymous review sample.

## Sample Summary

- Collections: 20
- Tree direction: reverse substring trees
- Pure tree collections: 10
- Impure tree collections: 10
- Full-tree tokens in the sample: 2,126
- Tokens covered by representative-token explanations: 2,044
- Excluded non-majority tokens in impure trees: 82
- Covered target categories: adult content, online gambling, online video, online game, and abnormal/noisy text

## Data Format

The primary file is JSONL:

```text
open_release_collections.jsonl
```

Each line is a JSON object describing one sampled tree collection. A collection contains the full tree tokens, the subset of tokens covered by the selected representative reason, excluded tokens for impure trees, and one concise category explanation.

The pretty JSON file is provided only for human readability. For scripts and evaluation, use the JSONL file.

## Anonymity Notes

This release is prepared for anonymous peer review. It intentionally excludes raw API prompts/responses, local file paths, user names, identity metadata, and full unpublished dataset files.
