# AI Tweet Generator - n8n Workflow

An automated n8n workflow that generates AI-related tweets using Google's Gemini API and sends them to Telegram at scheduled intervals.

## 🚀 Features

- **Automated Scheduling**: Runs at 9 AM, 6 PM, and 10 PM daily
- **AI-Powered Content**: Uses Google Gemini 2.0 Flash to generate engaging tweets
- **Telegram Integration**: Sends generated tweets directly to your Telegram chat
- **Random Topic Selection**: Covers 5 different AI-related categories
- **Recent News Focus**: Ensures content is based on developments from the last 7 days

## 📋 Prerequisites

Before setting up this workflow, you'll need:

1. **n8n Instance**: Self-hosted or cloud instance
2. **Google Gemini API Key**: From Google AI Studio
3. **Telegram Bot**: Created via BotFather
4. **Telegram Chat ID**: Your personal or group chat ID

## 🛠️ Setup Instructions

### 1. Google Gemini API Setup

1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create a new API key
3. Copy the API key for later use

### 2. Telegram Bot Setup

1. Message [@BotFather](https://t.me/BotFather) on Telegram
2. Use `/newbot` command to create a new bot
3. Follow the instructions and save your bot token
4. Get your chat ID by messaging [@userinfobot](https://t.me/userinfobot)

### 3. n8n Workflow Configuration

1. Import the workflow JSON file into your n8n instance
2. Configure the following credentials and parameters:

#### Gemini API Node
- Replace `YOUR_GEMINI_API_KEY_HERE` with your actual Gemini API key

#### Telegram Node
- Replace `YOUR_TELEGRAM_CHAT_ID` with your actual chat ID
- Set up Telegram credentials in n8n:
  - Go to Credentials → Add Credential → Telegram
  - Enter your bot token
  - Replace `YOUR_TELEGRAM_CREDENTIAL_ID` with the credential ID

#### Additional IDs to Update
- Replace `YOUR_WEBHOOK_ID` with a unique webhook ID
- Replace `MASKED_INSTANCE_ID` with your n8n instance ID
- Replace `MASKED_VERSION_ID` with a version identifier
- Replace `MASKED_WORKFLOW_ID` with a unique workflow ID

## 🔧 Workflow Structure

```
Schedule (Cron) → Gemini API → Extract Tweet → Send to Telegram
```

### Node Details

1. **Schedule Node**: 
   - Type: `n8n-nodes-base.cron`
   - Triggers: 9:00, 18:00, 22:00 daily

2. **Gemini API Node**:
   - Type: `n8n-nodes-base.httpRequest`
   - Method: POST
   - Endpoint: Gemini 2.0 Flash API

3. **Extract Tweet Node**:
   - Type: `n8n-nodes-base.function`
   - Extracts tweet content from API response

4. **Send to Telegram Node**:
   - Type: `n8n-nodes-base.telegram`
   - Sends formatted message to specified chat

## 📝 Tweet Categories

The workflow randomly selects from these AI-related categories:

1. **New AI Models**: Latest model releases and updates
2. **AI Tools**: Newly released applications and software
3. **Research Papers**: Trending academic publications
4. **Ethical/Legal Debates**: Current discussions in AI ethics
5. **Company Announcements**: Major corporate AI news

## 🔄 Customization Options

### Modify Schedule
Edit the `triggerTimes` in the Schedule node to change when tweets are generated:

```json
"triggerTimes": {
  "item": [
    {"hour": 9},   // 9 AM
    {"hour": 18},  // 6 PM  
    {"hour": 22}   // 10 PM
  ]
}
```

### Update Prompt
Modify the `text` field in the Gemini API node to change the tweet generation prompt:

```json
"text": "Your custom prompt here..."
```

### Change Output Format
Edit the Telegram message template in the "Send to Telegram" node:

```json
"text": "=📝 New Tweet Idea:\n\n{{$node[\"Extract Tweet\"].json[\"tweet\"]}}\n"
```

## 🚨 Security Considerations

- Never commit API keys to version control
- Use environment variables for sensitive data
- Regularly rotate API keys
- Monitor API usage and costs
- Review generated content before posting

## 📊 Monitoring & Troubleshooting

### Common Issues

1. **API Key Invalid**: Verify Gemini API key is correct and active
2. **Telegram Not Receiving**: Check bot token and chat ID
3. **Schedule Not Triggering**: Ensure workflow is active
4. **Content Extraction Failed**: Check Gemini API response format

### Logs
Monitor workflow execution in n8n's execution log for debugging.

## 🔄 Workflow Versions

- **Current Version**: 1.0
- **n8n Version Compatibility**: 0.235.0+
- **Node Versions**: 
  - Cron: v1
  - HTTP Request: v1
  - Function: v1
  - Telegram: v1

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 🆘 Support

If you encounter any issues:

1. Check the [n8n documentation](https://docs.n8n.io/)
2. Review [Gemini API documentation](https://ai.google.dev/docs)
3. Open an issue in this repository
4. Join the [n8n community](https://community.n8n.io/)

## 📚 Additional Resources

- [n8n Official Documentation](https://docs.n8n.io/)
- [Google Gemini API Guide](https://ai.google.dev/tutorials/get_started_web)
- [Telegram Bot API](https://core.telegram.org/bots/api)
- [Cron Expression Generator](https://crontab.guru/)

## ⚠️ Disclaimer

This workflow generates AI content automatically. Always review generated tweets before posting to social media. Be mindful of:

- Accuracy of information
- Compliance with platform guidelines  
- Potential bias in AI-generated content
- Rate limits and API costs

---

**Made with ❤️ and n8n**
