![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/wokwi_test/badge.svg)

# Tiny Tapeout 5: WS2812B LED strip driver

This is a [Tiny Tapeout 5](https://tinytapeout.com/) test project. This project drives a strip of WS2812B RGB LEDs, periodically updating the strip with random color values. The project consists of three main modules:
- a [linear feedback 16-bit shift register](https://en.wikipedia.org/wiki/Linear-feedback_shift_register) to generate a stream of pseudo-random bits
- a 5-bit synchronous increasing counter, wrapping to 0 when the counter reaches 25. WHen driven by a 20 MHz clock source, the counter generates the 1.25 us pulses required by the [WS2812B protocol](https://cdn-shop.adafruit.com/datasheets/WS2812B.pdf). The duration of the high phase of the pulse is controlled by the random bit stream generated above.
- a 16-bit ripple counter increasing at the end of each pulse, used to divide the pulse frequency and generate the LED strip refresh signal

The RST_N signal resets the state of the pulse generator and holds low the line driving the LED strip (LED strip refresh).

| Input   | Description     | 
|---------|-----------------|
| 0       | clock source selection | 
| 1       | external clock source |
| 2       | refresh freq sel (low) | 
| 3       | refresh freq sel (high) | 
| 4       | N/A |
| 5       | N/A | 
| 6       | WS2812B LED strip output |
| 7       | shift register input | 


| Output  | Description     | 
|---------|-----------------|
| 0       | shift register output | 
| 1       | shift register clock |
| 2       | WS2812B LED strip input | 
| 3       | LED strip overflow | 
| 4       | LED strip refresh |
| 5       | N/A | 
| 6       | N/A |
| 7       | N/A |

