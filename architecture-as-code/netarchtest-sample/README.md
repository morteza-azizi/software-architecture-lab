# Clean Architecture Sample with NetArchTest

A .NET 10 sample demonstrating **Clean Architecture** with automated validation using **NetArchTest**.

## Architecture Overview

```
┌─────────────────────────────────────────┐
│                   API                   │  ← Controllers, Program.cs
├─────────────────────────────────────────┤
│              Infrastructure             │  ← Business Services
├─────────────────────────────────────────┤
│                  Data                   │  ← Repositories, UnitOfWork
├─────────────────────────────────────────┤
│                 Domain                  │  ← Entities, Interfaces
└─────────────────────────────────────────┘
```

### Dependency Flow

- **Domain** — no dependencies (core business logic)
- **Data** — depends only on Domain (data access)
- **Infrastructure** — depends only on Domain (business services)
- **API** — depends on Domain interfaces only (presentation layer)

## Getting Started

Requires [.NET 10 SDK](https://dotnet.microsoft.com/download).

```bash
cd architecture-as-code/netarchtest-sample
dotnet build NetArchTestSample.sln
dotnet test NetArchTestSample.sln
```

Run the API:

```bash
dotnet run --project NetArchTestSample.Api
```

## Architecture Tests

The `NetArchTestSample.ArchitectureTests` project contains 15 tests in `ArchitecturalRules.cs`.

### Dependency Rules

- Domain must not depend on Infrastructure, Data, or API
- Infrastructure must not depend on API
- Data must not depend on Infrastructure or API
- Controllers must not depend on Infrastructure or Data

### Structural Rules

- Repository classes must live in `Data.Repositories`
- Service classes must live in `Infrastructure.Services`
- Controllers, services, and repositories must be sealed
- Interfaces must start with `I`

### Domain Rules

- Domain service interfaces must only expose async methods (custom `AsyncMethodRule`)

## Related Article

- [Enforce Architectural Rules with Tests using NetArchTest](https://www.mortezaazizi.com/posts/netarchtest-enforce-architectural-rules-with-tests/)

## Resources

- [Clean Architecture by Robert C. Martin](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
- [NetArchTest Framework](https://github.com/BenMorris/NetArchTest)
