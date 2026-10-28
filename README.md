# aud_audio_sequencer

English | [Deutsch](README.de.md)

Sequencer of the Audanika Audio Engine: render-thread sequencer with
tracks, clips, loops and transport.

Part of the Audanika Audio Engine; planned in
[aud_audio_pm](https://github.com/audaudio/aud_audio_pm).

## Motivation

An app that plays through the engine wants to arrange what it plays:
tracks of clips that loop and follow a transport, scheduled on the render
thread so that the timing does not depend on Dart. This package is meant
to become that sequencer over the graph of `aud_audio_graph`. Today it
holds the native boilerplate the sequencer will grow from: a C source
built by the build hook and called through `dart:ffi`.

## Installation

The package is not published to pub.dev; add it as a git dependency:

```yaml
dependencies:
  aud_audio_sequencer:
    git:
      url: git@github.com:audaudio/aud_audio_sequencer.git
      tag_pattern: "{{version}}"
    version: ^0.0.3
```

## Usage

The public API is the boilerplate of a native package: `sum` calls the C
function on the main isolate, `sumAsync` the long-running one on a helper
isolate. The example app (`example/lib/main.dart`) shows both results on
screen; the same calls as plain Dart:

```dart
import 'package:aud_audio_sequencer/aud_audio_sequencer.dart';

Future<void> main() async {
  print(sum(1, 2));
  print(await sumAsync(3, 4));
}
```

It prints:

```text
3
7
```

## Limitations

- No sequencer yet: no tracks, clips, loops or transport; the package
  builds and binds its C source, nothing more
- The native code is built by the build hook (`hook/build.dart`) with
  `native_toolchain_c`; on Windows it needs MSVC

## Documentation

- The guides in [doc/guides](doc/guides) and the blog posts in
  [doc/blog](doc/blog)
- The changes per version in [CHANGELOG.md](CHANGELOG.md)

## Status

Before 1.0 - the API may change between minor versions. The package is a
placeholder of the family until the sequencer is built.

## Contributing

Tickets run through the `gg` workflow: see the
[Develop Guide](doc/guides/develop-guide.md) and the
[Review Guide](doc/guides/for-ai/ai-review-guide.md).

## License

MIT - see [LICENSE](LICENSE).
