# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

This is a **collection of Claude Code skills** (not a buildable mobile project). Each subdirectory contains a single `SKILL.md` file that teaches Claude Code opinionated Mobile/Kotlin Multiplatform architecture patterns. Users install these by copying the folders into `~/.claude/skills/`.

There are 8 skills total, each in its own directory:

- **kmp-module-structure** -- Project layout, feature-layered modularization, convention plugins, dependency rules
- **kmp-data-layer** -- Repositories, data sources, DTOs, mappers, Room, Ktor, offline-first patterns
- **kmp-error-handling** -- Generic `Result<T, E>` wrapper, `DataError` types, safe call helpers, `UiText` mapping
- **kmp-presentation-mvi** -- MVI pattern: State/Action/Event, ViewModel, Root/Screen composable split, `SavedStateHandle`
- **kmp-navigation** -- Type-safe Compose Navigation with `@Serializable` routes, feature nav graphs, cross-feature callbacks
- **kmp-di-koin** -- Koin DI conventions: module-per-layer, `singleOf`/`viewModelOf`, assembly in `:app`
- **kmp-testing** -- JUnit 5 + AssertK + Turbine, fakes over mocks, Robot pattern for UI tests
- **kmp-compose-ui** -- Compose stability, recomposition, side effects, animations, previews, accessibility

## Key Architecture Decisions Encoded in the Skills

- **Feature-layered modularization**: split by feature first, then by Clean Architecture layer (`presentation` -> `domain` <- `data`). Features never depend on each other.
- **Domain is pure Kotlin** with no Android/framework imports. All data source/repository interfaces live in domain.
- **No `Impl` suffix** -- implementations are named for what makes them unique (e.g., `RoomNoteDataSource`, `OfflineFirstNoteRepository`).
- **Custom `Result<D, E>` wrapper** (not Kotlin stdlib Result) with typed errors and chaining extensions (`map`, `onSuccess`, `onFailure`, `asEmptyResult`).
- **Fakes over mocks** in tests. Dispatchers are only injected when a non-ViewModel class uses a non-main dispatcher AND is unit-tested.
- **UI is dumb** -- composables render state and forward actions. All state lives in the ViewModel's `StateFlow`. `remember`/`rememberSaveable` only for Compose-internal state (e.g., `LazyListState`).

## Working With This Repo

There is no build system, no tests to run, and no linting. The only meaningful files are the `SKILL.md` files and the `README.md`. Changes should maintain consistency across all skill files in terminology, naming conventions, and cross-references between skills (e.g., data-layer references error-handling, presentation-mvi references error-handling).
