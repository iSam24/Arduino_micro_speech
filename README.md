# Micro Speech — Arduino Nano 33 BLE Sense
*Based on the TinyML Book example by Pete Warden & Daniel Situnayake*

---

## What It Does

Runs a small speech recognition model on-device that listens continuously via the onboard microphone and detects two keywords — **"yes"** and **"no"** — without any cloud connection. The result is indicated via the onboard RGB LED.

| Detected | LED Colour |
|----------|-----------|
| "yes"    | Green     |
| "no"     | Red       |
| Unknown  | Blue      |
| Silence  | Off       |

---

## Hardware Required

- Arduino Nano 33 BLE Sense (Rev 2)
- USB cable (for power and flashing)

---


## How It Works

The example follows a three stage pipeline that runs in a continuous loop:

```
Microphone → Audio Provider
                  ↓
         Feature Provider
         (converts audio to
          MFCC spectrograms)
                  ↓
         TFLite Micro Inference
         (int8 quantised model)
                  ↓
         Command Responder
         (LED + Serial output)
```

The model was trained on the Google Speech Commands dataset and is stored as a C byte array. It is small enough to fit in the Nano's 1MB flash and requires only a few KB of RAM to run inference.

---

## References

- *TinyML* by Pete Warden & Daniel Situnayake (O'Reilly, 2020)
- [TensorFlow Micro Speech example](https://github.com/tensorflow/tflite-micro/tree/main/tensorflow/lite/micro/examples/micro_speech)
- [Arduino TensorFlowLite library](https://github.com/tensorflow/tflite-micro-arduino-examples)
