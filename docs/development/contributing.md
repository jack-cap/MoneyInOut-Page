# Contributing

Thank you for your interest in contributing to Money In & Out!

## Current Status

Money In & Out is currently **not open source**. However, we welcome:

- Bug reports
- Feature suggestions
- Documentation improvements
- Feedback and ideas

## How to Contribute

### Reporting Bugs

Found a bug? Help us fix it:

1. **Check existing issues** - May already be reported
2. **Create detailed report** - See [Support](../support.md) for what to include
3. **Email us** - Send to MoneyIO@thecapitalyst.com

### Suggesting Features

Have an idea? We'd love to hear it:

1. **Check if already suggested** - Review existing requests
2. **Describe the feature** - What and why
3. **Explain use case** - How you'd use it
4. **Email us** - Send your suggestion

### Improving Documentation

Documentation improvements are always welcome:

1. **Identify issues** - Unclear, outdated, or missing docs
2. **Suggest improvements** - What should change
3. **Submit corrections** - Email us with details

## Development Setup

If Money In & Out becomes open source in the future:

### Requirements

- macOS 26.0+
- Xcode 15.0+
- Apple Developer account (for testing on device)

### Getting Started

```bash
# Clone repository
git clone https://github.com/jack-cap/MoneyInOut-Page.git

# Open in Xcode
cd money-in-out
open "Money In & Out.xcodeproj"

# Build and run
⌘ + R
```

### Project Structure

See [Architecture](architecture.md) for detailed structure.

## Coding Standards

### Swift Style

Follow [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/):

- Clear, descriptive names
- Prefer clarity over brevity
- Use camelCase
- Document public APIs

### SwiftUI Best Practices

- Small, focused views
- Extract reusable components
- Use view modifiers
- Leverage environment

### Code Organization

- Group related files
- Use extensions for protocol conformance
- Keep files under 300 lines
- One type per file (generally)

## Testing

### Requirements

- Write tests for new features
- Update tests for changes
- Ensure all tests pass
- Maintain test coverage

### Running Tests

```bash
# Run all tests
⌘ + U

# Run specific test
Click diamond icon next to test
```

See [Testing](testing.md) for detailed guide.

## Pull Request Process

If/when open source:

### Before Submitting

1. **Create feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make changes**
   - Follow coding standards
   - Write tests
   - Update documentation

3. **Test thoroughly**
   - Run all tests
   - Test on device
   - Check different scenarios

4. **Commit changes**
   ```bash
   git commit -m "Add feature: description"
   ```

### Submitting PR

1. **Push to fork**
   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create pull request**
   - Clear title
   - Detailed description
   - Link related issues
   - Include screenshots if UI changes

3. **PR template**
   ```markdown
   ## Description
   Brief description of changes
   
   ## Type of Change
   - [ ] Bug fix
   - [ ] New feature
   - [ ] Documentation update
   
   ## Testing
   How was this tested?
   
   ## Screenshots
   If applicable
   ```

### Code Review

- Address feedback promptly
- Be open to suggestions
- Keep discussions professional
- Update PR as needed

## Design Philosophy

### Core Principles

1. **Simplicity** - Keep it simple
2. **Privacy** - No data collection
3. **Performance** - Fast and responsive
4. **Reliability** - Stable and predictable

### What We Avoid

- Unnecessary features
- Complex UI
- Third-party dependencies
- Data collection
- Ads and tracking

## Feature Requests

### Evaluation Criteria

We consider:

- **Alignment** - Fits our philosophy?
- **Simplicity** - Keeps app simple?
- **Value** - Benefits users?
- **Maintenance** - Sustainable to maintain?

### Likely to Accept

- Bug fixes
- Performance improvements
- Accessibility enhancements
- Documentation improvements
- Simple, focused features

### Unlikely to Accept

- Complex features
- Third-party integrations
- Features requiring data collection
- Anything compromising privacy
- Features that bloat the app

## Communication

### Be Respectful

- Professional and courteous
- Constructive feedback
- Assume good intentions
- Respect decisions

### Response Time

- We aim to respond within 48 hours
- Complex issues may take longer
- Be patient with reviews

## License

Currently proprietary. If open sourced, will use permissive license (likely MIT or Apache 2.0).

## Recognition

Contributors will be:

- Credited in release notes
- Listed in app (if significant contribution)
- Thanked publicly

## Future Plans

### Potential Open Source

We're considering open sourcing Money In & Out:

**Pros:**
- Community contributions
- Transparency
- Faster development
- Learning resource

**Cons:**
- Maintenance burden
- Quality control
- Support overhead

We'll announce if/when we open source.

## Questions?

Have questions about contributing?

- Email: MoneyIO@thecapitalyst.com
- Check [FAQ](../faq.md)
- Review [Support](../support.md)

## Thank You

Thank you for your interest in improving Money In & Out! Every contribution, big or small, helps make the app better for everyone.

---

**Note**: This guide will be updated if/when Money In & Out becomes open source.
