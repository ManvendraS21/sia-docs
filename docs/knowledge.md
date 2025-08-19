# The Knowledge Base: Teaching WrenAI Your Business Language

The Knowledge Base is a powerful feature that allows you to teach Sia AI the specific terminology, synonyms, and business logic unique to your organization. It acts as a centralized repository of contextual information that helps the AI better understand and respond to user prompts.

## Purpose of the Knowledge Base

Databases have technical names (`fct_transactions`, `dim_users`), but your team uses business terms ("revenue," "customers," "ARR"). The Knowledge Base bridges this gap.

Use it to define:

-   **Synonyms:** Map common terms to your data model.
    -   `customers` -> `users` model
    -   `revenue`, `sales`, `income` -> `total_price` column in the `orders` model
-   **Business Definitions:** Store definitions for complex metrics or concepts. When a user asks "What is ARR?", the AI can retrieve the definition you've stored.
-   **Common Filters:** Define frequently used filters.
    -   **Term:** `Active Users`
    -   **Mapping:** `users.last_login_date > DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY)`

## How to Add to the Knowledge Base

You can add entries to the Knowledge Base in two ways:

1.  **Directly on the Knowledge Page:**
    * Navigate to the "Knowledge" section from the main menu.
    * Click "Add New Entry."
    * Enter the term (e.g., "Churned Customer").
    * Provide its definition or map it to a specific model, column, or SQL expression.

2.  **From the Chat Interface (`Save to Knowledge`):**
    * This is the most common and effective workflow.
    * After the AI successfully generates a chart based on a complex prompt, you can save the underlying logic.
    * For example, you ask: `show me users who have not made a purchase in the last 6 months`.
    * After Sia AI generates the correct list, click **Save to...** -> **Save to Knowledge**.
    * You can then map the term "Churned Customer" to the logic WrenAI just used. The next time someone asks for "churned customers," the AI will know exactly what to do.

!!! note "The Knowledge Base is Proactive"
    Adding entries to the Knowledge Base is a proactive way to reduce errors and improve the accuracy of Sia AI for all users. Encourage your team to save common definitions and business logic whenever possible.
