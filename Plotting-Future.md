

This page provides a central location for future plotting goals.

Also see [BastiThoughtsOnPlotting Basti's thoughts], where Basti has made some good points and others have commented on them.

# Interfaces (External)

## Object Interface

#### Encapsulate Everything in Properties

#### Expose Properties in Logical Locations

## Window Interface

### Keyboard

#### 1-0 toggle p`[`n`]`.visible

#### Option for rotation in model (vs. view) Coordinate System

### Mouse

## Plot Objects

### Axes

### Grids

# Design (Internal)

## Class Hierarchy

## Rendering Control Flow

## Function Representation

#### Separation of Calculation and Display Code

2D and 3D calculation is a pattern that should be factored out of PlotCurve, PlotSurface, and the corresponding color calculation functions.

#### Support for Dynamic Level-of-Detail

In other words, be able to recalculate the display vertices for different zoom levels and perspectives dynamically, rather than calculating them once when the function is added to the plot.

## Window-less Plots

The ability to plot without creating a pyglet window.

## Camera

We need a better way to represent the camera for several reasons. First, we need to be able to determine the zoom level and calculate the viewport for dynamic LOD. Second, it currently relies on OpenGL calls and therefore cannot be used for window-less plots.