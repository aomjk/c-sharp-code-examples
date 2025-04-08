Company CompanyX C# Style Guide

Introduction
This style guide outlines the coding conventions for C# code developed at Company Betagro. It's based on standard C# conventions and best practices, particularly those recommended by Microsoft, with some modifications to address specific needs and preferences within our organization.

## Key Principles

* Readability: Code should be easy to understand for all team members. Use clear naming and logical structure.
* Maintainability: Code should be easy to modify and extend. Follow SOLID principles and established design patterns where appropriate.
* Consistency: Adhering to a consistent style across all projects improves collaboration and reduces errors. Utilize tooling to enforce consistency.
* Performance: While readability is paramount, code should be efficient. Be mindful of performance implications, especially in critical paths.
* Deviations from Common C# Conventions (if any - explicitly mention them here)

(This section is for noting any specific deviations Betagro chooses. The original Java guide only noted line length, which is less strictly defined in C# anyway)
## Line Length
* Maximum line length: 100 characters (aligning with the original guide's preference).
* While C# doesn't have a strict official limit, and tools often default to 120, we aim for 100 characters to maintain consistency where practical.
* Readability is the primary goal; longer lines are acceptable if they significantly improve clarity (e.g., LINQ queries, long strings, fluent configurations).

## Indentation
* Use 4 spaces per indentation level. (Standard C# convention)
* Do not use tabs for indentation. Configure IDEs accordingly.

## Naming Conventions
* Local Variables & Parameters: Use camelCase starting with a lowercase letter: userName, totalCount.
* Constants (const, static readonly): Use PascalCase: MaxValue, DatabaseName. Avoid underscores.
* For private const or private static readonly fields intended only for internal class use, _camelCase might be acceptable if consistent within the project, but PascalCase is generally preferred.
* Methods (including local functions): Use PascalCase: CalculateTotal(), ProcessData().
* Classes, Structs, Enums, Delegates, Records: Use PascalCase: UserManager, PaymentProcessor, OrderStatus.
* Interfaces: Use PascalCase prefixed with I: IUserService, IPaymentGateway.
* Properties: Use PascalCase: CustomerName, IsEnabled.
* Namespaces: Use PascalCase, typically reflecting the assembly structure: CompanyBetagro.Utilities, CompanyBetagro.Data.Repositories. Avoid underscores.
* Acronyms: Treat acronyms like words in PascalCase and camelCase (e.g., XmlReader, htmlDocument), except for two-letter acronyms which should be uppercase (e.g., IOStream).

## XML Documentation Comments
* Use ```/// <summary>...</summary>``` for all public/internal/protected types and members (classes, interfaces, methods, properties, fields, enums, delegates).
* First line of ```<summary>:``` Concise summary of the element's purpose, ending with a period.
* For complex methods/members: Include detailed descriptions in the <summary> or use <remarks>. Document parameters (<param name="name">), return values (<returns>), exceptions (<exception cref="Type">), and type parameters (<typeparam name="name">).

## Generics
* Utilize generics where appropriate to improve type safety and code reusability.
* Use descriptive names for type parameters (e.g., TKey, TValue, TEntity) or a single T if the context is obvious.

## Comments
* Write clear and concise comments using // for single-line or end-of-line comments. Use /* ... */ for temporarily commenting out blocks of code (avoid committing this).
* Use /// XML comments for documenting APIs (as described above).
* Explain the why behind non-obvious code, not just the what.
* Comment sparingly: Well-named variables, methods, and classes should make the code largely self-documenting.
* Avoid commented-out code in the final commit. Use source control history instead.

## Logging
* Use a standard logging framework: Company Betagro uses [Specify framework, e.g., Microsoft.Extensions.Logging with Serilog/NLog, Serilog directly].
* Inject logger instances (e.g., ILogger<T>) via dependency injection where possible.
* Log at appropriate levels: Trace, Debug, Information, Warning, Error, Critical.
* Provide context: Include relevant information (e.g., IDs, method names, key parameters) in log messages using structured logging placeholders (e.g., LogInformation("Processing order {OrderId} for customer {CustomerId}", orderId, customerId);).
* Avoid logging sensitive information like passwords or PII unless properly masked or required by specific security protocols.

## Error Handling
* Use specific exception types derived from System.Exception. Avoid catching System.Exception or System.SystemException unless re-throwing or at the top level for logging.
* Throw exceptions for exceptional conditions, not for normal control flow.
* Handle exceptions gracefully: Use try...catch blocks. Catch specific exceptions you can handle meaningfully. Let others propagate up.
* Use try...finally or preferably using statements for deterministic cleanup of resources (IDisposable objects like streams, database connections, etc.).
* Provide informative error messages in exceptions. Include relevant context where possible.
* Consider using the Result pattern or similar constructs for operations where failure is a common, expected outcome (instead of throwing exceptions).

## Tooling

* Code formatter: Utilize the formatting capabilities built into Visual Studio, VS Code, or JetBrains Rider. Ensure consistent settings across the team, potentially managed via .editorconfig.
* Static Analysis / Linting: Leverage Roslyn Analyzers (included with the .NET SDK and enhanced by installing additional analyzer packages like StyleCop.Analyzers, SonarAnalyzer.CSharp, etc.). Configure rule severity via .editorconfig or ruleset files.
* Team-wide Settings: Use .editorconfig files checked into source control to define and enforce many formatting and code style rules consistently across different IDEs.
