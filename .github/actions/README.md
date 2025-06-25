# WSUEs Fetch Workflow Actions

This directory contains reusable composite actions for the WSUEs (Windows Security Update Eligibility) fetch workflow.

## 📁 Actions Overview

### 🔧 setup-wsues
**Purpose**: Download and setup the WSUEs tool
- Downloads WSUEs from the specified repository
- Extracts the tool to a designated path
- Creates necessary directories
- Validates the installation

### 📊 fetch-wsues-data
**Purpose**: Fetch WSUEs data for specified products and dates
- Supports both single product and all products fetch
- Handles error checking and logging
- Provides flexible output options

### 🗜️ compress-files
**Purpose**: Compress JSON files with gzip
- Compresses each JSON file individually
- Calculates and reports compression ratios
- Organizes compressed files in a separate directory

### 🚀 create-release
**Purpose**: Create GitHub releases with the fetched data
- Creates properly formatted releases
- Includes comprehensive release notes
- Handles file path conversion for cross-platform compatibility

### 📅 check-patch-tuesday
**Purpose**: Determine if the current date is Patch Tuesday
- Calculates the second Tuesday of each month
- Provides formatted date outputs
- Includes detailed logging for transparency

## 🎯 Benefits of This Architecture

### ✅ Advantages
- **DRY Principle**: Eliminates code duplication
- **Maintainability**: Changes only need to be made in one place
- **Testability**: Each action can be tested independently
- **Reusability**: Actions can be used in other workflows
- **Clarity**: Each action has a single, clear responsibility
- **Error Handling**: Centralized error handling and logging

### 🔄 Workflow Structure
The main workflow now follows a clean, modular approach:

```yaml
jobs:
  manual-fetch:
    steps:
      - checkout
      - setup-wsues
      - fetch-wsues-data
      - compress-files (if needed)
      - upload-artifacts
      - create-release (if needed)

  scheduled-fetch:
    steps:
      - check-patch-tuesday
      - (conditional execution of the same steps as manual-fetch)
```

## 🛠️ Usage Examples

Each action is designed to be self-contained and easy to use:

```yaml
- name: Setup WSUEs
  uses: ./.github/actions/setup-wsues
  with:
    token: ${{ secrets.WSUESTOKEN }}
    workspace-path: ${{ github.workspace }}
```

## 📝 Maintenance Notes

- Each action includes comprehensive error handling
- Logging provides clear feedback about what's happening
- Output validation ensures data integrity
- Cross-platform path handling prevents issues
