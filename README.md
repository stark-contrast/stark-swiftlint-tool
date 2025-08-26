# Stark SwiftLint Tool - User Guide

A specialized SwiftLint tool that checks your iOS projects for accessibility compliance and automatically reports results to the Stark platform.

## What This Tool Does

The Stark SwiftLint Tool scans your iOS project for accessibility issues and helps ensure your app meets accessibility standards. It includes 30+ specialized accessibility rules that check for things like:

- Proper text contrast ratios
- Touch target sizes
- Screen reader compatibility
- Label associations
- Video captions and audio descriptions
- And many more accessibility best practices

## System Requirements

- **macOS with Apple Silicon (M1/M2/M3)** - Currently only Apple Silicon Macs are supported
- **Xcode** (if integrating with Xcode projects)
- **[Stark account](https://app.getstark.co)** with an iOS asset type

## Getting Started

### Step 1: Download the Tool

1. [Download the `stark-swiftlint-tool.tar.gz` file](https://github.com/stark-contrast/stark-swiftlint-tool/releases/latest/download/stark-swiftlint-tool.tar.gz)
2. Extract it to a convenient location on your Mac:
   ```bash
   tar -xzf stark-swiftlint-tool.tar.gz
   ```
3. This creates a folder containing the `stark-swiftlint-scan` executable and the `stark-swiftlint` executable (used by `stark-swiftlint-scan`).

### Step 2: Get Your Stark Token

1. Log in to your Stark account at [app.getstark.co](https://app.getstark.co)
2. Navigate to your project
3. Create or edit your iOS asset
4. Find your project's **Stark Token** (it looks like `stark_1452216e48434f07bd0cf4f6f6502e56`)
5. Copy this token - you'll need it for running the tool

## Usage Options

### Option A: Run from Terminal (Recommended for Testing)

Open Terminal and navigate to where you extracted the tool:

```bash
# Basic usage - scans current directory
./stark-swiftlint-scan --stark-token YOUR_STARK_TOKEN_HERE

# Scan a specific project path
./stark-swiftlint-scan --stark-token YOUR_STARK_TOKEN_HERE --path /path/to/your/ios/project

# Give your scan a custom name
./stark-swiftlint-scan --stark-token YOUR_STARK_TOKEN_HERE --name "My App Accessibility Scan"
```

**Example:**
```bash
./stark-swiftlint-scan --stark-token stark_1452216e48434f07bd0cf4f6f6502e56 --name "MyApp iOS Lint" --path ~/Projects/MyApp
```

### Option B: Integrate with Xcode (Recommended for Continuous Checking)

This automatically runs accessibility checks every time you build your project.

1. **Open your Xcode project**
2. **Edit your build scheme:**
   - Go to **Product > Scheme > Edit Scheme...** (or press **⌘ <**)
3. **Add a build script:**
   - In the left sidebar, expand the **Build** section
   - Click on **Pre-actions** (to run before building) or **Post-actions** (to run after building)
   - Click the **+** button and select **New Run Script Action**
4. **Configure the script:**
   - In the **Provide build settings from** dropdown, select your project
   - In the script text area, paste:
   ```bash
   /full/path/to/stark-swiftlint-scan --stark-token YOUR_STARK_TOKEN_HERE --name "iOS Lint Check" --path "${SRCROOT}"
   ```

**Important:** Replace `/full/path/to/stark-swiftlint-scan` with the actual path where you extracted the tool.

**Example:**
```bash
/Users/john/Tools/stark-swiftlint-scan --stark-token stark_1452216e48434f07bd0cf4f6f6502e56 --name "MyApp Accessibility" --path "${SRCROOT}"
```

## Command Options

| Option | Description | Required |
|--------|-------------|----------|
| `--stark-token` | Your Stark project token | Yes |
| `--name` | Custom name for the scan report | No (defaults to folder name) |
| `--path` | Path to your iOS project | No (defaults to current directory) |

## What Happens When You Run It

1. **Scans your code:** The tool examines all Swift files in your project
2. **Applies accessibility rules:** Checks against 30+ accessibility best practices
3. **Reports to Stark:** Automatically uploads results to your Stark project dashboard
4. **Shows summary:** Displays a summary in your terminal

## Viewing Results

After running the scan:

1. **Check your terminal** for a summary of issues found
2. **Visit your Stark dashboard** at [app.getstark.co](https://app.getstark.co) to see detailed results
3. **Review specific violations** with file names and line numbers
4. **Track progress** over time as you fix accessibility issues

## Accessibility Rules

The tool includes 33 specialized accessibility rules to help ensure your iOS app meets accessibility standards:

| Rule Identifier | Description |
|-----------------|-------------|
| `stark_accordion_accessibility` | Accordion components must have proper accessibility labels and state indicators |
| `stark_active_image_accessibility` | Images with interactive modifiers or within interactive containers must have accessibility labels communicating their function |
| `stark_alert_accessibility` | Alert components must have accessible titles and optional descriptions |
| `stark_checkbox_accessibility` | Checkbox controls must have accessible labels describing their purpose |
| `stark_checkbox_group_accessibility` | Checkbox groups must have accessible group labels and individual checkbox labels |
| `stark_color_information_accessibility` | Information conveyed through color must also be available through other means |
| `stark_control_boundary_contrast` | Interactive controls must have sufficient contrast with their background |
| `stark_data_table_accessibility` | Data tables must have proper headers and accessible structure |
| `stark_enhanced_text_contrast` | Text must meet enhanced contrast requirements for better readability |
| `stark_heading_accessibility` | Headings must be properly structured and accessible |
| `stark_image_button_role` | Image buttons must have appropriate accessibility roles |
| `stark_label_association` | Form controls must be properly associated with their labels |
| `stark_label_visibility` | Labels must be visible and not hidden from assistive technologies |
| `stark_link_color_contrast` | Links must have sufficient color contrast with surrounding text |
| `stark_link_role` | Links must have appropriate accessibility roles and context |
| `stark_menu_accessibility` | Menu components must have proper navigation and accessibility support |
| `stark_page_language` | Pages must declare their primary language for assistive technologies |
| `stark_picker_view_accessibility` | Picker views must have accessible labels and selection indicators |
| `stark_progress_bar_accessibility` | Progress bars must have accessible labels indicating current progress |
| `stark_progress_spinner_accessibility` | Progress spinners must have accessible labels for loading states |
| `stark_radio_button_accessibility` | Radio button controls must have accessible labels and state indicators |
| `stark_radio_group_accessibility` | Radio button groups must have accessible group labels and selection states |
| `stark_rating_control_accessibility` | Rating controls must have accessible labels and current rating information |
| `stark_screen_title_accessibility` | Screen titles must be accessible and properly structured |
| `stark_slider_accessibility` | Slider controls must have accessible labels and value indicators |
| `stark_switch_accessibility` | Switch controls must have accessible labels describing their function |
| `stark_tab_accessibility` | Tab components must have proper accessibility navigation and labels |
| `stark_text_contrast` | Text must have sufficient contrast with its background |
| `stark_text_field_accessibility` | Text fields must have accessible labels and input requirements |
| `stark_toggle_button_accessibility` | Toggle buttons must have accessible labels and state indicators |
| `stark_touch_target_size` | Interactive elements must meet minimum touch target size requirements |
| `stark_video_audio_descriptions` | Videos must provide audio descriptions for visual content |
| `stark_video_captions` | Videos must provide captions for audio content |

### Configuring Rules

Due to the limitations of static code analysis, there may be some false positives, so you might want to ignore one or more rules that don't apply to your specific use case.

To disable specific rules, create a `.swiftlint.yml` file in your project root with the following structure:

```yaml
disabled_rules:
  - stark_video_captions
  - stark_video_audio_descriptions
  - stark_enhanced_text_contrast

# You can also configure other SwiftLint settings
line_length: 120
```

**Example use cases for disabling rules:**
- Disable `stark_video_captions` if your app doesn't include video content
- Disable `stark_enhanced_text_contrast` if you're following standard contrast guidelines instead of enhanced ones
- Disable specific control rules if you're using custom UI components that handle accessibility differently

## Running Checks in your CI/CD

You can integrate the Stark accessibility scan into your CI/CD pipeline to automatically check for accessibility issues on every push or pull request. Here's an example using GitHub Actions:

Create a `.github/workflows/stark-accessibility.yml` file in your repository:

```yaml
name: Stark Accessibility Scan

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  run-command:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Run Stark accessibility scan
        run: |
          echo "Running Stark accessibility scan..."
          ./stark-swiftlint-scan --stark-token YOUR_STARK_TOKEN
```

**Important:** Make sure to:
1. Replace `YOUR_STARK_TOKEN` with your actual Stark token
2. Consider storing your token as a [GitHub secret](https://docs.github.com/en/actions/security-guides/encrypted-secrets) and referencing it as `${{ secrets.STARK_TOKEN }}`
3. Include the `stark-swiftlint-scan` executable in your repository or download it as part of the workflow

## Troubleshooting

### "Command not found" or Permission Errors
```bash
# Make the tool executable
chmod +x /path/to/stark-swiftlint-scan
```

### "Binary not compatible"
- This tool currently only works on Apple Silicon Macs (M1/M2/M3)
- Intel Macs are not yet supported

### "Stark token invalid"
- Double-check your token from the Stark dashboard
- Ensure you're using the token for the correct iOS project
- Tokens start with `stark_` followed by a long string of characters

### "No Swift files found"
- Make sure you're pointing to the correct project directory
- The tool looks for `.swift` files in the specified path

### Xcode Integration Issues
- Verify the full path to `stark-swiftlint-scan` is correct
- Make sure the file is executable (`chmod +x`)
- Check that your Stark token is valid

## Best Practices

1. **Start with terminal testing** before integrating with Xcode
2. **Use descriptive names** for your scans to track different builds
3. **Run regularly** to catch accessibility issues early
4. **Review results in Stark** to understand and prioritize fixes
5. **Keep the tool updated** by downloading new versions from Stark

## Getting Help

- **Stark Support:** Visit [Stark support](https://www.getstark.co/support/) or email [support@getstark.co](mailto:support@getstark.co)
- **Community:** Join the [Stark community on Slack](https://join.slack.com/t/stark-community/shared_invite/zt-2vcvslegh-hdKIWCsahSdsrk3CPq9k7w)

---

*This tool helps ensure your iOS app is accessible to all users. Regular scanning and fixing of accessibility issues makes your app more inclusive and often improves the experience for all users.*