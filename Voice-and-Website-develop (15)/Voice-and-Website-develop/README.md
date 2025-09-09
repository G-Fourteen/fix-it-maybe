# Voice and Website

This repository contains the current chat interface under the `ai2` directory.
The folders `ai` and `Unity-Jailbreak Voice Chat` are legacy versions kept only for reference and are not used in the active build.

## Pollinations API Token

To authenticate with the Pollinations text API, create a `.env` file in the project root (an example file is included) with your token:

```
POLLINATIONS_API_TOKEN=your_token_here
```

The application will automatically read this value at runtime and include it with all text requests.
