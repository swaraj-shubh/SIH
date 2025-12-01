# MÄRGARAKŞAK - Blockchain-Based Digital Travel Passport System

## 🚀 Overview

MÄRGARAKŞAK is a cutting-edge digital travel passport system that combines blockchain technology, AI-powered security, and smart geofencing to create a secure, tamper-proof travel credential platform. The system enables governments and tourism authorities to issue verifiable digital travel passes for tourists while ensuring security, transparency, and emergency response capabilities.

## ✨ Key Features

### 🔐 Security & Authentication
- **Blockchain-based identity verification** using NFTs on Ethereum
- **JWT token authentication** for secure API access
- **Military-grade encryption** for all sensitive data
- **QR code verification** with cryptographic signatures
- **Smart contract-based** minting and validation

### 📱 Digital Passport System
- **NFT-based digital travel passports** with unique token IDs
- **IPFS storage** for metadata and images
- **QR code generation** for physical/digital verification
- **Time-limited validity** with automated expiration
- **Digital signature verification** using backend private key

### 🗺️ Smart Mapping & Geofencing
- **Interactive heatmaps** showing tourist density
- **Geofenced restricted zones** with polygon overlays
- **Real-time location tracking** (planned feature)
- **Emergency SOS functionality** with precise coordinates
- **Region-specific access control**

### 🏗️ Technical Architecture

```
margaraksak/
├── backend/                    # Node.js/Express backend
│   ├── controllers/           # Business logic (auth, passport, IPFS)
│   ├── services/             # External services (blockchain, crypto, Firebase)
│   ├── models/               # Data models
│   ├── routes/               # API routes
│   └── index.js              # Server entry point
├── frontend/                  # React frontend
│   ├── src/pages/            # Main application pages
│   ├── src/components/       # UI components
│   ├── src/contexts/         # React context providers
│   └── src/lib/              # Utilities and Firebase config
└── README.md
```

## 🛠️ Tech Stack

### Backend
- **Node.js** with Express.js
- **Ethers.js** for blockchain interactions
- **Pinata SDK** for IPFS storage
- **Firebase Admin SDK** for database/storage
- **JWT** for authentication
- **QR Code generation** with node-qrcode

### Frontend
- **React 18** with Vite
- **Tailwind CSS** for styling
- **Leaflet.js** for interactive maps
- **Radix UI** components
- **Firebase Client SDK** for authentication

### Blockchain
- **Ethereum** (Sepolia testnet)
- **ERC-721 NFT standard** for digital passports
- **Smart contracts** for minting and verification
- **MetaMask** wallet integration

### Storage
- **IPFS** via Pinata for decentralized metadata
- **Firebase Firestore** for user data
- **Firebase Storage** for QR codes

## 📦 Installation & Setup

### Prerequisites
- Node.js (v18+)
- MetaMask browser extension
- Firebase project
- Pinata API credentials
- Ethereum wallet with testnet ETH

### 1. Backend Setup
```bash
cd backend
npm install
```

Create `.env` file:
```env
PORT=5000
PRIVATE_KEY=your_wallet_private_key
CONTRACT_ADDRESS=your_nft_contract_address
RPC_URL=https://sepolia.infura.io/v3/YOUR_PROJECT_ID
PINATA_API_KEY=your_pinata_api_key
PINATA_SECRET_API_KEY=your_pinata_secret
FIREBASE_PROJECT_ID=your_firebase_project
ENCRYPTION_KEY=32_char_encryption_key
```

### 2. Frontend Setup
```bash
cd frontend
npm install
```

### 3. Start Servers
```bash
# Backend
cd backend
npm start

# Frontend
cd frontend
npm run dev
```

## 🚀 Usage

### 1. User Registration
```
POST /api/auth/register
{
  "userId": "tourist123"
}

Response:
{
  "success": true,
  "userId": "tourist123",
  "walletAddress": "0x...",
  "isValidated": true
}
```

### 2. IPFS Metadata Upload
```
POST /api/ipfs/upload-metadata
{
  "userId": "tourist123",
  "fullName": "John Doe",
  "docNumber": "P1234567",
  "nationality": "Indian",
  "imageData": "base64_encoded_image"
}

Response:
{
  "success": true,
  "tokenURI": "ipfs://Qm...",
  "metadata": {...}
}
```

### 3. NFT Passport Minting
```
POST /api/passport/mint-qr-existing
{
  "userId": "tourist123",
  "userWallet": "0x...",
  "tokenURI": "ipfs://Qm..."
}

Response:
{
  "success": true,
  "txHash": "0x...",
  "tokenId": "7",
  "qrUrl": "data:image/png;base64,...",
  "payload": {...}
}
```

### 4. QR Code Verification
```
POST /api/qr/verify
{
  "tokenId": "7",
  "userId": "tourist123",
  "expiry": 1737158400000,
  "signature": "0x..."
}

Response:
{
  "valid": true,
  "tokenId": "7",
  "userId": "tourist123"
}
```

## 🔧 Smart Contract Integration

### Contract Address
`0x...` (Replace with deployed contract address)

### Key Functions
```solidity
function mintPassport(address to, string tokenURI) external returns (uint256)
event Transfer(address indexed from, address indexed to, uint256 indexed tokenId)
```

### Contract Interaction
```javascript
const contract = getNFTContract();
const tx = await contract.mintPassport(userWallet, tokenURI);
const receipt = await tx.wait();
```

## 📱 Frontend Features

### Dashboard
- User profile display
- Interactive map with tourist heatmap
- Restricted zone visualization

### Admin Panel
- User management interface
- Validation status tracking
- Travel history monitoring

### Minting Interface
- Passport metadata form
- IPFS upload functionality
- NFT minting with QR generation

### Map Visualization
- Leaflet-based interactive map
- Heatmap showing tourist density
- Geofenced restricted zones

## 🔒 Security Features

### Data Protection
- **AES-256-GCM encryption** for private keys
- **JWT tokens** with expiration
- **HTTPS enforcement**
- **Input validation** and sanitization

### Blockchain Security
- **Digital signatures** for QR verification
- **Smart contract access control**
- **Immutable transaction records**
- **Gas optimization** for cost efficiency

### Access Control
- **Role-based authentication**
- **API rate limiting**
- **CORS configuration**
- **Firebase security rules**

## 🎯 Use Cases

### For Governments/Tourism Boards
- Issue verifiable digital travel permits
- Monitor tourist distribution in real-time
- Enforce restricted area access
- Emergency response coordination

### For Tourists
- Single digital credential for all travel
- Quick verification at checkpoints
- Emergency SOS functionality
- Travel history record

### For Businesses
- Verify tourist credentials
- Access to authorized areas only
- Integration with existing systems
- Compliance with regulations

## 📊 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - User login

### IPFS Operations
- `POST /api/ipfs/upload-metadata` - Upload passport metadata
- `GET /api/ipfs/test-connection` - Test IPFS connection

### Passport Operations
- `POST /api/passport/mint` - Mint passport NFT
- `POST /api/passport/mint-qr-existing` - Mint with existing URI
- `POST /api/passport/mint-qr` - Full minting flow

### Verification
- `POST /api/qr/verify` - Verify QR code signature

## 🚀 Deployment

### Backend (Railway/Render)
```bash
# Set environment variables
# Deploy using platform CLI
```

### Frontend (Vercel/Netlify)
```bash
npm run build
# Deploy dist/ folder
```

### Smart Contract (Sepolia Testnet)
```solidity
// Deploy using Hardhat/Remix
npx hardhat run scripts/deploy.js --network sepolia
```

## 📁 Key Files

### Backend
- `backend/controllers/passportController.js` - Core minting logic
- `backend/services/blockchain.js` - Ethereum interactions
- `backend/services/pinataService.js` - IPFS operations

### Frontend
- `frontend/src/pages/MintNFT.jsx` - NFT minting interface
- `frontend/src/pages/Map.jsx` - Interactive heatmap
- `frontend/src/components/data.js` - Geofencing coordinates

### Services
- `backend/services/cryptoService.js` - Encryption utilities
- `backend/services/metadataService.js` - NFT metadata generation

## 🧪 Testing

### Smart Contract Tests
```bash
npx hardhat test
```

### API Testing
```bash
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"userId":"testUser"}'
```

### Frontend Testing
```bash
cd frontend
npm test
```

## 🔮 Future Enhancements

### Planned Features
- **Mobile app** with offline QR support
- **Biometric authentication** integration
- **Cross-chain compatibility** (Polygon, Arbitrum)
- **AI-powered anomaly detection**
- **Multi-language support**
- **Group travel management**

### Scalability Improvements
- **Layer 2 solutions** for gas optimization
- **CDN distribution** for IPFS content
- **Database sharding** for user growth
- **Microservices architecture**

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow existing code style and conventions
- Write comprehensive tests for new features
- Update documentation accordingly
- Use meaningful commit messages

## 📞 Support

For support, contact the development team or create an issue in the repository.

---

**Built with ❤️ for secure and transparent travel management**
