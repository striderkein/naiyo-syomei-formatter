# 内容証明フォーマッター (Naiyo-Syomei Formatter)

This is a static web application for formatting Japanese "naiyo-syomei" (content certification) documents according to legal postal requirements. The application runs entirely in the browser with no build process required.

**Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.**

## Working Effectively

### Quick Start - Running the Application
- Start a local web server: `python3 -m http.server 8000`
- Open browser to: `http://localhost:8000`
- Test core functionality: Click "サンプル投入" (Sample Input) button to load test data
- Verify formatting: Check that preview shows properly formatted Japanese legal document

### No Build Process Required
- This is a **single HTML file application** - no compilation, bundling, or build steps needed
- **No package.json, no npm install, no build commands**
- Files: `index.html` (19KB main app), `README.md`, `.gitignore`
- Technology: Pure HTML/CSS/JavaScript with embedded styles and scripts

### Dependencies and Limitations
- **External CDN Dependencies** (for PDF generation):
  - `html2canvas@1.4.1` from jsdelivr CDN  
  - `jspdf@2.5.1` from jsdelivr CDN
- **PDF Generation Note**: PDF download functionality may fail in environments that block CDN access. This is expected and documented behavior.
- **No local dependencies** - application works offline except for PDF generation

## Validation Scenarios

### CRITICAL: Complete End-to-End Testing
After making any changes, **ALWAYS** manually test these complete user workflows:

1. **Basic Document Creation Flow**:
   - Fill in title: "催告書" 
   - Fill in date: "2025年8月12日"
   - Fill in body text with Japanese content
   - Fill in sender/receiver addresses
   - Click "整形する" (Format) - verify preview updates
   - Verify line counting and page calculation is correct

2. **Sample Data Validation**:
   - Click "サンプル投入" (Sample Input) button
   - Verify all form fields populate with legal document sample
   - Check preview shows: 16 lines, 1 page, 1,070 yen cost calculation
   - Verify Japanese text formatting follows 20-character line limits

3. **Layout Testing**:
   - Test different layouts: 20×26, 13×40, 26×20 character configurations
   - Change paragraph indentation settings (none, 1-character, 2-character)
   - Toggle "1行目は件名行として中央揃え" (Center title line) checkbox
   - Verify line breaks and character counting adjust correctly

4. **Cost Calculation Validation**:
   - Change postal service type in dropdown
   - Change delivery confirmation options  
   - Verify cost updates automatically (内容証明 + 郵便 + 書留 + 配達証明)

### Browser Testing Requirements
- Test in Chrome/Chromium (primary target)
- Verify responsive layout on different screen sizes
- Test Japanese character input and display

## Application Structure

### Key Files and Locations
```
/
├── index.html          # Complete application (HTML + CSS + JavaScript)
├── README.md          # Basic usage documentation  
├── .gitignore         # Standard Node.js and macOS exclusions
└── .github/
    └── copilot-instructions.md  # This file
```

### Important Code Sections in index.html
- **Lines 1-200**: HTML structure and CSS styling
- **Lines 200-350**: Core text layout algorithm with Japanese bracket handling
- **Lines 350-440**: UI event handlers and sample data
- **Lines 440-490**: PDF generation functionality (external CDN dependencies)

### Core Functionality
- **Text Layout Engine**: Handles Japanese character counting with special bracket pair logic
- **Document Formatting**: 3 standard layouts (20×26, 13×40, 26×20) matching postal regulations
- **Cost Calculator**: Automatic pricing based on document length and postal options
- **PDF Export**: Browser-based PDF generation using html2canvas + jsPDF

## Common Development Tasks

### Testing Changes
1. Start local server: `python3 -m http.server 8000`
2. Open `http://localhost:8000` in browser
3. Run through validation scenarios above
4. **NEVER skip the complete end-to-end testing** - simply loading the page is insufficient

### Debugging Layout Issues
- Use browser developer tools to inspect `.sheet` elements
- Check character counting in JavaScript console
- Verify CSS grid layouts for different screen sizes
- Test with various Japanese text input lengths

### Deployment
- **GitHub Pages automatic deployment** - no manual steps required
- Any push to main branch automatically updates: https://striderkein.github.io/naiyo-syomei-formatter/
- **No build artifacts to deploy** - direct HTML file serving

## Known Issues and Workarounds

### PDF Generation Limitations
- PDF download button will show JavaScript errors in environments blocking CDN access
- Error: "Cannot destructure property 'jsPDF' of 'window.jspdf' as it is undefined"
- **This is expected behavior** - document this in any bug reports rather than attempting to fix
- Core application functionality (formatting, preview) works perfectly without PDF generation

### Character Encoding
- Application specifically designed for Japanese content
- Uses proper Japanese fonts: "Hiragino Kaku Gothic ProN", Meiryo, etc.
- Handles Japanese punctuation and bracket pairs correctly

## Time Expectations

### No Build/Test Commands
- **Application startup**: Instant (static HTML file)
- **Local server startup**: 1-2 seconds with `python3 -m http.server`
- **Browser loading**: 1-2 seconds for initial page load
- **Form interactions**: Immediate response for all formatting operations

### Manual Testing Time
- **Complete validation scenarios**: 5-10 minutes for thorough testing
- **Basic smoke test**: 2-3 minutes (load page + sample data + verify preview)
- **PDF testing**: 1 minute (attempt download + document expected failure if CDN blocked)

## Emergency Procedures

### If Application Won't Load
1. Check if `index.html` file exists and is not corrupted
2. Verify local web server is running on correct port
3. Test with different browsers
4. Check browser console for JavaScript errors (CDN blocking is expected, other errors are not)

### If GitHub Pages Deployment Fails
- Check GitHub Pages settings in repository
- Verify `index.html` is in repository root
- GitHub Pages automatically serves `index.html` - no additional configuration needed

## Developer Notes

### Code Style
- **No external frameworks** - pure vanilla JavaScript
- **Embedded CSS** - all styles in `<style>` block  
- **Japanese comments** - some code comments are in Japanese
- **Minimal dependencies** - only CDN resources for PDF generation

### Key Algorithms
- **Bracket pair counting**: Special logic treats paired brackets （）「」『』 as single characters
- **Line wrapping**: Respects Japanese text layout conventions
- **Cost calculation**: Implements current Japan Post pricing structure

Always test the complete user workflow after any modifications to ensure the application continues to serve its purpose of creating properly formatted legal documents.