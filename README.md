# TestingGithubActions

This is a step by step user guide to run jmeter test on github pipeline using GitHub Actions.
  It will automatically trigger the pipleline on new code commit to main branch.

- Create a new Jmeter test and save it as TestingGithubActions.jmx
![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/ce1ccf9d-e1f2-4ac0-8eb8-684b486f1537)

- Now Create a new Repo on github and upload the TestingGithubActions.jmx File
  ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/bdf0064d-99c3-4f80-8f24-423b59dc511f)

- Once Jmx file is uploaded, go to Actions and click New Workflow
  ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/77797fce-d8b6-42c0-8b1a-90b2c0b9e9fb)

- Click Configure in Simple workflow  
  ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/0bccb8b4-c539-4713-9c2f-b55b8c141f61)

- In MarketPlace search for ** PerfAction for Jmeter**
  ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/35d6f1b3-2e2f-4485-bb18-732f5a36cfff)

- It will create a dummy workflow file. Change Name of yml file and Remove Unnecessary Code
  ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/15829bc3-1abc-45f8-9092-b1876fda339d)

- Press Copy button to copy the code and paste it under
```
  steps:
        # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
        - uses: actions/checkout@v4
   ```
  ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/3c31a9eb-947b-40c5-a6d5-a57505489c7b)

- add testplan file link in **test-plan-path**
  ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/4f07193f-0822-4d16-9772-67621c809a57)

- Add following code to upload result file to build result 
```           
      - name: Upload Results
        uses: actions/upload-artifact@v3
        with:
          name: jmeter-results
          path: result.jtl
```
  ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/6f19a2d5-3f83-4efd-b499-1b41e35bd63a)
 
- Add following code to generate HTML report of test
  ```
    - name: Create reports directory
    run: mkdir reports
  
  - name: JMeter Test
    uses: QAInsights/PerfAction@v5.6.2
    with:
      test-plan-path: ./TestPlans/S01_SimpleExample/S01_SimpleExample.jmx
      args: "-e -o ./reports/html/"
      
  - name: Upload Results
    uses: actions/upload-artifact@v3
    with:
      name: jmeter-results
      path: result.jtl
      if-no-files-found: error
  
  - name: Upload HTML Reports
    uses: actions/upload-artifact@v3
    with:
      name: jmeter-html-reports
      path: reports
      if-no-files-found: error
  ```

- Go to All workflow and open last workflow
 ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/2ff15f59-c645-4c96-a665-7492003892f7)

- Scroll down to artifacts
  ![image](https://github.com/Waqar-Nadir/TestinGithubActions/assets/74316191/18d8adf6-81bb-469c-a755-0c043f766eda)


