# Valentine Card

A playful web application that asks the user to be your Valentine. The app features a "Yes" button that leads to a celebration and a "No" button that moves around the screen when interacted with, making it difficult to click.

### Url - [Click here for live view](https://valentine-card.junadhon81.workers.dev/)

## Tech Stack

- **Frontend Framework**: Svelte 5
- **Build Tool**: Vite
- **Deployment**: Cloudflare Workers
- **Language**: JavaScript

## Getting Started

### Prerequisites

- Node.js (version 16 or higher)
- npm

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/junaid-h0ssain/valentine-card.git
   cd valentine-card
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Start the development server:
   ```
   npm run dev
   ```

4. Open your browser and navigate to `http://localhost:5173`

### Building for Production

```
npm run build
```

### Deployment

The app is configured for deployment to Cloudflare Workers. Use the following command to deploy:

```
npx wrangler deploy
```

Make sure you have the Cloudflare CLI installed and configured.
