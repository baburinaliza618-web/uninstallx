# UninstallX

<p align="center">
  <strong>A modern, fast and beautiful Windows app uninstaller.</strong>
</p>

<p align="center">
  Built with Electron, React and Vite.
</p>

<p align="center">
  <a href="#features">Features</a>
  ·
  <a href="#installation">Installation</a>
  ·
  <a href="#development">Development</a>
  ·
  <a href="#build">Build</a>
  ·
  <a href="#roadmap">Roadmap</a>
</p>

<br />

<p align="center">
  <img src="assets/preview.png" alt="UninstallX Preview" width="900" />
</p>

---

## ✨ Overview

**UninstallX** is a modern Windows application uninstaller designed to make managing installed software fast, simple and beautiful.

Instead of navigating through the old Windows Control Panel, UninstallX provides a clean desktop interface for discovering and uninstalling applications installed on your system.

Built specifically for Windows with **Electron + React + Vite**, UninstallX combines a modern UI with native Windows functionality.

---

## 🚀 Features

### 📦 Installed Applications

Automatically discover installed applications using the Windows Registry.

UninstallX scans:

* `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall`
* `HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall`
* `HKCU\Software\Microsoft\Windows\CurrentVersion\Uninstall`

Application information includes:

* Application name
* Version
* Publisher
* Installation date
* Installation directory
* Application size
* Application icon
* Uninstall command
* Quiet uninstall command

---

### 🗑️ Safe Uninstallation

UninstallX launches the application's official Windows uninstaller instead of trying to delete application files manually.

Supports:

* `.exe` uninstallers
* MSI packages
* `msiexec`
* `QuietUninstallString`
* `UninstallString`
* uninstallers requiring administrator privileges

When administrator permissions are required, Windows UAC is used normally.

---

### 🔎 Instant Search

Quickly find installed applications by:

* Name
* Publisher
* Version
* Category

Use:

```text
Ctrl + K
```

to instantly focus the search field.

---

### 🎨 Modern Interface

Designed as a premium Windows desktop application.

The interface includes:

* Dark mode
* Glassmorphism
* Smooth animations
* Responsive layouts
* Grid view
* List view
* Application details
* Loading states
* Empty states
* Error states
* Toast notifications
* Modern icons

---

### 📊 Dashboard

Get an overview of your installed software:

```text
124 Applications
287 GB Used
18 Large Apps
6 Installed Recently
```

The dashboard provides a quick overview without having to browse through every application.

---

### 🗂️ Categories

Filter applications by category:

* All
* Windows
* Microsoft
* Browsers
* Games
* Utilities
* Other

---

### ↕️ Sorting

Sort applications by:

* Name
* Size
* Installation date
* Publisher

---

### 🖼️ Application Icons

UninstallX attempts to use the application's native Windows icon.

If an icon cannot be extracted, a clean fallback icon is displayed automatically.

---

### 📁 Open Installation Folder

If an application's installation directory is available, you can open it directly in Windows Explorer.

---

### 🔄 Refresh

Rescan installed applications at any time.

After uninstalling an application, refresh the list to update the interface.

---

## 🛡️ Security

Security is an important part of UninstallX.

The React renderer does **not** have direct access to Node.js or the operating system.

Electron uses:

```js
contextIsolation: true
nodeIntegration: false
```

System operations are performed through a controlled IPC bridge:

```text
React UI
   │
   ▼
Preload
   │
   ▼
IPC
   │
   ▼
Electron Main Process
   │
   ▼
Windows
```

The renderer cannot execute arbitrary shell commands directly.

UninstallX also does **not** attempt to bypass Windows UAC.

---

## 🧰 Tech Stack

| Technology       | Purpose                      |
| ---------------- | ---------------------------- |
| Electron         | Windows desktop runtime      |
| React            | User interface               |
| Vite             | Frontend development & build |
| Lucide React     | Icons                        |
| Node.js          | Electron backend             |
| Windows Registry | Application discovery        |
| electron-builder | Windows installer            |

---

## 📁 Project Structure

```text
UninstallX/
│
├── electron/
│   ├── main.cjs
│   └── preload.cjs
│
├── src/
│   ├── components/
│   ├── App.jsx
│   ├── main.jsx
│   └── styles.css
│
├── public/
│
├── assets/
│   └── preview.png
│
├── index.html
├── vite.config.js
├── package.json
├── .gitignore
└── README.md
```

---

## 💻 Requirements

Before running UninstallX locally, make sure you have:

* Windows 10 or Windows 11
* Node.js 20+ recommended
* npm

Check your versions:

```bash
node --version
npm --version
```

---

## 📥 Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/uninstallx.git
```

Enter the project directory:

```bash
cd uninstallx
```

Install dependencies:

```bash
npm install
```

---

## 🧑‍💻 Development

Start the development environment:

```bash
npm run dev
```

This starts:

1. Vite development server
2. Electron
3. React inside an Electron `BrowserWindow`

The application runs as a **desktop application**, not as a browser tab.

Development architecture:

```text
Vite
 │
 │ localhost:5173
 ▼
Electron BrowserWindow
 │
 ▼
React
```

---

## 🏗️ Production Build

Build the React application:

```bash
npm run build
```

Then launch Electron using the production build:

```bash
npm run start
```

Production architecture:

```text
React
  │
  ▼
Vite build
  │
  ▼
dist/
  │
  ▼
Electron
  │
  ▼
Windows Desktop App
```

---

## 📦 Build Windows Installer

Create a Windows installer:

```bash
npm run dist
```

The generated installer will be placed in:

```text
release/
```

The installer uses **electron-builder** and produces a Windows `.exe`.

---

## ⚙️ Available Scripts

| Command         | Description             |
| --------------- | ----------------------- |
| `npm install`   | Install dependencies    |
| `npm run dev`   | Start development mode  |
| `npm run build` | Build React/Vite        |
| `npm run start` | Run production build    |
| `npm run dist`  | Build Windows installer |

---

## 🧩 Architecture

UninstallX follows a secure Electron architecture.

```text
┌─────────────────────────────┐
│          React UI           │
│                             │
│ Search · Apps · Dashboard   │
└──────────────┬──────────────┘
               │
               │ IPC
               ▼
┌─────────────────────────────┐
│          Preload            │
│                             │
│ Controlled API / contextBridge│
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│      Electron Main          │
│                             │
│ Registry · Uninstaller      │
│ Explorer · Windows APIs     │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│           Windows           │
│                             │
│ Registry · UAC · Explorer   │
└─────────────────────────────┘
```

---

## 🗺️ Roadmap

UninstallX is actively evolving.

### Current

* [x] Windows Registry scanning
* [x] Installed application list
* [x] Search
* [x] Filtering
* [x] Sorting
* [x] Grid/List views
* [x] Application details
* [x] Windows uninstallers
* [x] MSI support
* [x] UAC support
* [x] Open installation folder
* [x] Electron desktop architecture
* [x] Windows installer

### Planned

* [ ] Deep leftover scanner
* [ ] Leftover Registry detection
* [ ] Leftover file detection
* [ ] Startup applications manager
* [ ] Windows services manager
* [ ] Batch uninstall
* [ ] Restore points
* [ ] Uninstall history
* [ ] System cleanup
* [ ] Duplicate application detection
* [ ] Portable application detection
* [ ] Advanced application analytics
* [ ] Windows notifications
* [ ] Automatic update system

---

## ⚠️ Disclaimer

UninstallX launches the uninstall commands registered by Windows and the applications themselves.

It does not intentionally bypass Windows security mechanisms or remove protected system components.

Some applications may require administrator privileges or may use their own uninstall procedures.

Always review what you are uninstalling before confirming.

---

## 🤝 Contributing

Contributions, bug reports and feature requests are welcome.

If you find a bug:

1. Open an issue.
2. Describe what happened.
3. Include your Windows version.
4. Include the application that caused the issue.
5. Include relevant logs or screenshots when possible.

Pull requests are welcome.

---

## ⭐ Star the Project

If UninstallX is useful to you, consider giving the repository a ⭐.

It helps the project grow and lets others discover it.

---

## 📄 License

This project is licensed under the **MIT License**.

See [`LICENSE`](LICENSE) for more information.

---

<p align="center">
  <strong>UninstallX</strong>
  <br />
  Clean your Windows apps. Fast.
</p>
