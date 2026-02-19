# Changelog

## 3.2.0

- Upgrade Redash from v24.04.0-dev to v25.8.0 (latest stable)
- Update default image repository from `redash/preview` to `redash/redash` for stable releases
- Upgrade PostgreSQL dependency from ^15.2.0 to ^18.2.0 (latest: 18.2.4)
- Upgrade Redis dependency from ^19.1.0 to ^24.1.0 (latest: 24.1.3)
- **NEW**: Added optional automatic PostgreSQL migration hooks for major version upgrades (15→18)
  - Enable with `postgresqlMigration.enabled: true` and configure a PVC for storage
  - See [README](charts/redash/README.md#upgrading) for details
- See upgrade notes in [README](charts/redash/README.md#upgrading)

**CRITICAL Upgrade Notes:**
- **Always backup your PostgreSQL database before upgrading**
- **Redash schema migrations** will run automatically via Helm hooks (handles Redash app schema changes)
- **PostgreSQL version upgrade (15→18)**:
  - **Option 1**: Enable automatic migration hooks (requires PVC) - see README
  - **Option 2**: Manual migration using `pg_dump`/`pg_restore` - see README
- PostgreSQL 15 → 18 is a major version jump requiring data migration
- Redis 19 → 24 upgrade should be automatic, but test thoroughly
- Test in staging environment first, especially if upgrading from v24.x
- Review Bitnami PostgreSQL and Redis chart changelogs for breaking changes

## 3.0.1 (unreleased)

- Change scheduler deployment strategy type to Recreate. (#121)

## 3.0.0

- Initial release supporting Redash v10.x
- See upgrade notes in [README](README.md#upgrading)

## 2.4.0

- Final v2.x release (except for critical fixes)
- Final release to support Redash v8.x
- Redis password is now required
- Kubernetes minimum version increased to v19.x
- Helm 2 depreciated, will be removed in a future version
- Supports stable Ingress API
- Add support for SQL Alchemy pool pre-ping configuration
- Add support for configurable worker pod labels
- Expand configurability of install/upgrade hooks

## 2.3.0

- Added externalPostgreSQLSecret / externalRedisSecret
- Depreciated envSecretName (plan to remove in 3.0.0 chart)
- Updated docs to make defaults clearer

## 2.2.0

- Update docs to Helm Docs 1.4+ format
- Removed duplicated env params that already come from "redash.env"
- Updated Redash environment variables and associated docs
- Updated CI to use Helm v3.4.1

## 2.1.0

- Added redash.samlSchemeOverride
- Added envSecretName
- Expanded service configuration: .service.annotations and .service.loadBalancerIP
- Moved postgresql and redis charts to Bitnami repo and update to latest patch release versions
- Updated CI to use Helm v2.16.12 and v3.3.4
- Updated CI to drop k8s v1.15, add v1.17, v1.18 and v1.19
- Improved CI release publishing flow

## 2.0.0

- Made secrets required, rather than auto-generating to avoid them [changing on upgrade](https://github.com/helm/charts/issues/5167)
- Variable additions and template updates to bring in line with Helm 3 chart template
- Add support for external secrets
- Extended CI testing for multiple k8s and Helm versions
- Extended CI testing for testing major version upgrades
- Moved install and upgrade logic to Helm hooks
- Added basic connectivity test hook for `helm test`
- Created values for each environment variable accepted by Redash

## 1.2.0

- Upgrade Redash to 8.0.2.b37747
- Upgrade PostgreSQL chart (the old version used depreciated APIs) and image tag
- Upgrade Redis chart

## 1.1.0

- Initial release of chart on getredash namespace
- Upgrade Redash to 8.0.1.b33387
- Add support for external Redis server
- Add CI linting/testing and release automation

## Pre-release

For pre-release versions please see the [pull request](https://github.com/helm/charts/pull/5071) where this was originally developed.
