# Setup Guide for Customer Support N8N Workflow

This guide will help you set up the Customer Support N8N workflow from scratch.

## Prerequisites

- N8N instance (cloud or self-hosted)
- Google Workspace account with Gmail, Sheets, and Drive access
- Slack workspace with admin access
- API accounts for AI services
- Basic understanding of N8N workflows

## Step 1: Import the Workflow

1. Open your N8N instance
2. Click "Import from file" or drag & drop
3. Select the `Customer Support.json` file
4. The workflow will be imported with all nodes and connections

## Step 2: Configure Credentials

### Gmail OAuth2
1. Go to Google Cloud Console
2. Create a new project or select existing
3. Enable Gmail API
4. Create OAuth2 credentials
5. Add the redirect URL from N8N
6. In N8N: Settings → Credentials → Add Credential → Gmail OAuth2
7. Enter client ID and secret
8. Complete the OAuth flow

### Google Sheets OAuth2
1. Enable Google Sheets API in Google Cloud Console
2. Use the same OAuth2 credentials as Gmail
3. In N8N: Add Google Sheets OAuth2 credential
4. Complete the authorization

### Google Drive OAuth2
1. Enable Google Drive API in Google Cloud Console
2. Use the same OAuth2 credentials
3. In N8N: Add Google Drive OAuth2 credential
4. Complete the authorization

### Slack OAuth2
1. Go to Slack API website
2. Create a new app
3. Add OAuth permissions for chat:write
4. Install app to workspace
5. Copy Bot User OAuth Token
6. In N8N: Add Slack OAuth2 credential
7. Enter the token

### OpenAI API
1. Sign up at OpenAI platform
2. Create an API key
3. In N8N: Add OpenAI API credential
4. Enter the API key

### Groq API
1. Sign up at Groq console
2. Create an API key
3. In N8N: Add Groq API credential
4. Enter the API key

### OpenRouter API
1. Sign up at OpenRouter
2. Create an API key
3. In N8N: Add OpenRouter API credential
4. Enter the API key

### Pinecone API
1. Sign up at Pinecone
2. Create an API key
3. Create an index named "customersupport"
4. In N8N: Add Pinecone API credential
5. Enter the API key

## Step 3: Set Up External Resources

### Google Sheets for Ticket Tracking
1. Create a new Google Sheet
2. Name it "Customer Support Tickets"
3. Create columns: Ticket ID, Email, Category, Priority, Status, Summary
4. Copy the sheet ID from the URL
5. Update the "Ticket data" node with your sheet ID

### Google Drive for FAQ Documents
1. Create a folder in Google Drive
2. Upload your FAQ PDFs
3. Get the file ID for your main FAQ document
4. Update the "Download file" node with your file ID

### Pinecone Vector Store
1. Create a new index in Pinecone
2. Name it "customersupport"
3. Set dimensions to 1536 (for OpenAI embeddings)
4. Update the "Pinecone Vector Store" node with your index name

### Slack Channel
1. Create a new Slack channel (e.g., #support-alerts)
2. Invite the Slack app to the channel
3. Copy the channel ID
4. Update all "Send a message" nodes with your channel ID

## Step 4: Test the Workflow

### Test Email Categories
Send test emails to your support address:

**Billing Test:**
```
Subject: Refund Request
I was charged twice for my subscription last month. Can you help me get a refund?
```

**Tech Test:**
```
Subject: Login Issues
I can't log into my account. It says my password is incorrect but I'm sure it's right.
```

**Order Test:**
```
Subject: Order Status
Where is my order #12345? It was supposed to arrive yesterday.
```

**FAQ Test:**
```
Subject: Company Hours
What are your business hours? I need to know when I can reach support.
```

### Verify Each Step
1. Check if emails are being received by the Gmail trigger
2. Verify classification is working correctly
3. Confirm tickets are being logged in Google Sheets
4. Check if replies are being sent
5. Verify Slack notifications for high-priority tickets
6. Test FAQ responses with the knowledge base

## Step 5: Activate the Workflow

1. Once all tests pass, click the "Active" toggle
2. The workflow will now run automatically
3. Monitor the first few real emails to ensure everything works

## Troubleshooting

### Common Issues

**Gmail not receiving emails:**
- Check OAuth2 credentials are properly configured
- Verify the Gmail account has the right permissions
- Check if the workflow is active

**AI responses not generating:**
- Verify API keys are valid and have credits
- Check if the correct models are selected
- Ensure the prompt templates are properly formatted

**Google Sheets not updating:**
- Verify sheet ID is correct
- Check OAuth2 permissions for Sheets
- Ensure column names match exactly

**Slack notifications not sending:**
- Verify channel ID is correct
- Check Slack app permissions
- Ensure the app is invited to the channel

**FAQ responses not working:**
- Verify Pinecone index is configured
- Check if documents are properly uploaded
- Ensure embeddings are generated correctly

### Debug Mode
1. Click on any node to see its input/output
2. Use the "Execute Node" button to test individual nodes
3. Check the execution history for errors
4. Enable debug logging in N8N settings

## Maintenance

### Regular Tasks
- Monitor API usage and credits
- Update FAQ documents as needed
- Review ticket categories and AI responses
- Check Google Sheets for data integrity
- Update Slack channel if needed

### Scaling Considerations
- Monitor email volume and response times
- Consider upgrading API plans for higher limits
- Add more categories as your business grows
- Implement additional AI models for better performance
- Set up monitoring and alerting for workflow failures

## Security Notes

- Never commit API keys to version control
- Use environment variables for sensitive data
- Regularly rotate API keys
- Monitor access logs for unusual activity
- Keep N8N updated to the latest version
- Use HTTPS for all external connections

## Support

If you encounter issues:
1. Check the N8N community forums
2. Review the execution logs
3. Test individual nodes
4. Verify all credentials are valid
5. Check API service status pages

For questions about this specific workflow, create an issue in the GitHub repository.
