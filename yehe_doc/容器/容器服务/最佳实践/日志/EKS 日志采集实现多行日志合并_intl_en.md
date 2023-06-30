
## Overview
When the EKS log collection is enabled via environment variables, the log extraction defaults to the single-line extraction mode. If the log data of the client occupies multiple lines (such as the Java program log), the line break `\n` cannot be used to mark the end of a log. To help the CLS to clearly distinguish each log, it is necessary to configure a configmap with the first-line regular expression. When a log in a line matches the preset regular expression, it is considered as the beginning of a log, and the next matching line will be the end mark of the log. This document describes how to merge multi-line logs when you use environment variables to enable EKS log collection.





## Directions
### Raw log sample
```
2020-09-24 16:09:07 ERROR System.out(4844) java.lang.NullPointerException
at com.temp.ttscancel.MainActivity.onCreate(MainActivity.java:43)
at android.app.Activity.performCreate(Activity.java:5248)
at android.app.Instrumentation.callActivityOnCreate(Instrumentation.java:1110) at android.app.ActivityThread.performLaunchActivity(ActivityThread.java:2162) at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:2257)
at android.app.ActivityThread.access$800(ActivityThread.java:139)
at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1210)
```





### Creating Configmap[](id:Configmap)
For the sample raw log file, the content of the parser.conf configuration file is:

```
apiVersion: v1 
data:
    parser.conf: |- 
      [PARSER]
      Name parser_name
      Format regex
      Regex ^(?<timestamp>[0-9]{2,4}\-[0-9]{1,2}\-[0-9]{1,2} [0-9]{1,2}\:[0-9]{1,2}\:[0-9]{1,2}) (?<message>.*) 
kind: ConfigMap
metadata:
    name: cm 
    namespace: default
```

Among them, `parser_name` needs to be set in the annotation (spec.template.metadata.annotations) when the workload is created. Run the following command to set:

```
eks.tke.cloud.tencent.com/parser-name: parser_name
```

For more information about `parser.conf` configuration file, see [Regular Expression](https://docs.fluentbit.io/manual/pipeline/parsers/regular-expression).

### Mounting Configmap when creating a Pod
You need to perform the following operations when creating a Pod:
1. Mount the created [Configmap](#Configmap) as a Volume.
2. For how to enable log collection via environment variables, see [Log Collection](https://intl.cloud.tencent.com/document/product/457/37907).
3. Specify two annotations.
```
eks.tke.cloud.tencent.com/parser-name: "parser_name"
eks.tke.cloud.tencent.com/volume-name-for-parser: "volume-name"
```
 - `eks.tke.cloud.tencent.com/parser-name` refers to the name of the created [Configmap](#Configmap).
 - `eks.tke.cloud.tencent.com/volume-name-for-parser` refers to the name of the Volume mounted in the Pod, which can be customized.

**Pod yaml template**

```
apiVersion: apps/v1 
kind: Deployment 
metadata:
    labels:
      k8s-app: multiline 
      qcloud-app: multiline
    name: multiline
    namespace: default 
spec:
    replicas: 1 
    selector:
      matchLabels:
        k8s-app: multiline
        qcloud-app: multiline 
    template:
      metadata: 
        annotations:
          eks.tke.cloud.tencent.com/parser-name: parser_name
          eks.tke.cloud.tencent.com/volume-name-for-parser: volume-name 
        labels:
          k8s-app: multiline
          qcloud-app: multiline 
      spec:
        containers: 
        - env:
          - name: EKS_LOGS_OUTPUT_TYPE 
            value: cls
          - name: EKS_LOGS_LOG_PATHS 
            value: stdout
          - name: EKS_LOGS_TOPIC_ID 
            value: topic-id
          - name: EKS_LOGS_LOGSET_NAME 
            value: eks
          - name: EKS_LOGS_SECRET_ID 
            valueFrom:
              secretKeyRef: 
                key: SecretId 
                name: cls 
                optional: false
          - name: EKS_LOGS_SECRET_KEY 
            valueFrom:
              secretKeyRef: 
                key: SecretKey 
                name: cls 
                optional: false
          image: nginx 
          imagePullPolicy: Always 
          name: ng
          resources:
            limits:
              cpu: 500m 
              memory: 1Gi
            requests:
              cpu: 250m 
              memory: 256Mi
          volumeMounts:
          - mountPath: /mnt
              name: volume-name 
              imagePullSecrets:
              - name: qcloudregistrykey 
              restartPolicy: Always 
          volumes:
          - configMap:
              defaultMode: 420
              name: cm
            name: volume-name
```




### Structured log sample

```
2020-09-24 16:09:07 ERROR System.out(4844) java.lang.NullPointerException \at com.temp.ttscancel.MainActivity.onCreate(MainActivity.java:43) \at android.app.Activity.performCreate(Activity.java:5248) \at android.app.Instrumentation.callActivityOnCreate(Instrumentation.java:1110) \at android.app.ActivityThread.performLaunchActivity(ActivityThread.java:2162) \at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:2257) \at android.app.ActivityThread.access$800(ActivityThread.java:139) \at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1210)
```
