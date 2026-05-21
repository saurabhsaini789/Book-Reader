# Walkthrough — Premium PDF Read-Aloud Web Application

We have successfully designed and built a highly polished, premium, and feature-rich single-page Web Application: **LuminaRead PDF Reader**. This application elevates the baseline PDF Read-Aloud concept into a modern E-Reader product with dynamic layout configurations, high-fidelity styles, and synchronized word-level audio-visual reading controls.

---

## 🎨 Premium Design System & Visuals

The app was developed following modern web design principles, completely using **Vanilla CSS variables** for rapid response times and beautiful, fluid theme changes:

1. **Midnight Glow (Default Dark)**: Immersive deep indigo and slate theme.
2. **Nordic Light**: Pristine white and cool slate layout with soft blue sky accents.
3. **Warm Sepia**: Traditional e-book feel with soft, low-contrast amber surfaces to minimize eye strain.
4. **Forest Moss**: Calming dark-green moss aesthetics for reading at night.
5. **Cyberpunk Neon**: Retro-futuristic dark neon mode with intense cyan text, neon rose borders, and glowing accents.

### Typography Panel
Supported by Google Fonts, the reader can easily toggle between four custom typography environments:
- **Inter Sans**: A high-legibility clean interface typeface.
- **Merriweather**: A premium literary serif face optimized for long-form screen reading.
- **Comic Neue**: An organic cursive-vibe face with outstanding character distinction.
- **OpenDyslexic**: A scientifically tuned specialized typeface with weighted bottoms to combat letter rotation and reading confusion.

---

## ⚙️ Key Technical Implementations

### 1. Synchronized Word-by-Word Narration Engine
To achieve professional-grade reading highlighting (similar to Speechify), we built a **lazy-tokenizing character index matching engine**:
* **On-Demand (Lazy) Tokenization**: Instead of tokenizing thousands of sentences at load time, which degrades browser memory, the application renders flat sentence elements. When a sentence is clicked or becomes active in the reader, its text is dynamically tokenized into individual word spans wrapped in `data-start` and `data-end` character offsets.
* **TTS Alignment via SpeechSynthesis `onboundary`**:
  ```javascript
  utt.onboundary = (event) => {
    if (event.name === 'word') {
      const charIdx = event.charIndex;
      // Lights up the exact word matching the active character boundary
    }
  }
  ```
  This calculates word positions down to the millisecond, resulting in a fluid visual highlight that matches the speaker's speed.

### 2. Multi-Tab Interactive Sidebar
A responsive sidebar slide-out includes three distinct workspaces:
* 📁 **Pages**: Maps all sentences to their original PDF pages. Displays checkboxes to mark pages as completed and highlights the current page dynamically.
* 🔖 **Bookmarks**: Allows users to double-click any sentence to bookmark it. Clicking bookmark entries instantly navigates to that sentence.
* 🔍 **Search**: Scans the entire extracted document and displays matching sentences with keywords highlighted inside `<mark>` tags. Clicking a search item navigates to that specific sentence.

### 3. Smart UX Conveniences
* **Sample Book Loader**: Includes a pre-formatted Alice in Wonderland sample, allowing users to test the application instantly with multi-page navigation and bookmarks without uploading a PDF.
* **Mini Floating Controller**: Displays a compact glassmorphic pill player at the bottom center of the page when the user scrolls deep down.
* **Sleep Timer**: A picker to auto-pause reading after 5 to 60 minutes, or at the end of the active page.
* **Keyboard Shortcuts**: Spacebar (Play/Pause), Left/Right Arrows (Skip sentence), Escape (Stop), and `B` (Toggle Bookmark).

---

## 📱 Mobile & Responsive Architecture

* Designed using dynamic viewport units (`100dvh`) to prevent safari/chrome mobile footer overlaps.
* Incorporates smooth sliding overlay panels and bottom sheets for mobile preferences.
* Mobile drag-swipe gestures allow users to easily drag down the preference sheet to dismiss it.
* Utilizes a highly robust **iOS Keep-Alive Silent Audio Loop** to maintain audio context focus when lock-screen changes or screen sleeps occur.

---

## 🔍 Validation & Verification Check

1. **Aesthetic Visual Verification**: Verified all five themes across desktop and simulated mobile devices. All transitions are butter-smooth and leak-proof.
2. **Sidebar Overlap Fix**: Successfully integrated `visibility: hidden` and a synchronized `visibility 0.35s` transition on `.sidebar.collapsed` and `.drawer` (desktop modes), ensuring that overflow tabs completely disappear during collapses, eliminating any overlapping layouts.
3. **Ergonomic Mobile-First Player**: Eliminated the redundant top `controls-strip` in mobile viewports (`display: none !important`), saving significant reading canvas space. Transitioned the compact floating control pill to be permanently locked visible at the bottom once a book is loaded, within easy reach of the thumb.
4. **Offline and PWA Support**: Verified Manifest PWA standalone app features and Cache-First Service Worker registration. Can be installed directly to home screens and loads content instantly when offline.
5. **Speech Alignments**: Lazy-tokenizer accurately matches word spans to boundaries, synchronizing audio with active glowing highlights on-the-fly.

---

## 🚀 Free PWA Deployment via GitHub Pages

Since LuminaRead is built entirely using premium, lightning-fast static HTML, JS, CSS, and manifest configuration, it is perfectly suited for **GitHub Pages**. GitHub Pages provides **free HTTPS hosting**, which is required by mobile devices to register PWA service workers and enable standalone app installation!

### Deployment Steps:

1. **Open Your Repo Settings**:
   Navigate to your GitHub repository: [saurabhsaini789/Book-Reader](https://github.com/saurabhsaini789/Book-Reader).
2. **Access Pages**:
   On the top menu bar, click on **Settings** (the gear icon). On the left-side sidebar, scroll down to the "Code and automation" section and click on **Pages**.
3. **Configure Branch**:
   * Under the **Build and deployment** section, verify the source is set to **Deploy from a branch**.
   * Under **Branch**, select `main` from the dropdown list (it will default to `None`).
   * Leave the directory as `/ (root)` and click **Save**.
4. **App is Live!**:
   GitHub will automatically run an Actions build workflow (takes ~45 seconds). Once complete, your premium PWA will be securely hosted and live at:
   👉 **`https://saurabhsaini789.github.io/Book-Reader/`**

Open this link in Safari on your iPhone (tap "Add to Home Screen") or Chrome on Android to install **LuminaRead** as a native app on your phone!
