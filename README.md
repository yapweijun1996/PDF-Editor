# PDF.js - JavaScript PDF Library

[![PDF.js Logo](https://mozilla.github.io/pdf.js/images/logo.svg)](https://mozilla.github.io/pdf.js/)

**PDF.js** is a Portable Document Format (PDF) viewer that is built with HTML5. It is community-driven and supported by Mozilla. Our goal is to create a general-purpose, web standards-based platform for parsing and rendering PDFs.

## 🚀 Features

### Core Functionality
- **PDF Rendering**: High-fidelity rendering of PDF documents in web browsers
- **Text Selection**: Select and copy text from PDF documents
- **Search**: Find text within PDF documents with highlighting
- **Zoom**: Multiple zoom levels and fit-to-page options
- **Navigation**: Page-by-page navigation with thumbnails and bookmarks

### Advanced Features
- **Annotation Editor**: Add and edit annotations including:
  - Text highlights
  - Free text annotations
  - Ink/draw annotations
  - Stamp annotations
  - Signature annotations
- **Form Support**: Interactive form filling capabilities
- **Layer Support**: Optional content group (OCG) layer visibility
- **Attachment Viewer**: View PDF attachments and embedded files
- **Presentation Mode**: Fullscreen presentation viewing
- **Print Support**: High-quality PDF printing

### Accessibility & Internationalization
- **Screen Reader Support**: ARIA labels and semantic structure
- **Keyboard Navigation**: Full keyboard accessibility
- **Internationalization**: Support for multiple languages
- **RTL Language Support**: Right-to-left text direction support
- **High Contrast Mode**: Support for accessibility color schemes

## 📦 Installation

### CDN
```html
<script src="https://mozilla.github.io/pdf.js/build/pdf.mjs"></script>
```

### NPM
```bash
npm install pdfjs-dist
```

### Build from Source
```bash
git clone https://github.com/mozilla/pdf.js.git
cd pdf.js
npm install
npm run build
```

## 🛠️ Usage

### Basic Example
```html
<!DOCTYPE html>
<html>
<head>
    <title>PDF.js Example</title>
    <script src="build/pdf.mjs"></script>
</head>
<body>
    <div id="viewerContainer">
        <div id="viewer" class="pdfViewer"></div>
    </div>

    <script>
        // Load PDF document
        pdfjsLib.getDocument('example.pdf').promise.then(function(pdf) {
            // Render PDF pages
            for (let pageNum = 1; pageNum <= pdf.numPages; pageNum++) {
                pdf.getPage(pageNum).then(function(page) {
                    const viewport = page.getViewport({scale: 1.0});
                    const canvas = document.createElement('canvas');
                    const context = canvas.getContext('2d');

                    canvas.height = viewport.height;
                    canvas.width = viewport.width;

                    const renderContext = {
                        canvasContext: context,
                        viewport: viewport
                    };

                    page.render(renderContext);
                    document.getElementById('viewer').appendChild(canvas);
                });
            }
        });
    </script>
</body>
</html>
```

### Advanced Configuration
```javascript
const loadingTask = pdfjsLib.getDocument({
    url: 'document.pdf',
    cMapUrl: 'cmaps/',
    cMapPacked: true,
    enableXfa: true,
    verbosity: 0
});
```

## 🏗️ Architecture

### Core Components
- **PDF.js Core**: PDF parsing and rendering engine
- **PDF.js Web**: Complete web viewer implementation
- **Worker**: Background processing for PDF operations
- **CMap Files**: Character encoding support for international text
- **Standard Fonts**: Embedded fonts for PDF rendering

### Module Structure
```
pdf.js/
├── build/                 # Compiled modules
│   ├── pdf.mjs           # Main PDF.js library
│   ├── pdf.worker.mjs    # Web worker for PDF processing
│   └── pdf.sandbox.mjs   # Scripting sandbox
├── web/                  # Web viewer application
│   ├── viewer.mjs       # Main viewer application
│   ├── viewer.css       # Styles and theming
│   ├── cmaps/           # Character map files
│   └── standard_fonts/  # Standard PDF fonts
└── src/                 # Source code
```

## 🌐 Browser Support

PDF.js supports all modern browsers:
- Chrome/Chromium 60+
- Firefox 55+
- Safari 12+
- Edge 79+

### Mobile Support
- iOS Safari 12+
- Chrome Mobile 60+
- Firefox Mobile 55+

## 🔧 Configuration Options

### Rendering Options
```javascript
const options = {
    // Canvas rendering options
    maxCanvasPixels: 5242880,
    maxCanvasDim: 32767,

    // Performance options
    enableHWA: true,
    enableOptimizedPartialRendering: false,

    // Text handling
    disableFontFace: false,
    useSystemFonts: true,

    // Accessibility
    enableAltText: true,
    textLayerMode: 'enable'
};
```

### Viewer Options
```javascript
const viewerOptions = {
    // UI Configuration
    toolbarDensity: 0,        // 0=normal, 1=compact, 2=touch
    sidebarViewOnLoad: -1,    // -1=auto, 0=none, 1=thumbs, 2=outline
    scrollModeOnLoad: -1,     // -1=auto, 0=vertical, 1=horizontal, 2=wrapped
    spreadModeOnLoad: -1,     // -1=auto, 0=none, 1=odd, 2=even

    // Feature toggles
    enableComment: true,
    enableSignatureEditor: false,
    enableHighlightFloatingButton: false,
    enableUpdatedAddImage: false
};
```

## 🎨 Theming

PDF.js supports multiple themes and color schemes:

### Light Theme (Default)
```css
:root {
    --main-color: rgb(249 249 250);
    --body-bg-color: rgb(42 42 46);
    --toolbar-bg-color: rgb(56 56 61);
}
```

### Dark Theme
```css
@media (prefers-color-scheme: dark) {
    :root {
        --main-color: rgb(12 12 13);
        --body-bg-color: rgb(212 212 215);
    }
}
```

### High Contrast Mode
```css
@media screen and (forced-colors: active) {
    :root {
        --focus-ring-color: CanvasText;
        --outline-color: CanvasText;
    }
}
```

## 🌍 Internationalization

PDF.js supports multiple languages with Fluent localization:

```javascript
// Supported locales
const locales = [
    'en-US', 'es-ES', 'fr-FR', 'de-DE',
    'it-IT', 'pt-BR', 'ru-RU', 'ja-JP',
    'ko-KR', 'zh-CN', 'zh-TW', 'ar-SA'
];

// Initialize with locale
const l10n = new FluentBundle(locale);
```

## 🔒 Security

### Content Security Policy (CSP)
```html
<meta http-equiv="Content-Security-Policy" content="
    default-src 'self';
    script-src 'self' 'unsafe-inline';
    style-src 'self' 'unsafe-inline';
    img-src 'self' data: blob:;
    font-src 'self' data:;
    object-src 'none';
    base-uri 'self';
">
```

### Sandboxing
PDF.js uses multiple sandboxing techniques:
- **Worker Isolation**: PDF processing in separate worker threads
- **Origin Separation**: Strict origin checking for file URLs
- **CSP Compliance**: Content Security Policy compatibility

## 📊 Performance

### Optimization Features
- **Progressive Loading**: Pages load incrementally
- **Canvas Pooling**: Reuses canvas elements for better performance
- **Lazy Initialization**: Components initialize only when needed
- **Memory Management**: Automatic cleanup of unused resources

### Performance Tuning
```javascript
// Optimize for large documents
const options = {
    disableAutoFetch: false,        // Enable progressive loading
    disableRange: false,           // Enable HTTP range requests
    disableStream: false,          // Enable streaming
    maxImageSize: 1024 * 1024,     // Limit image cache size
    verbosity: 0                   // Reduce console output
};
```

## 🧪 Testing

### Running Tests
```bash
# Unit tests
npm test

# Integration tests
npm run test:integration

# Visual regression tests
npm run test:visual
```

### Test Coverage
- **Unit Tests**: Core functionality testing
- **Integration Tests**: Full viewer testing
- **Visual Tests**: Screenshot-based regression testing
- **Accessibility Tests**: Screen reader compatibility

## 🤝 Contributing

### Development Setup
```bash
git clone https://github.com/mozilla/pdf.js.git
cd pdf.js
npm install
npm start
```

### Code Style
- **JavaScript**: ES6+ with JSDoc documentation
- **CSS**: Modern CSS with custom properties
- **HTML**: Semantic HTML5 markup

### Pull Request Process
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## 📜 License

PDF.js is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.

## 🆘 Support

### Documentation
- [Official Documentation](https://mozilla.github.io/pdf.js/)
- [API Reference](https://mozilla.github.io/pdf.js/api/)
- [Examples](https://mozilla.github.io/pdf.js/examples/)

### Community
- [GitHub Issues](https://github.com/mozilla/pdf.js/issues)
- [Mailing List](https://groups.google.com/forum/#!forum/mozilla.dev.pdf-js)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/pdf.js)

### Reporting Bugs
When reporting bugs, please include:
- PDF.js version
- Browser and version
- Steps to reproduce
- Expected vs actual behavior
- Sample PDF file (if applicable)

## 🔄 Version History

### v5.4.0 (Current)
- Enhanced annotation editor
- Improved accessibility support
- Performance optimizations
- Bug fixes and stability improvements

### Previous Versions
- **v4.x**: Major architecture updates
- **v3.x**: Modern JavaScript conversion
- **v2.x**: Initial ES6 migration
- **v1.x**: Original implementation

## 🙏 Acknowledgments

PDF.js is made possible by:
- Mozilla Foundation and community contributors
- The broader web standards community
- Open source contributors worldwide

---

**Made with ❤️ by the PDF.js community**