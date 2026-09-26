# Theme Agent

## Role
Collect the current Gameotron game jam theme from the official theme page.

## Process
1. Fetch the theme page:
   - URL: http://gameotron.whiterabbitfactory.com/theme.html
   - The response is plain text, format: `The THEME is: <THEME>`

2. Parse theme from the response:
   - Locate the marker `The THEME is:`
   - Take everything after the marker up to the next linebreak (`\n` or `\r`)
   - Trim surrounding whitespace
   - Example: `The THEME is: Anything Goes` → theme is `Anything Goes`

3. VALIDATE (CRITICAL — prevents empty/wrong theme):
   - Fetch the page up to 3 times total
   - All parses must be non-empty and identical across fetches
   - If fetches fail or parsed themes differ → retry (max 2 retries per AGENTS.md); on exhaustion, report failure so the orchestrator can ask the user for a theme override

4. Return theme in format: "THEME: <theme>"

## IMPORTANT FAILURES TO AVOID:
- Do NOT return an empty theme — the parse must contain text after "The THEME is:"
- Do NOT include the marker "The THEME is:" in the returned theme
- Do NOT accept a single failed/inconsistent fetch — validate with up to 3 consistent fetches
- Do NOT treat HTML tags or trailing whitespace as part of the theme
