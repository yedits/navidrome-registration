# Navidrome Registration Service

A self-service user registration middleware for [Navidrome](https://github.com/navidrome/navidrome) music server. Enables public user registration while maintaining admin control.

## 🎯 Features

- ✅ Self-service user registration via REST API
- ✅ Automatic user creation in Navidrome via Subsonic API
- ✅ Rate limiting to prevent spam registrations
- ✅ Input validation (username, email, password strength)
- ✅ CORS support for frontend integration
- ✅ Token-based authentication with Navidrome
- ✅ Configurable user permissions
- ✅ Admin accounts remain protected

## 📋 Prerequisites

- Node.js 14.x or higher
- Running Navidrome instance
- Navidrome admin credentials

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/onyxdagoat1/navidrome-registration.git
cd navidrome-registration
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Copy the example environment file:

```bash
cp .env.example .env
```

Edit `.env` with your settings:

```env
NAVIDROME_URL=http://localhost:4533
NAVIDROME_ADMIN_USER=admin
NAVIDROME_ADMIN_PASSWORD=your_admin_password_here
PORT=3001
FRONTEND_URL=http://localhost:3000
```

### 4. Start the Server

```bash
# Production
npm start

# Development (with auto-reload)
npm run dev
```

The server will start on `http://localhost:3001`

## 📡 API Endpoints

### Register User

**Endpoint:** `POST /api/register`

**Request Body:**
```json
{
  "username": "newuser",
  "password": "securepassword123",
  "email": "user@example.com"
}
```

**Success Response (200):**
```json
{
  "success": true,
  "message": "Account created successfully",
  "username": "newuser"
}
```

**Error Response (400/500):**
```json
{
  "success": false,
  "error": "Username must be 3-20 characters"
}
```

### Health Check

**Endpoint:** `GET /api/health`

**Response:**
```json
{
  "status": "ok",
  "message": "Registration service running",
  "navidromeUrl": "http://localhost:4533"
}
```

## 🔒 Validation Rules

- **Username:** 3-20 characters, alphanumeric + underscore/hyphen only
- **Password:** Minimum 8 characters
- **Email:** Valid email format required
- **Rate Limiting:** 5 registration attempts per 15 minutes per IP

## 👥 User Permissions

Registered users are created with these permissions:

- ✅ **Stream:** Listen to music
- ✅ **Download:** Download tracks
- ✅ **Upload:** Upload their own music
- ✅ **Playlists:** Create and manage playlists
- ✅ **Share:** Share music with others
- ✅ **Comments:** Add comments to tracks/albums
- ✅ **Podcasts:** Access podcast features
- ✅ **Cover Art:** Upload album artwork
- ❌ **Admin:** No admin panel access
- ❌ **Jukebox:** No jukebox control
- ❌ **Settings:** No global settings access

## 🎨 Frontend Integration

See the [frontend-example](./frontend-example) directory for a complete React registration form.

**Quick Example:**

```javascript
const registerUser = async (username, password, email) => {
  const response = await fetch('http://localhost:3001/api/register', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ username, password, email })
  });
  
  const data = await response.json();
  
  if (data.success) {
    console.log('Registration successful!');
    // Redirect to login
  } else {
    console.error('Registration failed:', data.error);
  }
};
```

## 🐳 Docker Deployment

Create a `docker-compose.yml`:

```yaml
version: '3'
services:
  navidrome-registration:
    build: .
    ports:
      - "3001:3001"
    environment:
      - NAVIDROME_URL=http://navidrome:4533
      - NAVIDROME_ADMIN_USER=admin
      - NAVIDROME_ADMIN_PASSWORD=your_password
      - FRONTEND_URL=http://localhost:3000
    restart: unless-stopped
```

## 🔐 Security Considerations

1. **Never commit `.env`** - Keep admin credentials secure
2. **Use HTTPS in production** - Set up a reverse proxy (Nginx/Caddy)
3. **Restrict CORS** - Set `FRONTEND_URL` to your actual domain
4. **Rate limiting enabled** - Prevents spam registrations
5. **Input validation** - All inputs are sanitized
6. **Token authentication** - Uses MD5 token method for API calls

## 📦 Production Deployment

### Using PM2

```bash
npm install -g pm2
pm2 start server.js --name navidrome-registration
pm2 save
pm2 startup
```

### With Systemd

Create `/etc/systemd/system/navidrome-registration.service`:

```ini
[Unit]
Description=Navidrome Registration Service
After=network.target

[Service]
Type=simple
User=www-data
WorkingDirectory=/opt/navidrome-registration
ExecStart=/usr/bin/node server.js
Restart=on-failure
Environment=NODE_ENV=production

[Install]
WantedBy=multi-user.target
```

Enable and start:
```bash
sudo systemctl enable navidrome-registration
sudo systemctl start navidrome-registration
```

## 🧪 Testing

### Test Registration Endpoint

```bash
curl -X POST http://localhost:3001/api/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "password": "testpass123",
    "email": "test@example.com"
  }'
```

### Test Health Check

```bash
curl http://localhost:3001/api/health
```

## 🤝 Related Projects

- [Navidrome](https://github.com/navidrome/navidrome) - The music server backend
- [Aonsoku](https://github.com/onyxdagoat1/aonsoku-fork) - Frontend streaming service

## 📝 License

MIT License - See [LICENSE](LICENSE) file for details

## 🐛 Issues & Support

For issues related to:
- **This registration service:** Open an issue in this repository
- **Navidrome itself:** Visit [Navidrome's GitHub](https://github.com/navidrome/navidrome)

## 🙏 Acknowledgments

- [Navidrome](https://www.navidrome.org) for the excellent music server
- [Subsonic API](https://www.subsonic.org/pages/api.jsp) for the API specification
