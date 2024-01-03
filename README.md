# RDP Client Generator Guide

This guide explains how to use the `rdp-generator.html` file from the [rdp-client-generator](https://github.com/elijahchen/rdp-client-generator) repository to generate a Remote Desktop Protocol (RDP) client configuration file.

## How to Use the HTML File

### 1. Open the HTML File
Open the `rdp-generator.html` file in any modern web browser. This file serves as the interface for generating your RDP client configuration.

### 2. Fill in the Form
Input the necessary details in the form provided in the HTML file:

- **Server**: The address of the server you wish to connect to.
- **Username**: Your username for the RDP session.
- **Password**: Your password for the RDP session.
- **RDP File Name**: The name you want for the generated RDP file.
- **Protocol**: Select between TCP and UDP. UDP is recommended for better performance, but your experience may vary.

### 3. Generate the Client
Click the "Generate Client" button after filling in the form. The JavaScript in the HTML file will process your inputs and create an RDP file.

### 4. Download the RDP File
The browser will automatically download the RDP file with your specified name once the client is generated.

## Making a URL Request

The process of generating the RDP file is handled entirely client-side by the JavaScript in the HTML file. It involves the following steps:

1. **Form Submission Handling**: The JavaScript code intercepts the form submission, preventing the default submission event.
2. **Data Processing**: It collects the data entered in the form.
3. **RDP File Creation**: The script creates a string representing the RDP file content, converts it into a Blob object, and then generates a URL using `URL.createObjectURL(blob)`.
4. **File Download**: An anchor (`<a>`) element is programmatically created with its `href` attribute set to the Blob URL. Triggering a click on this link (`a.click()`) initiates the download of the RDP file.

This method does not involve an HTTP URL request to a server; the entire process occurs within the browser.

## Example URL Format

While the `rdp-generator.html` file does not generate a server-based URL for the RDP file, if it were to do so, the URL might look something like this:

http://example.com/generate-rdp?server=your_server&username=your_username&password=your_password&rdpFileName=your_file_name&protocol=tcp

- `your_server` would be replaced with the server address.
- `your_username` with your username.
- `your_password` with your password (I would discourage filling this out unless you know the implications).
- `your_file_name` with the desired name for the RDP file.
- `protocol` can be either `tcp` or `udp`.

Please note that there are some parameters in the html file that forces certain behavior, such as restricting the resolution and multi-monitor support.
