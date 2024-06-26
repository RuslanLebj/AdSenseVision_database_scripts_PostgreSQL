﻿## Database Structure Description

The project's database is designed to manage the broadcasting and analysing content through cameras and displays. It includes tables for storing information about cameras, screens, links between them, content, statistics, and broadcasting schedules.

### ER Diagram
![ER Diagram](documentation/ER_Diagram.JPG)

### Database Tables

#### `camera` - Cameras
- `id`: Auto-incremented unique identifier for the camera.
- `name`: Name or description of the camera location, which may include address, room, or camera number.
- `url_address`: Public IP or DNS address for accessing the camera.
- `connection_login`: Login credential for camera access.
- `connection_password`: Password for camera access.
- `location_address`: Location (address) where the camera is installed.

#### `screen` - Displays
- `id`: Auto-incremented unique identifier for the screen.
- `name`: Name or description of the screen location, which may include address, room, or screen number.
- `start_time`: Time when content broadcasting starts on this screen.
- `end_time`: Time when content broadcasting ends on this screen.
- `pause_time`: Time interval between video shows.
- `update_date`: Date when the content on the screen was last updated.

#### `camera_screen` - Camera to Screen Link
- `id`: Auto-incremented unique identifier for the link.
- `camera_id`: References the `id` of a camera.
- `screen_id`: References the `id` of a screen.

#### `media_content` - Broadcasted Content
- `id`: Auto-incremented unique identifier for the content.
- `video`: File path of the video in the file system.
- `name`: Name of the content.
- `description`: Description of the content.
- `upload_date`: Date the video was uploaded.
- `duration`: Duration of the video.
- `preview`: Path to the video's preview image in the file system.

#### `statistics` - General Content Showing Statistics
- `id`: Auto-incremented unique identifier for the statistics entry.
- `media_content_id`: References the broadcasted content `id`.
- `screen_id`: References the screen where the content was broadcast.
- `total_viewing_time`: Total viewing time of the content.
- `max_viewers_count`: Maximum number of viewers at any given moment.
- `show_count`: Number of times the content was shown.

#### `schedule` - Content Showing Schedule
- `id`: Auto-incremented unique identifier for the schedule entry.
- `queue_number`: Sequence number of the content in the broadcasting queue.
- `media_content_id`: References the content to be broadcast.
- `screen_id`: References the screen broadcasting the content.

#### `statistics_per_show` - Statistics for Each Content Show
- `id`: Auto-incremented unique identifier for the show statistics.
- `media_content_id`: References the content for which statistics are recorded.
- `screen_id`: References the screen that showed the content.
- `viewing_time`: Viewing time for the content show.
- `viewers_count`: Number of viewers during the content show.

### Key Features

- All tables utilize `SERIAL` for primary keys, ensuring unique, automatically incremented IDs.
- Foreign keys are used extensively to maintain relational integrity between tables.
- String fields vary in length, accommodating different types of information from 50 to 360 characters.
