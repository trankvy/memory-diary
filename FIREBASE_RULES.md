# 🔥 Fix "Permission Denied" in Firebase

If the app isn't letting you share or join rooms, your **Firebase Security Rules** are likely blocking access. By default, Firebase blocks all reads/writes.

## 🛠️ How to Fix It (1 Minute)

1.  Go to your [Firebase Console](https://console.firebase.google.com/).
2.  Click on your project.
3.  In the left sidebar, click **Build** -> **Realtime Database**.
4.  Click the **Rules** tab at the top.
5.  **Delete** the current rules and **Paste** this:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

6.  Click **Publish**.

---

### ⚠️ Important Note
These rules allow **anyone** with your API key (which is public in your code) to read/write to your database.
*   **For this prototype/demo:** This is perfectly fine!
*   **For a real production app:** You would add Authentication rules later.

Once you publish these rules, refresh your app and try sharing again! 🚀

