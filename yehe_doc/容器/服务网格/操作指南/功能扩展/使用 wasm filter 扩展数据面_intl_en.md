Wasm is short for WebAssembly, which can compile binary instructions and load them into the Envoy's filter chain to extend mesh data plane capabilities. In this way, Envoy and extension components are decoupled, and users no longer need to extend capabilities by modifying Envoy code and compiling special Envoy versions. In addition, wasm delivers advantages of dynamic loading and secure isolation.

Since Istio 1.6, the Proxy-Wasm sandbox API has replaced Mixer as a main extension implementation of Istio to implement the interaction between Envoy and wasm virtual machines. Therefore, to extend Envoy through a wasm filter, you need to use [Proxy-WASM SDK](https://github.com/proxy-wasm/spec). 

Usually, steps of compiling a wasm file to extend mesh data plane capabilities include the following:

1. Compile a wasm filter by following [Examples](https://github.com/envoyproxy/envoy-wasm/tree/19b9fd9a22e27fcadf61a06bf6aac03b735418e6/examples/wasm).
2. Inject the wasm filter into a ConfigMap to mount the wasm filter to any workload through the ConfigMap, thereby preventing the wasm filter from being copied to multiple nodes.
   ```bash
   kubectl create cm -n foo example-filter --from-file=example-filter.wasm
   ```
3. Mount the wasm filter to a service workload. You can use [Istio Annotations](https://istio.io/latest/docs/reference/config/annotations/) to enable a corresponding file to be automatically mounted when creating a workload.
   ```yaml
   sidecar.istio.io/userVolume: '[{"name":"wasmfilters-dir","configMap": {"name": "example-filter"}}]'
   sidecar.istio.io/userVolumeMount: '[{"mountPath":"/var/local/lib/wasm-filters","name":"wasmfilters-dir"}]'
   ```
   Apply the annotation to the corresponding workload.
   ```bash
   
   kubectl patch deployment -n foo frontpage-v1 -p '{"spec":{"template":{"metadata":{"annotations":{"sidecar.istio.io/userVolume":"[{\"name\":\"wasmfilters-dir\",\"configMap\": {\"name\": \"example-filter\"}}]","sidecar.istio.io/userVolumeMount":"[{\"mountPath\":\"/var/local/lib/wasm-filters\",\"name\":\"wasmfilters-dir\"}]"}}}}}'
   ```
4. Create an Envoy filter, and add the wasm filter to the Envoy filter chain of the corresponding workload to have it to take effect.
   ```yaml
    apiVersion: networking.istio.io/v1alpha3
    kind: EnvoyFilter
    metadata:
      name: frontpage-v1-examplefilter
      namespace: foo
    spec:
      configPatches:
      - applyTo: HTTP_FILTER
        match:
          listener:
            filterChain:
              filter:
                name: envoy.http_connection_manager
                subFilter:
                  name: envoy.router
        patch:
          operation: INSERT_BEFORE
          value:
            name: envoy.filters.http.wasm
            typed_config:
              '@type': type.googleapis.com/envoy.extensions.filters.http.wasm.v3.Wasm
              config:
                name: example-filter
                root_id: my_root_id
                vm_config:
                  code:
                    local:
                      filename: /var/local/lib/wasm-filters/example-filter.wasm
                  runtime: envoy.wasm.runtime.v8
                  vm_id: example-filter
                  allow_precompiled: true 
      workloadSelector:
        labels:
          app: frontpage
          version: v1
   
   ```



Till now, the wasm filter has been deployed. The wasm filter can also be used as an image. For details, see [Build a wasm filter image](https://docs.solo.io/web-assembly-hub/latest/tutorial_code/getting_started/). For details about how to use the wasme tool to deploy the wasm filter, see [Deploying Wasm Filters with Wasme](https://docs.solo.io/web-assembly-hub/latest/tutorial_code/deploy_tutorials/deploying_with_istio/).

It can be seen that the deployment of a wasm filter is cumbersome, especially when large-scale deployment is required. It is difficult to deploy and manage a batch of wasm filters without a tool. Tencent Cloud Mesh provides convenient deployment tools, which can be used to deploy a batch of wasm filters in the binary or image format to services. For details, see [Using Tencent Cloud Mesh Tools to Deploy Wasm Filters in Batches](https://intl.cloud.tencent.com/document/product/1152/47492).

