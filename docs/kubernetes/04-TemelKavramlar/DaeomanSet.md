---
layout: default
title : DaemonSet
parent: Temel Kavramlar
nav_order: 4
---

# Tanım
DaemonSet objesi ile bütün Kubernetes worker'larında bir pod olarak çalışacak uygulama ayağa kaldırılabilir. Buradaki kritik nokta her bir Kubernetes worker'ında sadece bir pod'un çalıştırılmasıdır. ReplicaSet’de böyle bir kıstas yoktur. ReplicaSet’de oluşturulacak pod'lar herhangi bir node’a da schedule edilebilir.

DaemonSet’e örnek vermek gerekirse, Kubernetes Cluster'ımızda çalışan bütün servislerin log'larını toplamak istediğimizi farzedelim. Bunun için EFK (ElasticSearch-Fluentd-Kibana) stack'ini kullanmaya karar verdik. Bu stack'de Fluentd log'ları toplayıp ElasticSearch’e ileten agent rolünü üstlenir. Bütün sistem üzerindeki container'ları dinlemek için fluentd’yi DaemonSet olarak tanımlarız ve bütün kubernetes worker'lar da otomatik olarak ayağa kalkmasını sağlarız. Monitoring gibi durumlar için gerçekten çok kullanışlı bir objedir.

## Kullanım Senaryoları
* Küme İzleme: Her Node'da çalışan izleme ajanları (örneğin, Prometheus Node Exporter) çalıştırmak.
* Log Toplama: Her Node'da çalışan log toplama ajanları (örneğin, Fluentd) çalıştırmak.
* Ağ: Her Node'da çalışan ağ ajanları (örneğin, CNI plugin'leri) çalıştırmak.


* Node Selector:
DaemonSet'in Pod şablonunda bir nodeSelector belirleyerek Pod'ların hangi Node'larda oluşturulacağını sınırlayabilirsiniz.
```
spec:
  template:
    spec:
      nodeSelector:
        disktype: ssd
```


* Taints ve Tolerations:
Node'lara taint uygulanabilir ve Pod'larda karşılık gelen tolerations belirtilerek Pod'ların bu Node'lara yerleştirilmesi sağlanabilir.

```
spec:
  template:
    spec:
      tolerations:
      - key: "example-key"
        operator: "Exists"
        effect: "NoSchedule"
```



```
```