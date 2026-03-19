# Customer Support N8N Workflow

An intelligent automated customer support system built with N8N that processes incoming emails, categorizes them using AI, generates appropriate responses, and logs tickets for tracking.

## 🚀 Features

- **Email Processing**: Automatically monitors Gmail inbox for new support emails
- **AI-Powered Classification**: Uses LangChain agents to categorize tickets into Billing, Tech, Orders, or FAQs
- **Priority Detection**: Automatically assigns priority levels (low, medium, high)
- **Smart Responses**: Generates contextual replies using specialized AI agents for each category
- **Ticket Logging**: Stores all ticket data in Google Sheets for tracking and analytics
- **High-Priority Alerts**: Sends Slack notifications for urgent tickets
- **FAQ Knowledge Base**: Integrates with vector database for intelligent FAQ responses

## 📋 Workflow Architecture

### 1. Email Trigger
- **Node**: Gmail Trigger
- **Function**: Monitors Gmail inbox every minute for new support emails
- **Authentication**: OAuth2 with Gmail account

### 2. Data Processing
- **Node**: Clean Email
- **Function**: Extracts and structures email data (Subject, Text, From)

### 3. AI Classification
- **Node**: Ticket Classifier (LangChain Agent)
- **Model**: OpenRouter Chat Model
- **Function**: 
  - Categorizes emails into: Billing, Tech, Orders, FAQs
  - Detects priority levels
  - Generates structured ticket data
  - Creates ticket summaries

### 4. Ticket Management
- **Node**: Randomization
- **Function**: Generates unique ticket IDs
- **Node**: Ticket Data (Google Sheets)
- **Function**: Logs all ticket information to tracking spreadsheet

### 5. Category-Based Routing
- **Node**: Switch
- **Function**: Routes tickets to specialized handling based on category

### 6. Specialized AI Agents

#### Billing Agent
- **Model**: OpenAI GPT-4o-mini
- **Specialization**: Payment issues, invoices, refunds, subscription questions
- **Tone**: Empathetic and financially sensitive

#### Tech Agent
- **Model**: OpenAI GPT-4o-mini
- **Specialization**: Technical problems, bugs, troubleshooting, account access
- **Tone**: Clear technical explanations with simple terms

#### Order Tracking Agent
- **Model**: Groq Llama 3.1 8B Instant
- **Specialization**: Order status, tracking, delivery information
- **Tone**: Reassuring and informative

#### FAQ Agent
- **Model**: OpenAI GPT-5-mini
- **Knowledge Base**: Pinecone vector store with FAQ documents
- **Specialization**: General company, product, and service questions
- **Features**: Intelligent document retrieval and search

### 7. Response Delivery
- **Node**: Reply to Gmail
- **Function**: Sends AI-generated responses to customers
- **Features**: Professional formatting, no attribution

### 8. High-Priority Alerting
- **Node**: IF Conditions
- **Function**: Detects high-priority tickets
- **Node**: Slack Notifications
- **Function**: Sends immediate alerts to support team channel

## 🔧 Technical Components

### AI Models Used
- **OpenRouter**: For initial ticket classification
- **OpenAI GPT-4o-mini**: For billing and technical responses
- **Groq Llama 3.1 8B**: For order tracking responses
- **OpenAI GPT-5-mini**: For FAQ responses

### Integrations
- **Gmail**: Email receiving and sending
- **Google Sheets**: Ticket logging and tracking
- **Google Drive**: FAQ document storage
- **Slack**: Team notifications
- **Pinecone**: Vector database for FAQ knowledge base

### Data Flow
```
Email → Classification → Ticket ID → Google Sheets → Category Routing → AI Response → Email Reply
                                      ↓
                              High Priority Check → Slack Alert
```

## 📊 Categories Handled

### 💳 Billing
- Payment issues and failures
- Invoice inquiries
- Refund requests
- Subscription management
- Account billing questions

### 🔧 Technical Support
- Bug reports and issues
- Account access problems
- Feature troubleshooting
- Technical guidance
- System errors

### 📦 Order Management
- Order status inquiries
- Shipping and tracking
- Delivery issues
- Order modifications
- Returns and exchanges

### ❓ Frequently Asked Questions
- Company information
- Product details
- Service hours
- Contact information
- General inquiries

## 🛠️ Setup Requirements

### N8N Credentials Needed
1. **Gmail OAuth2**: Email access
2. **Google Sheets OAuth2**: Spreadsheet access
3. **Google Drive OAuth2**: Document access
4. **Slack OAuth2**: Team notifications
5. **OpenAI API**: AI model access
6. **Groq API**: Fast model access
7. **OpenRouter API**: Classification model
8. **Pinecone API**: Vector database

### External Resources
1. **Google Sheets**: Ticket tracking spreadsheet
2. **Google Drive**: FAQ documents (PDFs)
3. **Pinecone Index**: FAQ vector store
4. **Slack Channel**: Support team notifications

## 📈 Benefits

- **24/7 Availability**: Automated responses round the clock
- **Consistent Quality**: Standardized response quality across all categories
- **Reduced Response Time**: Instant email processing and replies
- **Smart Triage**: Automatic categorization and priority detection
- **Team Awareness**: Immediate alerts for urgent issues
- **Data Analytics**: Comprehensive ticket tracking in Google Sheets
- **Scalability**: Handles increasing email volumes without additional staff

## 🔍 Monitoring and Analytics

The workflow provides comprehensive tracking through:
- **Google Sheets**: Complete ticket history with timestamps, categories, and priorities
- **Slack Notifications**: Real-time alerts for high-priority issues
- **Response Logs**: All AI-generated responses are logged for quality assurance

## 🚀 Deployment

1. Import the `Customer Support.json` workflow into your N8N instance
2. Configure all required credentials
3. Set up the Google Sheets tracking spreadsheet
4. Upload FAQ documents to Google Drive
5. Configure Pinecone vector store
6. Set up Slack channel for notifications
7. Test with sample emails in each category
8. Activate the workflow

## 📞 Support

This automated system handles the majority of common customer inquiries while ensuring that complex or high-priority issues are immediately flagged for human attention. The combination of AI-powered responses and intelligent routing ensures customers receive fast, accurate, and appropriate support.

