# Pixel Art Grid & Palette Generator

An online tool designed for pixel art enthusiasts to quickly generate an enlarged preview image with a grid and color palette for your pixel art creations (e.g., 16x16, 32x32), with support for adding custom watermarks.

This project is based on a pure front-end implementation. All image processing is done in the user's browser, ensuring speed and user data privacy.

## ✨ Key Features

- **Upload PNG Images**: Supports uploading small-sized pixel art PNG files.
- **Image Scaling**: Customizable scaling factor (from 2x to 32x) while keeping pixel edges crisp.
- **Grid Generation**: Automatically draws a pixel-aligned grid on the enlarged image.
- **Palette Extraction**: Automatically analyzes and displays all colors used in the artwork.
- **Custom Watermark**: Allows users to input text as a watermark and adjust its opacity.
- **Multi-language Support**: Automatically adapts to Simplified Chinese, Traditional Chinese, and English interfaces.
- **Settings Persistence**: Automatically saves user settings for the scaling factor, watermark text, and opacity locally.
- **Client-Side Processing**: All operations are performed in the browser, with no need for server uploads, ensuring fast responses and protecting user privacy.
- **One-Click Download**: Download the final image, complete with grid, palette, and watermark, to your local machine.

## 🚀 Technical Implementation

This tool is built entirely with HTML, CSS, and vanilla JavaScript, with no external frameworks.

### Design Principles
1.  **Simple and Intuitive**: The UI design follows a minimalist approach, allowing users to understand the core workflow immediately: "Upload -> Configure -> Download".
2.  **Purely Client-Side**: Image processing is handled entirely in the user's browser via JavaScript, offering three main advantages:
    - **Fast**: No network uploads mean processing is instantaneous.
    - **Private**: The user's artwork data never leaves their local computer.
    - **Low Cost**: No need for server storage or computing resources.
3.  **Instant Feedback**: Any user action (like adjusting the scale or entering a watermark) is immediately reflected in the preview area (WYSIWYG).

### Core Logic
1.  **File Reading**: Uses the `FileReader` API to asynchronously read the user-uploaded PNG file.
2.  **Color Extraction**:
    - The uploaded image is drawn onto an offscreen `<canvas>`.
    - `getImageData()` is used to retrieve the RGBA data for every pixel.
    - The pixel data is iterated through, and color values are stored in a `Set` object to automatically handle deduplication, thus generating the color palette.
3.  **Image Scaling and Grid Drawing**:
    - On the main display `<canvas>`, image smoothing is first disabled (`imageSmoothingEnabled = false`), which is crucial for maintaining sharp pixel edges.
    - The original image is drawn onto the main canvas at the specified scaling factor.
    - The step size is calculated based on the scaling factor, and horizontal and vertical lines are drawn in a loop to form the grid.
4.  **Watermark and Final Image Composition**:
    - After the image and grid are drawn, the watermark text is rendered based on user input.
    - All elements—palette swatches, a white border, etc.—are drawn onto the same canvas to create the final, complete image.
5.  **Internationalization (i18n)**:
    - A JavaScript object is created to hold text in multiple languages.
    - `navigator.language` is used to detect the user's browser language and dynamically update the text content on the page.
6.  **State Persistence**:
    - `localStorage` is used to save user settings (like scaling factor, watermark text, etc.) in the browser.
    - These settings are automatically loaded when the page starts, restoring the user's last session state.
7.  **Download Generation**:
    - The `canvas.toDataURL('image/png')` method is called to convert the final rendered canvas content into Base64-encoded image data.
    - This data is assigned to the `href` attribute of an `<a>` tag, and its `download` attribute is set to enable file download. 