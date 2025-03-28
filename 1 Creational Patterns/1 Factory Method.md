# **Factory Method Pattern 
Factory Method ek **creational design pattern** hai jo **objects create karne ka ek systematic aur reusable tarika provide karta hai** bina directly `new` keyword use kiye.  

✔ **Instead of direct object creation, hum ek "factory" class use karte hain jo decide karti hai ki kaunsa object return karna hai.**  

➡ **Simple Words Me:**  
Tum ek **restaurant** chalate ho jisme alag-alag types ke **pizzas** bante hain:  

✅ **Cheese Pizza** 🧀  
✅ **Veggie Pizza** 🥦  
✅ **Pepperoni Pizza** 🍕  

❌ **Without Factory Pattern (Bad Approach):**  
   - Har baar `new CheesePizza()`, `new VeggiePizza()` likhna padega, jo **tight coupling** aur **code duplication** create karega.  

✅ **With Factory Pattern (Good Approach):**  
   - **Ek Pizza Factory class** bana lo jo **correct type ka pizza return karegi**, to **code maintainable aur reusable** ho jayega.  

---

## **2️⃣ Kab Zaroorat Padti Hai? (Motivation & Real-Life Example)**  

1️⃣ **Jab object creation complex ho aur har baar `new` keyword likhna inefficient ho.**  
2️⃣ **Jab ek common interface ya superclass se multiple types ke objects create karne ho.**  
3️⃣ **Jab ek centralized object creation approach chahiye jo maintainable ho.**  

➡ **Example:**  
Tum **"Car Manufacturing System"** bana rahe ho jisme alag-alag types ki **cars** ban rahi hain:  

🚗 **SedanCar**  
🚙 **SUVCar**  
🏎 **SportsCar**  

✔ **Instead of `new SedanCar()`, `new SUVCar()`, ek `CarFactory` bana lo jo `createCar(type)` method se correct car return karegi.**  

---

## **3️⃣ Factory Method Pattern ke Main Components**  

Factory Method **4 components** se bana hota hai:  

1️⃣ **Product (Interface ya Abstract Class)**  
   - **Ye ek common interface provide karta hai jo har object implement karega.**  

2️⃣ **Concrete Products (Actual Objects)**  
   - **Ye real implementations hain jo factory create karega.**  

3️⃣ **Creator (Factory Class)**  
   - **Ye ek class hoti hai jo objects create karti hai aur ek common interface return karti hai.**  

4️⃣ **Client (User Code)**  
   - **Jo Factory ko call karta hai aur object use karta hai.**  

---

## **4️⃣ UML Diagram & Code Example**  

### **Class Diagram (Structure of Factory Pattern)**  

```
┌─────────────────────────────┐
│         Car (Interface)     │
│ ─────────────────────────── │
│ + manufacture()             │
└─────────────────────────────┘
            ▲
            │
 ┌─────────┼──────────┐
 │         │          │
 ▼         ▼          ▼
┌──────────┐  ┌──────────┐  ┌──────────┐
│ SedanCar │  │ SUVCar   │  │ SportsCar│
│          │  │          │  │          │
└──────────┘  └──────────┘  └──────────┘
            ▲
            │
┌─────────────────────────────┐
│        CarFactory           │
│ ─────────────────────────── │
│ + create_car(type)          │
└─────────────────────────────┘
```

---

### **Python Code Example - Car Factory 🚗**  

```python
# Step 1: Product Interface
from abc import ABC, abstractmethod

class Car(ABC):
    @abstractmethod
    def manufacture(self):
        pass

# Step 2: Concrete Products
class SedanCar(Car):
    def manufacture(self):
        return "🚗 Sedan Car is being manufactured!"

class SUVCar(Car):
    def manufacture(self):
        return "🚙 SUV Car is being manufactured!"

class SportsCar(Car):
    def manufacture(self):
        return "🏎 Sports Car is being manufactured!"

# Step 3: Factory Class
class CarFactory:
    @staticmethod
    def create_car(car_type):
        if car_type == "sedan":
            return SedanCar()
        elif car_type == "suv":
            return SUVCar()
        elif car_type == "sports":
            return SportsCar()
        else:
            raise ValueError("Invalid car type!")

# Step 4: Client Code
if __name__ == "__main__":
    factory = CarFactory()

    sedan = factory.create_car("sedan")
    print(sedan.manufacture())  # 🚗 Sedan Car is being manufactured!

    suv = factory.create_car("suv")
    print(suv.manufacture())  # 🚙 SUV Car is being manufactured!

    sports = factory.create_car("sports")
    print(sports.manufacture())  # 🏎 Sports Car is being manufactured!
```

✅ **Output:**  
```
🚗 Sedan Car is being manufactured!
🚙 SUV Car is being manufactured!
🏎 Sports Car is being manufactured!
```

✅ **Factory Method ka use karke har baar `new` keyword likhne ki zaroorat nahi, sirf `CarFactory.create_car()` call karna hai!**  

---

## **5️⃣ Real-World Examples of Factory Pattern** 🌍  

1️⃣ **Database Connections**  
   - **Jab tum MySQL, PostgreSQL, ya SQLite ka connection create karte ho, ek factory decide karti hai ki kaunsa driver load hoga.**  

2️⃣ **Logger System (Debug, Info, Error Logs)**  
   - **Factory method dynamically correct logger return karta hai.**  

3️⃣ **Payment Gateways (PayPal, Stripe, Razorpay)**  
   - **Factory pattern se automatically correct payment provider ka object create hota hai.**  

4️⃣ **UI Components in Frameworks**  
   - **React/Angular me Button, InputField, Checkbox sab ek factory pattern se create hote hain.**  

5️⃣ **Car Manufacturing Plants 🚗**  
   - **Factory pattern real-world automobile industry me bhi kaafi use hota hai!**  

---

## **6️⃣ Limitations & Pitfalls** ⚠  

❌ **Complexity Increase:**  
   - **Chhoti applications me unnecessary complexity create ho sakti hai.**  

❌ **Subclass Explosion:**  
   - **Har naye product ke liye ek naya class likhna padta hai.**  

❌ **Factory Dependency:**  
   - **Agar factory class me kuch issue ho gaya to pura system impact ho sakta hai.**  

---

## **7️⃣ Factory Method ke Software Design Principles** 🎯  

✔ **Encapsulation:**  
   - **Object creation logic factory class me encapsulated hota hai.**  

✔ **Open/Closed Principle (OCP):**  
   - **Naye object types ko easily add kiya ja sakta hai bina existing code modify kiye.**  

✔ **Single Responsibility Principle (SRP):**  
   - **Factory ka kaam sirf object create karna hai, uska kaam alag se handle nahi karna.**  

✔ **Loose Coupling:**  
   - **Client code aur object creation tightly coupled nahi hote.**  

---

## **🔹 Factory Method Pattern Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - **Factory method ek creational pattern hai jo objects create karne ke process ko encapsulate karta hai.**  

2️⃣ **Kab Use Karte Hain?**  
   - **Jab multiple types ke objects create karne ho bina `new` keyword use kiye.**  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Common Interface + Concrete Products + Factory Class.**  

4️⃣ **Real-World Examples:**  
   - **Database Connections, Payment Gateways, Logging Systems, UI Components, Car Manufacturing.**  

5️⃣ **Fayde & Limitations:**  
   ✔ **Code reusability aur flexibility badhta hai.**  
   ❌ **Extra complexity aur subclassing ki zaroorat pad sakti hai.**  

---

### **💡 Conclusion**  
Factory Method Pattern **object creation ko easy aur reusable banata hai**, jo **large-scale applications** me kaafi useful hota hai. 🚀
