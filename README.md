# COSC2759 Assignment 1
## Notes App - CI Pipeline
- Full Name/Names: Anuji Nethara Peiris, Wen Bin Liang
- Student ID/IDs: s4059550, s4146749

## 1. Pipeline Overview

### 1.1 Pipeline Triggers:

The pipeline runs on git push to any branch or PR to main, executing steps like npm install, npm run test:unit -- --coverage, and npm run test:e2e

   <img src="/img/image1.png" style="height: 150px;"/>

### 1.2 Pipeline Stages:

#### 1.2.1 Environmental Setup
- Runner: ubuntu-latest
- Database: MongoDB running on port 27017
- Checkout Code: Uses actions/checkout@v4 to access the repository.
- Node.js: Version 20 Configures Node.js version 20 using actions/setup-node@v4
- Install Dependencies: Runs npm install in the src directory to set up project dependencies.

<img src="/img/image2.png" style="height: 300px;"/>

#### 1.2.2 Run Tests

##### 1.2.2.1 Lint Tests
- Run Linting: Executes npm run test:lint in src to check code quality.

<img src="/img/image3.png" style="height: 250px;"/>

##### 1.2.2.2 Unit Tests
- Performs npm run test:unit -- --coverage in src to run Jest unit tests with 100% coverage.

<img src="/img/image4.png" style="height: 250px;"/>

##### 1.2.2.3 Integration Tests
- Executes npm run test:integration in src to validate component integration.

<img src="/img/image5.png" style="height: 150px;"/>

##### 1.2.2.4 End-to-End(E2E) Tests
a. Start App: Launches the app with npm run start & in src, setting SERVER=mongodb://localhost:27017/yeetcode for MongoDB connection.
b. Wait for App: Uses wget to poll http://localhost:3000, waiting with a 3-second delay until the app is ready.
c. Install Playwright Browsers: Runs npx playwright install and install-deps in src to prepare E2E testing.
d. Run E2E Tests: Executes npm run test:e2e in src to validate UI functionality (e.g., adding/saving/deleting notes) using Playwright.

<img src="/img/image6.png" style="height: 150px;"/>

#### 1.2.3 Artefacts

- Generate Artefact: On the main branch, creates an artefact.zip excluding node_modules using zip.
- Upload Artefact: Uploads app-artefact to GitHub Actions artifacts on main branch only.

<img src="/img/image7.png" style="height: 200px;"/>

<img src="/img/image8.png" style="height: 200px;"/>

### 1.3 Expected Outcomes
- On any branch push – Executes linting, unit, integration and end-to-end (E2E) tests.
- On Pull Request to main – Runs all tests again to validate changes before merge.
- On Main branch – Runs all tests and generates/uploads artefacts. 

#### 1.3.1 Expected Output for each test
a. Static/Lint Test: The log shows no linting errors, confirming clean code success.
- Actual Output: 

<img src="/img/image9.png" style="height: 200px;"/>

b. Unit Test: The log shows that Jest runs, showing all test cases pass with 100% coverage metrics displayed along with duration.
- Actual Output: 

<img src="/img/image10.png" style="height: 200px;"/>

c. Integration Test:The log shows successful validation of component interactions, with no failures displayed, along with duration.
- Actual Output: 

<img src="/img/image11.png" style="height: 200px;"/>

d. E2E test: The log shows a successful run with a brief summary like "3 passed" or "1 passed" along with a duration.
- Actual Output:

<img src="/img/image12.png" style="height: 200px;"/>


## 2. Branching Strategies
- This project follows GitHub Flow, using feature/ branches (e.g., feature/refine-ci-pipeline) for developing individual components or tasks.
- Each branch is created for specific improvements, tested, and merged into main via pull requests after review, ensuring a linear history and collaboration.

<img src="/img/image13.png" style="height: 200px;"/>

<img src="/img/image14.png" style="height: 200px;"/>

## 3. Addressing Each Requirement

### 3.1 For Pass
a. Enabled Lint & Unit Testing ✅

<img src="/img/image15.png" style="height: 200px;"/>

b. Ensured Code Coverage with Jest is checked ✅

<img src="/img/image16.png" style="height: 150px;"/>

c. Generated an artefact that can be deployed ✅

<img src="/img/image17.png" style="height: 150px;"/>

d. New features are developed on feature branches and merged into main via PR ✅

<img src="/img/image18.png" style="height: 150px;"/>

### 3.2 For Credit

a. Ensured that artefacts are generated on main branch only. ✅
- Main branch: 

<img src="/img/image19.png" style="height: 150px;"/>

- Other branch:

<img src="/img/image20.png" style="height: 150px;"/>

### 3.3 For Distinction

a. Pipeline worked with all branches, CI triggered when commits are pushed to any branch.✅

<img src="/img/image21.png" style="height: 150px;"/>

### 3.4 For High Distinction

a. E2E playwright test is added. ✅

<img src="/img/image22.png" style="height: 150px;"/>

b. Application functions as expected from the UI on 3 platforms. ✅
- From src/playwright-report/index.html

<img src="/img/image23.png" style="height: 150px;"/>

c. If the tests fail, the build is stopped and cause of failure is reflected in the log. ✅

<img src="/img/image24.png" style="height: 150px;"/>
<img src="/img/image25.png" style="height: 150px;"/>
<img src="/img/image26.png" style="height: 150px;"/>
<img src="/img/image27.png" style="height: 150px;"/>





