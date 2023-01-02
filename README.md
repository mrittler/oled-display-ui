# Ui Library (OLEDDisplayUi)

The Ui Library is used to provide a basic set of user interface elements called `Frames` and `Overlays`. A `Frame` is used to provide
information to the user. The default behaviour is to display a `Frame` for a defined time and than move to the next `Frame`. The library also
provides an `Indicator` element that will be updated accordingly. An `Overlay` on the other hand is a piece of information (e.g. a clock) that
is always displayed at the same position.

## Features

* Display content in automatically side scrolling carousel
 * Define transition cycles
 * Define how long one frame will be displayed
 * Draw the different frames in callback methods
 * One indicator per frame will be automatically displayed. The active frame will be displayed from inactive once

## API

```C++
/**
 * Configure the internal used target FPS
 */
void setTargetFPS(uint8_t fps);

/**
 * Enable automatic transition to next frame after the some time can be configured with
 * `setTimePerFrame` and `setTimePerTransition`.
 */
void enableAutoTransition();

/**
 * Disable automatic transition to next frame.
 */
void disableAutoTransition();

/**
 * Set the direction if the automatic transitioning
 */
void setAutoTransitionForwards();
void setAutoTransitionBackwards();

/**
 *  Set the approx. time a frame is displayed
 */
void setTimePerFrame(uint16_t time);

/**
 * Set the approx. time a transition will take
 */
void setTimePerTransition(uint16_t time);

/**
 * Draw the indicator.
 * This is the default state for all frames if
 * the indicator was hidden on the previous frame
 * it will be slided in.
 */
void enableIndicator();

/**
 * Don't draw the indicator.
 * This will slide out the indicator
 * when transitioning to the next frame.
 */
void disableIndicator();

/**
 * Enable drawing of all indicators.
 */
void enableAllIndicators();

/**
 * Disable drawing of all indicators.
 */
void disableAllIndicators();

/**
 * Set the position of the indicator bar.
 */
void setIndicatorPosition(IndicatorPosition pos);

/**
 * Set the direction of the indicator bar. Defining the order of frames ASCENDING / DESCENDING
 */
void setIndicatorDirection(IndicatorDirection dir);

/**
 * Set the symbol to indicate an active frame in the indicator bar.
 */
void setActiveSymbol(const uint8_t* symbol);

/**
 * Set the symbol to indicate an inactive frame in the indicator bar.
 */
void setInactiveSymbol(const uint8_t* symbol);

/**
 * Configure what animation is used to transition from one frame to another
 */
void setFrameAnimation(AnimationDirection dir);

/**
 * Add frame drawing functions
 */
void setFrames(FrameCallback* frameFunctions, uint8_t frameCount);

/**
 * Add overlays drawing functions that are draw independent of the Frames
 */
void setOverlays(OverlayCallback* overlayFunctions, uint8_t overlayCount);

/**
 * Set the function that will draw each step
 * in the loading animation
 */
void setLoadingDrawFunction(LoadingDrawFunction loadingDrawFunction);

/**
 * Run the loading process
 */
void runLoadingProcess(LoadingStage* stages, uint8_t stagesCount);

// Manual control
void nextFrame();
void previousFrame();

/**
 * Switch without transition to frame `frame`.
 */
void switchToFrame(uint8_t frame);

/**
 * Transition to frame `frame`. When the `frame` number is bigger than the current
 * frame the forward animation will be used, otherwise the backwards animation is used.
 */
void transitionToFrame(uint8_t frame);

// State Info
OLEDDisplayUiState* getUiState();

// This needs to be called in the main loop
// the returned value is the remaining time (in ms)
// you have to draw after drawing to keep the frame budget.
int8_t update();
```

## Credits

This library has initially been written by [Daniel Eichhorn](https://github.com/squix78). Many thanks go to [Fabrice Weinberg](https://github.com/FWeinb) for optimizing and refactoring many aspects of the library. Also many thanks to the many committers who helped to add new features and who fixed many bugs. Mbed-OS support and other improvements were contributed by [Helmut Tschemernjak](https://github.com/helmut64).
