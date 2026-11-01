# woldtwerk-websites/scaffold

Shared Drupal scaffold files for the woldtwerk-websites sites: DDEV, Vite+, CI
workflows and tooling config. The package itself contains no Drupal code — it
only ships the files that are copied into a site by the
`drupal-scaffold` Composer plugin.

## Using it in a site

Add the VCS repository to the site's `composer.json`:

```json
{
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/woldtwerk-websites/scaffold",
      "only": ["woldtwerk-websites/*"]
    }
  ]
}
```

Then require it:

```bash
composer require woldtwerk-websites/scaffold:^1.0
```

The Drupal scaffold plugin only manages packages that are explicitly allowed, so
add the package to `extra.drupal-scaffold.allowed-packages` in the site's
`composer.json`:

```json
{
  "extra": {
    "drupal-scaffold": {
      "allowed-packages": ["woldtwerk-websites/scaffold"]
    }
  }
}
```

## How the files are mapped

The mapping from scaffold package files to site paths lives in this package's
`composer.json` under `extra.drupal-scaffold.file-mapping`. The source files
themselves are kept in `assets/`, mirroring the paths they are copied to in the
site (for example `assets/.ddev/config.vite.yml` becomes
`[project-root]/.ddev/config.vite.yml`).

## Releases

Releases are cut by [release-please](https://github.com/googleapis/release-please)
from conventional commits on `main` using `release-please-config.json` and
`.release-please-manifest.json`. `feat` bumps the minor version, `fix` bumps the
patch version, and a `!` (or `BREAKING CHANGE` footer) bumps the major version.
The resulting git tag is what the sites require via Composer.

The package's own `README.md` is not part of `file-mapping`, so it is never
copied into a site.
