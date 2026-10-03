# Essentials

[Knotly](https://www.knotly.com/) is an online platform for creating and visualizing crochet patterns using physics-based simulation in an interactive 3D environment. This guide walks you through the basics of using Knotly and offers helpful tips for creating and editing digital crochet projects. 

## Writing a pattern

Start with a small set of rounds or rows, and check the preview after each change. Knotly’s simulation engine parses the pattern text and then runs the simulations to produce 3d previews for your pattern.

Although the pattern editor can detect some basic syntax errors as you type, it may not catch every issue, especially problems with stitch placement or shaping. Keeping instructions concise and previewing your work after each change is highly recommended. Working in small sections makes the pattern easier to review, helps isolate errors, and allows you to correct shaping issues before they affect later rows or rounds.

Remember to save your work regularly to avoid losing your progress.

> [!TIP]
> - Use the editor’s formatting tool to keep your pattern text clean and readable
> - Use the notation controls to keep terminology consistent throughout your project

## Running simulations

Knotly’s simulations are physics-based. While this approach produces more realistic results, each simulation requires substantial computation and many iterations. Behind the scenes, Knotly’s physics engine continuously monitors and optimizes the process to deliver the best possible results as quickly as possible. It handles the complexity for you, so you do not need to understand the underlying iteration process or wrestle with tedious simulation settings.

For smaller projects, you can watch the model take shape almost instantly. Larger or more structurally complex projects may take a few seconds to simulate, depending on your device’s performance.

It is also worth noting that each part in a project is simulated independently. Parts generally do not affect one another unless they are connected by sewing or joining. Once connected, the involved parts are treated as a single assembly during simulation. You can simulate multiple parts at once in a single project, with the practical limit depending on your device’s performance.

## Working with render modes

Knotly can render your pattern text as 3D models in three modes: **Sketch**, **Chart**, and **Realistic**. Switch between them to examine and evaluate different aspects of the same pattern:

- **Sketch mode** renders stitches as simplified lines, making the structure and direction of your work easier to see. It also helps you distinguish between the front (shown in light blue) and back sides (shown in light grey). Like a blueprint, it provides a clear structural overview that helps you identify shaping issues at the design stage. <br>While color previews are available in this mode, enabling them is not recommended as they can obscure the distinction between front and back sides and make the structure harder to interpret.

- **Chart mode** renders stitches using standard crochet chart symbols commonly used by crocheters worldwide. This makes it easier to identify stitch types and understand their relative positions. It is also a great way to share your pattern, as graphical symbols provide a more universal and efficient way to communicate crochet ideas than text-based instructions. <br>In this mode, colors may appear slightly different from what have been specified in the pattern text to ensure that chart symbols remain easy to read.

- **Realistic mode**, on the other hand, renders your work using lifelike yarn materials, providing a more detailed and accurate preview of how your finished project may look. It helps you visualize the overall appearance and texture of your design before reaching to your yarns. It is also worth noting that color previews are most accurate in this mode.

> [!NOTE]
> Future updates to **Realistic mode** will allow you to choose from different yarn types, providing a more accurate preview based on the yarn you plan to use.

## Inspecting stitches

To trace a stitch back to its place in the pattern and understand how the pattern maps to the 3D preview, activate **inspection mode** by either *double-clicking* an object or selecting it and pressing <kbd>Space</kbd> or <kbd>Enter</kbd>. Inspection is available in all three render modes above.

In inspection mode, hover over or tap on a stitch to display a popover showing its part, row number, position within the row, and stitch type.


> [!NOTE]
> Future updates to the **inspection mode** will link each hovered stitch to its corresponding occurrence in the original pattern text.

## Selecting, moving, rotating an object

Switch between the transform tools to select, move, or rotate one or more objects:

- **Select tool** lets you select objects without displaying transform controls. Click an object to select it, or click an empty area to clear the selection. Use the arrow keys to cycle through objects.

- **Move tool** displays translation controls for the selected objects. Drag the center control to move them across the screen plane, or drag an axis handle to constrain movement to that axis. Hold <kbd>Shift</kbd> while dragging to snap movement to the grid.

- **Rotate tool** displays rotation controls for the selected objects. Drag the center control to rotate them freely, or drag an axis ring to rotate them around that axis. Hold <kbd>Shift</kbd> while dragging to snap the rotation to 45-degree increments.

> [!WARNING]
> Changing a part’s code resets any saved position and rotation data for that part. Since sewing, joining, and other similar operations create a new object with a compound code, they also reset the saved transform data for the affected parts.

Hold <kbd>Shift</kbd> while clicking to add objects to or remove them from the current selection. Selected objects can be moved or rotated together. Press <kbd><kbd>Ctrl</kbd> + <kbd>A</kbd></kbd> — or <kbd><kbd>Command</kbd> + <kbd>A</kbd></kbd> on macOS — to select all objects.

When the **Move** or **Rotate** tool is active, use arrow keys to make small adjustments. Hold <kbd>Alt</kbd> — or <kbd>Option</kbd> on macOS — to temporarily switch between the **Move** and **Rotate** tools.
