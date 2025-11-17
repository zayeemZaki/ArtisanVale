<div align="center">
  <img src="/public/ArtisanVale.png" alt="ArtisanVale Logo" width="300"/>
  
  # 🌸 ArtisanVale
  
  ### Your Voice Shapes Our Skincare Collection
  
  [![Vue.js](https://img.shields.io/badge/Vue.js-3.5.17-4FC08D?style=for-the-badge&logo=vue.js&logoColor=white)](https://vuejs.org/)
  [![Vite](https://img.shields.io/badge/Vite-7.0.0-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
  [![Live Demo](https://img.shields.io/badge/Live-Demo-pink?style=for-the-badge)](https://artisanvale.in/)
  
</div>

---

## 📖 About ArtisanVale

**ArtisanVale** is an interactive, conversational skincare survey platform that empowers users to share their favorite beauty brands and product recommendations. Founded by Zayeem, this modern Vue.js application creates an engaging user experience through chat-like interactions, helping to shape a curated skincare collection based on real customer preferences.

The platform features a beautiful, responsive interface with smooth animations, intuitive brand selection, and the ability for users to suggest new products—making it a collaborative space where your beauty routine insights truly matter.

## ✨ Key Features

- **🎯 Interactive Survey Experience**: Conversational UI with chat bubbles for a friendly, engaging interaction
- **🔍 Smart Brand Search**: Real-time search functionality to quickly find your favorite skincare brands
- **💡 Multi-Select Interface**: Easily select multiple brands with visual feedback and smooth animations
- **📝 Brand & Product Suggestions**: Submit new brand recommendations with optional product details and images
- **📱 Fully Responsive Design**: Optimized for mobile, tablet, and desktop experiences
- **✨ Beautiful UI/UX**: Gradient backgrounds, smooth transitions, and modern design aesthetics
- **🚀 Lightning Fast**: Built with Vite for instant development server startup and optimized builds
- **🎨 Splash Screen**: Welcoming animated splash screen on first load

## 🛠️ Tech Stack

<table>
  <tr>
    <td align="center" width="20%">
      <strong>Vue.js</strong><br>
      92.9%
    </td>
    <td align="center" width="20%">
      <strong>CSS</strong><br>
      4.6%
    </td>
    <td align="center" width="20%">
      <strong>HTML</strong><br>
      1.6%
    </td>
    <td align="center" width="20%">
      <strong>JavaScript</strong><br>
      0.9%
    </td>
  </tr>
</table>

### Core Technologies

- **[Vue 3](https://vuejs.org/)** - Progressive JavaScript framework with Composition API
- **[Vite](https://vitejs.dev/)** - Next-generation frontend tooling
- **[Tailwind CSS](https://tailwindcss.com/)** - Utility-first CSS framework (via CDN)

## 🌐 Live Demo

Check out the live application: **[artisanvale.in](https://artisanvale.in/)**

## 📸 Screenshots

> Add your application screenshots here to showcase the UI/UX

```
<!-- Example structure for when you add screenshots:
![Home Screen](./screenshots/home.png)
![Brand Selection](./screenshots/brand-selection.png)
![Product Suggestion](./screenshots/product-suggestion.png)
-->
```

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:
- **Node.js** (v18 or higher recommended)
- **npm** (v9 or higher) or **yarn**

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/zayeemZaki/ArtisanVale.git
   cd ArtisanVale
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

### Development

Run the development server with hot-reload:

```bash
npm run dev
```

The application will be available at `http://localhost:5173/` (or another port if 5173 is busy).

### Build for Production

Create an optimized production build:

```bash
npm run build
```

The built files will be generated in the `dist/` directory.

### Preview Production Build

Preview the production build locally:

```bash
npm run preview
```

### Deployment

Deploy to GitHub Pages:

```bash
npm run deploy
```

This command builds the project and deploys it to the `gh-pages` branch.

## 📁 Project Structure

```
ArtisanVale/
├── public/                  # Static assets
│   ├── ArtisanVale.png     # Logo and branding
│   ├── CNAME               # Custom domain configuration
│   └── vite.svg            # Vite icon
├── src/
│   ├── components/          # Vue components
│   │   ├── AddBrandForm.vue      # Form for suggesting new brands
│   │   ├── BrandList.vue         # Display list of brands
│   │   ├── ChatBubble.vue        # Chat message component
│   │   ├── ContactForm.vue       # User contact information form
│   │   ├── ConversationalForm.vue # Main conversational survey flow
│   │   ├── Footer.vue            # Application footer
│   │   └── Header.vue            # Application header with logo
│   ├── assets/              # Images, styles, and other assets
│   ├── App.vue              # Root Vue component
│   ├── main.js              # Application entry point
│   └── style.css            # Global styles
├── index.html               # HTML entry point
├── vite.config.js           # Vite configuration
├── package.json             # Project dependencies and scripts
└── README.md                # This file
```

## 📦 Dependencies

### Production Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| **vue** | ^3.5.17 | Core Vue.js framework for building the reactive UI |

### Development Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| **@vitejs/plugin-vue** | ^6.0.0 | Official Vite plugin for Vue 3 support |
| **vite** | ^7.0.0 | Build tool and development server |
| **gh-pages** | ^6.3.0 | Deployment tool for GitHub Pages |

### External Libraries (CDN)

- **Tailwind CSS** - Loaded via CDN for rapid styling

## 🌍 Browser Support

ArtisanVale supports all modern browsers:

- ✅ Chrome/Edge (latest 2 versions)
- ✅ Firefox (latest 2 versions)
- ✅ Safari (latest 2 versions)
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

> **Note**: The application uses modern JavaScript features and may not work in older browsers without polyfills.

## 🤝 Contributing

We welcome contributions to ArtisanVale! Here's how you can help:

### How to Contribute

1. **Fork the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/ArtisanVale.git
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```

3. **Make your changes**
   - Write clean, maintainable code
   - Follow the existing code style
   - Test your changes thoroughly

4. **Commit your changes**
   ```bash
   git commit -m "Add amazing feature"
   ```

5. **Push to your fork**
   ```bash
   git push origin feature/amazing-feature
   ```

6. **Open a Pull Request**
   - Provide a clear description of your changes
   - Link any relevant issues

### Code Style Guidelines

- Use Vue 3 Composition API
- Follow Vue.js style guide
- Use meaningful component and variable names
- Keep components focused and reusable
- Write self-documenting code

### Reporting Issues

Found a bug or have a feature request? [Open an issue](https://github.com/zayeemZaki/ArtisanVale/issues) with:
- Clear title and description
- Steps to reproduce (for bugs)
- Expected vs actual behavior
- Screenshots if applicable

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Zayeem Zaki**

- GitHub: [@zayeemZaki](https://github.com/zayeemZaki)
- Website: [artisanvale.in](https://artisanvale.in/)

## 💖 Acknowledgments

- Thanks to all users who share their skincare preferences
- Built with love using Vue.js and modern web technologies
- Inspired by the need for better customer-driven product curation

---

<div align="center">
  
  **Made with 💖 by Zayeem**
  
  If you find this project helpful, please consider giving it a ⭐!
  
</div>
