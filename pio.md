---
layout: default
---

*   [Project Overview](./)
*   [Development](./dev.html)
*   [Challenges](./challenges.html)
*   **PIO**
*   [Retrospective](./retrospective.html)

# PIO

For this project the Programmable IO (PIO) feature of the RP2040 was used to read in image data from the camera. The PIO program is selectively enabled capture a single frame at a time when requested by the main program.
After the PIO state machine is activated, it waits for a high state on the hsync (horizontal sync) pin, followed by a high state on the pixelclock pin. Then it waits for the pixel clock to return to 0. This results in one bit being read for each cycle of the clock pin. 
A DMA channel is set up to transfer the read data from the PIO RX FIFO to the data buffer specified in the configuration struct passed to the `arducam_capture_frame()` function.

While this particular application does not demonstrate it fully (since the frame capture function waits in the main thread for the vertical sync pin), the capability of the PIO to execute IO operations asynchronously with the main processor can be a very powerful feature. The PIO program used here could be improved to include this vsync wait, allowing the main thread to continue executing while the PIO waits for the start of a frame, which could result in slight performance improvements.