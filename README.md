# AuraOS

> **AuraOS** is an original, fluid, browser-based desktop operating system built with pure HTML5, CSS3, and Vanilla JavaScript (zero dependencies, no build steps, no external assets). It provides a distinct visual identity centered on frosted glass aesthetics, cosmic aurora color palettes, Web Audio sound synthesis, dynamic canvas shaders, and a full-featured desktop environment.

---

## ✨ Key Features & Architecture

### 1. Distinct Visual Identity
- **Original Logo & Vectors**: Procedural SVG glowing orbital rings with a radiant core. 100% original inline vector icon set for all apps and system controls.
- **Glassmorphic Optics**: Multi-layered backdrop blurs (`backdrop-filter: blur(28px) saturate(180%)`), subtle inner specular highlights, and soft elevation shadows.
- **Color Themes**: Deep Indigo / Cosmic Dark mode and Crisp Alabaster Light mode with 5 selectable dynamic accent glows (Aurora Cyan, Cosmic Violet, Warm Coral, Emerald Mint, Solar Amber).
- **4 Real-Time 60fps Wallpapers**:
  1. *Aurora Borealis* — Flowing undulating teal, cyan, and violet atmospheric curtains.
  2. *Deep Cosmos* — Twinkling starfields with drifting multi-hue nebulae.
  3. *Solar Twilight* — Warm coral and peach sunburst horizon with solar corona.
  4. *Cyber Grid* — Retro-futuristic neon perspective wave grid.
- **Signature Feature ("Aura Ambient Core")**:
  - Dynamically calculates ambient celestial radiance based on the current local time (Dawn Aurora, Solar Radiance, Sunset Ember, Midnight Nebula) and casts an ambient halo across the screen.
  - Built-in generative meditative audio drone synthesizer toggleable directly in the Control Center.

### 2. Desktop Shell
- **Boot Sequence & Lock Screen**: Animated glowing logo, progressive initialization steps, Web Audio boot chime, and user login card.
- **Top Menu Bar**: Original Aura logo menu (About, System Settings, Sleep, Restart, Shut Down), dynamic active application menus (File, Edit, View, Help), Wi-Fi, Battery, Volume, Control Center toggle, and live clock/date.
- **Magnifying Glass Dock**: Cosine-based parabolic magnification on hover, launch bounce physics, running app indicators, and Trash receptacle.
- **Window Manager (WM)**:
  - Draggable with header drag-bounds.
  - 8-directional edge and corner resizing (`n`, `s`, `e`, `w`, `ne`, `nw`, `se`, `sw`).
  - Active and inactive window depth styling.
  - Genie-style minimize curve into dock icons.
  - Edge snapping (drag to left half, right half, or top full-screen with real-time glass ghost preview).
  - Mission Control (`F3`): Exposé thumbnail matrix tiling all active windows.
- **Spotlight Search (`Cmd/Ctrl + Space`)**: Real-time fuzzy search across applications, virtual file system documents, and inline math calculations.
- **Launchpad**: Full-screen glass overlay with searchable app grid.
- **Control Center**: Quick sliders for master volume and display brightness, toggles for Wi-Fi, Bluetooth, Dark Mode, Focus Mode, and Ambient Aura.
- **Notifications & Toasts**: Slide-in toast alerts with audio chimes and a Notification Center history drawer.
- **Virtual File System (VFS)**: Persistent hierarchical file system stored in `localStorage` (`/Desktop`, `/Documents`, `/Pictures`, `/Music`, `/Downloads`, `/Trash`).

---

## 📱 13 Built-in Applications

| Application | Name | Description |
|---|---|---|
| 🗂️ File Manager | **Explorer** | Hierarchical file browser with sidebar, path breadcrumbs, grid/list view, folder creation, file deletion, and file launching. |
| 💻 Terminal | **Shell** | Unix-like CLI supporting `ls`, `cd`, `mkdir`, `touch`, `cat`, `rm`, `echo`, `clear`, `help`, `date`, `whoami`, `aurafetch`, `theme`, `open`, `calc`, and tab completion. |
| 📝 Notes | **Notes** | Rich text & markdown note editor with sidebar note organizer, markdown formatting buttons, search, and autosave. |
| 🔢 Calculator | **Calculator** | Glassmorphic calculator featuring Basic arithmetic, Scientific trigonometry & roots, memory registers, and calculation tape history. |
| 🌐 Browser | **Orbit** | Multi-tab web browser simulator with URL navigation, back/forward/reload, and pre-configured bookmarks. |
| 🎵 Audio Player | **Music Player** | Audio playback for custom MP3 uploads plus built-in synthetic ambient tracks with a real-time canvas frequency visualizer. |
| 🖼️ Gallery | **Photos** | Photo gallery preloaded with procedural artwork, custom image upload, and an interactive lightbox with zoom and rotate controls. |
| ⚙️ Preferences | **Settings** | Complete control panel for wallpapers, dark/light theme, accent colors, user profile name/avatar, dock position & size, and system reset. |
| 📅 Scheduler | **Calendar** | Month view calendar with today highlight, previous/next month navigation, and persistent event scheduling. |
| ⛅ Weather | **Weather** | Dynamic weather station with animated SVG weather scenes (Sun, Clouds, Rain, Aurora), hourly forecast, and city switcher. |
| ✍️ Code Editor | **Code Editor** | Text and code editor with dynamic line numbers, syntax status, cursor coordinates, and direct load/save integration with the Virtual File System. |
| 🎮 Mini Games | **Arcade** | Playable 60fps canvas **Snake** with score tracking & high score persistence, plus **2048** sliding tile puzzle game. |
| 🛍️ Marketplace | **App Store** | Discover and pin/unpin applications to/from the Dock and Launchpad. |

---

## 🚀 How to Run

Because AuraOS is built entirely with vanilla web standards and zero dependencies, you can run it immediately without compiling or installing packages:

### Option 1: Direct File Launch
Simply double-click `index.html` in your file explorer to open it in Chrome, Edge, Firefox, or Safari.

### Option 2: Local Static Server (Recommended)
You can serve the directory using Python's built-in HTTP server:
```bash
cd auraos
python -m http.server 8080
```
Then navigate to `http://localhost:8080` in your web browser.

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Cmd / Ctrl + Space` | Toggle Spotlight Search |
| `F3` | Toggle Mission Control (Exposé) |
| `Cmd / Ctrl + W` | Close active window |
| `Cmd / Ctrl + M` | Minimize active window to dock |
| `Cmd / Ctrl + Tab` | Switch between open windows |
| `Escape` | Dismiss Spotlight, Launchpad, Mission Control, or Control Center |

---

## 🛠️ Developer Guide: How to Add a New App

Every application in AuraOS is a self-contained module registered with the global `AuraApps` registry.

### Step 1: Create your app class
Define a class that creates and manages its DOM element:

```javascript
class MyCustomApp {
  constructor(wm, params = {}) {
    this.wm = wm;
    this.element = document.createElement('div');
    this.element.style.padding = '20px';
    this.element.innerHTML = `
      <h2>Hello from My App!</h2>
      <p>This is a custom AuraOS application.</p>
      <button class="explorer-btn" id="my-btn">Click Me</button>
    `;

    this.element.querySelector('#my-btn').addEventListener('click', () => {
      if (window.AuraNotifications) {
        window.AuraNotifications.toast({
          title: 'Custom App',
          body: 'Button was clicked!'
        });
      }
    });
  }

  // Optional: Called when window is closed
  destroy() {
    console.log('MyCustomApp closed');
  }
}
```

### Step 2: Register the app
Register your app with metadata, dimensions, and an icon:

```javascript
window.AuraApps.register({
  id: 'mycustomapp',
  name: 'My Custom App',
  category: 'Utilities',
  icon: window.AuraIcons.logo(16), // or custom SVG string
  defaultWidth: 500,
  defaultHeight: 360,
  createInstance: (wm, params) => new MyCustomApp(wm, params)
});
```

### Step 3: Include in `index.html`
Add `<script src="js/apps/mycustomapp.js"></script>` before `js/main.js`. Your application will immediately appear in **Launchpad**, **Spotlight**, and can be pinned to the **Dock**!
