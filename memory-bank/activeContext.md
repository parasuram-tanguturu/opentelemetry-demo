# Active Context: OpenTelemetry Demo

## Current Work Focus

### Initial Setup
- Memory bank creation and documentation
- Understanding project structure and architecture
- Establishing baseline knowledge of the codebase

## Recent Changes

### Project State
- This is the official OpenTelemetry Demo repository
- Actively maintained by OpenTelemetry community
- Regular SIG calls every other Wednesday
- Multiple vendors maintain forks for their platforms

## Next Steps

### Immediate Priorities
1. **Complete Memory Bank**: Ensure all core documentation files are created
2. **Understand Current State**: Review any open issues or recent changes
3. **Identify Work Areas**: Determine what improvements or features might be needed

### Potential Work Areas

#### Code Quality
- Review instrumentation patterns
- Ensure consistency across services
- Update dependencies as needed

#### Documentation
- Improve service-specific READMEs
- Add more examples
- Clarify setup instructions

#### Features
- Add new services (if needed)
- Enhance existing services
- Improve observability coverage

#### Testing
- Expand test coverage
- Add more trace-based tests
- Improve integration tests

## Active Decisions and Considerations

### Architecture Decisions
- Multi-language approach maintained for realism
- Docker Compose as primary local development method
- Kubernetes support for production deployments

### Observability Decisions
- OTLP as primary telemetry protocol
- Collector-based architecture for flexibility
- Multiple backends supported (Jaeger, Prometheus, Grafana)

### Community Decisions
- Open to contributions from community
- Buddy system for new contributors
- Regular SIG calls for coordination

## Current Context Notes

### Project Health
- Active development and maintenance
- Strong community involvement
- Multiple vendor integrations
- Comprehensive test coverage

### Key Files to Monitor
- `docker-compose.yml`: Service definitions
- `Makefile`: Build and run commands
- `README.md`: Project overview
- `CONTRIBUTING.md`: Contribution guidelines
- Service-specific READMEs: Individual service documentation

### Important Directories
- `src/`: All microservice source code
- `test/`: Test infrastructure
- `kubernetes/`: Kubernetes deployment manifests
- `pb/`: Protocol buffer definitions
- `memory-bank/`: Project documentation (this directory)

## Questions to Resolve

### When Starting New Work
1. What specific feature or improvement is needed?
2. Which service(s) are affected?
3. Does it require changes to multiple services?
4. Are there existing patterns to follow?
5. Does it need documentation updates?
6. Are tests needed or updates required?

### When Contributing
1. Is there an existing issue or discussion?
2. Have you signed the CLA?
3. Do you have a buddy/mentor?
4. Have you reviewed CONTRIBUTING.md?
5. Are you following the coding standards?

## Work Patterns

### Common Tasks
- **Adding Instrumentation**: Follow patterns in similar services
- **Adding Services**: Use existing services as templates
- **Updating Dependencies**: Test across all affected services
- **Fixing Bugs**: Reproduce, fix, test, document

### Testing Patterns
- Run full demo locally
- Check telemetry generation
- Verify UI functionality
- Run automated tests
- Check for regressions

### Documentation Patterns
- Update service READMEs when changing services
- Update main README for major changes
- Document new features
- Keep examples up to date
