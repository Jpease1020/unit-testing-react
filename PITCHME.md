+++
## Unit Testing React Components

+++
### Acceptance Tests
  * Definition
    * Automated tests ensuring the environment/application is successfully built to allow for manual User Acceptance testing
    * Front end: UI Tests
    * Back end: Smoke/End-to-End Tests

+++
### Acceptance Tests
  * CI Pipeline
    * Acceptance tests come before deploying to UAT/TEST environment
      * Assuming DEV --> UAT --> PRE-PROD environments
    * Acceptance tests can be run in DEV environment
    * Ensures environment/application is up and running for manual user acceptance testing to be performed
    * Automated tests that ensure newly deployed code works in environment

+++
### Back End
  * Smoke Tests
    * Run after deploying new apps/infrastructure
    * Ensures all back end services wire together successfully
      * Oracle, Cassandra, RabbitMQ, Kafka, etc.

+++
