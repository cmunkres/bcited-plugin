## Description: <br>
Show the recent citation runs for one of the user's b/cited projects: for each engine, whether the brand was mentioned, cited, at what rank, which competitors were cited instead, and the citation list. Use when the user asks how ChatGPT, Claude or Perplexity cite their site, what a tracked prompt returned, or why they are not being cited. Needs the b/cited account connection. <br>

This skill is ready for commercial/non-commercial use. <br>

## Third-Party Community Consideration
This skill is not owned or developed by NVIDIA. This skill has been developed and built to a third-party's requirements for this application and use case; see link to Non-NVIDIA [b/cited Agent Card](https://bcited.ai/claude-skill). <br>

### License/Terms of Use: <br>
MIT <br>
## Use Case: <br>
b/cited account holders reviewing recent citation runs for one of their projects: per engine, whether the brand was mentioned or cited, its rank, competitors cited instead, and the citation list. <br>

### Deployment Geography for Use: <br>
Global <br>

## Requirements / Dependencies: <br>
**Requires API Key or External Credential:** [Yes] <br>
**Credential Type(s):** [OAuth Token] <br>  

Do not include secrets in prompts/logs/output; use least-privilege credentials; rotate keys as appropriate. See skill body for more details. <br>

## Known Risks and Mitigations: <br>
Risk: Review before execution as proposals could introduce incorrect or misleading guidance into skills. <br>
Mitigation: Review and scan skill before deployment. <br>

## Reference(s): <br>
- [b/cited Claude plugin documentation](https://bcited.ai/claude-skill) <br>
- [bcited-plugin source repository](https://github.com/cmunkres/bcited-plugin) <br>


## Skill Output: <br>
**Output Type(s):** [API Calls, Analysis] <br>
**Output Format:** [Markdown summary of recent runs per engine] <br>
**Output Parameters:** [1D] <br>
**Other Properties Related to Output:** [Reads the signed-in user's own project data only] <br>

## Skill Version(s): <br>
1.2.8 (source: plugin.json) <br>


