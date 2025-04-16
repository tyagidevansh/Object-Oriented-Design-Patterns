# **Flyweight Pattern**

Flyweight design pattern ek **structural design pattern** hai jo **memory usage minimize karne ke liye objects share karta hai**. Is pattern ka use tab hota hai jab **bahut saare similar objects create karne hon** aur unme se repetitive data ya state ko share karke system ke overall memory consumption ko reduce karna ho. Does that sound familiar React devs?

➡ **Simple Words Me:**  
Assume aap ek **text editor** bana rahe ho jahan har letter ek object hai. Agar har letter ke liye ek naya object banaya jaaye, to system ki memory par bohot load aa jayega. **Flyweight pattern** se tum **common properties** (jaise font type, size, style) ko **share** kar sakte ho aur **unique properties** (jaise position ya character value) ko alag rakh sakte ho.

✅ **Solution:**  
   - **Intrinsic State:** Un properties ko share karo jo **har object me common ho**.  
   - **Extrinsic State:** Un properties ko alag se manage karo jo **object-specific ho**.  
   - Ek **Flyweight Factory** banao jo objects ko create karne aur share karne ke liye responsible ho.

➡ **Flyweight pattern se memory efficiency, performance aur scalability improve hoti hai.**

---

## **2️⃣ Kab Zaroorat Padti Hai?**  
Socho tumhare paas ek **graphical application** hai jahan **bohut saare similar shapes ya glyphs display kiye jaate hain**. Agar tum har ek shape ke liye alag object create karoge, to memory ka load bohut zyada ho jayega.

🔹 **Graphical User Interfaces:**  
   - Text editors, game objects, ya shapes jahan common properties share ki ja sakti hain.  
🔹 **Document Editors:**  
   - Har character ke liye ek object banane ki bajaye common properties (font, style) ko share karna.  

Agar tum **duplicate data** create karte ho bina share kiye, to system inefficient ho jata hai.

✅ **Flyweight Pattern ka Use:**  
   - **Intrinsic state share karna:** Data jo objects me common hai.  
   - **Extrinsic state separate rakho:** Data jo object ke specific details ko denote karta hai.

---

## **3️⃣ Flyweight Pattern ke Main Components**  
Flyweight pattern **3 primary components** se milkar banta hai:

1️⃣ **Flyweight Interface (Common Functionality)** 🧩  
   - Yeh interface define karta hai wo methods jo **flyweight objects implement karte hain**.

2️⃣ **Concrete Flyweight (Shared Object)** 🎯  
   - Yeh **actual shared object** hai jisme common (intrinsic) state stored hota hai.  
   - Example: Ek character object jisme font style ya type common ho.

3️⃣ **Flyweight Factory (Object Manager)** 🎛  
   - Yeh **objects create aur manage** karta hai, aur pehle se bante objects ko **reuse** karta hai.  
   - Agar koi object pehle se exist karta hai, to naya object create nahi hota, balki existing object return kiya jata hai.

---

## **4️⃣ UML Diagram & Code Example**

### **Class Diagram (Structure of Flyweight Pattern):**

```
┌─────────────────────────────┐
│         Client              │
│ (Uses flyweight objects)    │
└─────────────────────────────┘
            │
            ▼
 ┌─────────────────────────────┐
 │        Flyweight            │
 │  (Common Interface)         │
 └─────────────────────────────┘
            │
     ┌──────┼───────┐
     │              │
     ▼              ▼
┌────────────┐ ┌─────────────────────┐
│ Concrete   │ │ Flyweight Factory   │
│ Flyweight  │ └─────────────────────┘
└────────────┘
```

---

### **Python Code Example - Text Editor Glyphs** 📝

```python
from typing import Dict

# Step 1: Flyweight Interface
class Glyph:
    def render(self, position: tuple):
        raise NotImplementedError("This method should be overridden!")

# Step 2: Concrete Flyweight (Shared Object)
class CharacterGlyph(Glyph):
    def __init__(self, char: str, font: str, size: int):
        self.char = char               # Extrinsic state (unique identity)
        self.font = font               # Intrinsic state (shared)
        self.size = size               # Intrinsic state (shared)

    def render(self, position: tuple):
        # Render the character on the screen at the given position
        print(f"Rendering '{self.char}' in {self.font} at size {self.size} at position {position}")

# Step 3: Flyweight Factory (Manages Shared Objects)
class GlyphFactory:
    _glyphs: Dict[tuple, CharacterGlyph] = {}

    @classmethod
    def get_glyph(cls, char: str, font: str = "Arial", size: int = 12) -> CharacterGlyph:
        key = (char, font, size)
        if key not in cls._glyphs:
            # Create a new flyweight object if not available
            cls._glyphs[key] = CharacterGlyph(char, font, size)
            print(f"Created new glyph for {key}")
        else:
            print(f"Reusing existing glyph for {key}")
        return cls._glyphs[key]

# Step 4: Client Code (Using the Flyweight Pattern)
if __name__ == "__main__":
    # Simulate rendering a simple text
    text = "HELLO"
    positions = [(x * 10, 50) for x in range(len(text))]
    
    for char, pos in zip(text, positions):
        glyph = GlyphFactory.get_glyph(char, font="Arial", size=12)
        glyph.render(pos)

    # Demonstrating reuse: Asking for same glyph again
    duplicate_glyph = GlyphFactory.get_glyph("H", font="Arial", size=12)
    duplicate_glyph.render((0, 100))
```

✅ **Code Highlights:**  
   - **Memory Efficiency:** Common properties jaise font aur size ko share karte hue duplicate objects create nahi hote.  
   - **Intrinsic vs Extrinsic:** Character glyph me intrinsic state (font, size) shared hai, aur extrinsic state (position) runtime pe pass hota hai.  
   - **Flyweight Factory:** Ensures reuse of existing objects by checking key existence before creating a new one.

---

## **5️⃣ Real-World Examples** 🌍  

1️⃣ **Text Editors & Word Processors:**  
   - **Character rendering:** Har character ke liye shared glyph objects use karke memory optimize karna.  

2️⃣ **Graphical Applications:**  
   - **Icon Management:** Same icons ko bar bar create karne se bachna aur inhe share karna.  

3️⃣ **Game Development:**  
   - **Tiles or Sprites:** Similar visual elements ko share karke performance enhance karna.

4️⃣ **Web Applications:**  
   - **Caching Resources:** Common UI elements ko cache me rakhna aur reuse karna.

---

## **6️⃣ Limitations & Pitfalls** ⚠  

❌ **Increased Complexity in Implementation:**  
   - Flyweight pattern implement karte waqt **intrinsic aur extrinsic state ko clearly separate karna** padta hai, jo code complex bana sakta hai.

❌ **Over-optimization:**  
   - Har situation me flyweight use karna zaruri nahi; agar objects bahut simple hain to ye unnecessary abstraction ho sakta hai.

❌ **Thread Safety Issues:**  
   - Shared objects ko manage karte waqt **thread safety ka dhyaan rakhna zaruri hai**, khaaskar multi-threaded environments me.

---

## **7️⃣ Flyweight Pattern ke Software Design Principles** 🎯  

✔ **Memory Efficiency:**  
   - Unnecessary duplicate objects create nahi hote, jo overall performance ko improve karta hai.

✔ **Separation of Concerns:**  
   - **Intrinsic state share karna aur extrinsic state ko client se manage karwana.**

✔ **Open/Closed Principle (OCP):**  
   - Existing flyweight objects me changes kiye bina naye objects add karna asaan hota hai.

✔ **Single Responsibility Principle (SRP):**  
   - Flyweight object ka sirf ek hi responsibility hota hai: common state ko represent karna.

---

## **🔹 Flyweight Pattern Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - Flyweight pattern **memory efficiency** ke liye shared objects ka use karta hai jisme common properties hoti hain.

2️⃣ **Kab Use Karte Hain?**  
   - Jab bahut saare similar objects create hon aur unme se repetitive state ko share karna ho.

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Intrinsic state share karo, extrinsic state client se manage karo, aur factory object reuse ko ensure karti hai.**

4️⃣ **Real-World Examples:**  
   - **Text Editors, Graphical Interfaces, Game Development, Resource Caching.**

5️⃣ **Fayde & Limitations:**  
   ✔ **Memory aur performance optimization hota hai.**  
   ❌ **Implementation complexity aur thread safety challenges ho sakte hain.**

---

### **💡 Conclusion**  
Flyweight pattern **efficient memory utilization aur performance improvement** ko achieve karta hai by sharing common object states. Isse code modular, scalable aur optimized rehta hai, jab aapko bohut saare similar objects create karne padte hain. 🚀