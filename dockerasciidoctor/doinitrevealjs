#!/bin/bash
#  update: 2025-03-16

REPO_URL="https://github.com/hakimel/reveal.js.git"
ZIP_URL="https://github.com/hakimel/reveal.js/archive/master.zip"
CLONE_DIR="reveal.js"
ZIP_FILE="master.zip"
TEMP_DIR="reveal.js-master"

# Determine installation mode
MODE="$1"

# Function to extract version from package.json
extract_version() {
  PACKAGE_FILE="$CLONE_DIR/package.json"
  if [ -f "$PACKAGE_FILE" ]; then
    VERSION=$(grep '"version"' "$PACKAGE_FILE" | head -1 | sed -E 's/.*"version": *"([^"]+)".*/\1/')
    echo "Installed reveal.js version: $VERSION"
  else
    echo "Error: package.json not found in $CLONE_DIR."
    exit 1
  fi
}

# Basic installation (default or --basic)
if [ -z "$MODE" ] || [ "$MODE" == "--basic" ]; then
  echo "Performing basic installation..."
  curl -L -o "$ZIP_FILE" "$ZIP_URL"
  
  if [ $? -ne 0 ]; then
    echo "Error: Failed to download $ZIP_FILE"
    exit 1
  fi

  unzip "$ZIP_FILE"
  if [ $? -ne 0 ]; then
    echo "Error: Failed to unzip $ZIP_FILE"
    exit 1
  fi

  mv "$TEMP_DIR" "$CLONE_DIR"
  rm "$ZIP_FILE"
  echo "Basic installation completed."

# Full installation (--full)
elif [ "$MODE" == "--full" ]; then
  echo "Cloning reveal.js repository..."
  git clone "$REPO_URL"
  if [ $? -ne 0 ]; then
    echo "Error: Failed to clone the repository."
    exit 1
  fi
  echo "Full installation completed."

# Invalid argument
else
  echo "Usage: $0 [--basic|--full]"
  exit 1
fi

# Check if reveal.js directory exists
if [ -d "$CLONE_DIR" ]; then
  extract_version
else
  echo "Error: Directory '$CLONE_DIR' does not exist."
  exit 1
fi

