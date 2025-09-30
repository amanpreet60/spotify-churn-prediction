# Assignment Questions

## 1. Dataset Sourcing

The dataset was obtained from the **Open Government Portal**, which provides public access to open data and information to enhance transparency. Here are the following filtering options used to source the data:

**Portal Type:** Open Data,  **Collection Type:** Open Maps,  **Resource Type:** Dataset,  **Format:** GeoTIFF, TIFF  

These filters ensured that the dataset selected was spatial in nature, compatible with geospatial analysis tools, and available in raster formats commonly used for environmental and spatial research. The dataset I selected contains vessel density information (like vessel tracks per day for cargo vessels, 2023) derived from **Automatic Identification System (AIS)** data. The data is provided in GeoTIFF format and captures the spatial distribution and intensity of vessel traffic across the Northwest Atlantic region. The dataset is large in size (over 4 million rows when extracted), reflecting the high temporal and spatial resolution of vessel tracking data.

## 2. Application Description
I am exploring the spatial distribution of vehicle density across different vessel types (Passenger, Cargo, Fishing, Tanker, Other) using raster-based data. This application is significant because vessel density analysis helps improve maritime safety by identifying high-traffic routes prone to accidents, assesses environmental impact by revealing regions under pressure from fishing or tanker activity, and supports climate and policy studies by showing how trade, tourism, and regulations influence marine traffic patterns.

## 3. Data Transformation and Preprocessing
To preprocess the AIS raster dataset, I automated the conversion of raw .tif vessel density files into structured DataFrames organized by vessel type and year. Each raster was read with rasterio, and nodata values (representing land or missing regions) were replaced with NaN. The grid was reshaped into a tidy format with row, column, and density values, after which I computed the cell-center coordinates and transformed them from the raster’s CRS into geographic longitude and latitude using pyproj. Each record was then annotated with its corresponding vessel type and year, parsed from the filename.

## 4. Single-variable Analysis
**Variable Selected:** Vessel density

**Research Question:** “Does the distribution of vessel density suggest that ships follow fixed routes, or is vessel traffic spread randomly across the ocean?”

The histogram of total vessel density shows that most grid cells in the Northwest Atlantic have near-zero traffic, while a small fraction exhibit extremely high vessel densities. This highly skewed distribution indicates that vessel traffic is not random but instead concentrated along fixed maritime routes. If ship movements were random, we would expect vessel density to be more evenly spread across the study area. Instead, the presence of a long right tail in the distribution suggests repeated use of specific shipping lanes, port approaches, and fishing grounds. Thus, the data provide strong evidence that vessels follow structured and predictable routes rather than dispersing randomly across the ocean.

## 5. Multi-variable Analysis
**Variable Selected:** Vessel density and vessel type across spatial regions

**Research Question:** *How has the vessel density varied across different vessel types, and where are the densest regions for each type?*  

The spatial patterns of vessel density in 2023 reveal clear differences between cargo and fishing activity. Cargo vessel traffic is concentrated along fixed trans-Atlantic shipping lanes and approaches to major ports such as Halifax, Boston, and New York, resulting in narrow, high-density corridors. By contrast, fishing vessels display a more diffuse but localized pattern, with hotspots on the continental shelf, particularly around Georges Bank, the Gulf of Maine, and coastal Newfoundland. These differences highlight how cargo density reflects long-distance trade routes and predictable maritime corridors, whereas fishing density is shaped by localized access to productive fishing grounds.

## 5. Shiny Webpage

An interactive page is available [here](https://40nng4-amanpreet-singh.shinyapps.io/vessel_density_patterns1/), created using the shiny.

The site provides two main modes of analysis. The first is a histogram view, which shows the full distribution of vessel density values and reveals whether traffic is concentrated along fixed routes or dispersed randomly across the ocean. The second is a raster comparison view, where users can select any two density maps and view them side by side to compare spatial patterns across vessel types. A dropdown menu allows switching between modes, making exploration flexible and intuitive.