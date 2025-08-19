# Effective Prompting & Data Analysis

The quality of your input (the prompt) directly impacts the quality of Sia AI's output. Learning how to craft effective prompts and correct the AI when it makes mistakes is key to mastering the platform.

## Crafting Effective Prompts

Follow these best practices to get the most accurate results:

1.  **Be Specific:** Vague questions lead to vague answers.
    * **Bad:** `Show me sales.`
    * **Good:** `Show me total sales revenue by month for the year 2024.`

2.  **Use Correct Terminology:** Use the names of models, columns, and metrics as defined in the **Modeling Page**. If you've defined a metric called "Average Order Value," use that exact term.

3.  **Request a Chart Type:** You can guide the AI to the best visualization.
    * `Show monthly active users as a line chart.`
    * `What is the breakdown of sales by region? Show it as a pie chart.`

4.  **Build on a Conversation:** Use follow-up questions to drill down.
    * **Q1:** `What are our top 5 selling products this year?`
    * **Q2 (Follow-up):** `For those products, what was the monthly sales trend?`

## Correcting Mistakes with "Change SQL"

Even with perfect prompting, the AI can sometimes misunderstand your intent or generate an incorrect SQL query. The **Change SQL** feature gives you full control to correct it.

### Example Scenario: Detecting and Correcting an Error

Let's say you want to find the number of *distinct* users who made a purchase each month.

1.  **Your Prompt:** `Show me the number of users who made a purchase each month.`
2.  **AI's Interpretation:** The AI might misinterpret this and count the total number of *orders* instead of distinct users. The resulting chart shows unusually high numbers.
3.  **Detect the Mistake:** The numbers look wrong. You suspect the AI counted transactions instead of users.
4.  **Use "Change SQL":**
    * Above the chart, click the **Change SQL** button.
    * A modal will appear with the generated SQL query. You might see something like this:
    ```sql
    -- Incorrect Query
    SELECT
      DATE_TRUNC('month', order_date) AS month,
      COUNT(order_id) AS number_of_orders -- Mistake is here!
    FROM orders
    GROUP BY 1
    ORDER BY 1;
    ```
5.  **Update the SQL:** You can directly edit the query in the text box. You correct `COUNT(order_id)` to `COUNT(DISTINCT user_id)`.
    ```sql
    -- Corrected Query
    SELECT
      DATE_TRUNC('month', order_date) AS month,
      COUNT(DISTINCT user_id) AS number_of_distinct_users -- Corrected!
    FROM orders
    GROUP BY 1
    ORDER BY 1;
    ```
6.  **Apply Changes:** Click "Run Query." The chart will now update with the correct data based on your revised SQL.

### Improving Performance with Save Features

After correcting a query, you can teach Sia AI to avoid making the same mistake in the future.

#### Save to Knowledge
If the correction involves a specific business term, use **Save to Knowledge**.
-   **Scenario:** You prompted for "user growth," and the AI counted all new user signups. You used **Change SQL** to define it as *net* user growth (`new_signups - churned_users`).
-   **Action:** Click **Save to...** -> **Save to Knowledge**. Define the term "User Growth" and associate it with your corrected logic. The next time anyone asks for "user growth," Sia AI will use the correct definition.

#### Save to View
If the query is complex and likely to be reused often, save it as a **View**.
-   **Scenario:** You've crafted a multi-join query to generate a complex "Daily Operations Report."
-   **Action:** After finalizing the query with **Change SQL**, click **Save to...** -> **Save to View**. Name it "Daily Operations Report." Now, users can simply prompt `Show me the Daily Operations Report` instead of typing the complex question again.
