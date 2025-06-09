# Kubernetes Template Project

The readiness-condition-reporter is a library for publishing component-readiness as a Kubernetes Node status. This could be used for simplifying legacy component integration with [Node-Readiness-Gates](https://github.com/ajaysundark/node-readiness-gate-controller).

Here's how it could be integrated as a side-car container:

```yaml
# readiness-condition-reporter sidecar
spec:
  template:
    spec:
      serviceAccountName: node-status-patcher-sa
      initContainers:
      - name: readiness-reporter
        image: ghcr.io/ajaysundark/readiness-condition-reporter:0.1.0
        env:
        - name: NODE_NAME # injected from downward api
          valueFrom:
            fieldRef:
              fieldPath: spec.nodeName
        - name: CHECK_ENDPOINT
          value: "http://localhost:8080/health"
        - name: CONDITION_TYPE
          value: "COMPONENT_READY" # condition-type to update
        - name: CHECK_INTERVAL
          value: "15s"
```

## Community, discussion, contribution, and support

Learn how to engage with the Kubernetes community on the [community page](http://kubernetes.io/community/).

You can reach the maintainers of this project at:

- [Slack](https://slack.k8s.io/)
- [Mailing List](https://groups.google.com/a/kubernetes.io/g/dev)

### Code of conduct

Participation in the Kubernetes community is governed by the [Kubernetes Code of Conduct](code-of-conduct.md).

[owners]: https://git.k8s.io/community/contributors/guide/owners.md
[Creative Commons 4.0]: https://git.k8s.io/website/LICENSE
