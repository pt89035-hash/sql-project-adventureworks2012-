# sql-project-adventureworks2012-


use AdventureWorks2012


-- Perform the following with help of the above database:--


A. To view table name and details 

->  SELECT TABLE_SCHEMA, TABLE_NAME
    FROM INFORMATION_SCHEMA.TABLES
    WHERE TABLE_TYPE = 'BASE TABLE'
    ORDER BY TABLE_SCHEMA



B. Get all the details from the person table including email ID, phonenumber and phone number type

->  SELECT 
        p.BusinessEntityID,
        e.EmailAddress,
        ph.PhoneNumber,
        pnt.Name AS PhoneNumberType
    FROM Person.Person AS p
    LEFT JOIN Person.EmailAddress AS e 
        ON p.BusinessEntityID = e.BusinessEntityID
    LEFT JOIN Person.PersonPhone AS ph 
        ON p.BusinessEntityID = ph.BusinessEntityID
    LEFT JOIN Person.PhoneNumberType AS pnt 
        ON ph.PhoneNumberTypeID = pnt.PhoneNumberTypeID
    ORDER BY p.BusinessEntityID;



C. Get the details of the sales header order made in May 2011

->  SELECT * 
    FROM Sales.SalesOrderHeader AS May2011
    WHERE YEAR(OrderDate) = 2011 AND MONTH(OrderDate) = 5;



D. Get the details of the sales details order made in the month of May 2011

->  SELECT SUM(ORDERQTY)
    FROM Sales.SalesOrderHeader AS soh
    INNER JOIN Sales.SalesOrderDetail AS sod
        ON soh.SalesOrderID = sod.SalesOrderID
    WHERE YEAR(soh.OrderDate) = 2011 AND MONTH(soh.OrderDate) = 5;



E. Get the total sales made in the year 2011 by month order by increasing sales

->  SELECT * FROM SALES.SALESORDERHEADER
    SELECT * FROM SALES.SALESORDERDETAIL

  SELECT SOD.SALESORDERID, SOH.SUBTOTAL FROM SALES.SALESORDERHEADER AS SOH
  INNER JOIN SALES.SALESORDERDETAIL AS SOD 
  ON soh.SalesOrderID = sod.SalesOrderID 
  WHERE YEAR(SOH.ORDERDATE) = 2011
  ORDER BY SOH.SUBTOTAL ASC





F. Get the total sales made to the customer with FirstName='Gustavo'and LastName ='Achong'

->  SELECT 
    PP.FIRSTNAME ,
    PP.LASTNAME,
    SUM(SP.SalesLastYear)
    FROM 
    PERSON.PERSON AS PP
    LEFT JOIN  SALES.SALESPERSON AS SP
    ON PP.BusinessEntityID = SP.BusinessEntityID
    WHERE PP.FIRSTNAME = 'GUSTAVO' 
    AND PP.LASTNAME = 'ACHONG'
    GROUP BY PP.FIRSTNAME , PP.LASTNAME


