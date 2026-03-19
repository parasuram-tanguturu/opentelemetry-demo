# Technical Context: OpenTelemetry Demo

## Technologies Used

### Programming Languages & Frameworks

#### Frontend
- **TypeScript/React**: Main web application (`src/frontend/`)
- **React Native**: Mobile application (`src/react-native-app/`)
- **Node.js**: Payment service (`src/payment/`)

#### Backend Services
- **Go**: 
  - Checkout service (`src/checkout/`)
  - Product Catalog service (`src/product-catalog/`)
- **.NET/C#**: 
  - Cart service (`src/cart/`)
  - Accounting service (`src/accounting/`)
- **Java**: 
  - Ad service (`src/ad/`)
- **Kotlin**: 
  - Fraud Detection service (`src/fraud-detection/`)
- **Python**: 
  - Recommendation service (`src/recommendation/`)
  - Product Reviews service (`src/product-reviews/`)
- **Rust**: 
  - Shipping service (`src/shipping/`)
- **C++**: 
  - Currency service (`src/currency/`)
- **PHP**: 
  - Quote service (`src/quote/`)
- **Ruby**: 
  - Email service (`src/email/`)
- **Elixir**: 
  - Flagd UI (`src/flagd-ui/`)

### Infrastructure & Tools

#### Containerization
- **Docker**: Container runtime
- **Docker Compose**: Orchestration for local development
- **BuildKit**: Multi-platform builds

#### Service Mesh & Proxy
- **Envoy**: Frontend proxy (`src/frontend-proxy/`)

#### Message Queue
- **Apache Kafka**: Event streaming (`src/kafka/`)

#### Databases
- **PostgreSQL**: Relational database (`src/postgresql/`)

#### Observability Stack
- **OpenTelemetry Collector**: Telemetry processing (`src/otel-collector/`)
- **Jaeger**: Distributed tracing backend (`src/jaeger/`)
- **Prometheus**: Metrics storage (`src/prometheus/`)
- **Grafana**: Visualization (`src/grafana/`)
- **OpenSearch**: Log aggregation (`src/opensearch/`)

#### Feature Flags
- **Flagd**: Feature flag service (`src/flagd/`)
- **Flagd UI**: Management interface (`src/flagd-ui/`)

#### Other Infrastructure
- **Nginx**: Image provider (`src/image-provider/`)
- **Load Generator**: Synthetic traffic (`src/load-generator/`)

### Build Tools & Package Managers

- **npm**: Node.js dependencies (`package.json`)
- **Gradle**: Java/Kotlin builds
- **Maven**: Java dependencies (via Gradle)
- **Go Modules**: Go dependencies (`go.mod`, `go.sum`)
- **NuGet**: .NET packages
- **pip**: Python packages
- **Cargo**: Rust packages
- **Composer**: PHP packages
- **Bundler**: Ruby packages
- **Mix**: Elixir packages
- **CMake**: C++ builds

### Protocol & Communication

- **Protocol Buffers**: gRPC service definitions (`pb/demo.proto`)
- **gRPC**: Inter-service communication
- **REST/HTTP**: API endpoints
- **OTLP**: OpenTelemetry Protocol for telemetry export

## Development Setup

### Prerequisites
- Docker and Docker Compose
- Make (for running Makefile commands)
- Git

### Environment Configuration
- `.env`: Base environment variables
- `.env.override`: Local overrides
- `.env.arm64`: ARM64-specific overrides (for Apple Silicon)

### Key Environment Variables
- `IMAGE_NAME`: Docker image name prefix
- `DEMO_VERSION`: Version tag for images
- `OTEL_COLLECTOR_HOST`: Collector hostname
- `OTEL_COLLECTOR_PORT_HTTP`: Collector HTTP port
- `OTEL_EXPORTER_OTLP_ENDPOINT`: OTLP endpoint URL
- `OTEL_SERVICE_NAME`: Service name for telemetry
- `OTEL_RESOURCE_ATTRIBUTES`: Additional resource attributes

### Build Process

#### Multi-Platform Builds
- Supports `linux/amd64` and `linux/arm64`
- Uses Docker Buildx for multi-platform builds
- Configured in `buildkitd.toml`

#### Build Commands
- `make build`: Build all services
- `make build-multiplatform`: Build for multiple platforms
- `make build-and-push`: Build and push to registry

### Code Generation

#### Protocol Buffer Generation
- `make generate-protobuf`: Generate protobuf code for IDE
- `make docker-generate-protobuf`: Generate protobuf code in Docker
- Scripts: `ide-gen-proto.sh`, `docker-gen-proto.sh`

#### Kubernetes Manifest Generation
- `make generate-kubernetes-manifests`: Generate K8s manifests from Helm charts

## Technical Constraints

### Resource Limits
- Services have memory limits defined in `docker-compose.yml`
- Typical limits: 160M-300M per service
- Total system requires significant resources when running all services

### Platform Compatibility
- Primary target: Linux containers
- ARM64 support for Apple Silicon Macs
- Java workaround for macOS 15.2+ and M4 chips

### Version Constraints
- OpenTelemetry versions specified per language
- Docker Compose version compatibility
- Kubernetes version compatibility (for K8s deployment)

## Dependencies

### External Dependencies
- OpenTelemetry SDKs and agents (language-specific)
- Observability backends (Jaeger, Prometheus, Grafana)
- Infrastructure components (Kafka, PostgreSQL)

### Internal Dependencies
- Shared protobuf definitions (`pb/demo.proto`)
- Common build tools (`internal/tools/`)
- Test infrastructure (`test/`)

## Development Workflow

### Local Development
1. Clone repository
2. Copy `.env.override` if needed
3. Run `make start` to start all services
4. Access UI at `http://localhost:8080`
5. View traces at `http://localhost:8080/jaeger/ui`
6. View metrics at `http://localhost:8080/grafana/`

### Testing
- `make run-tests`: Run integration tests
- `make run-tracetesting`: Run trace-based tests
- Frontend tests: Automated UI tests
- Trace tests: Validate telemetry generation

### Code Quality
- `make check`: Run all checks (spelling, markdown lint, license, links)
- `make fix`: Auto-fix issues where possible
- Markdown linting: `.markdownlint.yaml`
- YAML linting: `yamllint`

## Deployment Options

### Docker Compose (Default)
- `make start`: Start full demo
- `make start-minimal`: Start minimal version
- `make stop`: Stop all services

### Kubernetes
- Helm charts available
- Generated manifests in `kubernetes/opentelemetry-demo.yaml`
- Deploy to any Kubernetes cluster

## Known Technical Considerations

### Java Services
- Requires OpenTelemetry Java agent
- Version specified via `OTEL_JAVA_AGENT_VERSION`
- macOS ARM64 workaround for JDK bug

### .NET Services
- Entity Framework Core instrumentation can be disabled
- Configured via `OTEL_DOTNET_AUTO_TRACES_ENTITYFRAMEWORKCORE_INSTRUMENTATION_ENABLED`

### Go Services
- Uses OpenTelemetry Go SDK
- Protocol buffer generation required
- gRPC dependencies managed via Go modules

### Python Services
- Uses OpenTelemetry Python SDK
- Protocol buffer generation for gRPC
- Virtual environment recommended
