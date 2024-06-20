---
layout: default
title : Deployments
parent: Temel Kavramlar
nav_order: 3
---

# Tanım
Deployment, ReplicaSet'in daha üst seviyede yönetimini sağlayan bir Kubernetes nesnesidir. Deployment, Pod'ların ve ReplicaSet'lerin yönetimini kolaylaştırır ve otomatikleştirir. Ayrıca, uygulamaların dağıtım süreçlerini, güncellemelerini ve geri dönüş işlemlerini daha kolay hale getirir.

Özellikler:
* ReplicaSet'leri yönetir ve bu sayede belirli bir sayıda Pod'un çalışmasını sağlar.
* Rolling updates ve rollback (geri dönüş) desteği sunar.
* Uygulamaların yeni sürümlerine geçişi (canary deployment, blue-green deployment) yönetir.
* Güncellemeler sırasında Pod'ların kesintisiz çalışmasını sağlar.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```        
## Commands

* Apply:
```
kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml
```
* Get:
```
kubectl get deployments
```
* Set İmage:
```
kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1
```
* Edit image:
```
kubectl edit deployment/nginx-deployment
```
* Rollout:
History Kubernetes varsayılan değer olarak 10 da tutar
.spec.revisionHistoryLimit değeri ile değiştirilebilir
```
kubectl rollout status deployment/nginx-deployment
```
History:
```
kubectl rollout history deployment/nginx-deployment
```
```
kubectl rollout history deployment/nginx-deployment --revision=2
```
```
kubectl rollout undo deployment/nginx-deployment --to-revision=2
```

* Detay:
```
kubectl describe deployments
```
* Scale
```
kubectl scale deployment/nginx-deployment --replicas=10
```
```
kubectl autoscale deployment/nginx-deployment --min=10 --max=15 --cpu-percent=80
```
* Failed Deployment: Deployment belli şartlarda fail ettirebilirsiniz
```
kubectl patch deployment/nginx-deployment -p '{"spec":{"progressDeadlineSeconds":600}}'
```

## Deployment Strateji
1. Recreate(Yeniden Oluşturma) : Eski podlar tamamen durdurulur ve hizmet kesilir
2. Rolling Update (Yuvarlanan Güncelleme) : Bu strateji, yeni Pod'ları aşamalı olarak başlatır ve eski Pod'ları aşamalı olarak durdurur. Bu yöntem, hizmet kesintilerini en aza indirir.
**maxSurge:** Eğer % 25 olarak ayarlandığında, rollingUpdate başlayınca yeni ReplicaSet hemen sistemi büyütmeye başlar ama eski ve yeni podların toplam sayısı tüm podların % 130'unu geçemez. 

**maxUnavailable:** Güncelleme işlemi sırasında kullanılamayacak duruma gelmesine izin verdiğimiz maksimum pod sayısını belirtir. Sayı da olabilir, istenen pod sayısının yüzdesi de olabilir. Varsayılan %25'tir. 
```
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
```
3. Blue-Green Deployment: Bu strateji, eski ve yeni sürümlerinin tamamen ayrı setler halinde çalıştırılmasıdır. Yeni sürüm tamamen hazır olduğunda trafiği eski sürümden yeni sürüme yönlendirir. Bu yöntem, hızlı geri dönüş (rollback) ve sıfır kesinti sağlar.İki farklı deployment dosyası vardır.Servis üzerinden yenisi ayakta olduğu görüldüğünde geçiş yapılır

4. Canary Deployment: Yeni bir uygulama sürümünün sınırlı sayıda kullanıcıya sunulması, ardından geri bildirim ve performans değerlendirmesi yapıldıktan sonra tam dağıtıma geçilmesi sürecidir. Bu yöntem, yeni sürümün potansiyel hatalarını ve performans sorunlarını erken aşamada tespit etmeye yardımcı olur.

Ingress Tanımından:
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress
  annotations:
    nginx.ingress.kubernetes.io/canary: "true"
    nginx.ingress.kubernetes.io/canary-by-header: "canary"
    nginx.ingress.kubernetes.io/canary-by-header-value: "always"
    nginx.ingress.kubernetes.io/canary-weight: "10"
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginx-service
            port:
              number: 80
```

