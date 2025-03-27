#### What’s New

- **Dedicated PostgreSQL Database:** A separate PostgresDB has been created.
	- Tables includes EmailRequest, EmailTemplate,EmailQueue & SchedulerAudit

- **API Payload Restructuring:** Payloads have been redesigned to manage data efficiently without the need for external database calls.
    
- **Enhanced Low-Level Design:** The LLD has been simplified and improved by applying SOLID principles.
	- Means its easier to add new changes
	- implement new email is now simplified
	- no more bunch of changes for a small feature
    
- **Liquibase Integration:** SQL changes are now tracked using Liquibase.
	- Now every changes is tracked
	- no more manual storage and update of sql queries
    
- **Code Coverage Monitoring:** Jacoco has been integrated to monitor code coverage
	- currently we've 50% code covered
	- aiming to maximize it as much as possible with initial target to 70%
    
- **Built-in Scheduler Monitoring:** The system Will includes monitoring by design.
	- Meaning Every Scheduler trigger will generate and sen
#### What’s Completed

- **API-Based Email Services:**
    
    - _Subscription-Based Emails:_ Features include sending welcome emails as well as notifications for resume, pause, skip, cancel, change frequency, and addOnInc.
        
    - _Child Order-Based Emails:_ Includes notifications for contract pause confirmations, pre-authorization, pre-ship, pre-ship pull-forward, and order processing failures.
        

#### What’s Pending

- **Bulk Email Features:** Bulk email functionalities, such as FST warnings and confirmations, are still in progress.
    
- **Scheduler Functions:** Pending tasks include schedulers for credit card expiration alerts, out-of-stock notifications, retry mechanisms, and data purging.
    

#### What’s Next

- **Ongoing LLD Optimization:** Further refinement of the low-level design to ensure simplicity, scalability, and long-term maintainability.

- **Continued Monitoring:** The commitment to a "monitoring by design" approach will be Continued

- **Code Coverage:** We'll continue to improve the code coverage  