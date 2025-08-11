# Setup SDK Example

This example demonstrates how to **initialize the Navigine SDK**  
in an Android project using the `Application` class.

---

## ✅ Step-by-step Guide

### 🔹 Step 1: Add the `.aar` dependency

Make sure the SDK `.aar` file is located in the `libs/` directory.  
Then add the following in your `build.gradle.kts`:

```kotlin
dependencies {
    implementation(files("../libs/navigine.aar"))
}
```

---

### 🔹 Step 2: Create your Application class

```kotlin
class App : Application() {
    override fun onCreate() {
        super.onCreate()
        initSdk(this)
    }
}
```

---

### 🔹 Step 3: Initialize the SDK with your data

```kotlin
private fun initSdk(context: Context) {
    try {
        Navigine.initialize(context)

        NavigineSdk.getInstance().apply {
            setServer("https://ips.navigine.com")  // replace with your server URL
            setUserHash("your_user_hash")          // replace with your user hash

            val locationManager = locationManager
            val navigationManager = getNavigationManager(locationManager)
            val measurementManager = getMeasurementManager(locationManager)
        }
    } catch (e: Exception) {
        Log.e("NavigineSdkManager", "Initialization failed", e)
    }
}
```

---

### 🔹 Step 4: Register your Application in `AndroidManifest.xml`

```xml
<application
    android:name=".yourPackage.App"/>
```

---

## ⚠️ Important Notes

- You can call `NavigineSdk.getInstance()` and set your data whenever you're ready,  
  but it must be once and **must be before** you start working with `LocationView` or any other SDK-related component.
- Setting the **user hash** and **server URL** is **mandatory**.
- You should obtain the user hash from a **trusted source** (e.g., login flow or configuration).
- Managers like `LocationManager`, `NavigationManager`, and `MeasurementManager`  
  can be accessed **only after successful initialization**.

---

## 📦 What's Next?

For further usage examples, refer to other modules like:

- [`locationmanager/`](../LocationManager)
- [`navigationmanager/`](../NavigationManager)
- [`measurement/`](../MeasurementManager)
- [`AsyncRouteManager/`](../AsyncRouteManager)
- [`LocationWindow_Camera/`](../Camera)
- [`LocationWindow_Add_Objects/`](../AddingObjects)
- [`LocationWindow_Pickers/`](../Pickers)
