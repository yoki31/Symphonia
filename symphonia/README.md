<div align="center">
<h1>Symphonia</h1>

<!--
<p>
    <img src="https://raw.githubusercontent.com/pdeljanov/symphonia/master/assets/logo.png" width="200px" />
</p>
-->

<p>
    <a href="https://crates.io/crates/symphonia">
        <img alt="Crate Info" src="https://img.shields.io/crates/v/symphonia.svg"/>
    </a>
    <a href="https://docs.rs/symphonia/">
        <img alt="API Docs" src="https://img.shields.io/badge/docs.rs-symphonia-brightgreen"/>
    </a>
    <a href="https://github.com/pdeljanov/Symphonia/actions/workflows/ci.yml">
        <img src="https://github.com/pdeljanov/Symphonia/actions/workflows/ci.yml/badge.svg" />
    </a>
    <a href="https://deps.rs/repo/github/pdeljanov/symphonia">
        <img src="https://deps.rs/repo/github/pdeljanov/symphonia/status.svg" />
    </a>
    <a href="https://blog.rust-lang.org/2021/03/25/Rust-1.53.0.html">
        <img alt="Rustc Version 1.53.0+" src="https://img.shields.io/badge/rustc-1.53%2B-lightgrey.svg"/>
    </a>
</p>

<p>
    <strong>
        Symphonia is a pure Rust audio decoding and media demuxing library supporting AAC, ALAC, FLAC, MKV, MP3, MP4, OGG, Vorbis, WAV, and WebM.
    </strong>
</p>

<p>
    <h3>
        <a href="https://github.com/pdeljanov/Symphonia/blob/master/GETTING_STARTED.md">Getting Started</a>
        <span> · </span>
        <a href="https://docs.rs/symphonia">Documentation</a>
        <span> · </span>
        <a href="https://github.com/pdeljanov/Symphonia/tree/master/symphonia/examples">Examples</a>
        <span> · </span>
        <a href="https://github.com/pdeljanov/Symphonia/blob/master/BENCHMARKS.md">Benchmarks</a>
    </h3>
</p>
</div>

---

## Features

* Decode support for the most popular audio codecs with support for gapless playback
* Demux the most common media container formats
* Read most metadata and tagging formats
* Automatic format and decoder detection
* Basic audio primitives for manipulating audio data efficiently
* 100% safe Rust
* Minimal dependencies
* Fast with no compromises in performance!

Additionally, planned features include:

* Providing a C API for integration into other languages
* Providing a WASM API for web usage

## Current Support

Support for individual audio codecs and media formats is provided by separate crates. By default, Symphonia enables support for FOSS codecs and formats, but others may be enabled via the features option.

The follow status classifications are used to determine the state of development for each format or codec.

| Status    | Meaning                                                                                                                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------|
| Good      | Many media streams play. Some streams may panic, error, or produce audible glitches. Some features may not be supported. |
| Great     | Most media streams play. Inaudible glitches may be present. Most common features are supported.                          |
| Excellent | All media streams play.  No audible or inaudible glitches. All required features are supported.                          |

A status of *great* indicates that major development is complete and that the feature is in a state that would be acceptable for most applications to use. A status of *excellent* is only assigned after the feature passes all compliance tests. If no compliance tests are freely available, then a status of *excellent* will be assigned if Symphonia's implementation matches the quality of a reference implementation, or `ffmpeg`.

### Formats (Demuxers)

| Format   | Status    | Gapless* | Feature Flag | Default | Crate                       |
|----------|-----------|----------|--------------|---------|-----------------------------|
| ISO/MP4  | Great     | No       | `isomp4`     | No      | [`symphonia-format-isomp4`] |
| MKV/WebM | Good      | No       | `mkv`        | Yes     | [`symphonia-format-mkv`]    |
| OGG      | Great     | Yes      | `ogg`        | Yes     | [`symphonia-format-ogg`]    |
| Wave     | Excellent | Yes      | `wav`        | Yes     | [`symphonia-format-wav`]    |

\* Gapless playback requires support from both the demuxer and decoder.

[`symphonia-format-isomp4`]: https://docs.rs/symphonia-format-isomp4
[`symphonia-format-ogg`]: https://docs.rs/symphonia-format-ogg
[`symphonia-format-wav`]: https://docs.rs/symphonia-format-wav
[`symphonia-format-mkv`]: https://docs.rs/symphonia-format-mkv

### Codecs (Decoders)

| Codec  | Status    | Gapless | Feature Flag | Default | Crate                      |
|--------|-----------|---------|--------------|---------|----------------------------|
| AAC-LC | Great     | No      | `aac`        | No      | [`symphonia-codec-aac`]    |
| ALAC   | Great     | Yes     | `alac`       | No      | [`symphonia-codec-alac`]   |
| FLAC   | Excellent | Yes     | `flac`       | Yes     | [`symphonia-bundle-flac`]  |
| MP3    | Excellent | Yes     | `mp3`        | No      | [`symphonia-bundle-mp3`]   |
| PCM    | Excellent | Yes     | `pcm`        | Yes     | [`symphonia-codec-pcm`]    |
| Vorbis | Excellent | Yes     | `vorbis`     | Yes     | [`symphonia-codec-vorbis`] |

A `symphonia-bundle-*` package is a combination of a decoder and a native demuxer.

[`symphonia-codec-aac`]: https://docs.rs/symphonia-codec-aac
[`symphonia-codec-alac`]: https://docs.rs/symphonia-codec-alac
[`symphonia-bundle-flac`]: https://docs.rs/symphonia-bundle-flac
[`symphonia-bundle-mp3`]: https://docs.rs/symphonia-bundle-mp3
[`symphonia-codec-pcm`]: https://docs.rs/symphonia-codec-pcm
[`symphonia-codec-vorbis`]: https://docs.rs/symphonia-codec-vorbis

### Tags (Readers)

All metadata readers are provided by the `symphonia-metadata` crate.

| Format                | Status    |
|-----------------------|-----------|
| ID3v1                 | Great     |
| ID3v2                 | Great     |
| ISO/MP4               | Great     |
| RIFF                  | Great     |
| Vorbis comment (FLAC) | Perfect   |
| Vorbis comment (OGG)  | Perfect   |

## Quality

In addition to the safety guarantees afforded by Rust, Symphonia aims to:

* Decode media as correctly as the leading free-and-open-source software decoders
* Prevent denial-of-service attacks
* Be fuzz-tested
* Provide a powerful, consistent, and easy to use API

## Performance

Symphonia aims to be comparable to, or faster than, popular open-source C-based implementations. Currently, Symphonia's decoders are generally +/-15% the performance of FFMpeg. However, the exact range will depend strongly on the codec, which features of the codec are being leveraged in the encoding, the Rust compiler version, and the CPU architecture being compiled for.

See the [benchmarks](https://github.com/pdeljanov/Symphonia/blob/master/BENCHMARKS.md) for more information.

## Examples

Basic usage examples may be found [`here`](https://github.com/pdeljanov/Symphonia/tree/master/symphonia/examples).

For a more complete application, see [`symphonia-play`](https://github.com/pdeljanov/Symphonia/tree/master/symphonia-play), a simple music player.

## Tools

Symphonia provides the following tools for debugging purposes:

* [`symphonia-play`](https://github.com/pdeljanov/Symphonia/tree/master/symphonia-play) for probing, decoding, validating, and playing back media streams.
* [`symphonia-check`](https://github.com/pdeljanov/Symphonia/tree/master/symphonia-check) for validating Symphonia's decoded output against various decoders.

## Author

The primary author is Philip Deljanov.

## Special Thanks

* Kostya Shishkov (AAC-LC decoder contribution, see `symphonia-codec-aac`)

## License

Symphonia is provided under the MPL v2.0 license. Please refer to the LICENSE file for more details.

## Contributing

Symphonia is an open-source project and contributions are very welcome! If you would like to make a large contribution, please raise an issue ahead of time to make sure your efforts fit into the project goals, and that there's no duplication of effort. Please be aware that all contributions must also be licensed under the MPL v2.0 license to be accepted.

When submitting a pull request, be sure you have included yourself in the CONTRIBUTORS file!
