---
layout: default
title:  Kubernetes
parent: Giriş
nav_order: 2
---

# Kubernete Nedir?
Kubernetes (k8s) Google tarafından open-source olarak geliştirilen, containerized uygulamalarımızı çalıştırabileceğimiz container orchestration alanında tercih edilen de-facto standart projedir.

## Kubernetes bize neler sağlıyor?


* **Service Discovery & Load Balancing:** Kubernetes bizler için içerisinde çalışan containerlara erişebileceğimiz dns tanımlamaları yapar. Aynı zamanda gelen yükü çalışan uygulamalarımıza dengeli bir şekilde dağıtabilmek için load balancing sorumluluğunu da üstlenir.

* **Depolama Yönetimi:** Data persist etmemiz gereken uygulamalar için dinamik olarak storage mount edebilmemizi sağlar. Bu storage çalıştığımız node üzerinde local storage veya bir cloud provider tarafında kullanabileceğimiz storage olabilir.

* **Otomatize Rollout & Rollback:**  Uygulamanızın kaç instance ile çalışmasını istediğinizi belirtebilirsiniz. Bu sayede kubernetes yeni bir deployment yaptığınız zaman bu süreci sizin için otomatize eder.

* **Resource Management:**
Kubernetes'e her bir konteyner için ne kadar CPU ve bellek (RAM) gerektiğini söylersiniz. Kubernetes, kaynaklarınızdan en iyi şekilde yararlanmak için konteynerlerinizi nodelarınıza göre ayarlar.

* **Healthcheck:**
Uygulamalarınız için healthcheck tanımlamaları yaparak belirttiğiniz kurallara uymayan uygulamaların çalışmamasını veya çalışma zamanında hata alması durumunda uygulamanın restart edilmesi* ni kubernetes bizlere sağlar.

* **Secret & Configuration Yönetimi:** Kubernetes, parolalar, OAuth anahtarları ve SSH anahtarları gibi hassas bilgileri depolamanızı ve yönetmenizi sağlar. Konteyner imajlarınızı yeniden oluşturmadan ve yığın yapılandırmanızdaki gizli bilgileri açığa çıkarmadan yeni gizli bilgileri ve uygulama yapılandırmasını dağıtabilir ve güncelleyebilirsiniz.

* Genel olarak: 
    - Service Discovery
    - Resillience (Cluster and resource level)
    - Load balancing
    - healthchecks
    - cluster authorization
    - resource management
    - autoscaling (horizontal & vertical)
    - Observability (Cluster and resurce level) (prometheus, grafana)
* Service mesh (istio, linkerd)
  - Trafik Management
    - Request Routing
    - Traffic Shifting
    - Mirroring
    - ingress gateway
    - egress gateway
  - Security
    - mTLS, Certicficate Management
    - Authentication
    - Peer Authentication
    - Request Authentication
  - Service Resilliency
    - Timeouts
    - Retries
    - Circuit breaker
    - Error İnjection (Ağ sağlamlığı)
  - Observability (service level)
    -  Metrics
    -  Logs and tracing
 -  Stateful Applications
    -  persistent storage
    -  statefulsets