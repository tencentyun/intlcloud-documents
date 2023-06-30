Call tracing information displayed through the UI is incomplete, for example, information about a previous or next call trace is absent.

## Cause

In most cases, it is because the HTTP headers required for tracing are not passed correctly or not passed at the service layer.

Using call tracing in Istio does not mean that services are non-intrusive. There is a basic requirement that a service needs to pass a received tracing-related header to a called service. This step cannot be done by Istio because Istio cannot perceive your service logic and does not know the previous request to which the request for the service to call another service corresponds. Therefore, the service needs to pass the header, and finally the traces can be chained completely.

