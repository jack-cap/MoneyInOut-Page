# Testing

Comprehensive testing guide for Money In & Out.

## Testing Philosophy

Money In & Out follows a pragmatic testing approach:

- **Test what matters** - Focus on critical functionality
- **Keep tests simple** - Easy to understand and maintain
- **Fast feedback** - Quick test execution
- **Reliable** - Tests should be deterministic

## Test Structure

### Test Targets

```
SpentUnitTests/          # Unit tests
├── DataModelTests.swift
├── TransactionViewModelTests.swift
├── CategoryViewModelTests.swift
├── AnalysisViewModelTests.swift
├── PeriodCalculationTests.swift
└── CategoryFilteringTests.swift

SpentUITests/            # UI tests
├── SpentUITests.swift
├── CategoryManagementUITests.swift
├── PeriodSelectorUITests.swift
└── ScreenshotUITests.swift
```

## Unit Tests

### Data Model Tests

Test SwiftData models:

```swift
class DataModelTests: XCTestCase {
    func testTransactionCreation()
    func testCategoryCreation()
    func testTransactionCategoryRelationship()
    func testDefaultValues()
}
```

### ViewModel Tests

Test business logic:

```swift
class TransactionViewModelTests: XCTestCase {
    func testAddTransaction()
    func testEditTransaction()
    func testDeleteTransaction()
    func testFilterTransactions()
    func testSearchTransactions()
}
```

### Calculation Tests

Test financial calculations:

```swift
class PeriodCalculationTests: XCTestCase {
    func testDailyTotal()
    func testWeeklyTotal()
    func testMonthlyTotal()
    func testYearlyTotal()
    func testIncomeVsExpense()
}
```

### Category Tests

Test category logic:

```swift
class CategoryFilteringTests: XCTestCase {
    func testFilterByCategory()
    func testCategoryTotals()
    func testDefaultCategory()
    func testCategoryDeletion()
}
```

## UI Tests

### Basic Flow Tests

Test common user flows:

```swift
class SpentUITests: XCTestCase {
    func testAddTransaction()
    func testEditTransaction()
    func testDeleteTransaction()
    func testNavigateBetweenTabs()
}
```

### Category Management

Test category features:

```swift
class CategoryManagementUITests: XCTestCase {
    func testCreateCategory()
    func testEditCategory()
    func testDeleteCategory()
    func testReorderCategories()
}
```

### Period Selection

Test time period navigation:

```swift
class PeriodSelectorUITests: XCTestCase {
    func testSwitchPeriods()
    func testNavigateForward()
    func testNavigateBackward()
    func testReturnToCurrent()
}
```

## Running Tests

### Xcode

Run all tests:
```
⌘ + U
```

Run specific test:
```
Click diamond icon next to test
```

Run test class:
```
Click diamond icon next to class
```

### Command Line

Run all tests:
```bash
xcodebuild test -scheme "Money In & Out" -destination 'platform=iOS Simulator,name=iPhone 15'
```

Run unit tests only:
```bash
xcodebuild test -scheme "Money In & Out" -destination 'platform=iOS Simulator,name=iPhone 15' -only-testing:SpentUnitTests
```

Run UI tests only:
```bash
xcodebuild test -scheme "Money In & Out" -destination 'platform=iOS Simulator,name=iPhone 15' -only-testing:SpentUITests
```

## Test Data

### Sample Data Generator

For testing and screenshots:

```swift
class SampleDataGenerator {
    static func generateSampleTransactions()
    static func generateSampleCategories()
    static func clearAllData()
}
```

### Test Fixtures

Create consistent test data:

```swift
extension Transaction {
    static func testTransaction() -> Transaction
    static func testIncome() -> Transaction
    static func testExpense() -> Transaction
}
```

## Testing Best Practices

### Unit Tests

1. **Arrange-Act-Assert**
   ```swift
   func testExample() {
       // Arrange
       let sut = ViewModel()
       
       // Act
       sut.performAction()
       
       // Assert
       XCTAssertEqual(sut.result, expected)
   }
   ```

2. **One assertion per test** (when possible)
3. **Clear test names** - Describe what's being tested
4. **Independent tests** - No dependencies between tests
5. **Fast execution** - Keep tests quick

### UI Tests

1. **Use accessibility identifiers**
   ```swift
   Button("Add")
       .accessibilityIdentifier("addButton")
   ```

2. **Wait for elements**
   ```swift
   let button = app.buttons["addButton"]
   XCTAssertTrue(button.waitForExistence(timeout: 5))
   ```

3. **Test user perspective** - What user sees and does
4. **Avoid implementation details** - Test behavior, not code
5. **Keep tests maintainable** - Extract common actions

## Test Coverage

### Current Coverage

- Unit tests: ~80% coverage
- UI tests: Critical flows covered
- Integration tests: CloudKit sync scenarios

### Coverage Goals

- Maintain 70%+ unit test coverage
- Cover all critical user flows
- Test edge cases and error states

### Measuring Coverage

In Xcode:
1. Edit scheme
2. Enable "Gather coverage data"
3. Run tests
4. View coverage in Report Navigator

## Continuous Integration

### GitHub Actions

Example workflow:

```yaml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: xcodebuild test -scheme "Money In & Out" -destination 'platform=iOS Simulator,name=iPhone 15'
```

## Testing CloudKit

### Challenges

- Requires iCloud account
- Network dependency
- Async operations
- Difficult to mock

### Strategies

1. **Use test container**
   ```swift
   let container = CKContainer(identifier: "iCloud.com.test")
   ```

2. **Mock CloudKit**
   - Create protocol for CloudKit operations
   - Implement mock for testing
   - Use real implementation in production

3. **Integration tests**
   - Test with real CloudKit in development
   - Separate test environment
   - Clean up test data

## Testing SwiftData

### In-Memory Storage

For fast, isolated tests:

```swift
let config = ModelConfiguration(isStoredInMemoryOnly: true)
let container = try ModelContainer(
    for: Transaction.self, Category.self,
    configurations: config
)
```

### Test Isolation

- Each test gets fresh container
- No persistent state between tests
- Fast and reliable

## Performance Testing

### Measure Performance

```swift
func testPerformance() {
    measure {
        // Code to measure
        viewModel.calculateTotals()
    }
}
```

### Performance Benchmarks

- Transaction list loading: < 100ms
- Analysis calculation: < 200ms
- Search: < 50ms
- Sync: < 5s (network dependent)

## Debugging Tests

### Common Issues

1. **Flaky tests**
   - Add waits for async operations
   - Check for race conditions
   - Ensure proper cleanup

2. **Slow tests**
   - Profile test execution
   - Reduce unnecessary setup
   - Use in-memory storage

3. **Test failures**
   - Check test isolation
   - Verify test data
   - Review recent changes

### Debugging Tools

- Xcode debugger
- Print statements
- Test logs
- Breakpoints in tests

## Test Maintenance

### Regular Tasks

- Update tests with new features
- Remove obsolete tests
- Refactor duplicated code
- Keep tests fast

### Code Review

- Review test coverage
- Check test quality
- Ensure tests are clear
- Verify edge cases

## Writing New Tests

### Checklist

- [ ] Test name describes what's tested
- [ ] Test is independent
- [ ] Test is fast
- [ ] Test is reliable
- [ ] Test has clear assertions
- [ ] Test covers edge cases
- [ ] Test is documented (if complex)

### Example Test

```swift
func testAddingTransactionUpdatesTotal() {
    // Arrange
    let viewModel = TransactionViewModel(container: testContainer)
    let initialTotal = viewModel.totalExpenses
    
    // Act
    viewModel.addTransaction(
        amount: 50.0,
        type: .expense,
        category: testCategory
    )
    
    // Assert
    XCTAssertEqual(
        viewModel.totalExpenses,
        initialTotal + 50.0,
        "Total expenses should increase by transaction amount"
    )
}
```

## Resources

### Apple Documentation

- [XCTest Framework](https://developer.apple.com/documentation/xctest)
- [UI Testing](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/testing_with_xcode/chapters/09-ui_testing.html)
- [Performance Testing](https://developer.apple.com/documentation/xctest/performance_tests)

### Best Practices

- [Testing Swift](https://www.swiftbysundell.com/basics/unit-testing/)
- [iOS Testing Guide](https://roadfiresoftware.com/unit-testing-in-swift/)
