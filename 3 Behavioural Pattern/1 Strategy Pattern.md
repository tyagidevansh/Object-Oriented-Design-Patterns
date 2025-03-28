# **Strategy Pattern**  
Strategy ek **behavioral design pattern** hai jo **ek class ke behavior ko dynamically change karne ki flexibility provide karta hai**. Is pattern ka use tab hota hai jab **multiple algorithms ya behaviors available ho** aur hum **runtime pe decide karna chahte hain ki kaunsa use karna hai**.  

➡ **Simple Words Me:**  
Maan lo tum ek **payment system** bana rahe ho jo **Credit Card, UPI, aur PayPal** se payment accept kare. Tum **alag-alag payment ke liye if-else ya switch case use kar sakte ho**, lekin ye **code complexity aur maintenance problem create karega**.  

✅ **Solution:**  
   - Har ek payment method ke liye **alag class** bana lo.  
   - **Common interface define karo** jo har method implement karega.  
   - Ek **context class banao jo runtime pe decide kare ki kaunsa strategy use karna hai**.  

➡ **Strategy pattern se code reusable, scalable aur maintainable ban jata hai.**  

---

## **2️⃣ Kab Zaroorat Padti Hai? (Motivation & Real-Life Example)**  
Socho tum **ek navigation system (Google Maps) bana rahe ho** jo different **routes suggest kare**:  

🔹 **Car ke liye Fastest Route** 🚗  
🔹 **Bike ke liye Shortest Route** 🏍️  
🔹 **Public Transport ke liye Bus/Train Route** 🚌🚆  
🔹 **Walking ke liye Safe Route** 🚶  

Agar tum **if-else ya switch case lagate ho**, to **code complex ho jayega** aur naye algorithms add karna mushkil hoga.  

✅ **Strategy Pattern ka Use:**  
   - Har ek routing method ke liye ek **alag strategy class** bana do.  
   - **Common Interface define karo** (sabhi strategies ko implement karna pade).  
   - **Context class** runtime pe decide karega kaunsa algorithm use karna hai.  

---

## **3️⃣ Strategy Pattern ke Main Components**  
Strategy pattern **3 major components** se bana hota hai:  

1️⃣ **Strategy Interface (Algorithm Interface)** 🧩  
   - Yeh ek **common interface** hota hai jo **sabhi algorithms implement karte hain**.  

2️⃣ **Concrete Strategies (Different Algorithms)** 🎯  
   - Yeh **actual algorithm classes hoti hain** jo interface ko implement karti hain.  
   - Example: `CreditCardPayment`, `UPIPayment`, `PayPalPayment`.  

3️⃣ **Context Class (Dynamic Behavior Selector)** 🎛  
   - Yeh **client ke request ke basis pe runtime pe strategy select karta hai**.  
   - Example: `PaymentContext` jo user ke **payment method ke basis pe appropriate class choose karega**.  

---

## **4️⃣ UML Diagram & Code Example**  

### **Class Diagram (Structure of Strategy Pattern):**  

```
┌───────────────────────────┐
│        Client            │
│  (User selects strategy) │
└───────────────────────────┘
            │
            ▼
┌───────────────────────────┐
│        Context           │
│  (Manages the Strategy)  │
│ PaymentContext.setStrategy() │
└───────────────────────────┘
            │
 ┌─────────┼──────────┐
 │         │          │
 ▼         ▼          ▼
┌──────────┐  ┌──────────┐  ┌──────────────┐
│  Credit  │  │  UPI     │  │  PayPal      │
│  Card    │  │ Payment  │  │ Payment      │
└──────────┘  └──────────┘  └──────────────┘
```

---

### **Python Code Example - Payment System** 📝  

```python
# Step 1: Strategy Interface (Common Interface for all strategies)
from abc import ABC, abstractmethod

class PaymentStrategy(ABC):
    @abstractmethod
    def pay(self, amount):
        pass

# Step 2: Concrete Strategy Classes (Different Payment Methods)
class CreditCardPayment(PaymentStrategy):
    def pay(self, amount):
        print(f"💳 Paid ₹{amount} using Credit Card.")

class UPIPayment(PaymentStrategy):
    def pay(self, amount):
        print(f"📱 Paid ₹{amount} using UPI.")

class PayPalPayment(PaymentStrategy):
    def pay(self, amount):
        print(f"💰 Paid ₹{amount} using PayPal.")

# Step 3: Context Class (Manages Strategy)
class PaymentContext:
    def __init__(self, strategy: PaymentStrategy):
        self.strategy = strategy

    def set_strategy(self, strategy: PaymentStrategy):
        self.strategy = strategy

    def execute_payment(self, amount):
        self.strategy.pay(amount)

# Step 4: Client Code (Using the Strategy Pattern)
if __name__ == "__main__":
    # User selects payment method
    payment = PaymentContext(CreditCardPayment())
    payment.execute_payment(500)  # 💳 Paid ₹500 using Credit Card.

    payment.set_strategy(UPIPayment()) 
    payment.execute_payment(200)  # 📱 Paid ₹200 using UPI.

    payment.set_strategy(PayPalPayment())
    payment.execute_payment(1000)  # 💰 Paid ₹1000 using PayPal.
```

✅ **Code kaafi clean aur scalable ho gaya hai. Naye payment methods add karne ke liye sirf ek new strategy class likhni padegi.**  

---

## **5️⃣ Real-World Examples** 🌍  

1️⃣ **Google Maps Navigation:**  
   - **Different algorithms for different travel modes** (Car, Bike, Walk, Public Transport).  
   - Strategy pattern ensures **flexibility** aur **modular design**.  

2️⃣ **Sorting Algorithms (Java Collections & Python Sorted):**  
   - **Different sorting strategies hoti hain** (`QuickSort`, `MergeSort`, `BubbleSort`).  
   - Strategy pattern ensure karta hai ki **correct sorting technique runtime pe apply ho sake**.  

3️⃣ **Compression Software (ZIP, RAR, 7z):**  
   - Different **compression algorithms (ZIP, RAR, TAR, GZIP)** ek hi interface ke through use hote hain.  

4️⃣ **E-Commerce Coupon System:**  
   - Different discount strategies:  
     - **Flat Discount (₹50 OFF)**
     - **Percentage Discount (10% OFF)**
     - **BOGO (Buy One Get One Free)**  
   - Strategy pattern ensure karta hai ki **correct discount rule apply ho**.  

---

## **6️⃣ Limitations & Pitfalls** ⚠  

❌ **Complexity Increase Ho Sakti Hai:**  
   - Har new behavior ke liye **new class likhni padti hai**, jo **codebase bada kar sakta hai**.  

❌ **Client ko Strategy Select Karni Padti Hai:**  
   - Client ko **yeh decide karna padta hai ki kaunsa algorithm use karna hai**, jo kabhi kabhi problematic ho sakta hai.  

❌ **More Classes, More Memory Usage:**  
   - **Har strategy alag class me likhne se memory consumption badh sakti hai**.  

---

## **7️⃣ Strategy Pattern ke Software Design Principles** 🎯  

✔ **Encapsulation:**  
   - Algorithms **alag classes me encapsulated hote hain**, jo **modularity improve karta hai**.  

✔ **Open/Closed Principle (OCP):**  
   - **New strategies add karna easy hota hai bina existing code modify kiye**.  

✔ **Single Responsibility Principle (SRP):**  
   - Har **strategy ka ek hi responsibility hota hai**.  

✔ **Loose Coupling:**  
   - Context **directly strategy classes ke methods call nahi karta**, balki **interface ke through interact karta hai**.  

---

## **🔹 Strategy Pattern Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - Strategy pattern **behavior change karne ke liye use hota hai** jo **runtime pe select ho sakta hai**.  

2️⃣ **Kab Use Karte Hain?**  
   - Jab **multiple algorithms ya behaviors available ho aur unko dynamically select karna ho**.  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Common interface + Concrete strategies + Context class jo runtime pe decide karega**.  

4️⃣ **Real-World Examples:**  
   - **Google Maps, Sorting Algorithms, E-Commerce Discounts, Payment Systems.**  

5️⃣ **Fayde & Limitations:**  
   ✔ **Code modular aur reusable hota hai**.  
   ❌ **Har naye behavior ke liye new class likhni padti hai**.  

---

### **💡 Conclusion**  
Strategy pattern **flexibility aur modular design ke liye best hai**, aur **run-time pe behavior change karne ka best solution provide karta hai**. 🚀
