# Multi-Bot System (Telegram & WhatsApp)

This is a full-featured Node.js bot system that integrates both Telegram and WhatsApp, designed to run efficiently on Termux (Android without root). It supports multi-user sessions, allowing each Telegram user to pair their own WhatsApp account. The system is modular, with commands separated into distinct files, and includes a JSON database for user data and settings.

## Features

### Core Features
- **Telegram Integration**: Uses `node-telegram-bot-api` for Telegram bot functionalities.
- **WhatsApp Integration**: Uses `Baileys` (latest version) for WhatsApp bot functionalities.
- **Termux Compatibility**: Optimized to run on Termux without root access.
- **Multi-User Sessions**: Each Telegram user can pair and manage their own WhatsApp account.
- **Session Storage**: WhatsApp sessions are stored using Baileys multi-file auth state.
- **User Data Storage**: User data and settings are stored in a JSON database.

### Telegram Side
- **`/start` Command**: Displays a welcome message and available commands.
- **`/pair <phone_number>` Command**: Generates a WhatsApp pairing code for the specified phone number.
- **Secure Pairing**: Only the requesting Telegram user receives their pairing code.
- **Separate Sessions**: Maintains distinct WhatsApp sessions for each Telegram user.
- **Connection Notifications**: Notifies the user upon successful WhatsApp connection.

### WhatsApp Side (after pairing)

The WhatsApp bot responds to commands using a configurable prefix (default: `.`) and includes the following menus:

#### FUN MENU
- `joke`: Tells a random joke.
- `meme`: Sends a random meme image.
- `truth`: Provides a truth question.
- `dare`: Provides a dare challenge.
- `compliment`: Sends a random compliment.
- `quote`: Sends a random inspirational quote.
- `tictactoe`: Initiates a Tic-Tac-Toe game (placeholder).
- `wcg`: Initiates a Word Guessing Game (placeholder).

#### OWNER MENU
- `restart bot`: Restarts the bot process.
- `block <user>`: Blocks a specified WhatsApp user.
- `unblock <user>`: Unblocks a specified WhatsApp user.
- `autostatus`: Toggles auto-viewing of WhatsApp statuses.
- `autorecording`: Toggles auto-recording presence.
- `autotyping`: Toggles auto-typing presence.
- `setprefix <prefix>`: Sets a custom command prefix.
- `private`: Sets the bot to private mode (only owner commands).
- `public`: Sets the bot to public mode (all commands available).
- `ping`: Checks bot latency.
- `uptime`: Shows bot uptime.

#### DOWNLOAD MENU
- `ytmp3 <link/query>`: Downloads YouTube video as MP3.
- `ytmp4 <link/query>`: Downloads YouTube video as MP4.
- `tiktok <link>`: Downloads TikTok video.
- `instagram <link>`: Downloads Instagram post.
- `facebook <link>`: Downloads Facebook video.
- `spotify <link>`: Downloads Spotify track.
- `snapchat <link>`: Downloads Snapchat content.
- `mp3 <query>`: Searches and downloads MP3.
- `mp4 <query>`: Searches and downloads MP4.

#### GROUP MENU
- `kick <user>`: Kicks a user from the group.
- `promote <user>`: Promotes a user to admin.
- `demote <user>`: Demotes an admin to participant.
- `tagall [message]`: Tags all group members.
- `welcome`: Toggles welcome message for new members (placeholder).
- `goodbye`: Toggles goodbye message for leaving members (placeholder).
- `antilink`: Toggles anti-link system.
- `antibot`: Toggles anti-bot system (placeholder).
- `antimention`: Toggles anti-group mention system (placeholder).
- `glink`: Gets the group invite link.
- `antispam`: Toggles anti-spam system (placeholder).
- `antibadword`: Toggles anti-bad words system.
- `list-active`: Lists active group members (placeholder).
- `add <number>`: Adds a user to the group (placeholder).
- `kickall`: Kicks all non-admin members (placeholder).
- `tagadmins [message]`: Tags all group admins.
- `list-inactive`: Lists inactive group members (placeholder).

#### ANTIBUG SYSTEM (Middleware)
- **Auto-detect spam messages**: Identifies and acts on spam.
- **Auto-delete suspicious messages**: Deletes messages matching certain criteria.
- **Auto-block bulk messages**: Blocks users sending too many messages rapidly.
- **Auto-block offenders**: Blocks users who trigger antibug rules.
- **Anti-crash protection**: Robust error handling.
- **Spam protection**: Prevents message flooding.

#### SEARCH MENU
- `google <query>`: Performs a Google search.
- `youtube <query>`: Performs a YouTube video search.
- `github <query>`: Performs a GitHub repository search.
- `bing <query>`: Performs a Bing search.

#### OTHER MENU
- `dict <word>`: Provides dictionary definition.
- `exchange <currency>`: Shows exchange rates (placeholder).
- `weather <city>`: Shows weather information (placeholder).
- `gemini <prompt>`: Interacts with Gemini AI (placeholder).
- `chatgpt <prompt>`: Interacts with ChatGPT AI (placeholder).

#### STICKER MENU
- `take`: Creates a sticker from a replied image/video (placeholder).
- `tocircle`: Converts image to circular sticker (placeholder).
- `tosticker`: Converts image/video to sticker.
- `slap`: Sends a slap sticker/emoji.
- `smile`: Sends a smile sticker/emoji.
- `sad`: Sends a sad sticker/emoji.

### System Features
- **Auto Reconnect**: Automatically reconnects on disconnects.
- **Error Handling**: Comprehensive error handling for async functions.
- **Modular Structure**: Commands and functionalities separated into logical files.
- **Logging System**: Uses `pino` for efficient and readable logging.
- **Lightweight & Optimized**: Designed for mobile environments like Termux.

### Optional Advanced Features
- **Two-way Message Bridge**: (Telegram ↔ WhatsApp) - Partially implemented.
- **Web Dashboard**: Basic Express.js server for status monitoring.
- **Admin Authentication System**: (Placeholder).
- **Rate Limiting**: Prevents command abuse.
- **Reduce Payload**: (Optimization consideration).

## Folder Structure

```text
/home/ubuntu/multi-bot/
├── src/
│   ├── index.js                # Main entry point to start the bot
│   ├── config.js               # Configuration file for tokens, prefixes, etc.
│   ├── database/
│   │   └── db.json             # JSON database for storing user data and settings
│   ├── lib/
│   │   ├── telegram.js         # Handles Telegram bot logic and commands
│   │   ├── whatsapp.js         # Manages WhatsApp sessions and Baileys client
│   │   ├── session.js          # (Not explicitly created, integrated into whatsapp.js)
│   │   ├── logger.js           # Configures the Pino logging system
│   │   ├── database.js         # Database wrapper for db.json
│   │   ├── handler.js          # WhatsApp message handler and command dispatcher
│   │   └── bridge.js           # Handles message bridging between Telegram and WhatsApp
│   ├── commands/
│   │   ├── whatsapp/           # Directory for WhatsApp command modules
│   │   │   ├── fun.js          # Fun commands (joke, meme, truth, dare, etc.)
│   │   │   ├── owner.js        # Owner-specific commands (restart, block, settings)
│   │   │   ├── download.js     # Media download commands (YouTube, TikTok, etc.)
│   │   │   ├── group.js        # Group management commands (kick, promote, tagall)
│   │   │   ├── search.js       # Search commands (Google, YouTube, GitHub, Dictionary)
│   │   │   ├── sticker.js      # Sticker creation and manipulation commands
│   │   │   └── other.js        # Other utility commands (weather, Gemini, ChatGPT - placeholders)
│   │   └── telegram/           # Directory for Telegram command modules
│   │       └── start.js        # Telegram /start command handler
│   ├── middleware/
│   │   ├── antibug.js          # Antibug system for spam, anti-link, etc.
│   │   └── ratelimit.js        # Rate limiting middleware
│   └── web/
│       └── dashboard.js        # (Not explicitly created, integrated into index.js for simplicity)
├── sessions/                   # Directory to store Baileys multi-file authentication states
├── package.json                # Project dependencies and scripts
└── README.md                   # This documentation file
```

## Installation Steps

### 1. Termux Setup

If you don't have Termux installed, download it from F-Droid or Google Play Store. After installation, update and upgrade packages:

```bash
pkg update && pkg upgrade -y
```

Install Node.js and Git:

```bash
pkg install nodejs git -y
```

Install `ffmpeg` for media processing (e.g., sticker creation):

```bash
pkg install ffmpeg -y
```

### 2. Clone the Repository

Navigate to your desired directory in Termux and clone the bot system:

```bash
cd ~/
git clone https://github.com/YOUR_USERNAME/multi-bot.git # Replace with your repo URL or create manually
cd multi-bot
```

### 3. Install Dependencies

Install all required Node.js packages:

```bash
npm install
```

### 4. Configuration

Create a `.env` file in the root directory (`/home/ubuntu/multi-bot/`) and fill in your Telegram bot token and Telegram admin ID. You can get your Telegram bot token from BotFather on Telegram. Your Telegram admin ID can be obtained by forwarding a message from yourself to `@userinfobot`.

```
TELEGRAM_TOKEN=YOUR_TELEGRAM_BOT_TOKEN
ADMIN_ID=YOUR_TELEGRAM_ID
```

Edit `src/config.js` to set your WhatsApp owner number and other preferences:

```javascript
// src/config.js
module.exports = {
    telegram: {
        token: process.env.TELEGRAM_TOKEN || 'YOUR_TELEGRAM_BOT_TOKEN',
        adminId: process.env.ADMIN_ID || 'YOUR_TELEGRAM_ID' // Your Telegram User ID
    },
    whatsapp: {
        prefix: '.', // Default command prefix
        ownerNumber: 'YOUR_PHONE_NUMBER', // e.g. 2348123456789 (without +)
        botName: 'MultiBot',
        pairingCode: true // Use pairing code instead of QR
    },
    dbPath: './src/database/db.json',
    sessionPath: './sessions',
    port: process.env.PORT || 3000,
    logging: {
        level: 'info'
    }
};
```

### 5. Running the Bot

Start the bot using npm:

```bash
npm start
```

Or, if you want to use `nodemon` for automatic restarts during development (you'll need to install it globally or locally):

```bash
npm install -g nodemon # If not already installed
npm run dev
```

### 6. Pairing WhatsApp

Once the bot is running, go to your Telegram bot and use the `/pair` command with your WhatsApp phone number (including country code, without `+`):

```
/pair 2348123456789
```

The bot will send you a pairing code. Open WhatsApp on your phone, go to `Linked Devices` -> `Link with Phone Number`, and enter the provided code. Your WhatsApp account should then connect to the bot.

## Important Notes

- **API Keys**: For features like Gemini, ChatGPT, and some downloaders, you will need to obtain API keys from their respective services and integrate them into the relevant command files or `config.js`.
- **Termux Background**: To keep the bot running in the background on Termux, you can use `pm2`:
  ```bash
  npm install -g pm2
  pm2 start src/index.js --name multi-bot
  pm2 save
  pm2 startup
  ```
- **Security**: Be cautious with the commands you enable and the information you expose, especially in public groups. Always review the code before deploying.

## Contributing

Feel free to fork the repository, open issues, and submit pull requests to improve this multi-bot system.

## License

This project is open-source and available under the MIT License.
