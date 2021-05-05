# Contributing to this repository

> 🚚 The goal is to ship small features, quickly, and frequently.

In order to do this we need to break our features down into smaller units of work and `🤖 automate` as much as possible. Testing should remain easy to setup, consistent with production, and enable rapid iteration. Local development should mirror that of `staging`, with as few network dependencies as possible.

1. Create a _feature-branch_ based on `master`
2. Create a PR and leave setting it to `draft` mode
   1. This will give us a deployment connected to `staging`
   2. use the `preview` branch if you need `production` data
3. Pull Request review process
   1. Take it out of `draft` mode
   2. Assign a reviewer or two
   3. Address feedback, learn and teach
4. Merge into master
   1. This will automate the deployment
   2. Watch Sentry for any new errors
   3. Validate the change on production

## 🌴 Branches

We've chosen to make use of the [Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) when working with Git.

- **master**
  - The source of truth, this is `live/production` code
  - All features are branched off of the master branch
- **preview**
  - Connects to `production` data sources
  - Will have a custom domain `admin.preview.haldiskin.com`
    - More to come around our domain usage
  - **Reserved** for integration testing against `production`
    - These are big and likely slow changes, hard to test, must be perfect
- **xxxxx**
  - `feature/development` branches will connect to `staging` data
  - These should be highly `disposable` and the default approach
