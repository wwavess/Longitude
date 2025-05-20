# Longitude Granular Synthesizer

Longitude is a granular synthesizer built in Max/MSP, focused on time-domain audio stretching and creating evolving soundscapes. It allows for detailed control over grain playback, crossfading, and randomization, making it suitable for ambient textures, sound design, and experimental music.

## Features

Based on the `Longitude_Alpha.maxpat` patch, the synthesizer includes the following features:

*   **Granular Synthesis Engine:** Core mechanism for breaking down audio into small "grains" and resynthesizing them.
*   **Time-Domain Audio Stretching:** Achieved by manipulating grain playback, allowing for significant elongation or compression of audio material without altering pitch.
*   **Crossfade Locking with Grain Play Rate:** A key feature for seamless modulation of parameters without audible gaps or clicks, by synchronizing the crossfade duration with the grain's playback speed.
*   **Adjustable Playback Rate and Direction:** Controls for modifying the speed and direction (forward, backward, palindrome) of grain playback.
*   **Grain Range Selection:** Ability to define a specific segment of the loaded audio sample from which grains are selected.
*   **Grain Randomization (Shuffle):** Randomly selects grain playback positions within the defined range.
*   **Interpolated Sliding between Shuffle Positions:** Smoothly transitions between different random playback positions when shuffle is active, controlled by a "Slide" parameter.
*   **Adjustable Crossfade Amount:** Controls the amount of overlap and fade between consecutive grains, influencing the smoothness of the resulting sound.
*   **Polyphonic Voice Management:** Supports multiple simultaneous voices (grains), with a display for active voices.
*   **File Loading:** Allows users to load their own audio samples as the source material.
*   **Basic Audio Output Controls:** Includes a master play/stop toggle and direct audio output (DAC~).
*   **Preset System:** Ability to save and recall parameter settings.
*   **Freeze:** A toggle to freeze the current sonic texture.
*   **Windowing:** Applies a windowing function (e.g., Kaiser, Welch) to grains to shape their amplitude envelope.

## Controls / Parameters

The main interface of `Longitude_Alpha.maxpat` (presentation mode) provides the following controls:

*   **File Loading Button:** (Top-left icon) Opens a dialog to load an audio sample. The loaded filename is displayed next to it.
*   **Play/Stop Toggle:** (Below File loading) Master toggle to start or stop audio output from the synthesizer.
*   **Rate Control (Dial/Number Box):** (Labeled "Rate") Adjusts the playback rate of the grains. Linked to the "PlayRate" parameter.
*   **Direction Control (Dropdown Menu):** (Labeled "Direction") Selects the playback direction for grains (e.g., "fwd", "bwd", "pnd").
*   **Range Selection (Slider & Toggle):**
    *   **Range Slider (`PlayRange`):** (Horizontal slider below file info) Sets the start and end points within the loaded sample from which grains will be selected.
    *   **Range Toggle (`PlayRange_Tog`):** (Checkbox next to "Range" label) Activates or deactivates the use of the selected range.
*   **Shuffle Toggle & Rate:**
    *   **Shuffle Toggle (`Shuffle_On`):** (Checkbox next to "Shuffle" label/Dial) Enables or disables random selection of grain playback positions.
    *   **Shuffle Rate Dial (`ShuffleRate`):** (Labeled "Shuffle") Controls the frequency or speed of randomization when shuffle is active.
*   **Slide Toggle & Rate:**
    *   **Slide Link Toggle (`Slide_Link`):** (Checkbox, potentially labeled "Link" or near Shuffle/Slide dials) Likely links the Slide rate to the Shuffle rate.
    *   **Slide Rate Dial (`SlideRate`):** (Labeled "Slide") Controls the interpolation time or smoothness when transitioning between different shuffle positions.
*   **Crossfade Amount Dial (`CrossFade`):** (Labeled "Crossfade") Adjusts the duration/amount of crossfade applied between grains.
*   **LapseGap Dial (`LapseGap`):** (Labeled "Lapse Gap") Controls the time interval or gap between the start of consecutive grains. This influences the density and overlap of grains.
*   **WindowLength Dial (`WindowLength`):** (Labeled "Window") Determines the duration of each individual grain (the "window" of audio).
*   **Slices Dial/Number Box (`slices`):** (Potentially linked to "LapseGap" and "File Length") Likely represents the number of segments or potential grain start points calculated based on file length and lapse gap.
*   **Active Voices Display:** (Labeled "Active Voices", visualizer) Shows the number of grains currently playing.
*   **Preset Controls:** (Numbered boxes/buttons on the left) Allows saving and recalling different states of the synthesizer's parameters.
*   **Freeze Toggle (`Freeze`):** (Toggle button, potentially near playback controls) Freezes the current granular texture.
*   **Output Level/DAC Controls:** While not a specific UI element in presentation, the patch includes `dac~` objects, implying direct audio output. Volume adjustments might be part of the `poly~` subpatch or a master volume (not explicitly labeled in presentation).
*   **Play Once Toggle (`PlayOnce`):** (Small toggle, potentially near Direction) When active, likely plays through the grain sequence or a defined segment once rather than continuously.

## Engine Components

*   **`Longitude_Alpha.maxpat`:** This is the main Max/MSP patch file. It contains all the synthesizer's logic, user interface elements, parameter controls, and patching that defines the granular engine's behavior.
*   **`dcblock.gendsp`:** A Gen DSP object referenced in the patch (e.g., within `LongPlay_Play_2.maxpat`). Its purpose is to remove any DC offset from the audio signal, which is good practice to prevent clicks and maintain headroom.
*   **`metro_down.gendsp`:** A Gen DSP object, likely implementing a metronome or a trigger generator. This is probably used for rhythmic triggering of grains or sequences, especially if the "Play Once" feature is not active, or to drive the `counter` object for sequential grain playback.

## Setup and Usage

1.  **Download Files:** Ensure all files (`Longitude_Alpha.maxpat`, and any associated files like `dcblock.gendsp`, `metro_down.gendsp`, and subpatchers like `LongPlay_Play_2.maxpat`) are downloaded.
2.  **Max/MSP File Preferences:**
    *   Place all downloaded files within a directory that is already in your Max/MSP File Search Preferences.
    *   Alternatively, add the new directory containing the files via Max/MSP's menu: Options -> File Preferences -> Click the '+' button (bottom left) and add the path to the directory.
3.  **Open the Patch:** Open `Longitude_Alpha.maxpat` in Max/MSP. You should see the user interface in presentation mode.
4.  **Load an Audio Sample:**
    *   Click the file icon in the top-left corner.
    *   Select an audio file from your computer. The filename will appear next to the icon.
5.  **Basic Playback:**
    *   Toggle the "Play" button (below the file icon) to start the synthesizer.
    *   You should start hearing sound if a sample is loaded and parameters are at default.
6.  **Adjust Parameters:**
    *   **Rate & Window:** Experiment with the "Rate" and "Window" dials to change the speed and duration of the grains.
    *   **Lapse Gap:** Adjust the "Lapse Gap" to change the density of grains.
    *   **Range:** Use the horizontal "PlayRange" slider to select a portion of the sample. Activate it with the "Range" toggle.
    *   **Shuffle & Slide:** Enable "Shuffle" to randomize grain positions. Adjust "Shuffle" and "Slide" dials to control the randomization speed and smoothness.
    *   **Crossfade:** Modify the "Crossfade" dial to change how grains blend into each other.
    *   Explore other controls like "Direction", "Freeze", and presets.
7.  **Output:** Audio is sent directly to your DAC (Digital-to-Analog Converter) / audio output. Ensure your Max/MSP audio settings are configured correctly.

## Contributing

Contributions are welcome! Please open an issue to discuss a new feature or bug, or submit a pull request with your changes.

## License

MIT License
