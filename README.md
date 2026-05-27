# Hierarchical Chinese Web-Token Tree Sample

This repository contains an anonymous-review sample for a hierarchical Chinese web-token dataset.

The full dataset described in the paper contains 630,684 token records organized into 92,972 hierarchical token trees. For anonymous review, this repository releases 20 sampled token trees to show the data format, tree structure, category labels, representative tokens, and classification explanations. This sample is not the full dataset and should not be used to estimate the category distribution of the full dataset.

## Files

- `hierarchical_chinese_web_token_tree_sample.jsonl`: main data file. Each line is one sampled hierarchical token tree.
- `tree_structure_visualization.ipynb`: Jupyter notebook for loading the JSONL file and visualizing the token-tree structure.
- `README.md`: this documentation file.

## Data Format

The primary file is:

```text
hierarchical_chinese_web_token_tree_sample.jsonl
```

Each line is a JSON object describing one sampled token tree. The main fields are:

- `collection_id`: anonymized sample collection identifier.
- `tree_id`: internal tree identifier for distinguishing sampled trees.
- `collection_type`: type of sampled tree collection.
- `root`: root token and its category label.
- `target_label`: target category label for the tree, written in English.
- `is_pure_tree`: whether all nodes in the tree belong to the target category.
- `labels_in_tree`: category labels that appear in the tree.
- `token_counts`: token-count statistics for the sampled tree.
- `composition`: optional field for composition-token cases.
- `hierarchical_tree`: recursive tree structure.
- `representative_token`: representative token for the sampled tree.
- `classification_reason`: English explanation for the category assignment.

## Hierarchical Tree Structure

The `hierarchical_tree` field is recursive. Each node contains:

- `token`: token string.
- `label`: English category label for the token.
- `depth`: node depth in the tree.
- `reason_covered`: whether the node is covered by the representative explanation.
- `children`: child nodes.

The data is therefore represented as a tree through nested `children` fields, rather than as a flat list of tokens.

## Composition Cases

Some sampled trees include a `composition` field for cases where normal component tokens compose into a polluted token family. 
- `菲律宾` + `申博` -> `菲律宾申博`: `菲律宾` means Philippines and `申博` can mean applying for a PhD; separately they can be normal tokens, but their combination is associated with an online gambling brand. Its descendants include agent, official-site, login, and international-casino variants.

## Visualization

Use the notebook below to inspect the tree structures:

```text
tree_structure_visualization.ipynb
```

Place the notebook and JSONL file in the same directory, open the notebook in VS Code, Jupyter Notebook, or JupyterLab, and run all cells. To inspect a specific tree, use:

```python
display_tree(11366, max_depth=4)
```

The first argument can be a `tree_id`, `collection_id`, or root token. To expand the full tree, use:

```python
display_tree(11366, max_depth=None)
```

## Anonymity Notes

This repository is prepared for anonymous peer review. It excludes raw prompts or responses, local file paths, user names, identity metadata, and full unpublished dataset files. The full dataset is planned for release after acceptance.
