# Thread-və--Virtual-Thread

# 📚 Java Thread və Virtual Thread - Tam İzahat və Interview Hazırlığı

- Hazırlayacağım fayl aşağıdakı bölmələri əhatə edəcək:

  - 📌 Giriş
  - 📌 Thread nədir?
  -  📌 Java Thread API-si və əsas metodları
  - 📌 Thread lifecycle (həyat dövrü)
  - 📌 Thread yaratmaq üsulları
  - 📌 Thread sinxronizasiyası
  - 📌 Deadlock nədir?
  - 📌 ExecutorService nədir?
  - 📌 Virtual Thread nədir?
  - 📌 Virtual Thread vs Platform Thread fərqləri
  - 📌 Virtual Thread istifadəsi
  - 📌 Kod nümunələri
  - 📌 Interview sualları və cavabları
  - 📌 Runnable nədir?
  - 📌 Callable nədir?
  - 📌 Runnable və Callable fərqləri
  - 📌 Future nədir?
  - 📌 ExecutorService ilə Runnable və Callable istifadəsi

---

## 📌 Giriş
Bu sənəd Java-da Thread və Virtual Thread konseptlərini dərindən izah edir, həm nəzəri, həm də praktiki bilik verir və interview suallarını rahatlıqla cavablaya bilməyiniz üçün hazırlanıb.

---

## 📌 Thread nədir?
Thread — bir proses içərisində ayrı icra axınıdır. Java-da hər proqram minimum bir thread ilə işləyir: **main thread**.

---

## 📌 Java Thread API-si və Əsas Metodlar

**Əsas metodlar:**

| Metod                  | Təsviri |
|:---------------------|:----------|
| `start()`               | Thread-i işə salır |
| `run()`                 | Thread-in icra olunacaq kodunu ehtiva edir |
| `sleep(milliseconds)`   | Thread-i müəyyən müddət yuxuya göndərir |
| `join()`                | Bir thread-in bitməsini gözləyir |
| `interrupt()`           | Thread-i dayandırmaq üçün siqnal verir |
| `isAlive()`             | Thread-in aktiv olub olmadığını yoxlayır |

---

## 📌 Thread Lifecycle (Həyat Dövrü)

**Dövrülər:**

1. New
2. Runnable
3. Running
4. Blocked/Waiting
5. Terminated

Şəkil:

- New -> Runnable -> Running -> (Blocked/Waiting) -> Terminated

--- 

## 📌 Thread Yaratma Üsulları

### 1. `Thread` class-ını extend edərək

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running.");
    }
}
```

### 2. Runnable interface-ni implement edərək

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread is running.");
    }
}
```

### 3. Lambda ilə Runnable

```java
Runnable r = () -> System.out.println("Thread is running.");
new Thread(r).start();
```

---

## 📌 Thread Sinxronizasiyası

- Eyni anda birdən çox thread-in eyni resursa müdaxilə etməsinin qarşısını almaq üçün istifadə olunur.

  - Synchronized blok:

```java
synchronized (object) {
    // critical section
}
```

- Synchronized metod:

```java
public synchronized void myMethod() {
    // critical section
}
```

---

## 📌 Deadlock Nədir?

- İki və ya daha çox thread-in bir-birinin resursunu gözləyərək sonsuz gözləmə vəziyyətində qalması.
  - Misal:
 
```java
Thread 1: lock A -> wait B  
Thread 2: lock B -> wait A  
```

---

## 📌 ExecutorService Nədir?

- Thread-lərin idarə olunması üçün yüksək səviyyəli API-dir.
  - Misal:
```java
ExecutorService service = Executors.newFixedThreadPool(10);
service.submit(() -> System.out.println("Task executed"));
service.shutdown();
```

---

## 📌 Virtual Thread Nədir?

- Java 19+ (Preview), Java 21+ (Stable) ilə gələn Virtual Thread-lər yüngül, asinxron və minlərlə thread-in paralel işləməsini təmin edən yeni texnologiyadır.

- Virtual Thread əsas xüsusiyyəti:
  - JVM tərəfindən idarə olunur
  - OS thread-lərinə bağlı deyil
  - Daha yüngül və performanslıdır
 
## 📌 Virtual Thread vs Platform Thread

| Özəllik                 | Platform Thread | Virtual Thread |
| :---------------------- | :-------------- | :------------- |
| OS thread istifadə edir | ✅              | ❌            |
| Yüksək resurs sərfi     | ✅              | ❌            |
| Minlərlə paralel thread | ❌              | ✅            |
| Performans              | Orta            | Yüksək         |
| İstifadə asanlığı       | Orta            | Çox asan       |


---

## 📌 Virtual Thread İstifadəsi

- Java 21

```java
Thread.startVirtualThread(() -> {
    System.out.println("Hello from virtual thread!");
});
```

- ExecutorService ilə

```java
ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor();
executor.submit(() -> System.out.println("Task in virtual thread"));
executor.shutdown();
```

---

## 📌 Kod Nümunələri

### 1. Virtual Thread-lə 1000 task

```java
ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor();
for (int i = 0; i < 1000; i++) {
    int finalI = i;
    executor.submit(() -> System.out.println("Task " + finalI));
}
executor.shutdown();
```

### 2. Platform Thread vs Virtual Thread Performansı

```java
long start = System.currentTimeMillis();

for (int i = 0; i < 1000; i++) {
    Thread.startVirtualThread(() -> {
        try { Thread.sleep(1000); } catch (InterruptedException e) {}
    });
}

long end = System.currentTimeMillis();
System.out.println("Time taken: " + (end - start));
```

## 📚 Java Thread, Runnable, Callable və Virtual Thread - Tam İzahat və Interview Hazırlığı

### 📌 Giriş
Bu sənəd Java-da `Thread`, `Runnable`, `Callable`, `Virtual Thread` anlayışlarını, sinxronizasiyanı, ExecutorService istifadəsini, fərqlərini və interview suallarını əhatə edir.

---

### 📌 Thread nədir?
Thread — bir proses içində müstəqil icra axınıdır. Java-da hər proqram minimum **main thread**-dən ibarətdir.

---

### 📌 Runnable nədir?

`Runnable` — Java-da multithreading üçün istifadə olunan **functional interfeys**-dir. Tək metodlu interfeysdir və `run()` metoduna malikdir.

**Functional Interface:**
```java
@FunctionalInterface
public interface Runnable {
    void run();
}
```
- ➡️ Runnable xüsusiyyətləri:
  - Geri dönüş dəyəri yoxdur.
  - Exception ata bilməz.
  - Thread class-ı ilə istifadə olunur.

Misal:
```java
Runnable task = () -> System.out.println("Runnable task");
new Thread(task).start();
```

### 📌 Callable nədir?

- Callable — Java-da multithreading üçün istifadə olunan interfeysdir. Runnable-dan fərqli olaraq:
  - geri dönüş dəyəri var.
  - exception ata bilir.

- Functional Interface:
```java
@FunctionalInterface
public interface Callable<V> {
    V call() throws Exception;
}
```
- ➡️ Callable xüsusiyyətləri:
  - call() metodunu implement edir.
  - İcra zamanı nəticə qaytarır.
  - Exception ata bilər.

Misal:
```java
Callable<Integer> task = () -> 5 + 10;
Integer result = task.call();
```

| Özəllik              | Runnable                                 | Callable                 |
| :------------------- | :--------------------------------------- | :----------------------- |
| Metod                | `run()`                                  | `call()`                 |
| Geri dönüş           | Yox                                      | Var                      |
| Exception ata bilir  | Yox                                      | Bəli                     |
| Thread ilə istifadə  | `Thread` class-ı və ya `ExecutorService` | Yalnız `ExecutorService` |
| Functional Interface | Bəli                                     | Bəli                     |


## 📌 Future nədir?
- Future — Callable task-lərinin nəticəsini gələcəkdə əldə etmək üçün istifadə olunur.
- Metodlar:
  - `get()` — nəticəni qaytarır, hazır deyilsə gözləyir.
  - `isDone()` — task tamamlanıbsa true qaytarır.
  - `cancel()` — task-i dayandırır.

Misal:
```java
ExecutorService service = Executors.newSingleThreadExecutor();
Future<Integer> future = service.submit(() -> 10 + 20);
Integer result = future.get();
service.shutdown();
```

---

## 📌 ExecutorService ilə Runnable və Callable İstifadəsi

- Runnable task-ləri submit etmək:
```java
ExecutorService service = Executors.newFixedThreadPool(2);
service.submit(() -> System.out.println("Runnable task"));
service.shutdown();
```

- Callable task-ləri submit etmək:

```java
ExecutorService service = Executors.newFixedThreadPool(2);
Future<Integer> future = service.submit(() -> 100 + 200);
Integer result = future.get();
service.shutdown();
```

---

## 📌 Virtual Thread-lə Callable

- Java 21

```java
ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor();
Future<String> future = executor.submit(() -> {
    Thread.sleep(1000);
    return "Done!";
});
System.out.println(future.get());
executor.shutdown();
```
---

## 📚 Parallel Stream nədir?

Java 8 ilə gələn Stream API içində parallelStream() metodu, kolleksiya elementləri üzərində paralel işləmə (multithreading) imkanı verir.
Normal stream() metodu elementləri sıralı (sequential) şəkildə icra edir.
Amma parallelStream() bu task-ləri ForkJoinPool.commonPool() üzərində bir neçə thread ilə paralel icra edir.

### 📌 İş prinsipi
- Java Stream API, Spliterator istifadə edərək kolleksiyanı hissələrə bölür.
- Hər hissə ForkJoinPool içində fərqli thread-lərdə işlənir.
- Nəticədə daha sürətli emal mümkündür (xüsusilə böyük datalar üçün).

### 📌 İstifadə Qaydası

- Sequential Stream:
```java
list.stream()
    .forEach(System.out::println);
```

- Parallel Stream:
```java
list.parallelStream()
    .forEach(System.out::println);
```

### 📌 Üstünlükləri
- ✅ Böyük dataset-lərdə daha sürətli nəticə.
- ✅ Thread management etməyə ehtiyac yoxdur, Java özü idarə edir.
- ✅ Kod daha oxunaqlı və funksional olur.

### 📌 Risk və Dezavantajlar
- ❌ Thread-safe olmayan obyektlərdə risklidir. (Concurrent modification exception və ya səhv nəticə ala bilərsən.)
- ❌ Hər zaman sequential stream-dən sürətli olmur. (Küçük dataset-lərdə overhead daha çox ola bilər.)
- ❌ Nəticələrin order-i zəmanətli deyil. (Əgər .forEachOrdered() istifadə etməsən)

### 📌 Nümunə Kodlar
- Sequential Stream:

```java
List<String> names = Arrays.asList("Elvin", "Aysel", "Kamran", "Leyla");

names.stream()
     .forEach(System.out::println);
```

- Parallel Stream:

```java
names.parallelStream()
     .forEach(System.out::println);
```

- Parallel Stream + Map + Collect

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

List<Integer> result = numbers.parallelStream()
    .map(n -> n * n)
    .collect(Collectors.toList());

System.out.println(result);
```

- Parallel Stream ilə Ordered Nəticə

```java
names.parallelStream()
     .forEachOrdered(System.out::println);
```

### 📌 ParallelStream harada istifadə etməliyik?
- ✅ Böyük və asinxron işlənməsi mümkün olan kolleksiyalarda.
- ✅ Heavy computational əməliyyatlarda.
- ✅ Thread-safe obyektlərlə işləyərkən.
Yoxsa:
- ❌ Kiçik dataset-lərdə
- ❌ I/O-bound əməliyyatlarda
- ❌ Mutable state-lərlə (və ya shared mutable data-larla) istifadə etmək risklidir.

---

## 📌 Interview Sualları və Cavabları

###🔹 1. Thread və Process fərqi nədir?
- Process: Müstəqil icra mühiti.
- Thread: Process daxilində ayrı icra axını.


### 🔹 2. Java-da Thread necə yaradılır?
- Thread class-ını extend edərək
- Runnable implement edərək
- Lambda ilə


### 🔹 3. Synchronized metod nə üçündür?
- Bir anda yalnız bir thread-in metodu icra etməsi üçün.

### 🔹 4. Deadlock nədir və necə qarşısını almaq olar?
- İki thread-in bir-birinin resursunu gözləyib sonsuz gözləmə vəziyyətində qalmasıdır.
- Çarə: Resurslara eyni ardıcıllıqla kilid qoymaq.

### 🔹 5. ExecutorService nə işə yarayır?
- Thread-lərin idarəsini asanlaşdırır, thread pool yaradır.

### 🔹 6. Virtual Thread nədir və üstünlüyü?
- Yüngül, OS thread-lərindən asılı olmayan thread-lərdir. Minlərlə paralel thread-i performans itirmədən işlədə bilir.

### 🔹 7. Virtual Thread necə yaradılır?
- Thread.startVirtualThread(Runnable)
- Executors.newVirtualThreadPerTaskExecutor()

### 🔹 8. Platform Thread və Virtual Thread fərqləri?
- Platform Thread OS tərəfindən idarə olunur, Virtual Thread isə JVM tərəfindən.
- Virtual Thread daha yüngüldür.

### 🔹 9. Runnable və Callable fərqi nədir?
- Runnable nəticə qaytarmır, exception atmır.
- Callable nəticə qaytarır, exception ata bilir.

### 🔹 10. ExecutorService nə işə yarayır?
- Thread-ləri idarə edən yüksək səviyyəli API-dir. Thread pool yaradır və task-ləri icra edir.

### 🔹 11. Future nədir və nə işə yarayır?
- Callable task-lərinin nəticəsini gələcəkdə əldə etmək və task-ləri idarə etmək üçün istifadə olunur.

### 🔹 12. Virtual Thread nədir?
- Java 19+ ilə gələn, yüngül, OS thread-lərindən asılı olmayan yeni thread növü.

### 🔹 13. Runnable neçə üsulla istifadə olunur?
- Lambda expression ilə
- Runnable implement edərək class yaratmaqla
- Anonymous inner class ilə

### 🔹 14. Callable neçə üsulla istifadə olunur?
- Lambda expression ilə
- Callable implement edərək class yaratmaqla
- Anonymous inner class ilə

### 🔹 15 ParallelStream və Stream fərqi nədir?
- stream() sequential işləyir.
- parallelStream() bir neçə thread-də eyni anda işləyir.

### 🔹 16 ParallelStream hansı thread pool-u istifadə edir?
- ForkJoinPool.commonPool()

### 🔹 17 ParallelStream-də sıra qorunurmu?
- Xeyr, forEach-də sıra zəmanətli deyil.
- Amma forEachOrdered istifadə etsən qorunur.

### 🔹 18 Hər zaman ParallelStream sürətli olurmu?
- Xeyr. Böyük dataset-lər üçün sürətlidir, amma kiçik datalarda overhead ucbatından sequential daha performanslı ola bilər.

### 🔹 19 Thread-safe olmayan obyektlərlə işləmək olarmı?
- Olmaz. Concurrent modification və ya səhv nəticə ola bilər.

---
