## Description: <br>
Trigger an immediate run of one tracked prompt across ChatGPT, Claude and Perplexity for one of the user's b/cited projects, wait for the three engines to land, and show the results. Spends one run; capped at once per prompt per hour. Use only when the user explicitly asks to run, re-run or refresh a prompt now. Needs the b/cited account connection with the run permission. <br>

This skill is ready for commercial/non-commercial use. <br>

## Third-Party Community Consideration
This skill is not owned or developed by NVIDIA. This skill has been developed and built to a third-party's requirements for this application and use case; see link to Non-NVIDIA [b/cited Agent Card](https://bcited.ai/claude-skill). <br>

### License/Terms of Use: <br>
MIT <br>
## Use Case: <br>
b/cited account holders who explicitly ask to run, re-run or refresh one tracked prompt now across ChatGPT, Claude and Perplexity and see the results. <br>

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
**Output Format:** [Markdown summary of the three engine results] <br>
**Output Parameters:** [1D] <br>
**Other Properties Related to Output:** [Spends one run against the account's allowance; capped at once per prompt per hour] <br>

## Skill Version(s): <br>
1.2.7 (source: plugin.json) <br>


