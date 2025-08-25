# Spring Core Concepts – Proxies, Reflection, Caching & CGLIB

This repository demonstrates my learning of **Spring Framework internals and advanced concepts** including **Spring Proxies**, **Reflection API**, **@Cacheable annotation**, and **CGLIB (Code Generation Library)**.  
These concepts are foundational for **AOP (Aspect-Oriented Programming)**, **dependency injection**, **method interception**, and **performance optimization** in Spring-based applications.

---

## 📌 **What I Learned**

### 1. **Spring Proxies**
- **What are Proxies?**  
  Proxies act as an intermediate layer between the **client** and the **target object** to **intercept method calls**.  
  In Spring, proxies are used for:
  - **AOP (Aspect-Oriented Programming)** – applying cross-cutting concerns (like logging, security, transactions).
  - **Lazy Initialization** of beans.
- **Types of Proxies in Spring**:
  - **JDK Dynamic Proxy** (uses `java.lang.reflect.Proxy`)
    - Works with **interfaces only**.
    - Uses **Reflection API** internally.
  - **CGLIB Proxy**
    - Works by **subclassing the target class**.
    - Used when there is **no interface** or `proxyTargetClass=true`.
- **Example Use Case:**  
  When you annotate a method with `@Transactional`, Spring creates a proxy around your bean to add transaction logic.

---

### 2. **Reflection API in Java**
- **What is Reflection?**
  - A feature of Java that allows us to **inspect classes, methods, and fields at runtime**.
- **Why is it used in Spring?**
  - Spring uses Reflection to **inject dependencies**, **initialize beans**, and **call methods dynamically**.
- **Example in code:**  
  `Method.invoke()` is used internally to call your method when you use dynamic proxies.

---

### 3. **@Cacheable Annotation**
- **What is Caching?**
  - Storing frequently accessed data in memory to **avoid repeated calculations or DB queries**.
- **@Cacheable in Spring:**
  - Provided by **Spring Cache abstraction**.
  - Marks a method’s result to be stored in cache.
  - Example:
    ```java
    @Cacheable("users")
    public User getUserById(Long id) {
        return userRepository.findById(id).orElseThrow();
    }
    ```
  - Next time the same `id` is requested, it will return data from **cache**, not DB.

---

### 4. **CGLIB (Code Generation Library)**
- **What is CGLIB?**
  - A library used by Spring to **generate subclasses at runtime** for method interception.
- **Why is it needed?**
  - When your class does **not implement an interface**, JDK proxies cannot be used → **Spring uses CGLIB**.
- **Example:**
  - If you have `@Transactional` on a class with no interface → CGLIB creates a subclass and adds extra logic.

---

### 5. **AOP (Aspect-Oriented Programming) Relation**
- All the above concepts are **fundamental for AOP** in Spring:
  - **Proxies** → Intercept method calls.
  - **Reflection** → Call methods dynamically.
  - **CGLIB** → Create proxy subclasses.
  - **@Cacheable** → Implement caching as a cross-cutting concern.

---

## ✅ **Technologies Used**
- **Java** (Core + Reflection API)
- **Spring Framework**
- **Spring Cache**
- **CGLIB**
- **Gradle**



