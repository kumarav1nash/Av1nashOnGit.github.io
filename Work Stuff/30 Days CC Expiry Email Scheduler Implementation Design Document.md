Initial Thought
- Get the list of prosubscription for which nextFFm scheduled falls on the given cadence date ie (t+28,t+21,t+14,t+7)
- clean the and prepare the proper data structure to map wallet ids with respective subscription ids
	- since one wallet id can be linked to multiple subscription, i'm thinking of creating ```Map<Long,List<Long>> ```
	- this can be used later to get the related data which will be required for composing mails
- now we have the unique list of wallet ids, we can hit the apis in the wallet service  to get the list of expired wallet ids.
	- this api will take list of wallet ids and give list of expired wallet id from the requests
	- this way we can limit ourself from performing 1000's of network query
	- hence we need to create new api for this in wallet service
- once we got the list of expired api we need another apis from wallet service
	- which will take list of wallet id which will be expired and return billing details for those in key value format, where key will be wallet id and value will be billing detail object
- then we can compose our email and send the mails



### NUMBERs WE CONSIDERED BASED ON INITIAL RESEARCH
- there can be 50K wallet a day that can be expired
- there can be 1-2L subscriptions a day for which we might need to send mails
- so on an average we'll be sending  2-4L subscriptions


Task Required
- Create a Scheduler that will run once a day (time yet to be decided)
- Create a service class to write alll the logic related to 30 days cc
- create first api in wallet micro-service with these details
request body - list of wallet ids
```
 {
	 "walletIds" : [435,343,222,34453]
 }
```
response body - list of wallet ids which are expired
```
 {
	 "walletIds" : [343,222]
 }
```

- create second apis in wallet micro-service with these details
request body - list of wallet ids
```
 {
	 "walletIds" : [435,343,222,34453]
 }
```

response body - list of billing address, with wallet id as key and billing object as value
```
{
"response":
	[
		{obj1},
		{obj2},
		{obj3},
		{obj4}
	]
}
```

- 30 day cc composer to compose the emails
- sql query to fetch the eligible pros subscription from the table


Things to consider
- since we have lacs of rows to fetch every time, we can use slice technique to fetch batch of rows, and then we can compose each batch and then we can send emails
	- let's say we have 2 lac rows for todays, we can take 10k row at a time process them and send the mails








Important Checkpoints
- Preparing EmailInfo
- Storing template in template table and email request in emailRequest table
- call sfmc api to send the mail
- Updating status in the db

- for schedulers
	- preparing emailInfoes => (3-5 db call + solr call+wallet call)
	- storing them in emailqueue+template db
	- fetching from them and sending the mails and updating their status in db
	- deleting those rows from email queue
	- 













### Failures and Error Handling

- **Error Logging and Reporting:**
    
    - Implement a centralized logging mechanism to capture errors and exceptions.
    - Log detailed error messages, stack traces, timestamps, and affected data.
    - Use logging levels to differentiate between informational messages and errors.
- **Error Notifications:**
    
    - Set up automated alerts or notifications when critical errors occur.
    - Use monitoring tools to trigger alerts via email, messaging platforms, or dashboards.
- **Graceful Degradation:**
    
    - Define fallback strategies for critical components or external dependencies.
    - If a non-critical component fails, the system can continue operating with reduced functionality.

### Batch Processing

- **Chunking and Batching:**
    
    - Divide your data into manageable chunks or batches for processing.
    - Process one batch at a time, and handle any failures before moving to the next batch.
- **Checkpointing:**
    
    - Maintain checkpoints to track the progress of processing.
    - After successfully processing a batch, update the checkpoint to the next batch's starting point.
- **Transaction Management:**
    
    - Use transactions to ensure data consistency during batch processing.
    - Roll back the transaction if any part of the batch fails, preventing partial or incorrect data updates.

### Retry Mechanisms

- **Exponential Backoff:**
    
    - When encountering transient errors, such as network timeouts, implement exponential backoff.
    - After each failed attempt, increase the time delay before the next retry, allowing the system to recover.
- **Retry Limits:**
    
    - Define a maximum number of retries for each operation.
    - If the operation fails after exhausting the retries, escalate the issue for manual intervention.

### Transactional and Idempotent Operations

- **Idempotence:**
    
    - Ensure that your operations are idempotent, meaning that they can be safely retried without causing duplicate or unintended effects.
    - This is crucial for situations where retries occur due to transient errors.
- **Transactional Integrity:**
    
    - When interacting with external services or databases, design operations to be transactional.
    - If one part of the operation fails, roll back any changes made up to that point.

###  Dead Letter Queue

- **Dead Letter Queue (DLQ):**
    
    - Set up a DLQ to capture operations that repeatedly fail despite retries.
    - Place failed operations in the DLQ for manual inspection and resolution.
- **Manual Intervention:**
    
    - Assign personnel to periodically review items in the DLQ.
    - Investigate the cause of failures, correct any data issues, and manually reprocess the failed items.

Remember that these steps are not isolated, and a holistic approach is key to building a robust and resilient system. Each step interacts with the others to create a comprehensive strategy for handling failures and ensuring smooth operation. By addressing these aspects, you can develop a reliable email microservice that can handle large volumes of data and deliver emails effectively while gracefully handling errors and issues.



Understood. Since you're using Salesforce Marketing Cloud to send emails and your main concern is handling data aggregation, composition, and potential failures before calling the Salesforce API for sending emails, here are some specific steps and strategies to consider:

1. **Data Collection and Aggregation:**
    
    - Collect data from various sources in a controlled and reliable manner.
    - Implement robust data validation and cleansing to ensure data quality.
    - Aggregate the collected data into a suitable format for email composition.
2. **Email Composition and Personalization:**
    
    - Use a template engine to dynamically compose personalized email content.
    - Incorporate placeholders for dynamic fields like names, order details, etc.
    - Ensure that the composed emails are properly formatted and visually appealing.
3. **Failures and Error Handling:**
    
    - Implement proper error handling and logging mechanisms at each step of the process.
    - Use try-catch blocks or error handling libraries to capture and log exceptions.
    - Identify different types of failures, such as data source errors, composition errors, or API call errors.
4. **Batch Processing:**
    
    - Process emails in batches rather than individually to improve efficiency.
    - Use batch checkpoints to keep track of progress and recover from failures.
5. **Retry Mechanisms:**
    
    - Implement retry logic for failed steps. For example, if a data source is temporarily unavailable, retry fetching the data after a short interval.
    - Use exponential backoff to avoid overwhelming the data sources or APIs during transient failures.
6. **Transactional and Idempotent Operations:**
    
    - Design your process to be transactional whenever possible. If one step fails, ensure that any changes made up to that point are rolled back.
    - Make API calls idempotent, meaning that sending the same request multiple times has the same effect as sending it once. This helps prevent duplicate operations.
7. **Dead Letter Queue:**
    
    - If an operation fails consistently after retries, consider routing the failed email compositions to a "dead letter queue" for manual intervention or analysis.
8. **Monitoring and Alerts:**
    
    - Implement monitoring tools to track the progress and health of your email composition process.
    - Set up alerts to notify you of significant failures or bottlenecks.
9. **Backups and Redundancy:**
    
    - Keep backup copies of aggregated data and composed emails in case of unexpected failures.
    - Use redundancy in your system architecture to ensure high availability.
10. **Graceful Shutdown:**
    
    - In the event of a planned maintenance or unexpected issue, implement a graceful shutdown process that ensures any ongoing tasks are properly completed before the system goes offline.
11. **Testing:**
    
    - Perform thorough testing with different scenarios to identify potential failure points and refine your error handling strategies.
12. **Documentation:**
    
    - Maintain clear documentation for the entire process, including data sources, composition logic, retry strategies, and API calls.