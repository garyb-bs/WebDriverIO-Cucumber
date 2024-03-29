<p float="left">
    <img src="https://www.browserstack.com/images/static/header-logo.jpg" width="350">
    <img src="https://www.fleekitsolutions.com/wp-content/uploads/2020/04/webdriverio.png" height="100" width="200">
    <img src="https://brandslogos.com/wp-content/uploads/images/large/cucumber-logo.png" height="100" width="100">
</p>

# BrowserStack Examples Cucumber WebdriverIO <a href="https://webdriver.io/"><img src="https://avatars.githubusercontent.com/u/72550141?s=48&v=4" alt="WebdriverIO" height="22" /></a> <a href="https://nodejs.org/en/"><img src="https://brandslogos.com/wp-content/uploads/images/large/nodejs-icon-logo.png" alt="nodejs" height="22" /></a> <a href="https://mochajs.org/"><img src="https://brandslogos.com/wp-content/uploads/images/large/mocha-logo.png" alt="mochs" height="22" /></a>

## Introduction

WebdriverIO is a progressive automation framework built to automate modern web and mobile applications. It simplifies the interaction with your app and provides a set of plugins that help you create a scalable, robust and flakiness test suite.

This BrowserStack Example repository demonstrates a WebdriverIO tests framework written in Cucumber and NodeJS with parallel testing capabilities. The WebdriverIO test scripts are written for the open source [BrowserStack Demo web application](https://bstackdemo.com) ([Github](https://github.com/browserstack/browserstack-demo-app)). This BrowserStack Demo App is an e-commerce web application which showcases multiple real-world user scenarios. The app is bundled with offers data, orders data and products data that contains everything you need to start using the app and run tests out-of-the-box.

The WebDriverIO tests are run on different platforms like on-prem, docker and BrowserStack using various run configurations and test capabilities.

---

## Repository setup

- Clone the repository

- Ensure you have the following dependencies installed on the machine
  - NodeJS >= 14.16.0 (includes npm 6.14.11)

- Run below command to configure dependencies

    ```sh
    npm install
    ```

## About the tests in this repository

  This repository contains the following WebdriverIO tests:

  | Features   | Scenario name                          | Description |
  | ---   | ---                                   | --- |
  | E2E      | End to End Scenario                | This test scenario verifies successful product purchase lifecycle end-to-end. It demonstrates the [Page Object Model design pattern](https://www.browserstack.com/guide/page-object-model-in-selenium) and is also the default test executed in all the single test run profiles. |
  | Login    | Login with given username          | This test verifies the login workflow with different types of valid login users. |
  | Login    | Login as Locked User               | This test verifies the login workflow error for a locked user. |
  | Offers   | Offers for Mumbai location     | This test mocks the GPS location for Mumbai and verifies that the product offers applicable for the Mumbai location are shown.   |
  | Product  | Apply Apple Vendor Filter          | This test verifies that the Apple products are only shown if the Apple vendor filter option is applied. |
  | Product  | Apply Lowest to Highest Order By   | This test verifies that the product prices are in ascending order when the product sort "Lowest to Highest" is applied. |
  
  ---


## Test infrastructure environments 

- [On-premise/self-hosted](#on-premise--self-hosted)
- [Docker](#docker)
- [BrowserStack](#browserstack)


## Configuring the maximum parallel test threads for this repository

  For all the parallel run configuration profiles, you can configure the maximum parallel test threads by changing the settings below.

  - Docker

    `./resources/conf/wdio-docker-service-parallel.conf.js`

    ```js
    maxInstances: 5,
    ```
  
  - BrowserStack
    
    `./resources/conf/wdio-bstack-parallel.conf.js`

    ```js
    maxInstances: 5,
    ```

## Test Reporting

- [Allure reports](#generating-allure-reports)

---

# On Premise / Self Hosted

This infrastructure points to running the tests on your own machine using a browser (e.g. Chrome) using the browser's driver executables (e.g. ChromeDriver for Chrome).

## Running Your Tests

### Run a specific feature on your own machine

- How to run the feature?

  To run the default feature (e.g. End to End feature) on your own machine, use the following command:
  
  ```sh
  npm test
  ```

  To run a specific feature, use the following command with the script names from package.json:
  
  ```sh
  npm run <script_name>
  ```
  For example:

  ```sh
  npm run on-prem
  ```

  where,  the argument 'script_name' can be any WebdriverIO feature name configured in this repository inside package.json.

- Output

  This run profile executes a specific feature on a single browser instance on your own machine.


### Run the entire feature suite on your own machine

- How to run the feature?

  To run the entire feature suite on your own machine, use the following command:
  
  ```sh
  npm run on-prem-suite
  ```

- Output

  This run profile executes the entire feature suite sequentially on a single browser, on your own machine.

### Run the entire feature suite on your own machine in parallel

- How to run the feature?

  To run the entire feature suite on your own machine in parallel, use the following command:
  
  ```sh
  npm run on-prem-suite-parallel
  ```

- Output

  This run profile executes the entire feature suite parallelly by opening multiple browser instances on your own machine.

---

# Docker

[Docker](https://docs.docker.com/get-started/overview/) is an open source platform that provides the ability to package and test applications in an isolated environment called containers.

## Prerequisites

- Install and start [Docker](https://docs.docker.com/get-docker/).
- Note: Docker should be running on the test machine. Ensure Docker Compose is installed as well.

## Running Your Tests

### Run a specific test on the docker infrastructure

- How to run the feature?

    - To run the default feature (e.g. End to End Feature) on your own machine, use the following command:

    ```sh
    npm run docker
    ```

- Output

  This run profile executes a specific feature on a single browser deployed on a docker image.

### Run the entire feature suite in parallel using Docker

- How to run the feature?

    - To run the entire feature suite in parallel on the docker image, use the following command:

  ```sh
  npm run docker-parallel
  ```

- Output

  This run profile executes the entire feature suite in parallel on a single browser, deployed on a docker image.

- Note: By default, this execution would run maximum 5 test threads in parallel on Docker. Refer to the section ["Configuring the maximum parallel test threads for this repository"](#Configuring-the-maximum-parallel-test-threads-for-this-repository) for updating the parallel thread count based on your requirements.

---

# BrowserStack

[BrowserStack](https://browserstack.com) provides instant access to 2,000+ real mobile devices and browsers on a highly reliable cloud infrastructure that effortlessly scales as testing needs grow.

## Prerequisites

- Create a new [BrowserStack account](https://www.browserstack.com/users/sign_up) or use an existing one.
- Identify your BrowserStack username and access key from the [BrowserStack Automate Dashboard](https://automate.browserstack.com/) and export them as environment variables using the below commands.

    - For \*nix based and Mac machines:

  ```sh
  export BROWSERSTACK_USERNAME=<browserstack-username> &&
  export BROWSERSTACK_ACCESS_KEY=<browserstack-access-key>
  ```

    - For Windows:

  ```shell
  set BROWSERSTACK_USERNAME=<browserstack-username>
  set BROWSERSTACK_ACCESS_KEY=<browserstack-access-key>
  ```
  
  Alternatively, you can also hardcode username and access_key objects in conf files releated to BrowserStack at `./resources/conf/` file.

Note:
- We have configured a list of test capabilities in the files at `./resources/conf/`. You can certainly update them based on your device / browser test requirements. 
- The exact test capability values can be easily identified using the [Browserstack Capability Generator](https://browserstack.com/automate/capabilities)


## Running Your Features

### Run a specific feature on BrowserStack

In this section, we will run a single feature on Chrome browser on Browserstack. To change test capabilities for this configuration, please refer to the `capabilities` object in `./resources/conf/wdio-bstack-single.conf.js` file.

- How to run the feature?
  
  - To run the default feature (e.g. End to End Feature) on BrowserStack, use the following command:

  ```sh
  npm run bstack-single
  ```

- How to custom build name?
  - When you run test on BrowserStack it creates a build and session under which you can see your results. In this framework, if you want to add some custome name for build and session you can do like below:

  - Set build name by setting env varaibale:
    - For \*nix based and Mac machines:

    ```sh
    export BROWSERSTACK_BUILD_NAME=<browserstack_build_name>
    ```

    - For Windows:

    ```shell
    set BROWSERSTACK_BUILD_NAME=<browserstack_build_name>
    ```

  If you dont want to add, this framework will add build name with a time stamp for better tracking.

- Output

  This run profile executes a single test on a single browser on BrowserStack. Please refer to your [BrowserStack dashboard](https://automate.browserstack.com/) for test results.


### Run the entire feature suite in parallel on a single BrowserStack browser

In this section, we will run the feature in parallel on a single browser on Browserstack. Refer to `capabilities` object in `./resources/conf/wdio-bstack-parallel.conf.js` file to change test capabilities for this configuration.

- How to run the feature?

  To run the entire feature suite in parallel on a single BrowserStack browser, use the following command:
  
  ```sh
  npm run bstack-parallel
  ```

- Output

  This run profile executes the entire feature suite in parallel on a single BrowserStack browser. Please refer to your [BrowserStack dashboard](https://automate.browserstack.com/) for test results.

  - Note: By default, this execution would run maximum 5 test threads in parallel on BrowserStack. Refer to the section ["Configuring the maximum parallel test threads for this repository"](#Configuring-the-maximum-parallel-test-threads-for-this-repository) for updating the parallel thread count based on your requirements.


### Run the entire feature suite in parallel on multiple BrowserStack browsers

In this section, we will run the features in parallel on multiple browsers on Browserstack. Refer to the `capabilities` object in `./resources/conf/wdio-bstack-parallel-browsers.conf.js` file to change test capabilities for this configuration.

- How to run the feature?

  To run the entire feature suite in parallel on multiple BrowserStack browsers, use the following command:
  
  ```sh
  npm run bstack-parallel-browsers
  ```

### [Web application hosted on internal environment] Running your tests on BrowserStack using BrowserStackLocal

#### Prerequisites

- Clone the [BrowserStack demo application](https://github.com/browserstack/browserstack-demo-app) repository.
  ```sh
  git clone https://github.com/browserstack/browserstack-demo-app
  ``` 
- Please follow the README.md on the BrowserStack demo application repository to install and start the dev server on localhost.
- In this section, we will run a single test case to test the BrowserStack Demo app hosted on your local machine i.e. localhost. Refer to the `capabilities` object in `./resources/conf/wdio-bstack-local.conf.js` file to change test capabilities for this configuration.
- Note: You may need to provide additional BrowserStackLocal arguments to successfully connect your localhost environment with BrowserStack infrastructure. (e.g if you are behind firewalls, proxy or VPN).
- Further details for successfully creating a BrowserStackLocal connection can be found here:
  
  - [Local Testing with Automate](https://www.browserstack.com/local-testing/automate)
  - [BrowserStackLocal Java GitHub](https://github.com/browserstack/browserstack-local-java)


### [Web application hosted on internal environment] Run a specific feature on BrowserStack using BrowserStackLocal

- How to run the feature?

  - To run the default feature (e.g. End to End Feature) on a single BrowserStack browser using BrowserStackLocal, use the following command:

  ```sh
  npm run bstack-local
  ```

- Output

  This run profile executes a single feature on an internally hosted web application on a single browser on BrowserStack. Please refer to your BrowserStack dashboard(https://automate.browserstack.com/) for test results.


### [Web application hosted on internal environment] Run the entire feature suite in parallel on a single BrowserStack browser using BrowserStackLocal

In this section, we will run the feature to test the internally hosted website in parallel on a single browser on Browserstack. Refer to the `capabilities` object in `./resources/conf/wdio-bstack-local-parallel.conf.js` file to change test capabilities for this configuration.

- How to run the feature?

  To run the entire feature suite in parallel on a single BrowserStack browser using BrowserStackLocal, use the following command:

  ```sh
  npm run bstack-local-parallel
  ````

- Output

   This run profile executes the entire feature suite on an internally hosted web application on a single browser on BrowserStack. Please refer to your [BrowserStack dashboard](https://automate.browserstack.com/) for test results.
  
- Note: By default, this execution would run maximum 5 test threads in parallel on BrowserStack. Refer to the section ["Configuring the maximum parallel test threads for this repository"](#Configuring-the-maximum-parallel-test-threads-for-this-repository) for updating the parallel thread count based on your requirements.

### [Web application hosted on internal environment] Run the entire feature suite in parallel on multiple BrowserStack browser using BrowserStackLocal

In this section, we will run the features to test the internally hosted website in parallel on multiple browsers on Browserstack. Refer to the `capabilities` object in `./resources/conf/wdio-bstack-local-parallel-browsers.conf.js` file to change test capabilities for this configuration.

- How to run the feature?

  To run the entire feature suite in parallel on a single BrowserStack browser using BrowserStackLocal, use the following command:

  ```sh
  npm run bstack-local-parallel-browsers
  ```

- Output

  This run profile executes the entire feature suite on an internally hosted web application on multiple browsers on BrowserStack. Please refer to your [BrowserStack dashboard](https://automate.browserstack.com/) for test results.

- Note: By default, this execution would run maximum 5 test threads in parallel on BrowserStack. Refer to the section ["Configuring the maximum parallel test threads for this repository"](#Configuring-the-maximum-parallel-test-threads-for-this-repository) for updating the parallel thread count based on your requirements.

## Generating Allure Reports

- Generate Report using the following command: `npm run generate-report`

## Additional Resources

- View your test results on the [BrowserStack Automate dashboard](https://www.browserstack.com/automate)
- Documentation for writing [Automate test scripts in Java](https://www.browserstack.com/automate/java)
- Customizing your tests capabilities on BrowserStack using our [test capability generator](https://www.browserstack.com/automate/capabilities)
- [List of Browsers & mobile devices](https://www.browserstack.com/list-of-browsers-and-platforms?product=automate) for automation testing on BrowserStack
- [Using Automate REST API](https://www.browserstack.com/automate/rest-api) to access information about your tests via the command-line interface
- Understand how many parallel sessions you need by using our [Parallel Test Calculator](https://www.browserstack.com/automate/parallel-calculator?ref=github)
- For testing public web applications behind IP restriction, [Inbound IP Whitelisting](https://www.browserstack.com/local-testing/inbound-ip-whitelisting) can be enabled with the [BrowserStack Enterprise](https://www.browserstack.com/enterprise) offering