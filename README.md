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
# ভিডিও কনভার্টার (1080p, 4.8Mbps, H.264) - Final Fixed Version
$inputPath = Read-Host "ভিডিও ফাইল বা ফোল্ডারের পাথ এখানে দিন"
$inputPath = $inputPath -replace '"', ''

if (!(Test-Path $inputPath)) { Write-Host "পাথটি খুঁজে পাওয়া যায়নি!" -ForegroundColor Red; Pause; exit }

$outputFolder = Join-Path (Get-Item $inputPath).DirectoryName "Converted_Videos"
if (!(Test-Path $outputFolder)) { New-Item -ItemType Directory -Path $outputFolder | Out-Null }

function Start-Conversion($file) {
    $baseName = [System.IO.Path]::GetFileNameWithoutExtension($file)
    $outputFile = Join-Path $outputFolder "$baseName`_1080p.mp4"
    
    Write-Host "`n----------------------------------------"
    Write-Host "প্রসেসিং হচ্ছে: $baseName" -ForegroundColor Cyan
    
    # ২>&১ যোগ করা হয়েছে যাতে লাল এরর মেসেজ না আসে
    & ffmpeg -i "$file" -vf "scale=1920:1080:force_original_aspect_ratio=decrease,pad=1920:1080:(ow-iw)/2:(oh-ih)/2" `
             -c:v libx264 -b:v 4.8M -maxrate 4.8M -bufsize 9.6M -preset fast `
             -c:a aac -b:a 192k "$outputFile" -y 2>&1 | ForEach-Object {
                 if ($_ -match "frame=") { Write-Host $_ -ForegroundColor Gray }
             }

    if (Test-Path "$outputFile") {
        Write-Host "সফলভাবে কনভার্ট হয়েছে: $baseName" -ForegroundColor Green
    } else {
        Write-Host "কনভার্ট করতে সমস্যা হয়েছে: $baseName" -ForegroundColor Red
    }
}

if (Test-Path $inputPath -PathType Leaf) {
    Start-Conversion $inputPath
} else {
    $files = Get-ChildItem -Path $inputPath -Include *.mp4,*.mkv,*.mov,*.avi,*.ts -File -Recurse
    foreach ($file in $files) { Start-Conversion $file.FullName }
}

Write-Host "`nসব কাজ শেষ! আপনার ভিডিওগুলো এই ফোল্ডারে আছে: $outputFolder" -ForegroundColor Green
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
