1 - Order Quantity = SUM('Sales Data'[OrderQuantity])


2 - Quantitty Returned = SUM('Returns Data'[ReturnQuantity]) 


3 - Average Retail Price = AVERAGE('Product Lookup'[ProductPrice])


4 - Total Return = COUNT('Returns Data'[ReturnQuantity])


5 - Total Orders = DISTINCTCOUNT('Sales Data'[OrderNumber])


6 - Quantitty Sold  = SUM('Sales Data'[OrderQuantity])

----------------------------------------------------------------------------

6  - Parent = IF('Customer Lookup (2)'[TotalChildren] > 0 , "YES" , "NO")

7 -   (Dax) = 
IF(
    'Calendar Lookup'[Month Name] = "January" , "1",
     IF
        (
            'Calendar Lookup'[Month Name] = "February" , "2" ,
            IF
                (
                   'Calendar Lookup'[Month Name] = "March" , "3" ,
                    "other"
                )
        

        )
    
)

8 - Month switch = 
SWITCH(
    'Calendar Lookup'[Month Name], 
    "January", "1",
    "February", "2",
    "March", "3",
    "April", "4",
    "May", "5",
    "June", "6",
    "July", "7",
    "August", "8",
    "September", "9",
    "October", "10",
    "November", "11",
    "December", "12",
    "Other", "0"  -- Default value if no match
)


9 - Price Point = 
SWITCH
(
    TRUE(),
    'Product Lookup'[ProductPrice] > 500 ,"High",
    'Product Lookup'[ProductPrice] > 100 , "Mid - Range",
    "Low"
)


10 -  customar Full Name (cc) = 'Customer Lookup (2)'[Prefix] & " " & 'Customer Lookup (2)'[FirstName] & " " & 'Customer Lookup (2)'[LastName]


11 -  Month short = 
 LEFT
 (
    'Calendar Lookup'[Month Name],
    3)


11 - 2 - 11 -  Month short = 
   UPPER(
    LEFT
    (
    'Calendar Lookup'[Month Name],
    3)
   )


12 - Day of week = 
WEEKDAY(
    'Calendar Lookup'[Date],1)


13 - Weekend = 
IF(
    'Calendar Lookup'[Day of week] = 6 ||
    'Calendar Lookup'[Day of week] = 7,
    "weekend",
    "weekday"
)



 14 - Weekend_Update = 
IF(
    'Calendar Lookup'[Day of week] IN {6,7},
    "weekend",
    "weekday"
)

15 - Retail Price = RELATED('Product Lookup'[ProductPrice])


16 - Bulk order = CALCULATE(
    [Total Orders],
    'Sales Data'[OrderQuantity] > 1
)


17 -  Weekend Orders = 
CALCULATE(
    [Total Orders], 
    'Calendar Lookup'[Weekend_Update] = "Weekend"
)


18 - % of All orders = 
DIVIDE(
    [Total Orders],
    [All Order]
) 


19 - Average Retail Price = AVERAGE
(
    'Product Lookup'[ProductPrice]
)


20 - overall Average Price = 
CALCULATE(
    [Average Retail Price],
    ALL(
        'Product Lookup'
    )
)

21 - High Ticket orders = 
CALCULATE(
    [Total Orders],
    'Product Lookup'[ProductPrice] > 714.44
)

22 - High Ticket orders Filter = 
CALCULATE(
    [Total Orders],
    FILTER(
        'Product Lookup',
        'Product Lookup'[ProductPrice] > [overall Average Price]
    )
)

23 - Order Quantity = SUM(

    'Sales Data'[OrderQuantity]
)

24 - Total Revenue (CC) = SUM
(
    'Sales Data'[Revenue]
)

25 - Total Revenue = 
 SUMX(
    'Sales Data',
    'Sales Data'[OrderQuantity] * 'Sales Data'[Retail Price]
)

26 - 
   Total Revenue Related = 
 SUMX(
    'Sales Data',
    'Sales Data'[OrderQuantity] * 
    RELATED
    (
        'Product Lookup'[ProductPrice]
    )
)

27 - Average Revenue per customar = DIVIDE([Total Revenue], [Total Customers])



28 - YTD Revenue = 
CALCULATE(
    [Total Revenue Related],
    DATESYTD('Calendar Lookup'[Date])
)
 

29 - Previous Month Revenue = 
 CALCULATE(
    [Total Revenue Related],
    DATEADD(
        'Calendar Lookup'[Date],
        -1,
        MONTH
    )
 )

30 - 10 Days Rolling Revenue = 
CALCULATE(
    [Total Revenue Related],
    DATESINPERIOD(
        'Calendar Lookup'[Date],
        4DAX(
            'Calendar Lookup'[Date] -
        ),
        -10,
        DAY
        )
        
    )




 