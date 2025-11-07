# RDP Client Generator Guide

This guide explains how to use the `rdp-generator.html` file from the [rdp-client-generator](https://github.com/elijahchen/rdp-client-generator) repository to generate a Remote Desktop Protocol (RDP) client configuration file.

## How to Use the HTML File

### Method 1: Manual Form Entry

1. **Open the HTML File**: Open the `rdp-generator.html` file in any modern web browser.

2. **Fill in the Form**: Input the necessary details:
   - **Server** (required): The address of the server you wish to connect to
   - **Username** (required): Your username for the RDP session
   - **RDP File Name** (required): The name you want for the generated RDP file
   - **Protocol**: Select between TCP (default) and UDP. UDP may offer better performance, but experience may vary
   - **Port**: The RDP port (defaults to 3389)

3. **Generate the Client**: Click the "Generate Client" button. The browser will automatically download the RDP file.

### Method 2: URL Parameters (Click-to-Download)

You can pre-fill the form or automatically download an RDP file by passing parameters in the URL. This is perfect for creating shareable links.

**Minimum Required Parameters:**
- `server` - The RDP server address
- `username` - The username for the RDP session

**Optional Parameters:**
- `rdpFileName` or `filename` - Custom name for the RDP file (defaults to server name)
- `protocol` - Either `tcp` or `udp` (defaults to `tcp`)
- `port` - The RDP port (defaults to `3389`)
- `autoDownload` or `auto` - Set to `false` or `0` to pre-fill form without auto-downloading

**Example URLs:**

Basic auto-download (minimal parameters):
```
file:///path/to/rdp-generator.html?server=example.com&username=john
```

Full parameters with custom settings:
```
file:///path/to/rdp-generator.html?server=remote.company.com&username=john.doe&filename=work-pc&protocol=udp&port=3389
```

Pre-fill form without auto-downloading:
```
file:///path/to/rdp-generator.html?server=example.com&username=john&autoDownload=false
```

Custom port example:
```
file:///path/to/rdp-generator.html?server=192.168.1.100&username=admin&port=3390
```

**When hosted on a web server, replace `file:///path/to/` with your server URL:**
```
https://example.com/rdp-generator.html?server=remote.example.com&username=john
```

## Making a URL Request

The process of generating the RDP file is handled entirely client-side by the JavaScript in the HTML file. It involves the following steps:

1. **Form Submission Handling**: The JavaScript code intercepts the form submission, preventing the default submission event.
2. **Data Processing**: It collects the data entered in the form.
3. **RDP File Creation**: The script creates a string representing the RDP file content, converts it into a Blob object, and then generates a URL using `URL.createObjectURL(blob)`.
4. **File Download**: An anchor (`<a>`) element is programmatically created with its `href` attribute set to the Blob URL. Triggering a click on this link (`a.click()`) initiates the download of the RDP file.

This method does not involve an HTTP URL request to a server; the entire process occurs within the browser.

## RDP File Configuration

The generated RDP file includes optimized settings for performance:

- **Resolution**: 1280x960 with smart sizing enabled
- **Color Depth**: 16-bit for reduced bandwidth
- **Visual Effects**: Disabled (wallpaper, window dragging, animations, themes) for better performance
- **Audio**: Disabled by default
- **Device Redirection**: COM ports, smart cards, and POS devices are disabled
- **Multi-monitor**: Configured for single monitor use

These settings prioritize performance and reduced bandwidth usage, making it ideal for remote connections over various network conditions.

## Security Considerations

- **No Password Storage**: This generator does NOT include password fields. Passwords should never be stored in RDP files.
- **Client-Side Only**: All processing happens in your browser - no data is sent to any server.
- **Safe to Share**: URLs with parameters can be safely shared as they don't contain sensitive credentials.
