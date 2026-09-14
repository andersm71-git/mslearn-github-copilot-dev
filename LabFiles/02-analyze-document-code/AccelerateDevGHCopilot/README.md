# Library App

## Description

Library App is a .NET 10 console application for managing library patrons, loans, and membership information. It provides a simple workflow for searching patrons, reviewing loan details, renewing memberships, extending due dates, and marking items as returned.

The application follows a layered architecture with:
- application core logic for domain rules
- interface-based repositories for data access
- infrastructure implementations that load and save JSON data
- a console front end for user interaction

## Project Structure

- src/
  - Library.ApplicationCore/
    - Entities/
      - Author.cs
      - Book.cs
      - BookItem.cs
      - Loan.cs
      - Patron.cs
    - Enums/
      - EnumHelper.cs
      - LoanExtensionStatus.cs
      - LoanReturnStatus.cs
      - MembershipRenewalStatus.cs
    - Interfaces/
      - ILoanRepository.cs
      - ILoanService.cs
      - IPatronRepository.cs
      - IPatronService.cs
    - Services/
      - LoanService.cs
      - PatronService.cs
  - Library.Console/
    - CommonActions.cs
    - ConsoleApp.cs
    - ConsoleState.cs
    - Program.cs
    - appSettings.json
    - Json/
      - Authors.json
      - BookItems.json
      - Books.json
      - Loans.json
      - Patrons.json
  - Library.Infrastructure/
    - Data/
      - JsonData.cs
      - JsonLoanRepository.cs
      - JsonPatronRepository.cs

- tests/
  - UnitTests/
    - ApplicationCore/
      - LoanService/
        - ExtendLoan.cs
        - ReturnLoan.cs
      - PatronService/
        - RenewMembership.cs
    - LoanFactory.cs
    - PatronFactory.cs
    - UnitTests.csproj

## Key Classes and Interfaces

- Program
  - Starts the application and configures dependency injection.

- ConsoleApp
  - Handles the console flow for searching patrons, selecting records, and performing actions such as renewals and loan updates.

- LoanService
  - Implements business rules for returning a loan and extending a loan due date.
  - Validates loan state, membership status, and due-date conditions before allowing actions.

- PatronService
  - Implements business rules for renewing a patron's membership.
  - Prevents early renewals and blocks renewal when the patron has overdue loans.

- JsonData
  - Loads and stores JSON records for authors, books, book items, patrons, and loans.
  - Rehydrates nested objects so the business layer can work with populated domain models.

- JsonPatronRepository
  - Provides data access for patron-related queries and updates.

- JsonLoanRepository
  - Provides data access for loan-related queries and updates.

- ILoanService / IPatronService
  - Define the application service contracts used by the console layer.

- ILoanRepository / IPatronRepository
  - Define the repository contracts for persistence operations.

## Usage

1. Restore dependencies:
   dotnet restore

2. Run the console application:
   dotnet run --project src/Library.Console/Library.Console.csproj

3. Search for a patron by name from the console prompt.

4. Select a patron or loan from the results to view details.

5. Use the menu options to:
   - renew a patron membership
   - extend a loan
   - mark a book as returned
   - search for another patron

## License

This project is provided for educational and demonstration purposes. Please check with the repository owner or organization for the appropriate licensing terms before commercial or public reuse.