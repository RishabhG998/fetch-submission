# Fetch-submission
This repo contains the answers to the submission for the Data Analytics Internship at Fetch.

---

### Review Existing Data and Diagram a New Structured Relational Data Model
![ER Diagram](ER%20Diagram.png "ER Diagram")

---

### Write a query that directly answers question(s) from a business stakeholder
- Which brand saw the most dollars spent in the month of June?
```
SELECT RI.BRAND_CODE
FROM RECEIPT_ITEMS RI LEFT JOIN RECEIPTS R ON RI.REWARDS_RECEIPT_ID = R.ID
WHERE MONTH(R.PURCHASE_DATE) = 6
GROUP BY RI.BRAND_CODE
ORDER BY SUM(RI.TOTAL_FINAL_PRICE) DESC
LIMIT 1;
```

- Which user spent the most money in the month of August?
```
SELECT USER_ID
FROM RECEIPTS
WHERE PURCHASE_DATE BETWEEN ‘2022-08-01’ AND ‘2022-08-31’
GROUP BY USER_ID
ORDER BY SUM(TOTAL_SPENT) DESC
LIMIT 1;
```

- What user bought the most expensive item?
```
SELECT USER_ID
FROM RECEIPTS
WHERE ID = 
	(SELECT REWARDS_RECEIPT_ID AS ID 
	FROM RECEIPT_ITEMS
	WHERE ((TOTAL_FINAL_PRICE)/(QUANTITY_PURCHASED)) = (SELECT MAX((TOTAL_FINAL_PRICE)/(QUANTITY_PURCHASED)) FROM RECEIPT_ITEMS));
```

- What is the name of the most expensive item purchased?
```
SELECT DESCRIPTION
FROM RECEIPT_ITEMS
WHERE ((TOTAL_FINAL_PRICE)/(QUANTITY_PURCHASED)) = (SELECT MAX((TOTAL_FINAL_PRICE)/(QUANTITY_PURCHASED)) FROM RECEIPT_ITEMS));
```

- How many users scanned in each month?
```
SELECT MONTH(DATE_SCANNED) AS MONTH, COUNT(USER_ID) AS USER_COUNT
FROM RECEIPTS
GROUP BY MONTH(DATE_SCANNED) 
ORDER BY MONTH(DATE_SCANNED) ASC;
```

---

### Choose something noteworthy about the data and share with a non-technical stakeholder
1. Target users (with advertisements) on those platforms from which most of the customers log in. The most common platform can be found easily using an SQL query.
2. Data inconsistency in tables such as `receipt_items` in columns like `BRAND_CODE`, this might lead to incorrect and poor results when use this column.
3. Users with highest reward points can be given extra benefits (discounts).
4. Which products experience an increase in demand during festive season, this may help in logistics and supply chain planning in advance.
5. List of top n states that generate the highest revenue for the company, a similar analysis can be done for categories. 


