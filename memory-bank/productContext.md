# Product Context: OpenTelemetry Demo

## Why This Project Exists

### Problem Statement
Developers and organizations need:
- **Clear Examples**: Real-world examples of how to instrument applications with OpenTelemetry
- **Multi-Language Coverage**: Examples across different programming languages and frameworks
- **Integration Patterns**: Demonstrations of how to integrate OpenTelemetry with various observability backends
- **Testing Platform**: A reliable system to test OpenTelemetry features and changes

### Solution
The OpenTelemetry Demo provides a complete, realistic e-commerce application (Astronomy Shop) that:
- Shows OpenTelemetry instrumentation across 10+ programming languages
- Demonstrates distributed tracing, metrics, and logging
- Integrates with popular observability backends (Jaeger, Grafana, Prometheus, etc.)
- Serves as a reference implementation for best practices

## How It Should Work

### User Experience Flow
```
User → Frontend → Multiple Microservices → Observability Backend
```

1. **End Users**: Browse the Astronomy Shop, add items to cart, checkout
2. **Developers**: Learn from code examples, instrument their own services
3. **Vendors**: Fork and customize to showcase their observability platforms
4. **Contributors**: Test new OpenTelemetry features and improvements

### Key User Journeys

#### For Developers Learning OpenTelemetry
1. Clone the repository
2. Start the demo (`make start`)
3. Browse the code to see instrumentation examples
4. View traces/metrics/logs in observability UIs
5. Understand how services communicate and generate telemetry

#### For Vendors Demonstrating Platforms
1. Fork the repository
2. Configure their observability backend
3. Customize services as needed
4. Showcase their platform's capabilities

#### For Contributors Testing Features
1. Make changes to OpenTelemetry instrumentation
2. Test across multiple services and languages
3. Verify telemetry generation and export
4. Submit improvements back to the project

## User Experience Goals

### Primary Goals
- **Clarity**: Code examples should be easy to understand
- **Completeness**: Cover common instrumentation scenarios
- **Reliability**: Demo should run consistently across environments
- **Performance**: Reasonable resource usage for local development

### Secondary Goals
- **Extensibility**: Easy to add new services or modify existing ones
- **Documentation**: Clear READMEs and inline comments
- **Testing**: Automated tests to ensure quality
- **Community**: Welcoming environment for contributors

## Problems It Solves

1. **"How do I instrument my [language] service?"** → See examples in corresponding service directory
2. **"How do traces flow through my system?"** → View distributed traces in Jaeger UI
3. **"What metrics should I collect?"** → See examples of business and technical metrics
4. **"How do I integrate with [observability backend]?"** → See collector configuration examples
5. **"How do I test OpenTelemetry changes?"** → Use the demo as a testbed
