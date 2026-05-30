# html-report <img src="./assets/icon.png" width="40" alt="html-report icon">

**Generates and opens a saved HTML report as a response format.**

**Exports the document into the workspace, then opens it in a browser.**

## Note

*This skill is configured to use `Brave` browser on `macOS` by default.*

## How to use

1. **Edit skill** to use your browser of choice.
2. Type `$html-report <request>` or use `$html-report recap` / `$html-report recap+`.
3. Follow the HTML export flow for the selected mode.

### Examples

- `$html-report Show me the performance of the latest simulation.`

- `$html-report recap`
  - Generates an HTML report of the **LAST** assistant reply in thread using only content source.
  
- `$html-report recap+`
  - Generates an HTML report from the last assistant reply along with any high value context already present in thread when it clearly improves the doc.

## Version

Current version: v1.1.1

## Install

`npx skills@latest add CratesSo/skills/html-report`
