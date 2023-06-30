<table>
<thead>
<tr>
<th><strong>Benefits</strong></th>
<th style="text-align:center;"><strong>With Auto Scaling</strong></th>
<th style="text-align:center;"><strong>Without Auto Scaling</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Automatic</strong></td>
<td><strong>Automatically scale instances without manual intervention</strong><br><br>Auto Scaling (AS) automatically and dynamically adds or removes CVM instances in real time based on the business load, ensuring that you are running the optimal number of instances without manual intervention.</br><br>For example, you can set a scaling policy to add CVM instances to the scaling group when the CPU utilization is high, and the new CVM instances will be charged by the second. Similarly, you can also set a policy to remove instances from the scaling group when the CPU utilization is low. If your load changes are predictable, you can set a scheduled task to plan your scaling activities.</br><br>The new instances can also be directly associated with the existing cloud load balancer (CLB) to share the distributed traffic of the scaling group and to improve service availability. You can also send an alarm to Admin to keep an eye on any exceptions.<br></td>
<td><strong>Cumbersome manual operations are needed</strong><br><br>The resources are subject to manual creation and termination. The CLB needs to be configured manually.<br>Manual operation is error-prone, which may affect the business.<br></td>
</tr>
<tr>
<td><strong>Cost Saving</strong></td>
<td><strong>Appropriate scaling of instances reduces costs</strong> <br><br>AS helps you maintain an optimal number of instances in response to changing business demands. AS launches new CVM instances seamlessly and automatically when demand increases, and terminates unneeded CVM instances automatically when demand decreases. This improves device utilization and reduces the costs of deployment and instances.<br></td>
<td><strong>Idle resources result in waste</strong><br><br>Extra CVMs need to be reserved to ensure the application always has enough capacity to meet demand.<br></td>
</tr>
<tr>
<td><strong>Fault Tolerance</strong></td>
<td><strong>AS automatically monitors the health of instances</strong><br><br>AS detects any unhealthy instance, and automatically replaces it with a new one. This ensures that your application is getting the desired computing capacity so that your business can run normally and smoothly.<br></td>
<td><strong>Unhealthy instances are exposed to delayed processing</strong><br><br>Unhealthy instances are not replaced until the business interruption is discovered, which compromises business availability.<br></td>
</tr>
</tbody></table>


