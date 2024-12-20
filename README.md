<img src="https://github.com/engswee/flashpipe/raw/main/docs/images/logo/flashpipe_logo_wording.png" alt="FlashPipe Logo" width="200" height="140"/>


# Companion GitHub Action for FlashPipe

This action provides a simplified approach for using [FlashPipe](https://github.com/engswee/flashpipe) in [GitHub Actions](https://github.com/features/actions) workflows.

It provides the following actions which execute their corresponding FlashPipe CLI command.

|CLI command|GitHub action|
|---|---|
|[update artifact](#update-artifact)|engswee/flashpipe-action/update/artifact@v1|
|[update package](#update-package)|engswee/flashpipe-action/update/package@v1|
|[deploy](#deploy)|engswee/flashpipe-action/deploy@v1|
|[sync](#sync)|engswee/flashpipe-action/sync@v1|
|[sync apim](#sync-apim)|engswee/flashpipe-action/sync/apim@v1|
|[snapshot](#snapshot)|engswee/flashpipe-action/snapshot@v1|
|[snapshot restore](#snapshot-restore)|engswee/flashpipe-action/snapshot/restore@v1|


## Usage
These actions are only valid when the workflow is executed in a [FlashPipe](https://hub.docker.com/r/engswee/flashpipe) container.
```yaml
jobs:
  update:
    runs-on: ubuntu-latest
    container:
      image: engswee/flashpipe:latest
```


### update artifact
```yaml
- uses: engswee/flashpipe-action/update/artifact@v1
  with:
    # Host for tenant management node of Cloud Integration
    # Required
    tmn-host:

    # User ID for Basic Auth
    # Required (for Basic Auth)
    tmn-userid:

    # Password for Basic Auth
    # Required (for Basic Auth)
    tmn-password:

    # Host for OAuth token server
    # Required (for OAuth)
    oauth-host:

    # Client ID for using OAuth
    # Required (for OAuth)
    oauth-clientid:

    # Client Secret for using OAuth
    # Required (for OAuth)
    oauth-clientsecret:

    # Path for OAuth token server
    # Optional
    # Default: /oauth/token
    oauth-path:

    # ID of artifact
    # Required
    artifact-id: 

    # Name of artifact
    # Optional
    # Default: Uses value of artifact-id when not provided
    artifact-name: 

    # ID of Integration Package
    # Required
    package-id: 

    # Name of Integration Package
    # Optional
    # Default: Uses value of package-id when not provided
    package-name:

    # Directory containing contents of designtime artifact - relative to root of Git repository
    # Required
    dir-artifact-relative: 

    # Artifact type. Allowed values: Integration, MessageMapping, ScriptCollection, ValueMapping
    # Optional
    # Default: Integration
    artifact-type:

    # Use a different MANIFEST.MF file instead of default META-INF/MANIFEST.MF
    # Optional
    file-manifest: 

    # Use a different parameters.prop file instead of default src/main/resources/parameters.prop
    # Optional
    file-param:

    # Comma-separated source-target ID pairs for converting script collection references during create/update
    # Optional
    script-collection-map:

    # Show debug logs
    # Optional
    # Default: false
    debug:
```

### update package
```yaml
- uses: engswee/flashpipe-action/update/package@v1
  with:
    # Host for tenant management node of Cloud Integration
    # Required
    tmn-host:

    # User ID for Basic Auth
    # Required (for Basic Auth)
    tmn-userid:

    # Password for Basic Auth
    # Required (for Basic Auth)
    tmn-password:

    # Host for OAuth token server
    # Required (for OAuth)
    oauth-host:

    # Client ID for using OAuth
    # Required (for OAuth)
    oauth-clientid:

    # Client Secret for using OAuth
    # Required (for OAuth)
    oauth-clientsecret:

    # Path for OAuth token server
    # Optional
    # Default: /oauth/token
    oauth-path:

    # Path to location of package file - relative to root of Git repository
    # Required
    package-file-relative:

    # Show debug logs
    # Optional
    # Default: false
    debug:
```

### deploy
```yaml
- uses: engswee/flashpipe-action/deploy@v1
  with:
    # Host for tenant management node of Cloud Integration
    # Required
    tmn-host:

    # User ID for Basic Auth
    # Required (for Basic Auth)
    tmn-userid:

    # Password for Basic Auth
    # Required (for Basic Auth)
    tmn-password:

    # Host for OAuth token server
    # Required (for OAuth)
    oauth-host:

    # Client ID for using OAuth
    # Required (for OAuth)
    oauth-clientid:

    # Client Secret for using OAuth
    # Required (for OAuth)
    oauth-clientsecret:

    # Path for OAuth token server
    # Optional
    # Default: /oauth/token
    oauth-path:

    # Comma separated list of artifact IDs
    # Required
    artifact-ids:

    # Artifact type. Allowed values: Integration, MessageMapping, ScriptCollection, ValueMapping
    # Optional
    # Default: Integration
    artifact-type:

    # Perform version comparison of design time against runtime before deployment
    # Optional
    # Default: true
    compare-versions: 

    # Delay (in seconds) between each check of artifact deployment status
    # Optional
    # Default: 30
    delay-length:

    # Max number of times to check for artifact deployment status
    # Optional
    # Default: 10
    max-check-limit:

    # Show debug logs
    # Optional
    # Default: false
    debug:
```

### sync
This action includes an implicit `git push` when syncing from tenant to Git, so the workflow does not require an additional push step.
```yaml
- uses: engswee/flashpipe-action/sync@v1
  with:
    # Host for tenant management node of Cloud Integration
    # Required
    tmn-host:

    # User ID for Basic Auth
    # Required (for Basic Auth)
    tmn-userid:

    # Password for Basic Auth
    # Required (for Basic Auth)
    tmn-password:

    # Host for OAuth token server
    # Required (for OAuth)
    oauth-host:

    # Client ID for using OAuth
    # Required (for OAuth)
    oauth-clientid:

    # Client Secret for using OAuth
    # Required (for OAuth)
    oauth-clientsecret:

    # Path for OAuth token server
    # Optional
    # Default: /oauth/token
    oauth-path:

    # ID of Integration Package
    # Required
    package-id:

    # Root directory of Git repository
    # Optional
    # Default: ${{ github.workspace }}
    dir-git-repo:

    # Directory containing contents of artifacts - relative to root directory of Git repository
    # Optional
    dir-artifacts-relative: 

    # Target of sync. Allowed values: git, tenant
    # Optional
    # Default: git
    target:

    # Name artifact directory by ID or Name. Allowed values: ID, NAME
    # Optional
    # Default: ID
    dir-naming-type:

    # Handling when artifact is in draft version. Allowed values: SKIP, ADD, ERROR
    # Optional
    # Default: SKIP
    draft-handling:

    # List of included artifact IDs
    # Optional
    ids-include:

    # List of excluded artifact IDs
    # Optional
    ids-exclude:

    # Message used in commit
    # Optional
    # Default: Sync repo from tenant
    git-commit-msg:

    # User used in commit
    # Optional
    # Default: github-actions[bot]
    git-commit-user:

    # Email used in commit
    # Optional
    # Default: 41898282+github-actions[bot]@users.noreply.github.com
    git-commit-email:

    # Comma-separated source-target ID pairs for converting script collection references during sync
    # Optional
    script-collection-map:

    # Sync details of Integration Package
    # Optional
    # Default: false
    sync-package-details:

    # Show debug logs
    # Optional
    # Default: false
    debug:
```

### sync apim
This action includes an implicit `git push` when syncing from tenant to Git, so the workflow does not require an additional push step.
```yaml
- uses: engswee/flashpipe-action/sync/apim@v1
  with:
    # Host for Developer Portal for API Management
    # Required
    tmn-host:

    # Host for OAuth token server
    # Required (for OAuth)
    oauth-host:

    # Client ID for using OAuth
    # Required (for OAuth)
    oauth-clientid:

    # Client Secret for using OAuth
    # Required (for OAuth)
    oauth-clientsecret:

    # Path for OAuth token server
    # Optional
    # Default: /oauth/token
    oauth-path:

    # Root directory of Git repository
    # Optional
    # Default: ${{ github.workspace }}
    dir-git-repo:

    # Directory containing contents of artifacts - relative to root directory of Git repository
    # Optional
    dir-artifacts-relative: 

    # Target of sync. Allowed values: git, tenant
    # Optional
    # Default: git
    target:

    # List of included artifact IDs
    # Optional
    ids-include:

    # List of excluded artifact IDs
    # Optional
    ids-exclude:

    # Message used in commit
    # Optional
    # Default: Sync repo from tenant
    git-commit-msg:

    # User used in commit
    # Optional
    # Default: github-actions[bot]
    git-commit-user:

    # Email used in commit
    # Optional
    # Default: 41898282+github-actions[bot]@users.noreply.github.com
    git-commit-email:

    # Show debug logs
    # Optional
    # Default: false
    debug:
```

### snapshot
This action includes an implicit `git push`, so the workflow does not require an additional push step.
```yaml
- uses: engswee/flashpipe-action/snapshot@v1
  with:
    # Host for tenant management node of Cloud Integration
    # Required
    tmn-host:

    # User ID for Basic Auth
    # Required (for Basic Auth)
    tmn-userid:

    # Password for Basic Auth
    # Required (for Basic Auth)
    tmn-password:

    # Host for OAuth token server
    # Required (for OAuth)
    oauth-host:

    # Client ID for using OAuth
    # Required (for OAuth)
    oauth-clientid:

    # Client Secret for using OAuth
    # Required (for OAuth)
    oauth-clientsecret:

    # Path for OAuth token server
    # Optional
    # Default: /oauth/token
    oauth-path:

    # Root directory of Git repository
    # Optional
    # Default: ${{ github.workspace }}
    dir-git-repo:

    # Directory containing contents of artifacts (grouped by packages) - relative to root directory of Git repository
    # Optional
    dir-artifacts-relative: 

    # Handling when artifact is in draft version. Allowed values: SKIP, ADD, ERROR
    # Optional
    # Default: SKIP
    draft-handling:

    # List of included package IDs
    # Optional
    ids-include:

    # List of excluded package IDs
    # Optional
    ids-exclude:

    # Message used in commit
    # Optional
    # Default: Tenant snapshot of <current_timestamp>
    git-commit-msg:

    # User used in commit
    # Optional
    # Default: github-actions[bot]
    git-commit-user:

    # Email used in commit
    # Optional
    # Default: 41898282+github-actions[bot]@users.noreply.github.com
    git-commit-email:

    # Sync details of Integration Package
    # Optional
    # Default: true
    sync-package-details:

    # Show debug logs
    # Optional
    # Default: false
    debug:
```

### snapshot restore
```yaml
- uses: engswee/flashpipe-action/snapshot/restore@v1
  with:
    # Host for tenant management node of Cloud Integration
    # Required
    tmn-host:

    # User ID for Basic Auth
    # Required (for Basic Auth)
    tmn-userid:

    # Password for Basic Auth
    # Required (for Basic Auth)
    tmn-password:

    # Host for OAuth token server
    # Required (for OAuth)
    oauth-host:

    # Client ID for using OAuth
    # Required (for OAuth)
    oauth-clientid:

    # Client Secret for using OAuth
    # Required (for OAuth)
    oauth-clientsecret:

    # Path for OAuth token server
    # Optional
    # Default: /oauth/token
    oauth-path:

    # Root directory of Git repository
    # Optional
    # Default: ${{ github.workspace }}
    dir-git-repo:

    # Directory containing contents of artifacts (grouped by packages) - relative to root directory of Git repository
    # Optional
    dir-artifacts-relative:

    # List of included package IDs
    # Optional
    ids-include:

    # List of excluded package IDs
    # Optional
    ids-exclude:

    # Show debug logs
    # Optional
    # Default: false
    debug:
```

## Examples

The following repository on GitHub provides examples of different use cases of of these actions.

[https://github.com/engswee/flashpipe-demo](https://github.com/engswee/flashpipe-demo)

## License

This project is licensed under the terms of Apache License, Version 2.0 - see the [LICENSE](LICENSE) file for details.
