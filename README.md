
# Lambda Function for Loading CSV Data into Redshift

This Lambda function automates the loading of CSV data from an S3 bucket into a Redshift table using the COPY command triggered by object creation events.

## Configuration

1. **Create Lambda Function**
   - Runtime: Python 3.8
   - Handler: lambda_function.lambda_handler

2. **Environment Variables**
   - *dbname* - Name of Redshift database
   - *host* - Cluster endpoint 
   - *port* - Port number (typically 5439)
   - *user* - Database username 
   - *password* - Database password
   - *tablename* - Target table name
   - *schema* - Schema name (where target table exists)
   
3. **IAM Permissions**  
   - Lambda execution role requires the following policy for S3 and Redshift access:
     - s3:GetObject 
     - redshift:GetClusterCredentials
     - redshift:DescribeClusters

4. **S3 Trigger**  
   - Configure S3 bucket to publish events to Lambda
   - Set event type to "Object Created"

## Usage

1. Upload CSV file to configured S3 bucket 
2. Lambda will be triggered on object creation
3. File will be copied to target Redshift table 
   - Schema must match CSV 
4. Check Redshift load error tables if issues

## Troubleshooting

- Validate environment variables match Redshift config
- Check IAM permissions allow accessing S3 file and Redshift
- Enable Lambda debugging for stacktraces 
- Query STL load error tables in Redshift for copy errors

## Project Reference

This Lambda function was designed to address issues encountered during the Redshift workgroup creation. For specific details, refer to the [Redshift Workgroup Creation Issues](https://docs.aws.amazon.com/redshift/latest/mgmt/serverless-known-issues.html) documentation.

