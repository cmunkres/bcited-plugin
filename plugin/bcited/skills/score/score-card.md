## Description: <br>
Show the AEO Visibility Score for one of the user's b/cited projects over 7, 30 or 90 days: runs, mention rate, citation rate, mean brand rank, and the per-engine split across ChatGPT, Claude and Perplexity. Use when the user asks how visible their site is to AI engines, for their score, or how it differs by engine. Needs the b/cited account connection. <br>

This skill is ready for commercial/non-commercial use. <br>

## Third-Party Community Consideration
This skill is not owned or developed by NVIDIA. This skill has been developed and built to a third-party's requirements for this application and use case; see link to Non-NVIDIA [b/cited Agent Card](https://bcited.ai/claude-skill). <br>

### License/Terms of Use: <br>
MIT <br>
## Use Case: <br>
b/cited account holders checking the AEO Visibility Score for one of their own projects over 7, 30 or 90 days, with the per-engine split across ChatGPT, Claude and Perplexity. <br>

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
**Output Format:** [Markdown summary of runs, mention rate, citation rate and mean brand rank] <br>
**Output Parameters:** [1D] <br>
**Other Properties Related to Output:** [Reads the signed-in user's own project data only] <br>

## Skill Version(s): <br>
1.2.8 (source: plugin.json) <br>


