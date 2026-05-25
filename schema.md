# Schema

The main data file is `data/open_release_collections.jsonl`. Each line is one JSON object representing a sampled reverse-substring tree collection.

## Top-Level Fields

| Field | Type | Description |
|---|---|---|
| `collection_id` | string | Stable sample identifier, e.g. `open_release_0001`. |
| `tree_id` | integer | Internal tree identifier used to connect this sample to the tree-construction output. |
| `tree_direction` | string | Tree construction direction. All released samples use `reverse`. |
| `collection_type` | string | Either `reverse_pure_tree` or `reverse_impure_tree_majority`. |
| `root_token` | string | Root token of the sampled reverse-substring tree. |
| `target_label` | string | Main category label assigned to the collection. |
| `is_pure_tree` | boolean | Whether all tokens in the full tree share the same label. |
| `labels_in_tree` | array[string] | All category labels observed in the full tree. |
| `token_counts` | object | Count summary for full, covered, and excluded tokens. |
| `full_tree_tokens` | array[string] | All tokens included in the sampled tree collection. |
| `reason_covered_tokens` | array[string] | Tokens covered by the selected representative token and explanation. |
| `excluded_tokens` | array[string] | Non-majority tokens excluded from representative-reason coverage for impure trees. Empty for pure trees. |
| `representative_token` | string | Token selected as the representative example for category explanation. |
| `classification_reason` | string | Concise explanation of why the representative token belongs to the target category. |

## `token_counts`

`token_counts` contains:

| Field | Type | Description |
|---|---|---|
| `full_tree` | integer | Number of tokens in `full_tree_tokens`. |
| `reason_covered` | integer | Number of tokens in `reason_covered_tokens`. |
| `excluded_non_majority` | integer | Number of tokens in `excluded_tokens`. |

For pure trees, `reason_covered` normally equals `full_tree`, and `excluded_non_majority` is `0`.

For impure trees, `full_tree_tokens` keeps the full sampled tree for transparency, while `reason_covered_tokens` contains the majority-label tokens used for representative-token explanation. Non-majority tokens are listed in `excluded_tokens`.

## Notes

- JSONL means one complete JSON object per line. It is the recommended format for programmatic loading.
- `open_release_collections_pretty.json` contains the same records as a formatted JSON array for manual inspection.
- Some token strings may contain a leading whitespace character. These are preserved because they reflect the original tokenizer output.

