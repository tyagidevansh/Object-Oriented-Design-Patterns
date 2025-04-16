# **Proxy Pattern**

Proxy design pattern is a **structural design pattern** jo **original object ka placeholder ya proxy (no way)** provide karta hai. Yeh pattern **object creation, access control, caching**, ya **logging** jaise features add karne ke liye use hota hai, without modifying the original object's code.

➡ **Simple Words Me:**  
Maan lo tumhare paas ek **expensive object** hai, jaise koi **high resolution image** ya **data-intensive service**. Directly is object ko load karne se system ki performance affect ho sakti hai. In this case, **Proxy pattern** use karke tum ek **lightweight substitute object** create kar sakte ho jo zarurat padne par hi asli object ko instantiate karega.  

✅ **Solution:**  
   - Ek **Proxy class** banao jo asli object ke saare operations forward kare ya control kare.  
   - **Common interface define karo** jo original object aur proxy dono implement kare.  
   - Proxy ke through additional functionalities jaise **access control**, **lazy initialization**, ya **logging** implement ki ja sakti hain.  

➡ **Proxy pattern se code modular, secure aur efficient ban jata hai.**

---

## **2️⃣ Kab Zaroorat Padti Hai?**  
Socho tum **remote resource access** ya **data fetching** ka system bana rahe ho, jahan direct access costly ya insecure ho sakta hai:

🔹 **Virtual Proxy:**  
   - Heavy objects ko delay se load karo jab actually zarurat ho.  
🔹 **Protection Proxy:**  
   - Sensitive objects ke access ko restrict karo (jaise user authentication ke basis par).  
🔹 **Logging Proxy:**  
   - Client ki request ko intercept karke log record maintain karo.  

Agar tum **direct access** dete ho, to system vulnerable, inefficient ya overloaded ho sakta hai.  

✅ **Proxy Pattern ka Use:**  
   - Ek **Proxy class** banayein jo real object ke creation ya method calls ko control karegi.  
   - **Common Interface** follow karne se client ko dono me farq nahi dikhega.

---

## **3️⃣ Proxy Pattern ke Main Components**  
Proxy pattern main **3 major components** involve hote hain:

1️⃣ **Subject Interface (Common Interface)** 🧩  
   - Yeh ek **contract** hota hai jo **real object aur proxy dono implement karte hain**.  

2️⃣ **Real Subject (Original Object)** 🎯  
   - Yeh **actual object** hai jisko access control ki zarurat hai ya jiska creation costly hai.  

3️⃣ **Proxy (Placeholder or Surrogate Object)** 🎛  
   - Yeh **real object ke liye substitute** hota hai aur **client ke operations ko intercept** karta hai.
   - Additional functionalities jaise **lazy initialization**, **access control**, **caching**, ya **logging** yahan add ki ja sakti hain.

---

## **4️⃣ UML Diagram & Code Example**

### **Class Diagram (Structure of Proxy Pattern):**  

```
┌─────────────────────────────┐
│         Client              │
│ (Interacts with Subject)    │
└─────────────────────────────┘
            │
            ▼
 ┌─────────────────────────────┐
 │       Subject Interface     │
 └─────────────────────────────┘
            │
     ┌──────┼───────┐
     │              │
     ▼              ▼
┌────────────┐ ┌────────────────┐
│ RealSubject│ │     Proxy      │
└────────────┘ └────────────────┘
```

---

### **Python Code Example - Virtual Proxy for Image Loading** 📝  

```python
from abc import ABC, abstractmethod
import time

# Step 1: Subject Interface
class Image(ABC):
    @abstractmethod
    def display(self):
        pass

# Step 2: Real Subject - High Resolution Image
class HighResolutionImage(Image):
    def __init__(self, filename):
        self.filename = filename
        self.load_image_from_disk()

    def load_image_from_disk(self):
        # Simulate a time-consuming operation
        print(f"📂 Loading image '{self.filename}' from disk...")
        time.sleep(2)
        print("✅ Image loaded.")

    def display(self):
        print(f"🖼 Displaying high resolution image: {self.filename}")

# Step 3: Proxy - Controls access to the RealSubject
class ImageProxy(Image):
    def __init__(self, filename):
        self.filename = filename
        self.real_image = None

    def display(self):
        # Lazy Initialization: Load real image only on demand
        if self.real_image is None:
            self.real_image = HighResolutionImage(self.filename)
        print("🔍 Proxy delegating display call to real image.")
        self.real_image.display()

# Step 4: Client Code (Using the Proxy Pattern)
if __name__ == "__main__":
    print("Client: Requesting to display image via proxy.")
    image = ImageProxy("sample_photo.jpg")
    
    # First call: image gets loaded
    image.display()
    
    print("\nClient: Requesting to display image again (should be fast).")
    # Second call: image is already loaded, so no delay
    image.display()
```

✅ **Code ab efficient hai:**  
   - **Lazy Initialization:** Image only load hoti hai jab first time display() call kiya jata hai.  
   - **Access Control & Additional Processing:** Proxy additional checks ya logging add kar sakta hai.

---

## **5️⃣ Real-World Examples** 🌍  

1️⃣ **Remote Proxies:**  
   - **Web Services:** Server ke expensive processes ya remote resources ko access karne ke liye.  

2️⃣ **Protection Proxies:**  
   - **File Systems:** Sensitive data ya methods ko unauthorized access se protect karna.  

3️⃣ **Caching Proxies:**  
   - **Database Queries:** Repeated query results ko cache karke performance improve karna.  

4️⃣ **Smart References:**  
   - **Virtual Proxies in GUI Applications:** Heavy resources (images/documents) ko tabhi load karna jab user actually unhe dekhna chahe.

---

## **6️⃣ Limitations & Pitfalls** ⚠  

❌ **Additional Complexity:**  
   - Proxy pattern use karne se code me extra abstraction layer add ho jati hai.  

❌ **Performance Overhead:**  
   - Har method call proxy ke through pass hota hai, jo additional latency la sakta hai (agar proper optimize na kiya jaaye).  

❌ **Maintenance Burden:**  
   - Agar proxy me zyada functionalities add kar di jaye, to debugging aur maintenance mushkil ho sakti hai.

---

## **7️⃣ Proxy Pattern ke Software Design Principles** 🎯  

✔ **Encapsulation:**  
   - Real object ke operations ko encapsulate karke extra functionalities add karna.  

✔ **Separation of Concerns:**  
   - Client aur real object ke beech mediation karna, jo alag responsibilities maintain karta hai.  

✔ **Open/Closed Principle (OCP):**  
   - Existing classes ko modify kiye bina naya behavior add karna possible hota hai.  

✔ **Single Responsibility Principle (SRP):**  
   - Proxy ka ek hi responsibility rehta hai: real object ke access ko control ya enhance karna.

---

## **🔹 Proxy Pattern Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - Proxy pattern ek **surrogate object** provide karta hai jo **real object ka access control**, **initialization**, ya **logging** manage karta hai.  

2️⃣ **Kab Use Karte Hain?**  
   - Jab real object expensive ho ya access control, security, ya caching ki zarurat ho.  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Common interface + Real Subject + Proxy class** jo extra functionalities provide kar sakti hai.  

4️⃣ **Real-World Examples:**  
   - **Remote Services, Protection Proxies, Caching Mechanisms, GUI Resource Management.**

5️⃣ **Fayde & Limitations:**  
   ✔ **Code modular aur secure ban jata hai**.  
   ❌ **Extra abstraction se complexity aur overhead badh sakta hai**.

---

### **💡 Conclusion**  
Proxy pattern **real object ke operations ko control, optimize aur secure** karta hai, aur **design ko modular aur extendable** banane ka ek effective tareeka provide karta hai. Is pattern se system ka performance improve hota hai aur code flexibility badh jati hai. 🚀