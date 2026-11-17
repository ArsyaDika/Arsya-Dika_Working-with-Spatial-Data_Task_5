# Polygon Geoprocessing with GeoPandas

How do you turn a raw hazard-class polygon layer into analysis-ready geometry? This notebook walks through nine core geoprocessing steps with GeoPandas on hazard polygons in Bandung, from reprojection and buffering to dissolve, union, area calculation and filtering, with every step **exported as GeoJSON**.

Task 5 of the WebGIS Developer bootcamp (Working with Spatial Data).

## Workflow

| Step | Operation | Output |
|---|---|---|
| 1 | Fetch polygons from the MAPID API and display them in Folium | – |
| 2 | Set CRS EPSG:4326, reproject to EPSG:3857 | – |
| 3 | 100 m buffer | `buffered_layer_100meter_new.geojson` |
| 4 | Simplify (5 m tolerance) | `Simplify_buffered_layer_100meter_new.geojson` |
| 5 | Clip to the study area bounding box | `clipped_layer_new.geojson` |
| 6 | Dissolve by `KELAS` | `dissolved_layer_per_kelas_new.geojson` |
| 7 | Union of all polygons | `hasil_union_new.geojson` |
| 8 | Calculate area (km²) in UTM 48S | `union_with_area_newest.geojson` |
| 9 | Filter `KELAS == "TINGGI"` | `filtered_tinggi_new.geojson` |

## Running

```bash
pip install geopandas folium requests
export MAPID_API_KEY=...        # PowerShell: $env:MAPID_API_KEY = "..."
jupyter notebook "Task day 5.ipynb"
```

The API key is read from an environment variable and is no longer written in the notebook.

## Notes on fixes

- **API key removed** from the notebook.
- **Buffer was not saved.** The result of `buffer(100)` was not assigned, so the "buffered" file held the original polygons. Fixed.
- **Simplify was not saved.** The result of `simplify` was also unused, so the "Simplify" file was identical to the buffer file. Fixed, with the tolerance in meters.
- **Wrong area unit.** `AREA_KM2` was previously calculated in EPSG:4326 (degrees), giving values around 1e-10. It is now calculated in UTM zone 48S (EPSG:32748).
- Clip now uses `gpd.clip`, and absolute Windows paths were replaced with relative paths.

The fixes were tested on the `filtered_tinggi_new.geojson` data. **The GeoJSON files in the repo are still from the old version.** Rerun the notebook with an API key to refresh them.

## Tools

Python · GeoPandas · Shapely · Folium · MAPID API

## Author

**Arsya Dika** · [GitHub](https://github.com/ArsyaDika)

------------------

# Geoprocessing Poligon dengan GeoPandas

Rangkaian operasi geoprocessing dasar pada poligon kelas kerawanan di Bandung, dari data API MAPID hingga ekspor GeoJSON: reproject, buffer, simplify, clip, dissolve, union, hitung luas, dan filter atribut.

Tugas 5 bootcamp WebGIS Developer (Working with Spatial Data).

## Alur

| Langkah | Operasi | Output |
|---|---|---|
| 1 | Ambil poligon dari API MAPID, tampilkan di Folium | – |
| 2 | Set CRS EPSG:4326, reproject ke EPSG:3857 | – |
| 3 | Buffer 100 m | `buffered_layer_100meter_new.geojson` |
| 4 | Simplify (toleransi 5 m) | `Simplify_buffered_layer_100meter_new.geojson` |
| 5 | Clip ke bounding box area studi | `clipped_layer_new.geojson` |
| 6 | Dissolve per `KELAS` | `dissolved_layer_per_kelas_new.geojson` |
| 7 | Union seluruh poligon | `hasil_union_new.geojson` |
| 8 | Hitung luas (km²) di UTM 48S | `union_with_area_newest.geojson` |
| 9 | Filter `KELAS == "TINGGI"` | `filtered_tinggi_new.geojson` |

## Menjalankan

```bash
pip install geopandas folium requests
export MAPID_API_KEY=...        # PowerShell: $env:MAPID_API_KEY = "..."
jupyter notebook "Task day 5.ipynb"
```

API key dibaca dari environment variable, tidak lagi ditulis di notebook.

## Catatan perbaikan

- **API key dihapus** dari notebook.
- **Buffer tidak tersimpan.** Hasil `buffer(100)` sebelumnya tidak di-assign, sehingga file "buffered" berisi poligon asli. Sudah diperbaiki.
- **Simplify tidak tersimpan.** Hasil `simplify` sebelumnya juga tidak dipakai, sehingga file "Simplify" sama dengan file buffer. Sudah diperbaiki, dengan toleransi dalam meter.
- **Luas salah satuan.** `AREA_KM2` sebelumnya dihitung di EPSG:4326 (derajat), sehingga nilainya sekitar 1e-10. Sekarang dihitung di UTM zona 48S (EPSG:32748).
- Clip sekarang memakai `gpd.clip`, dan path Windows absolut diganti path relatif.

Perbaikan sudah diuji pada data `filtered_tinggi_new.geojson`. **File GeoJSON di repo masih hasil versi lama.** Jalankan ulang notebook dengan API key untuk memperbaruinya.

## Tools

Python · GeoPandas · Shapely · Folium · MAPID API

## Penulis

**Arsya Dika** · [GitHub](https://github.com/ArsyaDika)
