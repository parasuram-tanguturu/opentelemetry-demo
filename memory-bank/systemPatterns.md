# System Patterns: OpenTelemetry Demo

## Architecture Overview

### High-Level Architecture
```
┌─────────────┐
│   Frontend  │ (React/TypeScript)
└──────┬──────┘
       │
       ▼
┌─────────────┐
│Frontend Proxy│ (Envoy)
└──────┬──────┘
       │
       ├──► Cart Service (.NET)
       ├──► Product Catalog (Go)
       ├──► Currency Service (C++)
       ├──► Ad Service (Java)
       ├──► Recommendation (Python)
       ├──► Product Reviews (Python)
       ├──► Quote Service (PHP)
       ├──► Shipping Service (Rust)
       ├──► Payment Service (Node.js)
       ├──► Email Service (Ruby)
       ├──► Checkout Service (Go)
       ├──► Accounting Service (.NET)
       └──► Fraud Detection (Kotlin)
       
       │
       ▼
┌─────────────┐
│OTel Collector│
└──────┬──────┘
       │
       ├──► Jaeger (Traces)
       ├──► Prometheus (Metrics)
       ├──► Grafana (Visualization)
       └──► OpenSearch (Logs)
```

## Microservices Architecture

### Service Communication Patterns

#### Synchronous (HTTP/gRPC)
- **Frontend → Services**: REST API calls through Envoy proxy
- **Service-to-Service**: Direct HTTP/gRPC calls
- **Protocol Buffers**: Used for gRPC communication (`pb/demo.proto`)

#### Asynchronous (Message Queue)
- **Kafka**: Used for event-driven communication
  - Checkout service publishes events
  - Accounting service consumes events
- **Event Types**: Order processing, payment events

### Service Responsibilities

#### Frontend Services
- **frontend**: React/TypeScript web application
- **frontend-proxy**: Envoy proxy for routing and observability

#### Core Business Services
- **cart**: Shopping cart management (.NET)
- **product-catalog**: Product information (Go)
- **product-reviews**: Customer reviews (Python)
- **recommendation**: Product recommendations (Python)

#### Supporting Services
- **currency**: Currency conversion (C++)
- **ad**: Advertisement display (Java)
- **quote**: Shipping quotes (PHP)
- **shipping**: Shipping management (Rust)
- **payment**: Payment processing (Node.js)
- **email**: Email notifications (Ruby)
- **checkout**: Order processing (Go)
- **accounting**: Financial records (.NET)
- **fraud-detection**: Fraud analysis (Kotlin)

#### Infrastructure Services
- **otel-collector**: OpenTelemetry Collector for telemetry processing
- **kafka**: Message broker
- **postgresql**: Database
- **flagd**: Feature flag service
- **flagd-ui**: Feature flag management UI (Elixir)
- **image-provider**: Static image serving (Nginx)
- **load-generator**: Synthetic traffic generation

#### Observability Stack
- **jaeger**: Distributed tracing backend
- **prometheus**: Metrics storage
- **grafana**: Visualization and dashboards
- **opensearch**: Log aggregation

## Design Patterns

### Observability Patterns

#### 1. Auto-Instrumentation
- Most services use OpenTelemetry auto-instrumentation agents
- Minimal code changes required
- Example: Java services use `opentelemetry-javaagent`

#### 2. Manual Instrumentation
- Some services demonstrate manual instrumentation
- Custom spans, metrics, and logs
- Example: Custom business metrics in checkout service

#### 3. Context Propagation
- Trace context propagated across service boundaries
- HTTP headers for trace context
- gRPC metadata for trace context

#### 4. Resource Attributes
- Services set resource attributes (service name, version, etc.)
- Environment variables for configuration
- Consistent naming conventions

### Deployment Patterns

#### Docker Compose
- Primary deployment method for local development
- Service dependencies defined
- Health checks configured
- Resource limits set

#### Kubernetes
- Production-ready deployment option
- Helm charts available
- Generated manifests in `kubernetes/` directory

### Testing Patterns

#### Integration Tests
- Frontend tests
- Trace-based tests using Tracetest
- Test definitions in `test/tracetesting/`

#### Load Testing
- Synthetic traffic generation
- Configurable load patterns
- UI for load generator at `/loadgen/`

## Key Technical Decisions

### Why Multiple Languages?
- Demonstrates OpenTelemetry's language-agnostic nature
- Shows instrumentation patterns across ecosystems
- Realistic representation of polyglot systems

### Why Microservices?
- Represents real-world distributed systems
- Generates realistic distributed traces
- Demonstrates cross-service observability

### Why Docker Compose?
- Easy local development
- Consistent environment
- Quick startup for demos

### Why Envoy Proxy?
- Industry-standard service mesh proxy
- Built-in observability features
- Demonstrates proxy-level instrumentation

## Component Relationships

### Data Flow
1. User request → Frontend
2. Frontend → Envoy Proxy
3. Envoy → Backend Services
4. Services → Database/Kafka
5. Services → OTel Collector
6. Collector → Observability Backends

### Telemetry Flow
1. Services generate telemetry (traces/metrics/logs)
2. Telemetry sent to OTel Collector via OTLP
3. Collector processes and exports to backends
4. Backends store and index telemetry
5. UIs query backends for visualization

### Event Flow
1. Checkout service processes order
2. Publishes events to Kafka
3. Accounting service consumes events
4. Updates financial records
5. Generates telemetry for all steps
