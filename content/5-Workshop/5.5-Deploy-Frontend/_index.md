---
title : "Deploy Frontend"
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

## Deploying the React Frontend

In this section, you will set up and run the React chat interface that connects to your FastAPI backend.

### Step 1: Clone or Create React Project

Create a new React application:

```bash
# Using Create React App
npx create-react-app ev-rental-frontend
cd ev-rental-frontend

# Or clone existing repository
git clone https://github.com/your-org/ev-rental-frontend.git
cd ev-rental-frontend
```

### Step 2: Install Dependencies

Install required npm packages:

```bash
# Core dependencies
npm install axios react-markdown
npm install @chakra-ui/react @emotion/react @emotion/styled framer-motion
npm install react-icons

# Or use package.json
npm install
```

**Sample package.json dependencies:**
```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "axios": "^1.6.2",
    "@chakra-ui/react": "^2.8.2",
    "@emotion/react": "^11.11.1",
    "@emotion/styled": "^11.11.0",
    "framer-motion": "^10.16.16",
    "react-markdown": "^9.0.1",
    "react-icons": "^4.12.0"
  }
}
```


### Step 3: Project Structure

Your frontend should have this structure:

```
ev-rental-frontend/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── App.js              # Main app component
│   ├── index.js            # Entry point
│   ├── components/
│   │   ├── ChatInterface.js   # Chat UI component
│   │   ├── MessageList.js     # Message display
│   │   └── InputBox.js        # User input
│   ├── services/
│   │   └── api.js          # API calls to backend
│   ├── utils/
│   │   └── constants.js    # Configuration
│   └── styles/
│       └── App.css
├── package.json
└── .env
```

### Step 4: Configure Environment Variables

Create `.env` file in the project root:

```bash
# .env
REACT_APP_API_URL=http://localhost:8000
REACT_APP_API_BASE_PATH=/api
```

⚠️ **Important:** In React, environment variables must start with `REACT_APP_` prefix.

### Step 5: Create API Service

Create `src/services/api.js`:

```javascript
import axios from 'axios';

const API_URL = process.env.REACT_APP_API_URL || 'http://localhost:8000';

const api = axios.create({
  baseURL: API_URL,
  headers: {
    'Content-Type': 'application/json',
  },
});

export const sendMessage = async (sessionId, message) => {
  try {
    const response = await api.post('/api/chat', {
      session_id: sessionId,
      message: message,
    });
    return response.data;
  } catch (error) {
    console.error('API Error:', error);
    throw error;
  }
};

export default api;
```

### Step 6: Create Chat Interface Component

Create `src/components/ChatInterface.js`:

```javascript
import React, { useState, useEffect, useRef } from 'react';
import {
  Box,
  VStack,
  HStack,
  Input,
  Button,
  Text,
  Container,
  Heading,
} from '@chakra-ui/react';
import ReactMarkdown from 'react-markdown';
import { sendMessage } from '../services/api';

function ChatInterface() {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState('');
  const [loading, setLoading] = useState(false);
  const [sessionId] = useState(() => 
    `session-${Date.now()}-${Math.random().toString(36).substr(2, 9)}`
  );
  const messagesEndRef = useRef(null);

  const scrollToBottom = () => {
    messagesEndRef.current?.scrollIntoView({ behavior: 'smooth' });
  };

  useEffect(() => {
    scrollToBottom();
  }, [messages]);

  const handleSend = async () => {
    if (!input.trim()) return;

    const userMessage = { role: 'user', content: input };
    setMessages((prev) => [...prev, userMessage]);
    setInput('');
    setLoading(true);

    try {
      const response = await sendMessage(sessionId, input);
      const assistantMessage = {
        role: 'assistant',
        content: response.response,
        data: response.data,
      };
      setMessages((prev) => [...prev, assistantMessage]);
    } catch (error) {
      const errorMessage = {
        role: 'error',
        content: 'Failed to get response. Please try again.',
      };
      setMessages((prev) => [...prev, errorMessage]);
    } finally {
      setLoading(false);
    }
  };

  return (
    <Container maxW="container.md" py={8}>
      <VStack spacing={4} align="stretch">
        <Heading size="lg">🚗 EV Rental AI Agent</Heading>
        
        <Box
          border="1px"
          borderColor="gray.200"
          borderRadius="lg"
          p={4}
          h="500px"
          overflowY="auto"
          bg="gray.50"
        >
          <VStack spacing={3} align="stretch">
            {messages.map((msg, idx) => (
              <Box
                key={idx}
                alignSelf={msg.role === 'user' ? 'flex-end' : 'flex-start'}
                maxW="80%"
                bg={msg.role === 'user' ? 'blue.500' : 'white'}
                color={msg.role === 'user' ? 'white' : 'black'}
                p={3}
                borderRadius="lg"
                boxShadow="sm"
              >
                {msg.role === 'assistant' ? (
                  <ReactMarkdown>{msg.content}</ReactMarkdown>
                ) : (
                  <Text>{msg.content}</Text>
                )}
              </Box>
            ))}
            {loading && (
              <Box alignSelf="flex-start" maxW="80%">
                <Text color="gray.500">Typing...</Text>
              </Box>
            )}
            <div ref={messagesEndRef} />
          </VStack>
        </Box>

        <HStack>
          <Input
            value={input}
            onChange={(e) => setInput(e.target.value)}
            onKeyPress={(e) => e.key === 'Enter' && handleSend()}
            placeholder="Ask about vehicle rentals, policies, or charging stations..."
            disabled={loading}
          />
          <Button
            onClick={handleSend}
            colorScheme="blue"
            isLoading={loading}
            disabled={loading}
          >
            Send
          </Button>
        </HStack>
      </VStack>
    </Container>
  );
}

export default ChatInterface;
```

### Step 7: Update App.js

Update `src/App.js`:

```javascript
import React from 'react';
import { ChakraProvider } from '@chakra-ui/react';
import ChatInterface from './components/ChatInterface';

function App() {
  return (
    <ChakraProvider>
      <ChatInterface />
    </ChakraProvider>
  );
}

export default App;
```


### Step 8: Run the Frontend

Start the React development server:

```bash
npm start
```

**Expected output:**
```
Compiled successfully!

You can now view ev-rental-frontend in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://192.168.1.10:3000
```

The application will automatically open in your browser at `http://localhost:3000`.

### Step 9: Test the Chat Interface

Try these sample queries:

1. **Knowledge Base Query:**
   - "Chính sách thuê xe là gì?"
   - "Tôi cần giấy tờ gì để thuê xe?"

2. **Vehicle Search:**
   - "Tìm xe VinFast VF8 ở Hà Nội từ ngày 20/12"
   - "Có xe nào available?"

3. **Charging Station:**
   - "Trạm sạc gần Hoàn Kiếm"
   - "Tìm trạm sạc ở Quận 1"

### Verification Checklist

Before proceeding, ensure:

- ✅ Node.js and npm installed
- ✅ All dependencies installed successfully
- ✅ `.env` file configured with backend URL
- ✅ Backend server running on port 8000
- ✅ Frontend running on port 3000
- ✅ Chat interface loads without errors
- ✅ Can send messages and receive responses
- ✅ Markdown formatting displays correctly

### Troubleshooting

**Issue: "Module not found"**
- Solution: Delete `node_modules` and run `npm install` again
- Check package.json for correct versions

**Issue: "Network Error" when sending messages**
- Check backend is running: `curl http://localhost:8000/health`
- Verify REACT_APP_API_URL in `.env`
- Check browser console for CORS errors

**Issue: "CORS policy error"**
- Ensure backend has CORS middleware configured
- Check `allow_origins` includes `http://localhost:3000`

**Issue: Port 3000 already in use**
- Change port: `PORT=3001 npm start`
- Or kill existing process

**Issue: Markdown not rendering**
- Verify `react-markdown` is installed
- Check import statement in ChatInterface.js

---

**Next:** Proceed to [Testing](../5.6-Testing/) to verify all features work correctly.
