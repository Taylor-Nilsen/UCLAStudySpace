# Scraping Guide

## Quick Start

### Basic Usage (scrape all classrooms with 4 workers)
```bash
python scrape.py
```

### Limit to first N classrooms
```bash
python scrape.py 50
```

### Customize number of parallel workers
```bash
python scrape.py 100 8
```

## Performance Improvements

### ⚡ Speed Optimizations:
1. **Multiprocessing**: Scrapes 4 rooms simultaneously by default (configurable)
2. **Reduced wait times**:
   - AJAX wait: 3 seconds (was 10)
   - Initial load: 8 seconds (was 20)
   - Calendar events: 5 seconds (was 15)
3. **No delays between requests** (parallel processing eliminates this need)
4. **Minimal logging** for faster execution

### 💾 Save Behavior:
- Saves every 20 completed rooms
- Final save at the end
- Progress preserved even if interrupted

### 📊 Expected Performance:

**For 1000+ classrooms:**
- **Old version (sequential)**: ~2-3 hours
- **New version (4 workers)**: ~30-45 minutes
- **New version (8 workers)**: ~15-25 minutes

**Note**: More workers = faster, but don't exceed your CPU cores (usually 4-8). Too many workers may cause rate limiting or system issues.

## Command Line Arguments

```bash
python scrape.py [limit] [workers]
```

- `limit` (optional): Number of classrooms to scrape (default: all)
- `workers` (optional): Number of parallel workers (default: 4)

## Examples

```bash
# Scrape first 10 classrooms with 2 workers (good for testing)
python scrape.py 10 2

# Scrape all classrooms with 8 workers (fast!)
python scrape.py 0 8

# Scrape first 500 classrooms with 6 workers
python scrape.py 500 6
```

## Recommendations

- **Testing**: Start with `python scrape.py 10 2` to test
- **Full run**: Use `python scrape.py 0 6` or `python scrape.py 0 8`
- **Conservative**: If worried about rate limiting, use 4 workers (default)
- **Maximum speed**: 8 workers (but watch system resources)
