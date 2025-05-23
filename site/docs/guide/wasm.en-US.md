---
nav:
  title: Guide
  order: 2
group:
  title: Start
order: 7
---

# Codecs

## Introduction

Codecs are compiled into separate wasm modules, the decoders are in the ```dist/decode``` directory, and the encoders are in the ```dist/encode``` directory. There are four versions of the encoding and decoding wasm module: baseline, atomic, simd, abd 64. The baseline version's instruction set corresponds to the MVP version of WebAssembly, but it needs to support Mutable Globals, with the highest compatibility and the lowest performance; atomic version add the atomic operation instruction set and Bulk memory instruction set; simd version add the simd vector acceleration instruction set, has the highest performance. The current simd version is automatically optimized by the compiler, and different codecs have different effects (currently I have not seen any codec projects has optimized for the wasm simd instruction set. If you want higher acceleration effects, you may want to optimize by yourself); 64 is a 64-bit instruction set, the previous three versions are all 32-bit. The 64-bit instruction set also includes atomic and simd instruction sets. It needs to be run in an environment that supports wasm64, and libmedia also needs to use the corresponding 64-bit compiled version.


## Compatibility support status of three versions and Webcodecs

| environment    | baseline     | atomic     | simd         | 64          | webcodecs            |
| -----------    | -----------  |----------- | -----------  | ----------- | -----------          |
| Chrome         | 74+          | 75+        | 91+          | 133+        |94+                   |
| Firefox        | 61+          | 79+        | 89+          | N/A         |130+                  |
| Safari         | 13.4+        | 15+        | 16.4+        | N/A         |16.4+(video only)     |
| Wasmtime       | 0.20+        | 15+        | 15+          | N/A         |N/A                   |
| Wasmer         | 0.7+         | N/A        | N/A          | N/A         |N/A                   |
| Node.js        | 12.0+        | 16.4+      | 16.4+        | N/A         |N/A                   |
| Deno           | 0.1+         | 1.9+       | 1.9+         | N/A         |N/A                   |
| wasm2c         | 1.0.1+       | N/A        | N/A          | N/A         |N/A                   |


## Decode Codecs

| codec       | baseline   | atomic     | simd        | 64            |  webcodecs(Chrome) |
| ----------- | -----------|----------- | ----------- | -----------   | -----------        |
| h264        | ✅         | ✅          | ✅          | ✅            | ✅                 |
| hevc        | ✅         | ✅          | ✅          | ✅            | ✅ (hardware only) |
| vvc         | ✅         | ✅          | ✅          | ✅            | ❌                 |
| av1         | ✅         | ✅          | ✅          | ✅            | ✅                 |
| vp8         | ✅         | ✅          | ✅          | ✅            | ✅                 |
| vp9         | ✅         | ✅          | ✅          | ✅            | ✅                 |
| mpeg1       | ✅         | ✅          | ✅          | ✅            | ❌                 |
| mpeg2       | ✅         | ✅          | ✅          | ✅            | ❌                 |
| mpeg4       | ✅         | ✅          | ✅          | ✅            | ❌                 |
| theora      | ✅         | ✅          | ✅          | ✅            | ❌                 |
| aac         | ✅         | ✅          | ✅          | ✅            | ✅                 |
| mp3         | ✅         | ✅          | ✅          | ✅            | ✅                 |
| opus        | ✅         | ✅          | ✅          | ✅            | ✅                 |
| flac        | ✅         | ✅          | ✅          | ✅            | ❌                 |
| speex       | ✅         | ✅          | ✅          | ✅            | ❌                 |
| vorbis      | ✅         | ✅          | ✅          | ✅            | ❌                 |
| ac3         | ✅         | ✅          | ✅          | ✅            | ❌                 |
| eac3        | ✅         | ✅          | ✅          | ✅            | ❌                 |
| dts         | ✅         | ✅          | ✅          | ✅            | ❌                 |
| G.711 A-law | ✅         | ✅          | ✅          | ✅            | ❌                 |
| G.711 μ-law | ✅         | ✅          | ✅          | ✅            | ❌                 |

## Encode Codecs

| codec       | baseline   | atomic     | simd        | 64            |  webcodecs(Chrome) |
| ----------- | -----------|----------- | ----------- | -----------   | -----------        |
| h264        | ✅         | ✅          | ✅          | ✅            | ✅                 |
| hevc        | ❌         | ✅          | ✅          | ✅            | ❌                 |
| vvc         | ❌         | ❌          | ❌          | ❌            | ❌                 |
| av1         | ❌         | ✅          | ✅          | ✅            | ✅                 |
| vp8         | ✅         | ✅          | ✅          | ✅            | ✅                 |
| vp9         | ✅         | ✅          | ✅          | ✅            | ✅                 |
| mpeg4       | ✅         | ✅          | ✅          | ✅            | ❌                 |
| theora      | ✅         | ✅          | ✅          | ✅            | ❌                 |
| aac         | ✅         | ✅          | ✅          | ✅            | ✅                 |
| mp3         | ✅         | ✅          | ✅          | ✅            | ❌                 |
| opus        | ✅         | ✅          | ✅          | ✅            | ✅                 |
| flac        | ✅         | ✅          | ✅          | ✅            | ❌                 |
| speex       | ✅         | ✅          | ✅          | ✅            | ❌                 |
| vorbis      | ✅         | ✅          | ✅          | ✅            | ❌                 |
| ac3         | ✅         | ✅          | ✅          | ✅            | ❌                 |
| eac3        | ✅         | ✅          | ✅          | ✅            | ❌                 |
| dts         | ✅         | ✅          | ✅          | ✅            | ❌                 |
| G.711 A-law | ✅         | ✅          | ✅          | ✅            | ❌                 |
| G.711 μ-law | ✅         | ✅          | ✅          | ✅            | ❌                 |

> X265 wasm encoder is special and cannot run in a non-multi-threaded environment

## Usage

The decoder is in the project's ```dist/decode``` directory, and the encoder is in the project's ```dist/encode``` directory. The wasm module does not publish an npm package, so it is recommended that you host the wasm file on your own cdn. You can also use some public cdns to access files hosted on github. The following takes ```cdn.jsdelivr.net``` as an example.

```javascript
let codecName = 'h264'
let wasmVersion = '-simd'
let libmediaVersion = '0.1.2'

const decoderH264 = `https://cdn.jsdelivr.net/gh/zhaohappy/libmedia@${libmediaVersion}/dist/decode/${codecName}${wasmVersion}.wasm`

```

**libmediaVersion uses the version of the package under libmedia that you depend on. It is not recommended to use the latest version, which may cause problems in the original project due to subsequent upgrades of wasm files**