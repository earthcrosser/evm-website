# Quick Start Guide

This guide will help you get up and running with the NASA APIs for Unity SDK in just a few minutes. By the end, you'll be able to display today's Astronomy Picture of the Day (APOD) in your Unity project.

## Installation

### Via Unity Package Manager (Git URL)

1. Open your Unity project
2. Go to **Window > Package Manager**
3. Click the **+** button in the top-left corner
4. Select **Add package from git URL...**
5. Enter `https://github.com/extremevisualmedia/nasa-unity-sdk.git` (or the appropriate Git URL once hosted)
6. Click **Add**

### Via Local Package

If you've downloaded a local copy of the package:

1. Open your Unity project
2. Go to **Window > Package Manager**
3. Click the **+** button in the top-left corner
4. Select **Add package from disk...**
5. Navigate to the package folder
6. Click **Open**

## Setting Up an API Key

The NASA SDK requires an API key to access NASA's APIs. You can use the `DEMO_KEY` for testing, but this has very low rate limits.

1. Go to [api.nasa.gov](https://api.nasa.gov/) and sign up for a free API key
2. In Unity, right-click in your Project window and select **Create > NASA > NasaConfig**
3. Select the newly created `NasaConfig.asset` file
4. In the Inspector, enter your NASA API key
5. Click the **Test Key** button to verify your key works

## Creating Your First NASA API Script

Let's create a simple script to display the Astronomy Picture of the Day:

1. Right-click in your Project window and select **Create > C# Script > NASA Quick Start Script**
2. Name it `ApodDisplay` and press Enter
3. Double-click the script to open it in your code editor

The script should look something like this:

```csharp
using UnityEngine;
using UnityEngine.UI;
using System.Threading.Tasks;
using ExtremeVisual.Nasa;

public class ApodDisplay : MonoBehaviour
{
    [Tooltip("Assign your NasaConfig ScriptableObject asset here.")]
    public NasaConfig nasaConfig;
    
    [Tooltip("Assign a UI RawImage component here to display the APOD picture.")]
    public RawImage apodDisplayImage;

    private NasaClient _nasaClient;

    async void Start()
    {
        if (nasaConfig == null)
        {
            Debug.LogError("NasaConfig not assigned.");
            return;
        }

        // Initialize the NasaClient
        _nasaClient = new NasaClient(nasaConfig);
        
        await FetchAndDisplayApod();
    }

    async Task FetchAndDisplayApod()
    {
        try
        {
            // Fetch APOD metadata
            ApodData apodData = await _nasaClient.GetApodAsync();

            if (apodData != null)
            {
                Debug.Log($"APOD Title: {apodData.Title}");
                
                if (apodData.MediaType == "image")
                {
                    // Download the image
                    Texture2D texture = await _nasaClient.GetApodTextureAsync(apodData);
                    
                    if (texture != null && apodDisplayImage != null)
                    {
                        // Display the image
                        apodDisplayImage.texture = texture;
                    }
                }
            }
        }
        catch (NasaApiException ex)
        {
            Debug.LogError($"NASA API Error: {ex.Message}");
        }
        catch (System.Exception ex)
        {
            Debug.LogError($"Error: {ex.Message}");
        }
    }

    void OnDestroy()
    {
        _nasaClient?.Dispose();
    }
}
```

## Setting Up Your Scene

1. Create a new scene or use an existing one
2. Add a UI Canvas to your scene (**GameObject > UI > Canvas**)
3. Add a RawImage to the Canvas (**GameObject > UI > Raw Image**)
4. Create an empty GameObject and name it `NasaManager`
5. Add your `ApodDisplay` script to the `NasaManager` GameObject
6. Drag your `NasaConfig.asset` from the Project window to the `Nasa Config` field in the Inspector
7. Drag the RawImage from your Hierarchy to the `Apod Display Image` field in the Inspector

## Run the Scene

Press Play! If everything is set up correctly, you should see today's Astronomy Picture of the Day load into your RawImage.

## Next Steps

- Check out the [sample scenes](samples.md) included with the SDK to see more examples
- Explore the other NASA APIs through the SDK's methods
- Try the Data Explorer window (**NASA > Data Explorer**) to preview data from the APIs directly in the editor
- Read the [configuration guide](configuration.md) to learn more about caching and other settings

## Troubleshooting

- If you encounter a "Demo API key rate limit exceeded" error, get your own API key from [api.nasa.gov](https://api.nasa.gov/)
- If the image doesn't load, make sure the APOD for today is an image and not a video (check `MediaType == "image"`)
- Check that all GameObject and component references are properly assigned