# 🤖 SmartMail Agent – AI Email Assistant via WhatsApp

An intelligent n8n workflow that lets you manage your Gmail inbox through WhatsApp using voice or text commands. Powered by OpenAI GPT-4 and Whisper for natural language understanding and voice transcription.

![n8n](https://img.shields.io/badge/n8n-Workflow-EA4B71)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-412991)
![WhatsApp](https://img.shields.io/badge/WhatsApp-Business-25D366)
![Gmail](https://img.shields.io/badge/Gmail-API-EA4335)

## ✨ Features

- 📱 **WhatsApp Integration** – Send voice or text commands via WhatsApp
- 🎤 **Voice Recognition** – Automatic transcription using OpenAI Whisper
- 📧 **Email Management** – Send emails, create drafts, and retrieve contact info
- 🧠 **AI-Powered** – GPT-4 understands context and intent in French & English
- 🔊 **Voice Responses** – Receive audio confirmations back via WhatsApp
- 📊 **Contact Database** – Integrates with Airtable for contact lookup
- 💬 **Bilingual Support** – Works in both French and English

## 🏗️ Architecture

The workflow consists of three main parts:

### 🟫 Part 1: Message Intake & Voice Transcription
Receives WhatsApp messages, identifies message type (text/audio), downloads and transcribes voice messages using OpenAI Whisper.

### 🟩 Part 2: Smart Email Agent
Processes commands using GPT-4, retrieves contact information from Airtable, and performs email actions (send, draft, reply).

### 🟥 Part 3: Voice Response & Feedback
Generates personalized responses, converts to speech if needed, and sends confirmations back via WhatsApp.

## 🧩 Prerequisites

Before deploying this workflow, ensure you have:

- ✅ **WhatsApp Business Cloud API** access with registered phone number
- ✅ **OpenAI API Key** (for GPT-4 and Whisper)
- ✅ **Gmail/Google Workspace** account with OAuth2 credentials
- ✅ **Airtable account** (free plan sufficient)
- ✅ **n8n instance** (cloud or self-hosted with HTTPS)
- ✅ Basic familiarity with n8n workflow builder

⏱️ **Estimated setup time:** 30-60 minutes

## 🚀 Installation

### 1. Clone or Import Workflow

Import the provided JSON file into your n8n instance:

```bash
# In n8n UI
Workflows → Import from File → Select the JSON file
```

### 2. Configure API Credentials

Set up the following credentials in n8n:

#### WhatsApp Business Cloud API
- Navigate to **Credentials** → **Add Credential** → **WhatsApp**
- Enter your access token and phone number ID
- Configure webhook URL in Meta Developer Console

#### OpenAI API
- Add **OpenAI** credential with your API key
- Used for both GPT-4 Chat and Whisper transcription

#### Gmail OAuth2
- Create OAuth2 credentials in Google Cloud Console
- Enable Gmail API
- Add authorized redirect URI for n8n
- Configure in n8n credentials

#### Airtable
- Generate Personal Access Token in Airtable
- Create a base with contact information (email, name, etc.)
- Add credential in n8n

### 3. Configure Airtable Base

Create an Airtable base with at least these fields:
- Name (Single line text)
- Email (Email)
- Company (Single line text)
- Additional custom fields as needed

### 4. Update Node Configurations

Update the following nodes with your specific IDs:

- **WhatsApp nodes**: Update `phoneNumberId` and `recipientPhoneNumber`
- **Airtable node**: Update `base` and `table` IDs
- **Email Agent**: Adjust system message if needed

### 5. Activate Workflow

Click **Active** toggle in n8n to start listening for WhatsApp messages.

## 📖 Usage Examples

### Send an Email
**Voice/Text:** "Send an email to Florence"

**Result:** AI composes and sends an email to Florence's address from your contact database

### Create Draft
**Voice/Text:** "Draft an email to John about the meeting tomorrow"

**Result:** Creates a Gmail draft with suggested content

### Casual Interaction
**Text:** "Bonjour"

**Response:** "Bonjour ! Ça va très bien, merci. Comment puis-je vous aider aujourd'hui ?"

## 🎯 How It Works

1. **Message Reception**: WhatsApp webhook receives your message
2. **Type Detection**: Switch node identifies text or audio
3. **Transcription**: If audio, Whisper converts speech to text
4. **Intent Analysis**: GPT-4 understands your command
5. **Contact Lookup**: Retrieves email address from Airtable
6. **Email Action**: Sends email or creates draft via Gmail API
7. **Confirmation**: Returns text or voice confirmation to WhatsApp

## 🔧 Customization

### Modify AI Behavior

Edit the system message in the **Email Agent** node to change:
- Response tone and style
- Language preferences
- Email formatting rules
- Default behaviors

### Add New Email Actions

The workflow uses LangChain tools. You can add:
- Read/Search emails
- Forward emails
- Manage labels
- Schedule send times

### Voice Response Settings

Adjust voice parameters in the **OpenAI1** (TTS) node:
- Voice selection (nova, alloy, echo, fable, onyx, shimmer)
- Speed and tone

## 🔒 Security Best Practices

- ⚠️ **Never hardcode API keys** – use n8n environment variables
- 🔐 **Secure webhooks** with custom headers or tokens
- 📊 **Monitor usage** regularly in API dashboards
- 🛡️ **Limit recipient numbers** in WhatsApp nodes for testing
- 🔍 **Review logs** for suspicious activity
- ✅ **Use error handling** nodes for graceful failures

## 🐛 Troubleshooting

### Voice Messages Not Transcribing
- Verify OpenAI API key has Whisper access
- Check audio file download in HTTP Request node
- Ensure WhatsApp media permissions are configured

### Emails Not Sending
- Confirm Gmail OAuth2 token hasn't expired
- Check Gmail API quotas
- Verify recipient email format

### Airtable Lookup Failing
- Validate base and table IDs
- Check filter formula syntax
- Ensure Personal Access Token has read permissions

### WhatsApp Connection Issues
- Verify webhook URL is publicly accessible (HTTPS)
- Check phone number ID is correct
- Review Meta App settings and permissions

## 📚 Additional Resources

- [n8n Documentation](https://docs.n8n.io)
- [WhatsApp Business Cloud API](https://developers.facebook.com/docs/whatsapp/cloud-api)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)
- [Gmail API Guide](https://developers.google.com/gmail/api)

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Test thoroughly
4. Submit a pull request with clear description

## 📄 License

This project is provided as-is for educational and personal use.

## 💡 Tips for Best Results

- Use clear, concise voice commands
- Mention recipient names as they appear in your Airtable
- Test with text commands first before using voice
- Start with simple commands and build complexity
- Keep Airtable contact data updated and clean

## 🙏 Acknowledgments

Built with:
- [n8n](https://n8n.io) – Workflow automation
- [OpenAI](https://openai.com) – GPT-4 and Whisper
- [WhatsApp Business](https://business.whatsapp.com) – Messaging platform
- [Airtable](https://airtable.com) – Contact database

---

**Made with ❤️ using n8n and AI**

*For questions or support, please open an issue in the repository.*
