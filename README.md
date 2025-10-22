# StormEye - Comprehensive System Documentation

## Table of Contents
1. [System Overview](#system-overview)
2. [Extension Features](#extension-features)
3. [Pricing Plans](#pricing-plans)
4. [Payment Methods](#payment-methods)
5. [Referral System](#referral-system)
6. [Wallet Management](#wallet-management)
7. [Withdrawal Process](#withdrawal-process)
8. [Extension-Sale Site Integration](#extension-sale-site-integration)
9. [Technical Architecture](#technical-architecture)
10. [User Workflows](#user-workflows)

---

## System Overview

**StormEye** is an automated bidding system for Freelancer.com consisting of:
- **Chrome Extension**: Automates bidding on Freelancer.com projects
- **Sale Website**: Manages subscriptions, payments, referrals, and wallet
- **Backend API**: Handles authentication, payments, and cryptocurrency transactions

### Core Components
```
├── Extension (Chrome)
│   ├── Background Service Worker
│   ├── Content Script (Freelancer.com integration)
│   ├── Popup Interface
│   └── Settings Page
│
├── Sale Site (React Frontend)
│   ├── Landing Page
│   ├── Pricing Plans
│   ├── Authentication (Google OAuth, Email/Password)
│   ├── Wallet Dashboard
│   └── Referral System
│
└── Backend API (Python Flask)
    ├── User Management
    ├── Payment Processing
    ├── Crypto Wallet Service
    ├── Blockchain Integration
    └── Referral System
```

---

## Extension Features

### 1. **AI Proposal Generation**

The extension offers three methods for generating bid proposals:

#### a) Template-Based Proposals
- Use custom templates with shortcodes
- **Available Shortcodes:**
  - `<EmployerName>` - Client's name
  - `<ProjectTitle>` - Project title
  - `<ProjectSkills>` - Required skills (comma-separated)
  - `<FreelancerName>` - Your name
  
- **Advanced Features:**
  - `<Separator>` - Split template into variants (random selection)
  - `[if_attachment]...[/if_attachment]` - Conditional blocks
  - `{option1|option2|option3}` - Random choice selection
  - `\n` - Line breaks

**Example Template:**
```
Hi <EmployerName>,

I've reviewed "<ProjectTitle>" and I'm excited to help with {this project|your requirements}.

With expertise in <ProjectSkills>, I can {deliver|provide|complete} {quality work|excellent results}.

[if_attachment]
I've reviewed your attachments and understand the requirements clearly.
[/if_attachment]

Best regards,
<FreelancerName>
```

#### b) Freelancer's AI
- Uses Freelancer.com's built-in AI
- Automatically generates proposals based on project details
- No configuration needed

#### c) Custom AI Integration
Supported AI providers:
- **Anthropic Claude**
- **OpenAI**
- **Google Gemini**
- **Z.ai**

Custom instructions can be provided for AI-generated proposals.

### 2. **Advanced Project Filtering**

#### Country Filters
- **Block Mode**: Exclude specific countries
- **Allow Mode**: Only bid on projects from selected countries
- Support for 195+ countries worldwide

#### Client Filters
- **Payment Verified**: Only bid on clients with verified payment methods
- **Client Verified**: Only bid on verified clients
- **Deposit Made**: Only bid on clients who made deposits

#### Project Type Filters
- Fixed Price Projects
- Hourly Projects
- Budget range filtering (min/max)
#### Delivery Time Filters
- Minimum delivery time (days)
- Maximum delivery time (days)

#### Budget Configuration
**Fixed Projects:**
- Bid at minimum budget
- Bid at maximum budget  
- Custom budget ranges by currency
- Custom delivery times per budget range

**Hourly Projects:**
- Bid at minimum rate
- Bid at maximum rate
- Use own hourly rate
- Custom rate ranges by currency

#### Skill Matching
- Match projects with your skills
- Automatic skill-based filtering

### 3. **Bid Management**

#### Milestone Configuration
- Split payments into milestones
- Configure percentage for each milestone
- Milestone 1: Initial payment (default 100%)
- Milestone 2: Final payment (optional)

#### Profile Selection
- Select bidding profile (General or custom profiles)
- Different profiles for different project types

#### Bid Logging
- Complete history of all bids
- Project title, URL, timestamp
- Success/failure status
- Direct links to projects

### 4. **Contract Handling**

The extension can automatically sign:
- **NDA (Non-Disclosure Agreement)**
- **IP Agreement (Intellectual Property Agreement)**

**Requirements:**
- Configure signature details in settings:
  - Full legal name
  - Date of birth
  - Address (Street, City, State, Zip, Country)
  - Agreement to terms

### 5. **Login Status Detection**

- Automatic Freelancer.com login detection
- Real-time status updates
- Cookie-based authentication
- Periodic status checks (every 30 minutes)
- Manual refresh option

### 6. **Automation Features**

- **Sound Notifications**: Play custom sound on successful bid
- **Auto-Open Projects**: Open project page after bidding
- **Rate Limiting**: Respects Freelancer API limits
- **Error Handling**: Graceful error recovery
- **Retry Logic**: Automatic retry on failures

---

## Pricing Plans

### Plan Comparison

| Plan | Price | Original Price | Duration | Savings |
|------|-------|----------------|----------|---------|
| **Free** | $0 | - | 7 Days | - |
| **Egg** 🥚 | $6 | $10 | 1 Month | 40% |
| **Zerger** 👾 | $15 | $30 | 3 Months | 50% |
| **Protossi** 🤖 | $24 | $60 | 6 Months | 60% |
| **Terranium** 💎 | $36 | $120 | 1 Year | 70% |

### Plan Features

**Free Plan (7-day trial):**
- Full access to all functionalities
- Test all features before purchasing
- No credit card required

**Paid Plans:**
All paid plans include:
- Unlimited automated bidding
- AI proposal generation (all methods)
- Advanced filtering options
- Contract signing
- Sound notifications
- Priority support
- SSL encryption & data protection

**Most Popular:** Zerger (3 months) - Best value for regular users

**Best Value:** Terranium (1 year) - Maximum savings for power users

---

## Payment Methods

### 1. Direct Crypto Payment

**How It Works:**
1. User selects a plan
2. System generates a temporary wallet address
3. User sends BEP20 USDT (BSC network) to temporary wallet
4. System automatically verifies payment on blockchain
5. Payment is split automatically:
   - **50%** to Admin wallet
   - **50%** to Referrer wallet (if user was referred)
6. Plan is activated immediately after confirmation

**Payment Details:**
- Network: BSC (Binance Smart Chain)
- Token: USDT (BEP20)
- Confirmation Time: 1-2 minutes
- Payment Expiry: 10 minutes

**Process Flow:**
```
User → Temporary Wallet → [Auto Split] → Admin (50%) + Referrer (50%)
                                      ↓
                               Plan Activated
```

### 2. Wallet Payment

**How It Works:**
1. User must have sufficient USDT in their wallet
2. System checks on-chain balance
3. If insufficient BNB for gas fees:
   - System automatically funds 0.0001 BNB from admin wallet
   - Waits for confirmation
4. Transfers USDT from user's wallet:
   - To admin wallet (50% or 100%)
   - To referrer wallet (50% if applicable)
5. Plan activated immediately

**Requirements:**
- Sufficient USDT balance in wallet
- BSC network
- BNB for gas (auto-funded if needed)

**Advantages:**
- Use referral earnings to purchase plans
- Instant activation
- No need to send from external wallet

---

## Referral System
### Commission Structure

**Commission Rate: 50%**

When someone purchases a plan using your referral link:
- **You receive:** 50% of the purchase price
- **Admin receives:** 50% of the purchase price

### Referral Link Format

```
https://stormeye.app?ref=YOUR_USERNAME
```

**Example:**
```
https://stormeye.app?ref=john_doe
```

### How It Works

#### Step 1: Share Your Link
- Get your unique referral link from the Referral section
- Share on social media, blogs, forums, or directly with friends

#### Step 2: User Signs Up
- New user clicks your referral link
- Referral code is stored in their browser
- Works even if they sign up later

#### Step 3: User Purchases
- Referred user purchases any paid plan
- System automatically calculates 50% commission

#### Step 4: Instant Payout
- Commission goes directly to your crypto wallet
- No waiting period
- No approval needed
- Visible in wallet instantly

### Earnings Examples

| Plan Purchased | Price | Your Commission (50%) |
|----------------|-------|-----------------------|
| Egg | $6 | **$3** |
| Zerger | $15 | **$7.50** |
| Protossi | $24 | **$12** |
| Terranium | $36 | **$18** |

### Tracking Referrals

In your account dashboard, you can see:
- Total number of referrals
- Total earnings from referrals
- Pending withdrawal amount
- Complete referral history

### Referral Earnings Management

**Automatic Distribution:**
- Earnings credited to your wallet automatically
- Blockchain transaction hash recorded
- Viewable in transaction history

**Use Your Earnings:**
- Withdraw to external wallet anytime
- Use to purchase your own plans
- No minimum withdrawal amount

---

## Wallet Management

### Wallet Creation

**Automatic Setup:**
- Every user gets a crypto wallet automatically
- Created during registration
- Private key encrypted and stored securely

**Wallet Details:**
- Network: BSC (Binance Smart Chain)
- Token: USDT (BEP20)
- Full custody: You control your wallet
- Private key encrypted with strong encryption

### Wallet Features

#### 1. **Real-Time Balance**
- Shows current USDT balance
- Updates automatically every 30 seconds
- Manual refresh available
- Displays on-chain balance (verified from blockchain)

#### 2. **Transaction History**
View complete history of:
- **Deposits**: Incoming USDT transfers
- **Withdrawals**: Outgoing USDT transfers
- **Purchases**: Plan purchases using wallet
- **Referral Earnings**: Commission from referrals

Transaction details include:
- Amount (USD)
- Currency (BEP20_USDT)
- Transaction hash (blockchain link)
- Timestamp
- Status (Confirmed/Failed)

#### 3. **Deposit Funds**
**How to Deposit:**
1. Click "Deposit" button in wallet
2. Copy your wallet address
3. Send BEP20 USDT from any wallet/exchange
4. Balance updates automatically after blockchain confirmation

**Supported Networks:**
- BSC (Binance Smart Chain) - BEP20 USDT

**Important:**
- Only send BEP20 USDT on BSC network
- Sending other tokens or wrong network will result in loss
- Minimum deposit: $0.01
- Confirmation time: 1-2 minutes

#### 4. **Withdraw Funds**
**How to Withdraw:**
1. Click "Withdraw" button
2. Enter amount to withdraw
3. Enter destination wallet address
4. Confirm network (BSC) and token (USDT)
5. Submit withdrawal

**Withdrawal Details:**
- Network: BSC (Binance Smart Chain)
- Token: USDT (BEP20)
- Minimum: $0.01
- Maximum: Your available balance
- Fee: Network gas fees (very low on BSC)
- Processing time: 1-2 minutes

**Gas Fee Handling:**
- System automatically handles gas fees
- If insufficient BNB in wallet, system funds it
- No manual BNB management needed

---

## Withdrawal Process

### Standard Withdrawal (From Wallet)

**Process:**
1. **Initiate Withdrawal:**
   - Go to Wallet page
   - Click "Withdraw"
   - Enter amount and destination address

2. **System Checks:**
   - Verifies sufficient balance
   - Checks destination address validity
   - Ensures sufficient gas (BNB)

3. **Auto Gas Funding (if needed):**
   - System detects low BNB balance
   - Sends 0.0001 BNB from admin wallet
   - Waits for confirmation

4. **Transfer Execution:**
   - USDT transferred to destination
   - Transaction hash generated
   - Blockchain confirmation

5. **Completion:**
   - Transaction recorded in history
   - Balance updated
   - Email notification (if enabled)

### Withdrawal from Referral Earnings

**Two Options:**

**Option 1: Direct Withdrawal**
- Wait for earnings to appear in wallet balance
- Follow standard withdrawal process
- Withdraw to any external address

**Option 2: Use for Plan Purchase**
- Earnings available immediately in wallet
- Use "Pay with Wallet" option when purchasing
- No withdrawal needed

### Important Notes

- **No Minimum Threshold**: Withdraw any amount
- **No Waiting Period**: Withdraw immediately after earning
- **No Fees** (except network gas fees)
- **Instant Processing**: 1-2 minute confirmation
- **Transaction Hash**: Full blockchain transparency

---
## Extension-Sale Site Integration

### Authentication Flow

#### 1. **Extension Initialization**
When extension starts:
```
Extension → Backend: POST /api/extension/init
{
  "username": "freelancer_username",
  "referrer": "optional_referrer"
}
```

Backend Response:
```json
{
  "success": true,
  "isNewUser": true/false,
  "user": {
    "username": "freelancer_username",
    "currentPlan": "egg",
    "planExpireDate": "2025-12-31T23:59:59Z",
    "isExpired": false,
    "referrals": 5,
    "earnings": 42.50
  }
}
```

#### 2. **Sale Site Authentication**
User logs in on sale site:
- Google OAuth
- Email/Password
- Email verification required

JWT tokens generated:
- Access Token (1 hour expiry)
- Refresh Token (30 days expiry)

#### 3. **Extension-Sale Site Sync**

**Sync Process:**
```
Extension → Sale Site: Check if user logged in
Sale Site → Backend: GET /api/extension/check_auth (with JWT)
Backend → Extension: Returns logged_in status and username

If logged in:
  Extension → Backend: POST /api/extension/sync
  {
    "freelancer_username": "john_doe"
  }
  Backend links: freelancer_username ↔ user_email
  
Extension → Backend: GET /api/extension/plan_info (with JWT)
Backend returns:
  {
    "plan_type": "egg",
    "plan_expire_date": timestamp,
    "plan_start_date": timestamp,
    "status": "Active"
  }
```

#### 4. **Plan Synchronization**

**Scenarios:**

**Scenario A: No Plan Purchased**
```json
{
  "success": true,
  "no_plan_purchased": true,
  "message": "Using extension free trial"
}
```

**Scenario B: Active Plan**
```json
{
  "success": true,
  "plan_type": "egg",
  "plan_expire_date": 1735689599000,
  "plan_start_date": 1732924800000,
  "status": "Active"
}
```

**Scenario C: Expired Plan**
```json
{
  "success": true,
  "plan_type": "egg",
  "plan_expire_date": 1732924800000,
  "status": "Expired"
}
```

### Extension Start Tracking

**Purpose:** Track when users start using the extension

**Process:**
1. Extension calls `/api/extension/register_start` on first launch
2. Backend stores `start_timestamp` (milliseconds)
3. Timestamp persists across sessions
4. Used for analytics and trial management

---

## Technical Architecture

### Technology Stack

#### Frontend (Sale Site)
- **Framework**: React 18
- **Routing**: React Router v6
- **State Management**: Context API
- **Styling**: CSS Modules
- **HTTP Client**: Fetch API
- **Authentication**: JWT + Google OAuth

#### Backend (API Server)
- **Framework**: Flask (Python)
- **Authentication**: Flask-JWT-Extended
- **Database**: MongoDB
- **Encryption**: Cryptography library
- **Blockchain**: Web3.py
- **Email**: SMTP (Gmail)

#### Extension
- **Manifest**: Version 3
- **Service Worker**: Background.js
- **Content Scripts**: Content.js
- **Storage**: chrome.storage.local
- **Permissions**: activeTab, storage, cookies, notifications

### Database Schema

#### Users Collection
```javascript
{
  username: String,
  email: String,
  password_hash: String (bcrypt),
  email_verified: Boolean,
  verification_token: String,
  currentPlan: String, // 'egg', 'zerger', etc.
  planExpireDate: DateTime,
  planStartDate: DateTime,
  wallet_address: String, // BSC address
  encrypted_private_key: String,
  referrer: String, // Username of referrer
  referrals: Number,
  earnings: Number, // USD
  pendingWithdrawal: Number, // Deprecated
  last_blockchain_balance: Number,
  createdAt: DateTime,
  updatedAt: DateTime
}
```

#### Transactions Collection
```javascript
{
  username: String,
  type: String, // 'deposit', 'withdrawal', 'purchase', 'referral_earning'
  amount: Number,
  currency: String, // 'BEP20_USDT'
  tx_hash: String, // Blockchain transaction hash
  status: String, // 'confirmed', 'pending', 'failed'
  from_address: String,
  to_address: String,
  metadata: Object,
  created_at: DateTime
}
```

#### Pending Payments Collection
```javascript
{
  payment_id: String,
  username: String,
  plan_id: String,
  amount: Number,
  duration_days: Number,
  temp_wallet_address: String,
  temp_wallet_private_key_encrypted: String,
  referrer: String,
  referrer_wallet: String,
  referrer_amount: Number,
  admin_amount: Number,
  status: String, // 'waiting', 'received', 'transferring', 'completed', 'expired', 'failed'
  received_amount: Number,
  transfer_tx_hash_admin: String,
  transfer_tx_hash_referrer: String,
  expires_at: DateTime,
  created_at: DateTime,
  updated_at: DateTime
}
```

#### Extension Infos Collection
```javascript
{
  freelancer_username: String,
  start_timestamp: Number, // milliseconds
  user_email: String, // Linked sale site account
  created_at: DateTime,
  updated_at: DateTime
}
```

#### Referrals Collection
```javascript
{
  referrer: String,
  referred_user: String,
  plan: String,
  commission: Number,
  currency: String,
  tx_hash: String,
  date: DateTime
}
```

### API Endpoints

#### Authentication
```
POST   /api/auth/signup              - Register with email/password
POST   /api/auth/login               - Login with email/password  
POST   /api/auth/google              - Login/Register with Google
POST   /api/auth/verify-email        - Verify email with token
POST   /api/auth/resend-verification - Resend verification email
POST   /api/auth/refresh             - Refresh access token
GET    /api/auth/me                  - Get current user
```

#### Extension Integration
```
POST   /api/extension/init           - Initialize extension
POST   /api/extension/register_start - Register start timestamp
POST   /api/extension/get_extension_info - Get extension info
GET    /api/extension/check_auth     - Check if logged in (JWT)
GET    /api/extension/plan_info      - Get plan info (JWT)
POST   /api/extension/sync           - Sync extension with account (JWT)
```

#### Payment
```
POST   /api/payment/direct/create    - Create direct crypto payment
POST   /api/payment/direct/verify    - Verify crypto payment
GET    /api/payment/direct/status/:id - Get payment status
POST   /api/wallet-payment/purchase  - Purchase with wallet balance
POST   /api/payment/auto/check/:id   - Auto-check payment status
```

#### Wallet
```
GET    /api/wallet/info              - Get wallet info with balance
GET    /api/wallet/transactions      - Get transaction history
POST   /api/wallet/withdraw          - Withdraw funds
POST   /api/wallet/deposit/verify    - Verify deposit transaction
GET    /api/wallet/balance/onchain   - Get on-chain balance
```

#### Pricing
```
GET    /api/pricing/plans            - Get all pricing plans (public)
```

### Security Features

#### Password Security
- **Hashing**: bcrypt with salt
- **Minimum Requirements**: 8+ characters
- **No plaintext storage**: Ever

#### JWT Authentication
- **Access Token**: 1 hour expiry
- **Refresh Token**: 30 days expiry
- **HttpOnly Cookies**: Prevents XSS
- **CORS**: Strict origin validation

#### Crypto Wallet Security
- **Private Key Encryption**: AES-256
- **Encryption Key**: Stored in environment variables
- **Never Exposed**: Private keys never sent to client
- **Server-Side Signing**: All transactions signed server-side

#### API Rate Limiting
- **Extension API**: Respects Freelancer.com rate limits
- **Backend API**: Rate limiting on sensitive endpoints
- **Blockchain Calls**: Cached to reduce RPC calls

---
## User Workflows

### Workflow 1: New User Registration & First Purchase

```
1. User visits https://stormeye.app
   ↓
2. Clicks "Sign Up"
   ↓
3. Chooses registration method:
   - Email/Password
   - Google OAuth
   ↓
4. If Email: Verifies email via link
   ↓
5. System automatically creates:
   - User account
   - Crypto wallet (BSC)
   - Encrypted private key
   ↓
6. User browses pricing plans
   ↓
7. Selects a plan (e.g., Zerger - $15)
   ↓
8. Chooses payment method:
   
   Option A: Pay with Crypto
   - Temporary wallet address generated
   - Sends BEP20 USDT from exchange/wallet
   - Payment auto-verified on blockchain
   - Auto-split: $7.50 admin + $7.50 referrer
   - Plan activated
   
   Option B: Pay with Wallet
   - Checks wallet balance
   - Insufficient funds → Must deposit first
   - Sufficient funds → Transfers to admin
   - Plan activated
   ↓
9. Downloads Chrome extension
   ↓
10. Opens extension settings
    ↓
11. Extension detects Freelancer login
    ↓
12. Extension calls /api/extension/init
    ↓
13. User can now click "Sync with Sale Site"
    ↓
14. Extension checks JWT authentication
    ↓
15. Extension syncs plan info
    ↓
16. User configures bidding settings
    ↓
17. Starts automated bidding!
```

### Workflow 2: Referral Earnings → Withdrawal

```
1. User gets referral link from dashboard
   ↓
2. Shares link on social media/forums
   ↓
3. Friend clicks link → ref=username stored
   ↓
4. Friend signs up and purchases Zerger ($15)
   ↓
5. System splits payment:
   - Admin: $7.50
   - Referrer (You): $7.50
   ↓
6. $7.50 deposited to your wallet instantly
   ↓
7. Transaction recorded with blockchain hash
   ↓
8. You see balance update in wallet dashboard
   ↓
9. Go to Wallet → Click "Withdraw"
   ↓
10. Enter:
    - Amount: $7.50
    - Destination: Your personal BSC wallet
    - Network: BSC (auto-selected)
    - Token: USDT (auto-selected)
    ↓
11. System checks:
    - Balance sufficient? ✓
    - BNB for gas? If not → Auto-fund 0.0001 BNB
    ↓
12. Withdrawal executed
    ↓
13. Transaction hash generated
    ↓
14. USDT arrives in your wallet (1-2 min)
    ↓
15. Transaction appears in history
```

### Workflow 3: Using Extension for Automated Bidding

```
1. Install extension & log into Freelancer.com
   ↓
2. Extension detects login automatically
   ↓
3. Open extension settings page
   ↓
4. Configure Country Filters:
   - Block: India, Pakistan, Bangladesh
   - Or Allow: USA, UK, Canada, Australia
   ↓
5. Configure Client Filters:
   - ✓ Payment Verified
   - ✓ Email Verified
   - ✓ Deposit Made
   ↓
6. Configure Budget:
   Fixed Projects:
   - If $100-$500 → Bid $120, Deliver in 7 days
   - If $500-$1000 → Bid $580, Deliver in 14 days
   
   Hourly Projects:
   - Use own rate: $50/hour
   ↓
7. Configure Proposal:
   Choose method:
   - Template (with shortcodes)
   - Freelancer's AI
   - Custom AI (Claude/GPT)
   ↓
8. If NDA/IP projects:
   - Add signature details
   - Extension will auto-sign
   ↓
9. Enable sound notification (optional)
   ↓
10. Click extension icon → Start Bidding
    ↓
11. Extension monitors Freelancer.com:
    - Checks new projects every 30 seconds
    - Applies all filters
    - Generates proposals
    - Submits bids automatically
    ↓
12. For each successful bid:
    - Sound notification plays (if enabled)
    - Project tab opens (if enabled)
    - Bid logged in history
    - Counter updated
    ↓
13. View bid history:
    - All bids with timestamps
    - Direct links to projects
    - Success/failure status
```

### Workflow 4: Using Referral Earnings to Buy Plans

```
1. Earned $15 from referrals
   ↓
2. Wallet shows: $15 available
   ↓
3. Current plan expires in 2 days
   ↓
4. Go to Pricing page
   ↓
5. Select Zerger plan ($15 for 3 months)
   ↓
6. Click "Purchase"
   ↓
7. Choose "Pay with Wallet"
   ↓
8. System checks balance: $15 available ✓
   ↓
9. System executes transfer:
   - Check BNB for gas
   - If low → Auto-fund from admin wallet
   - Transfer $15 to admin wallet
   - No referrer split (your own purchase)
   ↓
10. Plan activated immediately
    ↓
11. Extension syncs automatically
    ↓
12. New plan active: Zerger (3 months)
    ↓
13. Wallet balance: $0
    ↓
14. Continue bidding with new plan!
```

### Workflow 5: Failed Referrer Payment Scenario

```
1. Your referral purchases Terranium ($36)
   ↓
2. System attempts split:
   - Admin transfer: $18 → SUCCESS ✓
   - Referrer transfer: $18 → FAILED ✗
   ↓
3. Purchase still completes:
   - User's plan activated
   - Admin received payment
   ↓
4. System logs failed referrer transfer:
   - Referrer wallet address
   - Amount: $18
   - Admin TX hash (for reference)
   - Error message
   ↓
5. Your earnings recorded as "pending":
   - Shows in dashboard
   - Status: Pending manual payout
   ↓
6. Admin reviews failed transfers daily
   ↓
7. Manual payout processed within 24 hours:
   - Admin sends $18 directly to your wallet
   - Transaction hash recorded
   - Status updated to "confirmed"
   ↓
8. Email notification sent
   ↓
9. Balance available for withdrawal
```

---

## Best Practices

### For Users

#### Setting Up Extension
1. **Start with conservative filters**: Don't block too many countries initially
2. **Test proposal templates**: Create multiple variants and test which works best
3. **Monitor bid logs**: Check which projects you're winning
4. **Adjust budgets**: Update based on your win rate
5. **Use AI wisely**: Custom AI can be expensive, template works for most cases

#### Managing Referrals
1. **Share strategically**: Target freelancer communities and forums
2. **Create content**: Write blog posts or YouTube videos about the tool
3. **Track performance**: Monitor which channels bring most referrals
4. **Withdraw regularly**: Don't let earnings sit idle
5. **Reinvest earnings**: Use to extend your own subscription

#### Wallet Security
1. **Backup wallet**: Save your wallet address safely
2. **Never share private key**: System handles everything
3. **Verify addresses**: Double-check before withdrawing
4. **Use correct network**: Always BSC for USDT
5. **Keep small amounts**: Withdraw larger earnings regularly

### For Administrators

#### Payment Processing
1. **Monitor temporary wallets**: Check for stuck payments
2. **Handle failed referrer transfers**: Process manually within 24 hours
3. **Monitor gas prices**: Adjust gas funding amounts if BSC fees spike
4. **Verify blockchain transactions**: Always confirm on BSCScan
5. **Keep admin wallet funded**: Ensure enough BNB for gas funding

#### User Support
1. **Email verification issues**: Check spam folders, resend if needed
2. **Payment not confirmed**: Check blockchain explorer, may need more confirmations
3. **Wrong network deposits**: Educate users about BEP20 on BSC only
4. **Extension not syncing**: Verify JWT tokens, check CORS settings
5. **Referral not credited**: Check referral collection in database

---

## Troubleshooting Guide

### Extension Issues

**Extension not detecting login:**
- Clear browser cookies
- Log out and log back into Freelancer.com
- Click "Refresh Status" in extension
- Check if cookies are enabled

**Bids not submitting:**
- Verify Freelancer.com account is active
- Check if you have enough connects
- Verify project filters aren't too restrictive
- Check browser console for errors

**AI proposal generation failing:**
- Verify API key is correct
- Check API quota/billing
- Try different AI provider
- Fall back to template method

### Payment Issues

**Payment not confirmed:**
- Wait for blockchain confirmation (1-2 minutes)
- Check transaction on BSCScan
- Verify sent to correct address
- Verify correct network (BSC, not ETH/TRC20)

**Wallet balance not updating:**
- Click refresh button
- Wait 30 seconds for auto-refresh
- Check blockchain explorer
- Verify transaction confirmed

**Withdrawal failed:**
- Check if sufficient balance
- Verify destination address
- Check if address is BSC compatible
- Contact support if gas funding failed

### Account Issues

**Email not verified:**
- Check spam/junk folder
- Request new verification email
- Wait 5 minutes between requests
- Contact support if persistent

**Plan not activating:**
- Verify payment completed
- Check transaction status
- Refresh extension (reload settings page)
- Check plan expiry date in dashboard

**Referral not credited:**
- Verify referred user completed purchase
- Check if referral link was used correctly
- Wait 5 minutes for system processing
- Check transaction history

---

## API Reference (Quick)
### Base URL
```
Production: https://stormeye-backend-server.onrender.com
Development: http://localhost:5000
```

### Authentication Headers
```javascript
{
  "Authorization": "Bearer <access_token>",
  "Content-Type": "application/json"
}
```

### Example Requests

#### Get Pricing Plans (Public)
```bash
curl https://stormeye-backend-server.onrender.com/api/pricing/plans
```

Response:
```json
{
  "success": true,
  "plans": [
    {
      "id": "egg",
      "name": "Egg",
      "price": 6,
      "originalPrice": 10,
      "duration": "1 Month",
      "duration_days": 30,
      "avatar": "🥚",
      "features": ["Perfect for starters", "Save 40% cost"],
      "highlight": false,
      "color": "#ffd700"
    }
  ]
}
```

#### Create Direct Crypto Payment
```bash
curl -X POST \
  https://stormeye-backend-server.onrender.com/api/payment/direct/create \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "plan_id": "egg"
  }'
```

Response:
```json
{
  "success": true,
  "payment_id": "abc123def456...",
  "amount": 6,
  "temp_wallet_address": "0x1234567890abcdef...",
  "expires_at": "2025-10-22T12:30:00Z",
  "referrer": "john_doe",
  "referrer_amount": 3
}
```

#### Get Wallet Info
```bash
curl -X GET \
  https://stormeye-backend-server.onrender.com/api/wallet/info \
  -H "Authorization: Bearer <token>"
```

Response:
```json
{
  "success": true,
  "wallet": {
    "wallet_address": "0x1234567890abcdef...",
    "wallet_balance": 42.50,
    "earnings": 42.50,
    "blockchain_balances": {
      "bep20_usdt": 42.50,
      "total_usd": 42.50
    }
  }
}
```

#### Withdraw Funds
```bash
curl -X POST \
  https://stormeye-backend-server.onrender.com/api/wallet/withdraw \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "amount": 20.00,
    "to_address": "0xabcdef1234567890...",
    "network": "bsc",
    "token": "usdt"
  }'
```

Response:
```json
{
  "success": true,
  "message": "Withdrawal of $20.00 initiated",
  "tx_hash": "0x9876543210fedcba...",
  "explorer_url": "https://bscscan.com/tx/0x9876543210fedcba..."
}
```

---

## Configuration Files

### Pricing Configuration (pricing.json)
```json
{
  "plans": [
    {
      "id": "egg",
      "name": "Egg",
      "price": 6,
      "originalPrice": 10,
      "duration": "1 Month",
      "duration_days": 30,
      "avatar": "🥚",
      "avatarType": "emoji",
      "features": [
        "Perfect for starters",
        "Save 40% cost"
      ],
      "highlight": false,
      "color": "#ffd700"
    }
  ]
}
```

### Environment Variables

#### Backend (.env)
```bash
# Database
MONGODB_URI=mongodb+srv://...

# JWT
SECRET_KEY=your-secret-key
JWT_SECRET_KEY=your-jwt-secret-key

# Email
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=your-email@gmail.com
SMTP_PASSWORD=your-app-password

# Crypto Wallet
WALLET_ENCRYPTION_KEY=your-encryption-key
ADMIN_PRIVATE_KEY=your-admin-private-key

# BSC RPC
BSC_RPC_URL=https://bsc-dataseed.binance.org/

# Referral
REFERRAL_COMMISSION_RATE=0.5

# Pricing
PRICING_CONFIG_FILE=config/pricing.json

# Frontend URL
FRONTEND_URL=https://stormeye.app
```

#### Frontend (.env)
```bash
REACT_APP_API_URL=https://stormeye-backend-server.onrender.com
REACT_APP_BASE_URL=https://stormeye.app
REACT_APP_GOOGLE_CLIENT_ID=your-google-client-id
```

---

## Deployment Guide

### Backend Deployment (Render.com)

1. **Create Web Service**
   - Connect GitHub repository
   - Select backend folder
   - Environment: Python 3

2. **Configure Build Command**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure Start Command**
   ```bash
   gunicorn app:app
   ```

4. **Add Environment Variables**
   - Copy all from .env.example
   - Update with production values

5. **Deploy**
   - Automatic deployment on git push
   - Monitor logs for errors

### Frontend Deployment (Vercel/Netlify)

1. **Build Configuration**
   - Build Command: `npm run build`
   - Output Directory: `build`
   - Node Version: 18.x

2. **Environment Variables**
   - REACT_APP_API_URL
   - REACT_APP_BASE_URL
   - REACT_APP_GOOGLE_CLIENT_ID

3. **Domain Configuration**
   - Add custom domain: stormeye.app
   - Configure DNS records
   - Enable HTTPS (automatic)

### Extension Publishing (Chrome Web Store)

1. **Prepare Extension**
   - Update manifest.json with production URLs
   - Remove development permissions
   - Update icons and screenshots

2. **Create ZIP**
   ```bash
   cd Fab
   zip -r stormeye-extension.zip . -x "*.git*" "node_modules/*" ".env"
   ```

3. **Upload to Chrome Web Store**
   - Pay $5 one-time developer fee
   - Upload ZIP file
   - Fill in store listing details
   - Submit for review

4. **Privacy Policy**
   - Required for Chrome Web Store
   - Host on stormeye.app/privacy
   - Include data collection details

---

## Support & Contact

### For Users
- **Website**: https://stormeye.app
- **Email**: support@stormeye.app
- **Documentation**: https://stormeye.app/docs

### For Developers
- **GitHub**: (Private repositories)
- **API Docs**: https://stormeye.app/api-docs
- **Status**: https://status.stormeye.app

### Emergency Contact
- **Critical Issues**: admin@stormeye.app
- **Security Issues**: security@stormeye.app
- **Response Time**: 24 hours

---

## Changelog

### Version 1.0.0 (Current)
**Extension Features:**
- ✓ Automated bidding on Freelancer.com
- ✓ AI proposal generation (Template, Freelancer AI, Custom AI)
- ✓ Advanced project filtering (Country, Client, Budget)
- ✓ Automatic NDA/IP contract signing
- ✓ Bid logging and history
- ✓ Sound notifications

**Sale Site Features:**
- ✓ User registration (Email, Google OAuth)
- ✓ 5 pricing plans with discounts
- ✓ Crypto payment processing (BEP20 USDT)
- ✓ Wallet payment option
- ✓ 50% referral commission
- ✓ Crypto wallet management
- ✓ Withdrawal system
- ✓ Real-time balance updates
- ✓ Transaction history

**Backend Features:**
- ✓ JWT authentication
- ✓ MongoDB database
- ✓ Blockchain integration (BSC)
- ✓ Automatic payment splitting
- ✓ Gas fee management
- ✓ Email verification
- ✓ RESTful API

---

## Future Roadmap

### Planned Features

**Q1 2026:**
- Mobile app (iOS/Android)
- Additional payment methods (Card payments via Stripe)
- More AI providers (Anthropic Claude Opus, Grok)
- Advanced analytics dashboard
- Bid success rate tracking

**Q2 2026:**
- Multi-platform support (Upwork, Fiverr)
- Team collaboration features
- API for third-party integrations
- Webhook notifications
- White-label solution

**Q3 2026:**
- Machine learning bid optimization
- Automatic skill matching
- Portfolio integration
- Client relationship management
- Invoice generation

**Q4 2026:**
- Multiple wallet support (Polygon, Arbitrum)
- Fiat payment options
- Subscription management
- Advanced reporting
- Premium support tiers

---

## Legal & Compliance

### Terms of Service
- Users must be 18+ years old
- Freelancer.com account required
- Comply with Freelancer.com ToS
- No spam or abusive bidding
- Referral fraud prohibited

### Privacy Policy
- Data encryption at rest and in transit
- No selling of user data
- GDPR compliant
- Email used for notifications only
- Wallet keys stored encrypted

### Refund Policy
- 7-day money-back guarantee
- Pro-rated refunds on request
- No refunds for completed months
- Referral earnings non-refundable

---

## Glossary

**BEP20**: Token standard on Binance Smart Chain (BSC)

**BSC**: Binance Smart Chain - blockchain network for smart contracts

**Gas Fee**: Transaction fee on blockchain networks

**JWT**: JSON Web Token - authentication method

**NDA**: Non-Disclosure Agreement

**IP Agreement**: Intellectual Property Agreement

**TX Hash**: Transaction Hash - unique identifier for blockchain transactions

**USDT**: Tether - stablecoin pegged to USD

**Wallet**: Cryptocurrency wallet for storing and sending crypto

**RPC**: Remote Procedure Call - communication protocol for blockchain

**Chrome Extension**: Browser add-on that extends functionality

**Service Worker**: Background script that runs without UI

**Content Script**: Script that runs in webpage context

**OAuth**: Open standard for access delegation (Google login)

---

## Appendix

### Supported Countries (195 total)
Full list available in extension settings. Notable countries:
- 🇺🇸 United States
- 🇬🇧 United Kingdom  
- 🇨🇦 Canada
- 🇦🇺 Australia
- 🇩🇪 Germany
- 🇮🇳 India
- 🇵🇰 Pakistan
- ... (and 188 more)

### Supported Currencies
- USD - US Dollar
- EUR - Euro
- GBP - British Pound
- AUD - Australian Dollar
- CAD - Canadian Dollar
- INR - Indian Rupee
- ... (Freelancer.com supported currencies)

### Blockchain Explorers
- **BSC**: https://bscscan.com
- **Polygon** (future): https://polygonscan.com

---

**Document Version**: 1.0.0  
**Last Updated**: October 22, 2025  
**Maintained By**: StormEye Development Team

---

*This documentation is subject to change as the system evolves. Always refer to the latest version at https://stormeye.app/docs*