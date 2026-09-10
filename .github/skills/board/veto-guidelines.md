
# Skeptic's Veto Guidelines: Complexity vs. Value

To execute a Veto, the Skeptic must provide a clear, non-arbitrary justification based on the following criteria.

## 1. The Necessity Threshold

Is this feature or component a "must-have" or a "nice-to-have"?

- **Veto Trigger**: If the feature can be achieved through existing functionality without significant loss of utility, it is a **VETO**.
- **Justification**: "This functionality already exists in `module-x`; creating `module-y` introduces redundant logic."

## 2. The Placement (Nesting) Threshold

Does the addition increase the complexity of the filesystem organization?

- **Metric**: $\Delta \text{Nesting Depth}$.
- **Rule**: Any increase in folder/module nesting must be accompanied by a corresponding increase in "Surprising Value."
- **Veto Trigger**: If the proposed addition moves the project structure from level $N$ to $N+1$ without clearly justified complexity, it is a **VETO**.
- **Justification**: "Proposed change increases directory depth from 3 to 4 levels without adding significant autonomous capability."

## 3. The Depth (Complexity) Threshold

Does the implementation complexity outweigh the value provided?

- **Metric**: $\text{Surprising Value} = \frac{\text{Utility}}{\text{Complexity}}$.
- **Veto Trigger**: If the complexity (lines of code, new dependencies, new services) is disproportionate to the user utility, it is a **VETO**.
- **Justification**: "The implementation requires a new microservice for a task that can be handled by a simple helper function."

## Summary Table for Veto Decision

| Criterion | Check | Veto if... |
| :--- | :--- | :--- |
| **Necessity** | Is it redundant? | Yes $\rightarrow$ VETO |
| **Placement** | Does it increase nesting? | Yes (without high value) $\rightarrow$ VETO |
| **Depth** | Is it over-engineered? | Yes $\rightarrow$ VETO |
