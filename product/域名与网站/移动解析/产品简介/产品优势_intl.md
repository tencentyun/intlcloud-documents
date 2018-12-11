In principle, HttpDNS only replaces the domain name resolution protocol from DNS to HTTP, which is not complicated. However, this tiny change brings huge benefits:
#### Fixing Domain Name Resolution Exceptions
By bypassing the ISP's LocalDNS, end user's request to resolve the domain name is directly passed to the server IP of HttpDNS through the HTTP protocol, eliminating the possible exceptions caused to end user's domain name resolution request initiated in a client.
#### Accurate Scheduling
HttpDNS can directly obtain the IP of the end user and generate an IP library and speed testing system using patented DNSPod technology which help ensure the redirection of the end user to the fastest IDC node.
#### Low Cost of Implementation
For a business that is connected to HttpDNS, you only need to make a few of modifications to the client's access layer, without requiring the end user's mobile phone to be rooted or jailbroken. Moreover, since the HTTP protocol's request structure is very simple, it is compatible with various types of mobile operating systems. In short, it only takes the minimal cost of transformation to solve the problems with domain name resolution exceptions and meet the requirements of accurate traffic scheduling for the business.
#### Strong Scalability
HttpDNS provides a reliable domain name resolution service. You can combine your own scheduling logic with the HttpDNS return result to achieve even more refined traffic scheduling. For example, HttpDNS is able to direct clients of different version to the requested IP address and end users of different network types to specific IP address.

In summary, HttpDNS can effectively avoid the issues where the inaccessibility to the expected optimal access point due to the exceptions of LocalDNS used by mobile internet users eventually causes their inability to access your business properly.
