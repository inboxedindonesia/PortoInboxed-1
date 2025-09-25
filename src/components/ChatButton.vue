<template>
  <div class="chat-button-container">
    <!-- Chat Button -->
    <button 
      class="chat-button"
      @click="toggleChat"
      :class="{ 'active': isChatOpen }"
      aria-label="Open Chat"
    >
      <svg v-if="!isChatOpen" class="chat-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M8 12H8.01M12 12H12.01M16 12H16.01M21 12C21 16.418 16.97 20 12 20C10.89 20 9.84 19.81 8.87 19.46L3 21L4.54 15.13C4.19 14.16 4 13.11 4 12C4 7.582 8.03 4 12 4C16.97 4 21 7.582 21 12Z" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
      <svg v-else class="close-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M18 6L6 18M6 6L18 18" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </button>

    <!-- Chat Window -->
    <div 
      class="chat-window"
      :class="{ 'open': isChatOpen }"
      v-show="isChatOpen"
    >
      <div class="chat-header">
        <div class="chat-header-info">
          <div class="avatar">
            <div class="avatar-circle">
              <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M20 21V19C20 17.9391 19.5786 16.9217 18.8284 16.1716C18.0783 15.4214 17.0609 15 16 15H8C6.93913 15 5.92172 15.4214 5.17157 16.1716C4.42143 16.9217 4 17.9391 4 19V21M16 7C16 9.20914 14.2091 11 12 11C9.79086 11 8 9.20914 8 7C8 4.79086 9.79086 3 12 3C14.2091 3 16 4.79086 16 7Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </div>
            <div class="online-indicator"></div>
          </div>
          <div class="chat-info">
            <h4>Customer Support</h4>
            <p class="status">Online</p>
          </div>
        </div>
        <button class="close-chat" @click="toggleChat">
          <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M18 6L6 18M6 6L18 18" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
      </div>

      <div class="chat-body">
        <div class="welcome-message">
          <div class="message bot-message">
            <div class="message-content">
              <p>👋 Halo! Selamat datang di LuxeFurniture!</p>
              <p>Ada yang bisa kami bantu hari ini?</p>
            </div>
            <span class="message-time">{{ getCurrentTime() }}</span>
          </div>
        </div>

        <div class="quick-actions">
          <button 
            class="quick-action-btn"
            @click="sendQuickMessage('Saya ingin bertanya tentang produk')"
          >
            🛋️ Tanya Produk
          </button>
          <button 
            class="quick-action-btn"
            @click="sendQuickMessage('Bagaimana cara pemesanan?')"
          >
            📦 Cara Pesan
          </button>
          <button 
            class="quick-action-btn"
            @click="sendQuickMessage('Saya ingin konsultasi desain')"
          >
            🎨 Konsultasi
          </button>
        </div>
      </div>

      <div class="chat-footer">
        <div class="input-container">
          <input 
            type="text" 
            v-model="messageInput"
            @keypress.enter="sendMessage"
            placeholder="Ketik pesan Anda..."
            class="message-input"
          >
          <button 
            class="send-button"
            @click="sendMessage"
            :disabled="!messageInput.trim()"
          >
            <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M22 2L11 13M22 2L15 22L11 13M22 2L2 9L11 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'ChatButton',
  setup() {
    const isChatOpen = ref(false)
    const messageInput = ref('')

    const toggleChat = () => {
      isChatOpen.value = !isChatOpen.value
    }

    const getCurrentTime = () => {
      return new Date().toLocaleTimeString('id-ID', { 
        hour: '2-digit', 
        minute: '2-digit' 
      })
    }

    const sendMessage = () => {
      if (messageInput.value.trim()) {
        // Here you would typically send the message to your chat service
        console.log('Sending message:', messageInput.value)
        
        // For demo purposes, redirect to WhatsApp with the message
        const whatsappNumber = '628123456789' // Ganti dengan nomor WhatsApp Anda
        const encodedMessage = encodeURIComponent(messageInput.value)
        const whatsappUrl = `https://wa.me/${whatsappNumber}?text=${encodedMessage}`
        
        // Clear the input and close chat
        messageInput.value = ''
        isChatOpen.value = false
        
        // Open WhatsApp
        window.open(whatsappUrl, '_blank')
        
        // You could add logic here to:
        // - Send to WhatsApp Business API
        // - Send to your chat service
        // - Show user message in chat
      }
    }

    const sendQuickMessage = (message) => {
      // Handle quick action messages
      console.log('Quick message:', message)
      
      // You could redirect to WhatsApp or your preferred chat platform
      const whatsappNumber = '628123456789' // Ganti dengan nomor WhatsApp Anda
      const encodedMessage = encodeURIComponent(message)
      const whatsappUrl = `https://wa.me/${whatsappNumber}?text=${encodedMessage}`
      
      // Close chat window after sending quick message
      isChatOpen.value = false
      
      window.open(whatsappUrl, '_blank')
    }

    return {
      isChatOpen,
      messageInput,
      toggleChat,
      getCurrentTime,
      sendMessage,
      sendQuickMessage
    }
  }
}
</script>

<style scoped>
.chat-button-container {
  position: fixed;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1000;
}

.chat-button {
  width: 60px;
  height: 60px;
  border-radius: 30px 0 0 30px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border: none;
  color: white;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 20px rgba(102, 126, 234, 0.4);
  transition: all 0.3s ease;
  position: relative;
}

.chat-button:hover {
  transform: scale(1.1);
  box-shadow: 0 6px 25px rgba(102, 126, 234, 0.6);
}

.chat-button.active {
  background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
}

.chat-icon,
.close-icon {
  width: 32px;
  height: 32px;
  transition: all 0.3s ease;
  stroke-width: 1.5;
}

.chat-window {
  position: absolute;
  right: 70px;
  top: 50%;
  transform: translateY(-50%);
  width: 350px;
  height: 500px;
  background: white;
  border-radius: 16px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
  opacity: 0;
  visibility: hidden;
  transform: translateY(-50%) scale(0.8);
  transition: all 0.3s ease;
  overflow: hidden;
}

.chat-window.open {
  opacity: 1;
  visibility: visible;
  transform: translateY(-50%) scale(1);
}

.chat-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.chat-header-info {
  display: flex;
  align-items: center;
  gap: 12px;
}

.avatar {
  position: relative;
}

.avatar-circle {
  width: 40px;
  height: 40px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.avatar-circle svg {
  width: 20px;
  height: 20px;
}

.online-indicator {
  position: absolute;
  bottom: 2px;
  right: 2px;
  width: 12px;
  height: 12px;
  background: #4ade80;
  border: 2px solid white;
  border-radius: 50%;
}

.chat-info h4 {
  margin: 0;
  font-size: 14px;
  font-weight: 600;
}

.status {
  margin: 0;
  font-size: 12px;
  opacity: 0.8;
}

.close-chat {
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  padding: 4px;
  border-radius: 4px;
  transition: background-color 0.2s ease;
}

.close-chat:hover {
  background: rgba(255, 255, 255, 0.1);
}

.close-chat svg {
  width: 16px;
  height: 16px;
}

.chat-body {
  padding: 16px;
  height: calc(100% - 140px);
  overflow-y: auto;
}

.welcome-message {
  margin-bottom: 16px;
}

.message {
  margin-bottom: 12px;
}

.bot-message .message-content {
  background: #f1f5f9;
  padding: 12px;
  border-radius: 12px 12px 12px 4px;
  margin-bottom: 4px;
}

.bot-message .message-content p {
  margin: 0;
  font-size: 14px;
  line-height: 1.4;
}

.bot-message .message-content p:not(:last-child) {
  margin-bottom: 8px;
}

.message-time {
  font-size: 11px;
  color: #64748b;
  margin-left: 8px;
}

.quick-actions {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.quick-action-btn {
  background: white;
  border: 1px solid #e2e8f0;
  padding: 12px;
  border-radius: 8px;
  text-align: left;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.2s ease;
}

.quick-action-btn:hover {
  background: #f8fafc;
  border-color: #667eea;
  transform: translateY(-1px);
}

.chat-footer {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: white;
  border-top: 1px solid #e2e8f0;
  padding: 16px;
}

.input-container {
  display: flex;
  gap: 8px;
  align-items: center;
}

.message-input {
  flex: 1;
  padding: 12px;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  font-size: 14px;
  outline: none;
  transition: border-color 0.2s ease;
}

.message-input:focus {
  border-color: #667eea;
}

.send-button {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border: none;
  border-radius: 8px;
  color: white;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
}

.send-button:hover:not(:disabled) {
  transform: scale(1.05);
}

.send-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.send-button svg {
  width: 16px;
  height: 16px;
}

/* Mobile Responsive */
@media (max-width: 768px) {
  .chat-button-container {
    right: 0;
  }
  
  .chat-window {
    right: -280px;
    width: 320px;
    height: 450px;
  }
  
  .chat-window.open {
    right: -260px;
  }
}

@media (max-width: 480px) {
  .chat-window {
    right: -300px;
    width: 300px;
    height: 400px;
  }
  
  .chat-window.open {
    right: -280px;
  }
}
</style>