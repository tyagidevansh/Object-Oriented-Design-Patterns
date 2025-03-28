# Singleton Design Pattern

Singleton ek **creational design pattern** hai jo **ek class ka sirf ek hi instance ensure karta hai** aur us instance ko globally accessible banata hai.  

✔ **Matlab:**  
   - Ek hi object **poore system me reuse hota hai.**  
   - **Multiple objects create nahi hote, ek hi shared instance hota hai.**  

➡ **Real-World Example:**  
   - Tumhare **phone ka settings app** ek **singleton hota hai**, kyunki agar har baar naya instance banega to **alag-alag settings objects** honge, jo **system ko corrupt kar sakte hain.**  

---

## **2️⃣ Kab Zaroorat Padti Hai? (Motivation & Real-Life Example)**  

1️⃣ **Jab kisi class ka ek hi instance chahiye throughout the application.**  
2️⃣ **Jab ek shared resource ko manage karna ho, jaise Database Connection, Logging, Configuration Settings.**  
3️⃣ **Jab global state maintain karni ho bina multiple instances create kiye.**  

➡ **Example:**  

🖥 **Operating System ke Task Manager**  
   - Ek hi **task manager instance** system me hota hai.  
   - Agar multiple instances allow kare to **har instance alag CPU/memory usage dikhayega, jo galat hoga.**  

🔌 **Database Connection Pooling**  
   - Agar **har request ke liye naya database connection create ho** to **performance slow ho jayegi.**  
   - Singleton ensure karta hai ki ek hi **database connection shared ho.**  

📝 **Logging System**  
   - Har baar naye logger objects banane se unnecessary memory use hogi.  
   - Singleton ek **single logger instance** maintain karta hai.  

---

## **3️⃣ Singleton Pattern ka Structure & Components**  

Singleton pattern ke **3 main components** hote hain:  

1️⃣ **Private Constructor**  
   - **Direct object creation rokta hai.**  
   
2️⃣ **Static Method (getInstance)**  
   - **Instance ko manage karta hai aur ek hi baar create karta hai.**  

3️⃣ **Static Instance Variable**  
   - **Ek single instance ko store karta hai.**  

---

## **4️⃣ UML Diagram & Code Example**  

### **Class Diagram (Singleton Pattern Structure)**  

```
┌──────────────────────────────┐
│      SingletonClass          │
│ ──────────────────────────── │
│ - instance: SingletonClass   │   # Private Static Variable
│ + getInstance(): SingletonClass │  # Static Method
│ - __init__()                 │   # Private Constructor
└──────────────────────────────┘
```

---

### **Python Code Example - Singleton Pattern**  

```python
class Singleton:
    _instance = None  # Private static variable

    def __new__(cls):
        if cls._instance is None:
            print("Creating a new instance...")  # First time instance creation
            cls._instance = super(Singleton, cls).__new__(cls)
        return cls._instance

# Client Code
singleton1 = Singleton()
print(singleton1)

singleton2 = Singleton()
print(singleton2)

# Output will show both variables point to the same instance
print(singleton1 is singleton2)  # ✅ True
```

✅ **Output:**  
```
Creating a new instance...
<__main__.Singleton object at 0x7f...>
<__main__.Singleton object at 0x7f...>
True  # Both variables point to the same instance
```

✔ **Explanation:**  
   - `singleton1` pehli baar `Singleton` ka instance banata hai.  
   - `singleton2` ko jab call karte hain to **naya instance create nahi hota, balki existing instance return hota hai.**  

---

## **5️⃣ Thread-Safe Singleton (Multithreading Me Safe Kaise Kare?)**  

Agar **multithreading environment** me multiple threads ek saath `getInstance()` ko call kare to multiple instances create ho sakte hain. **Isko avoid karne ke liye threading safe Singleton implement karte hain.**  

```python
import threading

class ThreadSafeSingleton:
    _instance = None
    _lock = threading.Lock()  # Thread synchronization ke liye lock

    def __new__(cls):
        with cls._lock:  # Lock ensure karega ki ek hi thread ek time pe instance create kare
            if cls._instance is None:
                print("Creating a new instance in a thread-safe way...")
                cls._instance = super(ThreadSafeSingleton, cls).__new__(cls)
        return cls._instance

# Client Code
def test_singleton():
    singleton = ThreadSafeSingleton()
    print(singleton)

# Multiple threads execute karega
thread1 = threading.Thread(target=test_singleton)
thread2 = threading.Thread(target=test_singleton)

thread1.start()
thread2.start()

thread1.join()
thread2.join()
```

✅ **Thread-Safe Output:**  
```
Creating a new instance in a thread-safe way...
<__main__.ThreadSafeSingleton object at 0x7f...>
<__main__.ThreadSafeSingleton object at 0x7f...>
```

✔ **Multithreading me bhi sirf ek hi instance create hoga!**  

---

## **6️⃣ Real-World Examples of Singleton Pattern** 🌍  

1️⃣ **Database Connection (MySQL, PostgreSQL, MongoDB)**  
   - **Ek hi connection instance use hota hai taaki multiple unnecessary connections na bane.**  

2️⃣ **Logging Frameworks (Log4j, Python Logger)**  
   - **Ek hi logger instance maintain hota hai taaki log consistency bani rahe.**  

3️⃣ **Thread Pools in Web Servers**  
   - **Agar har request ke liye naya thread create hoga to system slow ho jayega.**  
   - **Singleton ek fixed pool maintain karta hai.**  

4️⃣ **Cache Management (Redis, Memcached)**  
   - **Data ko memory me store karke fast access provide karta hai.**  

5️⃣ **Configuration Management**  
   - **Application-wide configurations ek hi instance se manage hoti hain.**  

---

## **7️⃣ Singleton Pattern ke Fayde & Limitations** ⚠  

### **✅ Fayde (Advantages):**  
✔ **Memory Efficient:** Har baar naya object create nahi hota, sirf ek hi instance reuse hota hai.  
✔ **Thread-Safe Implementation:** Multi-threaded environments me ek hi instance ensure kiya jata hai.  
✔ **Global Access Point:** Pura system ek hi instance ko access karta hai.  
✔ **Performance Optimization:** Har baar naye objects create karne se bachata hai.  

---

### **❌ Limitations (Disadvantages):**  
❌ **Global State Issues:** Agar singleton instance corrupt ho jaye to pura system impact hota hai.  
❌ **Testing Difficulties:** Singleton ki wajah se mocking/testing difficult ho sakti hai.  
❌ **High Coupling Risk:** Agar ek singleton class kisi aur module pe depend hai, to tight coupling ho sakti hai.  

---

## **8️⃣ Singleton Pattern ke Software Design Principles** 🎯  

✔ **Encapsulation:** Instance variable ko private rakha jata hai.  
✔ **Single Responsibility Principle (SRP):** Ek hi kaam karta hai – ek instance maintain karna.  
✔ **Lazy Initialization:** Jab tak `getInstance()` call nahi hota, tab tak object create nahi hota.  
✔ **Thread Safety:** Synchronization ensure karta hai ki multiple threads ek hi instance share karein.  

---

## **🔹 Singleton Pattern Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - Singleton ek creational pattern hai jo **ek class ka ek hi instance** maintain karta hai.  

2️⃣ **Kab Use Karte Hain?**  
   - Jab ek **shared resource (Logger, Database Connection, Configurations) maintain karna ho.**  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Private Constructor + Static Method + Static Variable** use karke ek hi instance ensure kiya jata hai.  

4️⃣ **Real-World Examples:**  
   - **Logging System, Database Connections, Cache Management, Thread Pools.**  

5️⃣ **Fayde & Limitations:**  
   ✔ **Memory Efficient, Global Access, Thread-Safe Implementation.**  
   ❌ **Difficult to Test, Global State Issues, Risk of Tight Coupling.**  

---

### **💡 Conclusion**  
Singleton Pattern ek **powerful design pattern hai jo performance optimize karta hai**, lekin **sahi tarike se use na ho to overuse aur testing issues create kar sakta hai.** 🚀
