# RdbmsBillionaireDS
Description of dataset
The dataset provides information about various billionaires including their net worth, industry
affiliation, age, country, city, source of wealth, industries involved, organization (if applicable),
gender, birth date, last name, first name, title, and state.
Here's a breakdown of each column:
1. Net Worth: The amount of wealth the individual possesses, typically measured in billions of
dollars.
2. Category: The sector or industry in which the billionaire made their fortune.
3. Age: The age of the billionaire.
4. Country: The country in which the billionaire resides.
5. City: The city in which the billionaire resides.
6. Source of Worth: The primary source of the billionaire's wealth.
7. Industries: Specific industries related to the source of wealth.
8. Organization: The organization or company associated with the billionaire.
9. Gender: The gender of the billionaire.
10. Birth Date: The birth date of the billionaire.
11. Last Name: The last name of the billionaire.
12. First Name: The first name of the billionaire.
13. Title: Any title or position associated with the billionaire.
14. State: The state within the country where the billionaire resides.

    
This dataset seems to focus on billionaires primarily in the United States, providing detailed
information about their wealth, background, and industry involvement. It could be useful for
analysis related to wealth distribution, industry trends, demographic patterns among
billionaires, and more.


Problems faced with dataset-
I have experienced difficulty in the above dataset is that there are no unique columns that can
be used for fact table data. For if we see max unique data is in birthdate which is almost
around 498 only. Now to overcome that issue, I have created a new BillionaireID by First name
and last name first character "-" and birth date. For example first name is Jimmy and the Last
name is Rane. BirthDate is 9/15/46. BillionaireId is JR-091546.
Later in the title, there are empty cells were there. So I have kept NA for empty cells.
Lesson Learnt-
One crucial lesson learned from working with this dataset is the significance of establishing
unique identifiers for data integration and analysis(fact table). In this case, encountering
difficulty in identifying a suitable unique column highlighted the importance of careful dataset
preparation and consideration for subsequent analysis.
And carefully analysis for missing dataset is also important to maximize our dataset either by
relacing with null value or by discarding that row.

Output-

Query 1-
SELECT [Facts Table].BillionaireID, [Source Dimension Table].Industries FROM [Facts Table]
INNER JOIN [Source Dimension Table] ON [Facts Table].SourceKey = [Source Dimension
Table].SourceKey;
The result of this query will be a dataset containing the BillionaireID and the corresponding
Industries associated with each billionaire. It effectively merges the information about
billionaires' unique identifiers (BillionaireID) with the industries in which they have made their
fortunes, leveraging the relationship established through the "SourceKey" column.


Query 2-
SELECT [Facts Table].BillionaireID, [Source Dimension Table].Industries, [Date Dimentsion
Table].Quarter FROM ([Facts Table] INNER JOIN [Source Dimension Table] ON [Facts
Table].SourceKey = [Source Dimension Table].SourceKey) INNER JOIN [Date Dimentsion Table]
ON [Facts Table].DateKey = [Date Dimentsion Table].DateKey;
The query selects three columns: "BillionaireID" from the "Facts Table", "Industries" from the
"Source Dimension Table", and "Quarter" from the "Date Dimension Table". The SQL query
effectively retrieves a comprehensive dataset combining information about billionaires, their
associated industries, and temporal data represented by quarters. By joining the "Facts Table"
with the "Source Dimension Table" and subsequently with the "Date Dimension Table", the
query creates a cohesive dataset that enables analysis across multiple dimensions.


Query 3-
SELECT [Facts Table].BillionaireID, [Date Dimentsion Table].Quarter, [Source Dimension
Table].Industries, [Billionaire Dimension table].firstName, [Billionaire Dimension table].title
FROM ([Date Dimentsion Table] INNER JOIN ([Billionaire Dimension table] INNER JOIN [Facts
Table] ON [Billionaire Dimension table].BillionaireID = [Facts Table].BillionaireID) ON [Date
Dimentsion Table].DateKey = [Facts Table].DateKey) INNER JOIN [Source Dimension Table] ON
[Facts Table].SourceKey = [Source Dimension Table].SourceKey;
The query selects specific columns from each table: "BillionaireID" from the "Facts Table",
"Quarter" from the "Date Dimension Table", "Industries" from the "Source Dimension Table",
"firstName", and "title" from the "Billionaire Dimension table". The query outputs the selected
columns, providing information about the billionaire's unique identifier ("BillionaireID"), the
quarter associated with the data, the industries related to the billionaire's wealth, the
billionaire's first name, and their title.


Query 4-
SELECT [Facts Table].BillionaireID, [Billionaire Dimension table].firstName, [Billionaire
Dimension table].lastName, [Billionaire Dimension table].gender, [Date Dimentsion
Table].Month, [Date Dimentsion Table].WeekendOrWeekday, [Source Dimension
Table].Industries, [Source Dimension Table].[source of worth] FROM ([Date Dimentsion Table]
INNER JOIN ([Billionaire Dimension table] INNER JOIN [Facts Table] ON [Billionaire Dimension
table].BillionaireID = [Facts Table].BillionaireID) ON [Date Dimentsion Table].DateKey = [Facts
Table].DateKey) INNER JOIN [Source Dimension Table] ON [Facts Table].SourceKey = [Source
Dimension Table].SourceKey ORDER BY [Date Dimentsion Table].Month;
This SQL query selects billionaire data including their identifiers, name, gender, birth month,
weekend or weekday birth status, industry affiliations, and source of wealth. It's drawn from
four tables: "Facts Table", "Billionaire Dimension Table", "Date Dimension Table", and "Source
Dimension Table". The "WeekendOrWeekday" column likely derives from the "Date Dimension
Table", indicating the birth's occurrence on a weekend or weekday. Results are ordered by birth
month.


Query 5-
SELECT [Facts Table].BillionaireID, [Date Dimentsion Table].birthDate, [Source Dimension
Table].[source of worth], [Source Dimension Table].Industries, [Billionaire Dimension
table].gender, [Billionaire Dimension table].lastName, [Billionaire Dimension table].firstName,
[Billionaire Dimension table].title FROM (([Facts Table] INNER JOIN [Billionaire Dimension table]
ON [Facts Table].BillionaireKey = [Billionaire Dimension table].BillionaireKey) INNER JOIN [Date
Dimentsion Table] ON [Facts Table].DateKey = [Date Dimentsion Table].DateKey) INNER JOIN
[Source Dimension Table] ON [Facts Table].SourceKey = [Source Dimension Table].SourceKey
ORDER BY [Source Dimension Table].[source of worth] DESC;



This SQL query retrieves data from four tables: "Facts Table", "Billionaire Dimension Table",
"Date Dimension Table", and "Source Dimension Table". It selects information such as
BillionaireID, birthDate, source of worth, industries, gender, last name, first name, and title. The
tables are joined based on their respective keys, including BillionaireKey, DateKey, and
SourceKey. The query orders the results by the source of worth in descending order.
