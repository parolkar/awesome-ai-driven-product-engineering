---
description: This is to generate stories as per https://github.com/parolkar/awesome-ai-driven-product-engineering/blob/main/PROMPTS/parolkar_user_story_prompt.md
---

# Workflow for Generating User Story 

## User Story Fundamentals
A **user story** is a short description of functionality from a user's perspective. It represents valuable, small functionality for agile planning and prioritization.

**Core Format:**
```
As a [user/persona],
I want [capability/feature],
so that [benefit/value].
```

**INVEST Model Checklist:**
- **I**ndependent: Stands alone without dependencies
- **N**egotiable: Not rigid; details can be discussed
- **V**aluable: Delivers clear user benefit
- **E**stimable: Team can size the effort
- **S**mall: Fits in single iteration
- **T**estable: Can be verified with clear criteria

## Acceptance Criteria
Use Gherkin syntax (Given/When/Then) to define testable conditions:

```
Scenario: [Descriptive title]
  Given [precondition/context]
  When [user action]
  Then [expected outcome]
```

**Example:**
```
As a mobile bank customer,
I want to see balance on my accounts,
So that I can make better informed decisions about my spending.

Scenario: Show balance after login
  Given I have logged into the mobile banking app
  When I navigate to the accounts page
  Then I should see the balance for each of my accounts
```

## Best Practices
1. **Focus on single feature** - One incremental improvement per story
2. **User-centered perspective** - Address real user needs
3. **Clear titles** - Include specific user/persona
4. **Include business rationale** - Always have a clear "so that"
5. **Define acceptance criteria** - Outcomes, not implementations
6. **Keep stories small** - Split if too complex
7. **Avoid technical details** - Focus on what, not how
8. **Add supporting materials** - Attach mockups or flow diagrams if helpful
9. **Use appropriate story type** - Features for user functionality, Bugs for defects, Chores for technical tasks

## Quick Checklist
- [ ] Clear persona identified
- [ ] Need and value clearly stated 
- [ ] Meets INVEST criteria
- [ ] Acceptance criteria in Given/When/Then format
- [ ] No implementation details specified
- [ ] Appropriately sized
- [ ] Edge cases considered
- [ ] Additional context provided if needed
- [ ] Correct story type used