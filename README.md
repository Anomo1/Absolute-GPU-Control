Absolute GPU Control 🚀
A powerful browser extension for Chrome, Opera GX, Edge, and Brave that allows you to block WebGL and GPU acceleration on a per-tab basis.
⚠️ The Honest Technical Note:
This extension does not force "Software Rendering" (CPU mode) for a specific tab. That is technically impossible for browser extensions to do on a per-tab basis.
Instead, this extension completely blocks 3D Contexts (WebGL).
Global Browser Setting OFF: 3D content runs on your CPU (Laggy/Slow).
This Extension: 3D content is killed entirely (Black screen/Element removed/Zero lag).
Use this extension if you want to stop a website from eating your resources, spinning up your fans, or draining your battery.
✨ Features
Per-Tab Control: Toggle GPU/WebGL access for the specific site you are looking at.
Persistent Block List: Remembers which domains should always have acceleration disabled.
"Nuclear" Injection: Uses document_start injection to kill WebGL before the website even loads (prevents site crashes).
System Status Check: Detects if your global browser settings have already disabled the GPU.
Context Menu: Right-click anywhere on a page to quickly toggle acceleration.
Visual Feedback: Shows a red "OFF" badge on the icon when a site is blocked.
📂 Installation (Developer Mode)
Since this extension is not yet on the Chrome Web Store, you need to install it manually ("Load Unpacked").
Step 1: Download the Source
Clone this repository or download the ZIP.
Extract the files into a folder (e.g., named gpu-control).
Ensure the folder contains manifest.json, background.js, etc.
Step 2: Install in Chrome / Edge / Brave
Open your browser and navigate to chrome://extensions.
Toggle Developer mode in the top-right corner.
Click the Load unpacked button (usually top-left).
Select the folder containing the extension files.
Step 3: Install in Opera GX
Open Opera GX and navigate to opera://extensions.
Toggle Developer mode in the top-right corner.
Click Load unpacked.
Select the folder containing the extension files.
🎮 How to Use
Pin the Extension: Click the puzzle piece icon in your browser toolbar and pin "Absolute GPU Control."
Visit a 3D Site: Go to a site like get.webgl.org or webglsamples.org.
Toggle It:
Click the extension icon.
Click "DISABLE ACCELERATION".
The page will reload automatically.
Verify: The 3D content (like the spinning cube or fish) should disappear or show an error message. This means your GPU is no longer processing that tab.
🛠️ Technical Details
This extension operates by injecting a script into the MAIN world of the DOM. It overwrites the following browser prototypes:
HTMLCanvasElement.prototype.getContext
OffscreenCanvas.prototype.getContext
Deletes window.WebGLRenderingContext
Deletes window.WebGL2RenderingContext
This forces websites to fail their "Feature Detection" checks, causing them to disable their 3D engines immediately.
📝 License
This project is open-source. Feel free to modify and distribute it.