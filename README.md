# Mobile / KMP Architecture Skills for Claude Code

A collection of eight opinionated architecture skills that teach Claude Code how to write Mobile and Kotlin Multiplatform code the way you'd write it yourself. Once installed, Claude will automatically follow these patterns whenever you ask it to scaffold features, write tests, set up navigation, and more.

## Prerequisites: Installing Claude Code

If you don't have Claude Code yet, install it first.

### macOS / Linux

Open a terminal and run:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Then run `claude` to launch Claude Code and complete the authentication flow.

### Windows

Open **PowerShell** and run:

```powershell
irm https://claude.ai/install.ps1 | iex
```

Then run `claude` to launch Claude Code and complete the authentication flow.

> [Git for Windows](https://git-scm.com/downloads/win) is required. See the [official docs](https://docs.claude.com/en/docs/claude-code/quickstart) for detailed setup instructions.

## Installing the Skills

Each skill is a single markdown file (`SKILL.md`) inside its own folder. To install them, copy the eight skill folders into your Claude Code skills directory:

```
~/.claude/skills/
├── kmp-compose-ui/
│   └── SKILL.md
├── kmp-data-layer/
│   └── SKILL.md
├── kmp-di-koin/
│   └── SKILL.md
├── kmp-error-handling/
│   └── SKILL.md
├── kmp-module-structure/
│   └── SKILL.md
├── kmp-navigation/
│   └── SKILL.md
├── kmp-presentation-mvi/
│   └── SKILL.md
└── kmp-testing/
    └── SKILL.md
```

Simply paste the eight folders into `~/.claude/skills/` and they'll be picked up automatically the next time you start a Claude Code session. No restart or configuration is needed beyond having the files in place.

## What Each Skill Does

### kmp-compose-ui

Compose UI patterns: stability and recomposition optimization, side-effect guidelines, lazy layout best practices, animation without recomposition (graphicsLayer, deferred state reads), modifier extensions, design system slot APIs, previews, accessibility, and TextField state ownership.

### kmp-error-handling

The shared error-handling foundation used across all layers: a generic `Result<T, E>` wrapper, `DataError` sealed interface (Network + Local), `EmptyResult` typealias, chaining extensions (`map`, `onSuccess`, `onFailure`, `asEmptyResult`), `UiText` error mapping, and typed safe-call helpers for Ktor.

### kmp-module-structure

Defines the project-level blueprint: feature-layered modularization, Gradle convention plugins, version catalogs, and dependency rules. Claude will follow this structure whenever you ask it to create a new module, set up a project, or decide where code should live.

### kmp-data-layer

Covers everything below the domain boundary: repository implementations, DTOs, Room entities and DAOs, Ktor `HttpClient` setup, safe-call helpers, token storage, offline-first patterns, and the shared `Result` / `DataError` types.

### kmp-presentation-mvi

The MVI presentation layer pattern: a single `State` data class, a sealed `Action` interface, one-time `Event` side-effects via `Channel`, ViewModel wiring, the Root/Screen composable split, `UiText` error mapping, and process-death handling with `SavedStateHandle`.

### kmp-navigation

Type-safe Compose Navigation using `@Serializable` route objects, one nav graph per feature, cross-feature navigation through callbacks, and assembly in the `:app` module.

### kmp-di-koin

Koin dependency injection conventions: one module per feature layer, `single` / `viewModel` / `factory` scoping, assembling modules in `:app`, and injecting ViewModels in composables with `koinViewModel()`.

### kmp-testing

Testing patterns and stack: JUnit 5 + AssertK + Turbine for ViewModel unit tests, `UnconfinedTestDispatcher`, fake repositories, `SavedStateHandle` testing, and Compose UI tests with `ComposeTestRule`.

## How Skills Work

When you give Claude Code a task — for example, *"create a new notes feature with a list and detail screen"* — it checks whether any installed skills match the request. If they do, Claude reads the corresponding `SKILL.md` files and follows the patterns described in them. Multiple skills can activate at once, so a feature-scaffolding request might pull in module-structure, data-layer, presentation-mvi, navigation, DI, and testing all together.

You don't need to reference skills by name. Just describe what you want to build and Claude will apply the right patterns automatically.