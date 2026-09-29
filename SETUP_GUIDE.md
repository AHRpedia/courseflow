# Courseflow GitHub Actions Setup Guide

## Current Status

✅ Repository created: https://github.com/AHRpedia/courseflow
✅ Files uploaded:
  - package.json
  - electron-builder.yml
  - .gitignore
  - README.md (auto-generated)

⚠️ Still needed:
  - `.github/workflows/build.yml` (permission issue, add manually)
  - Courseflow source code
  - assets/icon.ico
  - All config files (tsconfig.json, vite.config.ts, etc.)

## Manual Steps

### Step 1: Add GitHub Actions Workflow

Since automated workflow upload failed due to permissions, add manually:

1. On GitHub, click "Add file" → "Create new file"
2. File path: `.github/workflows/build.yml`
3. Paste content from `build-workflow.txt` in output folder
4. Commit with message: "Add GitHub Actions workflow"

### Step 2: Add Courseflow Source Code

1. Clone the repository:
   ```bash
   git clone https://github.com/AHRpedia/courseflow.git
   cd courseflow
   ```

2. Copy your Courseflow source into:
   ```
   courseflow/
   ├── src/
   │   ├── main/
   │   ├── renderer/
   │   └── engine/
   ├── tests/
   ├── tsconfig.json
   ├── vite.config.ts
   ├── vitest.config.ts
   └── tailwind.config.js
   ```

3. Add application icon:
   ```
   courseflow/assets/icon.ico  (256x256 or larger)
   ```

4. Push changes:
   ```bash
   git add .
   git commit -m "Add Courseflow source code"
   git push origin main
   ```

### Step 3: Verify Workflow

1. Go to Repository → Actions tab
2. You should see "Build Courseflow Windows Executables"
3. Workflow should trigger automatically after push

### Step 4: Download Built Executables

**Option A - Artifacts (recommended for testing):**
- Actions tab → Latest workflow run
- Download "Courseflow-Setup" artifact
- Contains Setup.exe and Portable.exe

**Option B - Releases (for distribution):**
```bash
# Create a release tag
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```
GitHub Actions will automatically create a Release with .exe files

## Build Workflow Steps

Once workflow is added, it will:

1. Checkout code
2. Setup Node.js 22.x
3. Install dependencies (npm ci)
4. Build React UI (vite build)
5. Run tests (npm test)
6. Build NSIS installer (electron-builder)
7. Build Portable executable (electron-builder)
8. Upload artifacts or create Release

## Troubleshooting

### "Workflow not found"
- Ensure `.github/workflows/build.yml` file exists
- Check file path is exactly correct

### "npm install failed"
- Check package.json format
- Ensure all dependencies are valid npm packages

### "Missing assets/icon.ico"
- Icon must be .ico format (Windows icon)
- Minimum 256x256 pixels
- Place in `assets/` directory

### "Build failed on Windows runner"
- Check npm scripts in package.json
- Verify Electron version compatibility
- Check node_modules installation

## Repository Links

- Main repo: https://github.com/AHRpedia/courseflow
- Actions: https://github.com/AHRpedia/courseflow/actions
- Releases: https://github.com/AHRpedia/courseflow/releases
- Settings: https://github.com/AHRpedia/courseflow/settings/actions

## Next Steps

1. ✅ Repository created
2. ⏳ Add .github/workflows/build.yml manually
3. ⏳ Add Courseflow source code
4. ⏳ Add assets/icon.ico
5. ⏳ Push to trigger workflow
6. ⏳ Download .exe from artifacts

---

**Setup date**: 29 September 2026
**Status**: Partially automated (workflow needs manual addition)
