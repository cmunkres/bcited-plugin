## Description: <br>
Review a page's HTML or a component file for Answer Engine Optimization (AEO) gaps and produce a concrete patch list with exact code: llms.txt, ai.txt, robots.txt AI crawler stanzas, FAQPage/HowTo/Article/Person JSON-LD, author bylines, dateModified. Use when the user pastes HTML, names a page or component file, or asks how to make a page citable by AI engines. <br>

This skill is ready for commercial/non-commercial use. <br>

## Third-Party Community Consideration
This skill is not owned or developed by NVIDIA. This skill has been developed and built to a third-party's requirements for this application and use case; see link to Non-NVIDIA [b/cited Agent Card](https://bcited.ai/claude-skill). <br>

### License/Terms of Use: <br>
MIT <br>
## Use Case: <br>
Developers and content teams who paste page HTML or name a component file and want a concrete AEO patch list with exact code (llms.txt, ai.txt, robots.txt stanzas, JSON-LD, bylines, dateModified). <br>

### Deployment Geography for Use: <br>
Global <br>

## Requirements / Dependencies: <br>
**Requires API Key or External Credential:** [No] <br>
**Credential Type(s):** [None] <br>  

Do not include secrets in prompts/logs/output; use least-privilege credentials; rotate keys as appropriate. See skill body for more details. <br>

## Known Risks and Mitigations: <br>
Risk: Review before execution as proposals could introduce incorrect or misleading guidance into skills. <br>
Mitigation: Review and scan skill before deployment. <br>

## Reference(s): <br>
- [aeo-signals.md](references/aeo-signals.md) <br>
- [b/cited Claude plugin documentation](https://bcited.ai/claude-skill) <br>
- [bcited-plugin source repository](https://github.com/cmunkres/bcited-plugin) <br>


## Skill Output: <br>
**Output Type(s):** [Analysis, Code] <br>
**Output Format:** [Markdown patch list with code blocks] <br>
**Output Parameters:** [1D] <br>
**Other Properties Related to Output:** [Proposes edits only; the user applies them] <br>

## Skill Version(s): <br>
1.2.7 (source: plugin.json) <br>


