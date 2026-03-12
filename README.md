# sql_business_exploration
sql business analysis
## Description
### Analysis
*Business*
**SQL**


# 📊 SQL Business Analysis: Insights & Revenue Optimization

[![SQL](https://img.shields.io/badge/Language-SQL-blue.svg)](https://en.wikipedia.org/wiki/SQL)
[![Database](https://img.shields.io/badge/Database-PostgreSQL-336791.svg)](https://www.postgresql.org/)
[![Status](https://img.shields.io/badge/Status-Completed-success.svg)]()

## 📝 Projektbeschreibung
Dieses Repository enthält eine umfassende Business-Intelligence-Analyse basierend auf relationalen Datenbanken. Das Ziel ist es, Rohdaten in strategische Entscheidungen zu verwandeln. Ich analysiere hierbei Verkaufszahlen, Kundenverhalten und Produktperformance, um Wachstumspotenziale aufzudecken.

---

## 🧐 Geschäftsfragen (Key Business Questions)
Um den Erfolg des Unternehmens zu bewerten, beantwortet dieses Projekt folgende Fragen:
1. **Umsatzdynamik:** Wie entwickelt sich der monatliche Umsatz und wie hoch ist die Wachstumsrate ($MoM$)?
2. **Kundenbindung:** Welche Kunden gehören zum Top-Segment (RFM-Analyse)?
3. **Produkt-Mix:** Welche Produktkategorien haben die höchste Retourenquote oder die beste Marge?
4. **Kohorten-Analyse:** Wie lange bleiben Kunden nach ihrem ersten Kauf aktiv?

---

## 🛠️ Tech Stack & Konzepte
* **SQL Dialekt:** PostgreSQL (kompatibel mit MySQL/BigQuery)
* **Fortgeschrittene Techniken:**
    * **CTEs (Common Table Expressions)** für saubere Abfragestruktur.
    * **Window Functions** (`RANK`, `LEAD/LAG`, `PARTITION BY`) für Trendanalysen.
    * **Joins & Aggregationen** zur Konsolidierung komplexer Datenschemata.
    * **Subqueries** für geschachtelte Datenvalidierung.

---

## 📂 Datenbank-Schema
Die Analyse basiert auf einem klassischen E-Commerce-Schema:



---

## 🚀 Beispiel-Abfrage: Monthly Revenue Growth
Um den Trend der Geschäftsführung zu präsentieren, nutze ich Window Functions:

```sql
WITH MonthlySales AS (
    SELECT 
        DATE_TRUNC('month', order_date) AS month,
        SUM(total_price) AS current_revenue
    FROM orders
    GROUP BY 1
)
SELECT 
    month,
    current_revenue,
    LAG(current_revenue) OVER (ORDER BY month) AS previous_revenue,
    ROUND(((current_revenue - LAG(current_revenue) OVER (ORDER BY month)) 
           / LAG(current_revenue) OVER (ORDER BY month) * 100), 2) || '%' AS growth_percentage
FROM MonthlySales;
