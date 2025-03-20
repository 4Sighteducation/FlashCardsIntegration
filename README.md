# VESPA Flashcard Knack Integration

A JavaScript integration layer that bridges the gap between the VESPA Flashcards React app and the Knack platform.

## Overview

This integration script enables a React-based flashcard application to be embedded into a Knack platform page. It handles:

- Authentication & user data synchronization
- Secure communication via postMessage API
- Data storage & retrieval to/from Knack
- Error handling & data validation
- Cross-frame communication
- DOM manipulation for embedding

## Features

- **Robust Data Handling**: Includes safe URI decoding and JSON parsing with multiple fallback mechanisms
- **User Authentication**: Leverages Knack authentication for secure user identification
- **Connection Field Support**: Manages object relationships via Knack connection fields
- **Data Sanitization**: Cleans user inputs to prevent XSS and data corruption
- **Progressive Enhancement**: Multiple fallback methods for container selection
- **Spaced Repetition Support**: Specialized handling for spaced repetition data structures
- **HTML Cleaning**: Removes HTML tags from data that could cause rendering issues
- **Comprehensive Error Handling**: Graceful recovery from data loading/saving errors

## Installation

1. Create a JavaScript file in your Knack application
2. Add the following code to load the integration script:

```javascript
// Load VESPA Knack Integration from GitHub
(function() {
  var script = document.createElement('script');
  script.src = 'https://cdn.jsdelivr.net/gh/YourOrganization/YourRepo@main/knackIntegration.js';
  script.async = false; // Synchronous loading 
  script.onload = function() {
    console.log("VESPA Integration script loaded successfully");
  };
  script.onerror = function() {
    console.error("Failed to load VESPA Integration script from GitHub");
  };
  document.head.appendChild(script);
})();
```

3. Configure the integration:

```javascript
// Add this before loading the script
window.VESPA_CONFIG = {
  knackAppId: "your-knack-app-id",
  knackApiKey: "your-knack-api-key",
  appUrl: 'https://your-flashcard-app-url',
  // Optional custom configuration
  appConfig: {
    'scene_1206': {
      'view_3005': {
        appType: 'flashcard-app',
        elementSelector: '.kn-rich-text'
      }
    }
  }
};
```

## Knack Configuration Requirements

The integration expects the following fields to exist in your Knack application:

| Field Mapping | Description | Object | Field Type |
|---------------|-------------|--------|------------|
| field_2954 | User ID | object_102 | Text |
| field_2958 | User Email | object_102 | Email |
| field_2956 | Account Connection | object_102 | Connection |
| field_3008 | VESPA Customer Connection | object_102 | Connection |
| field_3009 | Tutor Connection | object_102 | Connection |
| field_2979 | Flashcard Bank JSON Store | object_102 | Text (Long) |
| field_2957 | Date Last Saved | object_102 | Date/Time |
| field_2986 | Box 1 JSON | object_102 | Text (Long) |
| field_2987 | Box 2 JSON | object_102 | Text (Long) |
| field_2988 | Box 3 JSON | object_102 | Text (Long) |
| field_2989 | Box 4 JSON | object_102 | Text (Long) |
| field_2990 | Box 5 JSON | object_102 | Text (Long) |
| field_3000 | Color Mapping | object_102 | Text (Long) |
| field_3011 | Topic Lists JSON | object_102 | Text (Long) |
| field_3030 | Topic Metadata JSON | object_102 | Text (Long) |
| field_3010 | User Name | object_102 | Text |
| field_565 | Tutor Group | object_102 | Text |
| field_548 | Year Group | object_102 | Text |
| field_73 | User Role | object_102 | Connection |

## React App Communication

The integration uses the `postMessage` API to communicate with the React app. It sends and receives messages with the following types:

### Messages to React App

- `KNACK_USER_INFO`: Sends user information and data to the React app
- `SAVE_RESULT`: Confirms save operation result
- `LOAD_SAVED_DATA`: Sends updated data from Knack

### Messages from React App

- `APP_READY`: Signals that the React app is loaded and ready to receive data
- `AUTH_CONFIRMED`: Confirms that authentication data was received 
- `SAVE_DATA`: Request to save data to Knack

## Error Handling

The integration includes robust error handling mechanisms:

1. **Safe URI Decoding**: Prevents crashes on malformed URI components
2. **JSON Recovery**: Multiple methods to recover from corrupt JSON data
3. **Connection Field Validation**: Ensures only valid Knack IDs are used
4. **HTML Sanitization**: Cleans potentially problematic HTML from fields
5. **Container Fallbacks**: Multiple strategies to find/create app containers

## Debugging

The integration includes detailed logging with the prefix "Flashcard app:" for easy filtering in the browser console. Set `localStorage.debug = 'flashcard:*'` in your browser console for even more detailed logs.

## Security Considerations

- API keys are stored in the Knack configuration, not in the GitHub repository
- Sanitization is applied to all user inputs to prevent injection attacks
- Connection fields are validated to ensure they contain valid Knack IDs
- HTML is stripped from sensitive fields

## Recent Updates

### Version 1.1.0
- Added safe URI decoding to prevent malformed URI errors
- Enhanced JSON parsing with multiple recovery mechanisms
- Improved error handling in data processing
- Added fallbacks for empty data structures

## License

MIT License

Copyright (c) 2025 4Sight Education

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

