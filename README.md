# MFA Editor

> **High-Performance Visual & HTML Code Rich Text Editor**  
> Created and maintained by **Mir Faisal Ahmad**  
> Package: `@mirfaisalahmad/editor`

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](package.json)
[![Author](https://img.shields.io/badge/author-Mir%20Faisal%20Ahmad-emerald.svg)](https://github.com/mirfaisalahmad)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

**MFA Editor** is a standalone, browser-native dual-mode rich text editor. It provides a polished **Visual (WYSIWYG)** writing canvas alongside an authentic **HTML / Code** editor tab with seamless state synchronization.

It has zero backend dependencies, requires no server-side runtime or database, and can be embedded into any modern web stack (React, Vue, Next.js, Svelte, Angular, Laravel, Django, Express, or static HTML).

---

## ✨ Features

- ⚡ **Dual-Mode Editing:** Seamlessly toggle between **Visual Mode** (rich formatting toolbar) and **Text Mode** (raw HTML editing with Quicktags).
- 🎨 **Modern Formatting Suite:** Headings, blockquotes, ordered/unordered lists, text alignment, colors, strikethrough, links, special characters, and code formatting.
- 🎛️ **Expandable Toolbars:** Built-in multi-tier toolbar toggle for clean and distraction-free writing.
- 📦 **Zero Backend Overhead:** 100% client-side execution in vanilla JavaScript.
- 🚀 **Framework Agnostic:** Easily mounts onto standard `<textarea>` elements in any frontend ecosystem.
- 🔌 **Extensible API:** Full programmatic control to retrieve HTML, update content, switch modes, and bind event handlers.

---

## 📁 Package Structure

```text
mfa-editor/
├── index.html                       # Live Interactive Demo & Playground
├── package.json                     # NPM Package Configuration (@mirfaisalahmad/editor)
├── README.md                        # Documentation & Developer Guide
└── assets/
    ├── css/
    │   ├── dashicons.min.css        # Clean vector icon suite
    │   ├── buttons.min.css          # Toolbar and action button styling
    │   └── mfa-editor.min.css       # Core MFA Editor layout and canvas styles
    ├── fonts/                       # Icon font files (woff2, woff, ttf, eot)
    │   ├── dashicons.woff2
    │   ├── dashicons.woff
    │   └── dashicons.ttf
    └── js/
        ├── jquery.min.js            # Bundled helper library
        ├── mfa-editor.js            # Primary MFA Editor engine, API & tab controller
        ├── quicktags.min.js         # Text/HTML mode formatting toolbar
        └── tinymce/                 # Visual rich text engine
            ├── wp-tinymce.js        # Core WYSIWYG runtime bundle
            ├── themes/modern/       # Modern UI theme
            ├── skins/lightgray/     # UI chrome skin
            └── skins/wordpress/     # Canvas iframe typography styles
```

---

## 🚀 Quick Start Guide

### 1. Include the Stylesheets in `<head>`
```html
<link rel="stylesheet" href="assets/css/dashicons.min.css">
<link rel="stylesheet" href="assets/css/buttons.min.css">
<link rel="stylesheet" href="assets/css/mfa-editor.min.css">
```

### 2. Add the Target Textarea
```html
<textarea id="my_editor" name="my_editor" rows="16" class="mfa-editor-area">
    <h2>Welcome to MFA Editor</h2>
    <p>Start writing rich content here...</p>
</textarea>
```

### 3. Load the Script Dependencies
```html
<!-- Runtime Scripts -->
<script src="assets/js/jquery.min.js"></script>
<script src="assets/js/mfa-editor.js"></script>
<script src="assets/js/tinymce/wp-tinymce.js"></script>
<script src="assets/js/quicktags.min.js"></script>
```

### 4. Initialize the Editor
```html
<script>
$(document).ready(function() {
    MFAEditor.init('my_editor', {
        tinymce: {
            wpautop: true,
            toolbar1: 'formatselect,bold,italic,bullist,numlist,blockquote,alignleft,aligncenter,alignright,link,fullscreen,wp_adv',
            toolbar2: 'strikethrough,hr,forecolor,pastetext,removeformat,charmap,outdent,indent,undo,redo'
        },
        quicktags: {
            buttons: 'strong,em,link,block,del,ins,img,ul,ol,li,code,more,close'
        }
    });
});
</script>
```

---

## 🛠️ Programmatic API Reference

MFA Editor provides a simple, high-level JavaScript API via the global `MFAEditor` namespace.

### Retrieve Content
Extracts the latest HTML markup from the editor (automatically synchronizes from Visual or Text mode):
```javascript
var html = MFAEditor.getContent('my_editor');
console.log(html);
```

### Update Content
Updates the editor content programmatically across both Visual and Code views:
```javascript
MFAEditor.setContent('my_editor', '<h2>New Heading</h2><p>Updated content body.</p>');
```

### Switch Editing Tabs
Toggles or specifies the active mode (`'tmce'` for Visual, `'html'` for Code):
```javascript
// Switch to Visual (WYSIWYG) mode
MFAEditor.switchTab('my_editor', 'tmce');

// Switch to Text (HTML Code) mode
MFAEditor.switchTab('my_editor', 'html');

// Toggle between modes
MFAEditor.switchTab('my_editor', 'toggle');
```

### Destroy / Cleanup Instance
Cleans up event listeners and DOM elements before unmounting:
```javascript
MFAEditor.remove('my_editor');
```

---

## 🖼️ Image Upload & Asset Management

For handling custom image uploads (e.g., S3, Cloudinary, or a custom API endpoint), connect a file input or drag-and-drop handler to `MFAEditor`:

```javascript
function uploadImageAndInsert(file) {
    const formData = new FormData();
    formData.append('image', file);

    fetch('/api/upload', {
        method: 'POST',
        body: formData
    })
    .then(res => res.json())
    .then(data => {
        // Insert uploaded image directly into the editor
        const currentHtml = MFAEditor.getContent('my_editor');
        const imgTag = `<img src="${data.url}" alt="${file.name}" style="max-width:100%; height:auto;" />`;
        MFAEditor.setContent('my_editor', currentHtml + imgTag);
    })
    .catch(err => console.error('Upload failed:', err));
}
```

---

## 📦 NPM Installation (When Published)

```bash
# Using npm
npm install @mirfaisalahmad/editor

# Using yarn
yarn add @mirfaisalahmad/editor

# Using pnpm
pnpm add @mirfaisalahmad/editor
```

---

## 🌐 Running the Demo Playground Locally

To test the interactive playground, launch any static web server in the project folder:

```powershell
# Using Node.js
npx serve .

# Using Python
python -m http.server 5500
```

Then visit `http://localhost:5500` to interact with the live editor.

---

## 👤 Author

**Mir Faisal Ahmad**  
- GitHub: [@mirfaisalahmad](https://github.com/mirfaisalahmad)
- Project: MFA Editor (`@mirfaisalahmad/editor`)

## 📄 License

This project is open-source and licensed under the [MIT License](LICENSE).
