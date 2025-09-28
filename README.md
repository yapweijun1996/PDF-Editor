# PDF Editor - Web-Based PDF Annotation Tool

[![PDF.js Logo](https://mozilla.github.io/pdf.js/images/logo.svg)](https://mozilla.github.io/pdf.js/)

**PDF Editor** is a powerful web-based PDF annotation and editing tool built on **Mozilla's PDF.js library**. This client-side application enables comprehensive PDF editing capabilities including highlighting, annotations, drawings, stamps, and signatures - all running entirely in the browser without requiring server-side processing.

## ✨ Key Features

### 📝 Annotation & Editing Tools
- **✏️ Text Highlighting**: Highlight important text with customizable colors
- **📝 Free Text**: Add text boxes and comments anywhere on documents
- **🖌️ Ink/Draw**: Hand-drawn annotations and signatures with stylus support
- **🏷️ Stamps**: Add predefined and custom stamp images
- **✍️ Signatures**: Create and manage digital signatures

### 👁️ PDF Viewing
- **High-Fidelity Rendering**: Accurate PDF display using PDF.js canvas rendering
- **Text Selection**: Select, copy, and search text within documents
- **Thumbnail Navigation**: Visual page overview with thumbnail previews
- **Zoom & Navigation**: Smooth zooming and multi-page navigation

## 🚀 Quick Start

### Basic Setup
```html
<!DOCTYPE html>
<html>
<head>
    <title>PDF Editor</title>
    <script src="build/pdf.mjs"></script>
</head>
<body>
    <div id="viewerContainer">
        <div id="viewer" class="pdfViewer"></div>
    </div>

    <script>
        // Load and display PDF for editing
        pdfjsLib.getDocument('document.pdf').promise.then(function(pdf) {
            console.log(`PDF loaded with ${pdf.numPages} pages ready for editing`);
        });
    </script>
</body>
</html>
```

### Enable Annotation Tools
```javascript
// Configure annotation editor
const editorConfig = {
    enableHighlightFloatingButton: true,
    highlightEditorColors: "yellow=#FFFF98,green=#53FFBC,blue=#80EBFF",
    enableSignatureEditor: true
};
```

## 🛠️ Annotation Tools

### Text Highlighting
- **Multiple Colors**: Yellow, green, blue and custom colors
- **Opacity Control**: Adjustable transparency
- **Multi-Page Support**: Highlight across multiple pages

### Free Text Annotations
- **Rich Text**: Add formatted text anywhere on documents
- **Font Control**: Customize size, color, and style
- **Resizable**: Drag corners to resize text boxes

### Drawing & Ink Tools
- **Freehand Drawing**: Natural pen and stylus support
- **Line Thickness**: Adjustable stroke width
- **Color Palette**: Full color selection
- **Smooth Curves**: Intelligent curve smoothing

### Stamps & Signatures
- **Predefined Stamps**: "Approved", "Confidential", etc.
- **Custom Images**: Upload your own stamp images
- **Digital Signatures**: Draw or upload signature images
- **Signature Storage**: Save signatures for reuse

## 💡 Why PDF.js?

**PDF Editor** leverages **Mozilla's PDF.js** because it provides:

### 🛡️ Client-Side Security
- **No Server Uploads**: PDFs processed entirely in the browser
- **Privacy First**: Documents never leave your device
- **Offline Capable**: Works without internet connection

### ⚡ Performance & Compatibility
- **Zero Dependencies**: Pure JavaScript, no external libraries required
- **Universal Support**: Works in all modern browsers
- **Progressive Loading**: Pages load incrementally for better performance
- **Mobile Friendly**: Optimized for touch devices and tablets

### 🎯 Accurate Rendering
- **Pixel-Perfect Display**: Faithful reproduction of PDF content
- **Text Layer**: Enables text selection and search functionality
- **Font Support**: Embedded fonts and system font fallbacks
- **Color Accuracy**: Precise color reproduction and transparency

## 🔧 Browser Support

✅ **Desktop**: Chrome 60+, Firefox 55+, Safari 12+, Edge 79+
✅ **Mobile**: iOS Safari 12+, Chrome Mobile 60+, Firefox Mobile 55+

## 📝 License

This PDF Editor is built on **PDF.js**, which is licensed under the **Apache License 2.0**.

## 🌐 Resources

- **[PDF.js Homepage](https://mozilla.github.io/pdf.js/)** - Official PDF.js website
- **[Documentation](https://mozilla.github.io/pdf.js/api/)** - Complete API reference
- **[Examples](https://mozilla.github.io/pdf.js/examples/)** - Live examples and demos

---

**Built with ❤️ using Mozilla PDF.js**