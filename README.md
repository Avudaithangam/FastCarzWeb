# FastCarzWeb
1) The build should trigger as soon as anyone in the dev team checks in code to master branch.
 - The azure pipeline trigger ensures that the pipeline gets triggered as soon as there is a change in the repo
  
  ```
  trigger:
  - master
  ```
2) There will be test projects which will create and maintained in the solution along the Web and API. The trigger should build all the 3 projects - Web, API and test.
  - Using the multi repo checkout option in Azure DevOps, a trigger is set which triggers the pipeline to build all the three projects at the same time
```
  - repository: FastCarzWeb
    type: github
    endpoint: Avudaithangam
    name: Avudaithangam/FastCarzWeb
    ref: master
```
The build should not be successful if any test fails.
  - The pipeline sequence is set in a way that the pipeline will fail on failure of the testcase execution
  - Build the application
  - Build docker image
  - Deploy the docker image
  - Run the test on deployed image
  - Build fails on test failure
- All the above tasks are done in the pipeline https://dev.azure.com/avuvig/FastCarz/_build?definitionId=18

3) The deployment of code and artifacts should be automated to Dev environment.
  - A pipeline is created to deploy to dev environment https://dev.azure.com/avuvig/FastCarz/_build?definitionId=16

4) Upon successful deployment to the Dev environment, deployment should be easily promoted to QA and Prod through automated process.

  - All the environment deployment is added on the same pipeline as above
5) The deployments to QA and Prod should be enabled with Approvals from approvers only.
  - The QA and Prod environments have been setup in a way that the deployment happens only on approval. https://dev.azure.com/avuvig/FastCarz/_environments/6/checks


# Known Issues
- The pipeline repository trigger is not working even when it is defined correctly
- The tests repo does not contain any testcases to test the application
