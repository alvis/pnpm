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

---

## What "Full Resolution" Actually Means

### The Common Misconception

**Full resolution does NOT mean ignoring the lockfile entirely.** This is a critical misunderstanding.

### What Actually Happens

**Full resolution means:**
1. ✅ Re-runs the dependency resolution algorithm
2. ✅ Checks for missing peer dependencies
3. ✅ Re-validates version compatibility
4. ✅ **PREFERS versions already in the lockfile**
5. ❌ Does NOT automatically upgrade packages
6. ❌ Does NOT ignore the lockfile

### The Mechanism: Preferred Versions

**Location:** `lockfile/preferred-versions/src/index.ts:29-38`

```typescript
function addPreferredVersionsFromLockfile(snapshots: PackageSnapshots, preferredVersions: PreferredVersions): void {
  for (const [depPath, snapshot] of Object.entries(snapshots)) {
    const { name, version } = nameVerFromPkgSnapshot(depPath, snapshot)
    if (!preferredVersions[name]) {
      preferredVersions[name] = { [version]: 'version' }  // Lockfile versions are preferred!
    } else if (!preferredVersions[name][version]) {
      preferredVersions[name][version] = 'version'
    }
  }
}
```

**During resolution:**
1. pnpm extracts all versions currently in the lockfile
2. These become "preferred versions" passed to the resolver
3. When picking a version, **lockfile versions are tried first**
4. Only if no lockfile version satisfies the range, a new version is selected

### Version Selection Priority

**Location:** `resolving/npm-resolver/src/pickPackageFromMeta.ts:147-182`

```typescript
export function pickVersionByVersionRange({ meta, versionRange, preferredVersionSelectors }) {
  // PRIORITY 1: Try preferred versions first (from lockfile)
  if (preferredVersionSelectors != null && Object.keys(preferredVersionSelectors).length > 0) {
    const prioritizedPreferredVersions = prioritizePreferredVersions(meta, versionRange, preferredVersionSelectors)
    for (const preferredVersions of prioritizedPreferredVersions) {
      // Try to pick a version already in lockfile that satisfies the range
      const preferredVersion = semver.maxSatisfying(preferredVersions, versionRange, true)
      if (preferredVersion) {
        return preferredVersion  // Use existing lockfile version!
      }
    }
  }

  // PRIORITY 2: Only if no preferred version satisfies, pick latest
  const latest = meta['dist-tags'].latest
  if (latest && semverSatisfiesLoose(latest, versionRange)) {
    return latest
  }

  // PRIORITY 3: Fallback to max satisfying version
  return semver.maxSatisfying(Object.keys(meta.versions), versionRange, true)
}
```

### The `proceed` Flag

**Location:** `pkg-manager/resolve-dependencies/src/resolveDependencies.ts:1065-1124`

```typescript
function getDepsToResolve(wantedDependencies, wantedLockfile, options) {
  let proceedAll = options.proceed  // forceFullResolution sets this to true

  for (const wantedDependency of wantedDependencies) {
    let proceed = proceedAll

    // Check if existing lockfile version satisfies the requirement
    if (resolvedDependencies[wantedDependency.alias] &&
        satisfiesWanted(resolvedDependencies[wantedDependency.alias])) {
      reference = resolvedDependencies[wantedDependency.alias]  // Use lockfile version
    } else if (
      // If dependencies that were used by the previous version of the package
      // satisfy the newer version's requirements, then pnpm tries to keep
      // the previous dependency.
      semver.validRange(wantedDependency.bareSpecifier) !== null &&
      preferredDependencies[wantedDependency.alias] &&
      satisfiesWanted(preferredDependencies[wantedDependency.alias])
    ) {
      proceed = true
      reference = preferredDependencies[wantedDependency.alias]  // Prefer old version
    }

    // ...
  }
}
```

**Key comment from the code:**
> "If dependencies that were used by the previous version of the package satisfy the newer version's requirements, then pnpm tries to keep the previous dependency."

### Comparison: Frozen vs Full Resolution

| Aspect | Frozen Install | Full Resolution |
|--------|----------------|-----------------|
| **Dependency resolution** | ❌ Skipped entirely | ✅ Re-runs algorithm |
| **Lockfile respected** | ✅ Used as-is (100% trust) | ✅ Used as preference (verified) |
| **Peer dependency check** | ❌ Skipped | ✅ Runs hoistPeers loop |
| **Version validation** | ❌ Skipped | ✅ Verifies version compatibility |
| **Package updates** | ❌ No | ❌ No (unless ranges changed) |
| **Preferred versions** | N/A | ✅ Lockfile versions prioritized |
| **Speed** | ⚡ Very fast | 🐌 Slower (network/validation) |

### When Packages Actually Get Updated

Packages will ONLY get new versions if:

1. **You explicitly request it:**
   ```bash
   pnpm update          # Updates all packages within their ranges
   pnpm update react    # Updates specific package
   pnpm install react@18  # Explicitly request new version
   ```

2. **The version range changed:**
   ```json
   // Before: "react": "^17.0.0" → lockfile has react@17.0.2
   // After:  "react": "^18.0.0" → lockfile version doesn't satisfy new range
   // Result: Resolves to react@18.x.x
   ```

3. **No existing version satisfies the range:**
   ```bash
   # New dependency added
   pnpm add new-package
   # No preferred version exists, picks latest satisfying version
   ```

### What `--fix-lockfile` Actually Does

**It does NOT upgrade packages.** It:

1. **Forces full resolution** (re-validates everything)
2. **Strips certain lockfile fields** (forces recalculation):
   ```typescript
   // pkg-manager/core/src/install/index.ts:1100-1112
   ctx.wantedLockfile.packages = mapValues(({ dependencies, optionalDependencies, resolution }) => ({
     dependencies,         // Keep deps
     optionalDependencies, // Keep optional deps
     resolution,           // Keep resolution info
     // REMOVES: peerDependencies, transitivePeerDependencies, etc.
     // These will be recalculated
   }), ctx.wantedLockfile.packages)
   ```
3. **Re-resolves peer dependencies** (what you want!)
4. **Uses preferred versions** (lockfile versions stay the same)
5. **Regenerates peer suffix hashes** (fixes broken paths)

### Example Scenario

**Before `pnpm install --fix-lockfile`:**
```yaml
# pnpm-lock.yaml
snapshots:
  ajv-keywords@1.5.0:
    dependencies: {}
    # Missing peer dependency info!
```

**After `pnpm install --fix-lockfile`:**
```yaml
# pnpm-lock.yaml
snapshots:
  ajv-keywords@1.5.0(ajv@4.10.4):
    peerDependencies:
      ajv: ^4.10.0
    peerDependenciesMeta:
      ajv:
        optional: false
    # ajv@4.10.4 was already in lockfile, so it stays!
```

**Key point:** `ajv@4.10.4` was already in the lockfile and stays at that version. Only the peer relationship is regenerated.

### Summary

**"Full resolution" = "Re-run resolution algorithm while preferring existing lockfile versions"**

It's NOT:
- Ignoring the lockfile
- Upgrading all packages
- Like `npm install` from scratch

It IS:
- Re-validating that everything is correct
- Filling in missing peer information
- Fixing broken lockfile entries
- **While preserving existing versions**

This is why `pnpm install --fix-lockfile` is safe to run - it fixes issues without changing your dependency versions (unless they no longer satisfy their ranges).

**Key Files:**
- `lockfile/preferred-versions/src/index.ts:29-38` - Extracting preferred versions from lockfile
- `resolving/npm-resolver/src/pickPackageFromMeta.ts:147-182` - Version selection algorithm
- `pkg-manager/resolve-dependencies/src/resolveDependencies.ts:1065-1124` - getDepsToResolve with proceed flag
- `pkg-manager/core/src/install/index.ts:1100-1112` - Lockfile field stripping

---

**Key Files:**
- `pkg-manager/plugin-commands-installation/src/install.ts:82` - Flag definition
- `pkg-manager/core/src/install/index.ts:430` - Forces full resolution
- `pkg-manager/core/src/install/index.ts:691` - Prevents frozen install
- `pkg-manager/core/src/install/index.ts:1100-1112` - Strips lockfile fields
- `pkg-manager/resolve-dependencies/src/resolveDependencies.ts:341-387` - Peers of peers loop
- `pkg-manager/resolve-dependencies/src/resolvePeers.ts:183-191` - Deduplication

---

## What Else Can Trigger the hoistPeers Loop?

The `hoistPeers` loop (which handles peers of peers) can be triggered in multiple ways beyond `--fix-lockfile`. Understanding these triggers is crucial for managing peer dependency resolution.

### hoistPeers Flag Activation

**Location:** `pkg-manager/resolve-dependencies/src/resolveDependencyTree.ts:201`

```typescript
hoistPeers: autoInstallPeers || opts.dedupePeerDependents,
```

The `hoistPeers` flag is enabled when **either** condition is true:
1. `autoInstallPeers` is `true`
2. `dedupePeerDependents` is `true`

### Direct Triggers (Enable hoistPeers Immediately)

#### 1. **`autoInstallPeers` Setting (Default: `true`)**

**Default Value:** `true` (`pkg-manager/core/src/install/extendInstallOptions.ts:188`)

**Configuration:**
- `.pnpmrc` file: `auto-install-peers=true`
- `package.json` > `pnpm` field: `{ "pnpm": { "autoInstallPeers": true } }`
- Environment variable: `npm_config_auto_install_peers=true`

**Behavior:**
- Automatically installs missing peer dependencies as `devDependencies`
- Enables the hoistPeers loop to resolve transitive peer dependencies
- **This is enabled by default**, so hoistPeers runs by default in full resolution mode

**Example:**
```bash
# Explicitly enable (already default)
pnpm install --auto-install-peers

# Disable auto-install-peers
pnpm install --auto-install-peers=false
```

**Documentation:** `config/config/CHANGELOG.md` mentions:
> "New setting supported: `auto-install-peers`. When it is set to `true`, `pnpm add <pkg>` automatically installs any missing peer dependencies as `devDependencies`."

#### 2. **`dedupePeerDependents` Setting**

**Purpose:**
- Deduplicates packages that have different peer dependency sets
- Also **forces full resolution** (see `pkg-manager/core/src/install/index.ts:1096`)

**Configuration:**
- Workspace-level setting in `pnpm-workspace.yaml`
- Used primarily in monorepos

**Behavior:**
- Enables hoistPeers
- Forces `needsFullResolution = true`
- Prevents frozen install

### Indirect Triggers (Force Full Resolution)

These conditions force full resolution, which then runs the hoistPeers loop (if `autoInstallPeers` or `dedupePeerDependents` is true):

#### 3. **CLI Flags**

**Location:** `pkg-manager/core/src/install/index.ts:1091-1096`

```typescript
const forceFullResolution = ctx.wantedLockfile.lockfileVersion !== LOCKFILE_VERSION ||
  !opts.currentLockfileIsUpToDate ||
  opts.force ||
  opts.needsFullResolution ||
  ctx.lockfileHadConflicts ||
  opts.dedupePeerDependents
```

| Flag | Description | File Location |
|------|-------------|---------------|
| `--fix-lockfile` | Repairs broken lockfile entries | `plugin-commands-installation/src/install.ts:82` |
| `--force` | Reinstalls all dependencies, ignoring cache | `core/src/install/index.ts:1093` |
| `--resolution-only` | Re-runs resolution without installing (for debugging) | `plugin-commands-installation/src/install.ts:83` |

**Example:**
```bash
# Force full resolution and reinstall everything
pnpm install --force

# Only re-run resolution (no download/linking)
pnpm install --resolution-only
```

#### 4. **Lockfile Version Mismatch**

**Location:** `pkg-manager/core/src/install/index.ts:428-432`

```typescript
const upToDateLockfileMajorVersion = ctx.wantedLockfile.lockfileVersion.toString().startsWith(`${LOCKFILE_MAJOR_VERSION}.`)
let needsFullResolution = outdatedLockfileSettings ||
  opts.fixLockfile ||
  !upToDateLockfileMajorVersion ||  // Lockfile major version mismatch
  opts.forceFullResolution
```

**When it triggers:**
- When the lockfile was created with an older major version of pnpm
- Example: lockfile has `lockfileVersion: '6.0'` but current pnpm uses `lockfileVersion: '7.0'`

**Behavior:**
- Automatically triggers full resolution
- No manual intervention required
- Ensures lockfile compatibility

#### 5. **Lockfile Merge Conflicts**

**Location:** `pkg-manager/core/src/install/index.ts:1095`

```typescript
ctx.lockfileHadConflicts
```

**When it triggers:**
- After a git merge where `pnpm-lock.yaml` had conflicts
- pnpm automatically detects conflict markers in the lockfile

**Behavior:**
- Forces full resolution to regenerate a clean lockfile
- Resolves conflicts automatically

#### 6. **Outdated Lockfile Settings**

**Location:** `lockfile/settings-checker/src/getOutdatedLockfileSetting.ts:39-69`

When **any** of these 9 settings differ from the current configuration, it triggers full resolution:

| Setting | Description | Line |
|---------|-------------|------|
| `overrides` | Dependency version overrides | 39-40 |
| `packageExtensionsChecksum` | Package.json extensions checksum | 42-43 |
| `ignoredOptionalDependencies` | Optional deps to skip | 45-46 |
| `patchedDependencies` | Patched package definitions | 48-49 |
| `settings.autoInstallPeers` | Auto-install peers setting | 51-52 |
| `settings.excludeLinksFromLockfile` | Exclude symlinks from lockfile | 54-55 |
| `settings.peersSuffixMaxLength` | Max length for peer suffix | 57-61 |
| `pnpmfileChecksum` | .pnpmfile.cjs checksum | 63-64 |
| `settings.injectWorkspacePackages` | Inject workspace packages | 66-67 |

**Example scenario:**
```yaml
# .pnpmrc changes from:
auto-install-peers=false

# to:
auto-install-peers=true

# Next `pnpm install` triggers full resolution because
# lockfile.settings.autoInstallPeers doesn't match current config
```

**Code:**
```typescript
if ((lockfile.settings?.autoInstallPeers != null && lockfile.settings.autoInstallPeers !== autoInstallPeers)) {
  return 'settings.autoInstallPeers'
}
```

#### 7. **`dedupePeerDependents` Configuration**

**Location:** `pkg-manager/core/src/install/index.ts:1096`

When `dedupePeerDependents` is set to `true`:
- Forces `forceFullResolution = true`
- Enables `hoistPeers`
- Deduplicates packages with different peer combinations

**Configuration:**
- Default: Can be enabled in workspace configuration
- Used in monorepos to reduce duplication

### Full Resolution Decision Tree

```
Can frozen install be used?
│
├─ NO (any of the following):
│  ├─ opts.fixLockfile === true
│  ├─ opts.force === true
│  ├─ opts.needsFullResolution === true
│  ├─ lockfile version mismatch
│  ├─ outdatedLockfileSettings !== null
│  ├─ lockfileHadConflicts === true
│  ├─ dedupePeerDependents === true
│  └─ → RUN FULL RESOLUTION
│       │
│       └─ hoistPeers enabled?
│          ├─ autoInstallPeers === true (default)
│          ├─ OR dedupePeerDependents === true
│          └─ → RUN HOISTPEERS LOOP (handles peers of peers)
│
└─ YES:
   └─ → USE FROZEN INSTALL (skip hoistPeers loop)
```

### Summary Table

| Trigger | Type | Default | How to Enable | Enables hoistPeers? |
|---------|------|---------|---------------|---------------------|
| `autoInstallPeers` | Config | `true` | `.pnpmrc` or CLI flag | ✅ Direct |
| `dedupePeerDependents` | Config | `false` | Workspace config | ✅ Direct |
| `--fix-lockfile` | CLI Flag | N/A | `pnpm i --fix-lockfile` | ✅ Via full resolution |
| `--force` | CLI Flag | N/A | `pnpm i --force` | ✅ Via full resolution |
| `--resolution-only` | CLI Flag | N/A | `pnpm i --resolution-only` | ✅ Via full resolution |
| Lockfile version mismatch | Auto | N/A | Upgrade pnpm version | ✅ Via full resolution |
| Lockfile had conflicts | Auto | N/A | Git merge conflicts | ✅ Via full resolution |
| Changed `overrides` | Auto | N/A | Modify `.pnpmrc` overrides | ✅ Via full resolution |
| Changed `patchedDependencies` | Auto | N/A | Add/remove patches | ✅ Via full resolution |
| Changed `packageExtensions` | Auto | N/A | Modify extensions | ✅ Via full resolution |
| Changed `autoInstallPeers` | Auto | N/A | Toggle setting in config | ✅ Via full resolution |

### Recommendation

**To ensure peers of peers are installed:**

1. **Use the default settings** - `autoInstallPeers` is `true` by default, which enables hoistPeers
2. **Force full resolution when needed:**
   - `pnpm install --fix-lockfile` - Best for fixing existing issues
   - `pnpm install --force` - Nuclear option, reinstalls everything
3. **Be aware of frozen installs** - When lockfile is up-to-date, pnpm skips resolution to be fast
4. **Understand configuration changes** - Changing any of the 9 lockfile settings will trigger full resolution

**Key Files:**
- `pkg-manager/resolve-dependencies/src/resolveDependencyTree.ts:201` - hoistPeers flag
- `pkg-manager/core/src/install/extendInstallOptions.ts:188` - autoInstallPeers default
- `pkg-manager/core/src/install/index.ts:1091-1096` - forceFullResolution logic
- `lockfile/settings-checker/src/getOutdatedLockfileSetting.ts:39-69` - Outdated setting checks
- `config/config/src/index.js:136` - auto-install-peers config

---

## Peer Dependency Hoisting Levels

### The Problem: Peers of Peers Not Hoisted to Expected Level

A common confusion is understanding the difference between:
1. **Whether** peers of peers are resolved (covered above)
2. **Where** peers of peers are placed in the node_modules tree

The `hoistPeers` function name is misleading - it determines **WHICH VERSION** to install, **NOT WHERE** to place the dependency.

### How Hoisting Location Actually Works

**Location:** `pkg-manager/resolve-dependencies/src/hoistPeers.ts:6-44`

The `hoistPeers()` function implements a **version selection algorithm**, not a location algorithm:

```typescript
export function hoistPeers(opts, missingRequiredPeers) {
  // TIER 1: Check workspace root dependencies
  // TIER 2: Check allPreferredVersions (highest version satisfying range)
  // TIER 3: Use peer's range if autoInstallPeers enabled

  // Returns: Record<string, string> - package names to version specs
  // Does NOT determine placement in node_modules!
}
```

The actual **location decision** happens in the **hoisting graph algorithm**.

### The Two-Level Hoisting System

**Location:** `pkg-manager/hoist/src/index.ts:127-138, 294-302`

pnpm has two hoisting levels:

| Level | Location | Controlled By | Default |
|-------|----------|---------------|---------|
| **Private Hoisting** | `.pnpm/node_modules/` | `hoist-pattern` | `['*']` (all packages) |
| **Public Hoisting** | `node_modules/` (root) | `public-hoist-pattern` | `[]` (none) |

**Decision tree:**

```typescript
// pkg-manager/hoist/src/index.ts:127-138
function createGetAliasHoistType(publicHoistPattern, privateHoistPattern) {
  const publicMatcher = createMatcher(publicHoistPattern)
  const privateMatcher = createMatcher(privateHoistPattern)

  return (alias: string) => {
    if (publicMatcher(alias)) return 'public'    // → node_modules/
    if (privateMatcher(alias)) return 'private'  // → .pnpm/node_modules/
    return false                                 // → no hoisting
  }
}
```

**Placement logic:**

```typescript
// Lines 294-302
const targetDir = hoistType === 'public'
  ? opts.publicHoistedModulesDir     // node_modules/
  : opts.privateHoistedModulesDir    // .pnpm/node_modules/

const dest = path.join(targetDir, pkgAlias)
await symlink(depLocation, dest)
```

### Why Peers of Peers May Not Be at Root Level

**Peers of peers are treated like any other dependency** - they follow the same hoisting rules:

1. **Default behavior:** Only private hoisting (`.pnpm/node_modules/`)
2. **They won't appear at root** unless they match `public-hoist-pattern`
3. **Pattern matching is by package name**, not by dependency type

**Example scenario:**

```
Your project
├── dependency-a
│   └── peerDependency: react
│       └── peerDependency: scheduler  ← peer of peer
└── node_modules/
    ├── dependency-a/           ← direct dependency (always at root)
    ├── .pnpm/
    │   └── node_modules/
    │       ├── react/          ← private hoisted (DEFAULT)
    │       └── scheduler/      ← private hoisted (DEFAULT)
    └── (react and scheduler NOT here unless public-hoist-pattern matches)
```

### Solutions: How to Hoist Peers of Peers to Root

#### Option 1: `shamefully-hoist` (Hoist Everything) ⚠️

**Configuration (.pnpmrc):**
```ini
shamefully-hoist=true
```

**Effect:**
- Sets `public-hoist-pattern=['*']` automatically
- **All packages** hoisted to root `node_modules/`
- Mimics npm/yarn behavior
- May cause version conflicts

**Location:** `config/config/src/index.ts:509-529`

**Result:**
```
node_modules/
├── dependency-a/
├── react/           ← NOW AT ROOT
└── scheduler/       ← NOW AT ROOT
```

**Trade-off:** Loses pnpm's strict dependency isolation

---

#### Option 2: `public-hoist-pattern` (Selective Hoisting) ✅ Recommended

**Configuration (.pnpmrc):**
```ini
public-hoist-pattern[]=react
public-hoist-pattern[]=react-*
public-hoist-pattern[]=scheduler
public-hoist-pattern[]=@babel/*
```

Or in `package.json`:
```json
{
  "pnpm": {
    "publicHoistPattern": ["react", "react-*", "scheduler", "@babel/*"]
  }
}
```

**Effect:**
- Only matching packages hoisted to root
- Maintains isolation for other dependencies
- Can use glob patterns

**Result:**
```
node_modules/
├── dependency-a/
├── react/           ← Matches pattern
├── scheduler/       ← Matches pattern
└── .pnpm/
    └── node_modules/
        └── other-deps/  ← Non-matching packages stay private
```

**Trade-off:** Must explicitly list packages or patterns

---

#### Option 3: Workspace Root Dependencies (Implicit Hoisting)

**Configuration (package.json at workspace root):**
```json
{
  "dependencies": {
    "react": "^18.0.0",
    "scheduler": "^0.23.0"
  }
}
```

**Effect:**
- Packages declared in workspace root are always at root level
- Peers resolved from workspace root when `resolve-peers-from-workspace-root=true` (default)
- Ensures consistent versions across workspace

**Location:** `pkg-manager/resolve-dependencies/src/hoistPeers.ts:14-20`

```typescript
// TIER 1: Check workspace root dependencies by alias
const rootDepByAlias = opts.workspaceRootDeps.find((rootDep) => rootDep.alias === peerName)
if (rootDepByAlias?.normalizedBareSpecifier) {
  dependencies[peerName] = rootDepByAlias.normalizedBareSpecifier  // Use root version
}
```

**Result:**
```
node_modules/
├── dependency-a/
├── react/           ← Declared at root
└── scheduler/       ← Declared at root
```

**Trade-off:** Must add dependencies to root package.json

---

### Configuration Reference

| Setting | Location | Default | Effect |
|---------|----------|---------|--------|
| `hoist` | `.pnpmrc` | `true` | Enable/disable hoisting entirely |
| `hoist-pattern` | `.pnpmrc` | `['*']` | Packages to hoist privately |
| `public-hoist-pattern` | `.pnpmrc` | `[]` | Packages to hoist publicly |
| `shamefully-hoist` | `.pnpmrc` | `false` | Shortcut for `public-hoist-pattern=['*']` |
| `node-linker` | `.pnpmrc` | `'isolated'` | Choose linker: `isolated`, `hoisted`, or `pnp` |
| `resolve-peers-from-workspace-root` | `.pnpmrc` | `true` | Use root deps for peer resolution |

**Defaults (from `config/config/src/index.ts`):**
```typescript
hoist: true,                              // Line 169
'hoist-pattern': ['*'],                   // Line 170
'public-hoist-pattern': [],               // Line 190 - EMPTY by default!
'resolve-peers-from-workspace-root': true, // Line 194
```

### Diagnostic Commands

Check where packages are actually located:

```bash
# List all hoisted packages
find node_modules -maxdepth 1 -type l

# List privately hoisted packages
find node_modules/.pnpm/node_modules -maxdepth 1 -type l

# Check specific package location
pnpm list react --depth=Infinity
```

### Understanding the Hoisting Decision Tree

```
Package needs to be installed
│
├─ Does it match public-hoist-pattern?
│  └─ YES → Place at node_modules/{package-name}
│
├─ Does it match hoist-pattern?
│  └─ YES → Place at node_modules/.pnpm/node_modules/{package-name}
│
└─ NO match
   └─ Place at node_modules/.pnpm/{parent-package}/node_modules/{package-name}
```

**Important:** Peer dependencies follow the **exact same rules** as regular dependencies.

### Real-World Example

**Scenario:** You have `@mui/material` which has peer: `react`, and `react` has peer: `scheduler`

**Without configuration:**
```
node_modules/
├── @mui/
│   └── material/
└── .pnpm/
    └── node_modules/
        ├── react/       ← peer (privately hoisted)
        └── scheduler/   ← peer of peer (privately hoisted)
```

**Problem:** `@mui/material` can't find `react` at root!

**Solution 1 - Public hoist pattern:**
```ini
# .pnpmrc
public-hoist-pattern[]=react
public-hoist-pattern[]=react-*
public-hoist-pattern[]=scheduler
```

**Result:**
```
node_modules/
├── @mui/
│   └── material/
├── react/           ← NOW VISIBLE
├── scheduler/       ← NOW VISIBLE
└── .pnpm/
    └── node_modules/
```

**Solution 2 - Workspace root deps:**
```json
// package.json (workspace root)
{
  "dependencies": {
    "@mui/material": "^5.0.0",
    "react": "^18.0.0",
    "scheduler": "^0.23.0"
  }
}
```

**Result:**
```
node_modules/
├── @mui/
│   └── material/
├── react/           ← Declared at root
└── scheduler/       ← Auto-installed as peer of react
```

### Key Insights

1. **hoistPeers function ≠ hoisting location** - It selects VERSION, not LOCATION
2. **Default behavior is private hoisting** - Peers go to `.pnpm/node_modules/`
3. **public-hoist-pattern controls root placement** - Must explicitly configure
4. **shamefully-hoist is the nuclear option** - Hoists everything like npm/yarn
5. **Workspace root deps get priority** - Use for consistent peer versions

**Key Files:**
- `pkg-manager/resolve-dependencies/src/hoistPeers.ts:6-44` - Version selection
- `pkg-manager/hoist/src/index.ts:127-138` - Pattern matching
- `pkg-manager/hoist/src/index.ts:294-302` - Location assignment
- `config/config/src/index.ts:169-190` - Hoisting defaults
- `config/config/src/index.ts:509-529` - shamefully-hoist handling

---

## How Packages Actually Resolve Their Peer Dependencies

### The Critical Question

If `your-package` is at `node_modules/your-package/` and has a peer dependency on `react`, but `react` is only in `.pnpm/node_modules/` (private hoisting), **how does `your-package` actually find `react`?**

### The Answer: Virtual Store Symlink Structure

**Location:** `deps/graph-builder/src/lockfileToDepGraph.ts:29-48, 201-202`

pnpm uses a clever symlink structure where **each package with peers gets its own dedicated directory in the virtual store**.

#### The Virtual Store Directory Structure

**Directory naming (packages/dependency-path/src/index.ts:172-183):**

```typescript
export function depPathToFilename(depPath: string, maxLengthWithoutHash: number): string {
  let filename = depPathToFilenameUnescaped(depPath).replace(/[\\/:*?"<>|#]/g, '+')
  if (filename.includes('(')) {
    filename = filename
      .replace(/\)$/, '')
      .replace(/\)\(|\(|\)/g, '_')  // Convert (ajv@4.10.4) to _ajv@4.10.4
  }
  return filename
}
```

**Dependency path format:**
- Without peers: `/ajv-keywords@1.5.0`
- With peers: `/ajv-keywords@1.5.0(ajv@4.10.4)`

**Filesystem directory:**
- Without peers: `.pnpm/ajv-keywords@1.5.0/node_modules/`
- With peers: `.pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/`

#### The Actual On-Disk Structure

When you install `ajv-keywords` (which has peer: `ajv`):

```
node_modules/
├── ajv-keywords/                    → symlink to .pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/ajv-keywords/
└── .pnpm/
    ├── ajv-keywords@1.5.0_ajv@4.10.4/   ← Unique directory for this package+peer combination
    │   └── node_modules/
    │       ├── ajv-keywords/             ← The actual package content
    │       └── ajv/                      → symlink to .pnpm/ajv@4.10.4/node_modules/ajv/
    │
    ├── ajv@4.10.4/
    │   └── node_modules/
    │       └── ajv/                      ← The actual ajv package
    │
    └── node_modules/                     ← Private hoisted (if hoist-pattern matches)
        ├── ajv/                          → symlink to .pnpm/ajv@4.10.4/node_modules/ajv/
        └── ajv-keywords/                 → symlink to .pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/ajv-keywords/
```

#### How Resolution Works

**Step-by-step resolution of `require('ajv')` from within `ajv-keywords`:**

1. **User code:** `require('ajv-keywords')` from your application
2. **Node.js resolves:** `node_modules/ajv-keywords/` → **symlink** → `.pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/ajv-keywords/`
3. **Inside ajv-keywords:** `require('ajv')`
4. **Node.js walks up:** From `.pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/ajv-keywords/`
5. **Finds:** `.pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/ajv/` ✅
6. **Resolves symlink:** → `.pnpm/ajv@4.10.4/node_modules/ajv/`
7. **Success!** `ajv-keywords` can access its peer dependency

**The magic:** The peer dependency `ajv` is placed **in the same `node_modules/` directory** as the package that needs it, within the virtual store.

#### The DependenciesGraphNode Structure

**Location:** `deps/graph-builder/src/lockfileToDepGraph.ts:29-48`

```typescript
export interface DependenciesGraphNode {
  modules: string                    // .pnpm/{depPath}/node_modules/
  dir: string                        // .pnpm/{depPath}/node_modules/{pkgName}/
  children: Record<string, string>   // Map of alias → directory path
  // Peers are added to children just like regular dependencies!
}
```

**Example node for `ajv-keywords`:**

```typescript
{
  modules: '.pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules',
  dir: '.pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/ajv-keywords',
  children: {
    'ajv': '.pnpm/ajv@4.10.4/node_modules/ajv'  ← Peer dependency added here!
  }
}
```

#### Different Peer Combinations Get Different Directories

**This is why the peer hash is in the directory name:**

```
.pnpm/
├── ajv-keywords@1.5.0_ajv@4.10.4/   ← Used when paired with ajv@4.10.4
│   └── node_modules/
│       ├── ajv-keywords/
│       └── ajv/                     → points to ajv@4.10.4
│
└── ajv-keywords@1.5.0_ajv@5.0.0/    ← Used when paired with ajv@5.0.0
    └── node_modules/
        ├── ajv-keywords/
        └── ajv/                     → points to ajv@5.0.0
```

This allows **different packages to use different versions of the same peer**, maintaining strict isolation while sharing disk space through symlinks.

#### Why Public Hoisting Is Optional

**With this structure, packages can resolve peers WITHOUT public hoisting:**

- Peer is in `.pnpm/{package}_{peers}/node_modules/peer/` ✅ Found via Node.js resolution
- Public hoisting just provides an ADDITIONAL location at `node_modules/peer/` for convenience
- Some tools expect packages at root level (legacy compatibility, IDE auto-discovery, etc.)

**When you DO need public hoisting:**

1. **Direct access:** Your application code does `require('react')` but didn't declare react as a dependency
2. **Legacy tooling:** Build tools that scan `node_modules/` at root level
3. **IDE support:** Some IDEs only discover packages at root level
4. **Type definitions:** TypeScript resolution in some configurations

**When you DON'T need public hoisting:**

1. **All access is via declared dependencies:** Everything imports through packages that properly declare dependencies
2. **Modern tools:** Build tools that follow Node.js resolution algorithm
3. **You want strict isolation:** Prevent accidental access to undeclared dependencies

### Real-World Example Revisited

**Scenario:** Install `ajv-keywords@1.5.0` (peer: `ajv@^4.0.0`)

**Without public-hoist-pattern (default):**

```
node_modules/
├── ajv-keywords/        → symlink → .pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/ajv-keywords/
└── .pnpm/
    ├── ajv-keywords@1.5.0_ajv@4.10.4/
    │   └── node_modules/
    │       ├── ajv-keywords/    ← Actual content
    │       └── ajv/             → symlink → .pnpm/ajv@4.10.4/node_modules/ajv/
    │
    ├── ajv@4.10.4/
    │   └── node_modules/
    │       └── ajv/             ← Actual content
    │
    └── node_modules/
        ├── ajv/                 → symlink → .pnpm/ajv@4.10.4/node_modules/ajv/
        └── ajv-keywords/        → symlink → .pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/ajv-keywords/
```

**Resolution:**
- `require('ajv-keywords')` from your app → ✅ Works (root symlink)
- `require('ajv')` from ajv-keywords → ✅ Works (virtual store node_modules)
- `require('ajv')` from your app → ❌ Fails (not at root, unless you declared it)

**With public-hoist-pattern=['ajv']:**

```
node_modules/
├── ajv/                 → symlink → .pnpm/ajv@4.10.4/node_modules/ajv/  ← NOW AT ROOT
├── ajv-keywords/        → symlink → .pnpm/ajv-keywords@1.5.0_ajv@4.10.4/node_modules/ajv-keywords/
└── .pnpm/ (same as above)
```

**Resolution:**
- All of the above → ✅ Works
- `require('ajv')` from your app → ✅ NOW WORKS (root symlink exists)

### Summary

**The core mechanism:**
1. **Dependency paths include peer information:** `/pkg@1.0.0(peer@2.0.0)`
2. **Converted to filesystem names:** `.pnpm/pkg@1.0.0_peer@2.0.0/`
3. **Each combination gets its own directory** with its own `node_modules/`
4. **Peers are symlinked into that `node_modules/`** alongside the package
5. **Node.js resolution finds them automatically** - no special logic needed
6. **Public hoisting is purely for root-level access** - not required for resolution

**Key insight:** pnpm's virtual store structure means **packages ALWAYS have access to their peers**, regardless of hoisting configuration. Public hoisting is only about whether YOUR application code can access them at root level.

**Key Files:**
- `packages/dependency-path/src/index.ts:172-216` - Peer path encoding
- `deps/graph-builder/src/lockfileToDepGraph.ts:29-48` - DependenciesGraphNode with children
- `deps/graph-builder/src/lockfileToDepGraph.ts:201-202` - Virtual store directory creation
- `deps/graph-builder/src/lockfileToDepGraph.ts:283-308` - Children path resolution
