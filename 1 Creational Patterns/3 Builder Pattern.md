# Builder Design Pattern

Builder Pattern ek **creational design pattern** hai jo **complex objects ko step-by-step construct** karne ki facility deta hai **without directly exposing their construction logic**.  

✔ **Matlab:**  
   - Agar ek object **bohot saari configurations aur variations** ke saath create hota hai, to **builder pattern usko systematically construct karta hai** bina unnecessary complexity ke.  
   - **Method chaining** ka use hota hai taaki code readable aur maintainable rahe.  

---

## **2️⃣ Kab Zaroorat Padti Hai? (Motivation & Real-Life Example)**  

1️⃣ **Jab ek object ka multiple variations ke saath construction ho.**  
2️⃣ **Jab object ka initialization bohot complex ho.**  
3️⃣ **Jab same class ke multiple variations kaafi confusing ho.**  

➡ **Example:**  

🍔 **McDonald's Burger Builder**  
   - Ek burger ke multiple customization hote hain:  
     - **Cheese chahiye ya nahi?**  
     - **Lettuce add karna hai ya nahi?**  
     - **Veg ya Non-Veg?**  
     - **Extra Sauce chahiye ya nahi?**  
   - **Agar normal constructor use karein, to constructor bohot overloaded ho jayega.**  
   - **Builder pattern ka use karke, step-by-step customized burger bana sakte hain.**  

---

## **3️⃣ Builder Pattern ka Structure & Components**  

Builder Pattern **4 main components** se bana hota hai:  

1️⃣ **Product (Complex Object to be built)**  
   - Jo object banana hai, jaise `Burger` ya `Car`.  

2️⃣ **Builder Interface**  
   - Object build karne ke liye necessary methods define karta hai.  

3️⃣ **Concrete Builder**  
   - Jo actual step-by-step object construction karta hai.  

4️⃣ **Director (Optional but recommended)**  
   - **Builder ke sequence ko define karta hai taaki ek specific type ka object ban sake.**  

---

## **4️⃣ UML Diagram & Code Example**  

### **Class Diagram (Builder Pattern Structure)**  

```
┌──────────────────────────────┐
│        Product               │
│ ──────────────────────────── │
│ - attributes                 │
│ + show()                     │
└──────────────────────────────┘
         ▲
         │
┌──────────────────────────────┐
│       Builder Interface      │
│ ──────────────────────────── │
│ + setPartA()                 │
│ + setPartB()                 │
│ + getResult()                 │
└──────────────────────────────┘
         ▲
         │
┌──────────────────────────────┐
│    Concrete Builder          │
│ ──────────────────────────── │
│ + setPartA()                 │
│ + setPartB()                 │
│ + getResult()                 │
└──────────────────────────────┘
         ▲
         │
┌──────────────────────────────┐
│        Director              │
│ ──────────────────────────── │
│ + construct()                 │
└──────────────────────────────┘
```

---

### **Python Code Example - Builder Pattern**  

```python
# Step 1: Product (Complex Object)
class Burger:
    def __init__(self):
        self.ingredients = []

    def add_ingredient(self, ingredient):
        self.ingredients.append(ingredient)

    def show(self):
        print(f"Burger with: {', '.join(self.ingredients)}")

# Step 2: Builder Interface
class BurgerBuilder:
    def add_bun(self): pass
    def add_patty(self): pass
    def add_cheese(self): pass
    def add_lettuce(self): pass
    def get_burger(self): pass

# Step 3: Concrete Builder
class VegBurgerBuilder(BurgerBuilder):
    def __init__(self):
        self.burger = Burger()

    def add_bun(self):
        self.burger.add_ingredient("Whole Wheat Bun")
        return self  # Method chaining

    def add_patty(self):
        self.burger.add_ingredient("Veg Patty")
        return self

    def add_cheese(self):
        self.burger.add_ingredient("Cheese")
        return self

    def add_lettuce(self):
        self.burger.add_ingredient("Lettuce")
        return self

    def get_burger(self):
        return self.burger

# Step 4: Director (Controls the order of steps)
class BurgerDirector:
    def construct_veg_burger(self, builder):
        return builder.add_bun().add_patty().add_cheese().add_lettuce().get_burger()

# Client Code
builder = VegBurgerBuilder()
director = BurgerDirector()

veg_burger = director.construct_veg_burger(builder)
veg_burger.show()

# Output:
# Burger with: Whole Wheat Bun, Veg Patty, Cheese, Lettuce
```

✔ **Explanation:**  
   - **`Burger`** class complex object hai jo **builder ke through step-by-step construct ho raha hai.**  
   - **`BurgerBuilder` (interface)** defines karti hai ki kaunse steps lagenge burger banane me.  
   - **`VegBurgerBuilder` (Concrete Builder)** step-by-step methods ko implement karta hai.  
   - **`BurgerDirector`** ye decide karta hai ki kaunse steps kis sequence me hone chahiye.  

---

## **5️⃣ Method Chaining (Fluent Interface) - Builder ka Best Feature**  

Builder pattern ka **sabse bada advantage method chaining hota hai**:  

```python
builder.add_bun().add_patty().add_cheese().get_burger()
```

✔ **Iska fayda kya hai?**  
   - **Readable aur maintainable code**  
   - **Multiple options ko easily customize kar sakte hain**  
   - **Har variation ke liye separate overloaded constructors ki zaroorat nahi hoti**  

---

## **6️⃣ Real-World Examples of Builder Pattern** 🌍  

1️⃣ **SQL Query Builders**  
   - `SELECT * FROM users WHERE age > 20 ORDER BY name`  
   - Builder pattern **SQL queries ko dynamically construct karne me help karta hai.**  

2️⃣ **Document Builders (PDF, HTML, XML)**  
   - Agar ek **complex PDF ya HTML page generate karna ho** to builder use kar sakte hain.  

3️⃣ **Car Configurator (Tesla, BMW)**  
   - **Car customization website** builder pattern use karti hai, jisme tum **engine type, color, wheels, interior, etc. choose kar sakte ho.**  

4️⃣ **UI Component Builders (Android, Flutter, React)**  
   - UI components kaafi **dynamic hote hain, isliye builder pattern unko configure karne me help karta hai.**  

---

## **7️⃣ Builder Pattern ke Fayde & Limitations** ⚠  

### **✅ Fayde (Advantages):**  
✔ **Complex object creation ko manageable banata hai.**  
✔ **Multiple variations easily implement ho sakti hain.**  
✔ **Code readable aur maintainable hota hai.**  
✔ **Method chaining se concise aur clear syntax milta hai.**  

---

### **❌ Limitations (Disadvantages):**  
❌ **Zyada chhoti objects ke liye overkill ho sakta hai.**  
❌ **Extra classes create karni padti hain (Director, Builder, Concrete Builder).**  
❌ **Implementation thoda complex ho sakta hai compared to Factory Pattern.**  

---

## **8️⃣ Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - **Step-by-step complex object construction ko manage karta hai.**  

2️⃣ **Kab Use Karte Hain?**  
   - Jab **ek object ke bohot saare configurations aur variations ho.**  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Builder Interface + Concrete Builder + Director** use hota hai.  

4️⃣ **Real-World Examples:**  
   - **Burger Customization, SQL Queries, Car Configurators, Document Builders.**  

5️⃣ **Fayde & Limitations:**  
   ✔ **Readable, Maintainable, Customizable**  
   ❌ **Extra classes ki zaroorat, thoda complex implementation**  

---

## **🔹 Conclusion**  
Builder Pattern **complex object creation ko easy aur flexible banata hai**, especially jab multiple configurations ki zaroorat ho. 🚀
