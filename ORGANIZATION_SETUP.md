# PowerCyber Lab GitHub Organization Setup

## Organization

GitHub organization:

```text
PowerCyber-Laboratory-ISU
```

Organization page:

```text
https://github.com/PowerCyber-Laboratory-ISU
```

## Profile

Suggested profile text:

```text
PowerCyber Lab
Iowa State University

Research on cybersecurity, power systems, cyber-physical infrastructure, and resilient energy systems.
```

## Owners

Keep at least two owners:

- `SouradeepB12`
- A backup faculty/admin owner

Avoid having only one owner. The lab should not depend on a single personal account.

## Teams

Recommended organization teams:

- `faculty`
- `postdocs`
- `phd-students`
- `masters-students`
- `undergraduate-researchers`
- `external-collaborators`
- `project-leads`
- `doe-cyderms`

## Repository Visibility

Default recommendation:

- Active DOE project repositories: private
- Published software: public after approval
- Governance/template repositories: private or public depending on lab preference
- Sensitive data repositories: private with limited team access

## Organization Security Settings

Recommended settings:

- Require two-factor authentication.
- Restrict repository creation to owners or trusted project leads.
- Restrict public repository creation.
- Enable secret scanning and push protection when available.
- Review outside collaborators quarterly.

## Default Branch Rules

For important repositories, protect `main`:

- Require pull request before merge.
- Require at least one approving review.
- Require status checks when CI is added.
- Do not allow force pushes.
- Do not allow deletion.

## Repository Naming

Use clear names for project repositories:

```text
DOE-CyDERMS
DOE-<ProjectName>
DOE-<ProjectName>-Data
DOE-<ProjectName>-Software
```

Prefer one repository per project unless access control, data size, or release policy requires separation.