# [DAX] AdventureWorks Performance Report 


#### Sales Transactions 

         = DISTINCTCOUNT('Sales Data'[OrderNumber])

#### All Orders
       
         = CALCULATE(
            [Sales Transactions],
            ALL(
              'Sales Data')) 
         
#### Return Transactions

         = COUNT('Returns Data'[ReturnQuantity])

#### All Returns

         = CALCULATE(
            [Return Transactions],
            ALL(
              'Returns Data')) 
     
#### (% of All Orders)

        = DIVIDE(
            [Sales Transactions],
            [All Orders])

#### (% of All Returns)

        = DIVIDE(
            [Return Transactions],
            [All Returns])

#### Total Revenue

        = SUMX(
            'Sales Data',
            'Sales Data'[OrderQuantity] * 
            RELATED(
              'Product Lookup'[ProductPrice]))

#### Total Cost

        = SUMX(
            'Sales Data',
            'Sales Data'[OrderQuantity] * 
            RELATED(
              'Product Lookup'[ProductCost]))

#### Total Customers

        = DISTINCTCOUNT('Sales Data'[CustomerKey])

#### Total Profit

        = [Total Revenue] - [Total Cost]

#### Total Revenue (Customer Detail)

        = IF(
            HASONEVALUE(
              'Customer Lookup'[CustomerKey]),
              [Total Revenue],
              "-")

#### Weekend Orders

        = CALCULATE(
            [Sales Transactions],
            'Calendar Lookup'[Weekend] = "Weekend")

#### YTD Revenue

        = CALCULATE(
            [Total Revenue],
            DATESYTD('Calendar Lookup'[Date]))

#### 10-Day Rolling Revenue

        = CALCULATE(
            [Total Revenue],
            DATESINPERIOD(
              'Calendar Lookup'[Date],
              MAX(
                'Calendar Lookup'[Date]),
              -10,
              DAY))

#### Average Retail Price

        = AVERAGE('Product Lookup'[ProductPrice])

#### Overall Average Price

        = CALCULATE(
            [Average Retail Price],
            ALL(
              'Product Lookup'))

#### Average Revenue Per Customer

        = DIVIDE(
            [Total Revenue],
            [Total Customers])

#### Adjusted Price

        = [Average Retail Price] * 
          (1 + 'Price Adjustment %'[Price Adjustment % Value])

#### Adjusted Revenue

        = SUMX(
            'Sales Data',
            'Sales Data'[OrderQuantity] * 
            [Adjusted Price])
            
#### Adjusted Profit

        = [Adjusted Revenue] - [Total Cost]

#### Average Revenue Per Customer

        = DIVIDE(
          [Total Revenue],
          [Total Customers])

#### Quantity Sold 

        = SUM('Sales Data'[OrderQuantity])

#### Bikes Sales
        
        = CALCULATE(
            [Quantity Sold],
            'Product Categories Lookup'[CategoryName] = "Bikes")

#### Bike Returns 
        
        = CALCULATE(
            [Return Transactions],
            'Product Categories Lookup'[CategoryName] = "Bikes")

#### Bulk Orders 

        = CALCULATE(
          [Sales Transactions],
          'Sales Data'[OrderQuantity] > 1)

#### Full Name (Customer Detail) 

        = IF(
            HASONEVALUE(
              'Customer Lookup'[CustomerKey]),
            MAX(
              'Customer Lookup'[Full Name]),
            "Multiple Customers")

#### High Ticket Orders

        = CALCULATE(
            [Sales Transactions],
            FILTER(
              'Product Lookup',
              'Product Lookup'[ProductPrice] > [Overall Average Price]))

#### Previous Month Orders 

        = CALCULATE(
            [Sales Transactions],
            DATEADD(
              'Calendar Lookup'[Date],
              -1,
              MONTH))

#### Order Target 
        
        = [Previous Month Orders] * 1.1

#### Order Target Gap 

        = [Sales Transactions] - [Order Target]

#### Previous Month Profit 

        = CALCULATE(
            [Total Profit],
            DATEADD(
              'Calendar Lookup'[Date],
              -1,
              MONTH))

#### Previous Month Revenue 

        = CALCULATE(
            [Total Revenue],
            DATEADD(
              'Calendar Lookup'[Date],
              -1,
              MONTH))

#### Revenue Target 

        = [Previous Month Revenue] * 1.1

#### Revenue Target Gap 

        = [Total Revenue] - [Revenue Target]

#### Profit Target 

        = [Previous Month Profit] * 1.1

#### Profit Target Gap 

        = [Total Profit] - [Profit Target]

#### Quantity Returned 

        = SUM('Returns Data'[ReturnQuantity])

#### Return Rate 

        = DIVIDE(
            [Quantity Returned],
            [Quantity Sold], 
            "No Sales")

#### Total Cost

        = SUMX(
            'Sales Data',
            'Sales Data'[OrderQuantity] * 
            RELATED(
              'Product Lookup'[ProductCost]))

#### Total Revenue (Customer Detail)

        = IF(
            HASONEVALUE(
              'Customer Lookup'[CustomerKey]),
              [Total Revenue],
              "-")  

#### Full Name (Customer Detail) 

        = IF(
            HASONEVALUE(
              'Customer Lookup'[CustomerKey]),
            MAX(
              'Customer Lookup'[Full Name]),
            "Multiple Customers")

#### High Ticket Orders

        = CALCULATE(
            [Sales Transactions],
            FILTER(
              'Product Lookup',
              'Product Lookup'[ProductPrice] > [Overall Average Price]))

 #### Previous Month Orders 

        = CALCULATE(
            [Sales Transactions],
            DATEADD(
              'Calendar Lookup'[Date],
              -1,
              MONTH))        

#### Total Revenue

        = SUMX(
            'Sales Data',
            'Sales Data'[OrderQuantity] * 
            RELATED(
              'Product Lookup'[ProductPrice]))

#### YTD Revenue

        = CALCULATE(
            [Total Revenue],
            DATESYTD('Calendar Lookup'[Date]))

#### 10-Day Rolling Revenue

        = CALCULATE(
            [Total Revenue],
            DATESINPERIOD(
              'Calendar Lookup'[Date],
              MAX(
                'Calendar Lookup'[Date]),
              -10,
              DAY))         
