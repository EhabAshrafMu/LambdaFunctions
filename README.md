# LambdaFunctions
Examples for some Lambda functions in Python 3.11

# salesAnalysisReport:
This AWS Lambda function retrieves a daily sales report from a database, formats it, and publishes the report via Amazon SNS. It performs the following steps:
Environment and Secrets: The function retrieves the Amazon SNS topic ARN and AWS region from environment variables. Database connection details (URL, username, database name, password) are fetched from AWS Secrets Manager.
Database Query Invocation: It invokes another Lambda function (salesAnalysisReportDataExtractor) to fetch the sales report data from the database, using the retrieved database credentials.
Report Formatting: The sales data is processed and formatted into a readable report, categorizing items by product group. A helper function setTabsFor adjusts tab spacing based on item name length to align columns.
Publishing to SNS: Using the Amazon SNS client, it publishes the formatted report to the specified SNS topic.
Return Response: The function returns a success message indicating the report has been sent.
This function is ideal for generating and distributing daily sales summaries.



# salesAnalysisReportDataExtractor:
This AWS Lambda function, lambda_handler, connects to a MySQL-compatible database to generate a daily sales analysis report. It retrieves database connection details from the input event, establishes a connection using pymysql, and executes a SQL query to aggregate the total quantity of each product sold by product group. After fetching the data, the function closes the database connection and returns the results as a JSON response. Error handling ensures any connection issues are logged, and the function exits gracefully if a connection cannot be established.
