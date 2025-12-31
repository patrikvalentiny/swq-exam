<!-- <div style="text-align: center; padding-top: 300px;"> -->

# Comparison of IDEs For Exploring and Testing APIs

**Student:** Patrik Valentiny  

<!-- </div> -->
<!-- <div style="page-break-after: always;"></div> -->

## 1. Introduction

## 2. Quality Metrics

I have chosen the metrics below to compare how each IDE performs in key areas relevant to developers working with and testing APIs.

### 2.1. Performance

Performance mainly covers tool responsiveness and resource use. The observation is based on the user experience instead of precise benchmarks. The observations include startup time, the time to run individual requests, and how the tool behaves under usual developer tasks.

### 2.2. Maintainability

Maintainability concerns how easily projects can be organised, shared and updated. Useful features are straightforward environment setup, reusable variables or templates, clear collection structure, and reliable import/export or versioning options.

### 2.3. Security

Security focuses on protecting credentials and sensitive data. Evaluating secure storage for secrets and support for common authentication methods.

### 2.4. Testing Capabilities

Testing capabilities include assertion support, testing framework, clear reporting, test collection running and scheduled tests. Tools should enable repeatable validation with readable and actionable results.

### 2.5. Additional Features

Additional features cover the inclusion of extras over API request and testing. For example mock servers, collaboration tools, automation hooks, and helpful integrations—can boost the speed of development.

## 3. IDEs Overview

### 3.1. Postman

Postman is probably the most well-known API testing tool. It offers a user-friendly interface and a wide range of features for testing RESTful APIs. Recently, Postman has become more bloated with features that may not be necessary for users that use it as an API testing tool. This can lead to a steeper learning curve and slower performance. It's closed-source nature and reliance on a proprietary platform may also be a drawback for some developers. The cloud first approach can be a concern for teams with strict data privacy requirements. Pricing can be a concern for teams, as advanced features require a paid subscription.

### 3.2. Insomnia

Insomnia started as an open-source project and has grown into a robust API client with a focus on usability and extensibility. Recently acquired by Kong, it continues to offer both free and paid plans. It has moved towards a cloud-first model but still supports local storage options for users concerned about data privacy. It is more lightweight compared to Postman, making it faster for many tasks. The transition to a cloud-first approach is concerning for users prioritizing data privacy.

### 3.3. Bruno

Bruno is an open-source API client that focuses on simplicity and performance. It stores collections directly on the filesystem using a plain text markup language called Bru, which allows for easy version control with Git or other systems. Bruno is designed to be offline-only, prioritizing data privacy by ensuring that all data remains on the user's device. This approach may limit collaboration features compared to cloud-based tools but appeals to users with strict privacy requirements. Its roadmap is focused on keeping the tool open source and allowing community contributions without commercial pressures. The local-first approach aid performance and responsiveness.

## 4. Comparison

### 4.1. Performance

Bruno is the most lightweight of the three tools, leading to fast startup times and quick request execution. Postman, while feature-rich, can feel sluggish due to its extensive capabilities cloud-based architecture. Insomnia is generally faster than Postman but may still lag behind Bruno in terms of responsiveness.

### 4.2. Maintainability

All three tools offer good maintainability features. Postman provides robust environment management and variable support, but its proprietary format can complicate version control. Insomnia offers similar features with better local storage options. Bruno's use of plain text files for collections makes it the most maintainable in terms of version control and collaboration through Git.
Variable management and environment setup are straightforward in all three tools. With option to define global, environment, and collection-specific variables. Bruno also supports variables defined directly in the request which can be useful for testing. 
All three tools support dynamic variable setting in order to allow **request chaining**.
Exporting and importing collections is straightforward in all three tools, Insomnia and Bruno can also import Postman collections, making migration easier.

### 4.3. Security

Variables and secrets are stored securely in all three tools. Postman and Insomnia offer encrypted storage for sensitive data, while Bruno's local storage approach ensures that data never leaves the user's device. All three tools support common authentication methods such as OAuth, API keys, and basic auth.
Sharing collections is easiest with Postman and Insomnia due to its cloud-based nature, Postman allows to choose what variables are stored on the cloud and which are local-only. Bruno requires manual sharing of files or using version control systems. Bruno does share variables marked as "private" when saving files.

### 4.4. Testing Capabilities

### 4.5. Additional Features

## 5. CI/CD Integration

### 5.1 CLI Support

All of the tools provide command-line interfaces (CLIs) that allow users to run tests. Postman offers Postman CLI or Newman, Insomnia provides Insomnia CLI, and Bruno has its own Bruno CLI. These CLIs can be integrated into CI/CD pipelines to automate API testing as part of the development workflow.

#### Postman CLI

Postman CLI is used to run Postman collections stored in the cloud by authenticating via an API key and running the predefined collection by it's id. The documentation is comprehensive and it is relatively straightforward to integrate into CI/CD pipelines. However, since Postman collections are stored in a proprietary format, version control and collaboration can be more challenging compared to tools that use plain text files. The CLI only executes collections stored in the Postman cloud, run details are then visible directly in the Postman app.

#### Insomnia CLI

Insomnia CLI seems to be in a more experimental state. It seems the switch from local storage to a cloud-first approach has affected the CLI usability. The documentation is sparse and it is not clear how to integrate it into CI/CD pipelines effectively.

#### Bruno CLI

Bruno CLI allows running Bru files directly from the collection root or by selecting folders or specific requests. It is straightforward to use and integrates well into CI/CD pipelines. Since Bruno stores collections as plain text files, it is easy to version control and manage within a CI/CD context.

### 5.2 GitHub Actions Integration

#### Postman

Postman CLI is setup in GitHub Actions by installing it via a shell script, logging in using an API key stored in GitHub Secrets, and then running the desired collection by its ID. Below is an example GitHub Actions workflow which was generated by Postman client for running a Postman collection:

```yaml
name: Automated API tests using Postman CLI

on: push

jobs:
  automated-api-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install Postman CLI
        run: |
          curl -o- "https://dl-cli.pstmn.io/install/linux64.sh" | sh
      - name: Login to Postman CLI
        run: postman login --with-api-key ${{ secrets.POSTMAN_API_KEY }}
      - name: Run API tests
        run: |
          postman collection run "29167626-4746e42d-43a8-40d6-9d8a-d24b44531c54"
```

#### Insomnia

Inso CLI can be integrated into GitHub Actions by using the official Kong setup action to install Inso, and then running the tests from the desired collection and environment. Below is an example provided by Kong, this, however, does not seem to be working with the latest version of Insomnia:

```yaml
name: Automated API tests using Inso CLI

on: push

jobs:
  automated-api-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: kong/setup-inso@v2
        with:
          inso-version: 11.3.0
      - run: inso --version
      - run: inso run collection wrk_da5c3b -e env_c19213 --verbose --ci
```

#### Bruno

Bruno CLI can be integrated into GitHub Actions by installing Node.js, installing Bruno CLI via npm, and then running the tests from the desired collection directory. Below is an example GitHub Actions workflow for running Bruno tests:

```yaml
name: Bruno API Tests

on: push

jobs:
  api-test:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4
      
    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '20'
    
    - name: Install Bruno CLI
      run: npm install -g @usebruno/cli
    
    - name: Run API Tests
      run: cd DummyJson && bru run
```

## 6. Conclusion and Recommendations

## 7. References

1. **Postman Learning Center**
   [https://learning.postman.com/docs/introduction/overview/](https://learning.postman.com/docs/introduction/overview/)
2. **Insomnia Documentation**
   [https://developer.konghq.com/insomnia/](https://developer.konghq.com/insomnia/)
3. **Bruno Documentation**
   [https://docs.usebruno.com/](https://docs.usebruno.com/)
4. **DummyJson API**
   [https://dummyjson.com/docs](https://dummyjson.com/docs)
5. **Insomnia GitHub Repository**
   [https://github.com/Kong/insomnia](https://github.com/Kong/insomnia)
6. **Bruno GitHub Repository**
    [https://github.com/usebruno/bruno](https://github.com/usebruno/bruno)