# **Decorator Pattern**  
Decorator ek **structural design pattern** hai jo **existing objects ki functionality ko dynamically modify** karta hai bina uska actual structure change kiye. Yeh **wrapper class** ki tarah kaam karta hai jo **extra behavior add karta hai** bina inheritance use kiye.  

➡ **Simple Words Me:**  
Socho tumhari **chai normal hai**, lekin tum usme **extra elaichi ya adrak** dalna chahte ho bina chai ki original recipe badle. Tumne **chai ko modify kar diya bina uska base change kiye**. Isi tarah, **Decorator pattern objects ke behavior ko runtime pe dynamically modify kar sakta hai**.  

---

#### **2️⃣ Kab Zaroorat Padti Hai? (Motivation)**  
Maan lo ek **Coffee shop ka software system** hai jisme tumhari ek **Simple Coffee class** hai. Ab naya feature add karna hai:  

- **Milk add karna**  
- **Sugar add karna**  
- **Chocolate syrup ya Whipped Cream add karna**  

Yeh sab **extra features** har coffee ke liye **optional** hone chahiye.  

➡ **Possible Solutions:**  

❌ **Inheritance Use Karna:**  
   - `SimpleCoffee`, `MilkCoffee`, `SugarCoffee`, `ChocolateCoffee`, `MilkSugarCoffee` jaise multiple classes banani padengi.  
   - **Class explosion ho jayega** (bahut saari unnecessary subclasses ban jayengi).  
   - Har naye feature ke liye **nayi class banani padegi**, jo **scalability ko reduce karega**.  

✅ **Decorator Pattern Use Karna:**  
   - Ek **wrapper class (Decorator)** banayenge jo **coffee ka behavior modify karega** bina original class ko modify kiye.  
   - **Multiple decorators ko combine kar sakte hain**, jaise `MilkDecorator + SugarDecorator + ChocolateDecorator`.  
   - **Code flexible aur maintainable rahega**.  

---

#### **3️⃣ Decorator Pattern ke Main Components**  
Decorator pattern **4 major components** se bana hota hai:  

1️⃣ **Component (Interface or Abstract Class)** 🎯  
   - Yeh wo **base class** hai jo **core object** define karti hai.  
   - Example: `Coffee` interface  

2️⃣ **Concrete Component (Original Object)** ☕  
   - Yeh **original class** hai jo sabse basic functionality implement karti hai.  
   - Example: `SimpleCoffee` class jo ek normal coffee banati hai.  

3️⃣ **Decorator (Abstract Wrapper Class)** 🧩  
   - Yeh **Component ko extend ya implement karta hai** aur **original object ko wrap karta hai**.  
   - Yeh **core functionality ko preserve karta hai aur extra behavior add karta hai**.  

4️⃣ **Concrete Decorators (Extra Features)** 🍫  
   - Yeh **actual decorators** hain jo **new behavior add karte hain**, jaise `MilkDecorator`, `SugarDecorator`, `ChocolateDecorator`.  

---

#### **4️⃣ UML Diagram & Code Example**  

**Class Diagram (Structure of Decorator Pattern):**  

```
┌────────────────────┐
│    Coffee (Interface)    │
└────────────────────┘
          ▲
          │
┌────────────────────┐
│  SimpleCoffee (Concrete)  │
└────────────────────┘
          ▲
          │
┌────────────────────┐
│  CoffeeDecorator (Abstract) │
└────────────────────┘
          ▲
          │
┌────────────────────┬────────────────────┐
│ MilkDecorator │ SugarDecorator │
└────────────────────┴────────────────────┘
```

---

### **Python Code Example** 📝  
```python
# Step 1: Base Component (Coffee Interface)
from abc import ABC, abstractmethod

class Coffee(ABC):
    @abstractmethod
    def cost(self) -> int:
        pass

    @abstractmethod
    def description(self) -> str:
        pass

# Step 2: Concrete Component (Simple Coffee)
class SimpleCoffee(Coffee):
    def cost(self) -> int:
        return 50  # Basic coffee cost

    def description(self) -> str:
        return "Simple Coffee"

# Step 3: Abstract Decorator (Wrapper)
class CoffeeDecorator(Coffee, ABC):
    def __init__(self, coffee: Coffee):
        self._coffee = coffee

    def cost(self) -> int:
        return self._coffee.cost()  # Calling wrapped object’s cost()

    def description(self) -> str:
        return self._coffee.description()  # Calling wrapped object’s description()

# Step 4: Concrete Decorators
class MilkDecorator(CoffeeDecorator):
    def cost(self) -> int:
        return self._coffee.cost() + 20  # Adding milk cost

    def description(self) -> str:
        return self._coffee.description() + ", Milk"

class SugarDecorator(CoffeeDecorator):
    def cost(self) -> int:
        return self._coffee.cost() + 10  # Adding sugar cost

    def description(self) -> str:
        return self._coffee.description() + ", Sugar"

class ChocolateDecorator(CoffeeDecorator):
    def cost(self) -> int:
        return self._coffee.cost() + 30  # Adding chocolate cost

    def description(self) -> str:
        return self._coffee.description() + ", Chocolate"

# Step 5: Client Code
coffee = SimpleCoffee()
print(f"{coffee.description()} : ₹{coffee.cost()}")  # Output: Simple Coffee : ₹50

milk_coffee = MilkDecorator(coffee)
print(f"{milk_coffee.description()} : ₹{milk_coffee.cost()}")  # Output: Simple Coffee, Milk : ₹70

sugar_milk_coffee = SugarDecorator(milk_coffee)
print(f"{sugar_milk_coffee.description()} : ₹{sugar_milk_coffee.cost()}")  # Output: Simple Coffee, Milk, Sugar : ₹80
```
✅ **Yeh code ensure karta hai ki hum naya behavior dynamically add kar sakein bina original class ko modify kiye.**  

---

#### **5️⃣ Real-World Example** 🌍  

1️⃣ **Text Formatting in Text Editors:**  
   - Ek **basic text editor** me bold, italic, underline **dynamically apply karne ke liye Decorator use hota hai**.  
   - `BoldDecorator`, `ItalicDecorator`, `UnderlineDecorator` **text ko modify karte hain** bina base class change kiye.  

2️⃣ **Cloud Services (AWS, GCP, Azure):**  
   - Cloud services **basic instance (VM) provide karti hain**, aur extra features **(Auto Scaling, Security, Monitoring)** as **add-ons** milte hain.  

3️⃣ **File Stream Operations:**  
   - Java/Python me file streams me **buffering, encryption, compression** jise operations **Decorator pattern se implement hote hain**.  

---

#### **6️⃣ Limitations & Pitfalls** ⚠  
Decorator pattern powerful hai, but kuch limitations bhi hain:  

❌ **Complexity Badhta Hai**  
   - Multiple decorators hone se **code structure complex ho sakta hai**.  
   - Debugging tough ho jata hai, kyunki **multiple layers of decorators** hone se actual execution trace karna mushkil ho sakta hai.  

❌ **Multiple Objects Banane Padte Hain**  
   - Har naye feature ke liye **naya decorator class likhna padta hai**, jo overhead badha sakta hai.  

---

#### **7️⃣ Decorator Pattern ke Software Design Principles** 🎯  

✔ **Open/Closed Principle (OCP)**  
   - **Naye features add kar sakte hain bina purane code modify kiye**.  

✔ **Single Responsibility Principle (SRP)**  
   - Har decorator sirf **ek specific modification handle karta hai**.  

✔ **Loose Coupling**  
   - Decorator **original object se tightly coupled nahi hota**, jo **flexibility badhata hai**.  

---

### **🔹 Decorator Pattern Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - Decorator **existing objects ka behavior modify karta hai bina inheritance use kiye**.  

2️⃣ **Kab Use Karte Hain?**  
   - Jab **features dynamically add karne ho bina base class modify kiye**.  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Decorator wrapper ka kaam karta hai jo object ki functionality enhance karta hai**.  

4️⃣ **Real-World Examples:**  
   - **Text Formatting, Cloud Services, File Streams, Coffee Customization**.  

5️⃣ **Fayde & Limitations:**  
   ✔ **Flexibility aur maintainability badhata hai**.  
   ❌ **Multiple layers hone se complexity increase hoti hai**.  

---

### **💡 Conclusion**  
Decorator pattern ek **powerful solution hai jab hume existing objects ko modify karna ho bina inheritance use kiye**. Yeh **code maintainability aur scalability improve karta hai**, lekin **overuse se complexity badh sakti hai**. 🚀
