# Frontend - Its Me Event ([GreatAIHackathon](https://greataihackathon.com/))

A real-time crowd monitoring dashboard built with React and Vite that visualizes venue occupancy, attendance trends, and risk assessments for event management.

## Overview

This dashboard provides event managers with a comprehensive view of crowd density across multiple venue zones, featuring live predictions, historical trends, and automated risk detection.

## Features

- **Live Attendance Tracking**: Real-time crowd density monitoring across 5 venue zones
- **Predictive Analytics**: Displays ML-based crowd predictions vs actual data
- **Risk Assessment**: Automated rule-based risk detection with actionable recommendations
- **Weather Integration**: Shows current temperature, conditions, and wind speed
- **Interactive Charts**: Click on venues to view detailed attendance trends
- **Responsive Design**: Dark-themed modern UI

## Tech Stack

- **React 19** - UI library
- **Vite 7** - Build tool and dev server
- **Recharts** - Charting library for data visualization
- **react-circular-progressbar** - Circular progress indicators

## Getting Started

### Prerequisites

- Node.js 18+
- npm or yarn

### Installation

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

### Environment

The dashboard connects to the prediction API at:

```
https://jhtl8la4ik.execute-api.ap-southeast-1.amazonaws.com/dev
```

## Project Structure

```
Frontend/
├── src/
│   ├── App.jsx           # Main application component
│   ├── main.jsx          # Entry point
│   ├── components/       # Reusable UI components
│   │   ├── AttendanceCard.jsx   # Live attendance display
│   │   ├── ChartCard.jsx        # Trend visualization
│   │   ├── RisksCard.jsx        # Risk recommendations
│   │   └── VenueRow.jsx         # Venue occupancy cards
│   └── utils/
│       └── color.js      # Color utility functions
├── public/
│   ├── data.json         # Static data fallback
│   └── output.json       # Static output fallback
└── ml/
    └── ml.md             # ML training documentation
```

## Components

| Component        | Description                                            |
| ---------------- | ------------------------------------------------------ |
| `AttendanceCard` | Displays total attendance with progress bar            |
| `ChartCard`      | Line chart comparing actual vs predicted crowd data    |
| `RisksCard`      | Lists detected risks with severity and recommendations |
| `VenueRow`       | Grid of venue cards with circular progress indicators  |

## Risk Detection Rules

The dashboard automatically detects:

- **Overcapacity** (≥98% utilization) - Critical
- **Near Capacity** (≥90%) - High priority
- **Rising Load** (≥75%) - Moderate concern
- **Rapid Inflow** - Accelerating crowd growth
- **Above Forecast** - Actual exceeds predicted by 15%+
- **Forecast Surge** - Predicted high density within 30 minutes
- **Load Imbalance** - Uneven distribution across venues

## Scripts

| Command           | Description              |
| ----------------- | ------------------------ |
| `npm run dev`     | Start development server |
| `npm run build`   | Build for production     |
| `npm run preview` | Preview production build |
| `npm run lint`    | Run ESLint               |

## License

Part of the Team Sental project for ItsMeEvent
