# Microservices Demo

A demo application with Java, Go, Javascript, Kafka and PostgresQL replicating this repository: https://github.com/okteto-community/microservices-demo

But using [Kubernetes Gateway API](https://gateway-api.sigs.k8s.io/) `HTTPRoute` objects instead of traditional `Ingress` resources, deployed and developed with [Okteto](https://okteto.com).

## HTTPRoute and parentRefs

The `HTTPRoute` object in in both services Result and Vote **omits the `parentRefs` field**.

This is designed to run in an Okteto instance where the Helm setting `endpoints.dev.gatewayAPI.gateway.force` is set to `true`. When that setting is enabled, Okteto automatically injects the required `parentRef` pointing to the cluster's gateway, so you don't need to specify it manually.

If `endpoints.dev.gatewayAPI.gateway.force` is `false` (the default), you must add the `parentRefs` field explicitly to your `HTTPRoute`:

```yaml
parentRefs:
  - kind: Gateway
    name: <GATEWAY_NAME>
    namespace: <GATEWAY_NAMESPACE>
    group: gateway.networking.k8s.io
```

