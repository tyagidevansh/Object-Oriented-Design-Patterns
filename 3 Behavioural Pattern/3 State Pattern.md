# **State Pattern**  
State Pattern ek **behavioral design pattern** hai jo **ek object ke internal state ko dynamically change karne aur uske behavior ko modify karne ka tarika provide karta hai**.  

➡ **Simple Words Me:**  
Maan lo **tum ek vending machine bana rahe ho**, jo **alag-alag states** me kaam karti hai:  

✅ **No Coin Inserted** – Machine idle hai  
✅ **Coin Inserted** – Machine ready hai  
✅ **Dispensing Item** – Item nikal raha hai  
✅ **Out of Stock** – Koi item available nahi hai  

✔ **State Pattern ka use karke hum vending machine ka behavior dynamically change kar sakte hain bina complex if-else statements likhe.**  

---

## **2️⃣ Kab Zaroorat Padti Hai? (Motivation & Real-Life Example)**  
Maan lo tum ek **Media Player Application** bana rahe ho jo **3 states me kaam karta hai**:  

🔹 **Playing State** 🎵  
🔹 **Paused State** ⏸  
🔹 **Stopped State** ⏹  

❌ **Without State Pattern (Bad Approach):**  
   - Har function me multiple **if-else conditions likhni padengi**, jo code ko **messy aur hard to maintain** bana degi.  

✅ **With State Pattern (Good Approach):**  
   - **Har state ka ek alag class hoga**, aur **state change hone par behavior automatically update ho jayega.**  

---

## **3️⃣ State Pattern ke Main Components**  

State pattern **3 major components** se bana hota hai:  

1️⃣ **Context (Main Object) 🎛**  
   - **Ye ek class hoti hai jo current state ko track karti hai.**  
   - **State transition manage karta hai (e.g., Playing → Paused).**  

2️⃣ **State Interface 📜**  
   - **Ye ek common interface provide karta hai jo saari states implement karti hain.**  

3️⃣ **Concrete States (State Implementations) 🛠**  
   - **Ye real states hoti hain jo object ke behavior ko define karti hain.**  

---

## **4️⃣ UML Diagram & Code Example**  

### **Class Diagram (Structure of State Pattern):**  

```
┌───────────────────────┐
│       Context        │
│ (Media Player)       │
│ state               │
│ setState(state)     │
│ pressPlay()         │
│ pressPause()        │
│ pressStop()         │
└───────────────────────┘
            ▲
            │
 ┌─────────┼──────────┐
 │         │          │
 ▼         ▼          ▼
┌──────────┐  ┌──────────┐  ┌──────────┐
│ Playing  │  │ Paused   │  │ Stopped  │
│ State    │  │ State    │  │ State    │
└──────────┘  └──────────┘  └──────────┘
```

---

### **Python Code Example - Media Player 🎵**  

```python
# Step 1: State Interface
from abc import ABC, abstractmethod

class State(ABC):
    @abstractmethod
    def press_play(self, player):
        pass

    @abstractmethod
    def press_pause(self, player):
        pass

    @abstractmethod
    def press_stop(self, player):
        pass

# Step 2: Concrete States
class PlayingState(State):
    def press_play(self, player):
        print("🎵 Already playing.")

    def press_pause(self, player):
        print("⏸ Pausing playback.")
        player.set_state(PausedState())

    def press_stop(self, player):
        print("⏹ Stopping playback.")
        player.set_state(StoppedState())

class PausedState(State):
    def press_play(self, player):
        print("▶ Resuming playback.")
        player.set_state(PlayingState())

    def press_pause(self, player):
        print("⏸ Already paused.")

    def press_stop(self, player):
        print("⏹ Stopping playback.")
        player.set_state(StoppedState())

class StoppedState(State):
    def press_play(self, player):
        print("▶ Starting playback.")
        player.set_state(PlayingState())

    def press_pause(self, player):
        print("⚠ Can't pause, media is already stopped.")

    def press_stop(self, player):
        print("⏹ Already stopped.")

# Step 3: Context Class
class MediaPlayer:
    def __init__(self):
        self.state = StoppedState()  # Default state

    def set_state(self, state):
        self.state = state

    def press_play(self):
        self.state.press_play(self)

    def press_pause(self):
        self.state.press_pause(self)

    def press_stop(self):
        self.state.press_stop(self)

# Step 4: Client Code
if __name__ == "__main__":
    player = MediaPlayer()

    player.press_play()   # ▶ Starting playback.
    player.press_pause()  # ⏸ Pausing playback.
    player.press_play()   # ▶ Resuming playback.
    player.press_stop()   # ⏹ Stopping playback.
    player.press_pause()  # ⚠ Can't pause, media is already stopped.
```

✅ **Output:**  
```
▶ Starting playback.
⏸ Pausing playback.
▶ Resuming playback.
⏹ Stopping playback.
⚠ Can't pause, media is already stopped.
```

✅ **Ab har state ka behavior alag class handle kar raha hai, bina kisi complex if-else conditions ke!**  

---

## **5️⃣ Real-World Examples** 🌍  

1️⃣ **Media Player (Play, Pause, Stop)** 🎵  
   - **Jab tum YouTube ya Spotify pe song play karte ho, pause ya stop karne se state change hoti hai.**  

2️⃣ **Traffic Light System 🚦**  
   - **Red Light → Green Light → Yellow Light → Red Light** (States automatically change hote hain).  

3️⃣ **ATMs (Insert Card, Enter PIN, Withdraw Money, Remove Card)** 🏧  
   - **Har action ke baad ATM ka state change hota hai.**  

4️⃣ **Order Processing in E-commerce 🛒**  
   - **Order Placed → Shipped → Out for Delivery → Delivered**.  

5️⃣ **Document Editor (Editing, Saving, Read-Only Mode) 📄**  
   - **MS Word me document read-only mode me hota hai jab tumhare paas editing permissions nahi hoti.**  

---

## **6️⃣ Limitations & Pitfalls** ⚠  

❌ **State Explosion:**  
   - **Bohot saari states hone par har state ka alag class banana complex ho sakta hai.**  

❌ **Increased Complexity:**  
   - **Chhoti applications me unnecessary complexity create ho sakti hai.**  

❌ **Extra Memory Usage:**  
   - **Har state ka alag object memory consume karta hai.**  

---

## **7️⃣ State Pattern ke Software Design Principles** 🎯  

✔ **Encapsulation:**  
   - **State transitions aur behavior encapsulated hote hain.**  

✔ **Open/Closed Principle (OCP):**  
   - **Naye states ko add karna easy hota hai bina existing code modify kiye.**  

✔ **Single Responsibility Principle (SRP):**  
   - **Har state ka alag class hota hai jo sirf us state ka kaam handle karta hai.**  

✔ **Loose Coupling:**  
   - **Context class ko har specific state ka detail nahi pata, bas interface ke through interact karta hai.**  

---

## **🔹 State Pattern Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - **State pattern ek object ke dynamic behavior ko manage karne ka design pattern hai.**  

2️⃣ **Kab Use Karte Hain?**  
   - **Jab kisi system ka behavior multiple states ke basis pe change hota ho.**  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **State Interface + Concrete States + Context Class.**  

4️⃣ **Real-World Examples:**  
   - **Media Players, Traffic Lights, ATMs, E-commerce Orders, Document Editors.**  

5️⃣ **Fayde & Limitations:**  
   ✔ **Encapsulation aur reusability badhti hai.**  
   ❌ **Complexity aur memory usage badh sakti hai.**  

---

### **💡 Conclusion**  
State Pattern **dynamic behavior control karne ka ek efficient design pattern hai** jo **real-world applications jaise Media Players, ATMs, aur Traffic Lights me kaafi useful hota hai.** 🚀
