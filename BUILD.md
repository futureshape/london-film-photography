BUILD instructions
==================

This project is a Jekyll site. This document describes how to build and preview it locally, notes about common native-gem issues on macOS (Apple Silicon), and recommended deploy options.

Prerequisites
-------------
- macOS: Xcode command line tools (for native gems):

```bash
xcode-select --install
```

- Ruby (use a version manager like `rbenv` or `rvm` recommended). The project uses Bundler; a modern Ruby (2.7+ or 3.x) is fine. If you use the system Ruby, some commands may require `sudo`.

- Bundler (installed via `gem install bundler` if not present).

Quick local setup (safe, local gem install)
-----------------------------------------
Run these from the repository root.

```bash
cd /path/to/london-film-photography

# Install gems into the project (avoids sudo/system gems)
bundle config set --local path 'vendor/bundle'

# On Apple Silicon (M1/M2) you may need to force building native gems
# for the local machine. This ensures extensions like `ffi`/`sassc` are compiled
# for your architecture:
bundle config set --local force_ruby_platform true

# Install/update gems
bundle install --jobs 4 --retry 3

# If Dependabot requested a rexml update, update only that gem:
# bundle update rexml --conservative
```

Build & preview
---------------
Build the site and serve it locally using the project's Gemfile (use `bundle exec`):

```bash
# Build into _site
bundle exec jekyll build

# Start a local server on port 4000 (accessible at http://localhost:4000)
bundle exec jekyll serve --host 0.0.0.0 --port 4000
```

Common issues and fixes
-----------------------
- ffi / native gem LoadError (incompatible architecture):
  - If you see an error about `ffi_c` or "incompatible architecture (have 'x86_64', need 'arm64')",
    set `force_ruby_platform` and reinstall gems (see Quick local setup above).

- Permission errors installing gems globally:
  - Use the local `vendor/bundle` approach above, or install a Ruby via `rbenv`/`rvm` to avoid `sudo`.

- Missing layout warning for `404.html`:
  - The build may warn: "Layout 'default' requested in 404.html does not exist." This is non-fatal; to remove
    the warning either create `_layouts/default.html` or edit `404.html` to use an existing layout.

- Duplicate watch errors when serving:
  - Jekyll/watch may report directories already being watched. It's harmless but can be ignored; disable `--watch`
    if it bothers you, or run `bundle exec jekyll build` instead of `serve`.

Security & dependency notes
--------------------------

- Use `bundle outdated` to review other updates. Update conservatively and run a build after changes.

Deployment
---------------------

The live site (http://londonfilm.photography/) is deployed from the main branch via AWS Amplify.