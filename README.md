# Absolute GPU Control

![Version](https://img.shields.io/badge/version-4.0-blue.svg?style=flat-square) ![Manifest](https://img.shields.io/badge/manifest-v3-green.svg?style=flat-square) ![Size](https://img.shields.io/badge/size-42kb-yellow.svg?style=flat-square)

> *Stop heavy websites from draining your battery. Kill the lag by killing the graphics engine.*

After seeing many users struggle with browser settings that are "all or nothing," I built this extension to solve a specific problem: sometimes you just want **one** specific tab to stop eating your GPU resources, while keeping the rest of your browser fast.

*This tool is geared towards gamers, developers, and battery-conscious users who need granular control over their browser's hardware acceleration.*

## 🌟 Highlights

I think a *"Highlights"* section is crucial to understand why this exists. Here are the main selling points:

- **True "Nuclear" Option:** It doesn't just ask the browser nicely; it forcefully removes 3D capabilities from the page.
- **Zero Lag:** Unlike "Software Rendering" (which puts load on your CPU), this extension simply stops the rendering entirely.
- **Per-Tab Memory:** It remembers which domains you've blocked, so they stay blocked.
- **Visual Feedback:** A clear red "OFF" badge on the icon so you know when the GPU is inactive.
- **Context Menu:** Right-click anywhere to toggle acceleration instantly.
- **Dark Mode UI:** Designed to look native on Opera GX and modern browsers.

## ℹ️ Overview

> *Most people think disabling Hardware Acceleration makes things slow. They are right. This extension does something different.*

A good tool needs to be honest about what it does. When you turn off Hardware Acceleration in your browser settings, your computer switches to "Software Mode," forcing your CPU to do the heavy lifting. This often results in a laggy, hot, and slow experience.

**Absolute GPU Control** does not force Software Mode. Instead, it injects code before the website loads to delete the 3D Contexts (`WebGL`) entirely.

### ⚡ The Difference

| Method | Result | Performance |
| :--- | :--- | :--- |
| **Browser Settings OFF** | CPU tries to render 3D | 🐢 Slow, Hot, Laggy |
| **This Extension** | 3D rendering is killed | ⚡ Fast, Cool, Silent |

### 🛑 Who is this for?

Use this if you are visiting a website that makes your fans spin up, drains your battery, or is unoptimized, and you just want the 3D elements to **stop**.

## 🚀 Usage instructions

> *Click. Block. Done.*

Using the extension is designed to be as fast as possible.

1.  **Pin the Extension:** Click the puzzle piece icon in your browser toolbar and pin "Absolute GPU Control."
2.  **Visit a 3D Site:** Go to a site like [webglsamples.org](https://webglsamples.org/aquarium/aquarium.html).
3.  **Toggle It:** Click the extension icon and hit **"DISABLE ACCELERATION"**.
4.  **Verify:** The page will reload, and the 3D content will vanish.

![Screenshot Placeholder](https://via.placeholder.com/600x300.png?text=Extension+UI+Screenshot+Here)

*You can also right-click anywhere on a page and select **"Toggle GPU Acceleration"** for even faster control.*

## ⬇️ Installation instructions

> *Since this is a specialized tool, you will need to install it via Developer Mode for now.*

Having simple, understandable installation instructions is important. Here is the one-minute setup guide.

### Step 1: Download
1.  **Clone** this repository or **Download ZIP**.
2.  Extract the files into a folder named `gpu-control`.
3.  Verify the folder contains `manifest.json`.

### Step 2: Load into Browser

**For Chrome, Edge, & Brave:**
1.  Navigate to `chrome://extensions`.
2.  Toggle **Developer mode** (top-right corner).
3.  Click **Load unpacked**.
4.  Select your `gpu-control` folder.

**For Opera GX:**
1.  Navigate to `opera://extensions`.
2.  Toggle **Developer mode**.
3.  Click **Load unpacked**.
4.  Select your folder.

## 🛠️ Technical Details

For the developers and curious minds, here is how the magic happens under the hood.

The extension uses `manifest v3` and injects a script into the `MAIN` world of the DOM at `document_start`. It aggressively overwrites the browser's native prototypes to fail feature detection:

```javascript
// The "Nuclear" Logic
HTMLCanvasElement.prototype.getContext = function(type) {
    // If the site asks for 3D, we say "No"
    if (type === 'webgl' || type === 'webgl2') return null;
    return oldGetContext.apply(this, arguments);
};

// Removing Constructors entirely
delete window.WebGLRenderingContext;
delete window.WebGL2RenderingContext;