# Prototype Design Pattern

## **1️⃣ Prototype Pattern Kya Hai?**  

Prototype Pattern ek **Creational Design Pattern** hai jo **existing objects ka duplicate banane** me help karta hai **bina naye object ko scratch se banaye**. Is pattern me ek object ko clone karke **naya object create** kiya jata hai, jo **memory efficient aur fast hota hai**.  

✔ **Matlab:**  
   - Agar **same object ko baar-baar instantiate karna expensive ya slow ho**, to **prototype pattern uska clone create karta hai** taaki performance improve ho.  
   - **Deep Copy aur Shallow Copy ka concept important hai yaha.**  

---

## **2️⃣ Kab Zaroorat Padti Hai? (Motivation & Real-Life Example)**  

1️⃣ **Jab ek object ka creation expensive ho (Database, API Calls, Complex Calculations)**  
2️⃣ **Jab ek object ka structure predefined ho aur baar-baar same cheezein initialize na karni pade**  
3️⃣ **Jab dynamically objects create karne ho bina `new` keyword ka baar-baar use kiye**  

➡ **Example:**  

🖼 **Image Editing Software - Photoshop Clone Feature**  
   - **Photoshop ya Canva me agar ek object (like shape, text, sticker) ko duplicate karna ho**, to **naya object scratch se create karne ki jagah, clone create hota hai**.  
   - **Isse performance improve hoti hai aur time bachta hai.**  

🎮 **Video Games - Character Cloning**  
   - **Agar ek game me enemy characters ka same model hai**, to **har baar naye object create karne se memory waste hoti hai**.  
   - **Prototype pattern ka use karke existing enemy ka clone create kar sakte hain.**  

---

## **3️⃣ Prototype Pattern ka Structure & Components**  

Prototype Pattern **3 main components** se bana hota hai:  

1️⃣ **Prototype Interface**  
   - **clone()** method define karta hai jo **object copy karta hai**.  

2️⃣ **Concrete Prototype (Actual Object)**  
   - Jo **prototype se clone hone wala object hai**.  

3️⃣ **Client**  
   - **Prototype ke clone() method ka use karke naye objects create karta hai**.  

---

## **4️⃣ UML Diagram & Code Example**  

### **Class Diagram (Prototype Pattern Structure)**  

```
┌──────────────────────────────┐
│        Prototype             │
│ ──────────────────────────── │
│ + clone()                    │
└──────────────────────────────┘
         ▲
         │
┌──────────────────────────────┐
│    Concrete Prototype        │
│ ──────────────────────────── │
│ + clone()                    │
└──────────────────────────────┘
         ▲
         │
┌──────────────────────────────┐
│        Client                │
│ ──────────────────────────── │
│ + createClone()              │
└──────────────────────────────┘
```

---

### **Python Code Example - Prototype Pattern**  

```python
import copy

# Step 1: Prototype Interface
class Prototype:
    def clone(self):
        pass

# Step 2: Concrete Prototype
class Car(Prototype):
    def __init__(self, brand, model, features):
        self.brand = brand
        self.model = model
        self.features = features  # List of features

    def show_details(self):
        print(f"Car: {self.brand} {self.model}, Features: {', '.join(self.features)}")

    # Clone method (Deep Copy)
    def clone(self):
        return copy.deepcopy(self)

# Step 3: Client Code
car1 = Car("Tesla", "Model S", ["Autopilot", "Electric", "Sunroof"])
car1.show_details()

# Cloning car1
car2 = car1.clone()
car2.features.append("Self-Driving Mode")  # Modify the cloned object

# Displaying both objects
print("\nAfter Cloning:")
car1.show_details()
car2.show_details()
```

### **Output:**
```
Car: Tesla Model S, Features: Autopilot, Electric, Sunroof

After Cloning:
Car: Tesla Model S, Features: Autopilot, Electric, Sunroof
Car: Tesla Model S, Features: Autopilot, Electric, Sunroof, Self-Driving Mode
```

✔ **Explanation:**  
   - **Car class ek prototype hai jo `clone()` method implement karta hai.**  
   - **Shallow Copy me agar koi mutable object (list) ho, to clone aur original dono me change hoga.**  
   - **Deep Copy ensure karta hai ki cloned object bilkul independent ho.**  

---

## **5️⃣ Deep Copy vs Shallow Copy - Prototype Pattern me Important Concept**  

### **Shallow Copy (Surface-Level Clone - `copy.copy()`)**
   - **Original aur Cloned object share karte hain same reference for mutable objects.**
   - **Agar ek object change hota hai, to dusra bhi change ho jata hai.**  

```python
import copy

car1 = Car("Tesla", "Model X", ["Autopilot", "Electric"])
car2 = copy.copy(car1)  # Shallow Copy

car2.features.append("Sunroof")  # Changing cloned object's list

car1.show_details()  # Original also gets affected
car2.show_details()
```

### **Deep Copy (Completely Independent Clone - `copy.deepcopy()`)**
   - **Original aur Cloned object completely independent hote hain.**
   - **Agar ek change hota hai, dusre me koi effect nahi hota.**  

```python
car3 = copy.deepcopy(car1)  # Deep Copy
car3.features.append("Self-Driving Mode")

car1.show_details()  # No effect on original
car3.show_details()
```

---

## **6️⃣ Real-World Examples of Prototype Pattern** 🌍  

1️⃣ **Operating Systems - File System Cloning**  
   - Jab ek file ka duplicate banta hai, OS **Prototype Pattern ka use karke fast copy create karta hai.**  

2️⃣ **Game Development - Object Cloning**  
   - Ek hi type ke bohot saare enemies ya objects ko fast load karne ke liye.  

3️⃣ **Machine Learning - Model Copying**  
   - ML Models ko train karne ke baad unka **prototype clone kiya jata hai taaki multiple variations test kiye ja sakein.**  

4️⃣ **Database Record Duplication**  
   - **Database me agar ek record ka duplicate banana ho** (audit logging ya backups ke liye), to **prototype pattern ka use hota hai.**  

---

## **7️⃣ Prototype Pattern ke Fayde & Limitations** ⚠  

### **✅ Fayde (Advantages):**  
✔ **Performance Improvement:** Object create karne ka time bachta hai.  
✔ **Memory Efficient:** Same object ko baar-baar instantiate karne ki zaroorat nahi hoti.  
✔ **Encapsulation:** Object creation logic ko hide karta hai.  
✔ **Customization Possible:** Clone ke baad object ko modify kar sakte hain.  

---

### **❌ Limitations (Disadvantages):**  
❌ **Deep Copy aur Shallow Copy ka difference samajhna zaroori hai.**  
❌ **Agar object bohot complex hai, to deep copy costly ho sakti hai.**  
❌ **Mutable aur Immutable objects handle karne me dikkat ho sakti hai.**  

---

## **8️⃣ Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - **Ek existing object ka fast duplicate create karna without new object creation.**  

2️⃣ **Kab Use Karte Hain?**  
   - **Jab object creation slow ya expensive ho (DB calls, APIs, Complex Computation).**  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Prototype Interface + Concrete Prototype + Client**  

4️⃣ **Real-World Examples:**  
   - **Photoshop Cloning, Video Game Enemy Spawning, ML Model Duplication.**  

5️⃣ **Fayde & Limitations:**  
   ✔ **Fast, Memory Efficient, Encapsulated Object Creation**  
   ❌ **Deep Copy vs Shallow Copy ka dhyan rakhna zaroori hai.**  

---

## **🔹 Conclusion**  
Prototype Pattern **fast aur memory-efficient object creation ka best solution hai**, especially jab **object expensive ya complex ho**. 🚀
