FAIRLTER Air Filter Web System

FAIRLTER is a student web prototype for viewing and managing air-filter bin locations and their sensor information. The site provides a bin dashboard, sensor-reading history, charts, a map view, and a contact form.

## Features

- View active bins and search by bin identifier
- Add bins, update bin details, and mark bins as deleted
- View deleted bins and recover them
- Add, edit, and remove sensors associated with a bin
- Record sensor readings and view recent readings in charts
- View bin locations on a map
- Submit a message through the contact form

The interface describes monitoring particulate matter (PM2.5/PM10), carbon monoxide (CO), carbon dioxide (CO2), and total volatile organic compounds (TVOC). The repository contains the web interface and PHP/MySQL backend; it does not include sensor firmware or an SQL schema.

## Built With

- HTML, CSS, and JavaScript
- PHP with MySQLi
- MySQL
- Chart.js for sensor charts
- Leaflet for the map

Chart.js and Leaflet are loaded from CDNs, so those features need an internet connection in the browser.

## Project Files

- `login.html` - main FAIRLTER web interface
- `script.js` - dashboard behavior and API requests
- `style.css` - page styling
- `index.php` - PHP JSON API for bins, sensors, readings, and contact messages
- `db_connect.php` - MySQL connection settings
- `failter.png`, `prototype.png`, `homepage.mp4` - included visual assets

## Requirements

- A local PHP development server such as XAMPP with Apache and MySQL
- PHP with the MySQLi extension enabled
- A MySQL database named `fairlter_db`, or update the database name in `db_connect.php`
- A compatible database schema for `bins`, `sensors`, `sensor_readings`, and `contact_messages`

> The ZIP does not include a `.sql` database setup file. The backend expects the tables above and their associated fields, so the database must be created and populated separately before the dashboard can load data.

## Local Setup

1. Copy the project folder into your local web server's document root (for example, `htdocs` in XAMPP).
2. Create a MySQL database named `fairlter_db` and import or create a schema compatible with the PHP queries. No schema file is included in this repository.
3. Open `db_connect.php` and set the host, database name, username, password, and port for your local MySQL setup. The current file uses `root` with a blank password for local development; change these values to match your environment.
4. In `script.js`, set `API_URL` to the location of the PHP endpoint. The current JavaScript points to `api/index.php`, but the supplied API file is at the project root as `index.php`. For the current file layout, change it to:

   ```js
   const API_URL = 'index.php';
   ```

5. Start Apache and MySQL.
6. Open the interface through the local web server, for example:

   ```text
   http://localhost/FAIRLTER-Air-Filter-Web-System/login.html
   ```

The PHP API must be served by Apache; opening `login.html` directly as a file will not run the backend.

## API Actions

The PHP endpoint accepts an `action` parameter for operations including:

- `get_bins`, `get_deleted_bins`, `get_bin_details`
- `add_bin`, `delete_bin`, `recover_bin`, `update_bin_detail`
- `add_sensor`, `delete_sensor`, `update_sensor_reading`
- `submit_contact`

Writes are sent as POST requests by the frontend. The API returns JSON responses.

## Notes

- The map uses a small hard-coded set of demo locations in Iligan City; add or update coordinates in `script.js` to match real deployment data.
- Sensor readings are stored when submitted to the API. No sensor-device ingestion service or hardware firmware is included in this repository.
- Use non-default database credentials and review the application security before deploying it publicly.
