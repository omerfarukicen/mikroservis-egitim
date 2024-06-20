---
layout: default
title: Job
parent: Temel Kavramlar
nav_order: 6
has_children: true
---

## Tanım
Kubernetes Job, bir veya daha fazla Pod çalıştırarak belirli bir görevi yerine getiren ve ardından sonlanan bir Kubernetes nesnesidir. 

```
apiVersion: batch/v1
kind: Job
metadata:
  name: pi-with-timeout
spec:
  backoffLimit: 5
  activeDeadlineSeconds: 100
  template:
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
```

* Completetions: çalıştığı zaman kaç kere tekrar çalışacak.
* Paralellism: kaç paralel iş aynı zamanda çalışsın. görev dağılımı için başka araçlardan yararlanması gerekir. Aynı işi yapmamayı garanti etmez.
* BackoffLimit: bu kadar kere çalıştırmayı dene ve vzgeç. default 6dır.
* activeDeadlineSeconds: jobın süresi bu zamandan fazla sürmesini engellemek için kullanılır. bu zamanı geçince podlar öldürülür.

## Pod failure policy
Kubernetes'te Job'ların Pod hatalarını daha iyi yönetebilmesi için esnek ve güçlü bir araçtır. Bu politikayı kullanarak, belirli hataları göz ardı edebilir, Job'ları belirli koşullarda başarısız olarak işaretleyebilir ve maliyetleri optimize edebilirsiniz. 
```
  podFailurePolicy:
    rules:
    - action: FailJob
      onExitCodes:
        containerName: main
        operator: In
        values: [42]
    - action: Ignore
      onPodConditions:
      - type: DisruptionTarget
```
action: FailJob: Eğer main konteyneri çıkış kodu 42 ile sonlanırsa, Job başarısız olarak işaretlenir ve tüm çalışan Pod'lar sonlandırılır.
action: Ignore: DisruptionTarget durumuna sahip Pod hataları göz ardı edilir ve yeniden deneme sayısı artırılmaz.

## Job Success Policy
Job Success Policy, Kubernetes'te Job'ların başarı durumlarını daha hassas ve özelleştirilmiş bir şekilde yönetmenizi sağlar. Bu politika, Job'un tamamlanma ve başarılı sayılma şartlarını belirlemenize olanak tanır. 



## Job Paremeter
* activeDeadlineSeconds : Kubernetes Job nesnesinde kullanılan bir alandır ve bir Job'un tamamlanması için izin verilen maksimum süreyi belirler. Bu süre zarfında Job tamamlanmazsa, Job başarısız olarak işaretlenir ve çalışmakta olan tüm Pod'lar sonlandırılır.
* ttlSecondsAfterFinished: Job tamamlandıktan sonra Job ve Pod'ların otomatik olarak silinmesi için geçen süreyi belirler.
* 