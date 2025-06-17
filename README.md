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

---

------


# Java-da Thread-lər

Java-da **Thread** çoxlu tapşırıqların (multitasking) eyni anda icra olunmasını təmin edən əsas mexanizmdir. Java-da hər bir proqram ən azı bir thread ilə işləyir ki, bu da əsas thread (main thread) adlanır. Thread-lər `java.lang.Thread` sinfi və ya `java.lang.Runnable` interfeysi vasitəsilə yaradılır.

## Thread Sinfinin Əsas Metodları və Funksiyaları

1. **start()**
   - **Nə edir?** Thread-i işə salır. Bu metod çağırıldıqda, thread-in `run()` metodu icra olunmağa başlayır.
   - **Nümunə:** 
     ```java
     Thread thread = new Thread(() -> System.out.println("Thread işləyir"));
     thread.start();
     ```
   - **Vacib qeyd:** `start()` metodu bir thread-i yalnız bir dəfə çağırıla bilər. Əgər eyni thread üzərində təkrar `start()` çağırılsa, `IllegalThreadStateException` xətası atılır.

2. **run()**
   - **Nə edir?** Thread-in icra olunacaq kodunu müəyyənləşdirir. Əgər `Runnable` interfeysi istifadə olunursa, bu metodun içindəki kod icra olunur.
   - **Nümunə:**
     ```java
     public class MyThread extends Thread {
         public void run() {
             System.out.println("Thread icra olunur");
         }
     }
     ```

3. **sleep(long millis)**
   - **Nə edir?** Thread-i göstərilən müddət (millisaniyə ilə) dayandırır (pause). Bu, digər thread-lərə CPU vaxtı vermək üçün istifadə olunur.
   - **Nümunə:**
     ```java
     Thread.sleep(1000); // 1 saniyə gözləyir
     ```
   - **Qeyd:** `InterruptedException` atma ehtimalı var, buna görə try-catch bloku ilə idarə olunmalıdır.

4. **join()**
   - **Nə edir?** Bir thread-in tamamlanmasını gözləyir. Məsələn, əsas thread digər thread-in bitməsini gözləyə bilər.
   - **Nümunə:**
     ```java
     Thread t1 = new Thread(() -> System.out.println("T1 işləyir"));
     t1.start();
     t1.join(); // T1 bitənə qədər gözləyir
     ```

5. **interrupt()**
   - **Nə edir?** Thread-i kəsir. Əgər thread `sleep()` və ya `wait()` kimi metodlarda gözləyirsə, `InterruptedException` atılır.
   - **Nümunə:**
     ```java
     Thread t = new Thread(() -> {
         try {
             Thread.sleep(5000);
         } catch (InterruptedException e) {
             System.out.println("Thread kəsildi!");
         }
     });
     t.start();
     t.interrupt();
     ```

6. **setPriority(int priority)**
   - **Nə edir?** Thread-in prioritetini təyin edir (1-dən 10-a qədər). Daha yüksək prioritetli thread-lərə CPU daha çox vaxt ayırır.
   - **Nümunə:**
     ```java
     thread.setPriority(Thread.MAX_PRIORITY); // 10
     ```

7. **getName() / setName(String name)**
   - **Nə edir?** Thread-in adını alır və ya dəyişdirir.
   - **Nümunə:**
     ```java
     thread.setName("MyThread");
     System.out.println(thread.getName()); // "MyThread"
     ```

8. **isAlive()**
   - **Nə edir?** Thread-in aktiv olub-olmadığını yoxlayır.
   - **Nümunə:**
     ```java
     System.out.println(thread.isAlive()); // true və ya false
     ```

## Thread-lərlə İşləməyin Əsas Yollar
1. **Thread sinfini genişləndirmək (extends Thread):**
   ```java
   public class MyThread extends Thread {
       public void run() {
           System.out.println("Thread işləyir");
       }
   }
   MyThread t = new MyThread();
   t.start();
   ```
2. **Runnable interfeysini implement etmək:**
   ```java
   public class MyRunnable implements Runnable {
       public void run() {
           System.out.println("Runnable işləyir");
       }
   }
   Thread t = new Thread(new MyRunnable());
   t.start();
   ```

## Thread-lərlə bağlı Müsahibə Sualları və Cavabları

1. **Thread nədir və Java-da necə yaradılır?**
   - **Cavab:** Thread Java-da çoxlu tapşırıqların eyni anda icra olunmasını təmin edən bir mexanizmdir. Thread-lər `java.lang.Thread` sinfini genişləndirməklə və ya `Runnable` interfeysini implement etməklə yaradılır. `start()` metodu ilə thread işə salınır, bu zaman `run()` metodu icra olunur. Məsələn:
     ```java
     Thread t = new Thread(() -> System.out.println("Thread işləyir"));
     t.start();
     ```

2. **Thread ilə Runnable arasındakı fərq nədir?**
   - **Cavab:** `Thread` bir sinfdir və birbaşa thread-i təmsil edir, `Runnable` isə bir interfeysdir və yalnız `run()` metodunu təmin edir. `Thread` sinfini genişləndirərək thread yaradıla bilər, lakin bu, sinifin miras alınmasını məhdudlaşdırır. `Runnable` isə daha çevikdir, çünki başqa sinfi genişləndirmək mümkün olur. `Runnable` istifadəsi daha çox tövsiyə olunur, çünki obyekt-orientasiya prinsipinə uyğundur.

3. **Thread-in həyat dövrü (lifecycle) haqqında danışın.**
   - **Cavab:** Thread-in həyat dövrü aşağıdakı mərhələlərdən ibarətdir:
     - **New:** Thread yaradılıb, amma hələ `start()` çağırılmayıb.
     - **Runnable:** `start()` çağırıldıqdan sonra thread icra olunmağa hazırdır.
     - **Running:** `run()` metodu icra olunur.
     - **Blocked/Waiting:** Thread `wait()`, `sleep()` və ya başqa səbəbdən gözləyir.
     - **Terminated:** Thread işini bitirib və ya kəsilib.

4. **Thread.sleep() və Thread.yield() metodları arasındakı fərq nədir?**
   - **Cavab:** `Thread.sleep()` thread-i müəyyən müddətə dayandırır və CPU-ya digər thread-lərə vaxt ayırmağa imkan verir. `Thread.yield()` isə cari thread-in icrasını müvəqqəti olaraq dayandırır və eyni və ya daha yüksək prioritetli thread-lərə CPU vaxtı verir. `sleep()` müəyyən vaxt gözləyir, `yield()` isə sadəcə növbəni buraxır.

5. **Thread-lərdə sinxronizasiya nədir və niyə vacibdir?**
   - **Cavab:** Sinxronizasiya thread-lərin paylaşılan resurslara eyni anda daxil olmasının qarşısını alır və məlumat tutarlılığını təmin edir. `synchronized` açar sözü ilə metodlar və ya kod blokları sinxronlaşdırılır. Məsələn:
     ```java
     synchronized void increment() {
         counter++;
     }
     ```
     Sinxronizasiya olmadan, birdən çox thread eyni resursu dəyişdirsə, data race vəziyyəti yarana bilər.

# Java-da Virtual Thread-lər

Java 19-da təqdim olunan **Virtual Thread-lər** (Project Loom çərçivəsində) yüksək miqyaslı, asinxron və yüngül çoxlu tapşırıqları dəstəkləmək üçün nəzərdə tutulmuşdur. Virtual thread-lər platform thread-lərindən (ənənəvi Java thread-ləri) fərqli olaraq JVM tərəfindən idarə olunan yüngül thread-lərdir. Onlar OS (əməliyyat sistemi) thread-lərinə bağlı deyil və minlərlə virtual thread-i eyni anda idarə etmək mümkündür.

## Virtual Thread-lərin Əsas Xüsusiyyətləri

1. **Yüngül və Miqyaslı:** Virtual thread-lər az yaddaş istifadə edir və milyonlarla virtual thread-i idarə etmək mümkündür.
2. **Bloklama Əməliyyatları:** Virtual thread-lər bloklama əməliyyatlarını (məsələn, I/O) avtomatik olaraq asinxron şəkildə idarə edir.
3. **Sadə API:** Virtual thread-lər `Thread` sinfi ilə eyni API-dən istifadə edir, lakin onların idarə olunması JVM tərəfindən optimallaşdırılır.

## Virtual Thread-lərin Yaradılması

Virtual thread-lər `Thread.ofVirtual()` metodu ilə yaradılır:
```java
Thread virtualThread = Thread.ofVirtual().start(() -> {
    System.out.println("Virtual thread işləyir");
});
```

Və ya `ExecutorService` ilə:
```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    executor.submit(() -> System.out.println("Virtual thread işləyir"));
}
```

## Virtual Thread-lərin Əsas Metodları

Virtual thread-lər `Thread` sinfindəki bütün metodları dəstəkləyir (`start()`, `join()`, `interrupt()` və s.), lakin onların daxili işləmə mexanizmi fərqlidir. Məsələn:
- **start():** Virtual thread-i işə salır, lakin bu, JVM-in daxili planlaşdırıcısı (scheduler) tərəfindən idarə olunur.
- **join():** Virtual thread-in tamamlanmasını gözləyir.
- **interrupt():** Virtual thread-i kəsir, lakin bu, platform thread-lərindən fərqli olaraq daha yüngül şəkildə idarə olunur.

## Virtual Thread-lərlə bağlı Müsahibə Sualları və Cavabları

1. **Virtual Thread nədir və nə üçün istifadə olunur?**
   - **Cavab:** Virtual thread-lər Java 19-da təqdim olunmuş yüngül thread-lərdir ki, bunlar JVM tərəfindən idarə olunur və OS thread-lərinə bağlı deyil. Onlar yüksək miqyaslı tətbiqlər üçün nəzərdə tutulub, çünki az yaddaş istifadə edir və milyonlarla thread-i idarə etmək mümkündür. Virtual thread-lər xüsusilə I/O-intensiv tapşırıqlar üçün effektivdir, çünki bloklama əməliyyatları avtomatik olaraq asinxron şəkildə idarə olunur.

2. **Virtual Thread-lər necə yaradılır?**
   - **Cavab:** Virtual thread-lər `Thread.ofVirtual()` metodu və ya `Executors.newVirtualThreadPerTaskExecutor()` ilə yaradılır. Məsələn:
     ```java
     Thread vThread = Thread.ofVirtual().start(() -> System.out.println("Virtual thread"));
     ```
     Və ya:
     ```java
     try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
         executor.submit(() -> System.out.println("Virtual thread"));
     }
     ```

3. **Virtual Thread-lərin üstünlükləri nələrdir?**
   - **Cavab:** Virtual thread-lər aşağıdakı üstünlüklərə malikdir:
     - **Yüngül:** Az yaddaş istifadə edir, buna görə minlərlə thread-i idarə etmək mümkündür.
     - **Miqyaslılıq:** Yüksək paralel tapşırıqları dəstəkləyir.
     - **Asan istifadə:** Mövcud `Thread` API-sindən istifadə edir.
     - **Bloklama optimizasiyası:** I/O əməliyyatları zamanı thread-lər avtomatik olaraq dayandırılır və bərpa olunur.

4. **Virtual Thread-lər hansı ssenarilərdə istifadə olunur?**
   - **Cavab:** Virtual thread-lər xüsusilə I/O-intensiv tətbiqlərdə (məsələn, veb serverlər, verilənlər bazası ilə iş, fayl əməliyyatları) effektivdir. Onlar hər bir istifadəçi sorğusu üçün ayrı thread tələb edən tətbiqlərdə (məsələn, REST API-lər) performansını artırır.

5. **Virtual Thread-lərin məhdudiyyətləri nələrdir?**
   - **Cavab:** Virtual thread-lər CPU-intensiv tapşırıqlarda platform thread-ləri qədər effektiv olmaya bilər, çünki onların planlaşdırılması JVM tərəfindən idarə olunur. Həmçinin, bəzi köhnə kitabxanalar və ya sinxron API-lər virtual thread-lərlə tam uyğun olmaya bilər.

# Thread və Virtual Thread Arasındakı Fərqlər

| **Xüsusiyyət**                | **Thread (Platform Thread)**                             | **Virtual Thread**                                      |
|-------------------------------|----------------------------------------------------------|---------------------------------------------------------|
| **Yaradılma**                 | `new Thread()` və ya `Runnable` ilə yaradılır            | `Thread.ofVirtual()` və ya `ExecutorService` ilə        |
| **Resurs İstifadəsi**         | Hər thread OS thread-inə bağlıdır, çox yaddaş tələb edir | Yüngüldür, az yaddaş istifadə edir                      |
| **Miqyaslılıq**               | Minlərlə thread-i idarə etmək çətindir                   | Milyonlarla thread-i idarə etmək mümkündür              |
| **Bloklama Əməliyyatları**    | Bloklama zamanı OS thread-i gözləyir                     | JVM avtomatik olaraq thread-i dayandırır/bərpa edir     |
| **Performans**                | CPU-intensiv tapşırıqlarda daha yaxşıdır                 | I/O-intensiv tapşırıqlarda daha yaxşıdır                |
| **API**                       | `Thread` sinfi və metodları                              | Eyni `Thread` API-si, lakin JVM tərəfindən idarə olunur |

## Thread və Virtual Thread-lərlə bağlı Müsahibə Sualları və Cavabları

1. **Platform Thread-ləri ilə Virtual Thread-lər arasındakı əsas fərqlər nələrdir?**
   - **Cavab:** Platform thread-ləri birbaşa OS thread-lərinə bağlıdır və hər biri çox yaddaş tələb edir, buna görə miqyaslılıq məhduddur. Virtual thread-lər isə JVM tərəfindən idarə olunan yüngül thread-lərdir, az yaddaş tələb edir və milyonlarla thread-i idarə etmək mümkündür. Virtual thread-lər I/O-intensiv tapşırıqlarda daha effektivdir, çünki bloklama əməliyyatları avtomatik olaraq optimallaşdırılır.

2. **Hansı ssenarilərdə Virtual Thread-lərdən istifadə etmək daha məqsədəuyğundur?**
   - **Cavab:** Virtual thread-lər I/O-intensiv tətbiqlərdə, məsələn, veb serverlərdə, verilənlər bazası sorğularında və ya çoxsaylı istifadəçi sorğularını idarə edən sistemlərdə daha məqsədəuyğundur. Platform thread-ləri isə CPU-intensiv tapşırıqlarda (məsələn, hesablamalar) daha yaxşı performans göstərir.

3. **Virtual Thread-lərin platform thread-lərindən üstünlüyü nədir?**
   - **Cavab:** Virtual thread-lər az yaddaş istifadə edir, yüksək miqyaslılıq təmin edir və I/O əməliyyatlarını avtomatik optimallaşdırır. Bu, xüsusilə çoxsaylı istifadəçi sorğularını idarə edən tətbiqlərdə performans artımı sağlar.

4. **Virtual Thread-lərin platform thread-lərindən hansı məhdudiyyətləri var?**
   - **Cavab:** Virtual thread-lər CPU-intensiv tapşırıqlarda platform thread-ləri qədər effektiv olmaya bilər. Həmçinin, köhnə sinxron API-lər və ya kitabxanalar virtual thread-lərlə tam uyğun olmaya bilər, çünki onların planlaşdırılması JVM-ə bağlıdır.
  

---
---
---
---
---
---
---
---
---

# Java-da Thread, Multithreading və Virtual Thread-lər: Dərin Bələdçi

Bu sənəd Java-da **thread**, **multithreading** və **virtual thread** anlayışlarını dərindən izah edir. Hər bir termin, mexanizm, problem və həll yolu detallı şəkildə təsvir olunur. Həmçinin, praktiki nümunələr, intervyu sualları və real-world tətbiqləri əhatə edilir.

## 1. Thread Nədir?

**Thread** (iş parçası) bir proqramın icra olunan ən kiçik vahididir. Java-da hər proqram ən azı bir thread ilə işləyir (adətən `main` thread). Thread-lər eyni proses daxilində paralel olaraq icra oluna bilər və resursları (yaddaş, fayl deskriptorları və s.) paylaşır.

### Thread-in Xüsusiyyətləri
- **Özəl Stack Yaddaşı**: Hər thread-in öz stack yaddaşı var ki, burada local dəyişənlər və metod çağırışları saxlanılır.
- **Paylaşılan Heap**: Thread-lər eyni prosesin heap yaddaşını paylaşır, bu da obyektlərin və statik dəyişənlərin hamı üçün əlçatan olması deməkdir.
- **Paralel İcra**: Çoxnüvəli CPU-larda thread-lər fərqli nüvələrdə işləyərək performansı artırır.

### Java-da Thread Yaradılması
Java-da thread yaratmağın iki əsas yolu var:
1. **Thread Siniini Miras Almaq**:
   ```java
   class MyThread extends Thread {
       @Override
       public void run() {
           System.out.println("Thread işləyir: " + Thread.currentThread().getName());
       }
   }
   public class Main {
       public static void main(String[] args) {
           MyThread thread = new MyThread();
           thread.start();
       }
   }
   ```
2. **Runnable İnterfeysini İmplement Etmək**:
   ```java
   class MyRunnable implements Runnable {
       @Override
       public void run() {
           System.out.println("Runnable işləyir: " + Thread.currentThread().getName());
       }
   }
   public class Main {
       public static void main(String[] args) {
           Thread thread = new Thread(new MyRunnable());
           thread.start();
       }
   }
   ```

### `start()` vs `run()`
- **`start()`**: Yeni bir thread yaradır və `run()` metodunu icra edir. JVM tərəfindən idarə olunur.
- **`run()`**: Sadəcə metodun icrasını cari thread-də yerinə yetirir, yeni thread yaratmır.

### Thread-in Həyat Dövrü
Java-da thread-in 6 vəziyyəti var:
1. **NEW**: Thread yaradılıb, amma `start()` çağırılmayıb.
2. **RUNNABLE**: Thread icra olunur və ya icra üçün hazırdır.
3. **BLOCKED**: Thread kilid gözləyir (məsələn, `synchronized` bloku).
4. **WAITING**: Thread `wait()`, `join()` və ya `LockSupport.park()` ilə gözləyir.
5. **TIMED_WAITING**: `Thread.sleep()`, `wait(timeout)` və ya `join(timeout)` ilə müəyyən müddət gözləyir.
6. **TERMINATED**: Thread icrasını bitirib.

**Diaqram**:
```
NEW → RUNNABLE ↔ BLOCKED/WAITING/TIMED_WAITING → TERMINATED
```

## 2. Multithreading Nədir?

**Multithreading** bir proses daxilində birdən çox thread-in eyni anda (və ya görünüşdə eyni anda) icra olunmasıdır. Java-da multithreading performansı artırmaq, resurslardan səmərəli istifadə etmək və tətbiqləri daha responsiv etmək üçün istifadə olunur.

### Multithreading-in Üstünlükləri
- **Paralel İcra**: Çoxnüvəli CPU-larda tapşırıqlar bölüşdürülərək daha sürətli icra olunur.
- **Resurs Paylaşımı**: Thread-lər eyni yaddaşı paylaşır, bu da yaddaş səmərəliliyini artırır.
- **Responsivlik**: UI tətbiqlərində (məsələn, JavaFX) uzunmüddətli əməliyyatlar ayrı thread-lərdə icra olunaraq interfeysin donmasının qarşısı alınır.
- **Modulyarlıq**: Tapşırıqlar müstəqil thread-lərə bölünərək kodun idarə olunması asanlaşır.

### Multithreading-in Çətinlikləri
1. **Race Condition**: Bir neçə thread eyni resursa eyni anda daxil olduqda gözlənilməz nəticələr yaranır.
2. **Deadlock**: Thread-lər bir-birini gözləyərək kilidlənə bilər.
3. **Starvation**: Bəzi thread-lər resurslara çata bilməyərək icra olunmur.
4. **Thread Interference**: Thread-lər eyni dəyişəni dəyişdirərkən məlumatın korlanması.
5. **Performans Xərcləri**: Çoxlu thread-lərin idarə edilməsi (context switching) CPU resurslarını istehlak edir.

### Race Condition
**Tərif**: Bir neçə thread-in eyni resursa nəzarətsiz daxil olması nəticəsində məlumatın korlanması.
**Nümunə**:
```java
class Counter {
    private int count = 0;
    public void increment() {
        count++; // Oxu, artır, yaz - atomik deyil
    }
}
```
Bu kodda iki thread eyni anda `count`-u dəyişdirərsə, nəticə yanlış ola bilər.

**Qarşısının Alınması**:
1. **synchronized**:
   ```java
   public synchronized void increment() {
       count++;
   }
   ```
2. **ReentrantLock**:
   ```java
   import java.util.concurrent.locks.ReentrantLock;
   class Counter {
       private final ReentrantLock lock = new ReentrantLock();
       private int count = 0;
       public void increment() {
           lock.lock();
           try {
               count++;
           } finally {
               lock.unlock();
           }
       }
   }
   ```
3. **AtomicInteger**:
   ```java
   import java.util.concurrent.atomic.AtomicInteger;
   class Counter {
       private AtomicInteger count = new AtomicInteger(0);
       public void increment() {
           count.incrementAndGet();
       }
   }
   ```

### Deadlock
**Tərif**: İki və ya daha çox thread-in bir-birini gözləməsi nəticəsində kilidlənməsi.
**Nümunə**:
```java
public class DeadlockExample {
    public static void main(String[] args) {
        String resource1 = "Resurs 1";
        String resource2 = "Resurs 2";
        Thread t1 = new Thread(() -> {
            synchronized (resource1) {
                System.out.println("T1: Resurs 1 kilidləndi");
                try { Thread.sleep(100); } catch (Exception e) {}
                synchronized (resource2) {
                    System.out.println("T1: Resurs 2 kilidləndi");
                }
            }
        });
        Thread t2 = new Thread(() -> {
            synchronized (resource2) {
                System.out.println("T2: Resurs 2 kilidləndi");
                try { Thread.sleep(100); } catch (Exception e) {}
                synchronized (resource1) {
                    System.out.println("T2: Resurs 1 kilidləndi");
                }
            }
        });
        t1.start();
        t2.start();
    }
}
```

**Qarşısının Alınması**:
1. **Resurs Sıralaması**: Resurslara həmişə eyni ardıcıllıqla daxil olun.
2. **Timeout**: `ReentrantLock` ilə `tryLock(timeout)` istifadə edin.
3. **Aşkarlama**: JConsole, VisualVM və ya `ThreadMXBean` ilə deadlock-ları monitor edin.

### Thread Sinxronizasiya Mexanizmləri
1. **synchronized**:
   - Obyektə və ya sinfə kilid qoyur.
   - Sadədir, lakin çevik deyil.
2. **ReentrantLock**:
   - Daha çevikdir: `tryLock()`, `lockInterruptibly()`, `Condition` dəstəyi.
   - Ədalətli kilidləmə (fairness) təmin edə bilər.
3. **Condition**:
   - `ReentrantLock` ilə işləyir, şərtə bağlı gözləmə və oyanma təmin edir.
   ```java
   Condition condition = lock.newCondition();
   condition.await(); // Gözlə
   condition.signal(); // Oyat
   ```
4. **Semaphore**:
   - Resurslara girişi məhdudlaşdırır.
   ```java
   import java.util.concurrent.Semaphore;
   Semaphore semaphore = new Semaphore(10);
   semaphore.acquire();
   semaphore.release();
   ```
5. **Atomic Dəyişənlər**:
   - `AtomicInteger`, `AtomicReference` kimi siniflər lock olmadan atomik əməliyyatlar təmin edir.
6. **ExecutorService**:
   - Thread hovuzlarını idarə edir.
   ```java
   import java.util.concurrent.ExecutorService;
   import java.util.concurrent.Executors;
   ExecutorService executor = Executors.newFixedThreadPool(4);
   executor.submit(() -> System.out.println("Task icra olunur"));
   executor.shutdown();
   ```

## 3. Virtual Thread-lər (Project Loom)

Java 19-da təqdim olunan **virtual thread-lər** (JEP 425) yüksək miqyaslı konkurrent tətbiqlər üçün nəzərdə tutulmuş yüngül thread-lərdir. Ənənəvi platform thread-lərindən (OS thread-ləri) fərqli olaraq, virtual thread-lər JVM tərəfindən idarə olunur.

### Virtual Thread-lərin Xüsusiyyətləri
- **Yüngül**: Hər virtual thread çox az yaddaş (~1KB) istifadə edir, platform thread-ləri isə ~1MB/stack tələb edir.
- **Miqyaslılıq**: Minlərlə və ya milyonlarla virtual thread yaratmaq mümkündür.
- **Bloklama Əməliyyatları**: I/O əməliyyatlarında (fayl oxuma, şəbəkə sorğuları) virtual thread avtomatik dayandırılır və bərpa olunur.
- **Thread Hovuzuna Ehtiyac Yoxdur**: Virtual thread-lər ənənəvi thread hovuzlarını əvəz edir.

### Virtual Thread-lərin Yaradılması
```java
public class VirtualThreadExample {
    public static void main(String[] args) {
        Thread virtualThread = Thread.ofVirtual().start(() -> {
            System.out.println("Virtual thread işləyir: " + Thread.currentThread());
        });
    }
}
```

### Virtual Thread-lər ilə ExecutorService
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
public class VirtualThreadExecutor {
    public static void main(String[] args) {
        try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
            for (int i = 0; i < 1000; i++) {
                executor.submit(() -> {
                    System.out.println("Task icra olunur: " + Thread.currentThread());
                });
            }
        }
    }
}
```

### Virtual Thread-lər Nə Vaxt İstifadə Olunur?
- **I/O-intensive Tapşırıqlar**: Fayl oxuma/yazma, şəbəkə əməliyyatları.
- **Yüksək Konkurrentlik**: Veb serverlər, mikroxidmətlər kimi sistemlər.
- **Sadəlik**: Sinxronizasiya və thread hovuzlarının idarə edilməsindən azad edir.

### Virtual Thread vs Platform Thread
| Xüsusiyyət              | Platform Thread         | Virtual Thread          |
|-------------------------|-------------------------|-------------------------|
| Yaratma Xərci           | Yüksək (OS thread-i)    | Aşağı (JVM idarə edir)  |
| Yaddaş İstehlakı        | Böyük (~1MB/stack)      | Kiçik (~1KB/stack)      |
| Miqyaslılıq             | Məhdud (~bir neçə min)  | Yüksək (~milyonlarca)   |
| Bloklama                | OS səviyyəsində         | JVM tərəfindən idarə    |
| İstifadə Sahəsi         | CPU-intensive           | I/O-intensive           |

## 4. Thread-lərlə İşləyərkən Problemlər və Həllər

### 4.1. Thread Interference
**Tərif**: Thread-lər eyni dəyişəni eyni anda dəyişdirərkən məlumatın korlanması.
**Həll**:
- `synchronized` və ya `ReentrantLock` ilə kilidləmə.
- `Atomic` siniflərdən istifadə.
- Thread-safe kolleksiyalar (`ConcurrentHashMap`, `CopyOnWriteArrayList`).

### 4.2. Starvation
**Tərif**: Bəzi thread-lərin resurslara çata bilməməsi.
**Həll**:
- `ReentrantLock` ilə ədalətli kilidləmə (`new ReentrantLock(true)`).
- Thread prioritetlərini ehtiyatla istifadə edin.

### 4.3. Livelock
**Tərif**: Thread-lər bir-birinə yol verməyə çalışarkən irəliləyə bilməməsi.
**Həll**:
- Təsadüfi gözləmə müddətləri əlavə edin.
- Resurs sıralamasından istifadə edin.

## 5. Praktiki Nümunə: Bilet Rezervasiya Sistemi

Aşağıda virtual thread-lərlə real-time bilet rezervasiya sistemi göstərilir. Sistem race condition-lardan qorunur, sinxronizasiya mexanizmləri istifadə edir və 30 saniyəlik rezervasiya müddətini idarə edir.

```java
import java.util.concurrent.*;
import java.util.concurrent.atomic.AtomicInteger;
import java.util.concurrent.locks.ReentrantLock;
import java.util.*;

public class VirtualTicketReservationSystem {
    private final int totalTickets;
    private final AtomicInteger availableTickets;
    private final Map<Integer, Reservation> reservations;
    private final ReentrantLock lock;
    private final ScheduledExecutorService scheduler;
    private final Semaphore paymentSemaphore;
    private final Random random;

    private static class Reservation {
        final int userId;
        final int ticketId;
        final long reservationTime;
        volatile boolean isPaid;

        Reservation(int userId, int ticketId, long reservationTime) {
            this.userId = userId;
            this.ticketId = ticketId;
            this.reservationTime = reservationTime;
            this.isPaid = false;
        }
    }

    public VirtualTicketReservationSystem(int totalTickets) {
        this.totalTickets = totalTickets;
        this.availableTickets = new AtomicInteger(totalTickets);
        this.reservations = new ConcurrentHashMap<>();
        this.lock = new ReentrantLock();
        this.scheduler = Executors.newScheduledThreadPool(4);
        this.paymentSemaphore = new Semaphore(10);
        this.random = new Random();
    }

    public boolean reserveTicket(int userId) throws InterruptedException {
        lock.lock();
        try {
            while (availableTickets.get() == 0 && reservations.size() >= totalTickets) {
                System.out.printf("User %d: Bilet yoxdur, gözləyir...%n", userId);
                return false;
            }

            if (availableTickets.get() > 0) {
                int ticketId = totalTickets - availableTickets.decrementAndGet();
                Reservation reservation = new Reservation(userId, ticketId, System.currentTimeMillis());
                reservations.put(ticketId, reservation);
                System.out.printf("User %d: Bilet %d rezerv edildi%n", userId, ticketId);
                scheduler.schedule(() -> checkReservationTimeout(reservation), 30, TimeUnit.SECONDS);
                return true;
            }
            return false;
        } finally {
            lock.unlock();
        }
    }

    private void checkReservationTimeout(Reservation reservation) {
        lock.lock();
        try {
            if (!reservation.isPaid) {
                reservations.remove(reservation.ticketId);
                availableTickets.incrementAndGet();
                System.out.printf("User %d: Bilet %d ödəniş vaxtı bitdi, ləğv edildi%n", 
                    reservation.userId, reservation.ticketId);
            }
        } finally {
            lock.unlock();
        }
    }

    public boolean processPayment(int userId, int ticketId) throws InterruptedException {
        if (!paymentSemaphore.tryAcquire(5, TimeUnit.SECONDS)) {
            System.out.printf("User %d: Ödəniş sistemi məşğuldur%n", userId);
            return false;
        }

        try {
            Reservation reservation = reservations.get(ticketId);
            if (reservation == null || reservation.userId != userId || reservation.isPaid) {
                return false;
            }

            Thread.sleep(random.nextInt(2000) + 1000);
            lock.lock();
            try {
                if (reservations.containsKey(ticketId)) {
                    reservation.isPaid = true;
                    System.out.printf("User %d: Bilet %d ödənildi%n", userId, ticketId);
                    return true;
                }
                return false;
            } finally {
                lock.unlock();
            }
        } finally {
            paymentSemaphore.release();
        }
    }

    public void shutdown() {
        scheduler.shutdown();
    }

    public static void main(String[] args) {
        final int TOTAL_TICKETS = 20;
        final int TOTAL_USERS = 50;
        VirtualTicketReservationSystem system = new VirtualTicketReservationSystem(TOTAL_TICKETS);

        try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
            for (int userId = 1; userId <= TOTAL_USERS; userId++) {
                final int currentUserId = userId;
                executor.submit(() -> {
                    try {
                        if (system.reserveTicket(currentUserId)) {
                            int behavior = new Random().nextInt(3);
                            if (behavior == 0) {
                                System.out.printf("User %d: Ödəniş etmədi%n", currentUserId);
                            } else if (behavior == 1) {
                                Thread.sleep(35000);
                                system.processPayment(currentUserId, TOTAL_TICKETS - system.availableTickets.get() - 1);
                            } else {
                                Thread.sleep(new Random().nextInt(10000));
                                system.processPayment(currentUserId, TOTAL_TICKETS - system.availableTickets.get() - 1);
                            }
                        }
                    } catch (InterruptedException e) {
                        Thread.currentThread().interrupt();
                    }
                });
            }
        }

        system.shutdown();
        System.out.println("Simulyasiya tamamlandı. Qalan bilet: " + system.availableTickets.get());
    }
}
```

### Sistem Xüsusiyyətləri
- **Race Condition Qorunması**: `ReentrantLock` və `AtomicInteger` ilə.
- **Thread Koordinasiyası**: `Condition` və `Semaphore` ilə resurs girişi idarə olunur.
- **Zaman İdarəetməsi**: `ScheduledExecutorService` ilə 30 saniyəlik rezervasiya müddəti.
- **Miqyaslılıq**: Virtual thread-lər minlərlə istifadəçini dəstəkləyir.

## 6. Intervyu Sualları və Cavablar

### Sual 1: Thread ilə Runnable arasındakı fərq nədir?
**Cavab**: `Thread` sinfdir və birbaşa thread yaradır. `Runnable` interfeysdir və yalnız icra ediləcək kodu təyin edir. `Runnable` daha çevikdir, çünki sinf başqa sinfi miras ala bilər və thread hovuzları ilə uyğundur.

### Sual 2: Virtual thread-lər nədir və nə üçün istifadə olunur?
**Cavab**: Virtual thread-lər JVM tərəfindən idarə olunan yüngül thread-lərdir. I/O-intensive tapşırıqlarda yüksək konkurrentlik təmin edir, çox az yaddaş istifadə edir və bloklama əməliyyatlarında avtomatik idarə olunur.

### Sual 3: Race condition nədir və necə qarşısını almaq olar?
**Cavab**: Race condition bir neçə thread-in eyni resursa nəzarətsiz daxil olmasıdır. Qarşısını almaq üçün:
- `synchronized` və ya `ReentrantLock` istifadə edin.
- `Atomic` siniflərdən istifadə edin.
- Thread-safe kolleksiyalar seçin.

### Sual 4: Deadlock nədir və necə aşkar edilir?
**Cavab**: Deadlock thread-lərin bir-birini gözləməsi nəticəsində kilidlənməsidir. Aşkar etmək üçün JConsole, VisualVM və ya `ThreadMXBean` istifadə olunur. Qarşısını almaq üçün resurs sıralaması və timeout tətbiq edin.

### Sual 5: `synchronized` ilə `ReentrantLock` arasındakı fərq nədir?
**Cavab**: `synchronized` daxili kilidləmədir, sadədir, lakin çevik deyil. `ReentrantLock` `tryLock()`, `Condition` və ədalətli kilidləmə kimi əlavə funksionallıq təklif edir.

## 7. Tövsiyələr
- **Thread-lərdə**:
  - Sinxronizasiyaya diqqət edin.
  - Deadlock və race condition-lardan qaçın.
  - Resurs istehlakını optimallaşdırın.
- **Virtual Thread-lərdə**:
  - I/O-intensive tapşırıqlarda istifadə edin.
  - `newVirtualThreadPerTaskExecutor()` ilə miqyaslı sistemlər qurun.
- **Intervyuya Hazırlıq**:
  - Sinxronizasiya mexanizmlərini dərindən öyrənin.
  - Deadlock və race condition nümunələri ilə praktiki həllər təklif edin.
  - Virtual thread-lərin üstünlüklərini izah edin.

Bu sənəd Java-da thread və multithreading mövzularını tam əhatə edir. Əlavə suallarınız varsa, əlaqə saxlayın!

5. **Thread pool ilə Virtual Thread-ləri müqayisə edin.**
   - **Cavab:** Thread pool məhdud sayda platform thread-lərindən ibarətdir və resurs istehlakı yüksəkdir. Virtual thread-lər isə thread pool-a ehtiyac olmadan minlərlə tapşırığı idarə edə bilər, çünki JVM tərəfindən optimallaşdırılmış planlaşdırma ilə işləyir. Virtual thread-lər `Executors.newVirtualThreadPerTaskExecutor()` ilə asanlıqla istifadə olunur.
