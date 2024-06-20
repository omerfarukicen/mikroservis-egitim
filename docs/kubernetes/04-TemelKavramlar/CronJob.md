---
layout: default
title: CronJob
parent: Temel Kavramlar
nav_order: 7
has_children: true
---

## Tanım
CronJob objesi ile de aynı Unix’de olduğu gibi belirli periyotlarda tetiklenecek işler tanımlanabilir. Zamanlanmış job demektir.

```
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox
            imagePullPolicy: IfNotPresent
            args:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure
```


```
kubectl create cronjob test-job image=busybox --schedule="*/2 * * * *" --dry-run -o yaml > cronjob.yaml
```