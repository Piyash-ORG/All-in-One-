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
Pause# ইউজার থেকে পাথ ইনপুট নেওয়া
$inputPath = Read-Host "Enter video file or folder path"
$inputPath = $inputPath.Trim('"')

# আউটপুট ফোল্ডার
$outputFolder = Join-Path (Get-Item $inputPath).DirectoryName "Converted_Videos"
if (!(Test-Path $outputFolder)) {
    New-Item -ItemType Directory -Path $outputFolder | Out-Null
}

function Convert-Video($file) {
    $baseName = [System.IO.Path]::GetFileNameWithoutExtension($file)
    $outputFile = Join-Path $outputFolder "$baseName`_1080p.mp4"
    
    Write-Host "Processing: $baseName"

    ffmpeg -i "$file" -vf "scale=1920:1080:force_original_aspect_ratio=decrease,pad=1920:1080:(ow-iw)/2:(oh-ih)/2" `
    -c:v libx264 -b:v 4.8M -preset medium -c:a aac -b:a 192k "$outputFile" -y
}

if (Test-Path $inputPath -PathType Leaf) {
    Convert-Video $inputPath
}
elseif (Test-Path $inputPath -PathType Container) {
    $files = Get-ChildItem -Path $inputPath -Include *.mp4, *.mkv, *.avi -Recurse
    foreach ($file in $files) {
        Convert-Video $file.FullName
    }
}
else {
    Write-Host "Wrong path!"
}

Write-Host "Done!"
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
