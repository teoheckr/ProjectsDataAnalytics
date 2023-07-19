# ProjectsDataAnalytics
--AMAZON CUSTOMER BEHAVIOUR SURVEY

--Data Extraction
--From Kaggle, it was dowloaded as an .exe and imported to SQL Server directly
--https://www.kaggle.com/datasets/swathiunnikrishnan/amazon-consumer-behaviour-dataset

--Taking a look through data
Select * From AmazonTable

--Data Cleaning & Transformation
--1.Get DATE from Timestramp, which has a DATETIME type:
SELECT CONVERT(DATE, Timestamp) AS DateAmazon
FROM AmazonTable;

--2.Delete register with age 3, since it must be a error and deleting one register will not be a significant change:
Delete From AmazonTable
Where Age = 3;

--3. Turning the empy registers to NULL in 'Product_Search_Method':
UPDATE amazontable
SET Product_Search_Method = NULL
WHERE Product_Search_Method = '';

--4.Change field 'Personalized_Recommendation_Frequency' to 'Personalized_Recommendation_Purchase':
Exec sp_rename 'amazontable.Personalized_Recommendation_Frequency', 'Personalized_Recommendation_Purchase', 'column';

--5.Turning the empy registers to NULL in 'Service_Appreciation':
UPDATE amazontable
SET Service_Appreciation = NULL
WHERE Service_Appreciation = '';

--6. Unify 'Improvement_Areas' in less categories:
UPDATE amazontable
SET improvement_areas = REPLACE(improvement_areas, '%interface%', 'UI')
WHERE improvement_areas LIKE '%interface%';

--Keep unifying categories in the same field:
UPDATE amazontable
SET improvement_areas = 
    CASE 
        WHEN improvement_areas = '%irrelevant%' THEN 'no problem'
        WHEN improvement_areas = 'nothing' THEN 'no problem'
        WHEN improvement_areas = 'nill' THEN 'no problem'
        WHEN improvement_areas = '%no problem%' THEN 'no problem'
        WHEN improvement_areas = '%any problem%' THEN 'no problem'
		WHEN improvement_areas = '%quality%' THEN 'quality'
	ELSE improvement_areas
	END
WHERE improvement_areas IN ('%irrelevant%', 'nothing', 'nill', '%no problem%', '%any problem%', '%quality%');
