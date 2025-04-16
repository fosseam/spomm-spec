# SpOMM – Core Structure Overview

### Overall Concept

SpOMM ("Sphere Object Meta Model") structures spherical observation objects into seven clearly separated main areas: three identifying attributes and four modular content blocks, aka JSON-Objects. This structure is designed for federation, transformation, curated collections, and semantic enrichment.

### Top-Level Attributes (simple values)

1. `number` – Local running ID within a dataset (auto-incremented)
2. `slug` – URL-friendly short name (human- and machine-readable)
3. `spommid` – Global unique UUID (for cross-dataset uniqueness)

### Top-Level Objects (structured blocks)

1. `base` – Metadata block with name, description, source, themes, timestamps
2. `location` – Geographic context: semantic (Wikidata) and cartographic (coordinates, map links)
3. `media` – Media objects (images, thumbnails, info links, embeds) with licensing and QA details
4. `camera` – Technical description of camera and viewing direction

### Short ASCII-Tree Catalog

```
SpOMM Object (Core Structure)
├── number                      Local auto-incremented ID within dataset
├── slug                        URL-friendly short name
├── spommid                     Globally unique UUID
├── base {}
│   ├── name {}                 Multilingual display title
│   │   ├── en                  Title in English
│   │   └── de                  Title in German
│   ├── description {}          Multilingual description
│   │   ├── en                  Description in English
│   │   └── de                  Description in German
│   ├── source {}               Source system and ID reference
│   │   ├── origin              System name (e.g. "google-sphere")
│   │   ├── id-desc             ID type (e.g. "panoid")
│   │   └── id                  Actual ID in source system
│   ├── theme []                Thematic tags (e.g. "nature", "event")
│   ├── added                   Timestamp when created (ISO 8601)
│   └── modified                Timestamp of last modification (optional)
├── location {}
│   ├── geo {}                  Semantic Wikidata-based references
│   │   ├── continent []        Continent [name, Wikidata QID]
│   │   ├── country []          Country [name, Wikidata QID]
│   │   ├── region []           Region/state [name, Wikidata QID]
│   │   ├── place []            Place [name, Wikidata QID]
│   │   └── tags []             Freeform location tags
│   ├── coordinates {}          Geographic coordinates and altitude
│   │   ├── longi               Longitude
│   │   ├── lati                Latitude
│   │   └── alti {}
│   │       ├── agl            Altitude above ground level
│   │       └── amsl           Altitude above mean sea level
│   └── map {}                  Map-related external links
│       ├── osm                OpenStreetMap URL
│       ├── osm_tags []        Relevant OSM tags or categories
│       ├── google             Google Maps link
│       ├── apple              Apple Maps link
│       └── ms                 Microsoft Maps link
├── media []                    List of media entries (image, info, embed)
│   └── (each) {}
│       ├── url                Direct media file or resource link
│       ├── meta {}            Metadata about the media file
│       │   ├── label          Descriptive media label
│       │   ├── type           Media type (e.g. "thumb", "highres")
│       │   ├── mime           MIME type (e.g. "image/jpeg")
│       │   ├── exif {}        EXIF metadata (if available)
│       │   ├── xmp {}         XMP metadata (creative info)
│       │   └── iptc {}        IPTC metadata (editorial info)
│       ├── usage {}           Rights and usage permissions
│       │   ├── license        License type (e.g. "CC-BY")
│       │   ├── contributor    Name of contributor or copyright holder
│       │   └── embedding      Reuse indicator ("allowed", "n/a", ...)
│       └── qa {}              Quality assurance info
│           ├── status         Media status
│           ├── added          Date media was added
│           └── checked        Last verification timestamp
├── camera {}                   Camera and viewing setup
│   ├── view {}                Field of view and projection
│   │   ├── angle              View angle in degrees
│   │   ├── resolution         Image/sphere resolution
│   │   └── projection         Projection type (e.g. "equirectangular")
│   ├── ptz {}                 Movement capabilities
│   │   ├── pan                Supports panning?
│   │   ├── tilt               Supports tilting?
│   │   └── zoom               Supports zoom?
│   ├── type                   Capture type (photo, video, lidar)
│   ├── indoor                 Indicates indoor scene
│   ├── audio                  Audio present?
│   ├── interval               Capture interval (e.g. "5s")
│   ├── timelapse              Part of a timelapse?
│   └── heading {}             Orientation angles
│       ├── direction          Compass direction (e.g. "NE")
│       ├── pitch              Vertical tilt (X-axis)
│       ├── yaw                Horizontal angle (Y-axis)
│       └── roll               Rotation around Z-axis

```





### `base`

The `base` object contains core metadata fields that describe the identity, context, and provenance of a sphere object.

- `name` {} – A multilingual object holding human-readable titles.
  - `en` – Title in English
  - `de` – Title in German
  - (extensible: `fr`, `es`, `nl`, ...)

- `description` {} – A multilingual object for narrative summaries.
  - `en` – Short description in English
  - `de` – Short description in German
  - (extensible as above)

- `source` {} – Defines where the sphere originates from and which identifier it carries.
  - `origin` – Source system (e.g. "google-sphere", "mapillary")
  - `id-desc` – Description of the identifier type (e.g. "panoid")
  - `id` – Concrete identifier used in the source system

- `theme` [] – A list of descriptive thematic tags (e.g. `nature`, `architecture`, `event`, ...)

- `added` – Timestamp when the object was first recorded (ISO 8601)

- `modified` – Timestamp of the last modification (optional, ISO 8601)

### `location`

The `location` object provides both semantic and cartographic information about the spatial context of the sphere.

- `geo` {} – Semantic location references linked to Wikidata.
  - `continent` [] – Name and Wikidata QID for the continent
  - `country` [] – Name and Wikidata QID for the country
  - `region` [] – Name and Wikidata QID for the region or state
  - `place` [] – Name and Wikidata QID for the specific place (e.g. island, city)
  - `tags` [] – Freeform tags to enrich the location context

- `coordinates` {} – Physical coordinates of the capture point.
  - `longi` – Longitude (East/West)
  - `lati` – Latitude (North/South)
  - `alti` {} – Altitude measurements
    - `agl` – Height above ground level
    - `amsl` – Height above mean sea level

- `map` {} – Optional links to mapping services
  - `osm` – OpenStreetMap URL
  - `osm_tags` [] – OSM-relevant keywords or tags
  - `google` – Google Maps link
  - `apple` – Apple Maps link
  - `ms` – Microsoft Maps link

### `media`

The `media` object holds a list of media elements such as images, thumbnails, info pages, or embeds. Each entry may carry metadata, usage permissions, and quality checks.

- `url` – Direct link to the media file or resource

- `meta` {} – Metadata about the content and file structure
  - `label` – Descriptive label or title for the media
  - `type` – Media type (e.g. `thumb`, `highres`, `info`, `embed`)
  - `mime` – MIME type of the file (e.g. `image/jpeg`, `text/html`)
  - `exif` {} – EXIF metadata block, if available (camera model, GPS, etc.)
  - `xmp` {} – XMP metadata block for creative tools or rights
  - `iptc` {} – IPTC metadata block, used for editorial information

- `usage` {} – Rights and reuse settings
  - `license` – License string (e.g. `CC-BY-SA 4.0`, `Public Domain`, `n/a`)
  - `contributor` – Name of contributor or rights holder
  - `embedding` – Reusability indicator (`allowed`, `forbidden`, `n/a`, "")

- `qa` {} – Quality assurance and status metadata
  - `status` – Current availability or review status (`active`, `broken`, `n/a`, etc.)
  - `added` – Timestamp when media was added (ISO 8601)
  - `checked` – Timestamp of the last validation (ISO 8601)

### `camera`

The `camera` object describes the technical and spatial properties of the recording device and its orientation.

- `view` {} – Field of view and projection information
  - `angle` – Horizontal field of view (in degrees)
  - `resolution` – Native resolution of the sphere or image
  - `projection` – Type of projection (e.g. `equirectangular`, `cubemap`, `flat-view`)

- `ptz` {} – Movement capabilities of the camera
  - `pan` – Supports horizontal rotation (true/false)
  - `tilt` – Supports vertical tilt (true/false)
  - `zoom` – Supports zoom (true/false)

- `type` – Type of recording (e.g. `photo`, `video`, `lidar`, `unknown`)
- `indoor` – Indicates if the scene is indoor (true/false)
- `audio` – Indicates if audio is present (true/false)
- `interval` – Interval between captures (e.g. `5s`, `live`, `unknown`)
- `timelapse` – Indicates if the recording is part of a timelapse (true/false)

- `heading` {} – Orientation angles of the view
  - `direction` – Compass direction (e.g. `NE`, `S`)
  - `pitch` – Vertical tilt (X-axis)
  - `yaw` – Horizontal direction (Y-axis)
  - `roll` – Lateral tilt (Z-axis)


