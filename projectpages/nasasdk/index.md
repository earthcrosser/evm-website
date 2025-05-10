# NASA APIs for Unity

Welcome to the NASA APIs for Unity SDK documentation! This SDK provides a comprehensive, production-quality interface to NASA's rich collection of public APIs. Fetch stunning astronomy pictures, browse Martian landscapes, track near-Earth asteroids, and more, all directly within your Unity applications at runtime.

## Overview

The NASA SDK provides an easy-to-use interface for accessing NASA's APIs, with features like:

- Easy configuration through a `NasaConfig` ScriptableObject
- Asynchronous API access using Tasks
- Built-in caching to reduce API calls
- Support for multiple NASA APIs, including:
  - Astronomy Picture of the Day (APOD)
  - Mars Rover Photos
  - Earth Imagery
  - Near Earth Objects (NeoWs)
  - EPIC (Earth Polychromatic Imaging Camera)
- Editor tools for previewing API data
- Sample scenes to help you get started

## Getting Started

- [Quick Start Guide](quickstart.md) - Get up and running in just a few minutes
- [Configuration](configuration.md) - Detailed information on configuring the SDK
- [API Reference](api-reference.md) - Reference documentation for classes and methods
- [Samples](samples.md) - Sample scenes included with the SDK

## Basic Usage

```csharp
// Initialize client
_nasaClient = new NasaClient(nasaConfig);

// Get today's Astronomy Picture of the Day
ApodData apod = await _nasaClient.GetApodAsync();

// Download the APOD as a texture
Texture2D texture = await _nasaClient.GetApodTextureAsync(apod);

// Use the texture (e.g., apply to a RawImage)
myRawImage.texture = texture;
```

## Requirements

- Unity 2022.3 LTS or newer
- Newtonsoft.Json package (automatically installed as a dependency)

## Support and Feedback

If you encounter issues or have feature requests, please file an issue on the [GitHub repository](https://github.com/extremevisualmedia/nasa-unity-sdk/issues).

## License

The SDK source code is released under the [MIT License](https://github.com/extremevisualmedia/nasa-unity-sdk/blob/main/LICENSE). Content from NASA's APIs is generally in the public domain, but please refer to [NASA's Media Usage Guidelines](https://www.nasa.gov/multimedia/guidelines/index.html) for details.