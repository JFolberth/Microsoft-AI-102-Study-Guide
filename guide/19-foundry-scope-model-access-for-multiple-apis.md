[Previous](./18-import-export-azure-ai-language-projects.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./useful-links.md)

# 19. Foundry: Scope model access for multiple APIs

Scenario: multiple internal APIs/microservices call **the same deployed model** in Foundry, but you want to control access per API.

Recommended approach: **Microsoft Entra ID + RBAC**
- Give each API its own identity (managed identity, service principal, or app registration).
- Assign that identity a role that grants inference access at the **Foundry resource scope**.
- Use token-based auth in each API instead of distributing keys.

Key concept
- Azure distinguishes **administration (control plane)** actions (deployments, settings) from **developer/inference (data plane)** actions (calling inference APIs). Admin rights do *not* automatically grant inference rights.

Docs:
- Keyless auth with Microsoft Entra ID: https://learn.microsoft.com/azure/ai-foundry/foundry-models/how-to/configure-entra-id
- Foundry RBAC concepts: https://learn.microsoft.com/azure/ai-foundry/concepts/rbac-foundry

Practical scoping patterns
- **Per-API isolation:** separate identities + separate role assignments (revoke one API without impacting others).
- **Hard separation:** create separate model deployments (or separate Foundry resources/projects) when you need different policies/filters/quotas per API.
- **Gateway enforcement:** put Azure API Management in front of your internal APIs to enforce per-client subscription keys, quotas, or JWT validation, while APIM (or your API) calls Foundry using a managed identity.

---

[Previous](./18-import-export-azure-ai-language-projects.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./useful-links.md)

