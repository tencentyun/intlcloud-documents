1. Download and compile the [Tez v0.10.0 source code package](https://downloads.apache.org/tez/0.10.0/). 
```
tar -zxvf  apache-tez-0.10.0-src.tar.gz
chmod -R 777 apache-tez-0.10.0-src
cd  apache-tez-0.10.0-src
mvn -X clean package -DskipTests=true -Dmaven.javadoc.skip=true
```
2. Decompress the compiled WAR package.
3. Configure the `yarn-site.xml` file. 
Create a `mkdir -p /usr/local/service/hadoop/filesystem/yarn/timeline` directory.
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Value</th>
</tr>
</thead>
<tbody><tr>
<td>yarn.timeline-service.enabled</td>
<td>true</td>
</tr>
<tr>
<td>yarn.timeline-service.hostname</td>
<td><code>172.**.**.9</code></td>
</tr>
<tr>
<td>yarn.timeline-service.http-cross-origin.enabled</td>
<td>true</td>
</tr>
<tr>
<td>yarn.resourcemanager.system-metrics-publisher.enabled</td>
<td>true</td>
</tr>
<tr>
<td>yarn.timeline-service.address</td>
<td><code>172.**.**.9:10201</code></td>
</tr>
<tr>
<td>yarn.timeline-service.webapp.address</td>
<td><code>172.**.**.9:8188</code></td>
</tr>
<tr>
<td>yarn.timeline-service.webapp.https.address</td>
<td><code>172.**.**.9:2191</code></td>
</tr>
<tr>
<td>yarn.timeline-service.generic-application-history.enabled</td>
<td>true</td>
</tr>
<tr>
<td>yarn.timeline-service.handler-thread-count</td>
<td>24</td>
</tr>
</tbody></table>
4. Configure the `tez.xml` file.
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Value</th>
</tr>
</thead>
<tbody><tr>
<td>tez.tez-ui.history-url.base</td>
<td><code>http://172.**.**.9:2000/tez-ui/</code></td>
</tr>
<tr>
<td>tez.history.logging.service.class</td>
<td>org.apache.tez.dag.history.logging.ats.ATSHistoryLoggingService</td>
</tr>
</tbody></table>
