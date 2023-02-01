# Antennas

The Antennas display allows the antennas database to be searched and updated so that an appropriate antenna will always be available to use in coverage predictions. 

# Antenna Search

The parameters of the search are defined in the three tabs (Performance, Details, Extra) of the Search panel. Each parameter may be excluded by unchecking the checkbox on the left side.  

## Performance

* **Frequency** Define a frequency range in which the antenna operates. Select MHz or Ghz as required. Antennas are defined by an operating range (upper and lower frequency), although some antennas are only defined by a single (midpoint) frequency, in which case this frequency will be recorded as the upper and lower ends of its range. In any case, the search range will match an antenna if it overlaps any of the the antennas operating range. 
* **Gain** The gain (dBi) of the antenna.
* **Azimuth** The 3dB azimuth beamwidth of the antenna. That is, the azimuth angle from the peak gain where the gain reduces by a half (3dB). 
* **Elevation** The 3dB elevation (vertical) beamwidth of the antenna. That is, the elevation angle from the peak gain where the gain reduces by a half (3dB).
* **Front to Back Ratio** The ratio of power gain between the front (maximum gain) and rear of the antenna. 

<div style="text-align:center"><img src="/_media/antenna_search.png" /></div>

## Details

* **Manufacturer** Partial name of the antenna manufacturer to match.
* **Model Number** Partial name of the antenna model to match.
* **Description** Partial description of the antenna to match.

<div style="text-align:center"><img src="/_media/antenna_details.png" /></div>

## Extra

* **Search scope** The search may be limited to only antennas that have been created by the user (own antennas).
* **Find single antenna by ID** A single antenna can be found be entering its ID eg. baaba3b9-9ee9-4950-95ca-146cdcca5876

<div style="text-align:center"><img src="/_media/antenna_extra.png" /></div>

# Search Results
 
The search results will update as changes are made to the search parameters. The total number of matches is shown as "Search Matches". Up to 400 results will be shown in the search results table. The results can be sorted by any column - click the column name, an arrow will show the sort direction.

<div style="text-align:center"><img src="/_media/antenna_search_results.png" /></div>

Selecting a row will display its pattern (see below) and also provides an option to use that antenna in the current coverage. Clicking on the button will insert the antenna into the coverage panel on the map. This will replace whatever antenna is currently being shown, and if a coverage prediction is selected will cause that coverage to be re-predicted with the newly selected antenna.

<div style="text-align:center"><img src="/_media/antenna_use_result.png" /></div>

# Patterns

The horizontal and vertical radiation patterns of the antenna selected in the search results are displayed. The scale of the polar plots can be kept at a standard setting, which allows for easier comparison when selecting multiple antennas in succession. Alternatively, a custom scale will adjust the range to the values of each antenna.

<div style="text-align:center"><img src="/_media/antenna_patterns.png" /></div>

# Management

## Favorite Antennas

Favorite antennas provide fast access to antennas that are used frequently. When an antenna is selected in the search results panel, it is also shown as an option to **Add**, with a suggested name, which can be overridden. Pressing the "plus" icon on the left adds the antenna to favorites.

Once added, antennas can be selected from the pulldown lists of **Remove** and **Display** and action performed accordingly by pressing the corresponding button on the left. 

<div style="text-align:center"><img src="/_media/antenna_favorites.png" /></div>

## Own Antennas

### Manage

The Twinkler antenna database can be supplemented by adding more antennas, which are only available to the user (and optionally their organisation). Once an antenna is created (see below) it can be selected from the pulldown lists of **Delete** and **Display** and action performed accordingly by pressing the corresponding button on the left. 

<div style="text-align:center"><img src="/_media/antenna_own.png" /></div>

### Create/Edit an antenna

To **Create** or **Edit** an antenna, press the corresponding button on the *Own Antennas* panel to show the *Antenna Creation* dialog. In this dialog, the parameters corresponding to those of the Search panel can be entered (frequencies, gain etc).

Additionally, the Horizontal Pattern and Vertical Pattern have to be entered. These are a list of 360 numbers corresponding to gain (relative to the antenna Gain value entered above) from 0 to 359 degrees. The numbers are separated by whitespace. The numbers start at the horizontal position, aligned with the peak gain and move clockwise for the horizontal pattern, and downards for the vertical pattern. That is, the numbers follow the same conventions as seen on the antennas pattern plots (above).

The **Load...** button allows ADF and PLA (Planet) antenna files to loaded. The files are read and their values  placed into the antenna dialog, where they can be reviewed/edited and used to create an antenna.

<div style="text-align:center"><img src="/_media/antenna_create.png" /></div>
