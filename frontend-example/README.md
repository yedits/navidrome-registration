# Frontend Registration Example

This directory contains a complete React registration form component that integrates with the Navidrome Registration Service.

## Files

- `RegisterForm.jsx` - Main registration component
- `RegisterForm.css` - Styling for the registration form

## Features

- ✅ Client-side form validation
- ✅ Password confirmation
- ✅ Real-time error display
- ✅ Loading states
- ✅ Success confirmation with redirect
- ✅ Responsive design
- ✅ Accessible form elements

## Installation

### Option 1: Add to Existing React Project

1. Copy both files to your React project:
```bash
cp RegisterForm.jsx your-project/src/components/
cp RegisterForm.css your-project/src/components/
```

2. Import and use the component:
```jsx
import RegisterForm from './components/RegisterForm';

function App() {
  return (
    <div>
      <RegisterForm />
    </div>
  );
}
```

### Option 2: Standalone React App

1. Create a new React app:
```bash
npx create-react-app registration-frontend
cd registration-frontend
```

2. Copy the files:
```bash
cp RegisterForm.jsx src/
cp RegisterForm.css src/
```

3. Update `src/App.js`:
```jsx
import RegisterForm from './RegisterForm';

function App() {
  return <RegisterForm />;
}

export default App;
```

4. Start the development server:
```bash
npm start
```

## Configuration

### API Endpoint

Update the API endpoint in `RegisterForm.jsx`:

```javascript
const REGISTRATION_API = 'http://localhost:3001/api/register';
```

Change this to your registration service URL.

### Redirect URL

After successful registration, users are redirected to `/login`. Update this in the component:

```javascript
window.location.href = '/login'; // Change to your login page
```

## Integration with Aonsoku

To integrate with your [Aonsoku frontend](https://github.com/onyxdagoat1/aonsoku-fork):

1. Add the component to your Aonsoku project
2. Create a registration route in your router
3. Update the API endpoint to point to your registration service
4. Style the component to match your Aonsoku theme

### Example Router Integration (React Router)

```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import RegisterForm from './components/RegisterForm';
import Login from './components/Login';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/register" element={<RegisterForm />} />
        <Route path="/login" element={<Login />} />
      </Routes>
    </BrowserRouter>
  );
}
```

## Customization

### Colors

Edit `RegisterForm.css` to match your brand colors:

```css
.register-container {
  background: linear-gradient(135deg, #YOUR_COLOR_1 0%, #YOUR_COLOR_2 100%);
}

.submit-button {
  background: linear-gradient(135deg, #YOUR_COLOR_1 0%, #YOUR_COLOR_2 100%);
}
```

### Validation Rules

Modify validation in `RegisterForm.jsx`:

```javascript
// Username validation
if (!/^[a-zA-Z0-9_-]{3,20}$/.test(formData.username)) {
  // Adjust pattern here
}

// Password validation
if (formData.password.length < 8) {
  // Change minimum length here
}
```

## Testing

1. Start your registration service:
```bash
cd navidrome-registration
npm start
```

2. Start your frontend:
```bash
cd your-frontend
npm start
```

3. Navigate to the registration page and test the form

## Troubleshooting

### CORS Errors

If you see CORS errors, ensure your registration service has the correct `FRONTEND_URL` in `.env`:

```env
FRONTEND_URL=http://localhost:3000
```

### API Connection Refused

Make sure:
1. Registration service is running
2. API endpoint URL is correct
3. No firewall blocking the connection

### Form Validation Not Working

Check browser console for JavaScript errors and ensure all dependencies are installed.

## Example Screenshots

### Registration Form
![Registration Form](https://via.placeholder.com/400x600?text=Registration+Form)

### Success State
![Success State](https://via.placeholder.com/400x300?text=Success+Message)

### Error Handling
![Error State](https://via.placeholder.com/400x600?text=Error+Handling)

## License

MIT License - Same as parent project
