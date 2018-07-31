## Tailor log
#### Istio version
v1.0.0

### AT FIRST
```bash
kubectl create namespace istio-system
```

### Replace / Remove fields
| field | origin status | edited |
|--|--|--|
| disablePolicyChecks | `false` | `true` |
| enableTracing | `true` | `false` |
| mixerCheckServer | istio-policy.istio-system.svc.cluster.local:9091 | `disabled` | 
| mixerReportServer | istio-telemetry.istio-system.svc.cluster.local:9091 | `disabled` |
| zipkinAddress | zipkin.istio-system:9411 | `disabled` |
| prometheus | `enabled` | `disabled` `Todo` `L:2116` |
| --zipkinAddress | `specified` | `disabled` `L:2205-2206` |
| --zipkinAddress | `specified` | `disabled` `L:2347-2348` |
| --trace_zipkin_url | `specified` | `disabled` `L:2516` |
| --trace_zipkin_url | `specified` | `disabled` `L:2613` |
| prometheus | `enabled` | `disabled` `Todo` `L:2824` |
| HorizontalPodAutoscaler: istio-egressgateway | / | T.B.D. |
| HorizontalPodAutoscaler: istio-ingressgateway | / | T.B.D. |
| HorizontalPodAutoscaler: istio-policy | / | T.B.D. |
| HorizontalPodAutoscaler: istio-telemetry | / | T.B.D. |
| HorizontalPodAutoscaler: istio-pilot | / | T.B.D. |

### Images
| App | Image | localImage |
|--|--|--|
| statsd-prom-bridge | docker.io/prom/statsd-exporter:v0.6.0 | |
| istio-egressgateway | docker.io/istio/proxyv2:1.0.0 | |
| istio-ingressgateway | docker.io/istio/proxyv2:1.0.0 | |
| mixer | docker.io/istio/mixer:1.0.0 | |
| istio-proxy | docker.io/istio/proxyv2:1.0.0 | |
| pilot | docker.io/istio/pilot:1.0.0 | |
| prometheus | docker.io/prom/prometheus:v2.3.1 | *remove it* |
| citadel | docker.io/istio/citadel:1.0.0 | |
