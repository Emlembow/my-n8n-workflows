# Data Table Schemas

This workflow requires two n8n data tables to be created in your n8n instance.

## 1. Training Data Table

**Purpose**: Stores historical training activities from Strava for analysis and coaching feedback.

**Table Name**: `Training` (or your preferred name)

**Columns**:

| Column Name | Type | Required | Description |
|------------|------|----------|-------------|
| `datetime` | DateTime | No | Date and time of the activity (from Strava) |
| `type` | String | No | Activity type (Run, Bike, Swim, etc.) |
| `sport_type` | String | No | Detailed sport type from Strava |
| `distance_miles` | Number | No | Distance covered in miles |
| `duration_minutes` | Number | No | Moving time in minutes |
| `pace_min_per_mile` | String | No | Pace in minutes per mile (format: "M:SS") |
| `calories` | Number | No | Estimated calories burned |
| `suffer_score` | Number | No | Strava suffer score |
| `average_heartrate` | Number | No | Average heart rate during activity |
| `max_heartrate` | Number | No | Maximum heart rate during activity |

**Notes**:
- This table is populated automatically by the workflow when new Strava activities are detected
- The workflow checks for duplicates using the `datetime` field before inserting
- Historical data from the last 90 days is used for AI coaching analysis

---

## 2. Training Plan Data Table

**Purpose**: Stores the AI-generated weekly training plan with scheduled workouts.

**Table Name**: `Training Plan` (or your preferred name)

**Columns**:

| Column Name | Type | Required | Description |
|------------|------|----------|-------------|
| `date` | DateTime | No | Date of the planned workout |
| `activity_type` | String | No | Type of workout (Swim, Bike, Run, Rest, Strength) |
| `workout` | String | No | Detailed workout description or "REST" |
| `notes` | String | No | Coaching notes and execution guidance |

**Notes**:
- This table is populated weekly by the AI Tri Planner agent
- Each day's plan is broken down into separate rows by activity type
- The AI Coach agent reads this table to compare actual workouts against planned workouts

---

## Creating Data Tables in n8n

### Steps:

1. Log into your n8n instance
2. Navigate to **Data** > **Data Tables** in the left sidebar
3. Click **Create Data Table**
4. Name the table (e.g., "Training" or "Training Plan")
5. Add columns using the schema above:
   - Click **Add Column**
   - Enter the column name exactly as shown
   - Select the appropriate data type
   - All columns can be set to "Not Required" (optional)
6. Click **Save**
7. Copy the Data Table ID from the URL or table settings
8. Repeat for the second table

### Getting Data Table IDs:

After creating each table:
1. Open the data table
2. Look at the URL in your browser, it will contain the table ID
3. Example URL: `https://your-n8n.cloud/projects/PROJECT_ID/datatables/TABLE_ID`
4. Copy the `TABLE_ID` portion
5. You'll need these IDs when configuring the workflow nodes

---

## Usage in Workflow

The workflow references these tables in several nodes:

### Training Table used in:
- **Is this new?** - Checks if activity already exists
- **If not, add it** - Inserts new activity data
- **Load Training History** - Reads historical data for AI analysis
- **Get row(s) in Data table** - AI Coach reads recent activities

### Training Plan Table used in:
- **Add to Training Plan** - Stores generated weekly plan
- **Get row(s) in Data table1** - AI Coach reads planned workouts

After importing the template, you'll need to update all these nodes with your actual Data Table IDs.
