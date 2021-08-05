# Miscellaneous Notes
Random notes and thoughts written down during development of the Puff Platform

### Backend ideas
* Security for secrets and config values
    * Vault?
    * Github secrets?
    * MS Azure?
* Code smells and vulnerabilities (Sonarcube?)

### Additional security for Docker containers
* SELinux?
* AppArmor?

### Front-end Ideas
Like designs for
* prisma.io
* Slack
* Github Co-pilot home page

Need a code editor like leetcode to allow for test case coding as well as suite file creation.

### Ideas for development
* Static syntax checking (front-end)
* Propose edits functionality (No idea how to add this, maybe in comments)

### Error codes correlation for running test cases
* virtual memory -v 139
* stack memory -s 139
* user processes -u
* max files -f 153
* max memory -m
* docker memory -m 125
* max file descriptors -n 127
* timeouts
    * SIGTERM 143
    * SIGKILL 137
* invalid python code 2
* pytest failure 1
* pytest pass 0

### Process ideas for running test cases
1. In target directory create new directory with unique name
    * combination of userId, submissionId, suiteId (maybe more? timestamp?)
2. Create a volume for the suitefile in directory and append the test case as necessary
3. Create a volume for the submission files
4. Based on result return one of ouput status codes
    * PASS, FAILED, TIMEOUT_ERROR, COMPILATION_ERROR, RUNTIME_ERROR

Note: Limit traceback error message to prevent information leaking

5. Set limits to enforce on timeouts and memory

### Integration & Unit Testing with Maven (surefire)
By default with surefire plugin looks for unit tests with 
* `*Tests.java`
* `*Test.java` or `*Test*.java`
* `*TestCase.java`

By default with failsafe plugin integration tests run with
* `**IT.java`
* `*IT*.java`
* `**ITCase.java`

Run with `mvn integration-test` or as part of the `verify` phase.