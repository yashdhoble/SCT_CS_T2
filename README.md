# SCT_CS_T2

1. Overview
The Advanced Pixel Encryptor is a web-based tool that allows users to apply simple, reversible cryptographic techniques to digital images directly in their browser. It provides two distinct methods for pixel manipulation: Pixel Swap, which scrambles the image by swapping adjacent pixels, and Pixel Shift, a key-based cipher that modifies the color values of each pixel. The application is built entirely with front-end technologies (HTML, Tailwind CSS, and JavaScript), making it a lightweight, serverless, and easily deployable tool.

2. User Workflow
The user interacts with the application through a simple, linear process:

Upload Image: The user clicks "Upload Image" and selects a local image file (.png, .jpg, etc.). The application then loads the image onto two HTML5 canvases: one for the "Original Image" and one for the "Processed Image."

Select Mode: The user chooses an encryption method:

Swap Pixels: A parameter-less method that shuffles pixel data.

Shift Pixels: Requires the user to input an "Encryption Key" (a number between 0 and 255).

Apply Operation:

The user clicks Encrypt. The chosen algorithm is applied to the "Processed Image" canvas.

The user clicks Decrypt. The inverse operation is applied. For "Pixel Swap," this means running the same algorithm again. For "Pixel Shift," it involves subtracting the key value.

Finalize:

Download-Processed: The user can save the modified image from the "Processed Image" canvas as a processed-image.png file.

Reset: The user can clear the entire application state to start over with a new image.

3. Core Encryption Logic
The application's logic resides in the JavaScript code, which directly manipulates the ImageData array obtained from the HTML canvas. An ImageData object is a flat array of numbers representing the RGBA (Red, Green, Blue, Alpha) values of each pixel.

applyPixelSwap():

This function iterates horizontally across each row of the image, two pixels at a time (x += 2).

For each pair of adjacent pixels, it swaps their entire RGBA data.

This method is its own inverse; running it a second time swaps the pixels back to their original positions.

applyPixelShift(value):

This function takes an integer value (the key) as input.

It iterates through every pixel in the image data.

For each pixel, it adds the value to the R, G, and B channels.

It uses modulo (%) arithmetic to ensure the color values "wrap around" the 0-255 range. For example, (250 + 10) % 256 results in 4. This is crucial for making the operation perfectly reversible.

To decrypt, the function is called with a negative value (e.g., applyPixelShift(-50)), which subtracts from the color channels and restores the original image, provided the correct key is used.
