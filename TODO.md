# Documentation Fix Plan

## Problem
Perception and Version Control sections are not clickable/empty in the docs navigation.

## Root Causes
- `perception/` and `versionControl/` directories are missing `index.md` files (required by `navigation.indexes`)
- `perception/camera/`, `versionControl/linux_/`, `versionControl/windows_/` contain no markdown files at all
- `perception/image_processing/.pages` has `index.md` at the end instead of beginning

## Tasks
- [x] 1. Create `md-pages/perception/index.md`
- [x] 2. Create `md-pages/versionControl/index.md`
- [x] 3. Update `md-pages/perception/.pages` to add `index.md`
- [x] 4. Update `md-pages/versionControl/.pages` to add `index.md`
- [x] 5. Create `md-pages/perception/camera/index.md`
- [x] 6. Update `md-pages/perception/camera/.pages` to add `index.md`
- [x] 7. Create `md-pages/versionControl/linux_/index.md`
- [x] 8. Update `md-pages/versionControl/linux_/.pages` to add `index.md`
- [x] 9. Create `md-pages/versionControl/windows_/index.md`
- [x] 10. Update `md-pages/versionControl/windows_/.pages` to add `index.md`
- [x] 11. Fix `md-pages/perception/image_processing/.pages` - move `index.md` to top

