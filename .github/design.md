# LYX Window Spy - Comprehensive Design Document

## 🎯 Project Overview

LYX Window Spy is a revolutionary dual-window desktop application designed from the ground up for universal window analysis and coordinate tracking. This completely independent application provides comprehensive window spying capabilities with precision coordinate tracking and advanced screenshot-based data collection tools.

### LYX Unique Value Proposition

LYX Window Spy stands apart as a completely independent solution that prioritizes:

- **Universal Compatibility** - Works seamlessly across all Windows applications and environments
- **Precision First** - Sub-pixel accuracy in coordinate tracking and measurement
- **User-Centric Design** - Intuitive interface that doesn't require extensive training
- **Performance Optimized** - Minimal system impact while maximizing functionality
- **Extensible Architecture** - Built with future enhancements and customization in mind

### Core Philosophy

- **KISS** - Keep It Simple Stupid: Manual selection beats unreliable detection
- **DRY** - Don't Repeat Yourself: Extract common automation patterns to shared utilities
- **Workflow** - Make it Work, Make it Right, Make it Fast: Focus on function before form
- **Clean Functional Design** - Function before form until application works correctly
- **Virtual Environment First** - Everything needed is in the virtual environment, no global installs
- **Universal Design** - Built to work across all Windows environments and applications

## 🏗️ Application Architecture

### High-Level Architecture

```text
┌─────────────────────────────────────────────────────────────┐
│                      LYX Window Spy                         │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────┐         ┌─────────────────────────────┐ │
│  │   Tracker GUI   │ ──────▶ │    Screenshot GUI           │ │
│  │                 │         │                             │ │
│  │ • Window Spy    │         │ • Capture Tools             │ │
│  │ • Mouse Track   │         │ • Analysis Tools            │ │
│  │ • Hotkey Copy   │         │ • Data Collection           │ │
│  │ • Settings      │         │ • Export Features           │ │
│  └─────────────────┘         └─────────────────────────────┘ │
├─────────────────────────────────────────────────────────────┤
│                     Shared Utilities                        │
│  • Coordinate System  • Hotkey Manager  • Config Manager   │
│  • Screen Capture     • Window Utils    • Data Export      │
└─────────────────────────────────────────────────────────────┘
```

## 🖥️ GUI Component Specifications

### 1. Tracker GUI (Primary Window)

#### Core Features

- **LYX Advanced Window Spy**
  - Real-time window detection with sub-millisecond updates                         # 👎 How can we have sub-millisecond updates?
  - Deep window hierarchy visualization with parent-child relationships             # 👎 I don't even know what this means.
  - Comprehensive process and application metadata extraction                       # ⁉️ What kind of metadata?
  - Dynamic window state monitoring (minimized, maximized, focus states)
  - Memory usage and performance metrics display                                    # 📌 Cool idea.  I didn't think of this one!

- **LYX Precision Mouse Tracking**
  - Multi-coordinate system display (screen, window, client coordinates)            # ⚙️ More like application-specific
  - Sub-pixel coordinate precision with floating-point accuracy
  - Configurable coordinate reference systems and transformations                   # ⚙️ This is kind of like the first point in this section
  - Optional visual crosshair with customizable appearance                          # 👎 Not for the tracking gui (that's for screenshot gui)
  - Real-time distance, angle, and geometric measurements                           # 👎 Not for the tracking gui (that's for screenshot gui)

- **LYX Smart Hotkey System**
  - Context-aware hotkey combinations with conflict detection
  - Instant coordinate copying with format auto-detection
  - Multiple coordinate format support (CSV, JSON, XML, custom)
  - Smart clipboard integration with format preservation
  - Audio/visual feedback on capture                                                # ⚙️ Audio, maybe. Not a fan of audio feedback

- **Settings Panel**
  - Hotkey configuration
  - Display preferences
  - Coordinate format settings
  - Always-on-top toggle
  - Transparency settings

#### UI Layout Design

```text
┌─────────────────────────────────────────────────────────────┐
│ [File] [Settings] [Tools] [Help]                     [_][-][X]│
├─────────────────────────────────────────────────────────────┤
│ Target Window: [Current Window Name              ] [📷 Shot] │
├─────────────────────────────────────────────────────────────┤
│ ┌─ Mouse Coordinates ───────────────────────────────────────┐ │
│ │ Screen:    X: 1234  Y: 567                              │ │
│ │ Window:    X: 234   Y: 67                               │ │
│ │ Client:    X: 200   Y: 45                               │ │
│ │ [ ] Relative Mode    [Hotkey: Ctrl+Shift+C]             │ │
│ └─────────────────────────────────────────────────────────┘ │
│ ┌─ Window Information ──────────────────────────────────────┐ │
│ │ Class:     SomeWindowClass                              │ │
│ │ Handle:    0x12345678                                   │ │
│ │ Process:   application.exe (PID: 1234)                  │ │
│ │ Size:      1024 x 768                                   │ │
│ │ Position:  100, 50                                      │ │
│ └─────────────────────────────────────────────────────────┘ │
│ ┌─ Quick Actions ───────────────────────────────────────────┐ │
│ │ [Copy Coords] [Save Target] [Pin Window] [Screenshot]    │ │
│ └─────────────────────────────────────────────────────────┘ │
│ Status: Ready | Last Copy: 12:34:56                         │
└─────────────────────────────────────────────────────────────┘
```

### 2. Screenshot GUI (Secondary Window)

#### Screenshot Features

- **Capture Modes**
  - Full screen capture
  - Window-specific capture
  - Region selection capture
  - Timed captures

- **Analysis Tools**
  - Pixel color picker
  - Ruler/measurement tools
  - Grid overlay
  - Magnification lens

- **Data Collection Tools**
  - Coordinate annotation
  - Color palette extraction
  - Text recognition (OCR)
  - Element detection hints

- **Export Features**
  - Multiple image formats
  - Coordinate data export
  - Annotation export
  - Batch processing

#### Screenshot UI Layout

```text
┌─────────────────────────────────────────────────────────────┐
│ [File] [Capture] [Tools] [Export]                    [_][-][X]│
├─────────────────────────────────────────────────────────────┤
│ [📷 Capture] [🎯 Region] [⏰ Timer] [🔍 Analyze]              │
├─────────────────────────────────────────────────────────────┤
│ ┌─ Preview ─────────────────────┐ ┌─ Tools ───────────────┐ │
│ │                               │ │ [🎨 Color Picker]    │ │
│ │                               │ │ [📏 Ruler]           │ │
│ │       Screenshot              │ │ [📝 Annotate]        │ │
│ │       Display Area            │ │ [🔍 Magnify]         │ │
│ │                               │ │ [📊 OCR]             │ │
│ │                               │ │ [⚡ Quick Copy]      │ │
│ └───────────────────────────────┘ └───────────────────────┘ │
│ ┌─ Coordinates & Data ──────────────────────────────────────┐ │
│ │ Cursor: (1234, 567) | Color: #FF5733 | RGB(255,87,51)   │ │
│ │ Selection: 100x75 @ (200,300)                           │ │
│ └─────────────────────────────────────────────────────────┘ │
│ [Save] [Copy] [Export Data] [Back to Tracker]               │
└─────────────────────────────────────────────────────────────┘
```

## 🔧 Technical Specifications

### LYX Technical Innovations

LYX Window Spy incorporates several groundbreaking technical innovations that set it apart as a completely independent solution:

- **LYX Coordinate Engine** - Proprietary coordinate system with sub-pixel precision and multi-reference frame support
- **LYX Window Inspector** - Advanced window detection algorithms with deep system integration
- **LYX Smart Capture** - Intelligent screenshot system with context-aware optimization
- **LYX Universal Compatibility Layer** - Ensures consistent behavior across all Windows versions and applications
- **LYX Performance Optimizer** - Custom memory management and CPU optimization for minimal system impact

### Technology Stack

- **Framework**: Python with tkinter/PyQt6 for GUI
- **Screen Capture**: PIL (Pillow) + platform-specific APIs
- **Hotkeys**: pynput or keyboard library
- **Window Management**: pywin32 (Windows-specific)
- **Image Processing**: OpenCV (optional for advanced features)
- **Data Export**: JSON, CSV, XML support

### Core Modules

#### 1. Window Management (`window_manager.py`)

```python
class WindowManager:
    """Handles window detection, tracking, and property extraction"""
    - get_window_at_cursor()
    - get_window_properties()
    - track_window_changes()
    - get_window_hierarchy()
```

#### 2. Coordinate System (`coordinate_system.py`)

```python
class CoordinateTracker:
    """Manages different coordinate systems and conversions"""
    - get_screen_coordinates()
    - get_window_coordinates()
    - get_client_coordinates()
    - convert_coordinates()
```

#### 3. Hotkey Manager (`hotkey_manager.py`)

```python
class HotkeyManager:
    """Global hotkey registration and handling"""
    - register_hotkey()
    - unregister_hotkey()
    - handle_hotkey_event()
```

#### 4. Screen Capture (`screen_capture.py`)

```python
class ScreenCapture:
    """Screenshot functionality with various modes"""
    - capture_screen()
    - capture_window()
    - capture_region()
    - capture_with_timer()
```

#### 5. Configuration Manager (`config_manager.py`)

```python
class ConfigManager:
    """Settings persistence and management"""
    - load_settings()
    - save_settings()
    - get_default_settings()
    - validate_settings()
```

### Data Models

#### Settings Configuration

```python
@dataclass
class AppSettings:
    hotkey_combination: str = "ctrl+shift+c"
    coordinate_format: str = "x,y"
    always_on_top: bool = False
    transparency: float = 1.0
    auto_copy: bool = True
    show_crosshair: bool = False
    default_capture_format: str = "png"
```

#### Coordinate Data

```python
@dataclass
class CoordinateData:
    screen_x: int
    screen_y: int
    window_x: int
    window_y: int
    client_x: int
    client_y: int
    timestamp: datetime
    window_handle: int
    window_title: str
```

## 🚀 LYX User Workflows

### LYX Primary Workflow: Precision Coordinate Tracking

1. **Launch LYX Window Spy** → Instant startup with Tracker GUI
2. **Smart Configuration** → Auto-detected optimal hotkey suggestions
3. **Universal Target** → Hover over any Windows application
4. **Real-time Precision** → Sub-pixel coordinate display with multi-reference frames
5. **Instant Capture** → Press hotkey for immediate coordinate copying
6. **Universal Integration** → Paste into any automation framework or script

### LYX Secondary Workflow: Advanced Screenshot Analysis

1. **One-Click Screenshot** → Seamless transition from Tracker to Screenshot GUI
2. **Intelligent Capture** → Auto-optimized capture mode selection
3. **Precision Screenshot** → Context-aware image capture with metadata
4. **Advanced Analysis** → LYX analysis tools with pixel-perfect accuracy
5. **Smart Data Extraction** → Automated coordinate, color, and text recognition
6. **Universal Export** → Multi-format export with automation-ready data structures

## 📋 Feature Roadmap

### Phase 1: Core Functionality (MVP)

- [ ] Basic Tracker GUI with mouse coordinate display
- [ ] Simple hotkey system for coordinate copying
- [ ] Basic window detection and information display
- [ ] Simple screenshot capture functionality
- [ ] Configuration file support

### Phase 2: Enhanced Features

- [ ] Advanced coordinate system options
- [ ] Screenshot GUI with analysis tools
- [ ] Multiple hotkey configurations
- [ ] Data export capabilities
- [ ] Always-on-top and transparency options

### Phase 3: Advanced Tools

- [ ] OCR text recognition
- [ ] Color palette extraction
- [ ] Automated element detection
- [ ] Batch processing capabilities
- [ ] Plugin system for extensions

### Phase 4: Polish & Optimization

- [ ] Performance optimizations
- [ ] UI/UX improvements
- [ ] Comprehensive documentation
- [ ] Installer creation
- [ ] Update system

## 🔒 Security & Performance Considerations

### Security

- Minimal system permissions required
- No network communication by default
- Local data storage only
- Secure hotkey handling to prevent conflicts

### Performance

- Efficient screen capture algorithms
- Minimal CPU usage during idle state
- Optimized memory usage for large screenshots
- Responsive UI with background processing

## 📖 User Documentation Strategy

### Documentation Structure

1. **Quick Start Guide** - Get running in 5 minutes
2. **User Manual** - Comprehensive feature documentation
3. **Automation Examples** - Sample use cases and scripts
4. **Troubleshooting Guide** - Common issues and solutions
5. **API Reference** - For advanced users and integrations

## 🎯 Success Metrics

### Functional Metrics

- Coordinate accuracy: ±1 pixel precision
- Hotkey response time: < 100ms
- Screenshot capture time: < 500ms for full screen
- Memory usage: < 50MB during normal operation

### User Experience Metrics

- Application startup time: < 3 seconds
- UI responsiveness: < 16ms frame time
- Configuration simplicity: < 2 minutes to setup
- Documentation clarity: Self-explanatory for 80% of features

---

*This design document serves as the foundation for LYX Window Spy development. This completely independent application has been designed from the ground up to be universal and will be iteratively updated as requirements evolve and implementation details are refined.*
