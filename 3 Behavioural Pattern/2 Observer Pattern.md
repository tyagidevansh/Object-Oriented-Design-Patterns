# **Observer Pattern**  
Observer ek **behavioral design pattern** hai jo **ek object (Subject) ke state change hone par automatically multiple objects (Observers) ko notify karne ka system provide karta hai**.  

➡ **Simple Words Me:**  
Maan lo **tumhare paas ek YouTube channel hai** aur **tumhare subscribers** ko **tumhare naye video ke baare me turant notify karna hai**. Agar **har subscriber ko manually message bhejna pade**, to ye kaafi tedious ho jayega.  

✅ **Solution:**  
   - **YouTube Channel (Subject) subscribers (Observers) ka ek list maintain karega.**  
   - **Jab bhi naya video upload hoga, saare observers ko automatic notification send ho jayega.**  

➡ **Observer pattern asynchronous aur event-driven architecture me kaafi useful hota hai.**  

---

## **2️⃣ Kab Zaroorat Padti Hai? (Motivation & Real-Life Example)**  
Socho tum **ek stock market application** bana rahe ho jo **investors ko stock price change hone pe notify kare**.  

🔹 **Investor 1:** TCS Stock price monitor kar raha hai 📈  
🔹 **Investor 2:** Reliance Stock price monitor kar raha hai 📊  
🔹 **Investor 3:** Multiple stocks track kar raha hai 📉  

✅ **Observer Pattern ka Use:**  
   - **Stock Exchange (Subject) investors (Observers) ka ek list maintain karega.**  
   - **Jab bhi kisi stock ka price badlega, toh related investors ko automatic notification chala jayega.**  

---

## **3️⃣ Observer Pattern ke Main Components**  
Observer pattern **3 major components** se bana hota hai:  

1️⃣ **Subject (Observable) 📡**  
   - **Yeh ek central object hota hai jo state changes ko track karta hai**.  
   - **Observers ko add, remove aur notify karta hai.**  

2️⃣ **Observers (Subscribers) 👥**  
   - **Jo bhi subject ki updates ko listen karna chahta hai, wo observer ban jata hai.**  
   - **Agar subject ka state change hota hai, to observer ko automatic notify kiya jata hai.**  

3️⃣ **Concrete Subject & Concrete Observer (Implementation Classes) 🚀**  
   - **Concrete Subject:** Real-world entity jo state change karti hai.  
   - **Concrete Observer:** Real-world entities jo state change pe react karti hain.  

---

## **4️⃣ UML Diagram & Code Example**  

### **Class Diagram (Structure of Observer Pattern):**  

```
┌───────────────────────┐
│      Subject         │
│ (Observable)         │
│ addObserver()        │
│ removeObserver()     │
│ notifyObservers()    │
└───────────────────────┘
            ▲
            │
 ┌─────────┼──────────┐
 │         │          │
 ▼         ▼          ▼
┌──────────┐  ┌──────────┐  ┌──────────────┐
│ Observer │  │ Observer │  │  Observer    │
│ User 1   │  │ User 2   │  │  User 3      │
└──────────┘  └──────────┘  └──────────────┘
```

---

### **Python Code Example - YouTube Notification System** 📝  

```python
# Step 1: Observer Interface
from abc import ABC, abstractmethod

class Observer(ABC):
    @abstractmethod
    def update(self, message):
        pass

# Step 2: Concrete Observers (Subscribers)
class Subscriber(Observer):
    def __init__(self, name):
        self.name = name

    def update(self, message):
        print(f"🔔 {self.name}, New Video Alert: {message}")

# Step 3: Subject Interface (Observable)
class YouTubeChannel:
    def __init__(self, channel_name):
        self.channel_name = channel_name
        self.subscribers = []

    def add_subscriber(self, subscriber: Observer):
        self.subscribers.append(subscriber)

    def remove_subscriber(self, subscriber: Observer):
        self.subscribers.remove(subscriber)

    def notify_subscribers(self, video_title):
        for subscriber in self.subscribers:
            subscriber.update(f"{self.channel_name} uploaded: {video_title}")

# Step 4: Client Code
if __name__ == "__main__":
    # YouTube Channel (Observable)
    channel = YouTubeChannel("Code Crusaders")

    # Subscribers (Observers)
    user1 = Subscriber("Alice")
    user2 = Subscriber("Bob")
    user3 = Subscriber("Charlie")

    # Add Subscribers
    channel.add_subscriber(user1)
    channel.add_subscriber(user2)
    channel.add_subscriber(user3)

    # Upload a new video (All subscribers notified)
    channel.notify_subscribers("Observer Pattern in Python")
    
    # Remove a subscriber
    channel.remove_subscriber(user2)

    # Upload another video
    channel.notify_subscribers("Decorator Pattern Explained")
```

✅ **Output:**  
```
🔔 Alice, New Video Alert: Code Crusaders uploaded: Observer Pattern in Python
🔔 Bob, New Video Alert: Code Crusaders uploaded: Observer Pattern in Python
🔔 Charlie, New Video Alert: Code Crusaders uploaded: Observer Pattern in Python

🔔 Alice, New Video Alert: Code Crusaders uploaded: Decorator Pattern Explained
🔔 Charlie, New Video Alert: Code Crusaders uploaded: Decorator Pattern Explained
```

✅ **Code kaafi flexible aur reusable ban gaya hai. Naye subscribers ko easily add/remove kiya ja sakta hai.**  

---

## **5️⃣ Real-World Examples** 🌍  

1️⃣ **YouTube Notifications:**  
   - **Jab bhi YouTuber naya video upload karta hai, subscribers ko automatic notification chala jata hai.**  

2️⃣ **Stock Market Price Alerts:**  
   - **Jab kisi stock ka price badalta hai, investors ko real-time update milta hai.**  

3️⃣ **E-Commerce Price Tracking:**  
   - **Agar kisi product ka price drop hota hai, subscribed users ko notification send hota hai.**  

4️⃣ **Social Media (Instagram, Twitter, Facebook):**  
   - **Tumhare kisi bhi post pe like ya comment aata hai, to tum notify hote ho.**  

5️⃣ **Event-Driven Programming (ReactJS, Node.js):**  
   - **Event Listeners ka kaam bhi observer pattern pe based hota hai.**  

---

## **6️⃣ Limitations & Pitfalls** ⚠  

❌ **Memory Leak Issue:**  
   - **Agar kisi observer ko remove nahi kiya jaye, to unneeded memory use hoti rahegi.**  

❌ **Complexity Badhti Hai:**  
   - **Multiple observers hone par debugging aur testing mushkil ho sakti hai.**  

❌ **Circular Dependencies:**  
   - **Agar observer aur subject cyclic dependency me fas jaye, to infinite loop ho sakta hai.**  

---

## **7️⃣ Observer Pattern ke Software Design Principles** 🎯  

✔ **Encapsulation:**  
   - **State changes ka encapsulation aur loosely coupled design ensure hota hai.**  

✔ **Open/Closed Principle (OCP):**  
   - **Naye observers ko add karna easy hota hai bina existing code modify kiye.**  

✔ **Single Responsibility Principle (SRP):**  
   - **Subject sirf state changes track karta hai aur observers sirf updates handle karte hain.**  

✔ **Loose Coupling:**  
   - **Observers aur subject loosely coupled hote hain, jo flexibility badhata hai.**  

---

## **🔹 Observer Pattern Summary in 5 Points**  

1️⃣ **Kya Hai?**  
   - Observer pattern **ek event-driven approach hai jo ek object ke state change hone par automatically multiple observers ko notify karta hai.**  

2️⃣ **Kab Use Karte Hain?**  
   - Jab **multiple components ko ek object ke state change hone pe update karna ho.**  

3️⃣ **Kaise Kaam Karta Hai?**  
   - **Observable (Subject) + Observers (Subscribers) + Notify Mechanism**.  

4️⃣ **Real-World Examples:**  
   - **YouTube, Stock Market, E-Commerce, Social Media, Event-Driven Programming.**  

5️⃣ **Fayde & Limitations:**  
   ✔ **Real-time updates aur loose coupling.**  
   ❌ **Memory leak aur complexity badh sakti hai.**  

---

### **💡 Conclusion**  
Observer pattern **real-time notifications aur event-driven programming ke liye ek powerful design pattern hai** jo **dynamic aur scalable applications banane me madad karta hai.** 🚀
