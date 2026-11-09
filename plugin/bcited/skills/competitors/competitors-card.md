## Description: <br>
Show which competitor domains AI engines cited instead of the user's site on their tracked prompts, ranked by how often, for one b/cited project. Use when the user asks who is taking their citations, which competitors AI engines prefer, or who they are losing to in ChatGPT, Claude or Perplexity answers. Needs the b/cited account connection. <br>

This skill is ready for commercial/non-commercial use. <br>

## Third-Party Community Consideration
This skill is not owned or developed by NVIDIA. This skill has been developed and built to a third-party's requirements for this application and use case; see link to Non-NVIDIA [b/cited Agent Card](https://bcited.ai/claude-skill). <br>

### License/Terms of Use: <br>
MIT <br>
## Use Case: <br>
b/cited account holders who want to see which competitor domains AI engines cited instead of their site on their tracked prompts, ranked by frequency. <br>

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
**Output Format:** [Markdown ranked list of competitor domains] <br>
**Output Parameters:** [1D] <br>
**Other Properties Related to Output:** [Reads the signed-in user's own project data only] <br>

## Skill Version(s): <br>
1.2.7 (source: plugin.json) <br>


