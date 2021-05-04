# Contributing

> 🚚 The goal is to ship small features, quickly, and frequently.

In order to do this we need to break our features down into smaller units of work and `🤖 automate` as much as possible. Testing should remain easy and consistent with production but `breakable` if necessary. Locally should mirror that of `staging`, with as few network dependencies as possible.

1. Create a _feature-branch_ based on `master`
2. Create a PR and leave it in `draft` mode
3. This will give us a deployment connected to `staging`
   1. use the `preview` branch if you need `production` data
4. Review Process
   1. Take it out of `draft` mode
   2. Assign a reviewer or two
   3. Address feedback, learn and teach
5. Merge into master
   1. This will automate the deployment
   2. Watch Sentry for any new errors
   3. Validate the change on production

## Review Process

Right now we simply have a very small headcount when it comes to folks that can actually review the code and test for us.

- Julia tests UI and functionality
- Matt + Marc + Steve + Nik
  - Review diffs, assign across PR's

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

## 🌎 Domains

We currently have two TLD's that we're managing, **haldi.com** and **haldiskin.com**. From what I understand the preferred domain is **haldi.com** and we've somewhat recently acquired it.

### Redirect top-level-domains

- `*.haldiskin.com` -> `*.haldi.com`
  - Better for SEO to have one domain
  - Better for our users as its simple

### Use ".dev" exclusively for testing

- `admin.haldiskin.dev`
  - Uses `staging` database
- `admin.preview.haldiskin.dev`
  - Uses `production` database

## 🙈 Environment Variables

NextJS has improved its overall support and now supports updating variables within their UI. See [the docs](https://vercel.com/docs/environment-variables) for more info.

> 👀 ⚠️ 👀
>
> Next.js will replace `process.env.customKey` with 'my-value' at build time. Trying to destructure process.env variables **won't work** due to the nature of webpack DefinePlugin.
>
> ⚠️ ⏰ ⚠️

### Naming Convention

The `name` of the service will be used as a suffix to all values, followed by the `actor` and `description` or key.

```bash
# Examples from the "Survey App"
SURVEY_ALGOLIA_APP_ID="XXXXXXXXX"
SURVEY_ALGOLIA_API_KEY="XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
SURVEY_FIREBASE_ENV="staging"
SURVEY_WEBAPP_URL="http://localhost:8000"
```

### System Environment Variables

We currently host this application on Vercel which exposes some "[system-environment-variables](https://vercel.com/docs/environment-variables#system-environment-variables)" which we make use of.

```tsx
// Vercel deployment(s) only
const VERCEL_GIT_COMMIT_REF = process.env NEXT_PUBLIC_VERCEL_GIT_COMMIT_REF;
const VERCEL_ENV = process.env.NEXT_PUBLIC_VERCEL_ENV;
const VERCEL_URL = process.env.NEXT_PUBLIC_VERCEL_URL;
```
