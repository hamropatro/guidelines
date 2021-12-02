# Technical guidelines for Parewa Team

[This document](https://hamropatro.github.io/guidelines/) is intended for members (or future) members of the Parewa team. Please use this as a reference for any future or current projects that you're working on. In case of any issues/concerns please consult with a team lead or engineering manager.

## Git

Every commit should be made in a new branch(feature, hotfix, etc). Each pull
the request should be reviewed by at least one person other than oneself to be
merged.

- Follow [gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- Follow [semver](https://semver.org/) for api and apps versioning.
- Use prefixes to branche names(feat, bugfix, hotfix,) and separate prefix by ``/``. Eg: `feat/env-detection`,`hotfix/nullpointer`, etc.
- Feature branch can be reviewed by any peer before it is merged into develop.
- Hotfix branch should be reviewed by the team lead or engineering manager before it is merged into main.
- Develop branch should be reviewed by the team-lead/engineering manager before it is merged into the main.
- Use [conventional commit](https://www.conventionalcommits.org/en/v1.0.0/) guidelines for commit messages.

## Formatting

- Every code should be formatted before it is committed.
- Code formatting should be automated via tools(CI/githooks) or manually(npm run fmt).
- Each project should have a standard format configuration committed into the git.
  For example: prettier.json.
- For each type of project(backend or frontend, a template will be created and
  all new projects should start from those templates).

## Dockerfile

- Each project should have a dockerfile named `Dockerfile.ci` that can build in
  Dockerhub CI successfully. You should use multistage builds if needed.
- Each project can have Dockerfile that optimizes for speed of build by copying local files into the image and hence not requiring multistage builds.
- You should never push any image other than `:latest` to the dockerhub. All other images should be built in dockerhub CI using tags.

## Deployment

- All the deployments should be made in k8s.
- imagePullPolicy: `Always` in dev and `IfNotPresent` for production.
- image tag: `:latest` in dev and `x.y.z` in prod. Production images should only be built and pushed by dockerhub and never manually.
- Tagging should be done to git commit and docker hub should watch for those tags and build docker images automatically.
- Production server will watch for new docker image tags in docker hub and then create a pull request in gitops repo which should be manually merged to be deployed to production. Merging of the PR should be done by Team Lead or Manager.
- Regular release should be at least 1 day prior to a holiday and in the morning.
- All components of a service (client-side frontend, cms frontend, backend API service) should be hosted under the same first party domain like: `/api` for backend, / for client-side frontend and `/admin` or `/cms` for cms frontend. To be away from CORS issue :)

## Backend

See template [micronaut](https://github.com/hamropatro/micronaut).

- Languages: Java with Micronaut framework.
- All the backends should implement
  - health checks: readiness and liveness
  - open tracing clients
  - swagger endpoint
- Unix based OS: MacOs or Linux
- IDE: Intellij IDEA
- Logs: only error logs in the production
- CORS should only be enabled for same first party domain.

## Frontend

See template [react-ant-cms](https://github.com/hamropatro/react-ant-cms).

- All the configs should be configurable via environment variables
- Nextjs with Typescript
- UI frame-work: Framework7(client-side), ant-design for cms. Can be changed according to need.
- Use of inline CSS is discouraged
- Use of `!important` is highly discouraged. One exception is when you need to override the style from dependencies.
- No logs should be visible on production deployment. It is advised to use debugger instead.
- IDE: VS-Code or its derivatives and/or Intellij or its derivatives
- For client-side: Light House score should always be above `80%` in each category before it can be deployed to production.

## Maintainer

The Parewa Team
