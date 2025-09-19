# Fix ChatGPT Login on iOS 15 (Route Error 400 / Session Expired)

> **Educational use only.** This workaround writes a session cookie to work around a broken login flow in iOS 15 Safari. Do not use it on untrusted devices or share your token.

## Why this happens
On **iOS 15 Safari**, the ChatGPT web login often fails with:
- `Route Error 400 – Unknown Error`
- `Session expired`

Safari blocks or loses the session cookie during redirects, so the flow never completes.

## Approach (TL;DR)
1. On a working desktop browser, copy your ChatGPT session cookie value `__Secure-next-auth.session-token`.
2. On the iOS 15 device, use a bookmarklet to set that cookie for `chatgpt.com`.
3. Refresh the page — you should be signed in.

---

## Step-by-step

### 1) Get the session token on a desktop
1. Log in at <https://chatgpt.com> or <https://chat.openai.com>.  
2. Open **DevTools → Application → Cookies**.  
3. Find **`__Secure-next-auth.session-token`** and copy its **Value** (a long string starting with `eyJ...`).

### 2) Create the bookmarklet on iOS (Safari)
1. Open any page in Safari → **Share** → **Add Bookmark** (name it `Set Cookie`).  
2. Open **Bookmarks → Edit → Set Cookie**, and replace the URL with:

```javascript
javascript:(function(){document.cookie="__Secure-next-auth.session-token=PASTE_YOUR_TOKEN_HERE; domain=chatgpt.com; path=/; secure";alert('Token set for chatgpt.com');})()
