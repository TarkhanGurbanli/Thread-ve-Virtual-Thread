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

5. **Thread pool ilə Virtual Thread-ləri müqayisə edin.**
   - **Cavab:** Thread pool məhdud sayda platform thread-lərindən ibarətdir və resurs istehlakı yüksəkdir. Virtual thread-lər isə thread pool-a ehtiyac olmadan minlərlə tapşırığı idarə edə bilər, çünki JVM tərəfindən optimallaşdırılmış planlaşdırma ilə işləyir. Virtual thread-lər `Executors.newVirtualThreadPerTaskExecutor()` ilə asanlıqla istifadə olunur.
