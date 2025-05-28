# Configuration Guide

This guide covers the configuration options for the Far Out SDK for Unity.

## NasaConfig

The `NasaConfig` asset is a ScriptableObject that stores all your settings for the Far Out SDK. It includes:

- API key
- Base URL
- Caching preferences

### Creating a NasaConfig Asset

1. In your Project window, right-click and select **Create > NASA > NasaConfig**
2. A new `NasaConfig.asset` file will be created
3. Select the asset to view and edit its properties in the Inspector

### Configuration Options

| Parameter | Description | Default |
| --- | --- | --- |
| **API Key** | Your NASA API key. If left empty, uses `DEMO_KEY`. | `""` (empty, falls back to DEMO_KEY) |
| **Base URL** | The base URL for NASA APIs. | `"https://api.nasa.gov"` |
| **Use Cache** | Enable/disable local caching of API responses and images. | `true` |
| **Cache Expiry Minutes** | Time in minutes before cached items expire. | `1440` (24 hours) |
| **Max Cache Size Mb** | Maximum size of disk cache in megabytes. | `100` |

### API Key

You can get a free NASA API key from [api.nasa.gov](https://api.nasa.gov/).

- The `DEMO_KEY` (used when API Key is empty) has these rate limits:
  - Hourly Limit: 30 requests per IP address per hour
  - Daily Limit: 50 requests per IP address per day

- A registered API key has these rate limits:
  - Hourly Limit: 1,000 requests per hour
  - Daily Limit: None

You can test your key by clicking the **Test Key** button in the Inspector.

### Base URL

The default base URL is `https://api.nasa.gov`, which should work for all supported endpoints. You generally shouldn't need to change this unless you're using a proxy or NASA changes their API domain.

### Caching

The Far Out SDK includes a built-in caching system to reduce API calls and save bandwidth.

#### Caching Options

- **Use Cache**: When enabled, API responses and downloaded images are cached to disk.
- **Cache Expiry Minutes**: The time (in minutes) before cached items expire. Default is 24 hours.
- **Max Cache Size Mb**: Maximum size of the cache. When exceeded, older items are removed first.

#### Cache Location

Cached files are stored in a subdirectory of `Application.persistentDataPath`:

```
{Application.persistentDataPath}/NasaSdkCache/
```

#### Cache Behavior

- If a requested item exists in the cache and hasn't expired, it's returned immediately without making an API call.
- If an item doesn't exist in the cache or has expired, an API call is made and the result is cached.
- For images, caching can significantly reduce load times on subsequent views.

## Programmatic Configuration

You can also configure the NASA client programmatically when initializing it:

```csharp
// Create a client with a custom HTTP implementation and cache
var httpClient = new CustomHttpClient(); // Your implementation of IHttpClient
var cache = new CustomCache(); // Your implementation of ICache
var nasaClient = new NasaClient(nasaConfig, httpClient, cache);

// Or use the default implementations but disable caching in NasaConfig
nasaConfig.UseCache = false;
var nasaClient = new NasaClient(nasaConfig);
```

## Multiple Configurations

You can create multiple `NasaConfig` assets for different purposes:

- One for development with a higher cache expiry time
- One for production with your official API key
- Different configurations for different NASA APIs or projects

Just create multiple config assets and reference the appropriate one in your scripts.