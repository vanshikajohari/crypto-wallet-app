# Crypto Wallet App

A comprehensive Flutter-based cryptocurrency wallet application that supports Ethereum blockchain operations, including wallet creation, token transfers, NFT management, and balance tracking. Built with modern web3 technologies and featuring a secure mnemonic-based wallet system.

## 📋 Table of Contents

- [Features](#-features)
- [Architecture](#-architecture)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [API Reference](#-api-reference)
- [Security](#-security)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

## ✨ Features

### Core Wallet Functionality
- **Secure Wallet Creation**: Generate new wallets using BIP39 mnemonic phrases
- **Wallet Import**: Import existing wallets using 12/24-word seed phrases
- **Private Key Management**: Secure storage and retrieval of private keys
- **Address Generation**: Ethereum address derivation from private keys

### Blockchain Operations
- **Balance Tracking**: Real-time ETH balance monitoring on Sepolia testnet
- **Token Transfers**: Send ETH to other wallet addresses
- **Transaction History**: View and track transaction activities
- **Gas Estimation**: Automatic gas price calculation for transactions

### NFT Management
- **NFT Display**: View all NFTs owned by the wallet address
- **Metadata Support**: Display NFT images, names, and descriptions
- **Cross-Chain Support**: Support for multiple blockchain networks

### User Interface
- **Modern UI**: Clean, intuitive Material Design interface
- **Responsive Design**: Optimized for various screen sizes
- **Tab Navigation**: Organized sections for Assets, NFTs, and Options
- **Real-time Updates**: Live balance and transaction updates

## 🏗️ Architecture

### Frontend (Flutter)
```
lib/
├── main.dart                 # Application entry point
├── providers/
│   └── wallet_provider.dart  # Wallet state management
├── pages/
│   ├── login_page.dart       # Authentication flow
│   ├── create_or_import.dart # Wallet creation/import choice
│   ├── generate_mnemonic_page.dart # New wallet generation
│   ├── verify_mnemonic_page.dart   # Mnemonic verification
│   ├── import_wallet.dart    # Existing wallet import
│   └── wallet.dart          # Main wallet interface
├── components/
│   ├── send_tokens.dart      # Token transfer component
│   └── nft_balances.dart     # NFT display component
└── utils/
    ├── routes.dart           # Navigation routes
    └── get_balances.dart     # Balance fetching utilities
```

### Backend (Flask)
```
backend/
└── app.py                   # Flask API server
```

### Key Technologies
- **Flutter**: Cross-platform mobile development
- **web3dart**: Ethereum blockchain interaction
- **BIP39**: Mnemonic phrase generation and validation
- **Flask**: Backend API server
- **Moralis**: Blockchain data provider
- **Provider**: State management
- **SharedPreferences**: Secure local storage

## 📋 Prerequisites

Before running this application, ensure you have the following installed:

- **Flutter SDK** (>=3.0.2)
- **Dart SDK** (>=3.0.2)
- **Python** (>=3.8)
- **pip** (Python package manager)
- **Git** (Version control)

### System Requirements
- **Android**: API level 21 or higher
- **iOS**: iOS 11.0 or higher
- **Windows**: Windows 10 or higher
- **macOS**: macOS 10.14 or higher
- **Linux**: Ubuntu 18.04 or higher

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/crypto-wallet-app.git
cd crypto-wallet-app
```

### 2. Install Flutter Dependencies
```bash
flutter pub get
```

### 3. Install Python Dependencies
```bash
cd backend
pip install -r requirements.txt
```

### 4. Environment Configuration
Create a `.env` file in the backend directory:
```bash
cd backend
touch .env
```

Add your Moralis API key to the `.env` file:
```
MORALIS_API_KEY=your_moralis_api_key_here
```

### 5. Run the Backend Server
```bash
cd backend
python app.py
```

The backend server will start on `http://localhost:5002`

### 6. Run the Flutter Application
```bash
# In the root directory
flutter run
```

## ⚙️ Configuration

### Environment Variables

#### Backend Configuration
Create a `.env` file in the `backend/` directory:

```env
MORALIS_API_KEY=your_moralis_api_key_here
FLASK_ENV=development
FLASK_DEBUG=True
```

#### Flutter Configuration
Update the API endpoints in the following files:

**lib/utils/get_balances.dart:**
```dart
final url = Uri.http('your_backend_ip:5002', '/get_token_balance', {
  'address': address,
  'chain': chain,
});
```

**lib/components/nft_balances.dart:**
```dart
final response = await http.get(
    Uri.parse('http://your_backend_ip:5002/get_user_nfts?address=${widget.address}&chain=${widget.chain}'),
    headers: {'Content-Type': 'application/json'});
```

**lib/components/send_tokens.dart:**
```dart
var apiUrl = "your_ethereum_rpc_url"; // Replace with your RPC URL
```

### Network Configuration

#### Supported Networks
- **Sepolia Testnet** (Default)
- **Ethereum Mainnet** (Configured via RPC URL)

#### RPC Endpoints
- **Sepolia**: `https://sepolia.infura.io/v3/YOUR_PROJECT_ID`
- **Mainnet**: `https://mainnet.infura.io/v3/YOUR_PROJECT_ID`

## 📱 Usage

### Getting Started

1. **Launch the Application**
   - Start the backend server: `python backend/app.py`
   - Run the Flutter app: `flutter run`

2. **Create a New Wallet**
   - Tap "Create Wallet" on the welcome screen
   - Securely store the generated 12-word mnemonic phrase
   - Verify the mnemonic phrase to complete wallet creation

3. **Import Existing Wallet**
   - Tap "Import from Seed" on the welcome screen
   - Enter your 12/24-word mnemonic phrase
   - Verify the phrase to access your wallet

### Wallet Operations

#### Viewing Balance
- The main wallet screen displays your ETH balance
- Balance is automatically updated from the Sepolia testnet
- Tap the refresh button to manually update balances

#### Sending Tokens
1. Tap the "Send" button on the main wallet screen
2. Enter the recipient's Ethereum address
3. Specify the amount of ETH to send
4. Tap "Send" to execute the transaction
5. Wait for transaction confirmation

#### Managing NFTs
1. Navigate to the "NFTs" tab
2. View all NFTs owned by your wallet address
3. Tap on an NFT to view detailed information
4. Images and metadata are automatically loaded

#### Logging Out
1. Navigate to the "Options" tab
2. Tap "Logout" to clear wallet data
3. You'll be returned to the welcome screen

### Security Best Practices

1. **Mnemonic Phrase Security**
   - Write down your mnemonic phrase on paper
   - Store it in a secure, offline location
   - Never share your mnemonic phrase with anyone
   - Never enter it on untrusted websites

2. **Private Key Protection**
   - The app stores private keys securely using SharedPreferences
   - Private keys are never transmitted over the network
   - Always verify transaction details before confirming

3. **Network Security**
   - Use only trusted RPC endpoints
   - Verify network connections before transactions
   - Keep your device and app updated

## 🔌 API Reference

### Backend API Endpoints

#### Get Token Balance
```http
GET /get_token_balance?address={address}&chain={chain}
```

**Parameters:**
- `address` (string): Ethereum wallet address
- `chain` (string): Blockchain network (e.g., "sepolia", "mainnet")

**Response:**
```json
{
  "balance": "1000000000000000000",
  "chain": "sepolia"
}
```

#### Get User NFTs
```http
GET /get_user_nfts?address={address}&chain={chain}
```

**Parameters:**
- `address` (string): Ethereum wallet address
- `chain` (string): Blockchain network

**Response:**
```json
{
  "result": [
    {
      "name": "NFT Name",
      "normalized_metadata": {
        "image": "https://example.com/image.png",
        "description": "NFT Description"
      }
    }
  ]
}
```

### Frontend API Classes

#### WalletProvider
```dart
class WalletProvider extends ChangeNotifier {
  String? privateKey;
  
  // Generate new mnemonic phrase
  String generateMnemonic();
  
  // Derive private key from mnemonic
  Future<String> getPrivateKey(String mnemonic);
  
  // Get public address from private key
  Future<EthereumAddress> getPublicKey(String privateKey);
  
  // Load private key from storage
  Future<void> loadPrivateKey();
  
  // Save private key to storage
  Future<void> setPrivateKey(String privateKey);
}
```

#### SendTokensPage
```dart
class SendTokensPage extends StatelessWidget {
  final String privateKey;
  
  // Send ETH transaction
  void sendTransaction(String receiver, EtherAmount txValue);
}
```

#### NFTListPage
```dart
class NFTListPage extends StatefulWidget {
  final String address;
  final String chain;
  
  // Load NFTs for wallet address
  Future<void> _loadNFTList();
}
```

## 🔒 Security

### Cryptographic Implementation
- **BIP39**: Standard mnemonic phrase generation
- **ED25519**: HD key derivation for wallet creation
- **SHA256**: Secure hashing for seed generation
- **AES-256**: Local storage encryption (via SharedPreferences)

### Data Protection
- Private keys are stored locally using SharedPreferences
- No sensitive data is transmitted over the network
- Mnemonic phrases are validated before wallet creation
- Transaction signing happens locally on the device

### Network Security
- HTTPS communication with backend services
- Input validation for all user inputs
- Rate limiting on API endpoints
- Secure RPC endpoint configuration

## 🛠️ Troubleshooting

### Common Issues

#### 1. Flutter Dependencies
```bash
# Clear Flutter cache
flutter clean
flutter pub get
```

#### 2. Backend Connection Issues
```bash
# Check if backend is running
curl http://localhost:5002/get_token_balance?address=0x123&chain=sepolia
```

#### 3. Network Configuration
- Verify RPC endpoint URLs are correct
- Check Moralis API key configuration
- Ensure network connectivity

#### 4. Wallet Import Issues
- Verify mnemonic phrase is 12 or 24 words
- Check for extra spaces or typos
- Ensure phrase is in correct order

#### 5. Transaction Failures
- Verify sufficient ETH balance for gas fees
- Check recipient address format
- Ensure network connection is stable

### Debug Mode
Enable debug logging by setting:
```dart
// In main.dart
debugPrint('Debug information');
```

### Performance Optimization
- Use `const` constructors where possible
- Implement proper state management
- Optimize image loading for NFTs
- Cache frequently accessed data

## 🤝 Contributing

We welcome contributions to improve the crypto wallet app! Please follow these guidelines:

### Development Setup
1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes
4. Add tests for new functionality
5. Commit your changes: `git commit -m 'Add feature'`
6. Push to the branch: `git push origin feature-name`
7. Submit a pull request

### Code Style
- Follow Dart/Flutter style guidelines
- Use meaningful variable and function names
- Add comments for complex logic
- Write unit tests for critical functions

### Testing
```bash
# Run Flutter tests
flutter test

# Run backend tests
cd backend
python -m pytest
```

### Documentation
- Update README.md for new features
- Add API documentation for new endpoints
- Include usage examples
- Document configuration changes

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Moralis**: Blockchain data provider
- **Flutter Team**: Cross-platform development framework
- **web3dart**: Ethereum blockchain integration
- **BIP39**: Mnemonic phrase standard

## 📞 Support

For support and questions:
- Create an issue on GitHub
- Check the troubleshooting section
- Review the documentation
- Contact the development team

---

**⚠️ Disclaimer**: This is a demonstration application. For production use, ensure proper security audits, testing, and compliance with local regulations. Never use this wallet for storing significant amounts of cryptocurrency without thorough security review.
