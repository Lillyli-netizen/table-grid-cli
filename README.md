# Table Grid

Turn HTML tables with merged cells into CSV or JSON, using only Python's standard library. Useful when table HTML comes from a web export, a report, or an OCR pipeline and the next step expects a regular grid.

**[Quickstart](#quickstart)** · **[See the examples](#examples)** · **[Run the browser demo](#browser-demo)**

| Model | Validation | Validation |
| --- | --- | --- |
| Model | Precision | Recall |
| Baseline | 0.82 | 0.76 |
| Revision A | 0.88 | 0.84 |

In the source HTML, “Model” spans two rows and “Validation” spans two columns. The default CSV output repeats those labels to keep their association with each row or column. Use `--fill blank` to leave the covered cells empty, or `--format json` for a grid plus the original cell positions and effective spans.

## Quickstart

Requires Python 3.8 or later. Clone the repository, then run the first example.

```sh
git clone https://github.com/Lillyli-netizen/table-grid-cli.git
cd table-grid-cli
python3 table_grid.py examples/experiment.html
```

Pass `--table 2` to select the second top-level table, `-o grid.csv` to write to a file, or `-` to read UTF-8 HTML from standard input. Use `python` in place of `python3` if that is your Python command.

## Examples

| Input | Options | Expected output |
| --- | --- | --- |
| [Two-level header](examples/experiment.html) | Defaults | [CSV](examples/experiment.csv) |
| [Lab inventory](examples/inventory.html) | `--fill blank --format json` | [JSON](examples/inventory.json) |

JSON cell coordinates are zero-indexed. Cells with `rowspan="0"` extend to the end of their row group. Table selection uses source order and skips nested tables. The tool reads UTF-8 HTML table markup. PDFs, images, and tables rendered only by JavaScript need an upstream extraction step.

## Browser demo

From the cloned directory, run `python3 -m http.server 8000` and open [http://localhost:8000](http://localhost:8000). You can load either example or paste your own table. Conversion runs in the browser.

If Table Grid is useful to you, a GitHub Star helps other people find it. For unexpected output, please share a small, non-sensitive HTML example and the grid you expected in an issue.
