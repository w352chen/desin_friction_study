# 🔒 Participant Data Isolation System

## Overview

This study system ensures **complete data isolation** between participants to prevent data contamination and ensure research integrity.

## How Data Isolation Works

### 🆔 Participant ID Entry

- **New Participant**: When a participant enters their ID, the system automatically clears ALL previous data
- **ID Change**: If someone changes the participant ID, they receive a warning and all data is cleared
- **Clean Slate**: Each participant starts with completely fresh data storage

### 📊 Data Storage

All participant data is stored locally in the browser's localStorage with the following categories:

#### Participant Information

- `participant_id` - Unique participant identifier
- `participant_start_time` - Session start timestamp

#### Task Performance Data (12 tasks)

- `[task_name]_start_time` - Task start timestamp
- `[task_name]_end_time` - Task completion timestamp
- `[task_name]_duration_seconds` - Task duration in seconds
- `[task_name]_rating` - Success rating (1-5 scale)

#### NASA-TLX Workload Assessment

- `nasa_tlx_mental_demand` - Mental demand rating (1-10)
- `nasa_tlx_physical_demand` - Physical demand rating (1-10)
- `nasa_tlx_temporal_demand` - Time pressure rating (1-10)
- `nasa_tlx_performance` - Performance rating (1-10)
- `nasa_tlx_effort` - Effort rating (1-10)
- `nasa_tlx_frustration` - Frustration rating (1-10)
- `nasa_tlx_overall_workload` - Calculated average score

### 🛡️ Data Protection Mechanisms

#### 1. Automatic Data Clearing

When a new participant ID is entered:

- System clears 47 different data keys
- Previous participant data is completely removed
- New session starts with clean state

#### 2. Change Protection

When attempting to change participant ID:

- System warns about data loss
- Requires confirmation if data exists
- Prevents accidental data mixing

#### 3. Download Validation

Before each CSV/JSON export:

- Console logs current participant ID
- Verifies data isolation
- Confirms export contains only current participant data

## 📁 CSV Export Structure

Each CSV file contains the following columns:

```csv
Participant ID,Participant Start Time,Task Name,Task Key,Start Time,End Time,Duration (Seconds),Duration (Minutes),Success Rating,Is Complete,NASA-TLX Mental Demand,NASA-TLX Physical Demand,NASA-TLX Temporal Demand,NASA-TLX Performance,NASA-TLX Effort,NASA-TLX Frustration,NASA-TLX Overall Workload
```

### Example CSV Row:

```csv
P001,2024-01-15T10:00:00.000Z,Task 1,task1,2024-01-15T10:30:00.000Z,2024-01-15T10:35:00.000Z,300,5,4,true,7,3,5,8,6,4,5.5
```

## 🎯 For Researchers

### Best Practices

1. **Unique IDs**: Assign unique participant IDs (P001, P002, etc.)
2. **Fresh Sessions**: Each participant should start from index.html
3. **Immediate Download**: Participants download their own CSV files
4. **Data Verification**: Check console logs for data isolation confirmation

### Data Collection Workflow

1. Participant visits `index.html`
2. Enters unique participant ID → **Previous data cleared**
3. Completes study tasks → **Individual data recorded**
4. Fills NASA-TLX assessment → **Workload data captured**
5. Downloads CSV file → **Only their data exported**
6. Proceeds to final questionnaire

### Manual Data Clearing

Researchers can manually clear data using:

- **Survey Results Page**: "Clear All Data" button
- **Browser Console**: Access to clearing functions
- **Index Page**: Change participant ID (with warning)

## 🔍 Verification Methods

### Console Logging

Every data operation logs to browser console:

```javascript
// Participant session start
"New participant session started: P001";
"All previous data cleared for clean session";

// Data download
"📥 Downloading CSV for participant: P001";
"🔒 Data isolation verified - CSV contains ONLY data for participant: P001";
```

### Visual Confirmations

- Participant ID displayed prominently in all interfaces
- CSV filenames include participant ID: `study_data_P001_2024-01-15.csv`
- Warning messages for data changes
- Confirmation dialogs for clearing operations

## 🚨 Important Notes

- **Single Browser Session**: Data isolation works within browser localStorage
- **Private/Incognito Mode**: Recommended for each new participant
- **Data Persistence**: Data persists until manually cleared or new participant starts
- **No Cross-Contamination**: Impossible for one participant's data to appear in another's CSV

## Technical Implementation

The system uses a comprehensive key-based clearing mechanism:

- Maintains list of all possible data storage keys
- Clears 47 different localStorage keys when needed
- Validates data isolation before every export
- Provides multiple confirmation layers for data safety

This ensures complete data integrity and participant privacy throughout the study process.
