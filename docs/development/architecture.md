# Architecture

Technical overview of Money In & Out's architecture and design decisions.

## Technology Stack

### Platform
- **SwiftUI** - Modern declarative UI framework
- **SwiftData** - Data persistence and modeling
- **CloudKit** - iCloud synchronization
- **Vision** - OCR and image analysis
- **Foundation Models** - On-device AI parsing
- **Swift** - Primary programming language

### Minimum Requirements
- iOS 26.0+
- macOS 26.0+
- Xcode 15.0+

## Project Structure

```
Spent/
├── Models/              # Data models
├── ViewModels/          # Business logic
├── Views/               # UI components
├── Services/            # Business services (OCR, parsing)
├── Extensions/          # Swift extensions
├── Utilities/           # Helper functions
└── Assets.xcassets/     # Images and colors
```

## Data Layer

### SwiftData Models

#### Transaction Model
```swift
@Model
class Transaction {
    var id: UUID
    var amount: Decimal
    var type: TransactionType // income/expense
    var category: Category
    var date: Date
    var note: String?
    var timestamp: Date
    var receiptImageData: Data? // Compressed receipt image
}
```

#### Category Model
```swift
@Model
class Category {
    var id: UUID
    var name: String
    var color: String
    var icon: String?
    var type: CategoryType
    var isDefault: Bool
    var sortOrder: Int
}
```

### Data Persistence

- **Local Storage**: SwiftData with SQLite backend
- **Cloud Storage**: CloudKit with automatic sync
- **Conflict Resolution**: Last-write-wins strategy

## Architecture Pattern

### MVVM (Model-View-ViewModel)

#### Models
- Pure data structures
- SwiftData models
- No business logic

#### ViewModels
- Business logic
- Data transformation
- State management
- API calls (if any)

#### Views
- SwiftUI views
- UI logic only
- Observe ViewModels
- No direct model access

## Key Components

### Transaction Management

**TransactionViewModel**
- CRUD operations
- Filtering and sorting
- Search functionality
- Export capabilities

### Category Management

**CategoryViewModel**
- Category CRUD
- Default category handling
- Color and icon management
- Category ordering

### Analysis

**AnalysisViewModel**
- Period calculations
- Category aggregation
- Chart data preparation
- Summary statistics

### Receipt Processing

**ReceiptOCRService**
- Vision framework integration
- Text extraction from images
- Image preprocessing
- Confidence scoring

**ReceiptParserService**
- Foundation Models integration
- On-device AI parsing (Qwen 1.7B 4-bit quantized)
- Merchant name extraction
- Amount and date parsing
- Structured data generation

**ReceiptImageManager**
- Image compression (JPEG 80%)
- Size management (max 5MB)
- Storage and retrieval
- Platform compatibility

### Sync

**SyncStatusMonitor**
- CloudKit status monitoring
- Sync state tracking
- Error handling

**CloudKitErrorHandler**
- Error detection
- User notifications
- Recovery strategies

## Data Flow

```
User Action
    ↓
View (SwiftUI)
    ↓
ViewModel
    ↓
Model (SwiftData)
    ↓
Local Storage / CloudKit
    ↓
Sync to other devices
```

## CloudKit Integration

### Schema

- **Transaction** record type
- **Category** record type
- Private database (user's iCloud)
- Automatic sync

### Sync Strategy

- Real-time sync when online
- Queued updates when offline
- Conflict resolution on sync
- Background sync support

### Error Handling

- Network errors
- iCloud account issues
- Storage quota exceeded
- Conflict resolution

## State Management

### SwiftUI State

- `@State` - Local view state
- `@StateObject` - ViewModel lifecycle
- `@ObservedObject` - Shared state
- `@Environment` - Dependency injection

### Data Observation

- SwiftData automatic observation
- View updates on model changes
- Efficient re-rendering

## Performance Considerations

### Optimization Strategies

1. **Lazy Loading**
   - Load transactions on demand
   - Paginated lists
   - Efficient queries

2. **Caching**
   - Cache analysis results
   - Cache category lookups
   - Invalidate on changes

3. **Background Processing**
   - Sync in background
   - Export in background
   - Heavy calculations off main thread

4. **Memory Management**
   - Efficient data structures
   - Release unused resources
   - Minimize retained objects

## Testing Strategy

### Unit Tests

- Model logic
- ViewModel business logic
- Utility functions
- Data transformations

### UI Tests

- User flows
- Navigation
- Data entry
- Error states

### Integration Tests

- SwiftData operations
- CloudKit sync
- Cross-device scenarios

## Security

### Data Protection

- iOS/macOS sandboxing
- Keychain for sensitive data (if needed)
- Encrypted iCloud storage
- No network transmission (except iCloud)

### Privacy

- No analytics
- No tracking
- No third-party SDKs
- Local-first architecture

## Accessibility

### VoiceOver Support

- Labeled UI elements
- Semantic descriptions
- Accessible navigation

### Dynamic Type

- Scalable fonts
- Flexible layouts
- Readable text

### Other Features

- High contrast support
- Reduce motion support
- Keyboard navigation (Mac)

## Localization

### Current Status

- English only (initial release)

### Future Plans

- Internationalization support
- Multiple languages
- Regional formats
- Currency localization

## Build Configuration

### Debug

- Verbose logging
- Test data generation
- Development features

### Release

- Optimized build
- Minimal logging
- Production configuration

## Receipt Scanner Architecture

### On-Device AI Pipeline

The receipt scanner uses a two-stage pipeline:

#### Stage 1: Text Extraction (Vision)
```
Receipt Image
    ↓
Image Preprocessing (resize, grayscale, contrast)
    ↓
VNRecognizeTextRequest (Vision framework)
    ↓
Raw Text + Confidence Scores
```

#### Stage 2: Intelligent Parsing (Foundation Models)
```
Raw Text
    ↓
SystemLanguageModel (Apple Intelligence)
    ↓
Guided Generation with Schema
    ↓
Structured Data (merchant, amount, date)
```

### AI Model Details

**Foundation Models Integration:**
- Uses Apple's on-device language models
- Qwen 1.7B 4-bit quantized model
- Runs entirely on device (no cloud)
- Guided generation for structured output
- 10-second timeout for responsiveness

**Privacy & Performance:**
- Zero network requests
- All processing on-device
- Fast inference (~2 seconds)
- Low memory footprint
- Works offline

### Fallback Strategy

If Apple Intelligence is unavailable:
- Falls back to Vision OCR only
- Basic pattern matching for amounts
- Manual field entry encouraged
- Graceful degradation

## Dependencies

### First-Party Only

Money In & Out uses only Apple frameworks:

- SwiftUI
- SwiftData
- CloudKit
- Foundation
- Combine
- Vision
- Foundation Models (Apple Intelligence)

**No third-party dependencies** - Keeps the app:
- Lightweight
- Secure
- Maintainable
- Privacy-focused

## Design Patterns

### Used Patterns

- **MVVM** - Architecture
- **Repository** - Data access
- **Observer** - State updates
- **Factory** - Object creation
- **Singleton** - Shared resources

### Avoided Patterns

- **Massive View Controller** - Use MVVM instead
- **God Object** - Keep classes focused
- **Tight Coupling** - Use protocols and DI

## Code Style

### Swift Guidelines

- Follow Swift API Design Guidelines
- Use meaningful names
- Document public APIs
- Keep functions small
- Prefer value types

### SwiftUI Best Practices

- Small, focused views
- Extract reusable components
- Use view modifiers
- Leverage environment

## Future Architecture Considerations

### Potential Improvements

- Modular architecture
- Plugin system
- Widget support
- Shortcuts integration
- Watch app

### Scalability

Current architecture supports:
- Thousands of transactions
- Hundreds of categories
- Multiple devices
- Years of data

## Contributing

### Code Standards

- Follow existing patterns
- Write tests
- Document changes
- Keep it simple

### Pull Request Process

1. Fork repository
2. Create feature branch
3. Write tests
4. Submit PR
5. Code review

## Resources

### Apple Documentation

- [SwiftUI](https://developer.apple.com/xcode/swiftui/)
- [SwiftData](https://developer.apple.com/xcode/swiftdata/)
- [CloudKit](https://developer.apple.com/icloud/cloudkit/)

### Design Guidelines

- [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/)
- [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
