# Playlists - IPTV & Movie Player 

Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\convert.ps1

A modern, fast, and lightweight web player designed for seamless streaming.  
Watch **Live TV**, **Movies**, and **Web Series** directly from your browser with a premium Netflix-style dark interface.

<br>

<p align="center">
  <a href="https://drive.google.com/uc?id=1WIn8V0-hcubpf7igxoz9PWOqMqyNWkmg&export=download">
    <img src="https://img.shields.io/badge/View_Live_Demo-➡️-1DB954.svg?style=for-the-badge" alt="Live Demo">
  </a>
</p>

```
# ভিডিও কনভার্টার (1080p, 4.8Mbps, H.264) - CPU Optimized

# ইউজার থেকে পাথ ইনপুট নেওয়া
$inputPath = Read-Host "আপনার ভিডিও ফাইল বা ফোল্ডারের পাথ এখানে দিন"

# পাথের আশেপাশের ডাবল কোটেশন (") রিমুভ করা (আগের এরর ফিক্স)
$inputPath = $inputPath -replace '"', ''

# আউটপুট ফোল্ডার তৈরি করা
$outputFolder = Join-Path (Get-Item $inputPath).DirectoryName "Converted_Videos"
if (-not (Test-Path $outputFolder)) { 
    New-Item -ItemType Directory -Path $outputFolder | Out-Null 
}

# ফাইল প্রসেসিং ফাংশন
function Start-Conversion($file) {
    $baseName = [System.IO.Path]::GetFileNameWithoutExtension($file)
    $outputFile = Join-Path $outputFolder "$baseName`_1080p.mp4"
    
    Write-Host "`nপ্রসেসিং শুরু হচ্ছে: $baseName" -ForegroundColor Yellow
    
    # FFmpeg কমান্ড (i5 6th Gen এর জন্য preset fast ব্যবহার করা হয়েছে)
    ffmpeg -i "$file" -vf "scale=1920:1080:force_original_aspect_ratio=decrease,pad=1920:1080:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -preset fast -b:v 4.8M -maxrate 4.8M -bufsize 9.6M -c:a aac -b:a 192k "$outputFile" -y
}

# পাথটি ফাইল না ফোল্ডার তা চেক করা
if (Test-Path $inputPath -PathType Leaf) {
    Start-Conversion $inputPath
} elseif (Test-Path $inputPath -PathType Container) {
    $files = Get-ChildItem -Path $inputPath -Include *.mp4,*.mkv,*.mov,*.avi,*.ts -File -Recurse
    foreach ($file in $files) { 
        Start-Conversion $file.FullName 
    }
} else {
    Write-Host "ভুল পাথ দিয়েছেন! দয়া করে সঠিক পাথ দিন।" -ForegroundColor Red
}

Write-Host "`nকনভার্ট সম্পন্ন হয়েছে! আপনার ফাইলগুলো এখানে আছে: $outputFolder" -ForegroundColor Green
Pause

```

```
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\convert.ps1
```
<br>

---

## ✨ Key Features

### ⚙️ Advanced Quality Selector  
Auto-detects all HLS qualities (Auto, 1080p, 720p...) with a clean custom menu.

### 🤖 Smart Recommendations  
While watching, it automatically shows **“You might also like”** based on category.

### 📂 Dynamic Category Filtering  
Parses playlist and builds a **horizontal scrollable category bar** (Sports, News, Movies, etc.).

### 🔓 CORS Proxy Toggle  
Built-in proxy switch for streams blocked by CORS.

### 📱 Fully Responsive UI  
Tailwind-based layout optimized for both mobile & desktop.

### 🚀 Optimized Performance  
Lazy-loaded logos + clean modular JavaScript for ultra-fast browsing.

---

## 📡 Playlist (Auto Copy Boxes Included)

### ✅ RAW M3U Link  
```
https://raw.githubusercontent.com/piyashltd/all-in-one/refs/heads/main/index.m3u
```

### ✅ GitHub Pages (Raw Output)  
```
https://piyashltd.github.io/all-in-one/index.m3u
```
---

## 🚀 Getting Started

### 1️⃣ Launch the Player  
Click the **View Live Demo** button above.

### 2️⃣ Browse Content  
Use the **top category bar** or **library grid**.

### 3️⃣ Player Controls  
- Tap any card to start playback  
- Use the **⚙️ Gear Icon** to change quality  
- Scroll for **recommended content**  

### ❗ If stream fails:
Go to **Header → Settings (⚙️) → Enable CORS Proxy → Reload**

---

## 🛠️ Built With
- HTML5 + Vanilla JS (ES6+)  
- Tailwind CSS  
- Video.js  
- VideoJS Contrib Quality Levels  
- FontAwesome Icons  

---

<p align="center">Made with ❤️ for streaming lovers.</p>
