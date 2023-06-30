Image signature and signature verification can avoid man-in-the-middle attacks and the update and running of invalid images, ensuring image consistency across the entire linkage ranging from distribution to deployment.

### Container image signature
TCR Enterprise Edition supports namespace-level automatic image signature. When an image is pushed to the registry, it will be automatically signed according to the matched signature policy to ensure image content trustworthiness in your registry.
### Image signature verification
TKE provides the image signature verification add-on Cerberus, which verifies signed images for trustworthiness. This is to ensure that only container images signed by trusted authorizing parties are deployed in TKE clusters, thereby reducing the risks to image security in the container environment.
