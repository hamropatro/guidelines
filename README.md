# Coding guidelines

## Git Flow

Please follow
[gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
for git. Gitflow can be ignored before first release if single person is working
on a codebase.

Every commit should be made in new branch(feature, hotfix, etc). Each pull
request should be reviewed by at least one person other than oneself to be
merged.

- Feature branch can be reviewed by any peer before it is merged into develop.
- Hotfix branch should be reviewed by team lead or engineering manager before it
  is merged into main.
- Develop branch should be reviewed by team-lead/engineering manager before it
  is merged into main.

## Formatting

- Every code should be formatted before it is committed.
- Code formatting should be automated via tools(CI/githooks) or manually(npm run
  fmt).
- Each project should have standard format configuration committed into the git.
  For example: prettier.json.
- For each type of project(backend or frontend, a template will be created and
  all new projects should start from those templates).

## Dockerfile

- Each project should have a dockerfile named Dockerfile.ci that can build in
  Dockerhub CI successfully. You should use multistage builds if needed.
- Each project can have Dockerfile that optimizes for speed of build by copying
  local files into the image and hence not requiring multistage builds.
- You should never push any image other than :latest to the dockerhub. All other
  images should be build in dockerhub CI using tags.

## Deployment

- All the deployments should be made in k8s.
- imagePullPolicy: `Always` in dev and `IfNotPresent` for production.
- image tag: :latest in dev and `x.x.x` in prod. Production images should only
  be build and pushed by dockerhub and never manually.
- Tagging should be done at git level and docker hub should watch for those tags
  and build docker images automatically.
- Production server will watch for new docker image tags and then create a pull
  request in gitops repo which should be manually merged to be deployed to
  production. Merging of the PR should be done by Team Lead or Manager.

## Backend

- Languages: Java with Micronaut.
- All the backends should implement
  - health checks: readiness and liveness
  - open tracing clients
  - swagger endpoint
- Unix based OS: MacOs or Linux
- IDE: Intellij IDEA
- Logs: only error logs in production

## Frontend

- All the configs should be configurable via environment variables
- Nextjs with Typescript
- UI frame work: Framework7(client side), ant-design for cms. Can be changed
  according to need.
- Use of inline CSS is discouraged
- Use of !important is not allowed.
- No logs should be visible on production deployment. It is advised to use
  debugger instead.
- IDE: VS-Code or its derivatives.
- Light House score should always be above 80% in each category before it can be
  deployed to production.

## Maintainer

Parewa Team
