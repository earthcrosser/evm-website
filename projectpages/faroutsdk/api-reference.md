# API Reference

This document provides an overview of the main classes and methods in the Far Out SDK for Unity.

## Main Classes

### NasaClient

The `NasaClient` class is the main entry point to the SDK. It provides methods for interacting with NASA's APIs.

```csharp
// Constructor
public NasaClient(NasaConfig config, IHttpClient? httpClient = null, ICache? cache = null)
```

#### APOD (Astronomy Picture of the Day)

```csharp
// Get APOD metadata for a specific date (defaults to today)
public async Task<ApodData?> GetApodAsync(DateTime? date = null, CancellationToken cancellationToken = default)

// Download APOD image as a Texture2D
public async Task<Texture2D?> GetApodTextureAsync(ApodData apodData, bool hd = true, CancellationToken cancellationToken = default)
```

#### Mars Rover Photos

```csharp
// Get Mars Rover photos
public async Task<MarsRoverPhotosResponse?> GetMarsPhotosAsync(
    string roverName, 
    int? sol = null, 
    string? camera = null, 
    DateTime? earthDate = null, 
    int page = 1, 
    CancellationToken cancellationToken = default)

// Download a Mars Rover photo as a Texture2D
public async Task<Texture2D?> GetMarsPhotoTextureAsync(MarsPhoto photoData, CancellationToken cancellationToken = default)
```

#### Earth Imagery

```csharp
// Get Earth imagery metadata
public async Task<EarthImageData?> GetEarthImageMetadataAsync(
    float latitude, 
    float longitude, 
    DateTime? date = null, 
    float? dimension = null, 
    bool cloudScore = false, 
    CancellationToken cancellationToken = default)

// Download Earth image as a Texture2D using metadata
public async Task<Texture2D?> GetEarthImageTextureAsync(EarthImageData earthImageData, CancellationToken cancellationToken = default)

// Directly fetch an Earth image without metadata
public async Task<Texture2D?> GetEarthImageAsync(
    float latitude, 
    float longitude, 
    DateTime? date = null, 
    float? dimension = null, 
    CancellationToken cancellationToken = default)
```

#### NeoWs (Near Earth Object Web Service)

```csharp
// Get Near Earth Objects feed
public async Task<NeoFeed?> GetNeoFeedAsync(DateTime startDate, DateTime? endDate = null, CancellationToken cancellationToken = default)
```

#### EPIC (Earth Polychromatic Imaging Camera)

```csharp
// Get EPIC image metadata for a date
public async Task<List<EpicImageMetadata>?> GetEpicImageMetadataAsync(DateTime date, CancellationToken cancellationToken = default)

// Download an EPIC image as a Texture2D using metadata
public async Task<Texture2D?> GetEpicImageTextureAsync(EpicImageMetadata imageMetadata, string imageType = "png", CancellationToken cancellationToken = default)

// Get all EPIC images for a date
public async Task<List<Texture2D>> GetEpicImagesAsync(DateTime date, string imageType = "png", CancellationToken cancellationToken = default)
```

### NasaConfig

`NasaConfig` is a ScriptableObject that stores configuration settings for the Far Out SDK.

```csharp
public class NasaConfig : ScriptableObject
{
    public string ApiKey = "";
    public string BaseUrl = "https://api.nasa.gov";
    
    public bool UseCache = true;
    public int CacheExpiryMinutes = 60 * 24; // 24 hours
    public int MaxCacheSizeMb = 100;
    
    public string GetApiKey() => string.IsNullOrEmpty(ApiKey) ? "DEMO_KEY" : ApiKey;
}
```

### Data Models

The SDK includes several model classes for deserializing API responses:

- `ApodData`: Astronomy Picture of the Day data
- `MarsRoverPhotosResponse`, `MarsPhoto`, `MarsCamera`, `MarsRover`: Mars rover photos data
- `EarthImageData`: Earth imagery data
- `NeoFeed`, `NearEarthObject`: Near Earth Object data
- `EpicImageMetadata`: EPIC image metadata

### Error Handling

The SDK throws `NasaApiException` for API-specific errors:

```csharp
public class NasaApiException : Exception
{
    public long StatusCode { get; }
    public string? RequestUri { get; }
    public UnityWebRequest.Result? WebRequestResult { get; }
    public NasaApiError? ApiError { get; }
    
    // Constructors and methods...
}
```

### Caching

The SDK includes built-in caching via the `ICache` interface and `DiskCache` implementation:

```csharp
public interface ICache
{
    Task<CacheResult<string>> TryGetStringAsync(string key);
    Task<CacheResult<byte[]>> TryGetByteArrayAsync(string key);
    Task SetStringAsync(string key, string value, DateTimeOffset expiry);
    Task SetByteArrayAsync(string key, byte[] value, DateTimeOffset expiry);
    Task RemoveAsync(string key);
    Task ClearAsync();
    Task PruneAsync();
}
```

### HTTP Client

The SDK uses the `IHttpClient` interface for HTTP requests, with a default implementation (`UnityWebRequestClient`) using Unity's `UnityWebRequest`:

```csharp
public interface IHttpClient : IDisposable
{
    Task<string> GetStringAsync(string uri, CancellationToken cancellationToken = default);
    Task<byte[]> GetByteArrayAsync(string uri, CancellationToken cancellationToken = default);
}
```

## Editor Tools

### DataExplorerWindow

The SDK includes a `DataExplorerWindow` that can be accessed via **NASA > Data Explorer** in the Unity Editor. This window allows you to:

- Test API endpoints
- Preview API responses
- View images directly in the editor

### Code Templates

The SDK provides a quick start script template that can be accessed via **Assets > Create > C# Script > NASA Quick Start Script**.

## Extensions and Utilities

### DateUtils

Utility methods for working with dates in NASA API formats:

```csharp
public static string ToNasaDateString(DateTime dateTime)
public static bool TryParseNasaDateString(string? nasaDateString, out DateTime dateTime)
```

### TextureUtils

Utility methods for working with textures:

```csharp
public static Texture2D? LoadTextureFromBytes(byte[] imageData, string? textureName = "NasaImage")
public static Sprite? ConvertTextureToSprite(Texture2D? texture, float pixelsPerUnit = 100.0f)
```