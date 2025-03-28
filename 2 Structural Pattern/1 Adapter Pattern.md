### Adapter Pattern
Adapter ek **structural design pattern** hai jo **do incompatible interfaces** ko ek saath kaam karne ke laayak banata hai. Agar koi **naya system purane system ke saath directly compatible nahi hai**, toh Adapter ek **bridge** ki tarah kaam karta hai, jo **interface conversion** karta hai bina kisi system ko modify kiye.  

➡ **Simple Words Me:**  
Socho tumhare **phone me USB-C port** hai, lekin charger **USB-A** hai. Dono directly connect nahi ho sakte, isliye ek **USB-A to USB-C adapter** ka use hota hai. Isi tarah, Adapter pattern software me bhi **interface compatibility** ka kaam karta hai.  

---

#### **2️⃣ Kab Zaroorat Padti Hai? (Motivation)**  
Maan lo ek **legacy logging system** hai jo logs **XML format** me store karta hai. Ab ek naya system introduce ho gaya hai jo logs **JSON format** me chahiye. Dono ke **interfaces aur method names alag hain**, toh dono ek saath kaam nahi kar sakte.  

➡ **Possible Solutions:**  
❌ **Code Merge Karna:**  
- Dono systems ko ek saath combine karna **complex aur risky** ho sakta hai.  
- Single Responsibility Principle (SRP) **break** ho jayega, kyunki ek system **multiple functionalities** handle karega.  
- Maintain karna mushkil ho jayega, aur naye changes ke saath bugs aa sakte hain.  

✅ **Adapter Pattern Use Karna:**  
- Ek **Adapter class** banakar **legacy XML logger ko JSON logger ke format me convert** kar sakte hain.  
- Naya system bina kisi problem ke **old system ke logs read aur use** kar sakega.  
- **Code maintainable aur scalable** rahega.  

---

#### **3️⃣ Adapter Pattern ke Main Components**  
Adapter pattern **4 major components** se bana hota hai:  

1️⃣ **Target Interface** 🎯  
   - Yeh wo **naya interface** hai jo system expect karta hai.  
   - Client code is interface ke through kaam karega.  

2️⃣ **Adaptee** 🔄  
   - **Old system** ya legacy component jo **Target Interface se compatible nahi hai**.  
   - Apni original functionality maintain karta hai, **sirf adapter ke through use hota hai**.  

3️⃣ **Adapter** 🔌  
   - **Bridge (Pul)** jo Adaptee ko Target Interface ke saath connect karta hai.  
   - **Method calls ko convert karta hai** taaki dono systems ek saath kaam karein.  

4️⃣ **Client** 💻  
   - Jo system ko **Target Interface ke through access karta hai**.  
   - **Adapter aur Adaptee ka existence client ko pata bhi nahi hota**.  

---

#### **4️⃣ UML Diagram & Code Example**  

**Class Diagram (Structure of Adapter Pattern):**  

```
┌──────────────────┐       ┌──────────────────┐
│ Target Interface │<------│     Adapter      │
└──────────────────┘       └──────────────────┘
                                   │
                           ┌──────────────────┐
                           │      Adaptee     │
                           └──────────────────┘
```

**Python Code Example:**  
```python
from abc import ABC, abstractmethod

# Target Interface (New System Logger)
class JSONLogger(ABC):
    @abstractmethod
    def log_message(self, message: str) -> None:
        pass

# Adaptee (Legacy System)
class XMLLogger:
    def log(self, XML_message: str) -> None:
        print(XML_message)

# Adapter (Bridge Between Target & Adaptee)
class LoggerAdapter(JSONLogger):
    def __init__(self, XML_logger: XMLLogger) -> None:
        self.XML_logger = XML_logger

    def log_message(self, message: str) -> None:
        self.XML_logger.log(message)

# Client Code
logger = LoggerAdapter(XMLLogger())
logger.log_message("<message>hello</message>")  
```
✅ **Yeh code ensure karta hai ki XMLLogger (Old System) ko JSONLogger (New System) ki tarah treat kiya ja sake.**  

---

#### **5️⃣ Real-World Example** 🌍  

1️⃣ **Hardware Example - USB Adapter:**  
   - Phone **USB-C port expect karta hai**, par charger **USB-A** hai.  
   - **Adapter use karne se dono kaam karne lagte hain.**  
   
2️⃣ **Software Example - Payment Gateway Integration:**  
   - E-commerce websites PayPal, Stripe, aur Razorpay jaise **multiple payment gateways** support karti hain.  
   - Har gateway ka **alag API aur method names hote hain**.  
   - **Adapter pattern ka use karke ek universal interface bana sakte hain**, jo internally har gateway ke API se connect ho sake.  

3️⃣ **Cross-Platform Compatibility:**  
   - Windows, Mac, aur Linux ke **file systems aur functions different hote hain**.  
   - Adapter pattern ka use karke **ek common interface** bana sakte hain jo sab platforms pe kaam kare.  

---

#### **6️⃣ Limitations & Pitfalls** ⚠  
Adapter pattern har situation ke liye best nahi hota. Kuch **limitations aur challenges** hain:  

❌ **Performance Overhead**  
   - Adapter extra conversion steps introduce karta hai, jo performance slow kar sakta hai.  
   - Agar **real-time processing** systems (e.g., stock trading) me use karein, toh carefully optimize karna padega.  

❌ **Complexity in Maintenance**  
   - Agar multiple adapters banane pad gaye, toh **system overly complex ho sakta hai**.  
   - Legacy system me **koi update aaye, toh uske adapters bhi modify karne padenge**.  

---

#### **7️⃣ Adapter Pattern ke Software Design Principles** 🎯  

✔ **Single Responsibility Principle (SRP)**  
   - Adapter **sirf conversion ka kaam karta hai**, original components ka kaam nahi badalta.  

✔ **Open/Closed Principle (OCP)**  
   - Naye adapters bana sakte hain bina purane system ko modify kiye.  

✔ **Loose Coupling**  
   - Adapter ensure karta hai ki **new aur old systems tightly coupled na ho**, taaki dono ko alag-alag update kiya ja sake.  

---

### **🔹 Adapter Pattern Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - Adapter **do incompatible interfaces ko compatible banata hai** bina code modify kiye.  

2️⃣ **Kab Use Karte Hain?**  
   - Jab **legacy systems aur new systems** ko saath kaam karwana ho.  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Adapter** bridge ka kaam karta hai jo **old system ke calls ko naya format** me convert karta hai.  

4️⃣ **Real-World Examples:**  
   - **USB-C to USB-A charger**, **Payment Gateways (PayPal, Stripe Adapter)**, **Cross-Platform File Systems**.  

5️⃣ **Fayde & Limitations:**  
   ✔ **Loose coupling aur maintainability improve hoti hai**.  
   ❌ **Performance slow ho sakta hai aur complexity badh sakti hai**.  

---

### **💡 Conclusion**  
Adapter pattern ek **powerful solution hai** jab legacy aur modern systems ko ek saath kaam karwana ho. Yeh **code reusability, flexibility aur maintainability** badhata hai. Agar **performance aur complexity manage kar sakein**, toh yeh **best solution ho sakta hai for integrating old & new systems**. 🚀
