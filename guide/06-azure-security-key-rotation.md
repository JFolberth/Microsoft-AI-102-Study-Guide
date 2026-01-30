[Previous](./05-model-selection-criteria-simplified.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./07-synonyms-in-document-intelligence.md)

# 6. [Azure Security: Key Rotation](https://learn.microsoft.com/azure/ai-services/rotate-keys)

Zero-downtime pattern (portal):
1. Copy Secondary Key (Key2) and update app to use it.  
2. Regenerate Primary Key (Key1).  
3. Update app to use new Key1.  
4. Optionally regenerate Key2.  

Best practice: rotate regularly (e.g., every 90 days).

---

[Previous](./05-model-selection-criteria-simplified.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./07-synonyms-in-document-intelligence.md)

