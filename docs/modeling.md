# The Modeling Page: Defining Your Data's Logic

The Modeling Page is where you build the semantic layer that Sia AI uses to understand your database schema. By defining models, relationships, and custom fields, you provide the essential context the AI needs to write accurate SQL queries.

## What is Modeling?

In the context of Sia AI, "modeling" is the process of mapping your raw database tables and columns to business-friendly concepts. It's about adding a layer of meaning on top of your data.

A well-defined model allows users to ask questions using business terms (e.g., "revenue," "customers") instead of database terms (e.g., `sum(order_items.sale_price)`, `count(distinct users.id)`).

## Key Modeling Concepts

The Modeling Page allows you to configure the following:

-   **Models:** A model is typically a direct mapping to a table or view in your database. You can select which tables to expose to Sia AI.
-   **Columns:** Within each model, you can manage its columns. You can rename them for clarity, hide them from the AI, or change their data type.
-   **Relationships:** This is where you define how models connect to each other. For example, you would define a `many-to-one` relationship from an `orders` model to a `users` model on the `user_id` column.
    -   `orders.user_id` -> `users.id`
-   **Calculated Fields:** Create new columns using SQL expressions. This is perfect for defining custom metrics that don't exist in the database.
    -   **Example:** Create a `profit` column in your `orders` model with the expression `sale_price - cost`.
-   **Custom Metrics:** Define aggregations that are frequently used.
    -   **Example:** Create a metric called `Average Order Value (AOV)` with the expression `AVG(total_price)`.

## How to Interact with the Modeling Page

1.  **Connect Your Data Source:** The first step is to connect Sia AI to your data warehouse or database.
2.  **Select Tables to Model:** From the list of available tables, select the ones you want to expose to the AI. Sia AI will create a default model for each selected table.
3.  **Define Relationships:** Navigate to the "Relationships" tab. Click "Add Relationship" and define the connections between your models (e.g., join `orders` and `products` on `product_id`).
4.  **Create Calculated Fields/Metrics:** Go to a specific model and click "Add Calculated Field." Provide a user-friendly name and the SQL expression.

!!! warning "Accurate Relationships are Critical"
    The AI relies heavily on the defined relationships to correctly join tables. An incorrect or missing relationship is the most common cause of failed queries. Ensure your join keys and cardinality (`one-to-one`, `many-to-one`, etc.) are accurate.
