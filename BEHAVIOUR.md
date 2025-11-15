# PNPM Package Behavior Documentation

## Overview

The pnpm repository is a **large TypeScript monorepo** with over **150+ packages** organized into logical categories by function. It implements a fast, disk-space efficient package manager using content-addressable storage and hardlinks.

### High-Level Architecture

```
pnpm (v11.0.0-alpha.1)
├── Core Installation Engine (@pnpm/core)
├── Package Resolution & Fetching
├── Lockfile Management
├── Workspace Management
├── Configuration System
├── CLI Command System
├── Storage/Cache System
└── Supporting Utilities
```

---

## Packages by Category

### 1. **CLI System** (`/cli` - 6 packages)
Handles command-line argument parsing, help text, and command metadata.

| Package | Description |
|---------|------------|
| `@pnpm/command` | Types and utils for pnpm commands |
| `@pnpm/cli-utils` | CLI utility functions |
| `@pnpm/cli-meta` | CLI metadata and version info |
| `@pnpm/parse-cli-args` | Parser for CLI arguments |
| `@pnpm/default-reporter` | Default output reporter for CLI |
| `@pnpm/common-cli-options-help` | Shared CLI options help text |

### 2. **Core Package Manager Engine** (`/pkg-manager` - 16 packages)
The heart of pnpm - handles installation, linking, hoisting, and dependency resolution.

| Package | Description |
|---------|------------|
| `@pnpm/core` | **Fast, disk space efficient installation engine** |
| `@pnpm/client` | Creates package resolve and fetch functions |
| `@pnpm/headless` | Headless installation (without workspace features) |
| `@pnpm/resolve-dependencies` | Resolves dependency graph from lockfile |
| `@pnpm/package-requester` | Requests packages from store |
| `@pnpm/direct-dep-linker` | Links direct dependencies |
| `@pnpm/hoist` | Standard hoisting algorithm |
| `@pnpm/real-hoist` | Real hoisting with node_modules structure |
| `@pnpm/link-bins` | Links package executables |
| `@pnpm/remove-bins` | Removes package executables |
| `@pnpm/modules-cleaner` | Cleans up unused node_modules |
| `@pnpm/modules-yaml` | Manages `.modules.yaml` metadata |
| `@pnpm/package-bins` | Manages package bin entries |
| `@pnpm/get-context` | Retrieves context for package operations |
| `@pnpm/read-projects-context` | Reads workspace project contexts |
| `@pnpm/plugin-commands-installation` | Install/add/remove commands |

### 3. **Dependency Resolution** (`/resolving` - 9 packages)
Resolves package references to specific versions and locations.

| Package | Description |
|---------|------------|
| `@pnpm/npm-resolver` | **Resolver for npm-hosted packages** |
| `@pnpm/default-resolver` | Default resolver (routes to appropriate resolver) |
| `@pnpm/git-resolver` | Resolves git-hosted packages |
| `@pnpm/local-resolver` | Resolves local file packages |
| `@pnpm/bun-resolver` | Resolves Bun package registry |
| `@pnpm/deno-resolver` | Resolves Deno packages |
| `@pnpm/tarball-resolver` | Resolves tarball URLs |
| `@pnpm/jsr-specifier-parser` | Parses JSR specifiers |
| `@pnpm/resolver-base` | Base classes and types for resolvers |

### 4. **Package Fetching** (`/fetching` - 6 packages)
Downloads/extracts packages from registries and sources.

| Package | Description |
|---------|------------|
| `@pnpm/tarball-fetcher` | **Fetcher for tarball-hosted packages** |
| `@pnpm/directory-fetcher` | Fetches from local directories |
| `@pnpm/git-fetcher` | Fetches from git repositories |
| `@pnpm/binary-fetcher` | Fetches pre-built binaries |
| `@pnpm/pick-fetcher` | Routes to appropriate fetcher |
| `@pnpm/fetcher-base` | Base classes for fetchers |

### 5. **Storage & Cache** (`/store` - 11 packages)
Manages the content-addressable filesystem (CAFS) for efficient storage.

| Package | Description |
|---------|------------|
| `@pnpm/store.cafs` | **Content-addressable filesystem for package storage** |
| `@pnpm/cafs-types` | Types for CAFS system |
| `@pnpm/create-cafs-store` | Factory for creating CAFS stores |
| `@pnpm/package-store` | Package store management |
| `@pnpm/store-path` | Determines store directory path |
| `@pnpm/store-controller-types` | Types for store controllers |
| `@pnpm/store-connection-manager` | Manages store connections |
| `@pnpm/plugin-commands-store` | `pnpm store` commands |
| `@pnpm/plugin-commands-store-inspecting` | Store inspection commands |
| `@pnpm/plugin-commands-server` | Store server commands |
| `@pnpm/server` | Server for store access |

### 6. **Lockfile Management** (`/lockfile` - 14 packages)
Parses, writes, and manipulates `pnpm-lock.yaml` files.

| Package | Description |
|---------|------------|
| `@pnpm/lockfile.types` | **Types for the pnpm-lock.yaml lockfile** |
| `@pnpm/lockfile.fs` | Lockfile file system operations |
| `@pnpm/lockfile.utils` | Lockfile utility functions |
| `@pnpm/lockfile.walker` | Walks lockfile dependency tree |
| `@pnpm/lockfile.filtering` | Filters lockfile entries |
| `@pnpm/lockfile.merger` | Merges lockfiles |
| `@pnpm/lockfile.verification` | Verifies lockfile integrity |
| `@pnpm/lockfile.pruner` | Removes unused entries from lockfile |
| `@pnpm/lockfile.preferred-versions` | Manages preferred versions |
| `@pnpm/lockfile-to-pnp` | Converts lockfile to PnP format |
| `@pnpm/detect-dep-types` | Detects dependency types |
| `@pnpm/lockfile.audit` | Audit lockfile for vulnerabilities |
| `@pnpm/plugin-commands-audit` | `pnpm audit` command |
| `@pnpm/lockfile.settings-checker` | Validates lockfile settings |

### 7. **Configuration** (`/config` - 10 packages)
Manages pnpm configuration and settings.

| Package | Description |
|---------|------------|
| `@pnpm/config` | **Gets configuration options for pnpm** |
| `@pnpm/config-writer` | Writes config to files |
| `@pnpm/matcher` | Pattern matching for config |
| `@pnpm/normalize-registries` | Normalizes registry URLs |
| `@pnpm/pick-registry-for-package` | Selects registry for packages |
| `@pnpm/parse-overrides` | Parses dependency overrides |
| `@pnpm/package-is-installable` | Checks if package can be installed |
| `@pnpm/version-policy` | Manages version policies |
| `@pnpm/deps-installer` | Installs config dependencies |
| `@pnpm/plugin-commands-config` | `pnpm config` command |

### 8. **Workspace Management** (`/workspace` - 12 packages)
Handles monorepo/workspace operations.

| Package | Description |
|---------|------------|
| `@pnpm/find-workspace-dir` | **Finds the root of a pnpm workspace** |
| `@pnpm/workspace.find-packages` | Finds packages in workspace |
| `@pnpm/workspace.read-manifest` | Reads workspace manifest files |
| `@pnpm/workspace.pkgs-graph` | Builds workspace dependency graph |
| `@pnpm/workspace.filter-packages` | Filters workspace packages |
| `@pnpm/filter-packages-from-dir` | Filters packages from directory |
| `@pnpm/workspace.resolve-workspace-range` | Resolves workspace ranges |
| `@pnpm/workspace.spec-parser` | Parses workspace specs |
| `@pnpm/workspace.state` | Tracks workspace state |
| `@pnpm/workspace.sort-packages` | Sorts packages topologically |
| `@pnpm/manifest-writer` | Writes manifest files |
| `@pnpm/injected-deps-syncer` | Syncs injected dependencies |

### 9. **Dependency Graph** (`/deps` - 3 packages)
Builds and analyzes dependency graphs.

| Package | Description |
|---------|------------|
| `@pnpm/deps.graph-builder` | **Builds dependency graph from lockfile** |
| `@pnpm/deps.graph-sequencer` | Sequences dependencies topologically |
| `@pnpm/deps.status` | Reports dependency status |

### 10. **File System Operations** (`/fs` - 9 packages)
Low-level file system utilities.

| Package | Description |
|---------|------------|
| `@pnpm/fs.packlist` | **Get list of files for npm package** |
| `@pnpm/fs.graceful-fs` | Graceful file system wrapper |
| `@pnpm/fs.v8-file` | V8 file serialization |
| `@pnpm/fs.hard-link-dir` | Creates hard-linked directories |
| `@pnpm/fs.symlink-dependency` | Creates symlinks for dependencies |
| `@pnpm/read-modules-dir` | Reads node_modules directory |
| `@pnpm/find-packages` | Finds package directories |
| `@pnpm/indexed-pkg-importer` | Imports packages with indexing |
| `@pnpm/is-empty-dir-or-nothing` | Checks if dir is empty |

### 11. **Network & Fetching** (`/network` - 3 packages)
Network operations and HTTP utilities.

| Package | Description |
|---------|------------|
| `@pnpm/fetch` | **node-fetch with retries** |
| `@pnpm/network.auth-header` | Generates auth headers |
| `@pnpm/fetching-types` | Types for fetching system |

### 12. **Execution & Lifecycle** (`/exec` - 9 packages)
Manages script execution and lifecycle.

| Package | Description |
|---------|------------|
| `@pnpm/exec.build-commands` | Executes build scripts |
| `@pnpm/exec.build-modules` | Builds native modules |
| `@pnpm/exec.lifecycle` | Manages lifecycle scripts |
| `@pnpm/exec.pkg-requires-build` | Checks if package needs building |
| `@pnpm/exec.pnpm-cli-runner` | Runs pnpm CLI commands |
| `@pnpm/exec.prepare-package` | Prepares package for use |
| `@pnpm/exec.run-npm` | Executes npm scripts |
| `@pnpm/plugin-commands-rebuild` | `pnpm rebuild` command |
| `@pnpm/plugin-commands-script-runners` | `pnpm run` command |

### 13. **Environment & Node.js** (`/env` - 5 packages)
Manages environment and Node.js versions.

| Package | Description |
|---------|------------|
| `@pnpm/env.path` | **Functions for changing PATH env variable** |
| `@pnpm/env.node.fetcher` | Fetches Node.js versions |
| `@pnpm/env.node.resolver` | Resolves Node.js versions |
| `@pnpm/env.system-node-version` | Detects system Node.js |
| `@pnpm/plugin-commands-env` | `pnpm env` command |

### 14. **Hooks & Plugins** (`/hooks` - 3 packages)
Extensibility through hooks and plugins.

| Package | Description |
|---------|------------|
| `@pnpm/hooks.pnpmfile` | Handles .pnpmrc.cjs hooks |
| `@pnpm/hooks.read-package-hook` | Read package hook system |
| `@pnpm/hooks.types` | Types for hooks |

### 15. **Package Manifest** (`/pkg-manifest` - 5 packages)
Reads and writes package.json files.

| Package | Description |
|---------|------------|
| `@pnpm/pkg-manifest.read-package-json` | Reads package.json |
| `@pnpm/pkg-manifest.read-project-manifest` | Reads project manifest |
| `@pnpm/pkg-manifest.write-project-manifest` | Writes project manifest |
| `@pnpm/pkg-manifest.manifest-utils` | Manifest utilities |
| `@pnpm/pkg-manifest.exportable-manifest` | Exportable manifest format |

### 16. **Patching** (`/patching` - 4 packages)
Manages dependency patches.

| Package | Description |
|---------|------------|
| `@pnpm/patching.apply-patch` | Applies patches to packages |
| `@pnpm/patching.config` | Patch configuration |
| `@pnpm/patching.types` | Types for patching |
| `@pnpm/plugin-commands-patching` | `pnpm patch` command |

### 17. **Cryptography** (`/crypto` - 3 packages)
Hash and crypto operations.

| Package | Description |
|---------|------------|
| `@pnpm/crypto.hash` | Hash functions |
| `@pnpm/crypto.object-hasher` | Object hashing |
| `@pnpm/crypto.shasums-file` | SHA-256 file operations |

### 18. **Deduplication** (`/dedupe` - 3 packages)
Checks for duplicate dependencies.

| Package | Description |
|---------|------------|
| `@pnpm/dedupe.check` | Checks for duplicates |
| `@pnpm/dedupe.issues-renderer` | Renders dedupe issues |
| `@pnpm/dedupe.types` | Types for deduplication |

### 19. **Package Review/Inspection** (`/reviewing` - 7 packages)
Lists, audits, and checks packages.

| Package | Description |
|---------|------------|
| `@pnpm/reviewing.list` | Lists installed packages |
| `@pnpm/reviewing.outdated` | Checks for outdated packages |
| `@pnpm/reviewing.dependencies-hierarchy` | Shows dependency tree |
| `@pnpm/reviewing.license-scanner` | Scans licenses |
| `@pnpm/plugin-commands-listing` | `pnpm list` command |
| `@pnpm/plugin-commands-outdated` | `pnpm outdated` command |
| `@pnpm/plugin-commands-licenses` | `pnpm licenses` command |

### 20. **Release & Publishing** (`/releasing` - 2 packages)
Handles package publishing and deployment.

| Package | Description |
|---------|------------|
| `@pnpm/plugin-commands-publishing` | `pnpm publish` command |
| `@pnpm/plugin-commands-deploy` | `pnpm deploy` command |

### 21. **Registry** (`/registry` - 2 packages)
Registry-related utilities.

| Package | Description |
|---------|------------|
| `@pnpm/registry.types` | Registry types |
| `@pnpm/registry.pkg-metadata-filter` | Filters package metadata |

### 22. **Tools** (`/tools` - 2 packages)
Special tools and utilities.

| Package | Description |
|---------|------------|
| `@pnpm/tools.plugin-commands-self-updater` | **Self-update command for pnpm** |
| `@pnpm/tools.path` | Path utilities |

### 23. **Miscellaneous Packages** (`/packages` - 15 packages)
Core utilities and helpers.

| Package | Description |
|---------|------------|
| `@pnpm/types` | Core TypeScript types |
| `@pnpm/logger` | **Logger for pnpm** |
| `@pnpm/error` | Error types and handling |
| `@pnpm/constants` | Constants and defaults |
| `@pnpm/dependency-path` | Dependency path parsing |
| `@pnpm/parse-wanted-dependency` | Parses dependency specs |
| `@pnpm/core-loggers` | Core logger implementations |
| `@pnpm/calc-dep-state` | Calculates dependency state |
| `@pnpm/naming-cases` | Case conversion utilities |
| `@pnpm/git-utils` | Git utilities |
| `@pnpm/render-peer-issues` | Renders peer dependency issues |
| `@pnpm/plugin-commands-setup` | `pnpm setup` command |
| `@pnpm/plugin-commands-init` | `pnpm init` command |
| `@pnpm/plugin-commands-doctor` | `pnpm doctor` command |
| `@pnpm/make-dedicated-lockfile` | Creates focused lockfiles |

### 24. **Completion & Utilities** (`/completion` - 1 package)
Shell completion support.

| Package | Description |
|---------|------------|
| `@pnpm/plugin-commands-completion` | Shell completion generator |

### 25. **Module Mounting** (`/modules-mounter` - 1 package)
Manages node_modules directory mounting (used by some integrations).

| Package | Description |
|---------|------------|
| `@pnpm/modules-mounter.daemon` | Daemon for mounting modules |

### 26. **Worker System** (`/worker` - 1 package)
Parallel processing for tarball extraction.

| Package | Description |
|---------|------------|
| `@pnpm/worker` | **Worker for extracting package tarballs to store** |

### 27. **Object & Text Utilities** (`/object`, `/text`, `/semver` - 5 packages)
Low-level utility packages.

| Package | Description |
|---------|------------|
| `@pnpm/object.key-sorting` | Sorts object keys |
| `@pnpm/object.property-path` | Property path utilities |
| `@pnpm/text.comments-parser` | Parses comments |
| `@pnpm/semver.peer-range` | Peer dependency ranges |

### 28. **Builder** (`/builder` - 1 package)
Build policy management.

| Package | Description |
|---------|------------|
| `@pnpm/builder.policy` | Filters dependencies allowed to be built |

### 29. **Cache Commands** (`/cache` - 2 packages)
Cache management commands.

| Package | Description |
|---------|------------|
| `@pnpm/cache.api` | **API for controlling the cache** |
| `@pnpm/cache.commands` | Cache management commands |

### 30. **Test & Build Utilities** (`/__utils__` - 12 packages)
Internal testing and build infrastructure.

| Package | Description |
|---------|------------|
| `@pnpm/assert-project` | Project assertion utilities |
| `@pnpm/assert-store` | Store assertion utilities |
| `@pnpm/prepare` | Test setup utilities |
| `@pnpm/test-fixtures` | Test fixture management |
| `@pnpm/test-ipc-server` | IPC server for tests |
| `@pnpm/jest-config` | Jest configuration |
| `@pnpm/eslint-config` | ESLint configuration |
| `@pnpm/tsconfig` | TypeScript configuration |
| `@pnpm/get-release-text` | Release notes generator |
| `@pnpm/scripts` | Build scripts |
| `@pnpm/build-artifacts` | Build artifact management |
| `@pnpm/prepare-temp-dir` | Temp directory setup |

---

## Key Architectural Insights

### 1. **Modular Design**
- Over 150 packages organized by functional domain
- Each package is independently publishable
- Clear separation of concerns

### 2. **Package Naming Conventions**
- Core packages: `@pnpm/package-name`
- Scoped by category: `@pnpm/category.package-name` (e.g., `@pnpm/lockfile.types`)
- Internal tools: `@pnpm-private/*` or `@pnpm/tools.*`

### 3. **Core Flow**
```
CLI Command → Config → Package Resolution → Fetching → Storage (CAFS) → Installation → Linking
```

### 4. **Content-Addressable Storage (CAFS)**
- Packages stored by content hash, not name
- Hard-linked into `node_modules` to save disk space
- Up to 2x more efficient than npm/yarn

### 5. **Workspace Support**
- Full monorepo support with `pnpm-workspace.yaml`
- Workspace packages can reference each other via `workspace:*` protocol
- Cross-workspace dependency resolution

### 6. **Plugin Architecture**
- Plugin command packages: `@pnpm/plugin-commands-*`
- Extensible via hooks (`.pnpmrc.cjs`)
- Commands: install, audit, config, env, rebuild, run, patch, etc.

---

## Summary Statistics

- **Total Packages**: 150+
- **Main Entry Point**: `pnpm` (the CLI)
- **Core Engine**: `@pnpm/core`
- **Language**: TypeScript (compiled to JavaScript)
- **Node.js Requirement**: >= 20.19
- **License**: MIT

This architecture makes pnpm highly modular, testable, and maintainable while providing a fast and efficient package management experience for JavaScript/Node.js projects.

---

## Peer Dependency Installation Behavior

### Issue: `pnpm i --fix-lockfile` vs `pnpm i` - Peers of Peers Installation

One of the key behavioral differences in pnpm is how **peers of peers** (transitive peer dependencies) are handled between `pnpm i` and `pnpm i --fix-lockfile`.

### The Difference

| Command | Behavior | Peer Resolution | Peers of Peers |
|---------|----------|-----------------|----------------|
| `pnpm i` | **Frozen Install** (when possible) | Skipped - uses existing lockfile | Uses what's already in lockfile |
| `pnpm i` | **Full Resolution** (when forced by changes) | Runs with `hoistPeers` enabled | Properly resolved if triggered |
| `pnpm i --fix-lockfile` | **Always Full Resolution** | Always runs with `hoistPeers` enabled | **Always resolved properly** |

### Root Cause Analysis

#### 1. **The `--fix-lockfile` Flag Implementation**

**Location:** `pkg-manager/plugin-commands-installation/src/install.ts:82`

The flag is defined as:
```typescript
'fix-lockfile': Boolean  // Line 82
```

Help text: "Fix broken lockfile entries automatically" (Line 154)

#### 2. **How `--fix-lockfile` Forces Full Resolution**

**Location:** `pkg-manager/core/src/install/index.ts:430`

```typescript
let needsFullResolution = outdatedLockfileSettings ||
  opts.fixLockfile ||                          // Forces full resolution
  !upToDateLockfileMajorVersion ||
  opts.forceFullResolution
```

When `fixLockfile` is true:
- Forces `needsFullResolution = true`
- Prevents frozen install (Line 691)
- Strips lockfile fields to force regeneration (Lines 1100-1112)

**Lockfile Field Stripping (Lines 1100-1112):**
```typescript
if (opts.fixLockfile && (ctx.wantedLockfile.packages != null) && !isEmpty(ctx.wantedLockfile.packages)) {
  ctx.wantedLockfile.packages = mapValues(({ dependencies, optionalDependencies, resolution }) => ({
    dependencies,
    optionalDependencies,
    resolution,
  }), ctx.wantedLockfile.packages)
}
```

This removes peer dependency information and other fields, forcing them to be recalculated.

#### 3. **Peer Dependency Resolution Mechanism**

**Location:** `pkg-manager/resolve-dependencies/src/resolveDependencyTree.ts:201`

```typescript
hoistPeers: autoInstallPeers || opts.dedupePeerDependents,
```

By default, `dedupePeerDependents` is `true` (see `pkg-manager/core/src/install/extendInstallOptions.ts:264`), so `hoistPeers` is enabled during full resolution.

#### 4. **The "Peers of Peers" Resolution Loop**

**Location:** `pkg-manager/resolve-dependencies/src/resolveDependencies.ts:341-387`

When `hoistPeers` is enabled, an iterative loop handles transitive peer dependencies:

```typescript
while (true) {
  // Resolve direct dependencies

  // Identify missing required peers
  const missingRequiredPeers: Array<[string, MissingPeerInfo]> = []
  for (const [peerName, peerInfo] of Object.entries(importerResolutionResult.missingPeers ?? {})) {
    if (peerInfo.optional) {
      // Handle optional peers
    } else {
      missingRequiredPeers.push([peerName, peerInfo])
    }
  }

  if (!missingRequiredPeers.length) break  // Exit when no more missing peers

  // Hoist the missing peers
  const dependencies = _hoistPeers(missingRequiredPeers)

  // Recursively resolve these hoisted peers
  const resolveDependenciesResult = await resolveDependencies(ctx, preferredVersions, wantedDependencies, {
    ...options,
    parentPkgAliases,
    updateToLatest: false,
  })

  // Continue loop if these resolved peers have missing peers themselves
  // This handles "peers of peers"
}
```

**Key Points:**
- The loop continues until no missing peers are found
- Each iteration can discover new peer dependencies from previously resolved peers
- This is how "peers of peers" are automatically installed

#### 5. **Peer Deduplication**

**Location:** `pkg-manager/resolve-dependencies/src/resolvePeers.ts:183-191`

When `dedupePeerDependents` is true, duplicate instances of the same package are deduplicated:

```typescript
if (opts.dedupePeerDependents) {
  const duplicates = Array.from(depPathsByPkgId.values()).filter((item) => item.size > 1)
  const allDepPathsMap = deduplicateAll(depGraphWithResolvedChildren, duplicates)
  // Replace duplicate paths with canonical path
}
```

### Why the Behavior Differs

#### Frozen Install Path
When `pnpm i` detects that the lockfile is up-to-date and no changes are needed:
- Uses `headlessInstall()` (Line 782 in `pkg-manager/core/src/install/index.ts`)
- **Only unpacks/links files** based on existing lockfile
- **Does NOT perform dependency resolution**
- **Does NOT run the hoistPeers loop**
- Uses whatever peer resolution was in the lockfile when it was created

If the lockfile was created with incomplete peer resolution (e.g., peers of peers were missing), frozen install will perpetuate this issue.

#### Full Resolution Path
When `pnpm i --fix-lockfile` is used:
- **Always forces full resolution**
- Strips lockfile fields to force regeneration
- Runs the complete dependency resolution process
- **Activates the hoistPeers loop**
- Iteratively resolves all missing peer dependencies, including peers of peers
- Properly deduplicates packages with different peer combinations

### Real-World Example

**Test Case:** `pkg-manager/core/test/install/fixLockfile.ts:240-263`

```typescript
test('--fix-lockfile should install successfully when package has no dependencies but has peer dependencies', async () => {
  const packages = {
    dependencies: {
      // has-has-y-peer-peer has no dependencies but has peer: has-y-peer
      // has-y-peer has peer: @pnpm/y
      '@pnpm.e2e/has-has-y-peer-peer': '1.0.0',
      '@pnpm.e2e/has-y-peer': '^1.0.0',
      '@pnpm/y': '^1.0.0',
    },
  }

  await install(packages, testDefaults())

  // Second install with --fix-lockfile regenerates peer resolution
  await install(packages, testDefaults({
    fixLockfile: true,
  }))
})
```

**Dependency Chain:**
```
has-has-y-peer-peer → peerDep: has-y-peer → peerDep: @pnpm/y
has-has-y-peer-peer → peerDep: @pnpm/y (direct)
```

### Configuration

**Location:** `pkg-manager/core/src/install/extendInstallOptions.ts`

Default settings that enable this behavior:
- **Line 264:** `dedupePeerDependents: true` - Enables peer hoisting by default
- **Line 265:** `resolvePeersFromWorkspaceRoot: true` - Resolves peers from workspace root

### Summary

**Why `pnpm i --fix-lockfile` installs peers of peers:**

1. **Forces full resolution** by setting `needsFullResolution = true` and preventing frozen install
2. **Strips lockfile fields** to force regeneration of peer dependency information
3. **Activates the hoistPeers loop** which iteratively resolves missing peer dependencies
4. **Handles transitive peer dependencies** by recursively checking for missing peers in each iteration
5. **Deduplicates packages** to ensure no duplicate instances exist

**Why `pnpm i` may not install peers of peers:**

1. **Uses frozen install** when the lockfile is up-to-date
2. **Skips dependency resolution** entirely in frozen install mode
3. **Uses existing lockfile as-is** which may have incomplete peer resolution
4. **Does not run the hoistPeers loop** in frozen install mode

### Recommendation

If you encounter missing peer dependencies (especially peers of peers), use `pnpm i --fix-lockfile` to regenerate the lockfile with proper peer dependency resolution.

**Key Files:**
- `pkg-manager/plugin-commands-installation/src/install.ts:82` - Flag definition
- `pkg-manager/core/src/install/index.ts:430` - Forces full resolution
- `pkg-manager/core/src/install/index.ts:691` - Prevents frozen install
- `pkg-manager/core/src/install/index.ts:1100-1112` - Strips lockfile fields
- `pkg-manager/resolve-dependencies/src/resolveDependencies.ts:341-387` - Peers of peers loop
- `pkg-manager/resolve-dependencies/src/resolvePeers.ts:183-191` - Deduplication
