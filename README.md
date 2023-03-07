# SQL- Bài tập level easy trên Datalemur
# Đề bài: Second Day Confirmation [TikTok SQL Interview Question]
New TikTok users sign up with their emails and each user receives a text confirmation to activate their account. Assume you are given the below tables about emails and texts.

Write a query to display the ids of the users who did not confirm on the first day of sign-up, but confirmed on the second day.

Assumption:
- action_date is the date when the user activated their account and confirmed their sign-up through the text.

emails **Table:**

|**Column name**|**Type**|
|---------------|--------|
|email_id|integer|
|user_id|integer|
|signup_date|datetime|

emails **Example Input:**

|**email_id**|**user_id**|**signup_date**|
|------------|-----------|---------------|
|125|7771|06/14/2022 00:00:00|
|433|1052|07/09/2022 00:00:00|

texts **Table:**

|**Column name**|**Type**|
|---------------|--------|
|text_id|integer|
|email_id|integer|
|signup_action|string ('Confirmed', 'Not confirmed')|
|action_date|datetime|

texts **Example Input:**

|**text_id**|**email_id**|**signup_action**|**action_date**|
|-|-|-|-|
|6878|125|Confirmed|06/14/2022 00:00:00|
|6997|433|Not Confirmed	|07/09/2022 00:00:00|
|7000|433|Confirmed|07/10/2022 00:00:00|

# Use Database of Datalemur.com
## My Solution:
```
SELECT user_id
FROM
  (
  SELECT user_id, signup_date, action_date, EXTRACT(day FROM (action_date - signup_date)) AS between_day
  FROM emails
  LEFT JOIN texts ON emails.email_id = texts.email_id
  ) AS new_table
WHERE between_day = 1;
```
## My Results
|**user_id**|
|-|
|1052|
|1235|
