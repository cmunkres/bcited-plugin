## Description: <br>
Run a live Answer Engine Optimization (AEO) and SEO readiness audit on a public URL using b/cited's rule-based scanner. Returns an A–F grade, a 9-category breakdown, and a prioritized fix list. Use when the user gives a URL and wants to know whether AI engines (ChatGPT, Claude, Perplexity) can cite it, or asks for an AEO, SEO, or site readiness audit. <br>

This skill is ready for commercial/non-commercial use. <br>

## Third-Party Community Consideration
This skill is not owned or developed by NVIDIA. This skill has been developed and built to a third-party's requirements for this application and use case; see link to Non-NVIDIA [b/cited Agent Card](https://bcited.ai/claude-skill). <br>

### License/Terms of Use: <br>
MIT <br>
## Use Case: <br>
Developers, site owners and marketers who give the skill a public URL to get a graded Answer Engine Optimization (AEO) and SEO readiness audit with a prioritized fix list. <br>

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
- [api-response.md](references/api-response.md) <br>
- [b/cited Claude plugin documentation](https://bcited.ai/claude-skill) <br>
- [bcited-plugin source repository](https://github.com/cmunkres/bcited-plugin) <br>


## Skill Output: <br>
**Output Type(s):** [Analysis, API Calls] <br>
**Output Format:** [Markdown report (grade, 9-category breakdown, fix list) built from the scan JSON returned by the b/cited MCP server] <br>
**Output Parameters:** [1D] <br>
**Other Properties Related to Output:** [Scan text echoed from the audited site is rendered as quoted data and never followed as instructions] <br>

## Skill Version(s): <br>
1.2.8 (source: plugin.json) <br>


