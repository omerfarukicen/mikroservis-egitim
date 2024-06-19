---
layout: default
title : Pod
parent: Temel Kavramlar
nav_order: 2
has_children: true
---

  

# PODS

Pod, birden fazla konteyneri içeren ve bu konteynerlerin aynı fiziksel veya sanal makinede çalışmasını sağlayan bir kavramdır. Bu konteynerler, birbirleriyle iletişim kurabilirler ve aynı kaynakları paylaşabilirler.
 

## Pod Lifecycle

1. **Creation:** Pod oluşturulmak üzere API sunucusuna gönderilir. Pod, Pending durumuna geçer.Kubernetes Scheduler, Pod'u uygun bir düğüme yerleştirir.
2. **Starting:** Düğüm, Pod'un gereksinim duyduğu konteyner görüntülerini indirir ve konteynerleri başlatır.Init konteynerleri varsa, önce bunlar çalışır. Başarıyla tamamlanmalarının ardından ana uygulama konteynerleri başlatılır.
3. **Running:** Pod, Running durumuna geçer ve belirtilen tüm konteynerler çalışmaya başlar.
Problar (Liveness, Readiness, Startup) sürekli olarak konteynerlerin durumunu izler.
4. **Graceful Termination:** 
Pod sonlandırılmak istendiğinde, Kubernetes nazik sonlandırma sürecini başlatır.
PreStop kancaları çalıştırılır, konteynerlere SIGTERM sinyali gönderilir ve belirli bir süre içinde kapanmaları beklenir.
5. **Completion or Failure:** Pod'un tüm konteynerleri başarılı bir şekilde tamamlanırsa, Pod Succeeded durumuna geçer.Bir veya daha fazla konteyner hata ile sonlanırsa, Pod Failed durumuna geçer.

## Restart Policy
* **Always:** Automatically restarts the container after any termination.
* **OnFailure:** Only restarts the container if it exits with an error (non-zero exit status).
* **Never:** Does not automatically restart the terminated container.

## Check Mechanisms

* **Liveness Probes:** Konteynerin canlı olup olmadığını kontrol eder. Başarısız olduğunda konteyner yeniden başlatılır.
* **Readiness Probes:** Konteynerin trafiği alıp almayacağını belirler. Başarısız olduğunda, Pod yük dengeleyici tarafından trafiğe kapatılır.
* **Startup Probes:** Konteynerin başlatılma durumunu kontrol eder. Başarısız olduğunda konteyner yeniden başlatılır.

**exec:**Executes a specified command inside the container
```
livenessProbe:
  exec:
    command:
    - /bin/sh
    - -c
    - echo hello
  initialDelaySeconds: 5
  periodSeconds: 5
```
**grpc:**Bu mekanizma, gRPC (Remote Procedure Call) kullanarak uzak bir prosedür çağrısı yapar.
'''
  grpc: 
    port: 8080
    service: my-service
'''

**httpGet:**Bu mekanizma, belirli bir port ve yol üzerinde Pod'un IP adresine karşı bir HTTP GET isteği yapar.
'''
  httpGet:
    path: /healthz
    port: 8080
'''
**tcpSocket:**Pod'un IP adresine belirli bir port üzerinden bir TCP bağlantısı yapar.

'''
  tcpSocket:
    port: 8080
'''

## Init Containers
Bir Pod'un ana konteynerlerinden önce çalıştırılan özel konteynerlerdir.Her zaman ana konteynerlerden önce çalışır.Başarılı bir şekilde tamamlanması gerekir; aksi takdirde Pod başlatılmaz.Init container'lar çalışırken Pod "Pending" durumunda kalır ve "Initialized" durumu false olarak ayarlanır.
```
apiVersion: v1
kind: Pod
metadata:
  name: maven-project-pod
spec:
  initContainers:
  - name: init-maven
    image: maven:3.6.3-jdk-8
    command: ['sh', '-c', 'mvn dependency:resolve']
    volumeMounts:
    - name: maven-repo
      mountPath: /root/.m2
  containers:
  - name: maven-app
    image: openjdk:8-jdk-alpine
    command: ['sh', '-c', 'mvn spring-boot:run']
    volumeMounts:
    - name: maven-repo
      mountPath: /root/.m2
  volumes:
  - name: maven-repo
    emptyDir: {}

```

 ## Sidecar Containers
 Sidecar container, Kubernetes’te Pod içindeki ana konteynerlere ek olarak çalışan yardımcı konteynerlerdir. Ana konteynerlerin işlevselliğini artırmak veya desteklemek amacıyla kullanılırlar. Sidecar container'lar, genellikle log toplama, proxy hizmeti, veri önbellekleme, yapılandırma yönetimi gibi görevlerde kullanılır.Sidecar container'lar ve ana konteynerler, Pod içindeki ortak kaynakları (volumes, network namespace gibi) paylaşır.Sidecar container, uygulamanın loglarını toplar ve merkezi bir log yönetim sistemine gönderir. Örn:Istio Kubernetes Cluster’ına deploy edildiğinde mevcut pod'ların içinde, virtual service olarak bir
container daha ayağa kaldırır. Mevcut container'lara gelen ve giden trafik ilk önce bu sidecar envoy proxy container’ı üzerinden geçmeye başlar.
```
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
  - name: myapp-container
    image: myapp:1.0
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log/myapp
  - name: log-collector
    image: log-collector:1.0
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log/myapp
  volumes:
  - name: shared-logs
    emptyDir: {}

```

## Ephemeral Containers
Kubernetes'te geçici veya kısa ömürlü işler için kullanılan özel konteynerlerdir. Bu konteynerler, mevcut Pod'lara eklenebilir ve genellikle hata ayıklama, sorun giderme veya geçici görevler için kullanılır. Pod içindeki container problem ve bu problemi çözemiyoruz.  İçine bir container atıp logları izleyebiliriz.
```
kubectl debug -it my-app-pod --image=busybox --target=my-app-container -- sh

```
Nginx Logları : cat /var/log/nginx/error.log
Environment değişkenleri : printenv


