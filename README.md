# DIY Smart Coffee and Espresso Scale

This project contains all the necessary software to program the micropython microcontroller and interface with it through a Bluetooth API-enabled web browser (Chrome, Opera).

The `firmware` folder contains the `.py` files that need to be uploaded into the ESP32's memory running the micropython interpreter.

The `src` folder contains the source for the Progressive Web App that allows to retrieve the scale's reading in real time (10Hz refresh rate) as well as the battery level.

## Settings

The app works as a timer to achieve the desired extraction in the desired time. A reference curve is displayed, taking into account the user parameters:

- Coffee Weight: how much coffee grounds were put in the basket (the "Read" button puts the current scale value into this field)
- Target ratio: the ratio of "coffee out" to "grounds in". The expected output weight is calculated next to the field.
- Pre-infusion time: this is an amount of time that is added to the timer as soon as >0.5g are detected in the cup. This allows to indicate the desired total brew time including pre-infusion. It's the user responsibility to perform the pre-infusion with this amount of time.
- Total time: the total brew time, including any pre-infusion.

## Workflow

- The basket or portafilter is put on the scale and tared with the scale's button.
- The desired amount of coffee grounds is put inside the basket
- the basket or portafilter is put back on the scales, thereby measuring the weight of the coffee grounds
- The "Read" button next to the "Coffee Weight" input is clicked to read the current value into it
- The cup is placed on the scale and it is tared with the button
- The "Start recording" button is pressed (only available when the scale reads 0g). The app now waits for an increase in weight.
- As soon as the weight exceeds 0.5g, the timer starts counting from the pre-infusion time (default 5s).
- The extraction can be followed in real time and should match the grey reference curve (in a direct drive lever machine, the user would adjust the pressure to match the curve)
- When the extraction is finished, the cup is lifted from the scale, thus stopping the recording.
