#### What’s New

- **Dedicated PostgreSQL Database:** A separate PostgresDB has been created.

- **API Payload Restructuring:** Payloads have been redesigned to manage data efficiently without the need for external database calls.
    
- **Enhanced Low-Level Design:** The LLD has been simplified and improved by applying SOLID principles.
    
- **Liquibase Integration:** SQL changes are now tracked using Liquibase.
    
- **Code Coverage Monitoring:** Jacoco has been integrated to monitor code coverage, which currently stands at 50%.
    
- **Built-in Scheduler Monitoring:** The system Will includes monitoring by design. Meaning Every Scheduler State will be send to respective team every time it runs.
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