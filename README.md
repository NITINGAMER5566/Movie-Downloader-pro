# **Movie Downloader - Step-by-Step Development Guide**  

This **README** explains how I built the **Movie Downloader** using the **HenzTech API**, providing a clean interface to search and download movies.  

---

## **📌 Features**  
✅ **Search Movies** – Enter a movie name and get direct download links  
✅ **Clean UI** – No API creator info, just movie titles and download buttons  
✅ **Episode Support** – Search for TV show episodes  
✅ **Quality Info** – Displays video quality (WEB-DL, HD, CAM)  
✅ **Responsive Design** – Works on desktop & mobile  

---

## **🛠️ How It Was Built**  

### **1️⃣ Understanding the API**  
The **HenzTech API** responds with:  
```json
{
  "creator": "EMMY HENZ",
  "status": 200,
  "success": true,
  "movie": "Moana 2 (NKIRI COM) WEB DL DOWNLOADED FROM NKIRI COM",
  "download_link": "https://example.com/Moana.2.mkv"
}
```
**Key Elements Used:**  
- `movie` → Displayed name (cleaned up)  
- `download_link` → Direct download URL  
- `success` → Checks if the movie is available  

---

### **2️⃣ HTML Structure**  
Created a simple, user-friendly interface:  
- **Search Bar** (`movieName`, `episode` inputs)  
- **Results Container** (Shows movie title & download button)  
- **Loading Spinner** (For API requests)  
- **Error Messages** (If movie not found)  

---

### **3️⃣ JavaScript Logic**  

#### **🔹 Step 1: Fetching Data from API**  
```javascript
async function searchMovie() {
  const movieName = document.getElementById('movieName').value.trim();
  const apiUrl = `https://henz-api.zone.id/api/moviedl?moviename=${encodeURIComponent(movieName)}`;
  
  const response = await fetch(apiUrl);
  const data = await response.json();
  
  if (!data.success) {
    showError("Movie not found!");
    return;
  }
  
  displayResult(data);
}
```

#### **🔹 Step 2: Displaying Results**  
- **Cleans up movie name** (removes `(NKIRI COM)`)  
- **Shows download button** with direct link  
- **Extracts quality info** (WEB-DL, HD, etc.)  

```javascript
function displayResult(data) {
  const cleanMovieName = data.movie.replace(/\(.*?\)/g, '').trim();
  
  resultContent.innerHTML = `
    <h2>${cleanMovieName}</h2>
    <a href="${data.download_link}" class="download-btn">Download Now</a>
    <p>Quality: ${extractQualityInfo(data.movie)}</p>
  `;
}
```

#### **🔹 Step 3: Error Handling**  
- Checks if `success: false`  
- Shows user-friendly error messages  

```javascript
function showError(message) {
  errorDiv.textContent = message;
  errorDiv.style.display = 'block';
}
```

---

### **4️⃣ Styling (CSS)**  
Used **modern, clean design** with:  
- **Flexbox** for responsive layout  
- **Hover effects** on buttons  
- **Loading spinner** for API requests  
- **Mobile-friendly** design  

---

## **🚀 How to Use the Downloader**  
1. **Enter a movie name** (e.g., "Moana")  
2. (Optional) Add an **episode number** if it's a series  
3. Click **"Search"**  
4. If found, click **"Download Now"**  

---

## **❓ Why Some Movies Aren’t Available**  
❌ **Netflix/Disney+ content** → Often blocked due to DRM  
❌ **API limitations** → HenzTech may not have all movies  
❌ **Incorrect search query** → Try exact names (e.g., "All of Us Are Dead 2022")  

**Fix:**  
```javascript
// Try adding the year or "series"
const apiUrl = `https://henz-api.zone.id/api/moviedl?moviename=All+of+Us+Are+Dead+2022`;
```

---

## **🔧 Possible Improvements**  
🔹 **Multiple API fallbacks** (if HenzTech fails)  
🔹 **YouTube trailers** for previews  
🔹 **Download history** (local storage)  
🔹 **User requests** for missing movies  

---

## **📥 Download & Run**  
1. **Copy the HTML/CSS/JS code** into a file (`index.html`)  
2. **Open in browser** (Chrome/Firefox)  
3. **Start downloading movies!** 🎬  

---

### **🎯 Conclusion**  
This downloader uses **HenzTech API** to fetch direct movie links while keeping the interface **clean and user-friendly**. If a movie isn’t available, try **different search terms** or check back later.  
