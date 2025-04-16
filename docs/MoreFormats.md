# SpOMM - Comparing Formats

## Introduction

The following overview highlights a growing ecosystem of JSON-based formats relevant to SpOMM – either as conceptual neighbors, as potential input sources, or as transformation targets. By understanding these related formats, SpOMM can serve as a semantic and structural bridge for integrating, converting, or federating data across 360° media, geospatial systems, live camera feeds, and immersive environments.

Each block categorizes related formats:
- **Reference formats** reflect existing 360° or geo-based data structures.
- **Target formats** represent typical output structures for apps and viewers.
- **Webcam formats** reflect real-time, API-based sources that could be mapped into SpOMM.

This modular orientation allows for bi-directional transformations and cross-domain interoperability.

## 1. Reference Formats (existing 360°/Geo/3D data formats)

| No. | Name                      | Typical Fields                           | Compatibility with SpOMM |
|-----|---------------------------|------------------------------------------|---------------------------|
| 1   | Google Street View JSON   | panoid, lat, lng, heading, pitch         | Very high                 |
| 2   | Mapillary V4              | compass_angle, captured_at, geometry     | High                      |
| 3   | Photosphere XMP           | GPano:* Tags                             | High (via XMP/EXIF)       |
| 4   | Three.js Cameras.json     | position, rotation, fov                  | Medium                    |
| 5   | Cesium / 3D Tiles         | bounding volume, transform               | Low                       |
| 6   | KML with ExtendedData     | <LookAt>, <Camera>, ExtendedData         | Medium (via tools)        |
| 7   | BIM/GeoBIM IFC-JSON       | Viewpoints, positions, metadata          | Low, but future-relevant  |
| 8   | GeoTIFF                   | Raster-based georeferenced imagery       | Medium                    |
| 9   | LiDAR-JSON                | Point cloud data, x/y/z/intensity        | Medium (for terrain)      |
| 10  | WebXR Viewer Config       | Scene config, camera, env mapping        | Medium                    |

## 2. Target Formats (transformation targets from SpOMM)

| No. | Name                      | Purpose / Use Case                                | Compatibility with SpOMM |
|-----|---------------------------|---------------------------------------------------|---------------------------|
| 1   | WanderVR JSON             | Compatible with WanderVR panoramas                | Very high                 |
| 2   | GeoJSON                   | Maps / GIS applications, point data               | High                      |
| 3   | OSM Custom Layer          | POI-based display in OSM                          | High                      |
| 4   | BIB-App JSON              | Library-like presentation, content discovery      | Medium                    |
| 5   | Static Website Embed      | JSON → viewer component for simple display        | High                      |
| 6   | GLTF / Scene Graph JSON   | Integration into virtual 3D environments          | Low to medium             |
| 7   | CSV/TSV Flat Export       | Statistics, tables, Excel                         | High (flattened)          |

## 3. Webcam Formats & Interfaces

| No. | Name                      | Description / Content                             | Compatibility with SpOMM |
|-----|---------------------------|---------------------------------------------------|---------------------------|
| 1   | Webcam Travel API         | JSON API with location, image, player metadata    | High                      |
| 2   | Windy.com Webcam API      | JSON with location, view, player, status          | High                      |
| 3   | OpenWeatherMap Cams       | JSON with stream metadata, image + geo            | High (for livecams)       |
| 4   | IPTC Streaming Metadata   | XML-based model for live feeds                    | Medium                    |
| 5   | ONVIF (via JSON proxy)    | Industry standard for IP cameras (original XML)   | Medium                    |
| 6   | FFmpeg/RTSP-Probe JSON    | Structured info from RTSP streams                 | Low                       |
| 7   | W3C MediaStream (WebRTC)  | Web standard for media tracks (JS/DOM)            | Low (browser only)        |



