# Apache SkyWalking data collect protocol
Apache SkyWalking typically collect data from 
1. Traces
2. Metrics(Meter system)
3. Logs
4. Command data. Push the commands to the agents from Server.
5. Event. 
6. eBPF profiling tasks.
7. Agent in-process profiling tasks.

This repo hosts the protocol of SkyWalking native report protocol, defined in gRPC. Read [Protocol DOC](https://skywalking.apache.org/docs/main/next/en/api/trace-data-protocol-v3/) for more details

## Development

### Building with Bazel

This repository uses [Bazel](https://bazel.build/) as its build system with [Bzlmod](https://bazel.build/external/overview#bzlmod) enabled.

Build all targets:
```bash
bazel build //...
```

### Protocol Buffer Best Practices

This repository uses [Buf](https://buf.build/) for protocol buffer linting and formatting to ensure code quality and consistency.

#### Running Lint Checks

To run buf lint checks on protocol buffers:
```bash
# Lint specific packages
bazel test //common:common_protocol_proto_lint
bazel test //language-agent:tracing_protocol_proto_lint
bazel test //language-agent:configuration_discovery_service_proto_lint
```

#### Formatting Protocol Buffers

To format all protocol buffer files:
```bash
bazel run //:buf_format
```

To check formatting without modifying files (useful in CI):
```bash
bazel run //:buf_format -- -d
```

#### Buf Configuration

The buf configuration is defined in `buf.yaml` at the repository root. The configuration specifies:
- Linting rules (with some exceptions for existing code compatibility)
- Breaking change detection rules
- Ignored paths

## Release
This repo wouldn't release separately. All source codes have been included in the main repo release. The tags match the [main repo](https://github.com/apache/skywalking) tags.

## License
Apache 2.0
