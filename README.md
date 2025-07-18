# Telegram Channel Saver

A Python tool for saving and analyzing Telegram channel content, including messages, users, and media.

## Features

- Save channel messages with reactions and media information
- Track channel users and their activity
- Search through saved messages
- Download and manage video content (including video circles/video messages)
- Support for multiple Telegram accounts
- Message download with rate limiting and error handling
- Detailed statistics about saved content

## Project Structure

```
/telegram-channel-saver/
  ├── LICENSE             # MIT License
  ├── README.md           # Project documentation
  ├── docs/               # Documentation directory
  │   ├── codebase.md     # Codebase documentation
  │   ├── contributing.md # Contribution guidelines
  │   ├── faq.md          # Frequently asked questions
  │   ├── setup.md        # Setup instructions
  │   └── telethon.txt    # Telethon library documentation
  ├── requirements.txt    # Project dependencies
  ├── main.py             # Main entry point
  ├── CLAUDE.md           # Best practices and code guidelines
  ├── src/                # Source code directory
  │   ├── __init__.py     # Package initialization
  │   ├── app.py          # Application initialization
  │   ├── channels.py     # Channel management
  │   ├── client.py       # Telegram client operations
  │   ├── config.py       # Application configuration
  │   ├── database.py     # Database operations
  │   ├── media.py        # Media file handling
  │   ├── messages.py     # Message operations
  │   └── users.py        # User tracking
  └── temp/               # Storage directory for data and sessions
```

## Author

Created by [Sergey Bulaev](https://t.me/sergiobulaev) - Follow my Telegram channel about AI and technology for more projects and updates.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/chubajs/telegram-channel-saver.git
   cd telegram-channel-saver
   ```

2. Create and activate virtual environment:
   ```bash
   # On Windows
   python -m venv venv
   venv\Scripts\activate

   # On macOS/Linux
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Get your Telegram API credentials:
   - Go to https://my.telegram.org/apps
   - Create a new application
   - Note your `api_id` and `api_hash`

5. Create a `.env` file in the project root directory:
   ```
   # Telegram API Credentials
   API_ID=your_api_id      # numbers only, no quotes
   API_HASH=your_api_hash  # string, no quotes
   
   # Optional: OpenRouter API Key for AI image analysis
   OPENROUTER_API_KEY=your_openrouter_api_key
   ```

## Usage

1. Run the application:
   ```bash
   python main.py
   ```

2. First-time setup:
   - Enter your phone number in international format
   - Enter the verification code sent to your Telegram
   - If you have 2FA enabled, enter your password

3. Main features:
   - List and select channels/groups
   - Save channel messages and users
   - Search through saved content
   - Browse messages with pagination and HTML viewing
   - View statistics and user information
   - Manage multiple Telegram sessions

### Message Download Options

- Download new messages only
- Force redownload all messages
- Download most recent messages (specify count)
- Download messages by ID range (specify min and max IDs)
- Automatic media download (videos, photos, files) with all messages
- Set custom message limits
- Automatic rate limiting to avoid API restrictions (respects Telegram's 100 messages per request limit)

### Media & Video Features

- Automatic media downloading with message saving
- Dedicated video download feature for targeted video downloading
- Download all video types or video circles (round video messages) only
- View information about downloaded videos
- Enhanced media download with:
  - Timeout handling for large files
  - Chunked downloading for better reliability
  - Progressive download with progress indication
  - Retry mechanism with exponential backoff
  - Detailed error reporting and recovery options
- Automatic handling of rate limits during download
- Media files stored locally in temp/videos directory

### Search Features

- Search by text content
- Search by date range
- Search by message ID
- Filter messages with reactions
- Filter messages with media
- View user's last messages

### Message Browsing Features

- Browse saved messages with pagination (10 messages per page)
- Navigate through message pages with simple commands
- Jump to specific messages by ID or page number
- View message HTML source with proper formatting
- Interactive navigation with next/previous page controls
- Message preview with ID, date, sender, and content snippet

### Export Features

- Export all messages from a channel to a text file
- Export messages from a specific user in a channel
- Export individual message files with AI-powered image analysis
- Channel statistics display (message count, media count, user count)
- Formatted export with original timestamps, user information, and replies
- Automatic file naming with channel ID, channel name, and timestamp
- Export files stored in 'exports' directory
- Media group handling for related messages
- OpenRouter API integration for GPT-4 image analysis

## Data Storage

All data is stored locally in JSON format:
- Messages and reactions
- User information
- Channel/group details
- Session data

Data location: 
- Messages and user data: `temp/channel_saver/database.json`
- Downloaded media: `temp/media/`
- Downloaded videos: `temp/videos/`
- Exported message logs: `exports/`

## Configuration

Default settings (can be modified in `src/config.py`):
- `MESSAGES_BATCH_SIZE = 100` - Messages per batch
- `BATCH_DELAY = 2` - Delay between batches (seconds)
- `SAVE_INTERVAL = 300` - Database save interval (seconds)
- `MAX_RETRIES = 3` - Maximum retry attempts
- `MEDIA_DOWNLOAD_DELAY = 3` - Delay between media downloads (seconds)
- `MEDIA_DOWNLOAD_TIMEOUT = 120` - Timeout for media downloads (seconds)
- `MEDIA_DOWNLOAD_RETRY = 3` - Maximum retries for failed media downloads
- `MEDIA_RETRY_DELAY_BASE = 5` - Base delay for exponential backoff (seconds)
- `CHUNK_SIZE = 1048576` - 1MB chunk size for large downloads
- `VIDEO_TEMP_DIR = 'temp/videos'` - Directory for storing downloaded videos

## Error Handling

- Automatic retry on failed requests
- Advanced media download error handling:
  - Smart retry with exponential backoff and jitter
  - Specific handling for different error types (timeout, network, server)
  - File verification after download
  - Detailed logging and statistics
- Session management and recovery
- Corrupted database detection
- Rate limit compliance with proper backoff strategies

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Documentation

Detailed documentation is available in the `docs/` directory:
- [Setup Instructions](docs/setup.md) - How to set up the project
- [Codebase Overview](docs/codebase.md) - Overview of the codebase structure
- [Contributing Guidelines](docs/contributing.md) - How to contribute to the project
- [Frequently Asked Questions](docs/faq.md) - Common questions and answers

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Disclaimer

This tool is for educational purposes only. Make sure to comply with Telegram's Terms of Service and API usage guidelines when using this application.

## Support

If you encounter any issues or have questions, please open an issue in the GitHub repository.

## Troubleshooting

Common issues:
1. **API Credentials Error**: Make sure your `.env` file exists and contains valid API credentials
2. **Database Errors**: Check if the temp directory has proper write permissions
3. **Rate Limiting**: If you encounter frequent rate limits, try increasing `BATCH_DELAY` and `MEDIA_DOWNLOAD_DELAY`
4. **Media Download Timeouts**: For large files that consistently timeout:
   - Increase `MEDIA_DOWNLOAD_TIMEOUT` for more time per download
   - Ensure you have sufficient disk space
   - Check your network connection stability
   - Try downloading smaller files first to confirm system functionality
5. **Server Errors During Download**: These are usually temporary; the retry mechanism should handle them automatically. If they persist, try again later as Telegram servers might be experiencing issues.
6. **Download Progress Stalls**: Some very large files might appear to stall during download. The progress indicator will update when data is actively being received. Consider adjusting `CHUNK_SIZE` if downloading large files (>100MB).