---
title : "Triển khai Frontend"
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

## Triển khai Giao diện React Frontend

Trong phần này, bạn sẽ thiết lập và chạy giao diện chat React kết nối với backend FastAPI.

### Bước 1: Clone hoặc Tạo Dự án React

Tạo ứng dụng React mới:

```bash
# Sử dụng Create React App
npx create-react-app ev-rental-frontend
cd ev-rental-frontend

# Hoặc clone repository có sẵn
git clone https://github.com/your-org/ev-rental-frontend.git
cd ev-rental-frontend
```

### Bước 2: Cài đặt Thư viện

Cài đặt các gói npm cần thiết:

```bash
# Thư viện cốt lõi
npm install axios react-markdown
npm install @chakra-ui/react @emotion/react @emotion/styled framer-motion
npm install react-icons

# Hoặc dùng package.json
npm install
```

**Ví dụ dependencies trong package.json:**
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

![Cài đặt Thư viện](/images/5-Workshop/5.5-Deploy-Frontend/image-10.png)

### Bước 3: Cấu trúc Dự án

Frontend của bạn nên có cấu trúc như sau:

```
ev-rental-frontend/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── App.js              # Component chính
│   ├── index.js            # Entry point
│   ├── components/
│   │   ├── ChatInterface.js   # Component giao diện chat
│   │   ├── MessageList.js     # Hiển thị tin nhắn
│   │   └── InputBox.js        # Nhập liệu người dùng
│   ├── services/
│   │   └── api.js          # Gọi API tới backend
│   ├── utils/
│   │   └── constants.js    # Cấu hình
│   └── styles/
│       └── App.css
├── package.json
└── .env
```

### Bước 4: Cấu hình Biến Môi trường

Tạo file `.env` ở thư mục gốc dự án:

```bash
# .env
REACT_APP_API_URL=http://localhost:8000
REACT_APP_API_BASE_PATH=/api
```

⚠️ **Quan trọng:** Trong React, biến môi trường phải bắt đầu với tiền tố `REACT_APP_`.

### Bước 5: Tạo API Service

Tạo file `src/services/api.js`:

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
    console.error('Lỗi API:', error);
    throw error;
  }
};

export default api;
```

### Bước 6: Tạo Component Giao diện Chat

Tạo file `src/components/ChatInterface.js`:

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
        content: 'Không thể nhận phản hồi. Vui lòng thử lại.',
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
                <Text color="gray.500">Đang nhập...</Text>
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
            placeholder="Hỏi về thuê xe, chính sách, hoặc trạm sạc..."
            disabled={loading}
          />
          <Button
            onClick={handleSend}
            colorScheme="blue"
            isLoading={loading}
            disabled={loading}
          >
            Gửi
          </Button>
        </HStack>
      </VStack>
    </Container>
  );
}

export default ChatInterface;
```

### Bước 7: Cập nhật App.js

Cập nhật file `src/App.js`:

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

![Giao diện Chat](/images/5-Workshop/5.5-Deploy-Frontend/image-11.png)

### Bước 8: Chạy Frontend

Khởi động máy chủ phát triển React:

```bash
npm start
```

**Kết quả mong đợi:**
```
Compiled successfully!

You can now view ev-rental-frontend in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://192.168.1.10:3000
```

Ứng dụng sẽ tự động mở trong trình duyệt tại `http://localhost:3000`.

### Bước 9: Kiểm tra Giao diện Chat

Thử các câu hỏi mẫu:

1. **Truy vấn Knowledge Base:**
   - "Chính sách thuê xe là gì?"
   - "Tôi cần giấy tờ gì để thuê xe?"

2. **Tìm kiếm Xe:**
   - "Tìm xe VinFast VF8 ở Hà Nội từ ngày 20/12"
   - "Có xe nào available?"

3. **Trạm Sạc:**
   - "Trạm sạc gần Hoàn Kiếm"
   - "Tìm trạm sạc ở Quận 1"

### Danh sách Kiểm tra

Trước khi tiếp tục, đảm bảo:

- ✅ Đã cài đặt Node.js và npm
- ✅ Tất cả thư viện đã cài đặt thành công
- ✅ File `.env` đã cấu hình URL backend
- ✅ Backend server đang chạy trên cổng 8000
- ✅ Frontend đang chạy trên cổng 3000
- ✅ Giao diện chat tải không có lỗi
- ✅ Có thể gửi tin nhắn và nhận phản hồi
- ✅ Định dạng Markdown hiển thị đúng

### Xử lý Sự cố

**Lỗi: "Module not found"**
- Giải pháp: Xóa `node_modules` và chạy lại `npm install`
- Kiểm tra phiên bản trong package.json

**Lỗi: "Network Error" khi gửi tin nhắn**
- Kiểm tra backend đang chạy: `curl http://localhost:8000/health`
- Xác minh REACT_APP_API_URL trong `.env`
- Kiểm tra console trình duyệt có lỗi CORS

**Lỗi: "CORS policy error"**
- Đảm bảo backend có cấu hình CORS middleware
- Kiểm tra `allow_origins` bao gồm `http://localhost:3000`

**Lỗi: Cổng 3000 đã được sử dụng**
- Đổi cổng: `PORT=3001 npm start`
- Hoặc kill process hiện tại

**Lỗi: Markdown không render**
- Xác minh `react-markdown` đã được cài đặt
- Kiểm tra câu lệnh import trong ChatInterface.js

---

**Tiếp theo:** Chuyển sang [Testing](../5.6-Testing/) để xác minh tất cả tính năng hoạt động đúng.
