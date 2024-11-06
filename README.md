<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Nysa Chatbot</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #FFD700;
            --secondary-color: #FDB931;
            --background-dark: #1a1a1f;
            --text-light: #ffffff;
            --text-dark: #000000;
            --accent-gradient: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background-color: var(--background-dark);
            color: var(--text-light);
            line-height: 1.6;
            min-height: 100vh;
        }

        /* Header Styles */
        .header {
            padding: 12px 20px;
            background: rgba(26, 26, 31, 0.95);
            position: fixed;
            width: 100%;
            top: 0;
            left: 0;
            z-index: 1000;
            border-bottom: 2px solid var(--primary-color);
            backdrop-filter: blur(10px);
        }

        .header-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8em;
            font-weight: 900;
            background: var(--accent-gradient);
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: 1.2px;
        }

        .connect-wallet {
            padding: 12px 24px;
            background: var(--accent-gradient);
            border: none;
            border-radius: 50px;
            color: var(--text-dark);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.95em;
            letter-spacing: 0.5px;
        }

        /* Main Content Styles */
        .main-content {
            padding-top: 80px;
            padding-bottom: 80px;
            min-height: calc(100vh - 140px);
        }

        /* Search Section */
        .search-section {
            max-width: 800px;
            margin: 40px auto;
            padding: 20px;
            text-align: center;
        }

        .search-container {
            position: relative;
            margin-top: 40px;
        }

        .search-input {
            width: 100%;
            padding: 16px 24px;
            padding-right: 50px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 215, 0, 0.3);
            border-radius: 30px;
            color: var(--text-light);
            font-size: 1.1em;
            transition: all 0.3s ease;
        }

        .search-input:focus {
            outline: none;
            border-color: var(--primary-color);
            background: rgba(255, 255, 255, 0.15);
        }

        .search-button {
            position: absolute;
            right: 16px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            color: var(--primary-color);
            cursor: pointer;
            font-size: 1.2em;
        }

        /* Featured Categories */
        .categories {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .category-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            padding: 20px;
            text-align: center;
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 215, 0, 0.1);
        }

        .category-card:hover {
            transform: translateY(-5px);
            background: rgba(255, 215, 0, 0.1);
        }

        .category-icon {
            font-size: 2em;
            color: var(--primary-color);
            margin-bottom: 15px;
        }

        /* Bottom Navigation */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: rgba(26, 26, 31, 0.95);
            padding: 10px 0;
            backdrop-filter: blur(10px);
            border-top: 1px solid rgba(255, 215, 0, 0.2);
            z-index: 1000;
        }

        .nav-container {
            display: flex;
            justify-content: space-around;
            align-items: center;
            max-width: 600px;
            margin: 0 auto;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: var(--text-light);
            transition: all 0.3s ease;
            padding: 5px;
            cursor: pointer;
        }

        .nav-item i {
            font-size: 20px;
            margin-bottom: 4px;
        }

        .nav-item span {
            font-size: 12px;
        }

        .nav-item.active {
            color: var(--primary-color);
        }

        /* Chatbot Styles */
        .chatbot-container {
            position: fixed;
             margin: 0px;
            right: 20px;
            width: 380px;
            height: 600px;
            background: rgba(26, 26, 31, 0.95);
            border-radius: 20px;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.2);
            display: flex;
            flex-direction: column;
            z-index: 999;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 215, 0, 0.1);
        }

        .chat-header {
            width: 550px;
            padding: 20px 20px;
            margin: 10px;
            background: linear-gradient(135deg, rgba(255, 215, 0, 0.1), rgba(253, 185, 49, 0.1));
            border-bottom: 1px solid rgba(255, 215, 0, 0.2);
            border-radius: 20px 20px 0 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .chat-status {
            display: flex;
            align-items: center;
            color: var(--primary-color);
            font-weight: 600;
            font-size: 0.95em;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background: var(--primary-color);
            border-radius: 50%;
            margin-right: 8px;
            animation: pulse 2s infinite;
        }

        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .message {
            display: flex;
            gap: 12px;
            max-width: 85%;
        }

        .bot-message {
            align-self: flex-start;
        }

        .user-message {
            align-self: flex-end;
            flex-direction: row-reverse;
        }

        .message-avatar {
            width: 36px;
            height: 36px;
            background: rgba(255, 215, 0, 0.1);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--primary-color);
        }

        .message-content {
            background: rgba(255, 255, 255, 0.05);
            padding: 12px 16px;
            border-radius: 16px;
            color: var(--text-light);
            font-size: 0.95em;
        }

        .user-message .message-content {
            background: rgba(255, 215, 0, 0.1);
        }

        .chat-input-container {
            padding: 16px;
            border-top: 1px solid rgba(255, 215, 0, 0.1);
            display: flex;
            gap: 12px;
            align-items: center;
        }

        #chatInput {
            flex: 1;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 215, 0, 0.2);
            border-radius: 12px;
            padding: 12px 16px;
            color: var(--text-light);
            font-size: 0.95em;
        }

        .input-actions {
            display: flex;
            gap: 8px;
        }

        .input-actions button {
            background: none;
            border: none;
            color: rgba(255, 215, 0, 0.7);
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: all 0.3s ease;
        }

        /* Animations */
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        /* Responsive Styles */
        @media (max-width: 768px) {
            .chatbot-container {
                width: 100%;
                height: 500px;
                right: 0;
                bottom: 60px;
                border-radius: 20px 20px 0 0;
            }

            .categories {
                grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header class="header">
        <div class="header-content">
            <div class="logo">Nysa</div>
            <button class="connect-wallet">
                <i class="fas fa-wallet"></i>
                Connect
            </button>
        </div>
    </header>

    <!-- Main Content -->
    <main class="main-content">
        <!-- Search Section -->
        <section class="search-section">
            <h1 style="background: var(--accent-gradient); -webkit-background-clip: text; color: transparent; font-size: 2.5em; margin-bottom: 20px;">
                Discover the Web3 Universe
            </h1>
            <div class="search-container">
                <input type="text" class="search-input" placeholder="Search NFTs, DApps, or blockchain projects...">
                <button class="search-button">
                    <i class="fas fa-search"></i>
                </button>
            </div>
        </section>

        <!-- Featured Categories -->
        <section class="categories">
            <div class="category-card">
                <i class="fas fa-paint-brush category-icon"></i>
                <h3>NFT Collections</h3>
                <p>Explore unique digital art and collectibles</p>
            </div>
            <div class="category-card">
                <i class="fas fa-cube category-icon"></i>
                <h3>DeFi Protocols</h3>
                <p>Discover decentralized finance platforms</p>
            </div>
            <div class="category-card">
                <i class="fas fa-gamepad category-icon"></i>
                <h3>GameFi</h3>
                <p>Play-to-earn blockchain games</p>
            </div>
            <div class="category-card">
                <i class="fas fa-code category-icon"></i>
                <h3>Smart Contracts</h3>
                <p>Verified contract addresses and audits</p>
            </div>
        </section>
    </main>

    <!-- Chatbot -->
    <div class="chatbot-container">
        <div class="chat-header">
            <div class="chat-status">
                <span class="status-dot"></span>
                Nysa AI Assistant
            </div>
            <div class="chat-actions">
                </button>
            </div>
        </div>
        <div class="chat-messages" id="chatMessages">
            <div class="message bot-message">
                <div class="message-avatar">
                    <i class="fas fa-robot"></i>
                </div>
                <div class="message-content">
                    <p>Hello! I'm your Web3 assistant. How can I help you explore the blockchain universe today?</p>
                </div>
            </div>
        </div>
        <div class="chat-input-container">
            <input type="text" id="chatInput" placeholder="Ask about Web3, NFTs, or blockchain..." />
            <div class="input-actions">
                <button class="voice-input">
                    <i class="fas fa-microphone"></i>
                </button>
                <button class="send-message">
                    <i class="fas fa-paper-plane"></i>
                </button>
            </div>
        </div>
    </div>

    <!-- Bottom Navigation -->
    <nav class="bottom-nav">
        <div class="nav-container">
            <div class="nav-item active">
                <i class="fas fa-home"></i>
                <span>Home</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-chart-line"></i>
                <span>Trending</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-compass"></i>
                <span>Explore</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-bookmark"></i>
                <span>Saved</span>
            </div>
            <div class="nav-item">
                <i class="fas fa-user"></i>
                <span>Profile</span>
            </div>
        </div>
    </nav>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // DOM Elements
            const chatInput = document.getElementById('chatInput');
            const chatMessages = document.getElementById('chatMessages');
            const sendButton = document.querySelector('.send-message');
            const minimizeButton = document.querySelector('.minimize-chat');
            const clearButton = document.querySelector('.clear-chat');
            const chatContainer = document.querySelector('.chatbot-container');
            const voiceButton = document.querySelector('.voice-input');
            const searchInput = document.querySelector('.search-input');
            const searchButton = document.querySelector('.search-button');
            const navItems = document.querySelectorAll('.nav-item');
            const connectWalletBtn = document.querySelector('.connect-wallet');

            // Chatbot functionality
            const generateResponse = (message) => {
                const responses = {
                    nft: [
                        "NFTs (Non-Fungible Tokens) are unique digital assets stored on the blockchain. They can represent art, music, videos, and more.",
                        "Popular NFT marketplaces include OpenSea, Rarible, and Foundation.",
                        "Always verify the authenticity of NFT collections before making a purchase."
                    ],
                    blockchain: [
                        "Blockchain is a distributed ledger technology that ensures transparency and security.",
                        "Popular blockchain networks include Ethereum, Solana, and Binance Smart Chain.",
                        "Smart contracts are self-executing contracts with terms directly written into code."
                    ],
                    defi: [
                        "DeFi (Decentralized Finance) offers financial services without traditional intermediaries.",
                        "Common DeFi activities include lending, borrowing, and yield farming.",
                        "Always research protocols thoroughly and be aware of the risks involved."
                    ],
                    wallet: [
                        "Crypto wallets are essential for storing and managing your digital assets.",
                        "Popular wallets include MetaMask, Trust Wallet, and Phantom.",
                        "Never share your private keys or seed phrase with anyone."
                    ],
                    default: [
                        "I'm here to help you explore the Web3 space. Feel free to ask about NFTs, blockchain, DeFi, or crypto wallets.",
                        "That's an interesting question. Let me help you understand this aspect of Web3.",
                        "I'd be happy to explain more about this topic in the context of blockchain technology."
                    ]
                };

                const topic = Object.keys(responses).find(key => 
                    message.toLowerCase().includes(key)
                ) || 'default';

                return responses[topic][Math.floor(Math.random() * responses[topic].length)];
            };

            const addMessage = (text, sender) => {
                const messageDiv = document.createElement('div');
                messageDiv.className = `message ${sender}-message`;
                
                const avatar = document.createElement('div');
                avatar.className = 'message-avatar';
                avatar.innerHTML = `<i class="fas fa-${sender === 'bot' ? 'robot' : 'user'}"></i>`;

                const content = document.createElement('div');
                content.className = 'message-content';
                content.innerHTML = `
                    <p>${text}</p>
                    <span class="message-time">${new Date().toLocaleTimeString()}</span>
                `;

                if (sender === 'user') {
                    messageDiv.appendChild(content);
                    messageDiv.appendChild(avatar);
                } else {
                    messageDiv.appendChild(avatar);
                    messageDiv.appendChild(content);
                }

                chatMessages.appendChild(messageDiv);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            };

            const sendMessage = () => {
                const message = chatInput.value.trim();
                if (!message) return;

                addMessage(message, 'user');
                chatInput.value = '';

                // Simulate typing indicator
                const typingDiv = document.createElement('div');
                typingDiv.className = 'message bot-message typing';
                typingDiv.innerHTML = '<div class="message-avatar"><i class="fas fa-robot"></i></div><div class="message-content"><p>typing...</p></div>';
                chatMessages.appendChild(typingDiv);
                chatMessages.scrollTop = chatMessages.scrollHeight;

                // Simulate bot response with delay
                setTimeout(() => {
                    chatMessages.removeChild(typingDiv);
                    const response = generateResponse(message);
                    addMessage(response, 'bot');
                }, 1500);
            };

            // Voice input functionality
            const startVoiceInput = () => {
                if ('webkitSpeechRecognition' in window) {
                    const recognition = new webkitSpeechRecognition();
                    recognition.continuous = false;
                    recognition.interimResults = false;

                    recognition.onstart = () => {
                        voiceButton.style.color = 'var(--primary-color)';
                    };

                    recognition.onresult = (event) => {
                        const text = event.results[0][0].transcript;
                        chatInput.value = text;
                    };

                    recognition.onend = () => {
                        voiceButton.style.color = 'rgba(255, 215, 0, 0.7)';
                    };

                    recognition.start();
                }
            };

            // Search functionality
            const performSearch = () => {
                const query = searchInput.value.trim();
                if (!query) return;

                // Add search animation
                searchButton.innerHTML = '<i class="fas fa-spinner fa-spin"></i>';
                
                // Simulate search delay
                setTimeout(() => {
                    searchButton.innerHTML = '<i class="fas fa-search"></i>';
                    // Here you would typically handle the actual search
                    addMessage(`Searching for: ${query}`, 'user');
                    addMessage('Here are some relevant results from the Web3 universe...', 'bot');
                }, 1000);
            };

            // Wallet connection
            const connectWallet = async () => {
                if (typeof window.ethereum !== 'undefined') {
                    try {
                        const accounts = await window.ethereum.request({ 
                            method: 'eth_requestAccounts' 
                        });
                        connectWalletBtn.innerHTML = `
                            <i class="fas fa-check-circle"></i>
                            ${accounts[0].slice(0, 6)}...${accounts[0].slice(-4)}
                        `;
                        addMessage('Wallet connected successfully!', 'bot');
                    } catch (error) {
                        addMessage('Failed to connect wallet. Please try again.', 'bot');
                    }
                } else {
                    addMessage('Please install MetaMask or another Web3 wallet.', 'bot');
                }
            };

            // Event listeners
            sendButton.addEventListener('click', sendMessage);
            chatInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') sendMessage();
            });

            minimizeButton.addEventListener('click', () => {
                chatContainer.style.display = 
                    chatContainer.style.display === 'none' ? 'flex' : 'none';
            });

            clearButton.addEventListener('click', () => {
                const firstMessage = chatMessages.firstElementChild;
                chatMessages.innerHTML = '';
                chatMessages.appendChild(firstMessage);
            });

            voiceButton.addEventListener('click', startVoiceInput);

            searchButton.addEventListener('click', performSearch);
            searchInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') performSearch();
            });

            connectWalletBtn.addEventListener('click', connectWallet);

            navItems.forEach(item => {
                item.addEventListener('click', () => {
                    navItems.forEach(i => i.classList.remove('active'));
                    item.classList.add('active');
                });
            });

            // Handle metamask events
            if (typeof window.ethereum !== 'undefined') {
                window.ethereum.on('accountsChanged', (accounts) => {
                    if (accounts.length === 0) {
                        connectWalletBtn.innerHTML = `
                            <i class="fas fa-wallet"></i>
                            Connect Wallet
                        `;
                    }
                });
            }
        });
    </script>
</body>
</html>
