# Hugo Base Theme

A comprehensive, production-ready Hugo theme that serves as an excellent starting point for modern website development. Built with semantic HTML5, accessibility best practices, responsive design, and developer-friendly architecture.

## ✨ Features

### 🎨 Design & User Experience
- **Responsive Design**: Mobile-first approach with flexible grid layouts
- **Dark Mode Support**: Automatic detection with manual toggle option
- **Semantic HTML5**: Proper use of semantic elements for better accessibility and SEO
- **Microformats2**: IndieWeb compatible
- **Modern CSS**: CSS custom properties, flexbox, and grid layouts
- **Typography**: Carefully crafted typography scale with web fonts

### ♿ Accessibility
- **WCAG AA Compliant**: Meets accessibility guidelines
- **Keyboard Navigation**: Full keyboard support throughout the site
- **Screen Reader Friendly**: Proper ARIA attributes and semantic markup
- **High Contrast**: Accessible color schemes in both light and dark modes

### 🚀 Performance
- **Fast Loading**: Optimized CSS and minimal JavaScript
- **Image Optimization**: Responsive images with lazy loading
- **Critical CSS**: Inlined critical styles for faster rendering
- **Caching**: Efficient browser caching strategies
- **Lighthouse Optimized**: High scores across all metrics

### 🔍 SEO & Social
- **Open Graph**: Complete Open Graph meta tags
- **Twitter Cards**: Rich Twitter card support
- **Structured Data**: JSON-LD markup for better search visibility
- **XML Sitemap**: Automatic sitemap generation
- **RSS Feeds**: Full-content RSS feeds for all sections

### 📝 Content Features
- **Blog Support**: Full-featured blog with categories and tags
- **Table of Contents**: Automatic TOC generation for long posts
- **Related Posts**: Intelligent content recommendations
- **Social Sharing**: Built-in social media sharing buttons
- **Reading Time**: Estimated reading time for posts
- **Author Profiles**: Rich author information and bios

### 🛠️ Developer Experience
- **Clean Code**: Well-organized, documented, and maintainable
- **Modular Architecture**: Reusable partials and components
- **Customizable**: Easy theming with CSS custom properties
- **Hugo Best Practices**: Follows Hugo conventions and best practices
- **No Dependencies**: Works with vanilla Hugo installation

## 🚀 Quick Start

### Prerequisites
- Hugo v0.112.0 or later
- Git (for theme installation)

### Installation

#### Option 1: Git Submodule (Recommended)
```bash
# Initialize your Hugo site
hugo new site my-site
cd my-site

# Initialize git and add theme as submodule
git init
git submodule add https://github.com/raisingpixels/hugo-base-theme.git themes/base-theme
```

#### Option 2: Hugo Modules
```bash
# Initialize your site as a Hugo module
hugo mod init github.com/yourusername/your-site

# Add theme to your hugo.toml
echo 'theme = ["github.com/raisingpixels/hugo-base-theme"]' >> hugo.toml

# Download the theme
hugo mod get
```

#### Option 3: Download and Extract
1. Download the latest release from GitHub
2. Extract to `themes/base-theme/`

### Preview the Theme

After downloading the theme, ensure you have the necessary configuration before starting the development server to preview the theme.

```bash
# Copy example configuration
cp themes/base-theme/exampleSite/hugo.toml .

# Start the development server
hugo server -D
```

## 📖 Documentation

### Configuration

The theme supports extensive configuration through your `hugo.toml` file. See the [example configuration](exampleSite/hugo.toml) for all available options.

Update your `hugo.toml` with basic settings:

```toml
baseURL = "https://example.com"
languageCode = "en-us"
title = "My Awesome Site"
theme = "base-theme"
```

#### Essential Parameters

```toml
[params]
  # Site information
  description = "Your site description"
  author = "Your Name"
  authorBio = "Brief bio about yourself"

  # Branding
  logo = "/images/logo.svg" # empty string for no logo
  favicon = "/images/favicon.ico"

  # Features
  enableDarkMode = true
  enableSearch = true
  enableComments = false
  enableTableOfContents = true
  enableSocialSharing = true
```

#### Menu Configuration

```toml
[[menu.main]]
  name = "Home"
  url = "/"
  weight = 10

[[menu.main]]
  name = "About"
  url = "/about/"
  weight = 20

[[menu.main]]
  name = "Posts"
  url = "/posts/"
  weight = 30
```

#### Social Media Links

```toml
[params.social]
  twitter = "yourusername"
  github = "yourusername"
  linkedin = "yourusername"
  email = "hello@example.com"
  rss = true
```

### Content Structure

```bash
content/
├── _index.md          # Homepage content
├── about.md           # About page
├── contact.md         # Contact page
├── posts/             # Blog posts
│   ├── _index.md      # Posts section page
│   └── my-post.md     # Individual post
└── projects/          # Custom section
    ├── _index.md
    └── project-1.md
```

### Front Matter

#### Page Front Matter
```yaml
---
title: "Page Title"
description: "Page description for SEO"
date: 2024-01-20T09:00:00Z
lastmod: 2024-01-20T09:00:00Z
draft: false
---
```

#### Post Front Matter
```yaml
---
title: "Post Title"
description: "Post description"
date: 2024-01-20T09:00:00Z
lastmod: 2024-01-20T09:00:00Z
draft: false
author: "Author Name"
categories: ["Category"]
tags: ["tag1", "tag2"]
featured_image: "/images/post-image.jpg"
featured_image_alt: "Image description"
toc: true
---
```

## 🎨 Customization

### Colors and Theming

The theme uses CSS custom properties for easy customization. Override these in your own CSS:

```css
:root {
  --color-primary: #your-color;
  --color-secondary: #your-color;
  --font-family-sans: "Your Font", sans-serif;
}
```

### Custom CSS

Add custom styles by creating `assets/css/custom.css` in your site:

```css
/* Your custom styles */
.my-custom-class {
  /* Custom styles */
}
```

### Custom Layouts

Override any template by creating the same file structure in your site's `layouts/` directory:

```bash
layouts/
├── _default/
│   └── single.html    # Override single post layout
├── partials/
│   └── header.html    # Override header partial
└── index.html         # Override homepage layout
```

The simplest method is to copy the theme template into your `layouts` directory, then modify it.

```bash
cp themes/base-theme/layouts/index.html layouts/index.html
```

### AI-Assisted Styling

The Hugo Base Theme is designed to work seamlessly with AI coding assistants. Here are effective prompts for customizing your theme:

#### Color Scheme Customization
```txt
"Update the CSS custom properties in themes/base-theme/assets/css/main.css to use a [blue/green/purple] color scheme. Keep the existing structure but change the primary colors to create a cohesive [modern/professional/vibrant] look."
```

#### Component Styling
```txt
"Add CSS styles to make the post cards have a [glassmorphism/neumorphism/minimalist] design. The cards should have [subtle shadows/rounded corners/gradient backgrounds] while maintaining accessibility and the existing responsive behavior."
```

#### Layout Modifications
```txt
"Modify the header layout in themes/base-theme/layouts/partials/header.html to add a [search bar/social icons/call-to-action button] while keeping the existing navigation structure and mobile responsiveness."
```

#### Typography Enhancements
```txt
"Update the typography system to use [Google Fonts/system fonts] with a [serif/sans-serif] font stack. Ensure proper font loading performance and maintain the existing font size scale."
```

#### Dark Mode Customization
```txt
"Enhance the dark mode theme with [warmer/cooler] colors and add [accent colors/gradient backgrounds] while maintaining WCAG AA contrast ratios."
```

#### Animation and Interactions
```txt
"Add subtle CSS animations to [buttons/cards/navigation] with [fade/slide/scale] effects. Use CSS transitions and respect the prefers-reduced-motion setting for accessibility."
```

#### Mobile Optimization
```txt
"Improve the mobile experience by adjusting [spacing/typography/navigation] for screens under 768px. Focus on [touch targets/readability/performance] while maintaining the existing responsive grid."
```

#### Performance Enhancements
```txt
"Optimize the CSS by [removing unused styles/combining selectors/improving specificity] while maintaining all existing functionality and visual design."
```

#### Tips for AI Collaboration:
- **Be Specific**: Mention exact file paths and CSS class names
- **Preserve Functionality**: Ask to maintain existing responsive behavior and accessibility features
- **Test Thoroughly**: Always test changes across different screen sizes and themes
- **Incremental Changes**: Make one modification at a time for easier debugging
- **Backup First**: Keep copies of working files or make interim commits before major changes

## 🔧 Advanced Features

### Search

The theme includes client-side search functionality. Enable it in your configuration:

```toml
[params]
  enableSearch = true

[outputs]
  home = ["HTML", "RSS", "JSON"]
```

### Comments

Support for multiple comment systems:

```toml
[params]
  enableComments = true
  commentsSystem = "disqus"  # or "utterances"
  disqusShortname = "your-shortname"
```

### Analytics

Add analytics tracking:

```toml
[params]
  googleAnalytics = "G-XXXXXXXXXX"
```

### Newsletter

Enable newsletter signup:

```toml
[params]
  enableNewsletter = true
  newsletterService = "mailchimp"
  mailchimpURL = "your-mailchimp-url"
```

## 📱 Browser Support

- **Modern Browsers**: Chrome, Firefox, Safari, Edge (latest versions)
- **Progressive Enhancement**: Graceful degradation for older browsers
- **Mobile First**: Optimized for mobile devices
- **Accessibility**: Screen readers and assistive technologies

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Bug Reports
- Use the GitHub issue tracker
- Include Hugo version and operating system
- Provide steps to reproduce the issue
- Include screenshots if applicable

### Feature Requests
- Check existing issues first
- Provide detailed description and use case
- Consider contributing the implementation

### Code Contributions
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Setup

```bash
# Clone the repository
git clone https://github.com/raisingpixels/hugo-base-theme.git
cd hugo-base-theme

# Run the example site
cd exampleSite
hugo server -D --themesDir ../..
```

## 📄 License

This theme is released under the [MIT License](LICENSE). You are free to use it for personal and commercial projects.

## 🙏 Acknowledgments

- [Hugo](https://gohugo.io/) - The world's fastest framework for building websites
- [Hugo Community](https://discourse.gohugo.io/) - For inspiration and support
- Contributors and users who help improve this theme

## 📞 Support

- **Documentation**: Check this README and the example site
- **Issues**: Use the GitHub issue tracker

---

**Made with ❤️ for the Hugo community**

If you find this theme useful, please consider giving it a ⭐ on GitHub!
